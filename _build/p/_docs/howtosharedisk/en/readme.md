---
layout: page
include_in_header: false
permalink: /_docs/howtosharedisk/en/
---


怎么样当共享网盘：
-------

继上次给pve添加子机透出panel面板后，这次,作者又添加了子机主机共享文件功能，子机也可以通过10.10.10.254这样的主机内网址获得主机/var/lib/vz/shares中的文件和文件夹。

这个共享同样可以对外提供服务变身独立分享网盘网盘（external share机制），支持提取码，支持文件夹分享，支持文件地址+提取码形成wget able的直链，支持按次提取。