---
title: virtualbox 安装
date: 2016-05-10 00:07:12
tags:
- virtualbox
categories: 系统
---

下载地址：[http://yunpan.cn/cFV9ShR4bdUBx](http://yunpan.cn/cFV9ShR4bdUBx "下载地址")访问密码：e8fb
1.next

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install01.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install01.png)

2.路径中不要有中文和空格

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install02.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install02.png)

3.选择路径

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install03.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install03.png)

4.创建桌面快捷方式

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install04.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install04.png)

5.警告

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install05.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install05.png)

6.安装

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install06.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install06.png)

7.正在安装

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install07.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install07.png)

8.完成安装

![http://7xng0o.com1.z0.glb.clouddn.com/vbx_install08.png](http://7xng0o.com1.z0.glb.clouddn.com/vbx_install08.png)

**问题1：无法创建unbuntu 64bit 虚拟机**

          安装完virtualbox后，新建虚拟机。类型选择为Linux时，版本下拉选项只有ubuntu 32bit，无ubuntu 64bit。

原因

     64 bit 的虚拟机需要硬件虚拟化支持，而BIOS 默认将它关闭了。

解决方案

     重启计算机，按F2进入BIOS设置

     在CPU设置下面，将“Intel虚拟化技术”状态设置为打开，保存并退出，重启计算机。

     再进入virtualbox就可以看到ubuntu 64bit这个选项了。


**问题2：virtualbox不能为虚拟电脑启动一个新任务**

     错误详情如下：

          Unable to load R3 module C:\Program Files\Oracle\VirtualBox/VBoxDD.DLL (VBoxDD): GetLastError=1790 (VERR_UNRESOLVED_ERROR).

         返回 代码:E_FAIL (0x80004005)

         组件:Console

         界面:IConsole {8ab7c520-2442-4b66-8d74-4ff1e195d2b6}

原因

      宿主机win7用的ghost系统，会破解uxtheme.dll文件，导致virtualbox启动失败

解决方案

      使用原版的uxtheme.dll替换c:\windows\system32\uxtheme.dll即可。Windows7 64bit uxtheme.dll这里下载
