---
layout: page
include_in_header: false
permalink: /_docs/howtopanel/en/
---


怎么样当面板：
-------

安装devdeskos

然后可以在任意一个lxc中安装8080端口的web应用，在panel8080中，就能看到。未部署8080服务前，显示502 Bad Gateway
（请保证lxc ip和lxc id相同，比如10.10.10.252与101010252是相同的）

比如安装bt后改端口为8080，就成了web面板
为什么要在pve中内嵌面板：因为这样可以让面板借力pve的异备，集群机制

还可以用pve的多集群。异备

有时想想：这才是lnmp面板的正确存在方式