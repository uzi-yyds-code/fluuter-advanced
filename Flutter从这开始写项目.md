# 目录

本人会针对Flutter从入门到相对熟练【具备开发水平】，专门讲述掌握Flutter的基本过程，每周会定期更新1-2篇博客！

*  我的高级交流群：1001906160，欢迎各位！

## 前言

通过过上篇博客大致了解Flutter项目的基本结构，以及Android Studio创建项目代码的讲述，大致了解了Flutter项目的基本结构！本篇博客将继续探寻Flutter在项目中的简单使用，通过两个例子

1.  Flutter是如何展示列表信息的？以及如何优化展示？【**讲述StatelessWidget的使用**】
2.  通过按钮实现自加的功能--【**讲述Statefulwidget的使用**】
3.  **Statefulwidget的生命周期讲述**

今天主要讲述上面的知识点就是想让大家掌握**StatelessWidget和StatefulWidget**的使用，希望大家可以跟着敲敲，通过一两个月的了解Flutter知识点，肯定可以具备开发水平的！**【动手写！动手写！动手写】**

如果有心从事**跨平台技术和原生技术**的**，欢迎大家点赞及关注，共同进步是目的！！！**

![image](https://upload-images.jianshu.io/upload_images/19704571-ce70ed217c1e11dc.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## StatelessWidget实现列表

### 2.1 问题及需求

有一个需求要求展示一个可滚动的静态列表,先来看一下案例的最终展示效果：

![image.png](https://upload-images.jianshu.io/upload_images/19704571-f620d74db5dcf3f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 2.2 分析

**2.2.1 自定义Widget**

案例中，很明显一个产品的展示就是一个大的Widget，这个Widget包含如下Widget：

*   标题的Widget：使用一个Text Widget完成； 

*   描述的Widget：使用一个Text Widget完成； 

*   图片的Widget：使用一个Image Widget完成； 上面三个Widget要垂直排列，可以使用一个Column的Widget，另外，三个展示的标题、描述、图片都是不一样的，所以让Parent Widget来决定内容

*   创建三个成员变量保存父Widget传入的数据

代码如下：

```
class ZXYHomeProductItem extends StatelessWidget {

  final String title;
  final String desc;
  final String imageURL;

  ZXYHomeProductItem(this.title, this.desc, this.imageURL);

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text(title, style: TextStyle(fontSize: 24)),
        Text(desc, style: TextStyle(fontSize: 18)),
        Image.network(imageURL)
      ],
    );
  }
}
复制代码
```

**2.2.2 列表数据展示**

现在可以创建三个ProductItem来让展示了

*   ZXYHomeContent中使用到了一个Column，因为创建的三个ZXYHomeProductItem是垂直排列的。

*   MyApp和[上篇博客](https://juejin.cn/post/6907199189935980552)内容差不多

代码如下

```
import 'package:flutter/material.dart';

main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ZXYHomePage(),
    );
  }
}

class ZXYHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("商品列表"),
      ),
      body: ZXYHomeContent(),
    );
  }
}

class ZXYHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("商品列表"),
      ),
      body: ZXYHomeContent(),
    );
  }
}
class ZXYHomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: <Widget>[
        ZXYHomeProductItem("Apple1", "Macbook Product1", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72j6nk1d4j30u00k0n0j.jpg"),
        ZXYHomeProductItem("Apple2", "Macbook Product2", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72imm9u5zj30u00k0adf.jpg"),
        ZXYHomeProductItem("Apple3", "Macbook Product3", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72imqlouhj30u00k00v0.jpg"),
      ],
    );
  }
}
复制代码
```

**2.2.3 运行代码界面展示**

![image.png](https://upload-images.jianshu.io/upload_images/19704571-e68769378db09b0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**2.2.4 问题分析**

*   **错误信息：下面出现了黄色的斑马线**
*   **在Flutter布局中，内容是不能超出屏幕范围的，当超出时不会自动变成滚动效果，就是报错误**

如何解决这种问题呢？

*   将Column换成ListView
*   ListView可以让自己的子Widget变成滚动的效果

代码如下：

```
class ZXYHomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        ZXYHomeProductItem("Apple1", "Macbook Product1", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72j6nk1d4j30u00k0n0j.jpg"),
        ZXYHomeProductItem("Apple1", "Macbook Product1", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72j6nk1d4j30u00k0n0j.jpg"),
        ZXYHomeProductItem("Apple1", "Macbook Product1", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72j6nk1d4j30u00k0n0j.jpg"),
      ],
    );
  }
}
复制代码
```

**2.2.5 改过之后界面效果**

![image.png](https://upload-images.jianshu.io/upload_images/19704571-a1c8f4079545fe2f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


上面效果是大致实现了，但是还是有比较多的细节需要调整，下面着手开始搞

### 2.3 案例细节调整

**2.3.1 界面整体边距**

如果希望整个内容距离屏幕的边缘有一定的距离，咋做呢？

*   需要另外一个Widget：Padding，有一个Padding属性用于设置边距大小、

    padding: EdgeInsets.all(12),

**2.3.2 商品内边距和边框**

如果希望给所有的商品也添加一个内边距，并且还有边框，咋做呢？

*   可以使用一个Container的Widget，里面有Padding属性，并且可以通过decoration来设置边框
*   Container后面会详细讲述【暂时先用起来】

**2.3.3 文字图片的间距**

如果希望给图片和文字之间添加一些间距，咋做呢？

*   方法一：给图片或者文字添加一个向上的内边距或者向下的内边距；
*   方法二：使用SizeBox的Widget，设置一个height属性，可以增加 一些距离；

### 2.4 最终代码【实现需求】

```
import 'package:flutter/material.dart';

main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HYHomePage(),
    );
  }
}

class HYHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("商品列表"),
      ),
      body: HYHomeContent(),
    );
  }
}

class HYHomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        HYHomeProductItem("Apple1", "Macbook1", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72j6nk1d4j30u00k0n0j.jpg"),
        SizedBox(height: 6,),
        HYHomeProductItem("Apple2", "Macbook2", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72imm9u5zj30u00k0adf.jpg"),
        SizedBox(height: 6,),
        HYHomeProductItem("Apple3", "Macbook2", "https://tva1.sinaimg.cn/large/006y8mN6gy1g72imqlouhj30u00k00v0.jpg"),
      ],
    );
  }
}

class HYHomeProductItem extends StatelessWidget {
  final String title;
  final String desc;
  final String imageURL;

  final style1 = TextStyle(fontSize: 25, color: Colors.orange);
  final style2 = TextStyle(fontSize: 20, color: Colors.green);

  HYHomeProductItem(this.title, this.desc, this.imageURL);

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(12),
      decoration: BoxDecoration(
          border: Border.all(
              width: 5, // 设置边框的宽度
              color: Colors.pink// 设置边框的颜色
          )
      ),
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        crossAxisAlignment: CrossAxisAlignment.end,
        children: <Widget>[
          Row(
            mainAxisAlignment: MainAxisAlignment.start,
            children: <Widget>[
              Text(title, style: style1),
            ],
          ),
          SizedBox(height: 8),
          Text(desc, style: style2),
          SizedBox(height: 8),
          Image.network(imageURL)
        ],
      ),
    );
  }
}
复制代码
```

## Statefulwidget实现按钮自加

### 3.1 问题及需求

有一个需求要求展示一个

*   +按钮点击数字自加1；

*   -按钮点击数字自减1；

先来看一下案例的最终展示效果：

![image.png](https://upload-images.jianshu.io/upload_images/19704571-1be48f3a98fcc33b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 3.2 认识StatefulWidget

在开发中，某些Widget情况下展示的数据并不是一层不变的：

*   比如Flutter默认程序中计数器案例，点击了+号按钮后，显示的数字需要+1； 

*   比如在开发中，会进行下拉刷新、上拉加载更多，这时数据也会发生变化； 

而StatelessWidget通常用来展示哪些数据固定不变的，如果数据会发生改变，使用StatefulWidget；

**3.2.1 StatefulWidget介绍**

如果阅读过创建[Flutter示例程序](https://juejin.cn/post/6907199189935980552)，那么会发现创建的是一个StatefulWidget程序。

为什么选择StatefulWidget呢？

*   因为在示例代码中，当点击按钮时，界面上显示的数据会发生改变； 

*   这时，需要一个变量来记录当前的状态，再把这个变量显示到某个Text Widget上； 

*   并且每次变量发生改变时，对应的Text上显示的内容也要发生改变；

但是有一个问题，之前说过定义到Widget中的数据都是不可变的，必须定义为final，为什么呢？

*   这次因为Flutter在设计的时候就决定了一旦Widget中展示的数据发生变化，就重新构建整个Widget； 

*   下一个章节会讲解Flutter的渲染原理，Flutter通过一些机制来限定定义到Widget中的成员变量必须是final的；

**Flutter如何做到在开发中定义到Widget中的数据一定是final的呢？**

看一下Widget的源码

```
@immutable
abstract class Widget extends DiagnosticableTree {
 // ...省略代码
}
复制代码
```

这里有一个很关键的东西@immutable，实际上官方有对[@immutable](https://api.flutter.dev/flutter/meta/immutable-constant.html)进行说明：**被@immutable注解标明的类或者子类都必须是不可变的**

```
结论： 定义到Widget中的数据一定是不可变的，需要使用final来修饰
复制代码
```

**3.2.2 如何存储Widget状态？**

既然Widget是不可变，那么StatefulWidget如何来存储可变的状态呢？

*   StatelessWidget无所谓，因为它里面的数据通常是直接定义完后就不修改的。 

*   但StatefulWidget需要有状态【可以理解成变量】的改变，这如何做到呢？

Flutter将StatefulWidget设计成了两个类，也就是你创建StatefulWidget时必须创建两个类： 

*   **一个类继承自StatefulWidget，作为Widget树的一部分；**

*   **一个类继承自State，用于记录StatefulWidget会变化的状态，并且根据状态的变化，构建出新的Widget；**

创建一个StatefulWidget，通常会按照如下格式来做：

*   当Flutter在构建Widget Tree时，会获取State的实例，并且它调用build方法去获取StatefulWidget希望构建的Widget； 

*   那么就可以将需要保存的状态保存在MyState中，因为它是可变的；

代码如下：

```
class ZXYStatefulWidget extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    // 将创建的State返回
    return ZXYState();
  }
}
复制代码
```

思考： 为什么Flutter要这样设计呢？

```
这是因为在Flutter中，只要数据改变了Widget就需要重新构建（rebuild）
复制代码
```

### 3.3 分析

**3.3.1 案例效果和分析**

案例效果及布局如下：

*   Column小部件：之前已经用过，当有垂直方向布局时，就使用它； 

*   Row小部件：之前也用过，当时水平方向布局时，使用它； 

*   RaiseButton小部件：可以创建一个按钮，并且其中有一个onPress属性是传入一个回调函数，当按钮点击时被回调

**3.3.2 创建StatefulWidget**

因为当点击按钮时，数字会发生变化，所以需要使用一个StatefulWidget，所以需要创建两个类； 

*   ZXYHomeContent继承自StatefulWidget，里面需要实现createState方法； 

*   _ZXYHomeContentState继承自State，里面实现build方法，并且可以定义一些成员变量；

代码如下：

```
//Widget是不加 _ :暴露给别人使用，加_自己使用
// State是加_: 状态这个类只是给Widget使用
class ZXYHomeContent extends StatefulWidget {
  final String message;
  ZXYHomeContent(this.message);

  @override
  State<StatefulWidget> createState() {
    return _ZXYHomeContentState();
  }
}

/**
 * 为什么Flutter在设计的时候StatefulWidget的build方法放在State中
 *  1.build出来的Widget是需要依赖State中的变量(状态/数据)
 *  2.在Flutter的运行过程中:
 *    Widget是不断的销毁和创建的
 *    当我们自己的状态发生改变时, 并不希望重新状态一个新的State
 */
class _ZXYHomeContentState extends State<ZXYHomeContent> {
  int _counter = 0;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          Text("当前计数$_counter", style: TextStyle(fontSize: 25),),
          Text("传递的信息:${widget.message}")
        ],
      ),
    );
  }
}
复制代码
```

**3.3.3 按钮布局及按钮监听状态**

```
Widget _getButtons() {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        RaisedButton(
          child: Text("+", style: TextStyle(fontSize: 20, color: Colors.white),),
          color: Colors.pink,
          onPressed: () {
            setState(() {
              _counter++;
            });
          },
        ),
        RaisedButton(
            child: Text("-", style: TextStyle(fontSize: 20, color: Colors.white),),
            color: Colors.purple,
            onPressed: () {
              setState(() {
                _counter--;
              });
            }
        ),
      ],
    );
  }
复制代码
```

### 3.4 最终代码【实现需求】

```
import 'package:flutter/material.dart';

main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ZXYHomePage(),
    );
  }
}

class ZXYHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("计数器项目"),
      ),
      body: ZXYHomeContent("你好呀，菜逼张程序员"),
    );
  }
}

//Widget是不加 _ :暴露给别人使用，加_自己使用
// State是加_: 状态这个类只是给Widget使用
class ZXYHomeContent extends StatefulWidget {
  final String message;
  ZXYHomeContent(this.message);

  @override
  State<StatefulWidget> createState() {
    return _ZXYHomeContentState();
  }
}

/**
 * 为什么Flutter在设计的时候StatefulWidget的build方法放在State中
 *  1.build出来的Widget是需要依赖State中的变量(状态/数据)
 *  2.在Flutter的运行过程中:
 *    Widget是不断的销毁和创建的
 *    当我们自己的状态发生改变时, 并不希望重新状态一个新的State
 */
class _ZXYHomeContentState extends State<ZXYHomeContent> {
  int _counter = 0;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          _getButtons(),
          Text("当前计数$_counter", style: TextStyle(fontSize: 25),),
          Text("传递的信息:${widget.message}")
        ],
      ),
    );
  }

  Widget _getButtons() {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        RaisedButton(
          child: Text("+", style: TextStyle(fontSize: 20, color: Colors.white),),
          color: Colors.pink,
          onPressed: () {
            setState(() {
              _counter++;
            });
          },
        ),
        RaisedButton(
            child: Text("-", style: TextStyle(fontSize: 20, color: Colors.white),),
            color: Colors.purple,
            onPressed: () {
              setState(() {
                _counter--;
              });
            }
        ),
      ],
    );
  }
}
复制代码
```

通过上面两个小案例，大致熟悉了**StatelessWidget** 和 **StatefulWidget**的内容，也基本可以实现小的列表功能展示以及状态更改的需求，希望大家可以手动敲写一般，写！写！写！！！

既然讲述到了**StatelessWidget和****StatefulWidget**内容，下面讲述一下StatefulWidget的生命周期。

## StatefulWidget生命周期

### 4.1 Flutter生命周期理解

什么是生命周期呢？

*   客户端开发：iOS开发中需要知道UIViewController从创建到销毁的整个过程，Android开发中需要知道Activity从创建到销毁的整个过程。以便在不同的生命周期方法中完成不同的操作； 

*   前端开发中：Vue、React开发中组件也都有自己的生命周期，在不同的生命周期中可以做不同的操作；

**Flutter小部件的生命周期：**

*   StatelessWidget可以由父Widget直接传入值，调用build方法来构建，整个过程非常简单； 

*   而StatefulWidget需要通过State来管理其数据，并且还要监控状态的改变决定是否重新build整个Widget； 

所以，我们主要讨论StatefulWidget的生命周期，也就是它从创建到销毁的整个过程。

### 4.2 StatefulWidget生命周期

道StatefulWidget本身由两个类组成的：`StatefulWidget`和`State`，分开进行分析

**首先，执行StatefulWidget中相关的方法：**

1.  执行StatefulWidget的构造函数（Constructor）来创建出StatefulWidget； 

2.  执行StatefulWidget的createState方法，来创建一个维护StatefulWidget的State对象； 

**其次，调用createState创建State对象时，执行State类的相关方法：**

1.  执行State类的构造方法（Constructor）来创建State对象； 

2.  执行initState，我们通常会在这个方法中执行一些数据初始化的操作，或者也可能会发送网络请求；【这个方法是重写父类的方法，必须调用super，因为父类中会进行一些其他操作】

3.  执行didChangeDependencies方法，这个方法在两种情况下会调用【情况一：调用initState会调用；情况二：从其他对象中依赖一些数据发生改变时】

4.  Flutter执行build方法，来看一下当前的Widget需要渲染哪些Widget；

5.  当前的Widget不再使用时，会调用dispose进行销毁；

6.  手动调用setState方法，会根据最新的状态（数据）来重新调用build方法，构建对应的Widgets；

7.  执行didUpdateWidget方法是在当父Widget触发重建（rebuild）时，系统会调用didUpdateWidget方法；

### 4.3 代码验证及打印

来通过代码进行演示

```
import 'package:flutter/material.dart';

main(List<String> args) {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text("Flutter生命周期"),
        ),
        body: ZXYHomeBody(),
      ),
    );
  }
}

class ZXYHomeBody extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    print("HomeBody build");
    return ZXYCounterWidget();
  }
}

class ZXYCounterWidget extends StatefulWidget {

  ZXYCounterWidget() {
    print("执行了ZXYCounterWidget的构造方法");
  }

  @override
  State<StatefulWidget> createState() {
    print("执行了ZXYCounterWidget的createState方法");
    // 将创建的State返回
    return ZXYCounterState();
  }
}

class ZXYCounterState extends State<ZXYCounterWidget> {
  int counter = 0;

  ZXYCounterState() {
    print("执行ZXYCounterState的构造方法");
  }

  @override
  void initState() {
    super.initState();
    print("执行ZXYCounterState的init方法");
  }

  @override
  void didChangeDependencies() {
    // TODO: implement didChangeDependencies
    super.didChangeDependencies();
    print("执行ZXYCounterState的didChangeDependencies方法");
  }

  @override
  Widget build(BuildContext context) {
    print("执行执行ZXYCounterState的build方法");
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              RaisedButton(
                color: Colors.redAccent,
                child: Text("+1", style: TextStyle(fontSize: 18, color: Colors.white),),
                onPressed: () {
                  setState(() {
                    counter++;
                  });
                },
              ),
              RaisedButton(
                color: Colors.orangeAccent,
                child: Text("-1", style: TextStyle(fontSize: 18, color: Colors.white),),
                onPressed: () {
                  setState(() {
                    counter--;
                  });
                },
              )
            ],
          ),
          Text("当前计数：$counter", style: TextStyle(fontSize: 30),)
        ],
      ),
    );
  }

  @override
  void didUpdateWidget(ZXYCounterWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    print("执行ZXYCounterState的didUpdateWidget方法");
  }

  @override
  void dispose() {
    super.dispose();
    print("执行ZXYCounterState的dispose方法");
  }
}
复制代码
```

打印结果如下【下图是第一次运行此项目的打印】

![image](https://upload-images.jianshu.io/upload_images/19704571-500ea14c6555d333.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当我们改变状态，手动执行setState方法后会打印如下结果：

![image](https://upload-images.jianshu.io/upload_images/19704571-020210ffc25b10b4.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**注意点**

当我们再次跑起程序时，查看打印

![image](https://upload-images.jianshu.io/upload_images/19704571-51f2f8f92fce43fb.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**【注意：Flutter会build所有的组件两次（查了GitHub、Stack Overflow，目前没查到原因）大神请赐教--个人感觉是编辑器Bug】**

## 总结

今天这篇文章，详细介绍了Flutter是如何展示列表信息的，从而带领大家来熟悉StatelessWidget的使用；以及通过按钮实现自加的功能来讲述Statefulwidget在项目中的使用；从而引出了一个知识点Statefulwidget的生命周期。

通过上面的三点，大家可以写出简单的列表展示以及交互，大家可以手动的编写上面的Demo例子！ 相信通过上面的例子以及进阶，可以加深大家对Flutter项目的认知和感触【动手写！动手写！动手写！！！】


[收录文章地址](https://juejin.cn/post/6909752239553216525)
