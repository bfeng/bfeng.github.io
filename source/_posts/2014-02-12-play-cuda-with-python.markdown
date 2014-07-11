---
layout: post
title: "Play Cuda with Python"
date: 2014-02-12 11:13:02 -0500
comments: true
categories: [fun, GPU]
---

##Introduction
This article is to introduce you PyCUDA, which is a python framework allows you write [NVidia](http://www.nvdia.com)'s GPU program in a pythonic way. This framework is consisted of two major parts. The first part is a cuda source code compiler, which compiles the embedded cuda code in python at runtime. The second part is to do the computing by leveraging the [numpy](http://www.numpy.org), which is also a famous python library for scientific computing.

##Start with your first Pycuda program
This [website](http://documen.tician.de/pycuda/) gives out the PyCUDA's [documentation](http://documen.tician.de/pycuda/).

Here is an example from the above.

{% codeblock lang:python %}

import pycuda.autoinit
import pycuda.driver as drv
import numpy

from pycuda.compiler import SourceModule
mod = SourceModule("""
	__global__ void multiply_them(float *dest, float *a, float *b)
	{
	  const int i = threadIdx.x;
	  dest[i] = a[i] * b[i];
	}
	""")

multiply_them = mod.get_function("multiply_them")

a = numpy.random.randn(400).astype(numpy.float32)
b = numpy.random.randn(400).astype(numpy.float32)

dest = numpy.zeros_like(a)
multiply_them(
drv.Out(dest), drv.In(a), drv.In(b),
block=(400,1,1), grid=(1,1))

print dest-a*b

{% endcodeblock %}

In this example, the `SourceModule` is used to create a python `Module` from the cuda source code. This involves the Just-in-time compilation. Then, `get_function` is used to extract the function from that compiled module, hence the following program can directly call the function like a normal python function.

`pycuda.driver` helps to copy-in and copy-out the data between the main memory and the GPU memory. `drv.Out` function wraps the variable, which is used in the main memory, in contrast if the variable will be used in GPU memory, use `drv.In`. Other parameters, like `block` and `grid` are the same as used in the normal c cuda program. This blog post gives nice explanation about them: [http://www.resultsovercoffee.com/2011/02/cuda-blocks-and-grids.html](http://www.resultsovercoffee.com/2011/02/cuda-blocks-and-grids.html).

##Conclusion
With the help of the some libraries, such as [numpy](http://www.numpy.org), [scipy](http://www.scipy.org) and etc., PyCuda gives us another handful method to do the scientific computing. By leveraging the GPU computing power, we can not only process and analyze data sets but also do it efficiently.
