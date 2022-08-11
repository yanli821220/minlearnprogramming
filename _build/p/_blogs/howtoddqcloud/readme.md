---
layout: page
include_in_header: false
permalink: /_blogs/howtoddqcloud/
---
di在进入低内存模式时，会出现很奇怪的问题，就是正常安装一段时间的udeb后，可能出现再也继续安装不下去了的情况，这属于di是在内存中工作，是用内存来安装udeb的原因

而此时，远远未进入到正常系统，是无法使用虚拟内存的。

也是成功了

原理是：及早加载硬盘驱动，划一片swapfile给di，这样，就克服了内存不足问题，可以使dd过程继续，然后dd完自动解除swap，因为它被覆盖了