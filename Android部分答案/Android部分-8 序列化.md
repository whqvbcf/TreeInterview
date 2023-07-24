### 2.8 序列化

- 1.什么是序列化 & 能用来干什么？

> [点击查看答案](https://www.cnblogs.com/wxgblogs/p/5849951.html)
概念
序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进行读写操作时所引发的问题。
序列化：把Java对象转换为字节序列的过程。
反序列化：把字节序列恢复为Java对象的过程。
用途
1、把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中;
2、在网络上传送对象的字节序列。
- 2.Android中序列化方式有几种？说说它们的区别。

> [点击查看答案](https://www.cnblogs.com/yezhennan/p/5527506.html)
Android中实现序列化的两种方式
（1）.Implements Serializable 接口 (声明一下即可)
（2）.Implements Parcelable 接口(不仅仅需要声明,还需要实现内部的相应方法)
Parcelable与Serializable的性能比较
首先Parcelable的性能要强于Serializable的原因我需要简单的阐述一下
  1）. 在内存的使用中,前者在性能方面要强于后者
  2）. 后者在序列化操作的时候会产生大量的临时变量,(原因是使用了反射机制)从而导致GC的频繁调用,因此在性能上会稍微逊色
  3）. Parcelable是以Ibinder作为信息载体的.在内存上的开销比较小,因此在内存之间进行数据传递的时候,Android推荐使用Parcelable,既然是内存方面比价有优势,那么自然就要优先选择.
  4）. 在读写数据的时候,Parcelable是在内存中直接进行读写,而Serializable是通过使用IO流的形式将数据读写入在硬盘上.
综上：虽然Parcelable的性能要强于Serializable,但是仍然有特殊的情况需要使用Serializable,而不去使用Parcelable,因为Parcelable无法将数据进行持久化,因此在将数据保存在磁盘的时候,仍然需要使用后者,因为前者无法很好的将数据进行持久化.(原因是在不同的Android版本当中,Parcelable可能会不同,因此数据的持久化方面仍然是使用Serializable)

- 3.如果想要序列化的类中某些字段不序列化，那么应该怎么做？

> 使用关键字：transient