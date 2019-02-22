### bl-api-cloud，轻云服务端

&emsp;

为轻量级可扩展的API服务端框架，主要用于响应http请求，开发者可通过开发自己的功能插件（.dll）进行加载以达到扩展。
&emsp;

**本程序主要面向EL（易语言）开发者，其他编程语言开发者可无视，主流语言一般都有各种类似的框架供使用。**
&emsp;

#  一、用途

为其他程序、应用，提供便捷的http接口搭建功能，开发者从而不再需要使用大型、复杂框架。

（毕竟很多时候为了一个小接口不值得用主流语言的比如java的Spring或python的Flask去搭建服务端）
&emsp;

> 举个最简单的例子，有时在授权、防破解等应用中，我们需要获取准确的北京时间。一般我们为了方便会通过第三方来获取：
>
> 1. 找个提供北京时间的第三方web页面；
> 2. 写个模块或DLL，提取页面里的北京时间；
>
> &emsp;
>
> **弊端：**
>
> 如果第三方页面出现问题，或web页面源码有变动，那么获取就会失败，进而影响了所有使用了此模块/DLL的程序。
> &emsp;
>
> 其实，很简单，我们让自己的服务器自动同步了时间，然后提供一个http接口即可，用自己的最稳定。
>
> ```c++
> 网页_访问 (“http://192.168.1.1:6680/api/sup/bjtime/10”)
> ```

&emsp;

#### 我自己使用本框架已应用的领域：

- 如取北京时间等实用接口；
- 搭建自己的网络验证系统（用户注册、登录、程序使用授权）；
- 搭建微信公众号后台程序（没错，完全没问题）；
- web页面搭建，只要有能力，你可以搭建出任意页面；（当然搭建企业级或大型复杂些的建议使用主流语言的主流框架，毕竟使用这个费劲死了，需要自己建设的方面太多）
- **详见最下方贴图案例效果。**

&emsp;




# 二、特色

&emsp;

#### 1、通讯组件使用的为HPsocket，强大、稳定

​	HP-Socket 是一套通用的高性能 TCP/UDP/HTTP 通信框架，包含服务端组件、客户端组件和Agent组件，广泛适用于各种不同应用场景的 TCP/UDP/HTTP 通信系统。

​	其Server 组件：基于IOCP / EPOLL通信模型，并结合缓存池、私有堆等技术实现高效内存管理，支持超大规模、高并发通信场景。

​	应用程序能够根据不同的容量要求、通信规模和资源状况等现实场景调整 HP-Socket 的各项性能参数（如：工作线程的数量、缓存池的大小、发送模式和接收模式等），优化资源配置，在满足应用需求的同时不必过度浪费资源。

