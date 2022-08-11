---
layout: page
include_in_header: false
permalink: /_booklets/106340440/
---
一种追求高度融合，包容软硬方案的云主机集群，云OS和云APP的架构全设计
=====

__本文关键字：兼容多主机硬件设计，兼容多os，兼容native/cloud程序模型,兼容本地程序/分布式程序。网络操作系统，不是x11,不是远程桌面，不是web nas,不是pouch存储同步。不是远程投屏。__

云在人们的观念中就是远端，它承诺将计算发展成水电煤一样的可被直接利用的资源，与内容和我们本地的客户端或终端接入（所以有了云存储，云GPU等各种传统资源的云化，以及一些或细分或复用的云资源，如云验证，云游戏,etc..），虽然云技术的背后是一层一层的虚拟化，可是它并没有将这种工作进行到我们日常使用APP方面，作为用户，我们还是停在手机上装APP使用云资源的历史情景下 —— 试想一下，我们老早以前就有网络操作系统，TCP/IP这样的C/S程序。可是一直到现在，我们依然这样子使用云。——— 云程序没有过任何改变。它只是将服务端越做越肥兼带更强大的content streaming的改变(比如即将到来的5G)。

稍微涉及到复杂一点的自建云/云系统管理情形下，比如群晖，ECS，裸金属虚拟化，虽然云装机的方式更灵活多样，但我们发现我们最终还是在使用传统的OS来建立和使用云。还有远程桌面，vnc，远程桌面，局域网投屏,wifi display,ip kvm，x11,web界面，这些永远是我们解决操作远程OS的方式。

云APP进化到现在最高级的形式，也就是webapp，它尝试解决一部分问题，可是它似乎依然不够完善，比如，它如同一些本质是”伪remoteapp“一样，永远基于某种远程界面，一部分逻辑在远端。无权直接访问本地资源，且延时较高。

> PS：以上三个问题,表层来看，是因为云APP总有个OS，它与本地分属二个OS二个独立迥异的运行实体，这种现实割裂了我们原来使用本地操作系统操作APP来操作远程APP的习惯。—— 人们一般把兼容多OS称为云OS（如fydeos,openstack,linux,windows,etc..），把分布式APP称为云APP(web算，走socket的也算。。p2p去中心的算，暗网的也算。。)。这些OS从来都是相互的复合，早就被设计成单机OS+tcpip，从来没变过，只是被分布到了网络。所以它不可能有真正的分布式。——— 小到content streaming,vnc，大到开发，甚至一切，都只是权宜之道。。以至我们没有过真正的分布式OS和分布式APP，一直在web的小概念里打滚。见我的《打造一个Applevel虚拟化，内置plan9的rootfs:goblin（1）》，我认为这是因为我们始终把“真正的分布式”做到APP层次。短板理论下所以一切都是伪的。

分布式架构的本质问题是OS和APP的选型和实现问题
-----

分布式架构本质是巨大的问题，这是我们bcxszy一直努力选型与实践的目标,因为有前面文章的铺垫，我们现在深入分析这个问题:

在前文《兼容多OS or 融合多OS?打造基于osxpe的融合OS管理器》中，我们看到，有时为了实用。我们宁愿牺牲少量的性能，选择融合这种折中的方案，而不是严肃意义上的那些破哪补哪直面问题解决问题的打法。 还比如:

1，为了促成能用好用的兼容多OS，从技术层面有二种流派和方案，一种是靠虚拟化，发明一套“OS的OS”，利用这样的元OS来管理guest os，一种是利用经典的再造OS的方法，像龙井，wsl，虽然它也是发展host os/guest os，guest os as subsystem，但与虚拟化流派的做法有着绝对的不同。前者依然是用传统的OS叠加OS，除了hypervisor，容器技术毫无创新，而后者，尝试从问题的源头重新去解决问题，从本生态内去解决问题而不是不断复合/融合（这里没有贬低该文OSXPE+PD方案的意思），如果问题出在最初考虑不周，抽象不够，那么就再抬高一个层次。结果是出来一个单一创新了的全新的OS ------ 这才是主体，其它子OS只是rootfs附属技术。

