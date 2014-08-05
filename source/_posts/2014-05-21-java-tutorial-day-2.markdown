---
layout: post
title: "Java Tutorial Day 2"
date: 2014-05-21 21:52:11 -0500
comments: true
categories: [java, tutorial]
---

## Introduction to Console I/O ##

I/O, which is short for **Input and Output**, is an important part in any programming language. So is in Java. Today we only refer the console I/O as the standard input and output in a console, which is also the simplest way how users interact with a program.

## Input and Output Usage ##
When a program is running in the console, it often requires users to input some characters, such as parameters, records and text. The program may also print some characters to the console in order to notify the information to users.

The output operation often involves the the array of characters and other variable types conversion, however the output operation in Java is simplified by providing many methods, so that programmers don't need to worry too much in output. When programmers compose the code to handle the input, it is often more complicated.

`System` class provides the standard input and output facilities, which are described in the following.


### Input Usage ###

The console input is Java is encapsulated in `System.in`, which is a `static InputStream`. A input stream could be imaged like a stream of bytes, from which program can read bytes. So from `System.in`, programs can read users' input from the console.

For the conversion reason, consoles may only accept characters, which should be converted into other types, such as integers. However, due to the consideration that [all input is evil](http://www.microsoft.com/mspress/books/sampchap/5957.aspx), programmers need to validate all the input data.

{% codeblock lang:java %}

import java.io.InputStream;
import java.io.IOException;

public class ConsoleEcho1 {
  public static void main(String[] args) throws IOException {
    InputStream in = System.in;
    int result = 0;
    while(true) {
      byte[] buffer = new byte[64];
      result = in.read(buffer);
      if(result == 0 || result == -1
          || (result == 1 && buffer[0] == '\n'))
        break;
      System.out.print("> " + new String(buffer));
    }
  }
}

{% endcodeblock %}

The above code gives an example of how to read byte array from `System.in`, how to covert the byte array into `String` and print on the console by `System.out`. `buffer` is an array of byte, which is used to store users' input content. In the line `System.out.print`, `new String` is used to convert the byte array into a string, so that the program can print the content into console.

The following gives a more sophisticated example, which uses `InputStreamReader` and `BufferedReader` to wrap the input stream. The reason is documented in the Java API documentations:

> In general, each read request made of a Reader causes a corresponding read request to be made of the underlying character or byte stream. It is therefore advisable to wrap a BufferedReader around any Reader whose read() operations may be costly, such as FileReaders and InputStreamReaders.

{% codeblock lang:java %}

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.IOException;

public class ConsoleEcho2 {
  public static void main(String[] args) throws IOException {
    BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

    String line;
    while(true) {
      line = reader.readLine();
      if(line.isEmpty())
        break;
      System.out.println("> " + line);
    }
    reader.close();
  }
}

{% endcodeblock %}


### Output Usage ###

The output operations is less complicated than the input. `System.out` is actually `static final PrintStream`, which provides many format and print methods. All these could be referred from the official Java API docs: [http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html](http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html).

## Practice ##

Please design and implement a program, which allows users to input a positive number each line. After users hit enter key, the program prints out all users' input in an ascending order.

For example:

    > Enter a number:
    > 3
    > Sorted: 3
    > Enter a number:
    > 5
    > Sorted: 3, 5
    > Enter a number:
    > 1
    > Sorted: 1, 3, 5
    > Enter a number:
    > 21
    > Sorted: 1, 3, 5, 21
    > Enter a number:
    > 20
    > Sorted: 1, 3, 5, 20, 21

