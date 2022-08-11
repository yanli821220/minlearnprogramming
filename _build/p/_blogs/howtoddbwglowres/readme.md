---
layout: page
include_in_header: false
permalink: /_blogs/howtoddbwglowres/
---

搬瓦工10g512m是一台普通难度的机器，唯一的挑战是没有挑战。要说有，就是镜像要满足等于10的，内存512M这个条件，还能DD且使onekeydevdesk工作



利用inst.sh在bwglowres上dd
-----

自动方法：

```
wget -qO- 1keydd.com/inst.sh | bash -s - -t deb或你的gz直链
```

手动方法：

```
wget -qO- 1keydd.com/inst.sh | bash -s - -d

用vnc客户端连接ip:5900，密码为空
```


利用ci.sh定制spt上的dd
-----

```
          ## bwglowres
          #sudo sed -i "s/export[[:space:]]custIMGSIZE='20'/export custIMGSIZE='10'/g" ./ci.sh
          #sudo sed -i "s/export[[:space:]]tmpTGT512MEM='0'/export tmpTGT512MEM='1'/g" ./ci.sh
          #sudo sed -i "s/imgsizeinfo=\$TARGETDDIMGSIZE/imgsizeinfo='10'/g" ./p/31.remaster/ci2.sh
          #sudo sed -i "s/gitee.com\/minlearn\/onekeydevdesk/gitee.com\/minlearn\/onekeydevdeskbwglowres/g" ./ci.sh
          #sudo sed -i "s/github.com\/minlearn\/onekeydevdesk/github.com\/minlearn\/onekeydevdeskbwglowres/g" ./ci.sh
          #sudo sed -i "s/_build\/onekeydevdesk/_build\/onekeydevdeskbwglowres/g" ./ci.sh
          #sudo chmod +x ./ci.sh && sudo ./ci.sh -b 0 -h 0 -t onekeydevdesk
```

