---
layout: page
include_in_header: false
permalink: /_booklets/106344572/
---
qtcling - 一种更好的C++和标准库
=====

作为一个程序员或编程技术爱好者，你是不是开始厌倦了各种虚拟机语言和脚本语言??no vm scripting

它们要么不是C系的。需要你重新学习一套语法。如python,c#,java,js之类….

可这是多大的资源浪费啊，要知道，C是这世上唯一的通用基础语言的教学典范啊（pascal也算吧。。。），计算机专业的学生和非专业的人士都是靠它入门的。学习曲线上自然希望以后学的高级语言也是基于它的为佳。相信很多人都在为适应开发而不断学习新语言的需要而苦恼，而且，大量第三方模块需要binding to c才能使用，而且即使转化后也只是运行在某个托管的环境下，还需要带一个宠大的执行环境才能完成发布或运行。是的，就是那个可恶的虚拟机。这种用内存和CPU资源模拟软件计算机的方式，简直就是在OS上再造了一层执行时。这种过度封装对有技术洁避的极客来说还能怎么忍受呢？

要么，像这类语言，语法上个个宣传它们是通用脚本语言，可还是专用性很强，如PHP大多都用于WEB as dsl,这造成的结果是不通用且怪异，而另一些语言，它们还可能变得越来越宠大和复杂，这是因为为了迎合日益复杂的应用的开发需要，它们需要不断集成，纳入各种新元素到语言生态中去，像java,其生态链已经进入到很完善的地步了，它们还可能无节制地膨胀。没有一个干净的典范开发方式和语言核心存在。这与CPP强调的保持一个干净核心的原则相左。

所以说，虽然它们有组件特性，可能有REPL环境，有脚本特性，可是在以上这二个巨大的缺点面前。那些好的方面也背上了不好的光环。有没有一种基于C系的解释型或带REPL的语言环境，既有传统CPP的好处，又可以直接在这种语法上无改地，或尽量少改地作脚本编程或解释编程呢？可喜的是，这并非技术的桎梧。可以有：

1，第一种是tcc，据说它的编译速度之快已达到了解释语言的级别。可实际上，它只是编译速度足够快而已，称不上，也不可能称得上是解释语言。略过。

2，然后就是我们的cling了。cling/clang是cern代替cint而开发的，基于jit,jit是一种能模拟REPL的技术，当然cling一个光吐吐的编译器还不够，cling/clang可以直接调用C系模块(call into libraries)，用户使用其内置的宏语法就可以测试。这使得在cling下组建自定义的CPP开发环境尤为现实，大多脚本语言都是先出来编译器，然后其它是binding C的，cling天然有纳入各种库的能力，所以有条件建设成为一个完善的语言系统，cern rootsys就是这样。

cling需要整合各种第三方库，原始的cling支持的库和扩展十分有限，一个在windows上不支持#include 的cling编译器语言是没意义的。一个具体的第三库如QT的整合，因此也可能需要面临各种问题，

等等，亲，你不是说cling是基于标准CPP实现，可以直接调用c系模块的吗，是的，但是局限也是有的：

1，可能模块有特殊的扩展。如qt的源码不是标准的clang能理解的，是受moc转化过的，带pme字典信息的。这种肯定需要转化过来。

2，有一些受clang特殊限制的，如内联汇编在clang中还不能工作得很好，使用了这种技术的QT库自然需要动点小手术修正，因此对qt源码的改造是需要的。

话说，克服了整合qt到cling，这足以成为一个十分实用的qtcling语言了，有了qtcling,从此我们的Cer就得福入门了，只需要学习一门语言，一种典范 – QT式基于PME的OO，我们就可以做系统编程和应用编程了，甚至是脚本编程。

-----------------------


（演示视频请通过点击右下原文链接查看）

下载地址（本站下载）：

qtcling

http://www.shaolonglee.com/owncloud/index.php/s/wh3yzswLrtNhwaa/download?path=%2F&files=qtcling.rar



-----


(此处不设回复，扫码到微信参与留言，或直接点击到原文)

![](/p/106344572/qrcode.png)

<!-- Markdeep: -->
<meta charset="utf-8">
<link rel="stylesheet" href="../../res/aloha.css?">

<script src="../../res/markdeep.min.js" charset="utf-8"></script>



