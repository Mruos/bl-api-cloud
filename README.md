# bl-api-cloud，轻云服务端

bl-api-cloud，为轻量级可扩展的API服务端框架，主要用于响应http请求，开发者可通过开发自己的功能插件（.dll）进行加载以达到扩展，并且主程序可加载多个插件。
&emsp;

**本程序主要面向EL（易语言）开发者，主流语言一般都有各种方便的框架轮子供使用。**
&emsp;

##  用途

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

**我自己使用本框架已应用的领域：**

- 如取北京时间等实用接口；
- 搭建自己的网络验证系统（用户注册、登录、程序使用授权）；
- 搭建微信公众号后台程序（没错，完全没问题）；
- web页面搭建，只要有能力，你可以搭建出任意页面；（当然搭建企业级或大型复杂些的建议使用主流语言的主流框架，毕竟使用这个费劲死了，需要自己建设的方面太多）
&emsp;

**详见最下方贴图案例效果。**
&emsp;


## 特色

1. 通讯组件使用的为[HPsocket](https://www.oschina.net/p/hp-socket/doc)，强大、稳定；

2. 既支持http服务端，也支持带SSL的https服务端；

3. 扩展（插件）为DLL文件，支持热加载与释放，开发模板为一个DLL模板，简单；（提供2个模板参考）。且每个插件都有自己的http访问请求处理域且可以是多个，插件之间不会互相冲突；

4. 自带集成多色日志输出、debug消息模式、访问频率保护等功能；

5. 提供异常监测demo，通过心跳包监测服务端运行，异常重启，可安心布置在服务器上；

6. 可以用于构建简单web页面，与web页面交互；（但不适用专业web搭建）

7. 提供命令行式命令输入操作，且可推送到每个插件；

&emsp;

8. 完整开源，包含主程序在内上手难度极低，代码注释齐全，结构明晰；

9. 网络应用、DLL插件类型热加载释放等，完美学习demo；

&emsp;

**详见最下方贴图案例效果。**

&emsp;

## 使用协议

本框架遵从BSD开源协议

1. 可以任意使用本框架及代码进行二次开发，开发后产品可以闭源，开发源码主文件需要注释版权引用说明；
2. 不可以使用本框架作者信息进行推广、营销；
&emsp;


## 下载

**Github：**[https://github.com/Mruos/bl-api-cloud](https://github.com/Mruos/bl-api-cloud)，还请 **【star】、【watch】**

**baiduDisk：**[https://pan.baidu.com/s/1TBIpAHSv6sV2B7rO-fNEzg](https://pan.baidu.com/s/1TBIpAHSv6sV2B7rO-fNEzg)

&emsp;


## 案例贴图：
&emsp;

#### 一、主界面：

![](http://images.burnlord.com/app/BAC/start.png)

&emsp;

#### 2、自带的北京时间获取示例插件
![](http://images.burnlord.com/app/BAC/bjtime.png)

&emsp;
#### 3、自带的web页面示例插件

**（1）访问页面（http与https）**

![](http://images.burnlord.com/app/BAC/web.png)
&emsp;

&emsp;
![](http://images.burnlord.com/app/BAC/web_https.png)

&emsp;
**（2）post数据**

![](http://images.burnlord.com/app/BAC/post.png)

![](http://images.burnlord.com/app/BAC/web_post.png)
&emsp;

#### 4、微信公众号后台程序
![](http://images.burnlord.com/app/BAC/wechat-mp.png)
&emsp;

#### 5、网络验证系统，用户登录
![](http://images.burnlord.com/app/BAC/bluser.png)
&emsp;

#### 6、自带的运行监测
![](http://images.burnlord.com/app/BAC/liveCheck.png)
&emsp;

#### 7、极简单的DLL插件开发模板
![](http://images.burnlord.com/app/BAC/develop.png)

![](http://images.burnlord.com/app/BAC/develop2.png)
&emsp;


## 其他

**by：** Mruos

**QQ/微信：** 812465371

**QQ群：** [465021903](https://jq.qq.com/?_wv=1027&k=5zYtwnT)

**web：** [www.burnlord.com](www.burnlord.com)
&emsp;

**使用问题、建议、Bug反馈，跟踪更新等欢迎加群交流~**
&emsp;

**本程序依然存在不足之处，欢迎各大佬批评、指出，一起完善。**

&emsp;

 ## 支持一下，给个打赏~



![](http://images.burnlord.com//app/BAC收款码.png?imageslist)

