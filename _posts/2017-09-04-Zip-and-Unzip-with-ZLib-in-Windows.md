---
layout: post
excerpt_separator: <!--more-->
title: "Zip and Unzip with ZLib in Windows"
date: 2017-09-04
tags: Zip zlib Windows
---

This is a quick post on *How to use ZLIB for Zippinga and Unzipping archives in Windows*. <!--more-->
Nothing much to do, it's all ready available in ZLIB source. You just need to download and compile it. That's all. 

I have used below configuration for my compilation:
+ OS Type : Windows 7, 64-Bit
+ Visual Studio 2010, Command line Compiler for 64-Bit


Before we begin, I will introduce you what's is there in ZLIB bundled.
ZLIB is a software library used for data compression. zlib was written by Jean-Loup Gailly and Mark Adler and is an abstraction of the DEFLATE compression algorithm used in their gzip file compression program. zlib is also a crucial component of many software platforms including Linux, Mac OS X, and iOS. It has also been used in gaming consoles such as the PlayStation 3, Wii, and Xbox 360. 
The first public version of zlib, 0.9, was released on 1 May 1995 and was originally intended for use with the libpng image library. It is free software, distributed under the zlib license.

But ZLIB by itself doesn't support Zipping and Unzipping of archives, files and folders [refer FAQs]. It can handle only data compression. So, we need an external application to handle files and folders zipping and unzipping activity.

Fortunately, there is a package integrated inside ZLIB itself, called MiniZip, which handles all kind of archives. This comes part of ZLIB source now a days. [refer MiniZip].

So, basically, in this post, we will going to compile MiniZip source for Windows, coming with ZLIB source code.

Well let's start then.
At the time of writing this post, ZLIB latest version was zlib1.2.5.
Download ZLIB source code form [HERE](http://www.zlib.net/) or from [HERE](http://www.winimage.com/zLibDll/zlib125.zip) [please inform me if the links are broken]

For our compilation, we basically don't need ZLIB source code. So I will use pre-compiled ZLIB static library for my work. Download pre-compiled ZLIB libraries from [HERE](http://www.winimage.com/zLibDll/zlib125dll.zip). This contains, Windows specific ZLIB DLLs and LIBs for both 64-bit and 32-bit compilation.

Unzip and keep both the directories in a common folder [for e.g, `C:\TEST\zlib1.2.5` and `C:\TEST\zlib125dll`]

I have written a Makefile for windows 64-bit compilation. Please refer it. Download it and copy it into `C:\TEST\zlib1.2.5\contrib\minizip\` directory. The Makefile already present in `minizip` directory will support Linux only. So you can either keep a back-up of old Makefile or replace it with the one I have given you.

Inside `minizip` directory, you must find below source files,
`ioapi.c, iowin32.c, zip.c, unzip.c, miniunz.c, minizip.c` and corresponding header files.
`minizip.c` and `miniunz.c` are main source files for Zipping and Unzipping demo.
Open all the source files and header files, if you see below include at the top,

`#include \"zlib.h\"`
replace it with
`#include \"..\\..\\zlib.h\"`
as our main zlib source is two directory below the hierarchy. 

Now, open \"Visual Studio 2010 x64 Win64 Command Prompt\" and navigate to `\"C:\\TEST\\zlib1.2.5\\contrib\\minizip\\"` directory and type command,

`nmake all`
If everything goes fine, and if you have followed all the steps from above properly, it should compile perfectly and should yield 2 binaries `\"MyMiniZip.exe\"` and `\"MyMiniUnZip.exe\"`

Now it's time to test binaries,
**To zip any files, use MyMiniZip.exe**
`MyMiniZip.exe  <output_file_name.zip>  <input_file1>  <input_file2>...<input_fileN>`


for e.g,(I hope no explanation is required)
`MyMiniZip.exe  test_file.zip  file1.txt  file2.jpg  subDir\\file3.png  C:\\MyDir\\file4.doc`


**To UnZip any zipped files, use MyMiniUnzip.exe**
`MyMiniUnZip.exe  <input_file_name.zip>`

for e.g,
`MyMiniUnZip.exe  C:\\MyDir\\MyTestArchive.zip`

**To list all the files inside a zipped files use MyMiniUnZip.exe with -l flag**
`MyMiniUnZip.exe -l <input_file_name.zip>` 

I hope everything went good at your side.