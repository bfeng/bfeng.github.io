---
layout: post
title: "Cracking Java Interview Questions"
date: 2014-02-27 20:56:52 -0500
comments: true
categories: [interview, java]
---

This questions are mainly from internet.

<!--more-->

1. What do you know about Java?

	Java is nothing but a high-level programming language from the Sun Microsystem, and now from Oracle Inc. It is released in the year 1995 and runs on multiple platforms like Linux, Windows, Mac and other variations of UNIX. [James Gosling](http://en.wikipedia.org/wiki/James_Gosling) is known as the father of Java programming language.

2. Can you differentiate between J2SDK 1.5 and J2SDK 5.0?

	There is no difference between J2SDK 1.5 and J2SDK 5.0. Sun Microsystems has just re-branded the versions. Since java 1.6, Java 6 and Java 7 are called for the version of 1.6 and 1.7, respectively.

3. Can you name a few platforms that support Java?

	Yes, Java is supported by Windows, Mac as well as UNIX/Linux like Ubuntu, Red Hat, Sun Solaris, etc..

4. Could you tell me why Java is called Architectural Neutral?

	The main reason is because the compiler creates an architecture neutral object file format. This makes the compiled code to be executable on different other processors.

5. What is the difference between an Interface and an Abstract class?

	An abstract class can have instance methods that implement a default behavior. An Interface can only declare constants and instance methods, but cannot implement default behavior and all methods are implicitly abstract. An interface has all public members and no implementation. An abstract class is a class which may have the usual flavors of class members (`private`, `protected`, etc.), but has some abstract methods.

6. What is the purpose of garbage collection in Java, and when is it used?

	The purpose of garbage collection is to identify and discard objects that are no longer needed by a program so that their resources can be reclaimed and reused. A Java object is subject to garbage collection when it becomes unreachable to the program in which it is used.

7. How do you implement a thread in Java?

	In Java, there is `Thread` class that can be extended and `Runnable` interface that can be implemented. Since Java 1.6, there is a new interface `Callable`, which is also used as a thread interface but usually used as a concurrency task.

8. Is the Java method called by reference or by value?

	Java does manipulate objects by reference, and all object variables are references. However, Java doesn't pass method arguments by reference; it passes them by value.

9. What is the difference between a constructor and a method?

	A `final` class can't be extended ie., final class may not be extended. A final method can't be overridden when its class is inherited. You can't change value of a final variable (is a constant).

10. Difference between `Vector` and `ArrayList`?

	`Vector` is synchronized whereas `ArrayList` is not.

11. What is `static` in Java? And `final`?

	`static` means one per class, not one for each object no matter how many instance of a class might exist. This means that you can use them without creating an instance of a class. Static methods are implicitly final, because overriding is done based on the type of the object, and static methods are attached to a class, not an object. A static method in a super class can be shadowed by another static method in a subclass, as long as the original method was not declared final. However, you can't override a static method with a non-static method. In other words, you can't change a static method into an instance method in a subclass.

12. What are the different ways you can use `static`?

	`static` can be used in four ways: static variables, static methods, static classes and it can be used across a block of code in any class in order to indicate code that runs when a virtual machine starts and before the instances are created.

13. Do you think all property of Immutable Object needs to be final?

	Not compulsory as we can easily achieve the same by making member as non-final but private and not changing them except in the constructor. Also, avoid providing setter methods for them. If it is a mutable object, then prevent leaking any reference for that member.

14. Can you brief me about Singleton Class?

	It basically controls object creation, restricting the number to one while allowing the flexibility to create objects if the scenario changes.
	Singleton is one of the design methods. It guarantees that there is only one instance at runtime.

15. In Java, what is the default value of float and double?

	Default value of Float is `0.0f` while `0.0d` for Double.

16. Can you explain type erasure?

	It is nothing but a JVM phenomenon, which means that the runtime has no idea about the types of generic objects like `List<Integer>`.

17. Explain Dot Operator.

	It is used to access the instance variables and methods of class objects. Also, we can use it to access classes and sub-packages from a package.

18. What do you mean by Serialization in Java?

	Well, serialization is nothing but a process of transforming objects into a stream of bytes. While deserialization is the opposite operation, which transforms the stream of bytes into an instance.

19. Can you tell me the reason why `String` class is considered immutable?

	It is because to avoid change in `String` object once it is created. As String is immutable, you can share it between different threads in a safe way. This is quite crucial in multithreaded programming.

20. Can you quickly brief about `Map`, `HashMap`, `HashTable`, and `TreeMap`?

	`Map` is an interface, and `HashMap` is a class that implements a `Map`. It is not synchronized and supports null values and keys `HashTable` is a synchronized version of `HashMap`. `TreeMap` is similar to `HashMap` but uses `Tree` to implement `Map`.

21. Do you think not overriding `hashcode()` method has any performance implication?

	A weak `hashcode` function will result into frequent collision in `HashMap`, which will at the end increase the time to add an object within `HashMap`.

22. Can you explain when and why Getters and Setters important?

	We can put setters and getters within interfaces, which can hide implementation details. This allows us to make member variables public in Java. Getters and Setters are important to encapsulate Java class, which hide the direct accesses to member fields. This design is called [Plain Old Java Object (POJO)](http://en.wikipedia.org/wiki/Plain_Old_Java_Object).

23. Is it possible to import same package or class twice? Will the JVM load the package twice at runtime?

	It is possible to import the same package or class more than one time. Also, it won’t have any effect on compiler or JVM. JVM will load the class for one time only, irrespective of the number of times you import the same class.

24. What is difference between Throw and Throws?

	While Throw is used to trigger an exception, Throws is used in the declaration of exception. It is not possible to handle checked exception without Throws.

25. What is the significance of the order in which catch statements for `FileNotFoundException` and `IOException` are written?

	It is crucial to consider the order as the `FileNoFoundException` is inherited from the `IOException`. Therefore, it is important that exception's subclasses caught first.

26. Can throw some light on Yielding and Sleeping?

	When any task invokes its `yield()` method, it will return to the ready state. Whenever a task invokes `sleep()` method, it will return to the wait state.

27. Why you should use Vector class?

	It provides the capability to implement a growable array of objects. It is quite useful when we don’t know the exact size of the array.

28. Can you tell me the number of bits used to represent Unicode, ASCII, UTF-16, and UTF-8 characters?

	For Unicode 16 bits and ASCII needs 7 bits. However, ASCII is usually represented as 8 bits. UTF-8 presents characters through 8, 16 and 18 bit pattern. UTF-16 will require 16-bit and larger bit patterns.

29. What is Applets?

	A small program based on Java that can be transformed from one computer to another using the Applet Viewer or web browser.

30. What is the use of Locale?

	Locale is an object containing geographical, cultural and political information which helps in using custom codes and conventions of specific country or region for writing applications in that language.

31. What is the use of Java Package?

	Java Package is useful for organizing projects containing multiple modules and protecting them from unauthorized access.

32. While working in the JVM, do we need to import java.lang package?

	No, by default it is loaded in the JVM.

33. Can Applets communicate with each other?

	Yes, they can communicate via shared static variables even if they belong to same of different classes.

34. Can a .java file support more than one java classes?

	Yes, it can support more than one Java classes in a condition where one of them is a public class.

35. MAIN, NEXT, DELETE & EXIT, which of these is a keyword in Java?

	None of these is a keyword in Java

36. How to handle errors while writing or accessing Stored Procedures.

	Store Procedure itself returns the error codes if any but, in case if it fails to do so, we can resort to catching SQL Exception.

37. From `ArrayList` and `LinkedList`, which one helps to perform an indexed search in a list of objects?

	`ArrayList`

38. What is the use of `File` Class?

	It helps in accessing files and directories of a local system. Note that both files and directories are represented by `File` class.

39. Does Java support Default arguments?

	No, it does not support.

40. Describe life cycle of Applets?

	Initialization, Starting, Stopping, Destroying & Painting. Applets are not so useful nowadays. As to the rich client applications in the web world, [HTML5](http://en.wikipedia.org/wiki/Html5) is the future.

41. What is the method applied to load an image in Applet class?

	It’s `getImage`.
