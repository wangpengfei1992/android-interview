## okio ##

学习链接：[https://blog.csdn.net/yhaolpz/article/details/54948521](https://blog.csdn.net/yhaolpz/article/details/54948521)

### okio概念 ###

1.okio是一个由square公司开发的开源库，它弥补了Java.io和java.nio的不足，能够更方便快速的读取、存储和处理数据。

2.okio有自己的流类型Source和Sink，对应于java.io的InputStream和OutputStream。

3.okio内部引入了ByteString和Buffer，提升了效率和性能。

4.okio引入了超时机制。

### Source和Sink ###

Source代表输入流，Sink代表输出流，Source和Sink的实现逻辑基本相似

### Buffer ###

**通过Buffer的应用，才实现了okio的高效性**

Buffer是BufferedSink和BufferedSource的实现类，因此它既可以用来读数据，也可以用来写数据。在Buffer的注释中说明了okio的高效性：

1. copy数组时仅仅改变底层字节数组的所有权，而不是把数据从一块内存复制到另一块内存中
2. 如ArrayList一样根据需要动态分配内存大小
3. 避免了数组创建时的zero-fill，降低了GC的频率。


Buffer是通过Segment和SegmentPool来实现以上高效功能的，Segment译为片段，**okio将数据也就是Buffer分割成片段**，同时Segment有前置节点和后置节点，**构成了一个双向循环链表**，如图：

![](https://img-blog.csdn.net/20170214112444337?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWhhb2xweg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


当我们想要把一个Buffer中的数据移动到另一个Buffer时，上面方法可能会处理的几种情景如下（【91%，61%】表示一个Buffer中有两个片段，91%表示此片段中已有数据占片段最大容量的91%）：

将 【72%】写入 【91%，61%】 –> 【91%，61%，72%】 

将 【99%，3%】写入 【100%，2%】 –> 【100%，2%，99%，3%】 

将 【3%，99%】写入 【100%，2%】 –> 【100%，5%，99%】 

将 【92%，82%】的头片段的30%写入 【51%，91%】 –> 首先把源Buffer分割成【30%，62%，82%】，移动 –> 【51%，91%，30%】

结合这几种情景再去分析write方法，逻辑就十分清晰了，其中有一点就是在程序中的逻辑往Buffer中插入数据是往前置节点插入的，而这些情景将数据插入到了尾部，其实这并不矛盾，因为片段本身就是双向链表，只要你插入数据的顺序和读取数据的顺序相对应就可以，上面的情景主要为了分析数据移动的可能结果。这里分析了在Buffer中是怎么通过Segment实现高效的，没有涉及到SegmentPool，SegmentPool的应用十分简单，只有take取片段和recycle回收片段两个方法，这里就不再展开了。


### okio的框架图 ###

![](https://img-blog.csdn.net/20170216164534656?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWhhb2xweg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



### 最后再来总结一下okio的优点： ###

1 **使用简便**

Buffer是处理可变byte序列的利器，它可以根据使用情况自动增长，在使用过程中不用关心位置的处理

Java.IO读取不同类型数据要用DataInputStream来包装，使用缓存要使用BufferedOutputStream，而在okio中BufferedSink/BufferedSource就具有以上所有功能

okio提供了方便压缩及字符常用处理工具

2 **速度快** （数组加双向链表）

okio采用了segment机制进行内存共享，极大减少了copy操作带来的时间消耗，加快了读写速度

okio引入ByteString使其在byte[]与String之间转换速度非常快

3 **稳定**

okio提供了超时机制，不仅在IO操作上加上超时的判定，包括close，flush之类的方法中都有超时机制

4 **内存消耗小**

虽然okio在byteString采用**空间换时间**，但是对内存也做了极致的优化，总体还是极大提高了性能

okio的segment机制进行内存复用，上传大文件时完全不用考虑OOM
