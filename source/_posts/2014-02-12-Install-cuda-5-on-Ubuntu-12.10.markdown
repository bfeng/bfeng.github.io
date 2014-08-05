---
layout: post
title: Install cuda 5 on Ubuntu 12.10
date: 2014-02-12 20:50:11 UTC
updated: 2014-02-12 20:50:11 UTC
comments: true
categories: GPU
---

 By default the cuda is not working on Ubuntu. You may not want to crash your system.&nbsp;Please do exactly follow the instruction step by step. If you are brave enough like me or you are still OK to handle the problem properly even if only the Linux kernel and SSH are working fine, there is no need to backup your system at first.<br /><ol><li>Go to the CUDA official website and download the Getting started guide for your system</li><ol><li>https://developer.nvidia.com/cuda-downloads</li></ol><li>Read the installation guide from Cuda official website</li><ol><li>install all the&nbsp;prerequisites for your system&nbsp;</li></ol><li>Download Cuda 5 installation</li><ol><li>typically it's a cuda5*.run file</li></ol><li>Remove the existing nvidia driver from Ubuntu official reposistory</li><ol><li>$ sudo apt-get remove --purge nvidia*</li></ol><li>Change tty to anyone without gui:</li><ol><li>eg. ctrl + alt + F1</li></ol><li>Stop the default dm:</li><ol><li>eg. $ sudo service lightdm stop</li></ol><li>Install gcc and change the default gcc to gcc-4.4:</li><ol><li>sudo apt-get install gcc gcc-4.4</li><li>sudo update-alternatives --remove-all gcc ( if you have previous configuration )</li><li>sudo update-alternatives --config gcc&nbsp;( if you have previous configuration )</li><li>sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.4 20</li><li>gcc --version</li><ol><li>gcc 4.4.* or something like that should be printed out</li></ol></ol><li>Run installation:</li><ol><li>chmod +x &lt;cuda&gt;.run</li><li>sudo ./&lt;cuda&gt;.run</li></ol></ol>
