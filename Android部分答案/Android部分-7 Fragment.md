### 2.7 Fragment

- 1.Android中v4包下Fragment和app包下Fragment的区别是什么？

> [点击查看答案](https://www.cnblogs.com/as3lib/p/6129313.html)

- 2.Fragment的生命周期 & 请结合Activity的生命周期再一起说说。

> [点击查看答案](https://blog.csdn.net/clandellen/article/details/79269680)

- 3.说说Fragment如何进行懒加载。

> [点击查看答案](https://www.cnblogs.com/dasusu/p/6745032.html)

- 4.ViewPager + Fragment结合使用会出现内存泄漏吗 & 如何解决？

> **原因:**一般ViewPager + Fragment结合使用出现内存泄漏的原因可能用某个集合存储了Fragment的实例,导致当用户滑动ViewPager的时候，某一个Fragment即将面临销毁的时候，由于这个集合持有的它的引用，因此不能被回收掉,如果Fragment里面有大量的数据占据内存，有可能会导致OOM。  
> **解决方法**：尽量不要使用集合来存储Fragment实例对象，除非你有良好的二次封装。再就是要做好每一页Fragment的数据缓存问题。

- 5.Fragment如何和Activity进行通信 & Fragment之间如何进行通信？
- 6.给我谈谈Fragment3种切换的方式以及区别 & 使用场景。

> [5~6题答案](https://blog.csdn.net/clandellen/article/details/79269680)
add()&remove()
hide()&show()
detach()&attach()
  也许你会问不是还有replace()方法吗？其实replace()其实是先调用了remove()然后再调用add()方法，所以不算那三种其实之一。那么这三种方式有什么区别呢？
add()&remove():就是添加和移除，因此replace()这个方法只是在上一个Fragment不再需要时采用的简便方法。
hide()&show():则是指隐藏和显示，这种方式防止Fragment多次创建实例对象，所以正确的切换方式是add()，切换时hide()，add()另一个Fragment；再次切换时，只需hide()当前，show()另一个，这样就能做到多个Fragment切换不重新实例化。
detach()&attach():使用detach()会将view从ViewTree中删除,和remove()不同,此时Fragment的状态依然保持着,在使用attach()时会再次调用onCreateView()来重绘视图,注意使用detach()后Fragment.isAdded()方法将返回false,在使用attach()还原Fragment后isAdded()会依然返回false(需要再次确认)执行detach()和replace()后要还原视图的话, 可以在相应的Fragment中保持相应的view,并在onCreateView()方法中通过view的parent的removeView()方法将view和parent的关联删除后返回,这种方式极少使用

- 7.getFragmentManager,getSupportFragmentManager,getChildFragmentManager之间的区别？

> [点击查看答案](https://blog.csdn.net/Allan_Bst/article/details/64920076)

- 8.FragmentPagerAdapter和FragmentStatePagerAdapter区别？

> [点击查看答案](https://www.cnblogs.com/nbls/p/7252307.html)
FragmentPagerAdapter
FragmentPagerAdapter 继承自pagerAdapter 该类更专注于每一页均为Fragment 的情况，该类内的每一个生成的Fragment 都将保存在内存之中，因此适用于那些相对静止的页，数量也比较少的那种；如果需要处理有很多页，并且数据动态性比较大，占用内存比较多的情况下，应该使用FragmentStatePagerAdapter。

FragmentStatePagerAdapter
FragmentStatePagerAdapter 和之前的FragmentPagerAdapter 一样，是继承子PagerAdapter。但是 和FragmentPagerAdapter 不一样的是 该PagerAdapter 的实现将只保存当前页面，当页面离开视线后，就会被消除，释放其资源；而在页面需要显示时，生成新的页面。这么实现的好处就是当拥有大量的页面时，不必在内存中占用大量的内存。
