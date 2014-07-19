---
layout: post
title: "Image processing with PyCuda"
date: 2014-07-09 14:57:20 -0500
comments: true
categories: [GPU]
---


## Build Cuda source module with Python

{% codeblock lang:python %}

module = SourceModule("""
    __global__ void histograms(float * hist_rgb, unsigned char * pix, int total)
    {
      int idx = threadIdx.x + blockDim.x * blockIdx.x;
      if(idx >= total) return;

      __shared__ float local_hist[256];

      if(threadIdx.x < 256)
        local_hist[threadIdx.x] = 0;

      __syncthreads();

      int pixel = pix[idx];
      atomicAdd((float *)&local_hist[pixel], 256.0/total);

      if(threadIdx.x < 256)
        atomicAdd((float *)&hist_rgb[threadIdx.x], local_hist[threadIdx.x]);
    }
    __global__ void enhance(unsigned char * pix, float * hist_rgb, int total)
    {
      int idx = threadIdx.x + blockDim.x * blockIdx.x;
      if(idx >= total) return;
      int pixel = pix[idx];
      pix[idx] = (int)(hist_rgb[pixel]);
    }
    """)

histograms 	= module.get_function("histograms")
enhance 	= module.get_function("enhance")

{% endcodeblock %}


## Use within Python code

{% codeblock lang:python %}

THREADS_PER_BLOCK = 512

def gpu_enhanceImage(pic):
    # convert to array
    pix = numpy.array(pic)
    width, height = pic.size
    total = width*height

    # ------------------------------------------------
    # accelerate the following part as much as possible using GPU
    #
    # compute histograms for RGB components separately
    # the value range for each pixel is [0,255]
    hist_rgb = [0]*256

    hist_rgb_buffer = numpy.float32(hist_rgb)
    pix = pix.astype(numpy.uint8)

    hist_rgb_gpu = cuda.mem_alloc(hist_rgb_buffer.nbytes)
    pix_gpu = cuda.mem_alloc(pix.nbytes)

    cuda.memcpy_htod(hist_rgb_gpu, hist_rgb_buffer)
    cuda.memcpy_htod(pix_gpu, pix)

    histograms(hist_rgb_gpu, pix_gpu,
         numpy.int32(total),
         block=(THREADS_PER_BLOCK, 1, 1),
         grid=((total + THREADS_PER_BLOCK - 1)/THREADS_PER_BLOCK,1))

    cuda.memcpy_dtoh(hist_rgb_buffer, hist_rgb_gpu)

    hist_rgb = hist_rgb_buffer

    # compute the accumulative histograms
    for intensity in range(1,256):
      temp = hist_rgb[intensity] + hist_rgb[intensity-1]
      # take care of rounding error
      temp = min(temp, 256 - 1)
      hist_rgb[intensity] = temp

    # enhance the picture according to the inversed histgram
    cuda.memcpy_htod(hist_rgb_gpu, hist_rgb)

    enhance(pix_gpu, hist_rgb_gpu,
      numpy.int32(total),
      block=(THREADS_PER_BLOCK, 1, 1),
      grid=((total + THREADS_PER_BLOCK - 1)/THREADS_PER_BLOCK, 1))

    cuda.memcpy_dtoh(pix, pix_gpu)
    # -----------------------------------------------

    # save the picture
    pic = Image.fromarray(pix)
    return pic

{% endcodeblock %}

* For each image, the function `enhanceImage` does three steps enhancement:
	* calculate the histogram of 256 color used in the image
	* accumulate the histogram calculated in step one
	* assign each pixel of the image according to the inversed histogram
* In step one and three, we could parallelize the program in GPU. Step two is a simple 256 iteration loop which should be pretty fast on CPU and there is data dependency, therefore we’d better do it in CPU.
* To do the acceleration in GPU, my implementation uses one thread per pixel of the image. Each thread reads the pixel out and adds its value to the appropriated position in the histogram.
	* Threads in the same block can share the local memory which is faster than the global memory, so in each block the threads are using the shared memory to calculate the histogram.
	* After the local shared histogram is calculated out, the first 256 threads add the value of the local histogram to the global one.
* The data movement between CPU and GPU via Cuda APIs:
	* `cudaMelloc` can allocate the space in GPU’s display memory
	* `cudaMellocpy` can copy the data from the main memory to the display memory and vice versa.
	* `cudaFree` can release the memory space used in GPU
* Optimization:
	* Use shared memory as much as possible. Because the shared memory in a block is 100x faster than the global memory.
	* In my implementation, `atomicAdd` is used, because the histogram might be accessed by more than one thread. However, this could be a performance bottleneck of the overall GPU program. So I tried to use a large global memory to avoid the conflicts, but the memory was becoming the new performance bottleneck. To keep the program neat, I still decided to use `atomicAdd`.
