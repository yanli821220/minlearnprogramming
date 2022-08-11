---
layout: page
include_in_header: false
permalink: /_blogs/howtoddgcp-md/
---

这是gcp的静态ip机器，多盘


记一次在gcp多盘机器的dd经验
-----

手动方法：

```
wget -qO- t.shalol.com:8011/inst.sh|bash -s - -n 10.140.0.3,255.255.255.0,10.140.0.1 -d

用ssh客户端连接ip:22，用户名sshd，密码为空
```


疑问问题
-----

wget -qO- dd包覆盖sda后，发现有个sda15 mount 在 /media上，而blkid，也显不出sda1,2,3

mount /media
fdisk /dev/sda w一下，显sda1,2,3

