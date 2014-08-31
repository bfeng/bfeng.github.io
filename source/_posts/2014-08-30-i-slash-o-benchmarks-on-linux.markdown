---
layout: post
title: "I/O benchmarks on Linux"
date: 2014-08-30 20:39:38 -0500
comments: true
categories: [benchmark, cluster, Linux]
---


Benchmarks are useful tools, which help to understand system performance in a simple manner. This is because that sometimes applications are too complicated to identify which part is the bottleneck. Another reason is the security. When the data usage or application algorithms are private, profiling these applications are not allowed. For some reasons, benchmarks can represent the performance-critical parts in applications.

There are many benchmarks under Linux platform, some of which are also applicable for any POSIX compliant systems.


## dd

`dd` command is to copy files from destination to target place. It invloves many aspects of copying.

[This](http://www.computerhope.com/unix/dd.htm) is a post, showing the description of this command and examples of usage.

## iozone

`iozone` is a file system benchmark, which can measure many aspects of performance for file systems.
The official documentation is the best to learn `iozone`. It can be downloaded from its offical website: http://www.iozone.org/


*To be continued...*
