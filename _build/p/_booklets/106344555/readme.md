---
layout: page
include_in_header: false
permalink: /_booklets/106344555/
---
软件即抽象
=====

__本文关键字：抽象是软件的本质，设计是编程的本质__

首先，什么是编程，这或许要先问，什么是软件，因为具体编程就是一种“在某平台下，使用某语言，针对解决某个需求进行实现，某个问题进行解决，由程序团队完成最终递交给客户并维护的整个过程，产生的结果就叫软件”，人们只注意到了作为结果的软件，但其实这里提到了很多实体和对象 ----- 整个软件和软件开发，它是一种寄涉众多的人类工程，每一个都不可分别而论。

具体到工业层次的软件开发和应用上，人们最终追求的始终是如何控制软件的生产周期，降低成本。更灵活地处理新出现的需求和软件本身改良的代价 ------ 历史上存在过的，和发展到现在，我们见过的不同编程形式都可以泛性地归入这个讨论。对于大中型软件开发，存在著名的关于银弹问题的讨论。这就是软件工程和开发的标准定义

那么，什么是抽象呢? 抽象，顾名思义,抽象抽象,抽取事物形象的一面, 那么，为什么需要抽象呢?首先,计算机科学和编程是一门复杂性很高的科学，人脑往往不适于长辐记忆或直接面对复杂的二进制底层,人们在面对根本无法控制的事情时,往往把它们转化为另外一件可控的事 - 这对于W事W物都是这样的。其次,**从问题到解决不是一步而就的,所以需要建立中间层**,先完成这诸多中间层,当中间的逻辑被解决的时候,最终的事情自然就变得简单了，还有更多，抽象源于一个简单的事实,把事物从逻辑上分开,这样就会解偶它们之间的联系.只有把接口拉高,向高层抽象,那么就可以忽视平台逻辑(实际上正是正面绕过)，面对一个抽象了的简单化的结果 **比如抽象是历史上在开发中解决移殖问题最好的方法**,而实际上，增加抽象是解决一切编程问题的方法！！（by某某牛人）**软件即抽象。抽象是软件的本质。****抽象足可以被称为“软件原理”**

总之，既然软件与开发在工程层面源于上面四大件（平台，语言，问题与需求，设计与人），抽象就在软件的这些各个层面都存在。下面，我们就从大的工程方面，从编程的最初形态开始，来讲解抽象在这四个层面各有哪些关联和体现。

1)平台和语言层中的抽象
-----

最初,人们想得到一台能高速模拟数学计算的自动化机器，试想只要有了这样一套机器和数学方法，只要机器的速度足够快，形式化的问题有解，它就能在人类有意义的等待时间内产生结果，图灵机的运作原理为自动机理论，它的计算方式被称为形式计算,形式化了的问题就叫“算法”，图灵机理论揭示并解决了现代计算机在抽象层次运行的本质即形式计算.这对计算机发展和工业化的意义不言而喻,.这不光是硬件上的，还是软件上的，

硬件上，出现了冯氏机.冯氏架构将执行指令的CPU和存放程序的内存分开,其带来了可置换软件的雏形 - 程序机器分离。CPU作为主导，集成了对内存的管理,是计算机中的总控制中心,机器运行的过程就表现为通电状态下的CPU从同样通电状态下的主存里取指令并高速译码串序执行的过程.在CPU的眼里一切都是内存地址,指令也是内存地址.** 可见，这里CPU不但执行指令,还管理组织数据的事.-------- 这深刻描述冯氏模型的特征和导致了冯氏编程的统一性.冯氏的哲学观就是数据和操作数据的指令。数据即指令，指令即数据。**

软件上，就是算法。既然在CPU眼里,一切都是内存地址和指令,而且这导致了冯氏模型的统一性.这些仅仅使机器知道如何寻址和译码，至于计算机如何形成任务,它能完成什么样的伤务内容呢? 冯氏计算机是如何把问题-这里是科学计算问题，形式化的呢？最初的人们是如何使用最原始的计算机的呢？------ 这就是CPU级的执行路径，由数据和指令组成的程序分片断在"栈式机"里运行，每个片断在一个个高速生成-消亡的可执行单元里进出，占据CPU的时间资源，CPU有机制直接表达这种栈帧 - 它里面的寄存器，CPU也用科学计算处理单元来完成指令的执行，空间上,CPU用寄存器编址内存地址，CPU也支持编址操作内存中存储的整型和浮点型数据，形成最终组成应用和程序的指令序列和数据址位，最终完成程序的执行。------ 这时的计算机应用当然首先是在一些大型主机上作科学计算不能作通用计算。机器是裸机，这时的软件形式就是一些用汇编写的应用，最初的软件就是问题尾端的应用，,开发上，没有复用，写程序一切都要从头开始，程序是离线开发（电传在另一台同类型机上开发调试），烧录到ROM的，开发过程就是直接电传写裸机上的应用（没有开发支持和安装支持）。软件也不能称为软件（我们把出现OS之后软件称为软件）。

