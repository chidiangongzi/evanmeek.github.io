---
title: ProxyChains入门使用教程
copyright: true
date: 2020-01-07 16:59:41
categories: 软件分享
tags: 
---

身为天朝的一名开发者，fq已经成为必备技能了。ProxyChains就是一个强大的强制代理工
具。
<!--more-->

# ArchLinux

Arch下直接安装`ProxyChains-ng`这个包即可。

``` shell
sudo pacman -S proxychains-ng
```

安装好后编辑`/etc/proxychains.conf`。

找到最下面的`[ProxyList]`，往里面添加映射的类型，例如我想要`http`协议走代理就可
以这么写。

``` conf
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
http 	127.0.0.1 8000
# socks5 127.0.0.1 1080
```

使用非常简单，可以直接在需要走代理的程序前加上`proxychains`即可。

``` shell
➜  ~ proxychains curl google.com
[proxychains] config file found: /etc/proxychains.conf
[proxychains] preloading /usr/lib/libproxychains4.so
[proxychains] DLL init: proxychains-ng 4.14
[proxychains] Strict chain  ...  127.0.0.1:8000  ...  google.com:80  ...  OK
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```

如果闲命令太长可以写一个`alias`，在这里就不演示了。





# MacOS

如果你使用包管理器，例如`homebrew`可以直接执行:

``` shell
> brew install proxychains-ng
```

但是会很慢，所以有第二种方式————手动编译安装。

``` shell
> git clone --depth 1 git@github.com:rofl0r/proxychains-ng
> cd proxychains-ng && ./configure --prfix=/usr --sysconfdir=/etc
> make && make install
> sudo make install-config # 生成proxychains.conf配置文件
```

这里可能会有一个坑————执行`make install`出错，想要解决很简单：

进入`configure`目录，修改`config.mak`文件，将`bindir=/usr/bin`改为`bindir=/usr/local/bin`

就算你安装好，并且配置好文件后可能照样不能使用，这一切都是因为苹果电脑的`SIP`保
护系统，有关`SIP`的信息自己谷歌一下，再考虑要不要关闭。

关闭分两种，一种是让`SIP`进入debug模式，再一种就是永久关闭（除非手动启动）。

首先重启Mac，在重启时按住`option`键，进入选择启动磁盘项，然后按组合键
`Command+R`即可进入恢复模式，进入恢复模式后先验证密码，然后在**顶栏找到实用工具
的终端**,再看下一步吧。

debug模式

``` shell
> csrutil enable --without debug 
```

永久关闭

```shell
> csrutil disable
```

进行设置了后重启打开终端输入`csrutil status`，如果显示`System Integrity
Protection status:disbaled`则说明关闭成功了。

除了配置文件路径不同其他都跟`Arch`下配置一样————`/usr/local/etc/proxychains.conf`

