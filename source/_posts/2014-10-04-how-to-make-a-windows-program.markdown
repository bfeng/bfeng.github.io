---
layout: post
title: "How to Make a Windows Program"
date: 2014-10-04 16:57:38 -0500
comments: true
categories: [tutorial, windows, c]
---

## Introduction

This is a tutorial of how to make a Windows program. It is just more like a hello-world program but implemented in Windows C. Windows C inherits from ANSI C but has many different features, including special data structures, system functions and even design patterns.

This tutorial introduces the basic elements of Windows programs, such as main entry functions, window class registration, window class creation, control procedure, message loop and so on. Please note that the code in this tutorial is *not* for production use.

## How to setup compilers

The first step to write a real application is to setup its compilers. `MinGW` is an open source compiler suite, including `GCC for C, C++, Fortran, Java, and Ada`, `binutils`, `Windows API, runtime`, and `make`. The following steps guide how to setup `MinGW` on Windows. In this tutorial, we use `MinGW-gcc` as the compiler for C and its runtime library to run the application on Windows.

### Download and install `MinGW`

The official site of `MinGW` gives a premium guide of how to: http://www.mingw.org/wiki/HOWTO_Install_the_MinGW_GCC_Compiler_Suite.

The summary of this guide are:

1. download a suitable installer
2. extract and run the installer
3. setup `MinGW\bin` in the `PATH` environment variable

To verify your installation, just open a console and test some commands, such as `gcc` and `make`.

## The basic elements of a Windows application

### The main function

The following is the main function example of Windows applications. Instead of using the `main` for ANSI C applications, the main function is defined as `WinMain` under Windows.

{% codeblock lang:c %}
#include <windows.h>

/* Main function */
int APIENTRY WinMain(HINSTANCE hInstance,
                     HINSTANCE hPrevInstance,
                     LPSTR     lpCmdLine,
                     int       nCmdShow)
{
}
{% endcodeblock %}

For Windows applications, each instance of an application is controlled by a `handle`, the structure of which is defined as `HINSTANCE`. So int `WinMain`, the first two arguments are instance handles of applications. `hInstance` is the handle to the current instance of the application. `hPrevInsance` is the handle to previous instance of the applications. However, the *previous* here is varied by cases. In addition to the third and fourth arguments, please refer to the official documentation of this function [here][1].

### Register a window class

A Windows application composites of a class of windows. Before creating a visible application under graphic environment, a new window class should be defined and registered in the system. The data structure `WNDCLASSEX` used with `RegisterClassEx` can define and register the window class. Below is an example of a window class in main function.

{% codeblock lang:c %}
#include <windows.h>

const char className[] = "MyWindowClass";

/* Main function */
int APIENTRY WinMain(HINSTANCE hInstance,
                     HINSTANCE hPrevInstance,
                     LPSTR     lpCmdLine,
                     int       nCmdShow)
{
  WNDCLASSEX winClass;
  winClass.cbSize = sizeof(WNDCLASSEX);
  winClass.lpfnWndProc = WndProc;
  winClass.cbClsExtra = 0;
  winClass.hInstance = hInstance;
  winClass.hIcon = LoadIcon(NULL, IDI_APPLICATION);
  winClass.hCursor = LoadCursor(NULL, IDC_ARROW);
  winClass.lpszMenuName = NULL;
  winClass.lpszClassName = className;
  winClass.hIconSm = LoadIcon(NULL, IDI_WINLOGO);
  /*	Register window class*/
  if (!RegisterClassEx(&winClass))
  {
    MessageBox(NULL, "Window Registration Failed!", "Errors!", MB_ICONERROR | MB_OK);
    return 0;
  }
}
{% endcodeblock %}

In this example, `winClass` is the variable of the `WNDCLASSEX` structure, and some properties are initialized. Calling `RegisterClassEx(&winClass)` is to register the class in Windows environment. Then, the window class can be used in the rest of the program.

#### The control procedure

In the above code, `lpfnWndProc` is an important but intentionally omitted property. This property is a function pointer of a *windows procedure*. A windows procedure is a special function, used to control the message events from a class of window. Its definition is like this:

