---
layout: page
include_in_header: false
permalink: /_docs/ciintro/en/
---


what is onekeydevdesk ci.sh
=============

in fact ealier in the brief summary of inst.sh,we demonstrate onekeydevdesk ci and its relationship with onekeydevdesk

in all words,the relationship bwteen them are:onekeydevdesk is onekeydevdesk ci.sh codebase

codebase structure
------

onekeydevdesk和onekeydevdesk ci.sh是：


```
onekeydevdesk是包含inst.sh的源码基础codebase
源码所有的更改在onekeydevdesk ci.sh端所处的源码处发生，并编译成一个inst.sh和一些target
之后,inst.sh -t可以DD这些target
```

高级
------

这里还将介绍onekeydevdesk ci的源码结构：


