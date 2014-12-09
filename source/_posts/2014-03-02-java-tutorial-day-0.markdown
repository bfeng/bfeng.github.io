---
layout: post
title: "Java Tutorial Day 0"
date: 2014-03-02 01:13:25 -0500
comments: true
categories: [java, tutorial]
---

## Introduction
Java is a computer programming language, which was invented by [Sun Microsystems](http://en.wikipedia.org/wiki/Sun_Microsystems) and now has been merged into [Oracle Corporation](http://en.wikipedia.org/wiki/Oracle_Corporation). Java was originally designed by a Canadian computer scientist [James Gosling](http://en.wikipedia.org/wiki/James_Gosling) when he worked at Sun Microsystems.

<!--more-->

Java is a distinguished language due to many features that other languages do not have. It is a static language but it does not run by the native code, like C or C++.
It is interpreted at runtime but it is not dynamic typed like Perl, Python, PHP, etc. It is compiled into a platform neutral byte code, which is then interpreted by the Java Virtual Machine (JVM).

	+-------+    +--------+    +-----+
	| .java | -> | .class | -> | JVM |
	+-------+    +--------+    +-----+

## Setup JDK
JDK, which is short of Java Development Kit, is a set of tools used to develop Java programs. Before one can compile and run a Java program, the JDK should be installed. Here there are two commands users should get familiar:

1. javac

	`javac` is a program which compiles the Java source code into byte code.

2. java

	`java` is a program which start up a JVM and run Java byte code.

So the above figure should be like this:

	+-------+             +--------+
	| .java | -> javac -> | .class | -> java
	+-------+             +--------+

### Download and Installation

There are many distributions of JDK. The two representatives of them are from Oracle or OpenJDK project. They are free to download and use. For the convince, I assume the JDK is version 7 from Oracle in the following.

### Setup System Environment Variables

This questions and answers give out a clear definition and usage about environment variables. Please refer them [here](http://superuser.com/questions/284342/what-are-path-and-other-environment-variables-and-how-can-i-set-or-use-them).

For Windows users with GUI available, this [post](http://www.computerhope.com/issues/ch000549.htm) is more friendly.

Add `JAVA_HOME` variable. `JAVA_HOME` variable is used by many famous java programs such as `maven`, `ant`, `hadoop`, etc.

	JAVA_HOME=< the folder path where you installed JDK >

Add the `< the folder path where you installed JDK >\bin` to your existing `PATH`. Please note that do not replace your `PATH` variable in case you will not run other programs.

## Write your first Java program

Here is the first java program, which does nothing than print a line `Hello, world!` in the console.

    public class HelloWorldApp {
	    public static void main(String[] args) {
	        System.out.println("Hello, world!");
	    }
	}

The following are the steps of building and run this program:

1. Save the above code into a file named `HelloWorldApp.java`
2. Open your console and go to the folder contains `HelloWorldApp.java`
3. Compile the code by `javac HelloWorldApp.java`, then if successful, there should be a file named `HelloWorldApp.class`
4. Run the code by `java HelloWorldApp`
5. The program should print `Hello, world!` on your screen.

## One step further

In the above code, `HelloWorldApp` is the class name. It should also be the file name, since it is the top level `public` class in the file. The method `public static void main` is the entry method for a Java program and the method arguments is `String[] args`, in which `String[]` refers the type as an array of `String` and `args` is the variable name. This arguments could be given from the command line when starting the program, like `java HelloWorldApp XXX`.

So let's change the source code like this:

    public class HelloWorldApp {
	    public static void main(String[] args) {
	        System.out.println("Hello, " + args[0]);
	    }
	}

Repeat the above steps of building this program: `javac HelloWorldApp.java`.
Run the program: `java HelloWorldApp XXX`. Then, the program should print `Hello, XXX` on your screen.

## Practice

Write your third program which could print a figure in the console like the following:


	         *
		    ***
		   *****
		  *******
		 *********
		***********
	   *************
	  ***************
	 *****************
	*******************
