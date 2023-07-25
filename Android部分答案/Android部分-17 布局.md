### 2.17 布局

- 1.说说Android中有哪些布局 & 特点。

> [点击查看答案](https://blog.csdn.net/ClAndEllen/article/details/82979812)
1.LinearLayout：线性布局
特点：排列方式只有水平排列和垂直排列两种，orientation 设置为 horizontal 为水平排列， 设置为 verital 为垂直排列
2.RelativeLayout：相对布局
特点： RelativeLayout 中子 View 的排列方式是基于彼此的依赖关系
3.FrameLayout：帧布局
特点：布局简单，所有的子 View 都放在布局左上角，写在下面的 View 会覆盖 写在上面的 View
4.TableLayout：表格布局
特点：TableLayout继承自Linearout，本质上仍然是线性布局管理器，不需要明确地声明包含多少行、多少列；每向TableLayout中添加一个TableRow就代表一行；每向TableRow中添加一个一个子组件就表示一列
5.AbsoluteLayout ：绝对布局
特点：Android不提供任何布局控制，而是由开发人员自己通过X坐标、Y坐标来控制组件的位置。每个组件都可指定如下两个XML属性：layour_x;layout_y;

- 2.你知道布局文件到控件对象的过程吗？

> 答案也在题1答案链接中

- 3.有这么一个布局需求，一个文本控件放在屏幕一半的一半的中间位置，你如何进行布局？

> 这里实际是在筛选你是否具备Android布局相关知识点,答案有多种，可以利用线性布局和相对布局的特性即可。

- 4.LinearLayout,FrameLayout,RelativeLayout性能对比，为什么？

> [点击查看答案](http://www.cnblogs.com/chenlong-50954265/p/5942182.html)