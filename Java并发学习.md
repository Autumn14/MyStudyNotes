# 并发 

## 1.简介

Java*并发*是一个涵盖 Java 平台上的多线程、并发和并行的术语。

**什么是多线程？**

多线程意味着，在同一个应用程序中拥有多个*执行线程*。

线程就像一个单独的 CPU 执行的应用程序。

因此，多线程应用程序就像一个具有多个 CPU 同时执行代码不同部分的应用程序。

线程并不等于 CPU。

通常单个 CPU 会将其执行时间分配给多个线程，并在给定时间内切换执行每个线程。

也可以让应用程序的线程由不同的 CPU 执行。

**为什么要使用多线程？**

单核CPU：

能够更好地利用计算机中的资源。

例如，如果一个线程正在等待通过网络发送的请求的响应，那么另一个线程可以在此期间使用 CPU 来执行其他操作。

多核CPU：

为应用程序使用多个线程，以便能够利用所有 CPU 核心。

响应性用户体验：

使用多线程的另一个原因是提供更好的用户体验。

公平性用户体验：

通过让每个客户端的请求由其自己的线程执行，那么没有一个任务可以完全独占 CPU。

**多线程与多任务**

多任务：

计算机可以同时执行多个程序（即任务或进程）。

但实际上并不是“同时”。

单个 CPU 由多个程序共享。

操作系统会在运行的程序之间切换，在切换之前先执行每个程序一小段时间。

多线程：

可以在同一个程序中拥有多个执行线程。

执行线程可以被认为是执行程序的 CPU。

当有多个线程执行同一个程序时，就像有多个 CPU 在同一个程序中执行一样。

**多线程很难**

多线程是提高某些类型程序性能的好方法。

但是，多线程比多任务更具挑战性。

线程在同一个程序中执行，因此同时读取和写入同一个内存。

这可能会导致单线程程序中看不到的错误。

其中一些错误可能在单 CPU 机器上看不到，因为两个线程从未真正“同时”执行。

多核 CPU 的出现，意味着单独的线程可以由单独的内核或 CPU 同时执行。

学习控制线程如何访问共享资源，如内存、文件、数据库等。

这是 Java 并发要讨论的主题之一。

多线程中出现的一些问题与多任务和分布式系统中出现的问题类似。

**并发模型**

第一个 Java *并发模型*假设在同一应用程序中执行的多个线程也会共享对象。

这种并发模型通常称为“共享状态并发模型”。

许多并发语言结构和实用程序都旨在支持此并发模型。

**共享状态并发模型**会导致很多并发问题，这些问题很难得到妥善解决。

因此，一种称为“无共享”或“分离状态”的替代并发模型已变得流行起来。

在**分离状态并发模型**中，线程不共享任何对象或数据。这避免了共享状态并发模型中的很多并发访问问题。

## 2.多线程优势

**更好的CPU利用率**

假设有一个应用程序从本地文件系统读取和处理文件。

假设从磁盘读取一个文件需要 5 秒，处理该文件需要 2 秒。

处理两个文件则需要

```
  5秒读取文件A
  2秒处理文件A
  5秒读取文件B
  2秒处理文件B
-----------------------
 共计 14 秒
```

从磁盘读取文件时，大部分 CPU 时间都花在等待磁盘读取数据上。

在此期间，CPU 几乎处于空闲状态。它可能正在执行其他操作。通过更改操作顺序，可以更好地利用 CPU。

看看这个顺序：

```
  5秒读取文件A
  5秒读取文件B + 2秒处理文件A
  2秒处理文件B
-----------------------
 共计 12 秒
```

一般来说，CPU 可以在等待 IO 时做其他事情。

**更简单的程序设计**

如果您要在单线程应用程序中手动编写上述读取和处理顺序，则必须跟踪每个文件的读取和处理状态。

相反，您可以启动两个线程，每个线程只读取和处理一个文件。

每个线程在等待磁盘读取其文件时将被阻止。

在等待期间，其他线程可以使用 CPU 来处理它们已经读取的文件部分。

结果是磁盘一直处于忙碌状态，将各种文件读入内存。

这样可以更好地利用磁盘和 CPU。

它也更容易编程，因为每个线程只需跟踪一个文件。

**响应速度更快的程序**

将单线程应用程序转变为多线程应用程序的另一个常见目标是实现响应更快的应用程序。

想象一下一个服务器应用程序在某个端口上侦听传入请求。当收到请求时，它会处理该请求，然后返回侦听。服务器循环如下所示：

```
  while(服务器处于活动状态){
    监听请求
    处理请求
  }
```

如果请求的处理时间过长，则在此期间没有新客户端可以向服务器发送请求。只有在服务器处于监听状态时，才能接收请求。

另一种设计是让监听线程将请求传递给工作线程，然后立即返回监听。工作线程将处理请求并向客户端发送回复。此设计如下所示：

```
  while(服务器处于活动状态){
    监听请求
    将请求传递给工作线程
  }
```

这样，服务器线程将更快地恢复监听。因此，更多的客户端可以向服务器发送请求。服务器的响应速度更快了。

桌面应用程序也是如此。

如果您单击一个启动长任务的按钮，并且执行任务的线程是更新窗口、按钮等的线程，那么在执行任务时，应用程序将显示无响应。

相反，可以将任务交给工作线程。

当工作线程忙于任务时，窗口线程可以自由响应其他用户请求。

当工作线程完成后，它会向窗口线程发出信号。

然后，窗口线程可以使用任务结果更新应用程序窗口。

具有工作线程设计的程序对用户来说将显得更具响应性。

**更公平的CPU资源分配**

想象一下，一台服务器正在接收来自客户端的请求。然后想象一下，其中一个客户端发送了一个需要很长时间才能处理的请求 - 例如 10 秒。如果服务器使用单个线程处理所有任务，那么处理缓慢的请求之后的所有请求都将被迫等待，直到整个请求处理完毕。

通过在多个线程之间划分 CPU 时间并在线程之间切换，CPU 可以在多个请求之间更公平地分配其执行时间。这样，即使其中一个请求很慢，其他处理速度更快的请求也可以与较慢的请求同时执行。当然，这意味着执行慢速请求会更慢，因为它不会将 CPU 单独分配给它来处理。然而，其他请求将不得不等待更短的时间才能得到处理，因为它们不必等待慢速任务完成后才能处理。如果只有慢速请求需要处理，那么 CPU 仍然可以单独分配给慢速任务。

多线程成本

从单线程应用程序转变为多线程应用程序不仅能带来好处，也需要付出一些代价。

不要仅仅因为可以就启用应用程序的多线程。您应该有充分的理由相信这样做的好处大于成本。如果有疑问，请尝试测量应用程序的性能或响应能力，而不是仅仅猜测。

**更复杂的设计**

尽管多线程应用程序的某些部分比单线程应用程序简单，但其他部分则更复杂。

多线程访问共享数据时执行的代码需要特别注意。线程交互并非总是那么简单。由于线程同步不正确而产生的错误可能很难检测、重现和修复。

**上下文切换开销**

当 CPU 从执行一个线程切换到执行另一个线程时，CPU 需要保存当前线程的本地数据、程序指针等，并加载下一个要执行的线程的本地数据、程序指针等。这种切换称为“上下文切换”。

CPU 从一个线程的上下文中执行切换到另一个线程的上下文中执行。

上下文切换并不便宜。您不会想在不必要的情况下在线程之间进行切换。

**增加资源消耗**

线程需要计算机的一些资源才能运行。

除了 CPU 时间之外，线程还需要一些内存来保存其本地堆栈。它还可能占用操作系统内部管理线程所需的一些资源。

尝试创建一个程序，该程序创建 100 个线程，这些线程除了等待什么也不做，然后看看应用程序运行时占用了多少内存。

## 3.并发模型

*并发系统可以使用不同的并发模型* 来实现。

