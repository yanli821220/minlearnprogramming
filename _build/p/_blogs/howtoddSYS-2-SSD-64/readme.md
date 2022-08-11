---
layout: page
include_in_header: false
permalink: /_blogs/howtoddSYS-2-SSD-64/
---
SYS-2-SSD-64 Server - Intel Xeon D1540 - 64GB DDR3 ECC 2133MHz - 2x 450Gb SSD NVMe Soft RAID

一键盲D

d成功了

这里面的坑有多少呢。。

1，它有四个网络uefi，一个本地硬盘uefi，四个网络是用refind做的。不够原生也不好用。
来看本地硬盘的uefi

这个本地uefi固件强行绑定了一个windows boot manager(由于我本人没有sys2辅助别人d的，我怀疑这个是另外一个盘的残留，一般uefi是遵从硬盘原始uefi逻辑的，虽然可以但没有绑定boot manager的必要)，这种行为像是linode强行绑定grub一样，后者可以取消，前者无法取消

所幸这种绑定是路径级的，你可以用grub efi代替，然后用我的二合一镜像分区稍微调整下配置文件即可启动系统。

恩恩，我也已做好定制镜像。