总之，这便是最初可编程(科学)计算机的基本雏形以及开发和应用的雏形。它是图灵理论算法的最原始表现形式(算法可以是一切最简的可形式化，到任何复杂化了的可执行，开发，发布程序形态，但始终不离图灵计算本质的那些计算问题，以下会不断提到)。直到出现真正的软件系统使之变得现代化，这就是现代OS的出现。

那么为什么要出现软件系统呢？

最初的大主机的处理能力太过于空闲,一个当前使用机器的用户对于这台机器的处理时间和处理能力是独占的,机器内没有管控这些程序该如何更好运行，出错了怎么防崩之类的逻辑，而且，不仅机器本身没有自理能力人力管理和使用机器也麻烦，很多很多年前，那时，会编下的操作员和程序员,要完成先控制机器的任务(机器上有重启,暂停等按钮,在机器内也有相应的控制指令)，再使用机器，效率不高也不够方便。更别说开发了。

于是急需出现一种能代替人管理机器的层面和机器管理程序的层面，将其显式地整合进一个随着机器存在的层面直接常驻裸机之上，这个层面就是最初的软件层面，（最初的分时系统，这些层面就逐渐演变为“软件OS”的原型。此时，它可能并不叫“操作系统”。)，再后来，人们自然想到，由于计算机的硬件速度足够快，为什么不到所有能想到的，都软件化整合进这个层面呢？比如为什么不把编程都搬到这个机器和集成到软件层面来呢？这样，各行各业使用计算机的人都可以面对一个统一的，大而全的，更强大的软件层,，普通用户可以面对一个更强大的功能，PC可以接入更强大的外设，供更多人使用，计算机终于开始像个PC了。对于开发者，高级语言完全也可以实现在软件层，软件开发发布就可也在软件层更方便进行，程序员可以直接在软件层实现应用，使用平台上的API，（这里并没有一个显式的OS和高级语言谁先谁后出现的问题，但肯定一前一后紧密，系统和系统开发是一对自然而然的结果和现象，比如OS本身也需要用更好的语言来开发完善，更强大的软件要求出现更强大的开发手段。。）。。

高级语言系统同样基于图灵理论，编译原理即是这样一种学科，发明语言本身用的是”图灵算法“，它为源端的源码建立一套形式表示，映射为可运行的目标逻辑，并传给目标运行（这里的目标即OS执行栈），语法表示和语义映射这样的问题，是高级语言前端的重要课题，由于是图灵原理，它要尽量避免二义性，用计算机来识别的语言只需是(不是只能,而是只需)某种形式语言而非我们的自然语言(如果硬要这样,那反倒是不合理和不必需的,因为自然语言是一种形式语言的超形式,在语法语义层面存在很多歧义,比如一个句子有二层语义,虽然这是现实中一语双关的美妙使用,但是在编程中这正是要极力避免的,仅仅因为不需要那么做,计算机本来就被设计成只处理确定性的算法。

在OS层集成高级语言，不管如何，事实上人们也这样做了，此处略去1W字有了操作系统和高级语言之后的好处 ----- 我们分别着重来说这二者给开发带来的新的复杂性和便利性，

对于开发，OS层为开发新增了一个平台和基础抽象的层面。平台上使用高级语言进行开发，发布，必须遵从和适配OS上的以上服务，调用和处理与此相关的所有抽象，对照原来只有汇编和硬件平台是直接对应原始的图灵运算模式的原始形式，它产生的程序本身就成了某种高级的混合算法态--我们暂时把它称为OS层的功能抽象。如果说OS那些抽象给开发带来的是功能层面的，那么，语言给开发带来的影响更为明显，它带来的是映射层面的整个叠加。------ 比起汇编和汇编语言是直接对应机器逻辑和语言机器逻辑一一映射的。用语言进行开发时，它产生的程序本身也是多种复合了的算法态。

>a) OS为开发贡献的新的功能抽象层有：