*并发模型*指定系统中的线程如何协作以完成它们所分配的任务。

不同的并发模型以不同的方式拆分任务，并且线程可以以不同的方式进行通信和协作。

下文是（2015 - 2019 年）使用的最流行的并发模型。

**并发模型和分布式系统的相似之处**

本文描述的并发模型类似于分布式系统中使用的不同架构。在并发系统中，不同的线程相互通信。在分布式系统中，不同的进程相互通信（可能在不同的计算机上）。线程和进程本质上非常相似。这就是为什么不同的并发模型通常看起来类似于不同的分布式系统架构。

当然，分布式系统还有额外的挑战，比如网络可能会出现故障，或者远程计算机或进程出现故障等。但是在大型服务器上运行的并发系统也可能会遇到类似的问题，比如 CPU 出现故障、网卡出现故障、磁盘出现故障等。出现故障的概率可能较低，但理论上仍然有可能发生。

由于并发模型与分布式系统架构相似，它们经常可以互相借鉴。例如，在工作器（线程）之间分配工作的模型通常类似于**分布式系统中的负载平衡模型**。日志记录、故障转移、任务幂等性等错误处理技术也是如此。

**共享状态与分离状态**

并发模型的一个重要方面是，组件和线程是否设计为在线程之间共享状态，或者具有永远不会在线程之间共享的单独状态。

共享状态意味着系统中的不同线程将共享某些状态。状态是指某些数据，通常是一个或多个对象或类似数据。当线程共享状态时，可能会出现**竞争条件**和**死锁**等问题。当然，这取决于线程如何使用和访问共享对象。

![](C:\Users\Rain7\Desktop\笔记md\javapic\gxzt.png)

*分离状态*意味着系统中的不同线程之间不共享任何状态。如果不同的线程需要通信，它们可以通过在它们之间交换不可变对象或发送对象（或数据）的副本来实现。因此，当没有两个线程写入同一个对象（数据/状态）时，您可以避免大多数常见的并发问题。

![](C:\Users\Rain7\Desktop\笔记md\javapic\flzt.png)

使用单独的状态并发设计通常可以使代码的某些部分更易于实现和推理，因为您知道只有一个线程会写入给定对象。您不必担心对该对象的并发访问。但是，您可能需要从总体上更深入地考虑应用程序设计，才能使用单独的状态并发。不过，我觉得这是值得的。我个人更喜欢单独的状态并发设计。

### 并行工作者模型

第一个并发模型是我所说的*并行工作者*模型。传入的作业被分配给不同的工作者。下面是说明并行工作者并发模型的图表：

delegator：委托者

worker：工作者

![](C:\Users\Rain7\Desktop\笔记md\javapic\bxgzzmx.png)

在并行工作者并发模型中，委托人将传入的作业分配给不同的工作者。每个工作者完成整个作业。工作者并行工作，在不同的线程中运行，并且可能在不同的 CPU 上运行。

如果在汽车厂实施并行工人模型，每辆汽车将由一名工人生产。工人将获得要制造的汽车的规格，然后从头到尾完成所有工作。

并行工作者并发模型是 Java 应用程序中最常用的并发模型（尽管这种情况正在发生变化）。

并行工作者并发模型可以设计为同时使用共享状态或单独状态，这意味着工作者要么可以访问某些共享状态（共享对象或数据），要么没有共享状态。

**并行工作者的优势**

并行工作者并发模型的优点是易于理解。要增加应用程序的并行化级别，只需添加更多工作者即可。

例如，如果您正在实现一个网络爬虫，您可以使用不同数量的工作器爬取一定数量的页面，然后查看哪个数量可以提供最短的总爬取时间（即最高的性能）。由于网络爬取是一项 IO 密集型工作，因此您的计算机中每个 CPU/核心可能最终会有几个线程。每个 CPU 一个线程太少了，因为它在等待数据下载时大部分时间都会处于空闲状态。

**并行工作者的缺点**

然而，并行工作者并发模型在简单的表面下隐藏着一些缺点。

共享状态可能会变得复杂

如果共享工作器需要访问某种共享数据（无论是在内存中还是在共享数据库中），管理正确的并发访问可能会变得很复杂。下图显示了这如何使并行工作器并发模型变得复杂：

![](C:\Users\Rain7\Desktop\笔记md\javapic\gxztknhbdhfz.png)

其中一些共享状态存在于作业队列等通信机制中。但还有一些共享状态是业务数据、数据缓存、数据库连接池等。

一旦共享状态潜入并行工作者并发模型，它就会开始变得复杂。线程需要以一种确保一个线程的更改对其他线程可见的方式访问共享数据（推送到主内存，而不仅仅是停留在执行线程的 CPU 的 CPU 缓存中）。线程需要避免**竞争条件**、 **死锁**和许多其他共享状态并发问题。

此外，当线程在访问共享数据结构时相互等待时，部分并行化会丢失。许多并发数据结构处于阻塞状态，这意味着一个或一组有限的线程可以在任何给定时间访问它们。这可能会导致这些共享数据结构上的争用。高争用本质上会导致访问共享数据结构的部分代码的执行一定程度的序列化（消除并行化）。

现代**非阻塞并发算法**可以减少争用并提高性能，但非阻塞算法难以实现。

持久数据结构是另一种选择。持久数据结构在修改时始终保留其自身的先前版本。因此，如果多个线程指向同一个持久数据结构并且一个线程修改了它，则修改线程将获得对新结构的引用。所有其他线程都保留对旧结构的引用，该结构仍保持不变，因此是一致的。Scala 标准 API 包含几个持久数据结构。

虽然持久数据结构是解决共享数据结构并发修改的一个优雅的解决方案，但持久数据结构的性能往往不太好。

例如，持久列表会将所有新元素添加到列表的头部，并返回对新添加元素的引用（然后指向列表的其余部分）。所有其他线程仍保留对列表中先前第一个元素的引用，并且对于这些线程来说，列表看起来没有变化。它们看不到新添加的元素。

这种持久列表以链表的形式实现。不幸的是，链表在现代硬件上的性能不佳。列表中的每个元素都是一个单独的对象，这些对象可以分散在整个计算机内存中。现代 CPU 在顺序访问数据方面要快得多，因此在现代硬件上，在数组之上实现的列表将获得更高的性能。数组按顺序存储数据。CPU 缓存可以一次将数组的较大块加载到缓存中，并让 CPU 在加载后直接在 CPU 缓存中访问数据。对于元素分散在整个 RAM 中的链表来说，这实际上是不可能的。

**无状态工作者**

共享状态可由系统中的其他线程修改。因此，工作者必须在每次需要时重新读取状态，以确保它们正在处理最新副本。无论共享状态保存在内存中还是外部数据库中，情况都是如此。不在内部保存状态（但每次需要时重新读取）的工作者称为*无状态*。

每次需要时重新读取数据会很慢。特别是当状态存储在外部数据库中时。

**作业排序是不确定的**

并行工作者模型的另一个缺点是作业执行顺序是不确定的。无法保证哪些作业先执行或最后执行。作业 A 可能在作业 B 之前交给工作者，但作业 B 可能在作业 A 之前执行。

并行工作者模型的不确定性使得很难推断出系统在任何给定时间点的状态。这也使得保证一个任务在另一个任务之前完成变得更加困难（甚至不可能）。然而，这并不总是会导致问题。这取决于系统的需求。

### 流水线并发模型

第二种并发模型是我所说的*装配线*并发模型。我选择这个名字只是为了符合前面的“并行工作者”比喻。其他开发人员根据平台/社区使用其他名称（例如反应系统或事件驱动系统）。下面是说明装配线并发模型的图表：

![](C:\Users\Rain7\Desktop\笔记md\javapic\lsxbfmx.png)

工人的组织方式类似于工厂流水线上的工人。每个工人只完成全部工作的一部分。完成这部分工作后，工人将工作转交给下一个工人。

