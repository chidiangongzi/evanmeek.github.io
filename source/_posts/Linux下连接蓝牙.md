---
title: Linux下连接蓝牙
copyright: true
date: 2020-02-09 12:47:42
categories: Linux
tags:
  - 蓝牙
  - Linux
---

<p align="center">Linux下连接蓝牙设备的方式</p>

<!--more-->

# 准备事项

## 必备软件 

如果是你Arch用户，你可以直接:

``` shell
> pacman -S bluez bluz-utils pulseaudio-bluetooth pavucontrol
```

其中:
- `bluez`包是提供蓝牙的协议栈
- `bluez-utils`包含了各式各样的工具
- `pulseaudio-bluetooth`为提供音频服务器
- `pavucontrol` 音频服务的图形化控制软件


## 启动蓝牙服务

``` shell
> systemctl enable bluetooth
> systemctl start bluetooth
```

## 启动音频服务

``` shell
> pulseaudio -k                   # 确保没有pulseaudio启动
> pulseaudio --start              # 启动pulseaudio服务
```

## 将当前用户添加到lp用户组

``` shell
> sudo usermo -a -G lp $USER
```




# 连接蓝牙 

这里以连接我耳机来举例

使用`bluetoothctl`命令，开始连接:

1. 键入`power on`打开控制电源器
2. 键入`scan on`扫描附近的蓝牙设备
3. 键入`scan off`关闭扫描（如果扫描出来你的设备再关闭）
4. 键入`devices`命令可以查看已经扫描过的设备
5. 键入`agent on`打开代理
6. 键入`pair $MAC`进行配对（如果是陌生设备才需要配对，$MAC代表了MAC地址，支持Tab
   补全)
7. 键入`trust $MAC` 如果你的设备是无PIN码的，可以这样手动认证。
8. 键入`connect $MAC`连接设备


下面为一个实例:

``` shell
[bluetooth]# power on
[CHG] Controller 84:C5:A6:00:59:64 Class: 0x001c010c
Changing power on succeeded
[CHG] Controller 84:C5:A6:00:59:64 Powered: yes
[bluetooth]# scan on
Discovery started
[CHG] Controller 84:C5:A6:00:59:64 Discovering: yes
[NEW] Device 67:68:09:5E:69:C8 67-68-09-5E-69-C8
[NEW] Device 60:21:6D:9E:D9:E8 60-21-6D-9E-D9-E8
[bluetooth]# scan off
[CHG] Device 60:21:6D:9E:D9:E8 TxPower is nil
[CHG] Device 60:21:6D:9E:D9:E8 RSSI is nil
[CHG] Device 67:68:09:5E:69:C8 RSSI is nil
[CHG] Controller 84:C5:A6:00:59:64 Discovering: no
Discovery stopped
[bluetooth]# devices 
Device E8:29:58:44:FE:D6 mobike
Device E0:DC:FF:DC:5A:88 我永远喜欢Linux
Device 94:BF:2D:90:7C:F9 EvanMeek的 Beats Studio³
Device 74:40:BB:C4:04:D4 74-40-BB-C4-04-D4
Device 67:68:09:5E:69:C8 67-68-09-5E-69-C8
Device 60:21:6D:9E:D9:E8 60-21-6D-9E-D9-E8
[bluetooth]# agent on
Agent is already registered
[bluetooth]# pair 94:BF:2D:90:7C:F9 
Attempting to pair with 94:BF:2D:90:7C:F9
[bluetooth]# connect 94:BF:2D:90:7C:F9 
Attempting to connect to 94:BF:2D:90:7C:F9
[CHG] Device 94:BF:2D:90:7C:F9 Connected: yes
Connection successful
[CHG] Device 94:BF:2D:90:7C:F9 ServicesResolved: yes
[EvanMeek的 Beats Studio³]# 
```



> 本文参考
> [ArchLinux Bluetooth Wiki](https://wiki.archlinux.org/index.php/Bluetooth)
> [暗无天日的博客](http://blog.lujun9972.win/blog/2017/07/18/%E5%9C%A8archlinux%E4%B8%AD%E4%BD%BF%E7%94%A8%E8%93%9D%E7%89%99%E8%80%B3%E6%9C%BA/)