>OS带来的程序运行栈：OS为软件准备了一个过程和函数栈，高级语言（我们稍后会讲到）的后端链接产生的程序会链接到OS运行可执行体的服务（它们在语言中被作为内存分配等函数）。
OS层封装软硬平台的服务：硬件的特性会被反映到编程上，编程语言上作为抽象，比如原子操作作为语言关键字。平台的并发有时也会成为软件的直接支持设施。
OS层的API服务：OS为应用准备了一套API，所有语言产生，运行在这个OS上的程序，都可以调用其API服务。
OS层的组件支持：OS上的应用可以以二进制组件复用体的形式出现，进行链接，生成，和运行。
OS也为应用准备一个appmodel，（这个放在领域问题部分来讲。）

>b) 高级语言叠加了一层映射计算方式作为抽象的叠加参与开发。

>首先，高级语言中的类型抽象。

>在前面说过冯氏模式就是处理逻辑和数据的，甚至这二者本来就是一个东西，高级语言会有一个类型系统，这里指的主要是简元类型系统（UDT，ADT这些扩展语言类型的放在跨越语言的复用部分讲），简元类型模拟了汇编下CPU的类型，而函数定义，过程式流程命令则显式化了原先无义执行序列中的部分，使之成为有意义的逻辑单元，冯氏开发就二个东西，数据和操作数据的逻辑,到了这里，类型已经成了一种综合数据结构抽象和代码结构抽象的东西（甚至它还综合了API和接口这些复用的机制。甚至语言的类型系统，OO使扩展语言的库成为一棵关于类型的大树。这放在复用部分），这一切都是抽象，让语言映射呈现出靠人便于使用方面的抽象。

>而语言后端与OS运行栈一起，，完成语言系统的根本任务。

>可见，OS和语言层为开发引进了抽象的叠加和复杂。是不断丰富的平台和语言系统给开发带来的方便性和不方便性产生的新矛盾体，它在带来方便的同时，也带来了这些复杂性。那为什么不抛弃它呢，这个问题问得好，问出了抽象的哲学出身：这其实是一对矛盾。**是抽象的特点。抽象是用更强大的方便性掩盖和代替相对不那么重要的方便**。

2)超越语言的抽象层，及问题域和人的工程需要给开发叠加的那些抽象层
-----

语言逻辑将到现在为止讲到的一切，包括语言本身和平台抽象的部分，都统一于语言服务，或封装在语言标准库，或封装在第三方库,在计算机看来,都是图灵原始算法不断复合，演变的复杂形式和高级形态.最终统一于高级语言开发。

那么，除了以上OS和语言本身带来的新的复杂性和抽象层，还有哪些会随着语言进入开发呢？这就是超越语言的抽象层，及问题域和人的工程需要给开发叠加的那些抽象层。它们超越语言，但也可以作为语言服务存在。比如，将加入人类工程和问题抽象的一次性设计，做成框架，这属于复用部分。

这首先是高级语言时代的算法抽象。

当图灵能解决数学问题的时候，它实际也能解决这种形式化表达的任何通用问题。试想“1个男人+1个女人=？”这样的抽象问题如果能得于形式化，在图灵机眼里都是可计算的，等价的，跟“1+1=？”一样，冯氏机自以前汇编时代就有这种能力，之前汇编的算法我们讲过，就是根据编程上的数据类型（汇编下是CPU的类型）然后按计算机的方法一定套路操作数据形成结果，只是在汇编时代，开发上没有让图灵算法一次演变到这种复杂形成的可能，那么现在正是时候，装配了软件层面和高级语言的冯氏机就正好可以在程序中抽象这些并映射解决这类的复杂抽象形成新的复合算法。并在软件和高级语言时代，算法形成了真正自己的学科。

所以算法，它首先也是个数学和科学问题（用计算机作科学计算）。它超越于具体语言语句和类型抽象之上，（因为它是跨越语言的，算法是计算机的学科，不是编程的学科），是开发界实现最初抽象，利用计算机原始的解法，建立问题域抽象的手段。

>a) 算法层和实现抽象层。