使用流水线并发模型的系统通常设计为使用非阻塞 IO。非阻塞 IO 意味着当一个 worker 启动 IO 操作（例如从网络连接读取文件或数据）时，该 worker 不会等待 IO 调用完成。IO 操作很慢，因此等待 IO 操作完成会浪费 CPU 时间。在此期间，CPU 可以执行其他操作。当 IO 操作完成时，IO 操作的结果（例如读取数据或写入数据的状态）将传递给另一个 worker。

使用非阻塞 IO，IO 操作决定了工作者之间的边界。工作者会尽其所能，直到它必须启动 IO 操作。然后它放弃对作业的控制。当 IO 操作完成后，装配线上的下一个工作者将继续处理该作业，直到它也必须启动 IO 操作等。

![](C:\Users\Rain7\Desktop\笔记md\javapic\fzsio.png)

实际上，作业可能不会沿着一条装配线流动。由于大多数系统可以执行多项作业，因此作业会根据下一步需要执行的作业部分从一名工人流向另一名工人。实际上，可能会有多条不同的虚拟装配线同时运行。实际上，装配线系统中的作业流可能如下所示：

![](C:\Users\Rain7\Desktop\笔记md\javapic\dglsx.png)



作业甚至可以转发给多个工人进行并发处理。例如，作业可以转发给作业执行器和作业记录器。下图说明了所有三条装配线如何通过将作业转发给同一工人（中间装配线的最后一名工人）来完成：

![](C:\Users\Rain7\Desktop\笔记md\javapic\zflsx.png)



装配线可能会比这更加复杂。

**反应式、事件驱动系统**

使用流水线并发模型的系统有时也称为*反应系统*或 *事件驱动系统*。系统的工作程序对系统中发生的事件做出反应，这些事件要么来自外部世界，要么由其他工作程序发出。事件的示例可以是传入的 HTTP 请求，或者某个文件已加载到内存中等。

受欢迎的平台：Node.JS（JavaScript）

**参与者与渠道**

参与者和渠道是装配线（或反应式/事件驱动）模型的两个类似例子。

在 Actor 模型中，每个工作者被称为一个*Actor*。Actor 之间可以直接发送消息。消息是异步发送和处理的。Actor 可用于实现一条或多条作业处理流水线，如前所述。下面是一张说明 Actor 模型的图表：

![](C:\Users\Rain7\Desktop\笔记md\javapic\cyzhqd.png)

在通道模型中，工作者不直接相互通信。相反，它们在不同的通道上发布消息（事件）。然后其他工作者可以在这些通道上监听消息，而发送者不知道谁在监听。以下是说明通道模型的图表：

![](C:\Users\Rain7\Desktop\笔记md\javapic\qudao.png)

在撰写本文时，我认为通道模型更加灵活。工人不需要知道哪些工人将在装配线上稍后处理该作业。它只需要知道将作业转发到哪个通道（或将消息发送到哪个通道等）。通道上的监听器可以订阅和取消订阅，而不会影响写入通道的工人。这允许工人之间的耦合稍微松散一些。

**装配线优势**

与并行工作模型相比，流水线并发模型有如下几个优点。

**没有共享状态**

事实上，工作者不与其他工作者共享状态，这意味着它们可以在不考虑并发访问共享状态时可能出现的所有并发问题的情况下实现。这使得实现工作者变得容易得多。你可以将工作者实现为执行该工作的唯一线程 - 本质上是单线程实现。

**有状态的 Worker**

由于工作线程知道没有其他线程会修改其数据，因此工作线程可以是有状态的。我说的有状态是指它们可以将操作所需的数据保存在内存中，只将更改写回最终的外部存储系统。因此，有状态的工作线程通常比无状态的工作线程更快。

**更好的硬件兼容性**

单线程代码的优势在于它通常更符合底层硬件的工作方式。首先，当您假设代码在单线程模式下执行时，您通常可以创建更优化的数据结构和算法。

其次，如上所述，单线程有状态工作器可以将数据缓存在内存中。当数据缓存在内存中时，该数据也更有可能缓存在执行线程的 CPU 的 CPU 缓存中。这使得访问缓存数据的速度更快。

当代码以自然受益于底层硬件工作方式的方式编写时， 我将其称为**硬件一致性**。一些开发人员称之为**机械同情**。我更喜欢硬件一致性这个术语，因为计算机的机械部件很少，而“同情”一词在此上下文中用作“更好地匹配”的隐喻，我认为“一致性”一词相当好地表达了这一点。无论如何，这是吹毛求疵。使用您喜欢的任何术语。

**作业排序是可能的**

可以按照流水线并发模型实现一个并发系统，以保证作业排序。作业排序使得推断系统在任何给定时间点的状态变得更容易。此外，您可以将所有传入的作业写入日志。如果系统的任何部分发生故障，可以使用此日志从头重建系统状态。作业按特定顺序写入日志，此顺序成为保证的作业顺序。这种设计可能如下所示：

![](C:\Users\Rain7\Desktop\笔记md\javapic\zuoypx.png)

执行有保证的作业顺序并不容易，但通常是可行的。如果可以，这将大大简化备份、恢复数据、复制数据等任务，因为这些都可以通过日志文件完成。

**装配线的缺点**

流水线并发模型的主要缺点是，作业的执行通常分散在多个工作器上，因此分散在项目中的多个类上。因此，很难确切地看到给定作业正在执行哪些代码。

编写代码也可能更加困难。工作代码有时被编写为回调处理程序。如果代码中嵌套了许多回调处理程序，则可能会导致某些开发人员称之为*回调地狱的*情况。回调地狱只是意味着很难跟踪代码在所有回调中实际执行的操作，以及确保每个回调都可以访问所需的数据。

使用并行工作者并发模型，这往往更容易。您可以打开工作者代码，并从头到尾阅读执行的代码。当然，并行工作者代码也可能分布在许多不同的类中，但从代码中读取执行顺序通常更容易。

### 功能并行模型

功能并行是目前被广泛讨论的第三种并发模型（2015 年）。

函数并行的基本思想是使用函数调用来实现程序。函数可以看作是相互发送消息的“代理”或“参与者”，就像在流水线并发模型（又称反应式或事件驱动系统）中一样。当一个函数调用另一个函数时，这类似于发送消息。

传递给函数的所有参数都会被复制，因此接收函数之外的任何实体都无法操纵数据。这种复制对于避免共享数据上的竞争条件至关重要。这使得函数执行类似于原子操作。每个函数调用都可以独立于任何其他函数调用执行。

当每个函数调用都可以独立执行时，每个函数调用都可以在单独的 CPU 上执行。这意味着，功能实现的算法可以在多个 CPU 上并行执行。

在 Java 7 中，我们获得了java.util.concurrent包含 **ForkAndJoinPool**的软件包，它可以帮助您实现类似于函数式并行的功能。在 Java 8 中，我们获得了并行**流** ，它可以帮助您并行化大型集合的迭代。

函数并行的难点在于知道要并行化哪些函数调用。协调跨 CPU 的函数调用会产生开销。函数完成的工作单元需要达到一定的大小才能值得这个开销。如果函数调用非常小，尝试并行化它们实际上可能比单线程、单 CPU 执行更慢。

根据我的理解（这并不完美），您可以使用反应式事件驱动模型实现算法，并实现与功能并行性类似的工作细分。使用事件驱动模型，您可以更好地控制并行化的内容和程度（在我看来）。

此外，将任务拆分到多个 CPU 上并承担协调开销，只有当该任务是程序当前正在执行的唯一任务时才有意义。但是，如果系统同时执行多个其他任务（例如 Web 服务器、数据库服务器和许多其他系统），则尝试并行化单个任务是没有意义的。计算机中的其他 CPU 无论如何都会忙于处理其他任务，因此没有理由尝试用速度较慢、功能并行的任务来干扰它们。您很可能更适合使用流水线（反应式）并发模型，因为它的开销较少（在单线程模式下按顺序执行）并且更符合底层硬件的工作方式。

