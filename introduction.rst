简介
====

Erlang是一门被设计用于编写并发、实时、分布式系统的新语言。

很多年来，并发实时系统的编程技术一直落后于串行应用的编程。当使用C或Pascal进行串行编程已经成为实践标准时，大多数实时系统的程序员还在倒腾着汇编。如今的实时系统可以使用Ada、Modula2、Occam等为并发编程提供了显式支持的语言来编写，或是仍旧使用C这样缺乏并发结构的语言。

我们对并发的兴趣源自于对一些展现出大规模并发的问题的研究。这是实时控制系统的一个典型属性。Erlang程序员可以显式指定哪些活动需要由并发进程来展现。这种观念与Occam、CSP、Concurrent Pascal等语言类似，但与那些并不为了对现实世界的并发进行建模而引入并发的语言不同，这些语言引入并发的目的只是为了将编译出可在并行处理器上运行的程序以获得更高的性能。

现今Prolog和ML等语言已经被大范围用于工业应用之中，并极大地降低了设计、实现和维护应用的成本。我们对Erlang的设计和实现也是为了将并发实时系统编程提高到一个相似的高度。

申明式语法

    Erlang具备申明式的语法，且大部分都无副作用。

并发

    Erlang具备一个使用消息传递的基于进程的并发模型。Erlang的并发机制是轻量级的，如进程只占用极少的内存，进程的创建、删除以及消息传递也都只涉及极少量的计算。

实时

    Erlang可用于对相应延迟在毫秒数量级的软实时系统进行编程。

持续运作

    Erlang具备替换运行时系统代码的原语，并允许新旧版本的代码同时执行。这在电话交换机、空中交通控制等“不停机”系统中有极大的用处，这些系统在软件变更时都不能停机。

健壮

    在上述系统中，安全性是一个关键需求。Erlang具备三种结构来检测运行时错误。这些可用于编写健壮的系统。

内存管理

    Erlang是一门具备实时垃圾回收机制的符号计算语言。内存在需要时自动分配，在不需要时自动回收。典型的内存管理相关的编程错误都不再存在。

分布式

    Erlang没有内存共享。所有进程间交互都通过异步消息传递完成。使用Erlang可以轻易地构建分布式系统。为单处理器编写的应用不花什么力气就可以移植到处理器网络上运行。

集成

    Erlang可以简单地调用其他语言编写的程序。通过Erlang的接口系统，这些程序对于程序员来看就好像是用Erlang编写的一样。

我们从申明式语言和并发语言中借鉴了大量思想。早期Erlang的语法多半归功于STRAND，尽管当前的语法让人觉得像是无类型的ML。其并发模型则与SDL类似。

我们的目标是为健壮的大规模并发工业应用编程提供一种精炼、简单和高效的语言。因此，出于效率原因，我们放弃了许多现代函数式语言中的特性。Currying、高阶函数、延迟求值、ZF comprehension、逻辑变量、deep guards等，增强了申明式编程语言的表达能力，但对于工业控制应用而言，没有这些特性也不会有什么显著影响。倒是模式匹配语法的使用和Erlang变量的“单次赋值”属性，使得我们能够编写清晰、短小且可靠的程序。

最初Erlang是边实现边设计的，第一个版本是一个使用Prolog编写的解释器。与此同时，我们非常幸运地拥有了第一批热情的用户群，他们当时正在开发一个新电话交换机的原型。

这便催生了一条极为有效的语言设计途径。不被使用的构件被抛弃，对于令我们的用户不得不编写令人费解的代码的问题，则引入新的语言构件予以解决。尽管我们经常会对语言进行一些不向下兼容的更改，我们的用户还是飞速地编写了成千上万行的代码，并积极地鼓动其他人来使用这门语言。他们的努力催生了一种新的电话交换机编程方法，相关的一些内容被发表在[??]和[??]。

第一版基于Prolog的Erlang解释器很早以前就被编译型的实现所替代了。其中的一个实现可以免费获取，并使用非商业许可证。当前的Erlang实现在兼顾速度和轻量级并发的同时满足了我们的实时性要求。Erlang实现已经被移植到多种操作系统及多种处理器上。

Erlang适用于对很大范围内的并发应用进行编程。不少工具被开发出来用于辅助Erlang编程，如X Window System的接口、ASN.1编译器（使用Erlang编写并生成Erlang代码）、分析程序生成器、调试器……

读者群
------

本书面向对实时控制系统感兴趣且有一定的编程经验的人。但并不需要对函数式或逻辑语言有所了解。

本书中的材料与近年来在Ericsson及其全世界范围内的子公司以及瑞士大学举办的多次Erlang课程有关。该课程为期四天，不光展示语言本身，也对Erlang的多种编程范式进行介绍。课程的最后一天通常是一个编程练习，学生们将编写一个与第??章所描述的类似的电话交换机控制系统，并在一台实际的交换机上执行！

概要
----

本书被划分为两大部分。第一部分“编程”，介绍Erlang语言以及在Erlang编程中常见的一些编程范式。第二部分，“应用”，由一系列完备的章节构成，包含典型Erlang应用的案例分析。

编程
----

第1章是对Erlang的一个介绍性教程。通过一系列示例对语言的一些主要思想予以说明。

第2章介绍串行编程。这里将会介绍模块系统，这会是我们谈及Erlang时的一个基本术语。

第3和第4章包含一系列使用列表和元组进行编程的示例。这里将介绍列表和元组的基本编程技巧。在后续章节中需要用到的一些标准模块在此也会提及。其中包括实现集合、字典、平衡及非平衡二叉树等等的模块。