​	[码云](https://www.oschina.net/p/hp-socket/doc)   

​	[Github](https://github.com/ldcsaa/HP-Socket)

&emsp;

#### 2、双服务端支持（http、https）

​	服务端启动端口自定义，默认http服务端`80`端口，https服务端`443`。当然本框架出发定性小众领域使用，可以设置其他端口，以免占用重要的web框架接口。

![](http://images.burnlord.com/app/BAC/start.png)

&emsp;

&emsp;

#### 3、扩展便捷

​	扩展（插件）为DLL文件，只需放入根目录下的`/plugins`即可。

​	DLL支持热加载与释放，无需终止服务端主程序即可进行DLL更新。

​	开发模板简单，一目了然，因为全部开源，开发者依然可以自主向插件传递更多可操作的主程序指针（通常模板自带功能足够使用了）。

&emsp;

​	**每个插件都有自己的http访问请求处理域且可以是多个，插件之间不会互相冲突；**

​	在两个示例demo中，对于`/api/sup/bjtime`根址的http请求，服务端只push到了bjtime.dll插件，对于`/web`的http请求，服务端只push到了web-demo.dll插件。

&emsp;

 **提供有2个扩展开发模板demo：**

&emsp;

#### （1）bjtime

示例如何返回Get请求，功能性代码不足20行即可实现；

![](http://images.burnlord.com/app/BAC/bjtime.png)

&emsp;

####  （2）web-demo

示例web页面返回，提供Get静态web目录文件回执和向服务端Post数据处理示例；

&emsp;

**1、访问页面（http与https）**

![](http://images.burnlord.com/app/BAC/web.png)

&emsp;
![](http://images.burnlord.com/app/BAC/web_https.png)

&emsp;
**2、post数据**



![](http://images.burnlord.com/app/BAC/post.png)

&emsp;

![](http://images.burnlord.com/app/BAC/web_post.png)

&emsp;

#### 4、集成实用便捷功能

​	自带集成多色日志输出、debug消息模式、访问频率保护等功能；

&emsp;

#### （1）多色日志输出

​	主程序的日志消息窗口，可以对应不同的日志显示不同的颜色，方便开发者一目了然的找到查看消息。

​	如：

​	灰色（gray）的为debug消息；

​	红色（red）的为异常或错误信息；

​	绿色（green）的为收到的事件；

​	黄色（yellow）为重要系统消息；

​	当然可以自己设置其他颜色，以及如何输出。



​	**注意：** 多色输出使用的是超级编辑框组件，在高并发下是否对程序效率影响有待考证（组件可能拖累程序），请自行进行取舍、替换。

&emsp;

#### （2）日志记录

​	主程序集成一个简单日志记录模块，主程序运行每一次运行后都会在`/log`目录创建一个日志文件（名称以`运行开始时间-运行结束时间.txt`为名，方便开发者查找时段消息）。

​	开发者也可以在自己开发的插件中加入独立的日志记录。

![](http://images.burnlord.com/app/BAC/log2.png)

&emsp;

#### （3）debug消息模式

​	主程序启动后通过输入`sys debug on`、`sys debug off`可开关debug模式，在debug模式下，会输出显示更多的日志消息（修改主程序文件可以自己定义显示什么内容为debug类型的消息），以便于程序调试。

&emsp;

#### （4）访问频率保护

​	主程序自带了一个频率保护功能，可以自行设置频率。如对于同一IP的访问限制在最近n秒内不可以超过i次。此功能用的自己简单设计的一个Belt模型，小众使用足够，高度使用下，开发者可根据实际需求决定是否自己去设计类似功能。

&emsp;

#### 5、心跳包异常监测

​	为了应对服务端布局在云服务器上异常退出的情形，用户可以通过发送Get心跳包的请求来确认服务端运行状态，发生异常可重启它。本框架目录下有个示例demo。

​	用户可以自己设置心跳包地址，默认`/api/this/heart`，

![](http://images.burnlord.com/app/BAC/liveCheck.png)

&emsp;

#### 6、web服务端

​	可以用于构建简单web页面，与web页面交互，理论上只要你精通web前端及后端处理逻辑，可以搭建（不过有这能力肯定不是用易语言搭建了）。

​	示例开发demo（plug-demo-web.e）提供了一个示例参考，可以搭建web页面，当然专业web设计等请移步使用主流语言的成熟框架。

​	参考上面图片。

&emsp;

#### 7、命令行式操作

​	最大化简化了服务端的UI界面（毕竟后端的东西），提供命令行式命令输入操作，除了系统前缀的命令，其他可推送到每个插件；

​	开发者可以在自己的插件里获取主程序输入的命令，然后进行相关处理。

&emsp;

#### 8、开发难度低

​	完整开源，包含主程序在内上手难度极低，代码注释齐全，结构明晰；也可以作为网络应用、DLL插件类型热加载释放等学习参考项目。

![](http://images.burnlord.com/app/BAC/develop2.png)



![](http://images.burnlord.com/app/BAC/develop.png)

&emsp;



# 三、使用协议

本框架遵从BSD开源协议

1. 可以任意使用本框架及代码进行二次开发，开发后产品可以闭源，开发源码主文件需要注释版权引用说明；
2. 不可以使用本框架作者信息进行推广、营销；
&emsp;


# 四、下载



**Github：**[https://github.com/Mruos/bl-api-cloud](https://github.com/Mruos/bl-api-cloud)，还请 **【star】、【watch】**

&emsp;

**baiduDisk：**[https://pan.baidu.com/s/1TBIpAHSv6sV2B7rO-fNEzg](https://pan.baidu.com/s/1TBIpAHSv6sV2B7rO-fNEzg)

&emsp;


# 五、案例贴图：
&emsp;
#### 1、微信公众号后台程序
![](http://images.burnlord.com/app/BAC/wechat-mp.png)

&emsp;

&emsp;

#### 2、网络验证系统，用户登录
![](http://images.burnlord.com/app/BAC/bluser.png)
&emsp;

&emsp;
&emsp;


# 六、其他

**by：** Mruos

**QQ/微信：** 812465371

**QQ群：** [465021903](https://jq.qq.com/?_wv=1027&k=5zYtwnT)

**web：** [www.burnlord.com](www.burnlord.com)
&emsp;

**使用问题、建议、Bug反馈，跟踪更新等欢迎加群交流~**
&emsp;

**本程序依然存在不足之处，欢迎各大佬批评、指出，一起完善。**

&emsp;

 # 七、支持一下，给个打赏~



![](http://images.burnlord.com//app/BAC收款码.png?imageslist)

