---
title: Learn-Qt5-Qt模块简介
copyright: true
date: 2019-06-12 20:30:42
categories: 学习笔记
tags:
  - Qt
  - C_++
---

Qt5分为两个大的模块，分别是`Qt Essentials`以及`Qt Add-Ons`以及一些额外的模块和工具．

<!--more-->

# Qt Essentials

`Qt Essentials`是Qt的基础，它可以在所有平台上运行，下面列出了Qt Essentials模块的组件．

|模块|简述|
|:-:|:-:|
|Qt Core|其他非图形类模块所使用的核心,|
|Qt GUI|图形界面组件的基类，包括了OpenGL.|
|Qt Multimedia|音频，视频，广播和摄像头相关功能.|
|Qt Network|提供跨平台的网络能力．|
|Qt Qml|提供QML使用的C++API.|
|Qt Quick|允许在Qt/C++程序中嵌入 Qt Quick|
|Qt SQL|允许使用SQL访问数据库|
|Qt Test|提供Qt程序的单元测试能力｜
|Qt Webkit|基于WebKit2的实现以及一套全新的QML API|

# Qt Add-Ons
`Qt Add-Ons`是Qt的扩展模块，建立在基础模块之上，在能运行Qt的平台之上可以酌情引人．

|模块|简述|
|:-:|:-:|
|Qt 3D|提供声明式语法，在Qt程序中可以简单地嵌入3D图像．｜
|Qt Bluetooth|提供用于访问蓝牙无线设备的C++和QML API.|
|Qt Contacts|用于访问地址薄或联系人数据库的C++和QML API.|
|Qt D-Bus|Unix平台独有的类库，用于使用D-Bus协议进与进程间进行交互|
|Qt Graphical Effects|提供一系列用于实现图像特效的类|
|Qt Image Formats|支持图片格式的一系列插件|
|Qt JS Backend|为V8 JavaScript引擎的移植，仅供QtQML模块内部使用|
|Qt Location|方便在Qt应用程序中使用OpenGL，保留于Qt4|
|Qt Organize|使用QML和C++API访问组织事件｜
|Qt Print Support|提供对打印功能的支持｜
|Qt Publish and Subscribe|为应用程序提供对项目值的读取，导航，订阅等功能.|
|Qt Quick 1|从Qt4移植而来的Qt Declarative模块，用于提供与Qt4兼容|
|Qt Script|提供脚本化机制，为了与Qt5兼容|
|Qt Script Tools|为了使用Qt Script模块的应用程序提供的额外的组件|
|Qt Sensors|提供访问各类传感器的QML和C++接口.|
|Qt Service Framework|提供客户端发现其他设备的服务.|
|Qt SVF|提供渲染和创建SVG文件的功能．|
|Qt System Info|提供一套API，用于发现系统相关的信息.|
|Qt Tools|提供了Qt开发的方便工具,例如Qt CLucene,Qt Designer,Qt Help以及Qt UI Tools.|
|Qt Versit|提供了对Versit API的支持．|
|Qt Wayland|仅用于Linux平台，用户替代QWS|
|Qt WebKit|从Qt4 一直来的基于WebKit1和QWidget的API|
|Qt Widgets|使用C++扩展的Qt Gui模块，提供了一些界面组建，比如按钮，单选框|
|Qt XML|SAX和DOM的C++实现．此模块已凉凉，更换为QXmlStreamReader/Writer|
|Qt XML Patterns|提供对XPath,XQuery,XSLT和XML Schema验证的支持．|



