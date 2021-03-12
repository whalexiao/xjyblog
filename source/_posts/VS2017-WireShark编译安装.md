---
title: VS2017+WireShark编译安装
date: 2020-03-16 00:02:28
tags:
---
任何一项软件通过源码编译安装都是困难的
刚刚源码编译完WireShark的我深有体会
依稀记得上次数据库老师让我们用源码编译PostGreSql花费了我一整天时间
这次网络分布式的实验--源码编译WireShark竟然花费了我近两天时间
安装的过程无非就是下载各种依赖，配置各种环境变量
但是一旦有一步出现一个小小的问题都会卡很久
下面我把自己编译WireShark过程中总结如下
<!--more-->
## 依赖项
- Install Visual Studio 
需要安装corresponding SDK，winSDK8.1...否则会报错MSBuild.exe fail
下载和安装Microsoft Visual Studio 2019 Community Edition。
在安装过程中，选择桌面应用Desktop development with C++，保留VC++ 2019、Windows 10 SDK、Visual C++ tools for CMake等组件。
- Install QT5
Go to https://www.qt.io/developers/ to download opensource qt 5.12.3
Config QT plugin in VS2017 
 tools -> extensions and updates -> onlinw -> Qt Visual Studio Tools
Set env QT5_BASE_DIR to be like C:\Qt\Qt5.12.3\5.12.3\msvc2017_64
- Install cygwin
Perl must be choose to install
Add env WIRESHARK_CYGWIN_INSTALL_PATH to be like C:\cygwin64
- python
(参看网络上安装python的教程即可)
- cmake
https://cmake.org/download/   
(直接解压出来bin目录下面的exe文件就可以运行，如果需要在命令行中运行cmake的话需要在path中加入环境变量：C:\Users\dell\Desktop\cmake-3.17.0-rc3-win64-x64\bin)  


## 生成wireshark的vs工程
- Download wireshark
https://www.wireshark.org/#download click Sourcec Code
- 创建build目录 
(1)Assume that the source code folder is C:/wireshark_src
(2)Create a different empty folder like C:/wireshark_build
(3)Add env variable WIRESHARK_LIB_DIR as C:/wireshark_build/wireshark-win64-libs-3.0
注意这里文件夹的名字是wireshark-*-libs-*.第一个*是平台位数，win64/win32，第二个*是版本，不一定是3.0需要根据CMakelist的信息进行修改。
- Download win_flex and unzip it
在环境变量Path中加入C:\Users\dell\Desktop\win_flex_bison3-latest
- Run Cmake
(1)可以使用cmake-GUI运行，但是好像使用VS2015及其以上版本的vs会报错：
![cmake-GUI](cmake-GUI.PNG)  
![error](error.png)  
这个错误地原因是因为VS系统没有设置PlatForm变量，网上查说是这个变量是在运行vs的prompt时候系统自动设置的。  
(2)使用VS-Prompt运行
在wireshark_src和wireshark_build的上级目录运行  
> cmake -G "Visual Studio 16 2019" -A x64 ..\wireshark_src 

![prompt](prompt.png)  
## 环境变量
在开始编译之前检查一下环境变量是否正确。
![env1](env1.PNG)  
![env2](env2.PNG)  
## 编译WireShark
使用VS打开wireshark_src中的WireShark.sln编译即可，可以生成Debug或者Release版本的。但是此时还不能运行，需要加入以下的DLL文件  
(1)Copy the following dlls and subfolder from Qt to ./run/release
- Qt5Core.dll
- Qt5Gui.dll
- Qt5Multimedia.dll
- Qt5Network.dll
- Qt5PrintSupport.dll
- Qt5Widgets.dll
- Qt5WinExtras.dll
- subfolder snmp/

(2)Copy the following dlls and subfolder from Qt to ./run/debug
- Qt5Cored.dll
- Qt5Guid.dll
- Qt5Multimediad.dll
- Qt5Networkd.dll
- Qt5PrintSupportd.dll
- Qt5Widgetsd.dll
- Qt5WinExtrasd.dll
- subfolder snmp/
- Subfolder Qt/5.12.3/msvc2017_64/plugins/platforms/
最后就大功告成可以开开心心运行WireShark了。  

## 错误总结  
(1)GUI运行错误  
![error](error.png) 
解决:使用VS-x64-Prompt运行cmake
(2)LEX_EXECUTABLE-NOTFOUND和YACC_EXECUTABLE_NOTFOUND
解决： 配置win_flex环境变量，或者在cmake-gui中选中对应的exe文件(LEX_EXECUTABLE-NOTFOUND:select win_flex.exe
YACC_EXECUTABLE_NOTFOUND:select win_bison.exe)
