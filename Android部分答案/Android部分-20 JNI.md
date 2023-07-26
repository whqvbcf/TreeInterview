### 2.20 JNI

- 1.什么是JNI?它主要用来干什么。

> [点击查看答案](https://blog.csdn.net/carson_ho/article/details/73250163)

- 2.Java Native方法如何和Native函数进行绑定的？
- 3.JNI如何实现数据传递？

> [2~3题答案](https://www.cnblogs.com/DengGao/p/jni.html)

- 4.如何全局捕获Native发生的异常？

> [点击查看答案(仅供参考,等笔者研究研究)](https://blog.csdn.net/qq_22654613/article/details/87883403)

> [上面答案失效，new一个](https://www.cnblogs.com/heweiquan/p/10973201.html)
Native层Crash捕获机制
Native层代码的错误可以分为两种。
C++异常：
在Native层，如果使用C++语言进行开发，而且使用了C++异常机制，那么函数执行可以抛出std::exception类型的异常；如果使用C/C++语言开发，使用的错误码机制，那么对于一些导致系统不可用的错误码，我们也可以进行捕获上报。总的来说，C++异常通常是可捕获的，一般不会引起APP Crash，当然如果处理不当，会引起逻辑错误。
Fatal Signal异常：
在Native层，由于C/C++野指针或者内存读取越界等原因，导致APP整个Crash的错误。这种Crash一般会在Logcat中打印出包含Fatal signal字样的日志。对于这种Crash，前面介绍的Java异常捕获类Thread.UncaughtExceptionHandler是检测不到的。那么如何捕获这种异常并上报呢？
熟悉Linux底层的应该很容易看出种种Crash是基于Linux的信号处理机制。信号（又称为软中断信号，signal）本质上是一种软件层面的中断机制，用来通知进程发生了异步事件。进程之间可以相互通过系统调用kill来发送软中断信号；Linux内核也可以应为内部事件而给进程发送信号，通知进程某个事件的发生。需要注意的是，信号并不携带任何数据，它只是用啦i通知某进程发生了什么事件。接受到信号后，通常有三种处理方式。
（1）自定义处理信号：进程为需要处理的信号提供信号处理函数。
（2）忽略信号：进程忽略不感兴趣的信号（SIGKILL和SIGSTOP忽略不了）/
（3）使用系统的默认处理：使用内核的默认信号处理函数，默认情况下，系统对大部分信号的缺省操作是终止进程。
了解信号的基本只是后，那么问题就变得恨简单了，由于Native层Crash大部分都是signal软中断类型错误，一次只要捕获signal并进行处理，得到中断的具体信息就很好帮助定位了。这一步可以通过sigaction注册信号处理函数来完成。

获取Native Crash的相关堆栈信息，然后上报给服务器。但是Native层并没有提供像Java层那样的Throwable.printStackTrace函数来获取堆栈信息，目前来说有两种思路。
1，抓取Logcat日志：前面说过，Native层发生fatal signal导致APP崩溃，也会在Logcat中打印出相关的堆栈信息，因此，当在Native层检测到fatal signal，利用我们的信号处理函数my_handler可以向Java层发送信息，通知它去抓取Logcat的日志，抓取的方式上面已经介绍过，需要注意的一点是，这时候由于Crash应用原有的进程将会很快被结束掉，因此Logcat的抓取应该开启新的进程，例如启动一个新进程在Service中进行操作。
2，Google Breakpad：这是一个跨平台的奔溃转储和分析工具，支持windows、linux、osx、android等，通过继承它提供的函数库，在应用发生奔溃时会将相关堆栈信息写入一个minidump格式文件中，通过将这个文件上传到服务器，开发人员可以通过addr2line等工具将dump文件中的函数地址转换成对应的代码行数，从而知道问题发生的具体位置。

- 5.只有C/C++能编写Native库吗？

> 这道题目实际上难度还是有点大的。答案首先回答当然不是只有C/C++能编写Nativie库，还可以用GoLang，
> Rust,Kotlin Native,Scala Native进行编写。