>那么这又是一种什么样的抽象开发过程呢？
>这里面的抽象就在于，VS机器和汇编时代CPU类型和操作法，这里的相当于高级语言中的变量和类型。算法相当于数据结构+数据结构操作。
>它将算法用语言的简元类型来表达成数据类型抽象，进而可以表达成数据结构抽象，然后结合处理这些数据结构的模式，可以提出ADT类型供复用。
>但当谈到ADT的时候，实际上进入了下一步，跨越具体语言的复用层级了。

>b) 语言的接口和复用层,扩展层，继续抽象层。

>分清语言的实现抽象层和扩展抽象层

>在前面不断提及过语言的复用层，一不小心它就总是和语言的简元类型和技法重合，高级语言最基本的类型和用法，过程式和简元类型抽象实际上就是最基础的可复用设施复用支持。（对类型的抽象就是编程设计的冯氏数据抽象思想为中心的开发方式，类型抽象和数据结构是高级语言用语言来解决计算，描述算法的最基础的工具。而代码结构就是复用手段，工程手段。所以提出类型本身，它就是一种复用，甚至这是语言用类型来完成语言本身的手段，比如运行时和库树），不过也有复杂和显式的（比如算法科学中，简元类型可以完成算法，但ADT则是用户抽象扩展的分水岭。）。现在我们正式来归类复用层面给开发增加的新抽象，------ 为什么复用这么重要，因为高级语言在映射层能解决的问题所有问题，就是使用算法实现抽象和使用复用连接已有实现或第三方抽象，扩展用户抽象，除了算法，高级语言的复用支持是语言对接人方面工程目需求那层的 -- 接口和复用。它是高级语言能连接抽象的第二种手段。

>更复杂的接口和复用层有：高级语言习惯用法。tricks，技法，语言的UDT，ADT扩展系统，高级语言的API和二进制复用机制。库级扩展系统，组件扩展系统。过程范式，等


>c) 问题域

>在软件时代，这里的软件和软件开发分系统软件和系统应用软件，系统编程领域，包括OS的发明，语言的实现本身，都是系统软件。上面提到的算法和数据结构，就频频服务于系统实现与系统应用开发。

>问题域为开发引入了什么新的抽象呢？
>首先，一个现代的OS，基本涵盖了对GUI，graphics,network,socket,持久，io，等领域的基本抽象建立。然后，一个具体APP中，最大的肯定是问题本身所处领域逻辑。
>最后，一般OS基本还建立了２个APPMODEL层，一个是console appmodel，一个是gui appmodel，你可以将appmodel理解为程序的模板，其作用将domainlogic+appmodel形成最终该OS下的一个具体app。

>d) 人带来的新的设计抽象层面。

>当考虑到人的需求，它又是一个更高级的，超越语言和问题域的话题，归纳一下，它为现代开发引入的新抽象有：设计模式，比如设计模式，可以在很高层次上，为问题建立一套MVC的框架。

>甚至更多的语言，如带来了脚本语言，更强大的虚拟机语言这样的课题。和领域语义，如xml, 中间件，更细分的appmodel和问题域抽象，web appmodel,game appmodel这样的东西。，你可以将它看作为是对前面1)a,b,2)a,b,c的全盘设计，修正，选型，创新，和附加，和全盘颠覆。或部分全部直接采用。
>如QT框架库，它是对CPP语言，平台库，等等，这四个东西的封装，修正增强，这里有鲜明的重设计特征和工程总层面进行开发的痕迹。

3) 总结：软件和开发的原理和模式-如何建立抽象，给问题建模，复用（扩展模式）和映射抽象，处理平台抽象
-----

所以，看出来了吗，软件和开发的原理和总模式，其实就如何2)中abcd一样，已经证明是这些抽象不断叠加或修正的过程呈现。而人类设计，它是对1)a,b,2)a,b,c。的部分全部直接采用。或重设计。最终，通用OS和高级语言如何解决新时代下，解决程序运行和开发的问题，就是解决如上抽象和设计的问题。

比如设计模式，当谈到设计是，表明这是一种人类设计。将加入人类工程和问题抽象的一次性设计，做成框架，这属于高级复用部分，同时又是典型的设计。

-------------

这是《编程新手真言vol1:编程新手抽象与理论》下文我们谈设计，编程即设计，



-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106344555/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>