{% codeblock lang:c %}
/* Windows Event Handler */
LRESULT CALLBACK WndProc(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam)
{
  return DefWindowProc(hwnd, message, wParam, lParam);
}
{% endcodeblock %}

Note that the function name is freely defined by programmers, but the argument list should be the same as the above example. The return result should be the result from `DefWindowProcW` So, the part of the register code should be revised like this:

{% codeblock lang:c %}
...
winClass.lpfnWndProc = WndProc; // pointer to WndProc
...
{% endcodeblock %}

### Create a window

Finally, we can create an visible application in Windows by using the event loop of windows. As I mentioned above, windows applications are event-driven programming model. Event-driven model means every operation of an application may trigger an event and all the events are handled within the handling loop. Once the loop stops, the application is about to exit.

{% codeblock lang:c %}
...
/* Create window */
hwnd = CreateWindowEx(
        WS_EX_TOOLWINDOW,
        winClass.lpszClassName,
        className,
        WS_OVERLAPPEDWINDOW,
        CW_USEDEFAULT, CW_USEDEFAULT, 240, 120,
        NULL, NULL, hInstance, NULL
      );
...
{% endcodeblock %}

### Show the window

Two simple functions are used to show the created window, otherwise the window is hidden from the graphics. Please refer to documents of `ShowWindow` and `UpdateWindow` on MSDN [here][2] and [here][3].

{% codeblock lang:c %}
ShowWindow(hwnd, SW_SHOW);
UpdateWindow(hwnd);
{% endcodeblock %}

### Message Loop

The Windows C programming model is message looping, which means all behaviors are converted to messages and all messages are either sent or received by appropriated functions. The messages are finally passed to the control procedure.

{% codeblock lang:c %}
...
while (GetMessage(&msg, NULL, 0, 0))
{
  TranslateMessage(&msg);
  DispatchMessage(&msg);
}
...
{% endcodeblock %}

### More details in the control procedure

As we mentioned that Windows C program is designed in message-loop pattern, all the behaviors are converted to messages. The control procedure gives programmers a chance that can trap system and application behaviors in a loop of messages. So a common implemention ion of the control procedure is a big switch-case block. In this switch-case block, there are system message cases, such as `WM_CREATE`, `WM_PRINT`, `WM_CLOSE` and `WM_DESTROY`. These four messages are emitted from Windows system. In addition, applications can also emit their own messages. We won't discuss message customization in this tutorial. For example, the following gives the implemention that two types of messages are trapped in the loop: `WM_CLOSE` and `WM_DESTROY`. `WM_CLOSE` is a message sent to applications to indicate that this window or application should terminate. So we call `DestroyWindow` function in this case. `WM_DESTROY` is a message to indicate that the window is removed from the screen after destroying. For the explanation of `DestroyWindow` and `PostQuitMessage`, please refer to documents on MSDN [here][4] and [here][5].

{% codeblock lang:c %}
/* Windows Event Handler */
LRESULT CALLBACK WndProc(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam)
{
  switch (message)
  {
    case WM_CREATE:
      break;
    case WM_PAINT:
      break;
    case WM_CLOSE:
      DestroyWindow(hwnd);
      break;
    case WM_DESTROY:
      PostQuitMessage(0);
      break;
  }
  return DefWindowProc(hwnd, message, wParam, lParam);
}
{% endcodeblock %}

## Conclusion

We present how to install `MinGW`, and the basic elements of a Windows application. We simply introduced and explained what `MinGW` is and the design pattern of a bare example of a Windows application. As we know, Windows development has evolved into a stage, at which this kind of C implementation might be no longer used, however, this example can help to understand other frameworks, such as `MFC` and `C#`, because they either use wrappers for many functions in C or build functions on top of C.


[1]:http://msdn.microsoft.com/en-us/library/windows/desktop/ms633559(v=vs.85).aspx
[2]:http://msdn.microsoft.com/en-us/library/windows/desktop/ms633548(v=vs.85).aspx
[3]:http://msdn.microsoft.com/en-us/library/windows/desktop/dd145167(v=vs.85).aspx
[4]:http://msdn.microsoft.com/en-us/library/windows/desktop/ms632682(v=vs.85).aspx
[5]:http://msdn.microsoft.com/en-us/library/windows/desktop/ms644945(v=vs.85).aspx
