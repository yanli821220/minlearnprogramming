---
layout: page
include_in_header: false
permalink: /_booklets/106339776/
---
aliyun,godaddy云主机单双网卡双IP单双网关，同时上内外网新方案和总结
=====

__本文关键字：双网卡双IP同时出网，aliyun静态路由映射，云主机多网卡设置,godaddy单网卡单网关内外网同时出网__

周未闲来无事，又折腾起云主机linux变windows了，具体参见我之前的文章《共享在阿里云ecs上安装自定义iso的方法》，在那里其中遇到的改静态路由部分可谓是十分具挑战，阿里云是使双网卡双网关机器能同时上内外网的教学例子典范，而这款godaddy的云主机实在是太可爱了SSD+共享带宽加5刀一月而且支持虚拟国际信用卡，勾起了我小试一下的兴趣，放心我不是打小广告的，所以链接不给了。以下是教程和技术部分（它与aliyun比较属另一种类型即单网卡多IP同时出内外网）：

关于为多网卡多IP段设置内外网同时出网的通用解决方法：

如果提供了双网关双IP，一般外网网卡指定网关，内网网卡就不指定了（因为同一时间只许一个网关出0.0.0.0，也就是互联网，我们一般用外网IP出），这些都可以在网卡的GUI设置界面（就是windows的网卡右击->tcpip属性（->或属性->高级））设定，然后在route print里会生成具体的active route map列表。在这个基础上，我们再加入控制“网内卡”的route -p add附加逻辑部分：使其加入内网网关部分，让其中的流量导向到内网IP。
基本上，单双网卡/单双网关/单双IP/的情形都是这样。
记住这个路子就没错关键是找准技术点比如我摸了一天才明白这是多网卡多IP同时上内外网的不同情形。然后就是解决方法：

aliyun，双网卡内网外网同时上
-----

像aliyun的双实网卡，在文章开头提到的那文章中我提到过。为内网卡添加静态持久路由可以参照文中的未尾图。

godaddy，单网卡内网外网同时上
-----

godaddy网卡比较特殊，godday的一实一虚双网卡（其中一张网卡是用loop back），实际上只有一个物理网卡(virtio网卡)可以操作，另一个可以删除或弃用，属于单网卡，也只有一个网关。

实际上godaddy云主机只有一张真正网卡我也是测试猜的，下面说一下我转到正常思路上的一波三折：

godaddy主机都是有linux脚本的，在机器安装好windows的CD盘中，可以看到有二网卡，正是这个极大误解了我。以为WINDOWS下也需要虚拟一个网卡出来，此时通过web vnc可以看到virtio网卡被设置为dhcp，所有的内卡配置都是对的，但是不能远程桌面，在web vnc中可以ping到其它主机的DNS，选择一些godaddy的内网主机完全可以ping通且浏览其中的网站，可以对于普通其它主机，ping测试可以解出DNS，但接下来4次丢包率100%（有些教科书说法丢包就是不可达，跟那个不可达提示是一样的效果），此时接着linux下设置的思路，我为windows添加microsoft loopback，静态指定其为外网地址，可以上远程桌面。但是在机器内部还是不能上外网的，接下来的工作就是使之上外网。

其linux配置脚本是这样的：

```
 GATEWAY=`/bin/grep "gateway" /etc/network/interfaces | awk '{print $2}'`
 /sbin/ip route del default
 /sbin/ip route replace default via $GATEWAY dev eth0 src 192.169.164.234 proto static metric 1024
```

上面意为把唯一的那个网关，也是默认网关删掉，把它改写为windows下的对应逻辑，一开始我想到windows下并没有route replace，于是百度windows下配置多网卡源地址替代方案，找到dog250的《Windows配置路由时可以指定源地址啦》，但是几经测试不成功可能思路不对并不是人家指导有误。

后来我想到windows命令行netsh指定给ms tcp loopback interface静态外网地址也不行（这个网卡跟我新建的loop网卡ID不一样）。提示网卡不存在。

折腾一天后我终于意识到那个loopback永远不可能出网，因为它出网的数据量永远都是0.

后来知道windows单网卡可以指定多IP，那天试的最多的就是在virtio上静态绑定外内网IP和设置（注意这个顺序先绑）。试了很多次，机器上打开网页终于肯出外网了，像百度之类都可以，才最终意识到，这可能是个“单网卡多IP单网关主机，使其同时出内外网”之类的问题 — 这正是aliyun的相反或相对情形 。再测试，bingo!!成功。以下是结果图和解决方法：

这个贴图中的IP我也就不mark了(10.192打头的是内网IP，192.169打头的是外网IP，网关只有一个10.192.31.254),重点是绑定IP的顺序和针对内网的那二个持久路由。



-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106339776/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>




