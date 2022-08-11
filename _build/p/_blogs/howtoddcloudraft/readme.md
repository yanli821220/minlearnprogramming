---
layout: page
include_in_header: false
permalink: /_blogs/howtoddcloudraft/
---
这个厂商做的机器配置和性价比还是可以的。其它的也轮不到我来说

机型是典型的用pve虚拟出来的机器，难能可贵的实现了一套多用户自动恢复的功能，不过听说要自己扩展硬盘。
我记得还有人找我写过一段脚本，如果cpu三次100%的，就给他重启的脚本

也是DD成功了

这里并没有网络问题，这里的经验是：它的grub貌似安装有问题，而一键dd脚本跟grub有关，此时卸载掉旧grub，直接重装一次grub，配置文件正常了，一键dd即可。