**哪种并发模型最好？**

那么，哪种并发模型更好？

通常情况下，答案取决于你的系统应该做什么。如果你的作业天生就是并行的、独立的，并且不需要共享状态，那么你也许能够使用并行工作者模型来实现你的系统。

但许多作业并不是天生并行和独立的。对于这类系统，我相信流水线并发模型的优点多于缺点，并且比并行工作者模型的优点更多。

很多平台实现了并发模型的功能。

## 4.并发和并行

*并发*意味着应用程序正在执行多个任务——同时或至少看似同时（并发）。

并行执行是指计算机拥有多个 CPU 或 CPU 核心，并同时执行多个任务。

**并行执行**与**并行性**并不是指同一种现象 。

*并行性* 这一术语的意思是，应用程序将其任务拆分为可并行处理的较小子任务，例如同时在多个 CPU 上处理。

## 5.创建和启动Java线程

**创建并启动线程**

在 Java 中创建线程的步骤如下：

```java
Thread thread = new Thread();
```

要启动 Java 线程，您可以调用其 start() 方法，如下所示：

```java
thread.start();
```

此示例未指定线程要执行的任何代码。因此线程启动后将立即再次停止。

有两种方法可以指定线程应执行哪些代码。

第一种方法是创建 Thread 的子类并重写`run()`方法。

第二种方法是将实现 Runable 接口。

### 继承 Thread 类

指定线程要运行的代码的第一种方法是创建 Thread 的子类并重写该`run()`方法。

该`run()`方法是调用后线程执行的代码`start()`。

以下是创建 Java 子类的示例`Thread`：

```java
  public class MyThread extends Thread {

    public void run(){
       System.out.println("MyThread running");
    }
    
  }
```

要创建并启动上述线程，您可以这样做：

```java
  MyThread myThread = new MyThread();
  myTread.start();
```

线程启动后，调用`start()`将立即返回。它不会等到`run()`方法完成。`run()`方法的执行将像由不同的 CPU 执行一样。方法`run()`执行时，它将打印出文本“MyThread 正在运行”。

`Thread`还可以创建这样的 匿名子类：

```java
  Thread thread = new Thread(){
    public void run(){
      System.out.println("Thread Running");
    }
  }

  thread.start();
```

`run()`一旦新线程执行 该方法，此示例将打印出文本“Thread Running” 。

### 实现 Runable 接口

指定线程应运行哪些代码的第二种方法是创建一个实现`java.lang.Runnable`接口的类。

实现接口的 Java 对象 `Runnable`可以由 Java 执行`Thread`。

该接口是Java 平台自带的Runnable标准Java 接口Runnable。该接口只有一个方法run()。

该接口的基本样子如下Runnable：

```java
public interface Runnable() {

    public void run();

}
```

线程执行时要执行的操作都必须包含在`run()`方法的实现中。有三种方法可以实现该`Runnable`接口：

1. 创建一个实现`Runnable`接口的 Java 类。
2. 创建一个实现`Runnable`接口的匿名类。
3. 创建一个实现`Runnable`接口的 Java Lambda。

以下章节将解释所有三个选项。

### 创建一个实现`Runnable`接口的 Java 类。

```java
  public class MyRunnable implements Runnable {

    public void run(){
       System.out.println("MyRunnable running");
    }
      
  }
```

此`Runnable`实现所做的只是打印出文本 `MyRunnable running`。

打印完该文本后，该`run()`方法退出，并且运行该方法的线程`run()`将停止。

### 创建一个实现`Runnable`接口的匿名类。

```java
Runnable myRunnable =
    new Runnable(){
        public void run(){
            System.out.println("Runnable running");
        }
    }
```

### 创建一个实现`Runnable`接口的 Java Lambda。

```java
Runnable runnable =
        () -> { System.out.println("Lambda Runnable running"); };
```

### 使用 Runnable 启动线程

```java
Runnable runnable = new MyRunnable(); // or an anonymous class, or lambda...

Thread thread = new Thread(runnable);
thread.start();
```

当线程启动时，它将调用实例`MyRunnable`的`run()`方法 ，而不是执行它自己的`run()`方法。上面的示例将打印出文本“MyRunnable running”。

### 两种方式哪种更好？

没有规则规定这两种方法哪种最好。两种方法都有效。

但就我个人而言，我更喜欢实现Runnable，并将实现的实例交给实例Thread。

当通过**线程池**执行Runnable时，很容易将实例排队，直到池中的线程空闲。对于子类来说，这有点困难。

有时可能这两种方式都要执行。例如，如果创建一个`Thread`子类，去执行多个`Runnable`。实现线程池时通常就是这种情况。

### 常见陷阱：调用 run() 而不是 start()

创建和启动线程时，一个常见的错误是调用`Thread`的`run()`方法而不是`start()`，如下所示：

```java
  Thread newThread = new Thread(MyRunnable());
  newThread.run();  //should be start();
```

一开始你可能什么都没注意到，因为`Runnable`的`run()`方法按你预期的那样执行。

但是，它不是由你刚创建的新线程执行的。而是由创建线程的线程执行的`run()`。换句话说，就是执行上述两行代码的线程。要让`newThread`新创建的线程 `MyRunnable`调用实例`run()`的方法，你必须调用`newThread.start()`方法。

### 线程名称

创建 Java 线程时，您可以为其命名。名称可以帮助您区分不同的线程。

```java
   Thread thread = new Thread("New Thread") {
      public void run(){
        System.out.println("run by: " + getName());
      }
   };

   thread.start();
   System.out.println(thread.getName());
```

注意传递给构造函数`Thread`的字符串“New Thread”作为参数 。此字符串是线程的名称。可以通过`Thread`的`getName()`方法获取该名称。

```java
   MyRunnable runnable = new MyRunnable();
   Thread thread = new Thread(runnable, "New Thread");

   thread.start();
   System.out.println(thread.getName());
```

但请注意，由于`MyRunnable`类不是`Thread`的子类 ，因此它无权访问执行它的线程的`getName()`方法。

### 线程.currentThread()

`Thread.currentThread()`方法返回对正在执行的实例的引用。

```java
Thread thread = Thread.currentThread();
```

一旦获得了`Thread`对象的引用，就可以调用其方法。例如，你可以像这样获取当前正在执行代码的线程的名称：

```java
String threadName = Thread.currentThread().getName();
```

### Java 线程示例

下面是一个小例子。

首先打印出执行`main()`方法的线程的名称。这个线程由 JVM 分配。

然后它启动 10 个线程并给它们一个数字( `"" + i`)作为名称 。

然后每个线程打印出它的名称，然后停止执行。

```java
public class ThreadExample {

  public static void main(String[] args){
    System.out.println(Thread.currentThread().getName());
    for(int i=0; i<10; i++){
      new Thread("" + i){
        public void run(){
          System.out.println("Thread: " + getName() + " running");
        }
      }.start();
    }
  }
    
}
```

请注意，即使线程按顺序启动（1、2、3 等），它们也可能不会按顺序执行，这意味着线程 1 可能不是第一个将其名称写入`System.out`的线程。

这是因为线程原则上是并行执行的，而不是按顺序执行的。JVM 和/或操作系统决定线程的执行顺序。此顺序不必与线程启动的顺序相同。

### 暂停线程

线程可以通过调用静态方法`Thread.sleep()`来暂停自身。

`sleep()` 方法以毫秒数作为参数。

`sleep()`方法将尝试在恢复执行之前休眠该毫秒数。

`sleep()`并非 100% 精确，但仍然相当不错。

