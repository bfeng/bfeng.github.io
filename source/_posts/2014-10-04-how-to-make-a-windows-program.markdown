---


published: false
---

# Introduction

# How to setup compilers

The first step to write a real application is to setup its compilers. `MinGW` is an open source compiler suite, including GCC for C, C++, Fortran, Java, and Ada, binutils, Windows API, runtime, and make. The following steps guide how to setup `MinGW` on Windows. In this tutorial, we use `MinGW gcc` as the compiler for C and its runtime library to run the application on Windows.

## Download and install `MinGW`

The official site of `MinGW` gives a premium guide of how to: http://www.mingw.org/wiki/HOWTO_Install_the_MinGW_GCC_Compiler_Suite. Please refer to this page.

The summary of this guide are:
1. download a suitable installer
2. extract and run the installer
3. setup `MinGW\bin` in the `PATH` environment variable

To verify your installation, just open a console and test some commands, such as `gcc` and `make`.

# The basic elements of a Windows application

## The main function

The following is the main function example of Windows applications. Instead of using the `main` for ANSI C applications, the main function is defined as `WinMain` under Windows.

~~~c
#include <windows.h>

/* Main function */
int APIENTRY WinMain(HINSTANCE hInstance,
                     HINSTANCE hPrevInstance,
                     LPSTR     lpCmdLine,
                     int       nCmdShow)
{
}
~~~

For Windows applications, each instance of an application is controlled by a `handle`, the structure of which is defined as `HINSTANCE`. So int `WinMain`, the first two arguments are instance handles of applications. `hInstance` is the handle to the current instance of the application. `hPrevInsance` is the handle to previous instance of the applications. However, the *previous* here is varied by cases. In addition to the third and fourth arguments, please refer to the official documentation of this function: http://msdn.microsoft.com/en-us/library/windows/desktop/ms633559(v=vs.85).aspx

## Register a window class

A Windows application composites of a class of windows. Before creating a visible application under graphic environment, a new window class should be defined and registered in the system. The data structure `WNDCLASSEX` used with `RegisterClassEx` can define and register the window class. Below is an example of a window class in main function.

~~~c
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
~~~

In this example, `winClass` is the variable of the `WNDCLASSEX` structure, and some properties are initialized. Calling `RegisterClassEx(&winClass)` is to register the class in Windows environment. Then, the window class can be used in the rest of the program.

## The control procedure

In the above code, `lpfnWndProc` is an important but intentionally omitted property. This property is a function pointer of a *windows procedure*. A windows procedure is a special function, used to control the message events from a class of window. Its definition is like this:

~~~c
/* Windows Event Handler */
LRESULT CALLBACK WndProc(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam)
{
  return DefWindowProc(hwnd, message, wParam, lParam);
}
~~~

Note that the function name is freely defined by programmers, but the argument list should be the same as the above example. The return result should be the result from `DefWindowProcW` So, the part of the register code should be revised like this:

~~~c
...
winClass.lpfnWndProc = WndProc; // pointer to WndProc
...
~~~

## Create a window

Finally, we can create an visible application in Windows by using the event loop of windows. As I mentioned above, windows applications are event-driven programming model. Event-driven model means every operation of an application may trigger an event and all the events are handled within the handling loop. Once the loop stops, the application is about to exit.

~~~c
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
~~~

## Show the window

~~~c
ShowWindow(hwnd, SW_SHOW);
UpdateWindow(hwnd);
~~~

## Message Loop

~~~c
...
while (GetMessage(&msg, NULL, 0, 0))
{
  TranslateMessage(&msg);
  DispatchMessage(&msg);
}
...
~~~

## More details in the control procedure

~~~c
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
~~~

# Conclusion