第5章介绍并发。在串行编程基础之上添加少量的原语便将Erlang变为一门并发编程语言。我们将介绍用于创建并行进程以及在进程间进行消息传递的原语。我们还将介绍为了将进程与一个名称相关联而引入的进程注册机制。

此处将解释服务器—客户端模型背后的基本思想。该模型在后续章节中被大量使用，同时也是用于协调多个并行进程间的活动的一种基本编程技术。我们还将介绍可让我们编写实时程序的超时。

第6章是对分布式编程的一个概述，解释了编写分布式应用的一些动机。我们描述了用于编写分布式Erlang程序的语言原语并解释了如何在Erlang节点网络中排布多组进程。

第7章解释了Erlang中的错误处理机制。我们将Erlang设计用于编写健壮的应用，语言中包含了三种正交的机制用于完成错误检查。我们认为语言应该在运行时检测出尽可能多的错误并让程序员负责纠正这些错误。

第8章展示了如何使用前一章介绍的错误处理原语来构建健壮的容错系统。我们展示了如何将错误的代码拒之门外，提供了一个容错的服务器（通过扩展客户端服务器模型）并展示了如何对计算进行“隔离”以便在出错时对破坏范围进行限制。

第9章包含了一系列在本书其他部分未提及的编程思想和技巧。我们在此讨论尾递归优化。对于希望正确编写出不间断运行程序的程序员而言，对该优化的理解是至关重要的。We then introduce references which provide unique unforgetable symbols. 本章之后的两节描述了如何更改运行时系统的Erlang代码的细节（编写不停机系统需要使用这种技术）以及如何将Erlang与使用其他语言编写的程序对接。之后，我们将介绍用于高效处理大量无类型数据的二进制数据处理、为每个进程提供了可销毁存储能力的进程字典，以及作为分布式Erlang核心的网络内核。最后我们将对执行效率进行讨论，并举例说明如何编写高效的Erlang代码。

应用
----

第10章展示了如何使用Erlang编写一个数据库。我们从第??章开发的简单字典模块和第??章的客户端—服务器模型开始，由此完成一个简单的并发数据库。然后我们将展示如何以组织成多级树形结构的并行进程来实现该数据库，以此改善其吞吐量。接着我们加入事务性，以使得多个串行数据库操作可以表现出原子性。

在这之后，我们为数据库增加“回滚”机制以允许我们“撤销”先前的数据库操作。回滚示例对非破坏性赋值进行了漂亮的展示。

接着我们讨论如何让我们的数据库能够容错。最后，我们展示如何将一个外部数据库与我们的数据库集成，并为程序员提供统一的接口。

第11章介绍分布式编程技术。我们展示如何使用Erlang实现多种常见的分布式编程技术，如远程过程调用、广播、promises等等。

第12章研究分布式数据问题。许多情况下，运行在不同物理机器上的多个应用希望共享一些公共数据结构。本章描述用于实现分布式系统中的共享数据的各种技术。

第13章是对Erlang操作系统的讨论。由于所有的进程管理都在Erlang内部完成，我们对传统操作系统提供的服务所需甚少。我们在此展现Erlang操作系统中用于完成语言标准分布式任务的主要组件。该操作系统可以作为更专一化的操作系统的基础以用于某个具体应用之中。

第14章与两个实时控制问题相关。第一个是著名的电梯控制问题——这里我们将看到将系统建模为一组并行进程提供了一套简单优雅的解决方案。第二部分讨论“进程控制”，此处我们的“进程”是一个卫星。观测卫星的唯一途径是分析安装在卫星上的传感器所发送的数据。变更卫星行为的唯一途径是向卫星上的仪器发送指令。尽管这里以卫星控制系统为例，相关技术可以应用于更广泛的范围。

第15章是一个小型本地电话交换机的实时控制系统实例。Erlang是Ericsson计算机科学实验室开发出来的，而Ericsson也是世界上主要电话交换机的生产商之一——简化电信编程始终都是我们的主要兴趣所在！

本章中的示例只是一个“玩具”系统。然而麻雀虽小五脏俱全，它展示了用Erlang构建电信软件的许多技术。该示例只是那些用于控制复杂电信应用的庞大Erlang程序的小兄弟。这些程序都由数万行Erlang代码构成，是本章所描述的各种编程技术的扩展应用。

本章的末尾对SDL做了一个简短的介绍（SDL被广泛用于描述电信系统的行为）——我们在此展现了一份SDL规范与实现这份规范的Erlang代码的一一对应关系。SDL与Erlang之间的概念“鸿沟”很小——这将降低实时系统的设计实现成本。

第16章简短地介绍了ASN.1并给出了一个从ASN.1到Erlang的交叉编译器。ASN.1是用于描述通讯协议数据格式的标准。本章展现了ASN.1规范与用于操作ASN.1描述的数据包的Erlang代码间的相似性。为系统中通讯软件部分自动产生大部分代码的能力大大简化了系统的构建过程。

第17章展示了如何为Erlang应用构建用户界面。本章展示了两点：第一，并发进程组如何良好地映射到窗口系统中的一组对象；第二，让Erlang与其他语言编写软件包协同运作。

第18章中我们讨论面向对象程序语言的一些主要属性以及如何在Erlang中予以实现。我们将讨论面向对象设计及其Erlang实现之间的关系。

.. vim:ft=rst ts=4 sw=4 fenc=utf-8 enc=utf-8 et