2，带着这些观点再谈分布式APP，我们发现这种历程正有点像业界对于分布式APP的挣扎和创新，在前面我们不断谈到分布式应用模型的讨论，其中最重要的地方《Plan9：一个从0开始考虑分布式，分布appmodel的os设计》中讨论得最为深刻，在那里，我们提到plan9正是这样的创新。它有别于用传统OS叠加的云化分布式 ——— 正如那些单调的兼容多OS技术一样，而是一种从协议级去创新，去重新发明不同理念OS的一种努力，plan9协议是一种从开发，从内核理念到语言，到APP的变革，去促成不同于现今可见的任一分布式APP的全新分布APP，而谈到协议，它必定是某种上种抽象。刚好在《用开发本地tcpip程序的思路开发webapp》，我们还讲到协议化。使用本地方式开发web程序。将web首先升阶抽象变为协议化的东西这样可以融进“静态web仅为资源”这样的webapp。那文中，我们还坚持一惯贬低了webapp vs 通用分布式app的那些优缺对比，因为它使用传统os，利用appstack层打洞，所以它是分布式OS中极为狭隘的一支，Web绝对是分布式appmodel中最浅层的一个典型。

无论如何，从这二大段说的正是：a,虽然能融合也很不错，不过话说回来。这并不表示能直接解决问题也并不是就不能实现效果最大化，b, ——— OS与APP，本来就是问题的一对最原始中心 ——— 只要先解决这类问题并创新，挖掘发现“真正的分布式APP”才能稍后解决开发，语言和工具。c,而抽象和协议升阶，是软工解决新问题出现的手段。

其中,b是中心的中心。

所以，我们为什么不能做一个真正的OS和分布式呢？

首先来看兼容OS解决多硬件，多主机软硬平台融合:一个多主机环境，跨本地远程，多os兼容的多主机方案设计
-----

前文《兼容多OS or 融合多OS?打造基于osxpe的融合OS管理器》中，我们谈到的是单主机多OS的方案，稍微提到但没有深入多主机方案，我们提到，多OS的需求跟多显示器，多桌面机制一样可笑却实际存在。但其实细说起来一点也不奇怪，我可以在一台电脑上装三系统，一桌面系统用于生产，一类似dsm的系统用于同步文件，人手三件套手机电脑路由器，OS各各不一，未来公共使用的物联网（华为hm os?）。基于容器，OS也不会少。我经常看到和能想到的是，有些人还有二部手机，开发者有二个主机甚至多个电脑，

