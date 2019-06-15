---
title: Linux-Linux命令行简介-0
copyright: true
date: 2019-06-15 16:35:38
categories: Linux系列
tags:
 - Linux
---

# 1.1 Linux命令行概述

## 1.1.1 Linux命令行的作用与意义

  Linux命令行相比图形界面操作的优点:

  - 快速

  - 批量

  - 自动化

  - 智能化管理

## 1.1.2 Linux命令行介绍

  大多数互联网企业在使用Linux不会安装图形界面，而是才用文本模式（命令行）的方式进行使用，如图:

  ![命令行图](Linux-Linux命令行简介/1.1.2-0.png)

## 1.1.3 Linux命令行的开启及退出

  主机开机时，Linux将会进行初始化等各种操作，最终将进入命令行，想使用必须先登录。

  ~~~Shell
  user login:\_
  password:\_
  ~~~

  等待你输入用户名密码，密码输入时是不会显示的。

  使用`exit`,`logout`或者`Ctrl+d`快捷键可退出登录，若退出则需要重新登录才会被允许使用Shell命令。

## 1.1.4 Linux命令行提示符介绍
