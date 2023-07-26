### 2.29 UI卡顿优化

- 1.ANR是什么？导致原因有哪些？

- 2.谈谈你项目中避免ANR的一些经验。

> [1~2答案](https://www.jianshu.com/p/388166988cef)

针对各种ANR，常见解决方法：
1，主线程阻塞或主线程数据读取
解决办法：避免死锁的出现，使用子线程来处理耗时操作或阻塞任务。尽量避免在主线程query provider、不要滥用SharePreferenceS
2，CPU满负荷，I/O阻塞
解决办法：文件读写或数据库操作放在子线程异步操作。
3，内存不足
解决办法：AndroidManifest.xml文件<applicatiion>中可以设置 android:largeHeap="true"，以此增大App使用内存。不过不建议使用此法，从根本上防止内存泄漏，优化内存使用才是正道。
4，各大组件ANR
各大组件生命周期中也应避免耗时操作，注意BroadcastReciever的onRecieve()、后台Service和ContentProvider也不要执行太长时间的任务。