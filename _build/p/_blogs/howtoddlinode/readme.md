---
layout: page
include_in_header: false
permalink: /_blogs/howtoddlinode/
---
linode据说dd windows不会触发tos，

这货后台磁盘设置configurations中有一个boot settings中，要把主硬盘select kernel选择为direct disk，其它倒没啥

否则会一直以grub启动。

cloudcone也是自带启动的。