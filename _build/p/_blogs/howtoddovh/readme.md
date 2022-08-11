---
layout: page
include_in_header: false
permalink: /_blogs/howtoddovh/
---
前几天协助个MJJ给ovh做dd，其实我没有拥有过ovh的任何产品，只玩过ks，听说它有sys，ovh，和ks三个型号的产品和官网

也最终成功了
方法依然是ip命令一把梭

这个主机听说是独服开出来的，肯定不是自己装pve装esxi弄出来的，应该是ipmi开出来的，否则不会弄出这么复杂的网络结构：

表现也是在debianinstaller界面获取不到ip
另外，它的网关和ip不是同域的。这是常识了，其实一台机器可以有多个dns和多个gateway，但是路由上，只允许同时一个gateway出互联网，其它的gateway大概是做内网用的。

比如：54.39.xx.xx通过内网的192.168.2.7出网。这种

记忆中，还有二种在di界面无法获取ip的例子：

1，多网卡
2，需要借助网络邻居发现来辅助路由的。