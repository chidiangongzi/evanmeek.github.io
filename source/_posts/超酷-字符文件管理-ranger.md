---
title: 超酷-字符文件管理-ranger
copyright: true
date: 2019-07-03 09:47:24
categories: 折腾日记
tags:
  - Linux
---

<!--more-->

![ranger](超酷-字符文件管理-ranger/ranger-pre.png)

# 0x0 什么是ranger?

`ranger`是一个基于文本的文件管理器，由Python编写。

# 0x1 为什么要选择ranger?

`ranger`具有以下特性:

- vi风格的快捷键

- 书签

- 选择

- 标签

- 选项

- 命令历史

- 创建符号链接

- 任务视图

- 自定义命令

- 自定义快捷键按

# 0x2 使用ranger

在终端内输入`ranger`以启动ranger

使用`h j k l`进行目录之间的进出。

# 0x3 配置ranger

配置文件:

- rc.conf 基本选项与快捷键设置

- commands.py 可在ranger下使用`:`执行的命令

- rifile.conf 文件关联，控制不同文件用不同程序打开

配色方案:

`ranger`默认自带四种配色方案:`defalut` `jungle` `snow` `zenburn`

使用`:set colorscheme scheme`进行切换。

自定义配色方案文件放在`~/.config/ranger/colorschemes`

# 0x4 我的ranger配置

以上传至Github

[点击访问](https://github.com/EvanMeek/Vanilla/tree/master/ranger)

# 0x5 其他

下载地址:[点击获取](https://github.com/ranger/ranger/releases)

Arch系:

~~~
> pacman -S ranger
~~~
