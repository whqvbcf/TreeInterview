### 2.26 悬浮窗

- 1.在做悬浮窗的时候你遇到了什么困难(主要指悬浮窗权限适配)？

> 悬浮窗权限的适配是个难题，但好在有一个第三方库可以使用:
> [悬浮权限适配库](https://github.com/czy1121/settingscompat)

- 2.如何制作一个悬浮窗？

> [点击查看答案](https://www.jianshu.com/p/ac63c57d2555)

一点简单的设计思路：
1，一个MainActivity作为App的窗口，APP在打开时启动MainAcitivity，MainActivity在确定权限等操作后转到Service并关闭自己。
2，一个Service作为Windowmanager的载体。在Service中我们进行悬浮窗的初始设置并开启它。
4，WindowManager，配套一个XML文件，里面是悬浮窗的布局和里面的各种组件，本Demo中就放一个小小的ImageButton。