### 2.5 Handler

- 1.子线程一定不能更新UI吗？

> 这个问题要回答2个要点：  
> 第1个要点：是否有些控件支持在子线程更新UI呢？比如：SurfaceViw
> 第2个要点：在Activity的onResume()生命周期函数之前是可以在子线程中更新UI的。

- 2.给我说说Handler的原理。

> [点击查看答案](https://www.cnblogs.com/huhx/p/handlerTheory.html)

- 3.Handler导致的内存泄露你是如何解决的？

> **Handler导致内存泄漏的原因是**：非静态内部类持有外部类的引用，导致外部类在没有被使用的时候，迟迟不能被回收，从而导致内存泄漏。即非静态Handler内部类持有外部Activity的引用，导致外部Activity退出/销毁的时候，它迟迟不能被回收，最终导致Activity的内存泄漏。
> **解决方法**：将Handler类声明为静态，如果Handler需要访问外部类Activity的成员变量或者成员方法，可以用弱引用的方式解决。

- 4.如何使用Handler让子线程和子线程通信？
- 5.你能给我说说Handler的设计原理？

> [4~5题答案](https://blog.csdn.net/ClAndEllen/article/details/79343538)

- 6.HandlerThread是什么 & 原理 & 使用场景？

> [点击查看答案](https://blog.csdn.net/ClAndEllen/article/details/79346492)

- 7.IdleHandler是什么 & 原理？

> [点击查看答案](https://www.jianshu.com/p/a1d945c4f5a6)

- 8.一个线程能否创建多个Handler,Handler和Looper之间的对应关系？

> 一个线程可以有多个Handler，但是一个线程只能有一个Looper，一个MessageQueue。因此它们之间的关系是一个线程只能有一个Looper,一个MessageQueue,多个Handler。

- 9.为什么Android系统不建议子线程访问UI？

>首先，UI控件不是线程安全的，如果多线程并发访问UI控件可能会出现不可预期的状态

>那为什么系统不对UI控件的访问加上锁机制呢？

>缺点有两个：

>加上锁机制会让UI访问的逻辑变得复杂;
>锁机制会降低UI访问的效率，因为锁机制会阻塞某些线程的执行;

- 10.Looper死循环为什么不会导致应用卡死？

> [点击查看答案](https://www.jianshu.com/p/cfe50b8b0a41)
> [这个答案回答挺好](https://www.jianshu.com/p/4b52800e3523)
Looper无限循环如何导致阻塞的
Looper无限循环是Looper不停取MessageQueen中的Message并执行这个message的一种机制。我们的APP中的事件，如Activity的生命周期切换、点击、长按、滑动、都是依赖这种机制。
如果主线程的MessageQueue中没有消息，便会阻塞在Loop的queue.next()中的nativePollOnce方法。这个时候主线程会进入休眠状态并释放CPU资源，如果下一个消息到达或者有事物发生，通过向pipe管道写入数据来进行唤醒主线程工作。
Looper无限循环为啥没有ANR?
Looper循环的阻塞是在消息队列无消息需要处理时的一种机制，这种机制就是让CPU停下来去做别的事。而且消息队列无消息，那么就是需要需要让cpu停下来，避免cpu空转，这个机制和ANR是没有关系的，完全不是同一个事，所以自然不会导致ANR

- 11.使用Handler的postDealy后消息队列有什么变化？

> [点击查看答案](https://blog.csdn.net/qingtiantianqing/article/details/72783952)

- 12.可以在子线程直接new一个Handler出来吗？

> [点击查看答案](https://www.cnblogs.com/jingmo0319/p/5730963.html)

- 13.Message对象创建的方式有哪些 & 区别？

> [点击查看答案](https://blog.csdn.net/dfskhgalshgkajghljgh/article/details/52672115)