```java
try {
    Thread.sleep(10L * 1000L);
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

执行上述 Java 代码的线程将休眠大约 10 秒（10.000 毫秒）。

### 停止线程

停止 Java 线程需要对线程实现代码进行一些准备。

Java `Thread`类包含一个`stop()`方法，但该方法已被弃用。

原始`stop()` 方法无法保证线程在何种状态下停止。这意味着，线程在执行期间访问的所有 Java 对象都将处于未知状态。如果应用程序中的其他线程也可以访问相同的对象，则应用程序可能会意外且不可预测地失败。

您必须实现线程代码才能停止线程，而不是调用`stop()`方法。

下面是一个类的示例，`Runnable`该类包含一个额外的方法，称为`doStop()`方法，该方法会向 发出`Runnable`停止信号。`Runnable`会检查此信号并在准备好时停止。

```java
public class MyRunnable implements Runnable {

    private boolean doStop = false;

    public synchronized void doStop() {
        this.doStop = true;
    }

    private synchronized boolean keepRunning() {
        return this.doStop == false;
    }

    @Override
    public void run() {
        while(keepRunning()) {
            // keep doing what this thread should do.
            System.out.println("Running");

            try {
                Thread.sleep(3L * 1000L);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
    }
}
```

注意`doStop()`和`keepRunning()`方法。

下面是启动一个 Java 线程来执行上述类的实例`MyRunnable` ，并在延迟后再次停止它的示例：

```java
public class MyRunnableMain {

    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();

        Thread thread = new Thread(myRunnable);

        thread.start();

        try {
            Thread.sleep(10L * 1000L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        myRunnable.doStop();
    }
}
```

请记住，如果您的`Runnable`实现需要的不仅仅是 `run()`方法（例如，还需要`stop()`或`pause()`方法），那么您就不能在`Runnable`使用 Java lambda 表达式来创建实现。Java lambda 只能实现一个方法。相反，您必须使用自定义类或扩展的自定义接口， `Runnable`该接口具有额外的方法，并由匿名类实现。

## 6.守护线程

Java 中的守护线程是指主线程退出应用程序时不会让 Java 虚拟机 (JVM) 保持运行的线程。

非守护线程即使主线程退出应用程序也会让 JVM 保持运行。

你可以通过 setDaemon() 方法将线程设置为守护线程。下面是在 Java 中创建守护线程的示例：

```java
Thread thread = new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Daemon Thread running.");
    }
});

thread.setDaemon(true);
thread.start();

try {
    thread.join();
} catch (InterruptedException e) {
    throw new RuntimeException(e);
}
```

最后一次调用 thread.join() 只是为了确保在守护进程线程有机会执行之前，主应用程序线程不会退出（并关闭 JVM）。

## 7.虚拟线程

下图显示了由平台线程执行的 Java 虚拟线程，这些虚拟线程又由 OS 线程执行。虽然平台线程一次只能执行一个虚拟线程，但当当前执行的虚拟线程进行阻塞调用（例如网络或并发数据结构）时，它可以切换到执行不同的虚拟线程。

![](C:\Users\Rain7\Desktop\笔记md\javapic\xnxc.png)

**虚拟线程被挂载到平台线程**

Java 虚拟线程由平台线程执行。平台线程一次只能执行一个虚拟线程。当虚拟线程由平台线程执行时 - 虚拟线程被称为已*安装* 到该线程。

新的虚拟线程将排队等待，直到平台线程准备好执行它。当平台线程准备就绪时，它将获取虚拟线程并开始执行它。

执行某些阻塞网络调用（IO）的虚拟线程将在等待响应时从平台线程中*卸载*。与此同时，平台线程可以执行另一个虚拟线程。

**虚拟线程之间没有时间切片**

虚拟线程之间没有时间分片。换句话说，平台线程不会在执行多个虚拟线程之间切换 - 除非在阻塞网络调用的情况下。只要虚拟线程正在运行代码并且没有被阻塞以等待网络响应 - 平台线程将继续执行相同的虚拟线程。

**创建 Java 虚拟线程**

要在 Java 中创建新的虚拟线程，请使用新的 Thread.ofVirtual() 工厂方法，并传递Runnable 接口 的实现。

```java
Runnable runnable = () -> {
    for(int i=0; i<10; i++) {
        System.out.println("Index: " + i);
    }
};

Thread vThread = Thread.ofVirtual().start(runnable);
```

此示例创建一个虚拟线程并立即启动它

如果不想让虚拟线程立即启动，可以使用 unstarted() 方法。

```java
Thread vThreadUnstarted = Thread.ofVirtual().unstarted(runnable);
```

要启动未启动的虚拟线程，只需调用它的 start() 方法，如下所示：

```java
vThreadUnstarted.start();
```

**虚拟线程的join()**

join() 方法会阻止调用线程，直到虚拟线程完成其工作并停止执行。

```java
Thread vThread = Thread.ofVirtual().start(runnable);

