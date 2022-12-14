---
layout: page
include_in_header: false
permalink: /_booklets/15610692517369/
---
免内置mysql和客户端媒体的kbengine demo,kbengine通用版
=====

__关键字：kbengine换外部mysql数据源和外部客户端托管地址,kbengine js demo外部托管 黑屏,kbengine外置mysql__

kbengine的引擎意义
-----

kbengine是一个优秀的游戏服务端逻辑引擎 大于 其作为游戏服务器引擎存在的意义（假设游戏应用域架构首先按CS这个粒度来分脱离不了服务端客户端之分的话 — 当然并不排除更广泛的游戏方案域抽象将CS视为低级抽象），它为游戏APP定义了一个appstack。就像GAME界的WEBAPP一样，开发游戏就是开发一些gameapp（人类总是要研究终极之道），你也可以叫它WEBGAME engine.

然而此WEBGAME指的并不是客户端富网页技术和微端发布那些,而侧重指的是其使用了WEB的开发发布模式，是GAME界的“WEBGAME引擎”（对GAME这个东西方案域和程序域开发发布通观的总抽象），首先要说的是它运用了广为流行的CS和BS架构，

1，它分开了游戏C端和S端，使得不同终端平台上的C端可以共享一个服务器，而服务器上，可以同时共存很多游戏。你可以叫他们assert,mod或其它什么东西，呆会详解

2，其次，它隐藏了开发者需要从0开始面对的所有东西，它封装了协议，甚至最终的游戏逻辑定义，它并不提倡直接对引擎开发，开发者仅需要定义游戏领域逻辑。它透露给开发者立马可工作产生一个游戏的那些方面（服务端的游戏编辑器，当然带点开发）

3,重点在这里——它封装的程度是使用户（包括非专业的）只需要作换装和UGC就可以开发出一个游戏的功能，就像客户端的gamestudio一样，而且kbe是游戏容器。它像WAMP架构一样，负责运行，整个开发发布就像WEB界成熟的那些框架和应用服务器一样。当然还有开发范式。

谈到UGC，这其实也是WEB应用的方式。WEB是开发更是应用，它使用户直接参与程序（内容）建设。

总之，mod+ugc，这一切，使游戏编程有了终极游戏编程的味道。这也是当今所有领域编程最终要达到和到达的境界。

> 什么是终极编程，编程的最高境界是什么
 
> 终极编程真的存在,然而并不需要是类似编程葵花宝典之类的东西，我们可以理解让编程体现为适可而止，有止境的境界，在工程上(编程上让事情变得越来越容易最后不需投入或极少投入再学习成本)，通往其的方法可以有很多种，但一种无疑是那种直到脚本和可视编辑器的封装。就像WEB前端，以及上面的GAME MOD开发一样。
如果编程方法可以归结为一门最终的哲学，学者可以利用它举一反三，完成自举学习，那么这种元性质的哲学，就是终极。
图形界面的出现和DLL API机制，VB可视化，在这个意义上都是伟大的铺垫作品，面向对象也是一种终极编程，它在语言内在抽象接近平民，各种OO范式，PME，再后来，框架容器，都是使编程变得终极的方法和基础工作。
kbengine只是运用了所有这些（当然还有更多，比如接下提到的持久机制）。
kbengine的程序技术

在程序技术上，KBE使用到了分布式架构和传统服务器多载的方式，它的各个部件可以分布式存在不同物理机甚至进程中，扩展负载，本身作为分布式云存在。

然而，以上所有这些，都不是重点，KBE对“服务端游戏逻辑”的应用抽象，才是它的根本。它将一切抽象为实体，空间，等等，它首次提出了对游戏逻辑->世界的抽象，这种方式下，它完全可以视RPG/RTS为同一个游戏(准备地说是游戏虚拟世界)。因为可以共享一个服务端的世界。产生区别的仅是客户端。可以产生混合的游戏世界。

其次，它对于协议处理，数据定义，这些方面也有自己的创新。特别是它对组件和XML持久数据的应用。这些都是让游戏编程变得终极的方法（硬要给点提示的话：持久化和XML语义化=使数据与逻辑对接，让数据化代码转领域逻辑的终极手段，将不可见的黑箱逻辑变得可编辑hook到用户可视化操作，跟脚本变量，数据库，ORM等，都有异曲同工之妙）

未来会专门详细一篇文章分析其架构。

修改kbengine使得mysql和客户端可外置外部托管
-----

原KBE引擎python,js,cpp都是大小写敏感的，作为混合编制的程序体系，一个kbe demo要处理这些，kbengine官方的方法是强制验证大小写。规定mysql.ini大小写。这使得对mysql环境有限制，这里谈的即是让kbengine换外部数据源和外部客户端媒体文件托管地址的方法。

这里所用到的是0.9.4的kbegine src和js demo.

1，首先cpp src端要处理一下，在src\lib\db_interface\db_interface.cpp中将如下三行注释：

```
//if(ret)
// {
// ret = pdbi->checkEnvironment();
// }
```

2，在kbegine asserts设置文件中，server.xml中，强制外网IP为某个IP：

<externalAddress> 115.28.103.100 </externalAddress>

3，改动最大的地方，.py中有大量大小写要改。media js中要改。

首先，Main.js，IP换成外网地址，然后将client media放到外部托管环境中发现大部分加载黑屏是因为JS大小写敏感获取不到正确的类名：

方法：在chrome F12下，不断测试，找出monster.js,npc.js,avatar.js,gate.js,account.js中的KBEngine.xxx中的xxx要改成小写，注意文件名中的大小写不用处理

以下是最终能运行的测试图，



下载地址及相关msyscuione程序包见原贴，之所以不发具体地址是因为地址经常会失效。只能维护在原贴了，原贴也有本文新增内容及错误堪正方面的修改。

以后demo发布类带下载的文章基本也会这样所以第一时间找不到资源请去官网谢谢。


-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/15610692517369/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>



