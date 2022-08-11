---
layout: page
include_in_header: false
permalink: /_booklets/106338101/
---
在阿里云上安装黑苹果的一种设想
=====

__本文关键字：在阿里云上安装黑苹果，省事方案之把osx icloud当nas用__

我们为什么执着于在云上安装黑苹果，其实我们的目的不是使用osx的工具链和编译环境，以我个人来说，我只是喜欢iclouddrive。它有着极快的同步速度，和极科学的同步算法。而且与finder集成。使得osx即nas，可以很容易做成异备，而且它的客户端app即服务端app的结构，使得如果本地osx结合云上osx，能容易打造出一台省事的nas。这些在前文《聪明的Mac osx本地云：同一生态的云硬件，云装机，云应用，云开发的完美集》中我们都说过。

在《在阿里云上装黑苹果（1）》和《在阿里云上装黑苹果（2）》文我们讲了一些有关这个话题的可能性和资源。

uefi可以理解为就是一类pc（支持uefi代码的），另一类就是我们用了很久的bios机器，强调机器是不是bios或uefi，主要是它们与os安装这个关系上产生了联系，有些os同时支持bios和uefi下的安装，有些os仅支持uefi（最新的osx），有些pc可以同时工作在bios或uefi下。（通过开机设置切换）有些只能工作在bios下(如guest云主机）。——— 即，bios,uefi是机器从固件上如何工作与os安装支持发生关系的二种方式。

要让这个uefi发挥作用，在安装os时，特定uefi firmware往往安装在硬盘中某特定分区，所以它又涉及到了分区格式。一般地，bios机用mbr，uefi机用gpt，现在的机器，一般可以这二种方式，现在的os也一般同时支持bios+mbr方式或uefi+gpt方式安装（2者居1）。当然，也存一些混合的方式和分区格式可以允许某os从mbr+gpt分区上安装启动（如bootcamp）。但要实现直接让一个不支持uefi的os支持bios方式安装则要难得多，—— 这里的本质问题，首先是firmware，并非分区格式。虽然相关但前者是机器本身的问题，后者无足重轻。

那么，黑群晖能不能在云主机上安装，问题的关键在于，1，云主机是没有uefi的。只有bios，除非那种能nested kvm的。能以软件方式喂给uefi。2，能不能有一种方式，使得改造osx或找一个特定的osx，使之在bios+mbr也能完成安装，(osx catalina 10.15能经过patch以mbr的hfs+启动)，3,如果2能解决，那么在guest云主机是不是还满足这个osx的其它硬件支持，如cpu是不是支持sse，osx是不是支持virtio盘。4，如果2不能解决，那么安装一种clover类似的启动器能不能帮忙解决(clover这类virtual uefi的作风就是在bios或uefi机上利用软件生造出一个新的类uefi层———能引导osx的固件层。原理与uefi类似)。依赖它guest 云主机不能虚拟成支持uefi，但能引导osx所需要的固件环境就够了。5，启动了osx rececvery是不是就算成功了呢？不是的。osx本体跟黑群晖不一样，不是所有的驱动都做在loader中。系统只是升级数据包。osx recovery跟osx有独立的os级的驱动。正是osx本体的驱动判断cpu是不是支持sse4这些能不能运行的后续过程。

如果2，3，4都能解决，实际上在guest上安装黑osx是完全可能的。我们选择的机型是阿里云的至强cpu类型支持sse4的，kvm+qemu是半虚拟的，所有的硬件中，cpu是host的，但是是直通到guest的，所以也算是guest的，virtio是guest自己的，这样的guest机是完成可以安装osx 10.10以上系列的(裸金属是调度器级别的有专门的硬件，不存在虚拟化，而阿里云机属于流行的半虚拟机和全虚拟化，都在os内核中做了手脚外加CPU vtd支持，kvm,xen属于半虚拟化)。

验症了事物的充要性，（模拟硬件和适配镜像，始终是问题最大的二个坑），已初步排除一个，下面就是完成镜像，制造一个能bios+mbr安装运行的osx dd直装式镜像，这二个过程实际是一个过程。我们可以在本地建造kvm+quem虚拟环境。我们选择的是osx 10.10，据说这个版本最温和可驯，实用性也接近最新推出的osx10.15,其它的版本也可以依理尝试。测试好了。就导出。

ps:这个其实google一下，网上有。 搜索Catalina MBR HFS Firmware Check Patch 10.15.x可得。

话说回来，为什么我们不提倡在云上完成安装过程，使用“正规黑苹果”的那种方式（这个说法不可笑，黑苹果黑的是硬件和loader，跟黑群晖一样，不黑安装包）。因为我们有installNET.sh这样的东西，这更符合云装机的风格。我们在本地，也有工具和资源模拟这样的制造环境。—— 而且，结果跟一步一步安装得到的结果并不矛盾。—— 更并且，有了一个dd image，这样以后在白苹果上安装更方便（不用再依赖recovery或usb那套了，而这，dd这不就是ghost或timemachine吗）。

最终继续实验以实证。把镜像上传到云主机实测，如果不行，反复测试。



—————

下文就是《省事方案之把osx icloud当nas用》，这样省事个人云系列1，黑群，2，黑果，3，自实现，都有了，就算基本有了精神本体了。恩恩



-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106338101/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>




 