vThread.join();
```

## 8.线程冲突

线程冲突是指多个线程同时访问和操作共享数据时，由于执行顺序的不确定性而导致的数据不一致或程序逻辑错误的情况。

当多个线程访问同一个共享变量、对象或者其他资源时，每个线程的操作顺序和时间是由操作系统的线程调度机制决定的。

**解决方法：**

**使用同步块（synchronized 关键字）**

`synchronized`关键字可以用于修饰方法或者代码块。当一个线程进入被`synchronized`修饰的方法或代码块时，它会获取对象的锁。其他线程如果想要进入相同的被`synchronized`修饰的区域，必须等待锁被释放。

**使用显式锁（Lock 接口）**：

Java 的`java.util.concurrent.locks`包提供了`Lock`接口及其实现类（如`ReentrantLock`）来实现更灵活的同步。

与`synchronized`不同，`Lock`接口提供了如`lock`、`unlock`、`tryLock`等方法，可以根据具体情况进行更精细的控制。例如，可以在特定的条件下尝试获取锁，而不是像`synchronized`那样一直等待。

**线程安全**

在 Java 中，线程安全是指一段代码或者一个数据结构在多线程环境下能够正确地运行，不会出现数据不一致、程序逻辑错误或者其他意外行为。简单来说，就是多个线程同时访问和操作某个对象或方法时，该对象或方法的行为是可预测的、正确的。

**临界区**

可能发生线程冲突的地方

## 9.Volatile关键字

在 Java 中，`volatile`是一个关键字，用于修饰变量。它主要用于确保变量在多线程环境下的可见性。当一个变量被声明为`volatile`时，这意味着该变量的值一旦被某个线程修改，其他线程能够立即看到这个修改后的值。

**可见性问题的产生**：

在多线程环境下，每个线程都有自己的工作内存（也称为本地内存）。当一个线程访问一个共享变量时，它会先将变量的值从主内存复制到自己的工作内存中进行操作。如果没有适当的同步机制，当一个线程修改了共享变量的值后，这个新值可能不会立即更新到主内存中，其他线程也就无法及时看到这个新值。

**volatile 解决可见性问题**：

当一个变量被标记为`volatile`时，Java 虚拟机（JVM）会确保对这个变量的修改操作会立即更新到主内存中，并且其他线程在访问这个变量时，会先从主内存中重新读取该变量的值，而不是使用自己工作内存中的旧值。例如，假设有两个线程`A`和`B`，它们都访问一个`volatile`变量`flag`。当线程`A`修改了`flag`的值后，线程`B`能够马上察觉到这个变化并获取到新的值。

## 10.死锁

如果线程 1 锁定了 A，并尝试锁定 B，

而线程 2 已经锁定了 B，并尝试锁定 A，

则会出现死锁。

循环死锁：

线程 A 等待线程 B 持有的资源，

线程 B 等待线程 C 持有的资源，

线程 C 又等待线程 A 持有的资源

数据库死锁：

发生死锁的更复杂情况是数据库事务。数据库事务可能包含许多 SQL 更新请求。当在事务期间更新记录时，该记录将被锁定，无法从其他事务进行更新，直到第一个事务完成。因此，同一事务中的每个更新请求可能会锁定数据库中的某些记录。

**解决：**

锁排序：

为所有的资源分配一个唯一的顺序编号。当线程请求资源时，必须按照编号递增的顺序获取资源。这样就可以避免循环等待的情况。例如，在上述示例中，如果规定线程必须先获取编号较小的资源，那么就可以避免死锁。

锁定超时：

在获取锁的时候，可以设置一个超时时间。如果在规定时间内无法获取锁，就放弃获取并采取其他措施，如释放已经持有的资源，然后稍后再尝试获取。不过这种方法可能会导致程序的逻辑变得复杂，需要谨慎使用。

死锁检测：

Java 提供了一些工具来帮助检测死锁。例如，`jstack`是一个命令行工具，它可以打印出 Java 线程的栈信息，包括线程的状态和锁的持有情况。通过分析`jstack`输出的信息，可以发现是否存在死锁。另外，一些集成开发环境（IDE）也提供了死锁检测的功能。

## 11.线程阻塞

在 Java 多线程编程中，线程阻塞是指线程因为某些原因暂停执行，让出 CPU 资源，直到满足特定条件后才会继续执行。这是一种线程状态的转换，从运行状态（Runnable）转变为阻塞状态（Blocked）或等待状态（Waiting）。

**线程阻塞的常见原因**

**等待 I/O 操作完成：**

当线程执行输入 / 输出（I/O）操作，如读取文件、网络通信中的接收或发送数据时，如果数据尚未准备好或者操作尚未完成，线程会被阻塞。

例如，一个线程从网络套接字读取数据，在数据没有到达之前，线程会处于阻塞状态，直到有数据可读。

**等待获取锁（synchronized 或 Lock）：**

当多个线程竞争一个被`synchronized`关键字修饰的方法或者代码块，或者竞争一个`Lock`接口实现的锁时，没有获取到锁的线程会进入阻塞状态。

例如，在一个多线程访问共享资源（如共享的计数器）的场景中，使用`synchronized`关键字保证线程安全，当一个线程正在执行被`synchronized`修饰的方法时，其他试图访问该方法的线程会被阻塞。

**调用`Object.wait()`方法：**

线程可以调用对象的`wait()`方法，这会使线程进入等待状态，直到其他线程调用该对象的`notify()`或`notifyAll()`方法。

这种机制通常用于线程之间的协调。

例如，在生产者 - 消费者模型中，消费者线程在共享缓冲区为空时可以调用`wait()`方法进入等待状态，直到生产者生产了数据并调用`notify()`方法唤醒消费者。

**调用`Thread.sleep()`方法：**

线程可以主动调用`sleep()`方法来暂停自己的执行一段时间。

这是一种人为控制线程暂停的方式，线程会在指定的睡眠时间内处于阻塞状态。

例如，一个线程可以通过`Thread.sleep(1000)`暂停 1 秒钟，用于模拟一些耗时操作或者实现简单的定时功能。

**线程阻塞的状态转换和影响**

**状态转换：**

**从运行状态到阻塞状态：**

当线程遇到上述阻塞原因之一时，会从运行状态转换为阻塞状态。

例如，当线程执行`Object.wait()`操作后，它的状态就会从运行状态变为等待状态，此时线程不再占用 CPU 资源。

**从阻塞状态到运行状态：

当导致阻塞的条件满足时，线程会再次转换为运行状态。

例如，当一个线程等待的 I/O 操作完成，或者获取到了之前竞争的锁，或者被`Object.notify()`方法唤醒，它就会重新进入运行状态，继续执行后续的代码。

**对系统性能的影响：**

适当的线程阻塞是正常的并发编程操作，但如果大量线程长时间阻塞，可能会影响系统性能。

例如，如果有过多的线程因为等待 I/O 操作而阻塞，可能会导致 CPU 资源利用率低下，因为 CPU 在等待这些线程重新变为可运行状态。同时，线程的频繁阻塞和唤醒也会带来一定的开销，如上下文切换的成本。

## 12.饥饿（Starvation）

是指一个或多个线程由于无法获取所需的资源（如 CPU 时间片或锁）而长时间处于等待状态，无法执行任务。这是一种资源分配不公平导致的情况，就好像某些线程一直 “挨饿”，没有机会获取资源来执行。

**公平锁：**

**使用`ReentrantLock`实现公平锁**：

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
class FairLockExample {
   private final Lock fairLock = new ReentrantLock(true);
   public void doWork() {
       fairLock.lock();
       try {
           // 对共享资源进行操作
           System.out.println(Thread.currentThread().getName() + "获取了公平锁");
       } finally {
           fairLock.unlock();
       }
   }
}
```

## 13.线程池

线程池是一种多线程处理形式，它预先创建了一定数量的线程，并将这些线程存储在一个 “池子” 中。当有任务需要执行时，从线程池中获取一个线程来执行任务，任务执行完毕后，线程不会销毁，而是返回线程池等待下一个任务，从而避免了频繁创建和销毁线程带来的开销。

**作用**：

**性能提升**：

线程的创建和销毁是有成本的，包括系统资源的分配（如内存）和回收。

线程池通过重复利用已创建的线程，减少了这种开销，提高了系统的性能和响应速度。

例如，在一个 Web 服务器中，频繁地处理 HTTP 请求，如果每次请求都创建一个新线程，会消耗大量资源；而使用线程池可以高效地处理请求。

**资源管理与控制**：

可以通过设置线程池的大小来控制同时执行任务的线程数量，从而有效地管理系统资源。

比如，限制线程池的大小为 10，就可以确保系统不会因为创建过多线程而导致资源耗尽。

**提供任务队列**：

当线程池中的所有线程都在执行任务，而又有新的任务到来时，这些新任务会被放入一个任务队列中等待。

这使得任务可以按照一定的顺序进行处理。

**Java 中线程池的实现类（Executor 框架）**

**Executor 接口和 ExecutorService 接口**：

**Executor 接口**：

这是 Java 线程池框架的基础接口，它定义了一个简单的方法`execute(Runnable command)`，用于提交一个可执行的任务（`Runnable`对象）到线程池中执行。

```java
import java.util.concurrent.Executor;
public class SimpleExecutorExample {
   public static void main(String[] args) {
       Executor executor = new ThreadPoolExecutor(1, 1, 0L, TimeUnit.MILLISECONDS,
               new LinkedBlockingQueue<>());
       executor.execute(() -> System.out.println("任务执行"));
   }
}
```

**ExecutorService 接口**：

