---
layout: page
include_in_header: false
permalink: /_blogs/howtoddzzidc/
---
景安的快云VPS跟早期的阿里很像，它有二张网卡

这个属于典型的双网卡抢占出网网关的路由问题，导致表现在debianinstaller界面没有网络连结

也是成功了

方法是把公网IP那张卡的网关给route default gw就好了

这里的经验是：（以下经验任何dd都适用）

经验一：在di弹出窗口叫你配置时，不要去配置，不要去配置，它会冲掉你手动打ip命令配置出来的效果

经验二：di没有网络管理器的功能，不可自动生效，但是一般有dns管理器功能，如果8.8.8.8能ping成功（最好用-4 -c），dns设置也要手写一个配置文件，会自动生效，此时再ping google.com即可