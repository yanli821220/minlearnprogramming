---
layout: page
include_in_header: false
permalink: /_booklets/106607485/
---
一个netdisk storage backend app webos和增强的全功能网站云设想
=====

__本文关键字：利用网盘空间,network filesystem代替静态网站空间,做成静态网站的动态模块,利用v2ray,nginx给onedrive+onemanager做自动cdn,利用网盘代替函数计算__

在前面《利用大容量网盘onedrive配合公有云做你的nas及做站》我们说到用网盘空间达成网站云和用网盘做附件床，一般这样的云网站方案中，静态html都是用oss做的空间。但其实配合oneindex等程序，网盘也可以存放md资源。直接in memeory servering md pages成html，这样网盘+云函数空间或ecs，就不仅可作为附件床了，甚至可以作为静态网页生成器空间。达到全功能网站云的效用（配合下面的内容加速甚至可以代替cdn）。

包括上文在内，我们所有的努力是让网站app和网站资源，聚合进一个网盘 as nas中，网盘网站通过客户端挂载后，可以本地文件形式一个一个编辑和同步，也可以直接在远程编辑md，类似mediawiki和gitpages在线编辑。网页和附件可以统一打包备份。服务于你的中心nas库建设(onedrive as nas)，一套下来可谓省事不少。


利用网盘直接展示和写作静态网站，自建静态展示空间
-----

依然用前文的onemanger来举例，我们可以把静态网站的md文件按树形层次文件夹组织好，文件夹名即为文档标题（当然可以稍为处理一下，标题中不要出现特殊符号），然后一个文档文件夹中放一个head.md，它里面放主要文档内容因为它主要是在页面前面显示的。如果你的文档文件夹只有此内容部分，那么接下来显示的就是一栏只有一个head.md文件的附件列表，如果你的文档文件夹中还有其它下载资源和资源需要说明，可以在这里上传（或通过网盘上传）再放一个read.md，read.md效果会出现在页面下面，，如果是非文档文件夹和非文档子文件夹，就光放下载资源就可以了，一个页面除了文档部分就是附件列表，附件列表就相当于做成静态网站的动态模块（评论模块处）。整站主页嘛，就在网盘根下放一个head.md。

这样下来，一个利用网盘展示markdown网站文档的效果就达成了。

你可能需要定制一下把head.md和readme.md隐藏这样效果更好，在后台设置就好了。Pagenatior可能也需要处理一下更美观，—— 如果一文件夹下有太多下载资源或文档子文件夹的话。你当然还可以再定义主题风格。

网站可能还需要一些强化，因为纯粹依赖网盘没有本地部分，可能网盘一旦挂了，网站就空了，所以需要提供虚拟目录的功能，即网盘程序会挂载本地目录作为跟外来网盘同级的文件夹展示，你可以在这里放一个由markdown组成的备份网站（或者指定部分文件夹自动从网盘缓存到本地servering，如markdown网站所在文件夹然后挂载，后台有某个开关切换展示本地缓存的网站。）。如https://github.com/reruin/sharelist支持虚拟目录。可以本地和盘内共享一个域名。

内容加速，自备cdn
-----

onedrive官方的外链速度由于在港区和新加坡，跟轻量机的带宽一样，也分闲时忙时，深夜凌晨快，白天很慢。那么有没有办法为网站加速吗，如果你托管onemanager的云主机是港区轻量再好不过，流量充足30M带宽。虽然转发是建立在轻量线路其实也分闲时忙时的提前下，但假设轻量线路比onedrive线路好，至少可以一试。

用二种方案，在服务器nginx加速，在客户端v2ray加速。服务端加速就是通过利用Nginx反代加速Oneindex，让Onedrive流量通过服务器中转，解决Onedrive在线播放视频下载慢等的问题。Nginx处和Onemanager处理处(支持sharepoint.com的反代)都要设置一下，

客户端v2ray嘛。不用介绍了吧。话说，如果v2ray也像网盘api一样。可以通过编程方式给内容加速就好了。提供api就接入了编程。

利用网盘代替函数计算,直接托管云程序cloud demo，自建脚本空间
-----

我们知道网盘自身没有计算能力，必须要搭配函数计算或云主机调用其开放api才能调用其中数据为建站所有或用于nas目的，但如果在网盘中托管的是非静态数据，而是程序或脚本。然后考虑通过搭配云函数或云主机去运行它呢？？vs 渲染静态md成html，这里是运行脚本，呈现结果界面。比如，可以用于展示自己收藏的脚本并让用户点击launch it看到运行结果。形成自己的online demo repo —— 类似我们之前的折腾《使用群晖作mineportalbox（2）：把webstation打造成snippter空间》。脚本形式放网盘，还可以一同参与备份（网站数据和代码一起备份）。

这种方案有点接近让网盘具备云函数能力，与jupyter和herku容器这样的东西重复。这些都是利用脚本语言的runtime做程序执行机制的变体技术，比如，云函数计算实际上是将语言 Runtime 本质上是一个 HTTP Server, 再为web建立api机制而已（api,zeromq，消息件,restful也可以）。—— 当然，接近归接近，其本质并非如此，我们始终用的是网盘的存储能力它本身并不具备运行能力。只是可以作为一种折腾方向，不过值得一试，比如通过在onemanager中增加相关功能达成。

—————

最近转到腾讯云了。发现其优惠力度和实用性比阿里云还大。尤其是618或1111，1212时的新购1到2折，所有主机还是100%CPU和5M带宽，企业用户更是优惠，这实在比抠抠嗖嗖的某些云服务商要好，很适合做云桌面(阿里云只有一个港区云轻量还算物美价廉其线路还是分忙闲的)。你可以赶在618新购，然后下一个3年用家人的再新购，腾讯函数云网站做成小程序可以接入大量微信用户。。3年1500左右是我的理想投入，因为一台手机3年就刚好报费。视云主机为托管实体机的成本考虑就很容易理解吧。618的onedrive也几乎半价，仅官方版，

要购买互联onedrive参照https://docs.microsoft.com/zh-cn/microsoft-365/admin/services-in-china/buy-or-try-subscriptions?view=o365-21vianet，也是导向去买官方onedrive的网站购买，https://www.microsoft.com/zh-cn/microsoft-365/compare-china-global-versions-microsoft-365，互联只有Microsoft 365商业版，它是 Office 365 的升级版,(单用户43一个月，包年36，由于疫情听说包年有6月免费)没有官方细分的个人版和家庭版,每个用户都是1t加很多附属服务（商业基础只有web office），我们知道，windows是使用域的。世纪互联和windows官方用的是windows的基础设施搭建的onedrive，使用的登录域完全不同,二套产品是分别开发的，api支持和客户端支持情况不一，因此在接下来创建帐号时域名位置就可以区别看到。互联使用的是xxx@xxx.partner.onmschina.cn。这跟去互联官方azure.cn创建帐买通用云资源和主机创建帐号一样的，不要淘宝买互联帐号，那些全是各种公司的域控下分出来的子帐号（虽然单用户有5t的）而且有各种局限有的没有api权限。淘宝没有行货的互联。除了onedrive计划，互联还有https://www.microsoft.com/zh-cn/microsoft-365/sharepoint/compare-sharepoint-plans这个sharepoint专门计划。72一个月云盘无限容量(实际上就是1到 5到25自提)还可以绑定自定义域控，和享有一个网站。

本人使用的是官方office365+阿里轻量，明年转sharepoint+8元一月的cloud ecs得了。

————

关注我


-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106607485/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>