它继承自`Executor`接口，提供了更多的方法，如`submit`（用于提交任务并返回一个`Future`对象，用于获取任务结果）、`shutdown`（用于平滑地关闭线程池）和`shutdownNow`（用于立即关闭线程池）等。

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
public class ExecutorServiceExample {
   public static void main(String[] args) {
       ExecutorService executorService = Executors.newFixedThreadPool(3);
       Future<?> future = executorService.submit(() -> System.out.println("任务执行"));
       // 关闭线程池
       executorService.shutdown();
   }
}
```

**ThreadPoolExecutor 类**：

这是 Java 中最核心的线程池实现类。它有多个构造参数，用于灵活地配置线程池的各种属性，如核心线程数、最大线程数、线程存活时间、时间单位和任务队列等。

```java
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;
public class ThreadPoolExecutorExample {
   public static void main(String[] args) {
       BlockingQueue<Runnable> workQueue = new LinkedBlockingQueue<>();
       ThreadPoolExecutor threadPool = new ThreadPoolExecutor(2, 4, 10, TimeUnit.SECONDS, workQueue);
       for (int i = 0; i < 6; i++) {
           threadPool.execute(() -> System.out.println(Thread.currentThread().getName() + "执行任务"));
       }
       threadPool.shutdown();
   }
}
```

**线程池的主要参数和配置策略**

- **核心线程数（corePoolSize）**：

  线程池长期维持的线程数量。

  当有新任务到来，且线程池中的线程数量小于核心线程数时，会创建新的线程来执行任务，而不是将任务放入任务队列。

  例如，对于一个长期有稳定任务量的系统，可以将核心线程数设置为能处理大部分任务的数量。

- **最大线程数（maximumPoolSize）**：

  线程池允许创建的最大线程数量。

  当任务队列已满，且线程数量小于最大线程数时，会创建新的线程来执行任务。

  这是为了应对任务突发高峰，防止任务堆积过多。例如，在一个有突发流量的 Web 应用中，可以根据预期的最大并发请求量来设置最大线程数。

- **线程存活时间（keepAliveTime）和时间单位（unit）**：

  当线程池中的线程数量超过核心线程数时，空闲线程（没有任务执行的线程）在存活时间后会被销毁。

  这可以避免线程资源的浪费。

  例如，如果设置存活时间为 60 秒，当一个非核心线程空闲了 60 秒后，就会被销毁。

- **任务队列（workQueue）**：

  用于存储等待执行的任务。

  常见的任务队列有`LinkedBlockingQueue`（无界队列）、`ArrayBlockingQueue`（有界队列）和`SynchronousQueue`（不存储任务，直接将任务交给线程执行）。

  选择合适的任务队列会影响线程池的行为。

  例如，使用`LinkedBlockingQueue`可以存储大量任务，但可能导致任务堆积过多；使用`SynchronousQueue`可以保证任务被及时处理，但可能需要更多的线程。

**线程池的生命周期和状态管理**

生命周期阶段：

- **创建（Creation）**：通过`ThreadPoolExecutor`构造函数或者`Executors`工厂方法创建线程池。
- **运行（Running）**：线程池处于正常运行状态，可以接收和执行任务。
- **关闭（Shutdown）**：调用`shutdown`方法后，线程池不再接受新任务，但会继续执行已接收的任务，直到所有任务完成或者超时。
- **终止（Termination）**：当线程池中的所有任务都执行完毕，并且所有线程都被销毁后，线程池进入终止状态。

状态转换：

- 从创建到运行：线程池创建后自动进入运行状态，开始接收和执行任务。
- 从运行到关闭：调用`shutdown`方法后，线程池状态从运行转换为关闭状态。
- 从关闭到终止：在关闭状态下，当所有任务完成和线程销毁后，线程池进入终止状态。如果在关闭状态下调用`shutdownNow`方法，可以立即中断所有正在执行的任务，强制线程池进入终止状态，但这种方式可能会导致部分任务无法正常完成。

**使用场景：**

**Web 服务器和网络应用**：

用于处理大量的 HTTP 请求，如 Tomcat 服务器内部就使用了线程池来处理请求。

**任务调度系统**：

可以将定时任务或异步任务放入线程池执行，提高系统的并发处理能力。

**大数据处理和批量任务**：

在处理大量数据或批量任务时，通过线程池可以高效地利用系统资源，例如对海量数据进行并行计算。

**最佳实践：**

**合理配置线程池参数**：

根据任务的类型（是 CPU 密集型还是 I/O 密集型）和系统资源来确定核心线程数、最大线程数等参数。对于 CPU 密集型任务，线程数一般不宜过多，可设置为 CPU 核心数 + 1；对于 I/O 密集型任务，可以适当增加线程数。

**正确处理任务异常：**

在任务执行过程中可能会出现异常，要确保异常得到正确处理，避免影响线程池的正常运行。例如，可以在任务代码中使用`try - catch`块来捕获异常，或者在`Future`对象获取结果时处理异常。

**监控和调整线程池状态：**

在生产环境中，要对线程池进行监控，包括线程池的大小、任务队列的长度、任务执行时间等参数。根据监控结果，可以适时调整线程池的配置，以达到最佳性能。

## 14.非阻塞算法

在 Java 并发编程中，非阻塞算法是一种设计用于在多线程环境下能够高效并发执行，并且不会导致线程阻塞的算法。与传统的基于锁的同步算法不同，非阻塞算法不依赖于锁来控制对共享资源的访问，从而避免了线程因为等待锁而被阻塞的情况。

**非阻塞算法的实现原理 - 原子操作与 CAS（比较并交换）**

**原子操作**：

原子操作是指不会被线程调度机制中断的操作，它在执行过程中要么全部执行完成，要么不执行，不会出现执行到一半被其他线程干扰的情况。

在 Java 中，有一些基本类型的操作是原子性的，如对`volatile`变量的读写操作在一定程度上是原子的，但对于复合操作（如`++`操作）就不是原子的。

**CAS 操作**：

比较并交换（Compare - and - Swap，CAS）是实现非阻塞算法的关键机制。

它有三个操作数：内存位置（V）、旧的预期值（A）和新值（B）。

CAS 操作会先比较内存位置 V 的值是否等于旧的预期值 A，如果相等，则将内存位置 V 的值更新为新值 B；如果不相等，则说明有其他线程已经修改了这个值，操作失败。

这个过程是原子性的。

Java 中的`java.util.concurrent.atomic`包下的原子类（如`AtomicInteger`、`AtomicLong`等）内部就使用了 CAS 操作来实现原子性。例如，`AtomicInteger`的`incrementAndGet`方法就利用 CAS 来实现原子自增操作，代码逻辑大致如下：

```java
 public final int incrementAndGet() {
     for (;;) {
         int current = get();
         int next = current + 1;
         if (compareAndSet(current, next))
             return next;
     }
 }
```

在这里，`compareAndSet`方法就是执行 CAS 操作，它会不断尝试更新`AtomicInteger`的值，直到成功。

**非阻塞算法的优势**

**高并发性能**：

由于不需要等待锁，线程之间的竞争开销大大减少，在高并发场景下能够提供更好的性能。

例如，在一个高并发的计数器应用中，使用非阻塞算法（如`AtomicInteger`）来计数，多个线程可以同时尝试更新计数器的值，而不会像基于锁的计数器那样因为线程阻塞而产生性能瓶颈。

**避免死锁和活锁**：

非阻塞算法不依赖于锁的获取和释放顺序，所以不会出现像基于锁的算法那样由于锁的不当使用而导致的死锁和活锁问题。

例如，在一个复杂的多线程系统中，如果有多个线程按照不同的顺序获取多个锁，很容易出现死锁；而非阻塞算法不存在这种问题。

**更好的响应性**：

线程不会因为等待锁而被阻塞，所以系统的响应性更好。

例如，在一个实时系统中，非阻塞算法可以确保线程能够及时处理其他任务，而不是被阻塞等待锁的释放。

**非阻塞算法的应用场景和示例**

**计数器和统计数据收集：**

如前面提到的计数器应用，使用`AtomicInteger`或`AtomicLong`来记录系统中的访问次数、请求数量等统计信息。

例如，在一个 Web 服务器中，可以使用`AtomicInteger`来统计每个小时的 HTTP 请求数量。

```java
 import java.util.concurrent.atomic.AtomicInteger;
 public class RequestCounter {
     private final AtomicInteger counter = new AtomicInteger(0);
     public void increment() {
         counter.incrementAndGet();
     }
     public int getCount() {
         return counter.get();
     }
 }
