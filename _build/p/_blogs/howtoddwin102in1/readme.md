---
layout: page
include_in_header: false
permalink: /_blogs/howtoddwin102in1/
---
我们知道grub有biosboot技术，可以实现uefi/bios gpt二合一，那么windows呢？

继前面一贴
https://hostloc.com/thread-980262-1-1.html
有人说这是不可能的。

我试了下。
实验结果证明，windows uefi/bios gpt二合一兼容dd包，是完全可以行的。
(即不管你的机器是bios的还是uefi的某种，，代表同一份系统的同一份镜像都可以毫无修改毫无感知地以同一效果运行)
（gpt下，2t，4t盘都可以用尽）
使用了grub2上特殊的启动（见接下来贴子里的wuyou链接），和系统相分离的技术，，，不动系统文件本身，系统本身还是原生无改的

不用再傻傻弄二个包分包DD了。

-----------------

以下菜单，会视你的机器是bios还是uefi自动启动进对应菜单项，无须手动（你可以看到下方自动数秒过程，手动会打断这个过程）

（这里的演示图仅贴uefi的情形，bios的已经尝试过了）