---
layout: post
excerpt_separator: <!--more-->
title: "Qt in MAC OS-X - 4 simple points to know"
date: 2017-12-14
tags: Qt MAC-OS
---

I have been working on Qt for Mac OS-X and found it is quite different compare to Windows or Linux.
Mac is a very vast on its own and introduces many levels of security for user safety.
Let's have a look into 4 basic points about Qt in Mac OS-X. <!--more-->
I have used MacBook Pro, with OS X 10.8.4 and Qt version of 4.8

**Point 1**
Qt installer comes as `.DMG` files, stands for `Disk Image files`. A DMG file is like a virtual DVD or hard drive. They can be “mounted” on your Mac in order to work with their contents, or even burned to an actual physical disc.
Right click on DMG file and chose `Open Wint > DiskImageMounter.app` or double click on DMG it should auto mount using `DiskImageMounter` if it's your default image mounter application in Mac. Once the image is mounted, it is very easy to install Qt file from image.

**Point 2**
Where all Qt gets installed in Mac?
This is little tough to explain. When I installed my Qt version `4.8.4`, it got installed into many directories.
However, after installation, for `qmake-query`, I found this results,
```
QT_INSTALL_PREFIX:/
QT_INSTALL_DATA:/usr/local/Qt4.8
QT_INSTALL_DOCS:/Developer/Documentation/Qt
QT_INSTALL_HEADERS:/usr/include
QT_INSTALL_LIBS:/Library/Frameworks
QT_INSTALL_BINS:/Developer/Tools/Qt
QT_INSTALL_PLUGINS:/Developer/Applications/Qt/plugins
QT_INSTALL_IMPORTS:/Developer/Applications/Qt/imports
QT_INSTALL_TRANSLATIONS:/Developer/Applications/Qt/translations
QT_INSTALL_CONFIGURATION:/Library/Preferences/Qt
QT_INSTALL_EXAMPLES:/Developer/Examples/Qt/
QT_INSTALL_DEMOS:/Developer/Examples/Qt/Demos
QMAKE_MKSPECS:/usr/local/Qt4.8/mkspecs
QT_VERSION:4.8.4
```
Still it is difficult to say where all it got installed :)

**Point 3**
How to deploy Qt application in Mac?
It is quite easy to deploy Qt applications in Mac, when it is dynamically built. Mac applications will have executable extension `.APP`. This `.APP` file is a special type of container [in other word - folder] which will going to hold all Qt dependencies inside, for application to launch. Great thing is, the main executable will also be inside APP directory, here in this location,
`MyDemo.app/Contents/MacOS/MyDemo`
Let's build and deploy `.app` for `MyDemo` application.
Once you are able to successfully compile Qt application, Qt creates executable for your convenience. 
If in case it is not created, just run below command,
```
sh-3.2# otool -L MyDemo.app/Contents/MacOS/MyDemo
```
After above step is done, we need to use a tool called install_name_tool.
Let's run these build scripts,
```
sh-3.2# mkdir -p MyDemo.app/Contents/Frameworks
sh-3.2# cp -R /Library/Frameworks/QtCore.framework  MyDemo.app/Contents/Frameworks
sh-3.2# cp -R /Library/Frameworks/QtGui.framework  MyDemo.app/Contents/Frameworks
```
Above two lines copy frameworks dynamic libraries into app `Contents/Frameworks` directory. 
After copying Qt library into the bundle, we must update both the library and the executable so that they know where they can be found. This is where the `install_name_tool command-line tool` comes in handy. For the Qt library, run these two lines,
```
sh-3.2# install_name_tool  -id  @executable_path/../Frameworks/QtCore.framework/Version/4/QtCore  MyDemo.app/Contents/Frameworks/QtCore.framework/Version/4/QtCore
sh-3.2# install_name_tool  -id  @executable_path/../Frameworks/QtGui.framework/Version/4/QtGui  MyDemo.app/Contents/Frameworks/QtGui.framework/Version/4/QtGui
```
And for the executable,
```
sh-3.2# install_name_tool -change @executable_path/../Frameworks/QtCore.framework/Version/4/QtCore  MyDemo.app/Contents/MacOS/MyDemo
sh-3.2# install_name_tool -change @executable_path/../Frameworks/QtGui.framework/Version/4/QtGui  MyDemo.app/Contents/MacOS/MyDemo
```
Now that your application is ready to deploy. Just give `MyDemo.app` files as executable. 

**Point 4**
How to UnInstall Qt from Mac?
This is also a tough to explain. But I did below steps to uninstall Qt from my MacBook.
For all below steps to execute, you must be super-user. 
```
sh-3.2# cd  /Applications/
sh-3.2# rm  -r  QtCreater.app/*
sh-3.2# rm  -r  QtCreater.app
sh-3.2# cd  /Library/Frameworks/
sh-3.2# rm  -r  Qt*
sh-3.2# cd  ~/Library/Preferences/
sh-3.2# rm  com.qt*
sh-3.2# rm  org.qt*
sh-3.2# cd  /usr/local/
sh-3.2# rm  -r  Qt*
```
After all above steps, now run Qt uninstaller located in `/Developer/Tools/`
```
sh-3.2# cd  /Developer/Tools/
sh-3.2# ./uninstall-qt.py
```
This, hopefully, will going to uninstall Qt successfully from your Mac Book.

That's it for now.