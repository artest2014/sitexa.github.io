---
layout: post
title: MapReduce的运行原理
category: 'technology'
---


江湖传说永流传：谷歌技术有"三宝"，GFS、MapReduce和大表（BigTable）！

谷歌在03到06年间连续发表了三篇很有影响力的文章，分别是03年SOSP的GFS，04年OSDI的MapReduce，和06年OSDI的BigTable。SOSP和OSDI都是操作系统领域的顶级会议，在计算机学会推荐会议里属于A类。SOSP在单数年举办，而OSDI在双数年举办。

##  MapReduce是干啥的

![image](/images/mapreduce01.jpg)

Hadoop实际上就是谷歌三宝的开源实现，Hadoop MapReduce对应Google MapReduce，HBase对应BigTable，HDFS对应GFS。HDFS（或GFS）为上层提供高效的非结构化存储服务，HBase（或BigTable）是提供结构化数据服务的分布式数据库，Hadoop MapReduce（或Google MapReduce）是一种并行计算的编程模型，用于作业调度。
GFS和BigTable已经为我们提供了高性能、高并发的服务，但是并行编程可不是所有程序员都玩得转的活儿，如果我们的应用本身不能并发，那GFS、BigTable也都是没有意义的。MapReduce的伟大之处就在于让不熟悉并行编程的程序员也能充分发挥分布式系统的威力。

简单概括的说，MapReduce是将一个大作业拆分为多个小作业的框架（大作业和小作业应该本质是一样的，只是规模不同），用户需要做的就是决定拆成多少份，以及定义作业本身。

下面用一个贯穿全文的例子来解释MapReduce是如何工作的。

##  例子：统计词频

如果我想统计下过去10年计算机论文出现最多的几个单词，看看大家都在研究些什么，那我收集好论文后，该怎么办呢？

方法一：我可以写一个小程序，把所有论文按顺序遍历一遍，统计每一个遇到的单词的出现次数，最后就可以知道哪几个单词最热门了。

这种方法在数据集比较小时，是非常有效的，而且实现最简单，用来解决这个问题很合适。

方法二：写一个多线程程序，并发遍历论文。

这个问题理论上是可以高度并发的，因为统计一个文件时不会影响统计另一个文件。当我们的机器是多核或者多处理器，方法二肯定比方法一高效。但是写一个多线程程序要比方法一困难多了，我们必须自己同步共享数据，比如要防止两个线程重复统计文件。

方法三：把作业交给多个计算机去完成。

我们可以使用方法一的程序，部署到N台机器上去，然后把论文集分成N份，一台机器跑一个作业。这个方法跑得足够快，但是部署起来很麻烦，我们要人工把程序copy到别的机器，要人工把论文集分开，最痛苦的是还要把N个运行结果进行整合（当然我们也可以再写一个程序）。

方法四：让MapReduce来帮帮我们吧！

MapReduce本质上就是方法三，但是如何拆分文件集，如何copy程序，如何整合结果这些都是框架定义好的。我们只要定义好这个任务（用户程序），其它都交给MapReduce。

在介绍MapReduce如何工作之前，先讲讲两个核心函数map和reduce以及MapReduce的伪代码。

##  map函数和reduce函数

map函数和reduce函数是交给用户实现的，这两个函数定义了任务本身。

map函数：接受一个键值对（key-value pair），产生一组中间键值对。MapReduce框架会将map函数产生的中间键值对里键相同的值传递给一个reduce函数。

reduce函数：接受一个键，以及相关的一组值，将这组值进行合并产生一组规模更小的值（通常只有一个或零个值）。

统计词频的MapReduce函数的核心代码非常简短，主要就是实现这两个函数。

```
map(String key, String value):
    // key: document name
    // value: document contents
    for each word w in value:
        EmitIntermediate(w, "1");

reduce(String key, Iterator values):
    // key: a word
    // values: a list of counts
    int result = 0;
    for each v in values:
        result += ParseInt(v);
        Emit(AsString(result));

```

在统计词频的例子里，map函数接受的键是文件名，值是文件的内容，map逐个遍历单词，每遇到一个单词w，就产生一个中间键值对<w, "1">，这表示单词w咱又找到了一个；MapReduce将键相同（都是单词w）的键值对传给reduce函数，这样reduce函数接受的键就是单词w，值是一串"1"（最基本的实现是这样，但可以优化），个数等于键为w的键值对的个数，然后将这些“1”累加就得到单词w的出现次数。最后这些单词的出现次数会被写到用户定义的位置，存储在底层的分布式存储系统（GFS或HDFS）。

##  MapReduce是如何工作的

![image](/images/mapreduce02.jpg)

