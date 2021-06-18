本人会不断提供优质的内容博客给大家，内容目前涵盖Objective-C、Swift、Flutter、小程序的开发。**欢迎点赞博客及关注本人，共同进步~~~**

* 本人高级技术交流圈：1001906160，欢迎家人

## 背景与问题

1.  中小公司维护一个App的成本好高呀，有没有办法可以降低成本的可能性，但是又不想让代码缺少维护？

2.  有没有方案可以实现一份代码可以运行在多个平台，减少沟通成本呢？

## 问题方案选择

各公司都开始关注和使用跨端方案【包括大厂阿里巴巴以及腾讯】目前主流的跨端方案主要分为两种：一种是将JavaScriptCore引擎作为虚拟机的方案，代表框架是React Native；另一种是使用非JavaScriptCore虚拟机的方案，代表框架是Flutter。【其中还有一种是使用Webview的方案-待会也会讲解到】

使用跨端方案进行开发，必然会替代原有平台的开发技术，所以我们在选择跨端方案时，不能只依赖于某几项指标，比如编程语言、性能、技术架构等，来判断是否适合自己团队和产品，更多的还要考虑开发效率、社区支持、构建发布、 DevOps、 CI 支持等工程化方面的指标。

![image](https://upload-images.jianshu.io/upload_images/19704571-bd4f3d1c7d12712e.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

目前本公司其它项目采用的是Flutter和Swift混编，感觉下一步本负责项目也要进入这个模式，所以开启Flutter之旅。

希望通过本篇博客，大家能够理解为什么选择Flutter，以及几种跨平台的区别，**欢迎关注与点赞，彼此共同进步，谢谢！！！**

## 方案特点原理

![image](https://upload-images.jianshu.io/upload_images/19704571-cf838c4d5eef7b44.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 方案一：Webview

**Webview是基于JavaScript和WebView的跨平台。主要工作在Webkit中完成**

最早出现的跨平台框架是基于JavaScript和WebView，代表框架有PhoneGap，Apache Cordova，Ionic等。

WebView主要是通过HTML来构建自己的界面，再将其显示在各个平台的WebView中，但是它默认是不能调用本地的一些服务的【比如蓝牙、相机等】所以需要调用JavaScript进行桥接调用Native的一些代码来完成某些功能。但是根据本人亲自对WebView的使用，WebView的性能并不够理想，而且开发过程中的坑也比较多。

下图是WebView的原理图--**认真看下**

![image](https://upload-images.jianshu.io/upload_images/19704571-50f150fc63850296.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 方案二：React Native

React Native【简称RN】是Facebook于2015年4月开源的跨平台移动应用开发框架，，是Facebook早先开源的JS框架 React 在原生移动应用平台的衍生产物，目前支持iOS和安卓两大平台。

RN使用JavaScript语言类似于HTML的JSX，以及CSS来开发移动应用，并且在保留基本渲染能力的基础上，用原生自带的UI组件实现核心的渲染引擎，从而保证了良好的渲染性能。

但是，由于RN的本质是通过JavaScript VM调用原生接口，通信相对比较低效，而且是间接通过原生进行渲染的。

![image](https://upload-images.jianshu.io/upload_images/19704571-1cd4ee68e2aec674.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 方法三：Flutter

Flutter是谷歌的移动UI框架，可以快速在iOS和Android上构建高质量的原生用户界面。 Flutter可以与现有的代码一起工作。在全世界，Flutter正在被越来越多的开发者和组织使用，并且Flutter是完全免费、开源的。

总体来说，相比于React Native框架，Flutter的优势最主要体验在性能、开发效率和体验两大方面。

React Native所使用的JavaScriptCore，原本用在浏览器中，用于解释执行网页中的JavaScript代码。为了兼容Web标准留下来的历史包袱，无法专门针对移动端进行性能优化。Flutter却不一样，它一开始就抛弃了历史包袱，使用全新的Dart语言编写，同时支持AOT和JIT两种编译方式，而没有采用HTML/CSS/JavaScript组合方式开发，在执行效率上明显高于JavaScriptCore。

除了编程语言的虚拟机，Flutter的优势还体现于**UI框架的实现**上。它重写了UI框架，从UI控件到渲染，全部重写实现了，依赖Skia图形库和系统图形绘制相关的接口，保证了不同平台上能有相同的体验。

**Flutter利用Skia绘图引擎，直接通过CPU、GPU进行绘制，不需要依赖任何原生的控件。【Andriod操作系统中，编写的原生控件中实际上也是依赖于Skia进行绘制，所以Flutter在某些Andriod操作系统上甚至还要高于原生-因为原生Andriod中的Skia必须随着操作系统进行更新，而Flutter SDK中总是保持最新的】**

### Flutter对比优势

下面用andriod平台来对比：Flutter、原生与RN等平台的对比，可以看出除了原生开发，Flutter的性能更高

![image](https://upload-images.jianshu.io/upload_images/19704571-58a1713ad705f504.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## Flutter剖析

### Flutter绘制原理图

![image](https://upload-images.jianshu.io/upload_images/19704571-a25dc7612c0a8c30.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

*   GPU将信号同步到UI线程
*   UI线程用Dart来构建图层树
*   图层树在GPU线程中合成
*   合成后的视图数据提供给SKia引擎
*   Skia引擎通过OpenGL或者Vulkan将显示内容提供给GPU，所以有两个GPU构成一个闭环

Flutter和React Native的本质区别：

*   React Native 只能通过JavaScript虚拟机扩展调用系统组件，由iOS 和 Andriod系统组件的渲染
*   Flutter是自己完成了组件渲染的闭环

### 帧率与刷新率

**1、基础知识**

帧率【fps】：Frame Per Second 

刷新率：显示器的频率，比如iPhone 的 60HZ等

**拓展：**

```
我们为什么能看到类似于动画的效果呢？
1、这是因为它播放的速度非常快，研究表明： p 当图片连续播放的频率超过16帧（16张图片），人眼就会感觉非常流畅，当少于16帧时，会感觉到卡顿
2、所以我们平时看到的电影，通常都是24帧或者30帧的（李安之前拍摄120帧的电影，目的就是让图片间隔更小，画面更加的流畅）
复制代码
```

**2、帧率与刷新率的关系**

![image](https://upload-images.jianshu.io/upload_images/19704571-a9cae32fbb2cfd92.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**CPU/GPU 向 Buffer 中生成图像，屏幕从 Buffer 中取图像、刷新后显示。**

这是一个典型的生产者---消费者模型。理想的情况下帧率和刷新率相等，每绘制一帧，屏幕显示一帧，但是实际情况下往往它们的大小是不同的。如果没有锁来控制同步，很容易出现问题。例如当帧率大于刷新频率，当屏幕还没有刷新第 n-1帧的时候，GPU 已经在生成第 n 帧了。从上往下开始覆盖第n - 1帧的数据，当屏幕开始刷新第n - 1帧的时候，Buffer中的数据上半部分是第n帧数据，下半部分是第n - 1 帧的数据。显示出来的图像就是上下部分出现明显偏差，称之为“撕裂”。

### 双重缓存【Double Buffer】

**1、基本概念**

为了解决单缓存的“撕裂”问题，就出现了双重缓存和Vsync。

两个缓存区分别为 Back Buffer 和 Frame Buffer。

GPU 向 Back Buffer 中写数据，屏幕从 Frame Buffer 中读数据。

VSync 信号负责调度从 Back Buffer 到 Frame Buffer 的复制操作。当然底层不是通过复制，而是通过交换内存地址方式，所以可以瞬间完成，效率是非常高的；

![image](https://upload-images.jianshu.io/upload_images/19704571-4458b32acb8638ec.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

工作流程：

*   **在某个时间点，一个屏幕刷新周期完成，VSync 信号产生，先完成复制操作，然后通知 CPU/GPU 绘制下一帧图像。**

*   **复制操作完成后屏幕开始下一个刷新周期，即将刚复制到 Frame Buffer 的数据显示到屏幕上。**

*   **在这种模型下，只有当 VSync 信号产生时，CPU/GPU 才会开始绘制。**

****2、存在的问题**
**

双重缓存的缺陷在于：当 CPU/GPU 绘制一帧的时间过长（比如超过16ms）时，会产生 Jank（画面停顿，甚至空白）。

蓝色代表 CPU 生成 Display List；

绿色代表 GPU 执行 Display List 中的命令从而生成帧；

黄色代表生成帧完成，在屏幕上显示；

![image](https://upload-images.jianshu.io/upload_images/19704571-05e43d8f3a7ae654.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

CPU生成蓝色B的数据，由GPU进行B的绘制，但是这个过长由于过长，那么第二个A就产生了Jank。

B在屏幕上显示之后，发出Vsync信号，A开始绘制，但是由于绘制时间过长，第二个B位置又产生了Jank

### 渲染引擎Skia

Skia（全称Skia Graphics Library（SGL））是一个由C++编写的开源图形库，**Skia就是 Flutter向 GPU提供数据的途径。**

Skia 已然是 Android 官方的图像渲染引擎了，因此 Flutter AndroidSDK 无需内嵌 Skia 引擎就可以获得天然的 Skia 支持； 而对于 iOS 平台来说，由于 Skia 是跨平台的，因此它作为 Flutter iOS 渲染引擎被嵌入到 Flutter 的 iOS SDK 中，替代了 iOS 闭源的 Core Graphics/Core Animation/Core Text，这也正是 Flutter iOS SDK 打包的 App 包体积比Android 要大一些的原因。 

底层渲染能力统一了，上层开发接口和功能体验也就随即统一了，开发者再也不用操心平台相关的渲染特性了。也就是说，Skia 保证了同一套代码调用在Android 和 iOS 平台上的渲染效果是完全一致的。

## 总结

从11月份开始进军Flutter领域，本人的博客也会由iOS 底层探寻 + Flutter初体验 + 小程序的研发为主，**欢迎大家关注及点赞**，共同在移动端提升自己的专业技能+才干，共勉！！！

 [收录于文章](https://juejin.cn/post/6902707237345558542)
