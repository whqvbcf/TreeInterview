### 2.22 通知

- 1.Android 8.0如何适配通知？

> [点击查看答案](https://blog.csdn.net/guolin_blog/article/details/79854070)

- 2.自定义通知流程？

> [点击查看答案](https://www.cnblogs.com/dongweiq/p/5407815.html)  
> 回答这道问题的关键就是如何自定义布局，以及如何给通知里的控件设置点击机制,详情请看链接。


### 2.23 对话框(Dialog & DialogFragment & PopWindow)

- 1.说说Android中对话框可以用哪些方式完成？

> 标题括号中已有答案。


### 2.24 蓝牙

- 1.说说最新的蓝牙版本？新版本的特性是什么？

> [点击查看答案](https://www.cnblogs.com/michaelzero/p/6796689.html)

BLE通信三步：
第一步：我们要判断手机是否支持BLE，并且获得各种权限，才能让我们之后的程序能正常运行。 
然后，我们去搜索BLE设备，得到它的MAC地址。 
第二步：我们通过这个MAC地址去连接，连接成功后，去遍历得到Characteristic的uuid。 
在我们需要发送数据的时候，通过这个uuid找到Characteristic，去设置其值，最后通过writeCharacteristic(characteristic)方法发送数据。 
如果我们想知道手机与BLE设备的距离，则可以通过readRemoteRssi()去得到rssi值，通过这个信号强度，就可以换算得到距离。 
第三步：连接上后，我们就可以用BluetoothGatt的各种方法进行数据的读取等操作