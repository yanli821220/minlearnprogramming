---
layout: page
include_in_header: false
permalink: /_booklets/106344586/
---
clingrootsys原理剖析(1):JIT到底是怎么回事
=====

所有的高级语言技术，都是由前端的翻译转化，源码理解，和后端的运行技术和语义实现的: 即编译-链接-运行循环这个标准过程组成的（真正了解这个三段式过程，无论是多复杂或复合了的语言系统，给其定性将不再是难事），而且其编译器实现一开始都是以静态过程式、函数为实现机制的。都是C语言和标准编译原理教程那套。而高级和复杂语言实现，都是先过程元素，然后再在编译器前端实现语法增强，或封装到class和库级增强实现的。（而真正分清这个，可以分步理清很多错综复杂的编译原理过程。 特别是cling这样的复杂语言系统的定性和实现原理。包括其实现，如JIT和库级pme都大有帮助。下面细述。

什么是解释系统
-----

解释系统与编译系统最大的区别是在一个前后端配合循环(标准编译原理上的compile-link-run，实际上这里的compile更适合称为translate才能与其它语言共享同样的编译子过程称代而显得无歧义)中，它每次只取一条代码（最小生成和执行代码的单元）来运行，且纯粹依赖语言系统本身的后端—-往往是一个软件系统 来运行，往往无需link，因为它是运行期完成query的，类似组件（接下来本文第三部会说到这个组件有什么魔力）。
这里的软件系统运行设施往往还负责其它方面的工作—比如一个虚拟机要完成的那些当然也有可能不像虚拟机那么复杂，就是一个简单的if-case流程（这是最初脚本语言的原型），它属于整个语言系统的一部分，所以说是在线解释。由于它在翻译和链接过程中是运行期实时完成的，运行期的那个大VM天然维护着这样一个软件从翻译到运行所需的全部设施的宠大环境 — 它就是整个软件化的语言系统连执行都是软件托管的，所以在前端它不耗时（较编译系统而言），耗时的是运行期的代码效率。
而编译系统是事先将整个应用一次全翻译好（这里耗时巨大），将每个模块链接起来（这里又一次耗时巨大），依赖后端-往往是一层薄薄的支持层仅起传手传递作用 – 传递喂给机器offline运行，此时的运行不干语言系统的事所以说是offline。由于机器执行机器码是2的8次方这个效率（这个数字还在不断增长），所以自然就快了。
解释系统每次只执行一个代码的本质无非是在编译器实现中在后端提供一个execframe对象就能达到，使语言系统具备生成动态最小可执行单元，比如一个调用路径中的函数栈，然后将代表其的ast node喂给后端执行时-那个execframe就行了。解释语言最鲜明的技术特点就是这个动态执行后端。可见它跟是否必有一个虚拟机没有关系，跟是否必生成中间码或平台码，或以其为最终目标运行没有关系。它就是一个普通后端会“emit function->feed it to execframe”的东西，免compiler免link，后端直接运行代码（一般运行后端可直接识别的中间码）的东西。
我们称以上这种解释系统称为普通解释系统。
令我们迷或的往往是JIT式的解释系统。而实际上，它是普通解释系统加了“以平台码为翻译目标和运行目标”之后的解释系统。这里详述：

Jit到底什么东西
-----

JIT有什么特别，你依然得联系到标准的三段编译原理过程来解释它，即translate->link->run ,jit也被称为jit compiler,jit interpter，那么jit顾名思议，jitcompiler=jit translator，是语言都有的，所以这不是它的特征，而我们立马发现其有jit interpter，如果说到现在为止提到了解释，编译系统和这个JIT三大语言系统,这个新事物名称就证明它属于偏向类似解释系统。也许这个名称可以再加一条，即jit=jit to native。
上面解释了普通interpter是什么原理的，而基于jit的interpter除了它模拟了普通解释系统后端的最小单元编译和执行机制(或者它类似TCC编译过程十分快显得像解释器)，它还显得有那么一点特殊之处，即它针对平台码，无论是RAW CPP源码，还是二进制DLL符号，它都能实现compile和连接不费时，和运行期直接查找到符号， 这二者都齐了所以jit才表现得像个解释器。
可见，JIT它也并没有带来新的东西，原理上Jit只是接通了生成到native code同时为目标翻译码和执行码的东西，别无它。是传统解释套装并列的部件。实际上也并没有破坏编译原理的外观。它依然是一整套语言系统，只不过在流程上它可以与解释语言并列，通过开启JIT的选项转到使用JIT套件（再重复一次，jit它代表整个JIT语言系统，同时包含前后端，需在三段式环境下理解它）。

Cling中的jit
-----

Cling基于clang+llvm,最主要的意义是其jit interpter机制，即解释语言那套+针对平台码平台符号，作为一个“特殊了一点的”解释器存在：即Cling jit后端可以jit to native,emit native function，其AST可以按NODE喂给运行器。
而其实JIT不仅限这个功能，cling依赖于jit能call into native libs不需binding，是JIT本身的功能，（当然，这事先需要在编译成二进制时保留JIT所需的符号，rdynamic causes symbols to be exported even though this is not a lib ,it Keep symbols for JIT resolution 这些DLL都是符号解析级的动态可载入组件，受操作系统DLL实现支持）。这种组件免除了link。因为组件都是在运行期link的。而从DLL中获得符号，就能省去compile->tranlate的需要。所以这也不脱离cling jit的作为解释系统的产品外观范围。
所以，这个面向DLL的特性，一定意义上可当成，cling jit视DLL为raw cpp code组件（暂时你可以把这里和接下来的组件当成脚本源码文件一类的东西来理解），为“源码”（而普通解释器面向解释单元，解释模块，是真实可视的源码组件，JIT只工作在二进制导出符号层，能作CPP源码和二进制混合编程）。因为它视平台DLL为组件，因此能做到动态持续从“DLL源码”(DLL其中源码实际并不可见，这里说的是其中符号类似llvm jit眼中的“源码”，被它当成了组件）加载符号和运行.
这点意义上，宠统来说，JIT就是一个更高级的”DLL“机制而已，使其还可以直接视库为开发件，具备组件的特性。这是后话更多组件的情况将在第三部分介绍。


-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106344586/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>