> PS:多主机PC，这些主机可以要么是Computer as unit，便携显示器加nano itx小主机打造新式便携pc(用一个双系统机箱，或定制一个类双盘位的nas铝盒把这二个主板装上，nano itx 二个是24*12,下面刚好有空位上电池+整机箱上面覆盖键盘键盘就更好了，,打造多主机笔电式机箱）或者直接多nano itx PC集群,随身网吧（直接定制长vesa挂架挂墙）,都可以带着出远门。，最现实的方案：要不就2台pc，一台带typec的笔记本,一台无屏带typec供电的便携显示器。也可以组成至少二主机环境。要么一台有双vesa的显示器，主机在显示器后，二个位。

无论是使用实体现，还是这些实体主机配合使用一台云主机，或全云主机，或云主机加一台实体主机，兼容多OS管理器都能使它们协同工作，我样可以将这些云主机中的一部分分出来一些，比如，负责某些任务较重的APP可以独占一个CPU较强大主机。负责存储的可以独占一台配有大容量存储的主机，因为我们要谈到的兼容多OS主要是在一台机器上装多个OS，负责路由的分在另外一个台机，etc… 如何将这些平台上的OS，以及平台本身用兼容平台/兼容os方案整合起来，使之协调一体，前提是：这一切受兼容OS管理器的管理，它本身是个融合OS。

前面我讲到使用macmini+oray控控的方案，wifi局域网纯软或借助硬件的投屏技术，内网穿透+VNC桌面，或ip kvm显示技术，都可以被舍弃了。因为这是个：远程OS也能被统一的虚拟机以桌面虚拟机同样的模式被分布式管理的架构，如下：

一种mirror to local的远程投屏操作系统，可放在pd
-----

我们在前面《聪明的Mac osx本地云：同一生态的云硬件，云装机，云应用，云开发的完美集》谈到mac的云是一种很聪明的云，它主要将浏览器直接作为云存储的同步客户端，而且通过server app+描述文件管理器，利用caching as sync在苹果不同终端间建立私有线上线下打通的云，而且客户APP和服务性APP同宿一个osx，有别于群晖这种分二端APP的做法。而且它的IDE自带devops，也是一体化客户/服务性APP模式 —— 利用本地浏览器作同步客户端，利用sync+caching同时建立云content streaming，提倡使用客服一体化app ——— 正是Mac显得聪明的几个地方， 一言以概之，mac将云理解为传统桌面的附属，所以在实现上尽量向它靠近。

为什么就不能有一种OS：它将远程的一切无缝mirror到本地，如果远程OS可以被管理，可以像mac server一样，它作为分布式远端的OS，不只是一个远程桌面，而是一个实实在在的与其它OS等同的OS，只是被mirror到这里，所以在本地，有跟远程一模一样的运行状态和所有资源，如果放到PD下，就跟其它虚拟机一样，也即，我们本地会mirror远程机一模一样的状态，如果可以这样做到，为什么不呢？当然，mac也做得并不完善，反正，群晖这种webos，需要急待改进了。

缺少一个真正的分布式OS外观,正是分布式问题得不到真正解决，麻烦开始的地方，必须要在这里攻克它。

是不是还想到了plan9？它将API和运行状态都用本地/远程统一的协议来保存。它可以将nativeapp的四栈全部协议化,包括上面提到的投屏和界面。最主要还是其存储协议化，这种协议不光是面向本地的，也面向分布式。所以plan9是一种协议化升阶OS，它解决的是API,但是这种抽象和协议要向下兼容，即，把远程OS也弄为跟本地一样。

真正的分布式云程序，其行为要类似本地，不仅要从开发层透出API，api as services.而且要mirror出当时的host环境，才能透出整个对应native app的文件系统，等信息。这样才能以类似编程本地app的方式去编程dist app，比如，上传一个文件，你有界面，也有upload api，但是没有远程机器的磁盘信息。更具体点，远程桌面要有上传下载文件。所以，新的applvl runtime，要整合一个xaas环境，而不仅仅是api这些app本身的东西，要么在每个applvl像go塞进去一个vm一样，可以为每个app像plan9一样集成一套9p rootfs，也可以像plan9一样用相同协议的OS来保证这类远程APP有同样的本地/远程互操作性。

其中，第三种方法就可以将这种OS作为管理远程OS的实例，塞入PD，实现本地管理，而不必受到远程桌面之类的限制。有相同的外观。下面谈APPLVL的文件系统外观。


云APP/本地APP融合:一种uniform navtive/cloud appmodel抽象的appmodel设计
-----

我们现在一些分布式文件系统，或oss，或文档数据库最大的毛病，是因为它们在操作系统的粒度上，没有给用户呈现一个类本地文件的打包视图。这些必须做在OS层面。才能给后来的APP提供统一的外观。应该上升到os层作为os的理念。和applvl虚拟化程度。

就如同plan9协议化了分布式OS交流用的存储协议一样，mac osx用finder作云同步客户端一样，统一的文件系统外观，使得可以结合plan9以操作本地文件和界面的方式来操作这些存储，形成真正的storage backend distapp。比如，用于web,可以有，基于化远程可观文件系统的网盘，可以有基于网盘同步的通用webapp设计。

基本，搞定了PD管理器，uniform navtimve/cloud 存储和界面协议。一个app的栈就被完全定义下来了，关键是，这些是按本地原来的用户开发和应用习惯设计的。而不是像web一样打洞，像虚拟化一样造更多雷同的东西（虚拟化只是解决了通往分布式APP问题的平台层及一些层面。更多其它的工作需要完成），而是重新从0开始，重发明，创新包容。也即，为了制造那种nativecloud体验合一的分布式，唯有像plan9一样。从经典的内核，API这些源头做起。

这样。从装机，OS到语言，开发，app，这些最终才能做到最好融合，对于促成一种真正的一种native/cloud融化方案平台和app这一最终目的，才能达成。

———————

Bcxszy用goblin这种被创造以整合plan9rootfs，工作在applvl虚拟级，可用于linux kernel based兼容多OS装机环境的分布式集群环境和类PD管理器，做到平台和OS级的融合。Bcxszy将最终打造一个网盘app用于说明云app/本地app融合的概念的实践。


-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106340440/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>


