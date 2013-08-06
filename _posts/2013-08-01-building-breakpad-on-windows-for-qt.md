---
layout: blog
title: Building Google Breakpad on Windows for Qt applications
summary: Documenting the process to build Google Breakpad, crash reporting tool on Windows, so that it can be used with Qt applications
---

# {{ page.title }}

__01 August 2013 - Chandigarh, India__

[Google Breakpad](http://code.google.com/p/google-breakpad/) is a multi-platform crash reporting library. However, I had a tough time building it with Visual Studio 2010 Express for a QT application, which is supposed to be run on Windows.

+ Download the latest snapshot of breakpad source code, by checking out a copy of the code from SVN:

        cd C:\
        svn checkout http://google-breakpad.googlecode.com/svn/trunk/ breakpad

+ This source does not contain a Visual Studio solution (.sln) file. However, it ships with a tool called [gyp](http://code.google.com/p/gyp/). Please make sure that you have Python installed, as GYP need Python to run. A popular Python distribution for Windows is ActiveState Python, which can be downloaded from [here](http://www.activestate.com/activepython/downloads). Run the following commands to generate a Visual Studio solution file.

        cd breakpad\src\client\windows
        ..\..\tools\gyp\gyp.bat --no-circular-check

+ Open the solution generated with GYP with Visual Studio. Now, for each project in the solutions, open the Property pages (Right Click -> Properties). You need to set the following paramaters for each project:

    + C/C++ -> General -> Treat Warning as Errors - No (`/WX-`)
    + C/C++ -> Code Generation -> Runtime Library - Multi-threaded DLL (`/MD`)
    + C/C++ -> Langugage -> Treat WChar_t As Built in Type - No (`/Zc:wchar_t-`) - This is required because this is how Qt treats `wchar_t` types.

+ Build all the libraries with Visual Studio and you should be able to generate .lib files now.

+ Add the following in `.pro` file in your application to generate .pdb file:

        QMAKE_CFLAGS_RELEASE += -Zi
