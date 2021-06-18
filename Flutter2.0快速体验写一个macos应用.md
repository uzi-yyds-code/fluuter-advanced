本人会不断提供优质的内容博客给大家，内容目前涵盖Objective-C、Swift、Flutter、小程序的开发。**欢迎点赞博客及关注本人，共同进步~~~**

* 本人高级技术交流圈：1001906160，欢迎家人

## 1.简介

Flutter2.0将桌面端的开发支持加入到了`stable`分支中，这对于我一个移动开发小码农，产生了巨大的兴趣（/手动狗头）,于是开始了我的第一个`macos`应用的开发(`FTools`)，简单的说：开发桌面应用真的不要太简单了吧！下面是应用的截图，多图警告

## 2.屏幕截图

*   明亮模式：

![image](https://upload-images.jianshu.io/upload_images/19704571-054b21458868f620.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/19704571-f9f27bdc149f9c28.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/19704571-09003da39ac5cda1.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/19704571-f1eb107c1608ecd5.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

*   深色模式：

![image](https://upload-images.jianshu.io/upload_images/19704571-e684c409539ee91c.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 ![image](https://upload-images.jianshu.io/upload_images/19704571-84e62a51f49fa702.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 ![image](https://upload-images.jianshu.io/upload_images/19704571-04c986debbcc79c9.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 ![image](https://upload-images.jianshu.io/upload_images/19704571-f601bca6e43063d8.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3.MacOS应用开发

看到上面，是不是也是像我一样，想自己也写一个macos的工具应用，不要着急，下面来教大家如何创建和生成MacOS应用

### 1.配置环境

首先，确保你的FlutterSDK为2.0，我使用的是beta分支，也可以在stable分支下面查看到相同的版本号，至于Flutter的环境搭建，网上已经有很多相关的文章了，这里就直接省略了 ![image.png](https://upload-images.jianshu.io/upload_images/19704571-d8728e7742fd35e4.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2.配置可开发MacOS应用

运行下面命令即可

```
flutter config --enable-macos-deaktop
复制代码
```

### 3.创建项目

我一般使用的是`Android Studio`，所以，按照步骤：

`Create New Flutter Project`

->选择 `Flutter Application` -> 点击 `Next`

->输入项目名`Project Name` -> 点击`Next`

->输入包名`Package Name` -> 点击`Finish`

-> 等待创建完毕（如果卡住了，可以试试设置代理，百度搜索：Flutter设置国内镜像）

-> 因为`Android Studio` 给我们创建的项目只能运行`Android`和`IOS`，我们需要再命令行下切换到项目的根目录下，运行`flutter create .`命令即可，完成后，可以看到macos文件夹

![image](https://upload-images.jianshu.io/upload_images/19704571-4bc030adc3d5a7c9.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4.运行项目

这里，我们需要给`Android Studio` 升级`Flutter`插件到最新的版本,然后选择macOS点击绿色三角按钮进行运行即可

![image](https://upload-images.jianshu.io/upload_images/19704571-3be13f39300212a4.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/19704571-4e2f4ea533bae6d6.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/19704571-1bb8e11451823819.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 4.FTools后续开发

这个应用目前只耗时了两天，后续还会继续维护并免费上架到AppStore，如果你想这个应用有哪些功能(用户面向于开发者)，欢迎评论区留言给我，在能够实现并且时间充足的话会安排在开发计划当中。目前计划安排!

1.  Json To Table （JSON 转表格）
2.  Json To Create SQLite (JSON 转Sqlite创建)
3.  App Icon Make (应用图标制作)
4.  ...欢迎留言



 [收录于文章](https://juejin.cn/post/6938390739990609956)
