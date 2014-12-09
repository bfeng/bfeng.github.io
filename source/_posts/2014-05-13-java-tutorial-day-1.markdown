---
layout: post
title: "Java Tutorial Day 1"
date: 2014-05-13 17:19:23 -0500
comments: true
categories: [java, tutorial]
---

Introduction
------------

Primitive data types are the basic data types used in Java. With primitive data types and arrays of them, many questions could be solved now. This post will cover what the primitive data types are and usage of the 1-d array of them. The control flow helps to build more complex program execution.

<!--more-->

Primitive data types
--------------------

Java is a static typed language as we described on [Day 0](2014/03/java-tutorial-day-0.html). This  feature requires the compiler knows the variable data types before usage. In practice, programmers have to declare which type the variable is.

In Java, there are eight data types, called primitive data types,  because the
usage of them is different from other Java object variables and all other Java
classes are built by using them.

The table below shows these eight primitive data types and their default values. Default values are the values when those variables are declared. The default values prevent the variables are not allocated memory space.

<table>
	<caption>Table: Default values for the primitive data types</caption>
	<tr>
		<th>Data Types</th>
		<th>Default Values (for fields)</th>
	</tr>
	<tr>
		<td>byte</td>
		<td>0</td>
	</tr>
	<tr>
		<td>short</td>
		<td>0</td>
	</tr>
	<tr>
		<td>int</td>
		<td>0</td>
	</tr>
	<tr>
		<td>long</td>
		<td>0L</td>
	</tr>
	<tr>
		<td>float</td>
		<td>0.0f</td>
	</tr>
	<tr>
		<td>double</td>
		<td>0.0d</td>
	</tr>
	<tr>
		<td>char</td>
		<td>'\u0000'</td>
	</tr>
	<tr>
		<td>boolean</td>
		<td>false</td>
	</tr>
</table>
Source: http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html

Please refer [this page](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) for more details of what these primitive data types are.

Array and java specialty
------------------------

### Basic usage
Using primitive data types are not enough to build many variables. `Array` is used to declare as many the same type of variables as programmers want. An `Array` is a structure, which contains a serial of the same variables. Programs can access each element in the array by specifying a fixed `index`.

    public class ArrayDemo1 {
	    public static void main(String[] args) {
	        int[] arr1;
			arr1 = new int[2];
			System.out.println(arr1[0]);
			System.out.println(arr1[1]);

			int[] arr2 = {1, 2};
			System.out.println(arr2[0]);
			System.out.println(arr2[1]);
	    }
	}

The example above shows two kinds of declaration of arrays. `int[] arr1` first declares  `arr1` is an array of integers. `arr1 = new int[2]` allocates the memory for two integers. Since we don't specify the initial values for each element, the element values in `arr1` should be `0` by default. `int[] arr2 = {1, 2}` declares variable name, allocates memory for two integers and gives out the initial values of the two integers: `1` and `2`.

### Array length
Java array has a special property named `length`, which is quite useful to get the length of this array. The usage is quite simple as `arr1.length` and `arr2.length` for the variables in the above example.

Control flow statements
-----------------------

All the statements are generally executed from top to bottom and line by line. Control flow statements are the statements can break the normal work flow of the execution. Programmers can break, branch and set conditions to control the execution of programs. More specifically, the following list shows the basic control syntax in Java.

- if else
	- else if
- switch case
- for
- while
- do while
- break
- continue
- return

More examples and explanations could be found here: [http://docs.oracle.com/javase/tutorial/java/nutsandbolts/flow.html](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/flow.html)

Practice
--------
A prime number is a natural number greater than 1 that has no positive divisor other than 1 and itself. ([Wikipedia](http://en.wikipedia.org/wiki/Prime_number))

Please write a program to produce all the primes less than 1000. The output should be like this:

	2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569, 571, 577, 587, 593, 599, 601, 607, 613, 617, 619, 631, 641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701, 709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773, 787, 797, 809, 811, 821, 823, 827, 829, 839, 853, 857, 859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937, 941, 947, 953, 967, 971, 977, 983, 991, 997
