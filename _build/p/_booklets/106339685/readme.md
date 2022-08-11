---
layout: page
include_in_header: false
permalink: /_booklets/106339685/
---
统一的分布式数据库和文件系统mongodb，及其用于解决aliyun上做站的存储成本方案
=====

__本文关键字：mongopress安装，0维护网站系统,web程序静态资源/媒体文件维护/备份,阿里云mongodb__

从本地打包技术到分布式存储中的做站媒体维护
-----

在大型本地程序的客户端发布中脱离不了文件系统/打包技术， — 这在游戏技术中很常见(看看大型3D网游DATA中的那些动则几G的资料片/资产库文件就知道了)。比如，zip包也是一种简单的文件系统。不过更复杂一些的场景，比如发布大量小文件还需要维护更新和版本化的时候，往往用打包+hash+加密技术(一个索引一个存储库)，像warcraft系列的mpq啊这些都是例子，就不细说了。

事情到了WEB和做站，同样地，WEB的静态资源往往有时变得很巨大，有图片这种小文件也有大文件存储这些需求，我们来细细分析 — 在其底下首先是分布式存储和其各种方案，从服务器上的raw filesystem，分布式文件系统。到简单的ftp，webdav(支持统一客户端同步etc..如owncloud和davros),到网盘的切片文件系统(支持秒传,如dropbox)，到对象存储技术（es2,aws,aliyun oss）,到传统数据库和它们的结合体如mysql+fuse文件(aw3fs,okasoft)，甚至像基于云计算渲染的游戏中免发布客户端资源做成stream,都可用于操作和存储网站文件。我们现在的web栈也往往都是一个httpd的page ui srv + 一个数据库srv + 具体WEB程序维护的程序数据库条目索引本地文件或分布式中的文件，可见，对存储的处理是通用web栈中一个基础环节。

然而，现在的以上这些，都涉及到不同的技术显得太碎片了，同是存储却用了不一样的多种不同质的技术，而且都不能使web做到像本地一样存储维护网站系统（除了OSS可以挂载到本地盘稍微有点接近这个之外）。这使得维护网站静态资源过程往往变得很痛苦，那么有没有一种像打包文件的本地方式一样维护/备份网站系统。统一备份网站数据/媒体，且避免像wordpress这种紧绑定媒体和数据库不好备份的缺点。更进一点，可以做到像dokuwiki那样免数据库一样，发贴即存储，打包复制带走即整个网站维护。

ps:整合的东西往往有一个干净，简单的门面。可以改造成各层开发者适用的版本，稳藏代码后面的复杂。这其实是现代开发，在源码处理（语法上）和发布上（组件技术上）的通用技术了。软件抽象和设计模式中的门面，都是这样的例子。整合的东西还可以提高应用的简便性。
而我们的工作，就是使web stacks中的存储自成一体，使之变得更整合更易维护。本站以前的发布/演示中，ocwp,cmserpone都是在一定程序上使媒体维护变得免维护化这样的例子,owcp用网盘作媒体后端，备份即同步网盘,cmserpone是导出一个公司的db。而接下来介绍的mongodb更像是一种突破。—– 与oss不属数据库技术不同（它是干净的分布式存储），它是一种称为文档数据库，此文档二字即为网站资源，它具有gridfs本身就是一个文件系统,整合了mysql和fs。同时可用作mysql存储程序数据，你可以将它视为mysql+oss,或native storage backend for web apps(that shipped with webstack as ehanced lamp)，是web栈中一个很合理的整合存在。

mongodb与在阿里云中省事/低成本/免坑做站
-----

阿里云是这样设计ECS的，在其产品计划中它把ECS作为计算产品出售，并不是一个带存储/计算的全能iaas产品(如果你要这样做，技术上是可以的，但是成本很高，ecs在安全/负载/流量方面没有优势不利直接建站，而其存储类产品有这方面的设施和价格优惠)，因此云存储中，有oss,ecs文件系统，块这样各层的东西，包括rds,mongodo这样的存储产品。比如，在iaas层，阿里云希望用户搭配使用ecs+rds。

甚至有负载ecs,更甚至，根据这些，阿里向用户提出游戏解决方案电商解决方案，搭配使用的方案。

but,这太乱了。而且其存储成本组成，不但包括存储本身还包括存储中的媒体产生的流量。

我希望有一种方案。像ECS一样全包但是不要涉及太多产品和计费方案。只涉及到最多二产品，且避免ecs的以上做站的短处，再来搭配ecs。aliyun Apsara for mongodb+ecs就是这样一种，内网中的这二个产品流量是免费的，mongodb中的出流量是免费的，ecs按量收费仅放web程序应该不会产生太多流量，这样流量带宽方面综合起来比较划算。ecs+rds for mysql+oss也可以，但是这处方案至少涉及到三个产品。

在mongodb这种方案中，你仅需要租用mongodo即可，外带一个支持程序的空间（比如阿里云的免费PHP空间），在程序支持方面，如果你是个人博客，可以选用比如mongopress,或成熟的nodejs+mongodb的mean stack系列下的app（不过这样你至少需要一个ecs，因为aliyun ews中的js下架了）。

安装方法：下载mongopress 0.2.3放到apps/wamdata/source下，默认密码admin/admin安装,然后在安装成功的后台点导入数据，下载plupload 1.5.1，解压2个文件plupload.js，plupload-html5.js覆盖mp-admin/js/plupload/中的2文件即可。

下面是我在msyscuione+ocwp使用的wam/wnm架构中测试的结果：


——————–

当然它aliyun Apsara for mongodb也不是不贵，合租mongodb才划算，，体外话：对于降低个人网站最低成本和同类产品的自然整合考虑，我最初的想法是mailbox当网站空间的附件呢并把它发展为像owncloud这样的东西，不过还是偏向到web这块来了，那个想法有点疯狂有点像web1.0时代的google openwave设想。不过openwave现在也有成功的替代品了。叫什么来着我忘了。。


-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106339685/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>