上图是论文里给出的流程图。一切都是从最上方的user program开始的，user program链接了MapReduce库，实现了最基本的Map函数和Reduce函数。图中执行的顺序都用数字标记了。

-   MapReduce库先把user program的输入文件划分为M份（M为用户定义），每一份通常有16MB到64MB，如图左方所示分成了split0~4；然后使用fork将用户进程拷贝到集群内其它机器上。
-   user program的副本中有一个称为master，其余称为worker，master是负责调度的，为空闲worker分配作业（Map作业或者Reduce作业），worker的数量也是可以由用户指定的。
-   被分配了Map作业的worker，开始读取对应分片的输入数据，Map作业数量是由M决定的，和split一一对应；Map作业从输入数据中抽取出键值对，每一个键值对都作为参数传递给map函数，map函数产生的中间键值对被缓存在内存中。
-   缓存的中间键值对会被定期写入本地磁盘，而且被分为R个区，R的大小是由用户定义的，将来每个区会对应一个Reduce作业；这些中间键值对的位置会被通报给master，master负责将信息转发给Reduce worker。
-   master通知分配了Reduce作业的worker它负责的分区在什么位置（肯定不止一个地方，每个Map作业产生的中间键值对都可能映射到所有R个不同分区），当Reduce worker把所有它负责的中间键值对都读过来后，先对它们进行排序，使得相同键的键值对聚集在一起。因为不同的键可能会映射到同一个分区也就是同一个Reduce作业（谁让分区少呢），所以排序是必须的。
-   reduce worker遍历排序后的中间键值对，对于每个唯一的键，都将键与关联的值传递给reduce函数，reduce函数产生的输出会添加到这个分区的输出文件中。
-   当所有的Map和Reduce作业都完成了，master唤醒正版的user program，MapReduce函数调用返回user program的代码。

所有执行完毕后，MapReduce输出放在了R个分区的输出文件中（分别对应一个Reduce作业）。用户通常并不需要合并这R个文件，而是将其作为输入交给另一个MapReduce程序处理。整个过程中，输入数据是来自底层分布式文件系统（GFS）的，中间数据是放在本地文件系统的，最终输出数据是写入底层分布式文件系统（GFS）的。而且我们要注意Map/Reduce作业和map/reduce函数的区别：Map作业处理一个输入数据的分片，可能需要调用多次map函数来处理每个输入键值对；Reduce作业处理一个分区的中间键值对，期间要对每个不同的键调用一次reduce函数，Reduce作业最终也对应一个输出文件。

我更喜欢把流程分为三个阶段。第一阶段是准备阶段，包括1、2，主角是MapReduce库，完成拆分作业和拷贝用户程序等任务；第二阶段是运行阶段，包括3、4、5、6，主角是用户定义的map和reduce函数，每个小作业都独立运行着；第三阶段是扫尾阶段，这时作业已经完成，作业结果被放在输出文件里，就看用户想怎么处理这些输出了。

##  词频是怎么统计出来的

结合第四节，我们就可以知道第三节的代码是如何工作的了。假设咱们定义M=5，R=3，并且有6台机器，一台master。

![image](/images/mapreduce03.jpg)

这幅图描述了MapReduce如何处理词频统计。由于map worker数量不够，首先处理了分片1、3、4，并产生中间键值对；当所有中间值都准备好了，Reduce作业就开始读取对应分区，并输出统计结果。

##  用户的权利

用户最主要的任务是实现map和reduce接口，但还有一些有用的接口是向用户开放的。

-   an input reader。这个函数会将输入分为M个部分，并且定义了如何从数据中抽取最初的键值对，比如词频的例子中定义文件名和文件内容是键值对。
-   a partition function。这个函数用于将map函数产生的中间键值对映射到一个分区里去，最简单的实现就是将键求哈希再对R取模。
-   a compare function。这个函数用于Reduce作业排序，这个函数定义了键的大小关系。
-   an output writer。负责将结果写入底层分布式文件系统。
-   a combiner function。实际就是reduce函数，这是用于前面提到的优化的，比如统计词频时，如果每个<w, "1">要读一次，因为reduce和map通常不在一台机器，非常浪费时间，所以可以在map执行的地方先运行一次combiner，这样reduce只需要读一次<w, "n">了。

map和reduce函数就不多说了。

##  MapReduce的实现

目前MapReduce已经有多种实现，除了谷歌自己的实现外，还有著名的hadoop，区别是谷歌是c++，而hadoop是用java。另外斯坦福大学实现了一个在多核/多处理器、共享内存环境内运行的MapReduce，称为Phoenix，相关的论文发表在07年的HPCA，是当年的最佳论文哦！