```

**并发数据结构**：

**无锁队列（Lock - Free Queue）**：这是一种常见的非阻塞数据结构。

在多线程环境下，多个线程可以同时对队列进行插入和删除操作，而不会因为锁而阻塞。

实现无锁队列的关键是使用原子操作和 CAS。

例如，一个简单的基于数组的无锁队列可以通过维护队头和队尾指针（使用`AtomicInteger`来实现原子性），并利用 CAS 操作来更新指针位置来实现。以下是一个简单的概念性示例：

```java
    import java.util.concurrent.atomic.AtomicInteger;
    public class LockFreeQueue<T> {
       private final T[] array;
       private final AtomicInteger head = new AtomicInteger(0);
       private final AtomicInteger tail = new AtomicInteger(0);
       public LockFreeQueue(int capacity) {
           array = (T[]) new Object[capacity];
       }
       public boolean offer(T element) {
           int currentTail = tail.get();
           int nextTail = (currentTail + 1) % array.length;
           if (nextTail == head.get()) {
               return false; // 队列已满
           }
           array[currentTail] = element;
           tail.compareAndSet(currentTail, nextTail);
           return true;
       }
       public T poll() {
           int currentHead = head.get();
           if (currentHead == tail.get()) {
               return null; // 队列已空
           }
           T element = array[currentHead];
           int nextHead = (currentHead + 1) % array.length;
           head.compareAndSet(currentHead, nextHead);
           return element;
       }
    }
```

在这个示例中，`offer`方法用于向队列中插入元素，`poll`方法用于从队列中取出元素。通过使用原子的队头和队尾指针以及 CAS 操作，多个线程可以并发地对队列进行操作，而不会出现阻塞的情况。

**非阻塞算法的局限性和挑战**

**ABA 问题：**

CAS 操作存在 ABA 问题。

即一个值从 A 变为 B，再变回 A，此时使用 CAS 操作可能会认为这个值没有被修改过。

在某些场景下，这可能会导致问题。

例如，在一个链表数据结构中，如果一个节点被删除后又重新插入相同的节点，使用 CAS 操作来判断节点是否被修改时可能会出现误判。解决 ABA 问题的一种方法是使用带有版本号的原子引用（如`AtomicStampedReference`），它不仅比较引用的值，还比较版本号，这样即使值相同，但版本号不同，也能识别出变化。

**实现复杂性：**

非阻塞算法的实现通常比基于锁的算法更复杂。

需要深入理解原子操作、CAS 操作以及内存模型等知识，并且在实现过程中容易出现错误。

例如，在设计一个复杂的无锁数据结构时，要考虑到各种并发情况下的正确性，代码的调试和维护也相对困难。

**性能在低并发场景下可能不佳：**

非阻塞算法在高并发场景下性能优势明显，但在低并发场景下，由于不断地进行 CAS 操作（CAS 操作虽然是原子的，但也有一定的开销），其性能可能不如简单的基于锁的算法。

例如，在一个只有少量线程访问共享资源的系统中，使用非阻塞算法可能会因为频繁的 CAS 尝试而浪费资源。

## 15.springboot实现线程池

在 Spring Boot 中实现线程池可以通过 `ThreadPoolTaskExecutor` 或直接使用 Java 的 `ExecutorService` 来实现。Spring Boot 提供了对线程池的良好支持，可以方便地配置和管理线程池。

------

### **1. 使用 `ThreadPoolTaskExecutor` 实现线程池**

`ThreadPoolTaskExecutor` 是 Spring 提供的一个线程池实现，适合在 Spring Boot 项目中使用。

#### **步骤 1：配置线程池**

在 Spring Boot 的配置类中定义线程池 Bean。

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor;

@Configuration
public class ThreadPoolConfig {

    @Bean(name = "taskExecutor")
    public ThreadPoolTaskExecutor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        // 核心线程数
        executor.setCorePoolSize(5);
        // 最大线程数
        executor.setMaxPoolSize(10);
        // 队列容量
        executor.setQueueCapacity(20);
        // 线程名前缀
        executor.setThreadNamePrefix("Async-");
        // 拒绝策略
        executor.setRejectedExecutionHandler(new java.util.concurrent.ThreadPoolExecutor.CallerRunsPolicy());
        // 初始化
        executor.initialize();
        return executor;
    }
}
```

#### **步骤 2：使用线程池**

在需要异步执行的方法上使用 `@Async` 注解，并指定线程池 Bean 名称。

```java
import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;

@Service
public class MyService {

    @Async("taskExecutor") // 指定线程池 Bean 名称
    public void asyncTask() {
        System.out.println("异步任务开始执行，线程名称：" + Thread.currentThread().getName());
        try {
            Thread.sleep(5000); // 模拟耗时操作
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("异步任务执行完成，线程名称：" + Thread.currentThread().getName());
    }
}
```

#### **步骤 3：启用异步支持**

在 Spring Boot 启动类或配置类上添加 `@EnableAsync` 注解。

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.scheduling.annotation.EnableAsync;

@SpringBootApplication
@EnableAsync // 启用异步支持
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

#### **步骤 4：测试线程池**

在 Controller 中调用异步方法。

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    @Autowired
    private MyService myService;

    @GetMapping("/runAsyncTask")
    public String runAsyncTask() {
        myService.asyncTask();
        return "异步任务已启动";
    }
}
```

访问 `/runAsyncTask` 接口，可以看到异步任务在后台线程池中执行。

------

### **2. 使用 Java 的 `ExecutorService` 实现线程池**

如果不依赖 Spring 的线程池管理，可以直接使用 Java 的 `ExecutorService`。

#### **步骤 1：创建线程池**

在 Service 中创建线程池。

```java
import org.springframework.stereotype.Service;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

@Service
public class MyService {

    private final ExecutorService executorService = Executors.newFixedThreadPool(5);

    public void asyncTask() {
        executorService.submit(() -> {
            System.out.println("异步任务开始执行，线程名称：" + Thread.currentThread().getName());
            try {
                Thread.sleep(5000); // 模拟耗时操作
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("异步任务执行完成，线程名称：" + Thread.currentThread().getName());
        });
    }
}
```

#### **步骤 2：测试线程池**

在 Controller 中调用异步方法。

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    @Autowired
    private MyService myService;

    @GetMapping("/runAsyncTask")
    public String runAsyncTask() {
        myService.asyncTask();
        return "异步任务已启动";
    }
}
```

------

### **3. 线程池配置参数说明**

| 参数                       | 说明                                                         |
| :------------------------- | :----------------------------------------------------------- |
| `corePoolSize`             | 核心线程数，线程池中始终保持的线程数量。                     |
| `maxPoolSize`              | 最大线程数，线程池中允许的最大线程数量。                     |
| `queueCapacity`            | 任务队列容量，当线程数达到核心线程数时，新任务会放入队列中等待执行。 |
| `threadNamePrefix`         | 线程名前缀，方便日志跟踪。                                   |
| `rejectedExecutionHandler` | 拒绝策略，当线程池和队列都满时如何处理新任务。               |

------

### **4. 拒绝策略**

| 策略名称              | 说明                                             |
| :-------------------- | :----------------------------------------------- |
| `AbortPolicy`         | 直接抛出异常（默认策略）。                       |
| `CallerRunsPolicy`    | 由调用线程执行该任务。                           |
| `DiscardPolicy`       | 直接丢弃任务，不抛出异常。                       |
| `DiscardOldestPolicy` | 丢弃队列中最旧的任务，然后尝试重新提交当前任务。 |

------

### **5. 注意事项**

1. **线程池资源释放**：
   - 如果使用 `ExecutorService`，需要在应用关闭时手动关闭线程池。
   - 使用 `ThreadPoolTaskExecutor` 时，Spring 会自动管理线程池的生命周期。
2. **线程池大小设置**：
   - 根据任务类型（CPU 密集型或 IO 密集型）合理设置线程池大小。
   - CPU 密集型任务：线程数 ≈ CPU 核心数。
   - IO 密集型任务：线程数 ≈ CPU 核心数 * 2。
3. **异步方法的返回值**：
   - 如果需要获取异步方法的返回值，可以使用 `Future` 或 `CompletableFuture`。

------

### **总结**

在 Spring Boot 中实现线程池有两种主要方式：

1. 使用 `ThreadPoolTaskExecutor`，适合与 Spring 集成，支持配置化和声明式使用。
2. 使用 Java 的 `ExecutorService`，适合不依赖 Spring 的场景。

通过合理配置线程池参数和拒绝策略，可以提升应用的并发处理能力和稳定性。