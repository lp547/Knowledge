# Qt概述	

##  什么是Qt

Qt是一个**跨平台**的C++**图形用户界面应用程序框架**。完全面向对象的，很容易扩展，并且允许真正的组件编程

## Qt的发展史

- 1991年 Qt最早由芬兰奇趣科技开发
- 1996年 进入商业领域，它也是目前流行的Linux桌面环境KDE的基础
- 2008年 奇趣科技被诺基亚公司收购，Qt称为诺基亚旗下的编程基础
- 2012年 Qt又被Digia公司（芬兰一家软件公司）收购
- 2014年4月 跨平台的集成开发环境Qt Creator3.1.0发布，同年5月20日配发了Qt5.3正式版，至此Qt实现了对iOS、Android、WP等各平台的全面支持。

## Qt的优势

-  跨平台，几乎支持所有的平台
- 接口简单，容易上手，学习QT框架对学习其他框架有参考意义。
- 一定程度上简化了内存回收机制 
- 开发效率高，能够快速的构建应用程序。。

## 成功案例

l Linux桌面环境KDE（K Desktop Environment）

l WPS Office 办公软件

l Skype 网络电话

l Google Earth 谷歌地球

l VLC多媒体播放器

l VirtualBox虚拟机软件

# 创建Qt项目

## 使用向导创建

1. 打开Qt Creator 界面选择 New Project或者选择菜单栏 【文件】-【新建文件或项目】菜单项
2. 弹出New Project对话框，选择Qt Widgets Application， 
3. 选择【Choose】按钮，弹出如下对话框
4. 设置项目名称和路径，按照向导进行下一步，
5. 选择编译套件
6. 向导会默认添加一个继承自QMainWindow的类，可以在此修改类的名字和基类。默认的基类有QMainWindow、QWidget以及QDialog三个，我们可以选择QWidget（类似于空窗口），这里我们可以先创建一个不带UI的界面，继续下一步
7. 系统会默认给我们添加main.cpp、mywidget.cpp、 mywidget.h和一个.pro项目文件，点击完成，即可创建出一个Qt桌面程序。

## 一个最简单的Qt应用程序

### main函数中

```c++
#include "widget.h"//Qt一个类对应一个头文件，类名和头文件名一致
#include <QApplication>//Qt系统提供的类头文件没有.h后缀

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);//QApplication应用程序类
    Widget w;
    w.show();

    return a.exec();
}
```

 **QApplication应用程序类**

1. 管理图形用户界面应用程序的控制流和主要设置。
2. 是Qt生命，一个程序要确保一直运行，就肯定至少得有一个循环，**这就是**Qt**主消息循环**，在其中完成来自窗口系统和其它资源的**所有事件消息处理和调度**。它也处理**应用程序的初始化和结束**，并且**提供对话管理**。
3. 对于任何一个使用Qt的图形用户界面应用程序，都正好存在一个QApplication 对象，不论这个应用程序在同一时刻有多少个窗口。

**a.exec()**

- **程序进入消息循环**，等待对用户输入进行响应。这里main()把控制权转交给Qt，Qt完成事件处理工作，当应用程序退出的时候exec()的值就会返回。**在exec()中，Qt接受并处理用户和系统的事件并且把它们传递给适当的窗口部件**。

### 类头文件

```c++
#include <QWidget>

class MyWidget : public QWidget
{
    //引入Qt信号和槽机制的一个宏
    Q_OBJECT

public:
//构造函数中parent是指父窗口
//如果parent是0，那么窗口就是一个顶层的窗口
    MyWidget (QWidget *parent = 0);
    ~ MyWidget ();
};
```

### .pro文件

.pro就是工程文件(project)，它是qmake自动生成的用于生产makefile的配置文件。类似于VS中的.sln 和vsproj文件

```c++
#以下是.pro文件的一个案例：
#引入Qt的模块，core gui//注释  从“#”开始，到这一行结束。

QT    += core gui//模块引入
    /*
    QT += 模块名，表示当前项目引入Qt哪些模块。
引入模块的意思就简单理解为引入C/C++头文件搜索路径，如果没引入对应模块就使用该头文件的话会报错说找不到该头文件。不必要的模块别引入，包括引入连接的库等一系列操作，会让程序变臃肿。
Qt详细模块有哪些可以参照附录。
    */

\#如果qt版本大于4，那么引入widgets模块

greaterThan(QT_MAJOR_VERSION, 4): QT += widgets

\#生成最终文件的文件名，可执行文件exe

TARGET = 01_MyWidget

\#项目类型，生成什么类型的文件，可执行程序还是库文件

TEMPLATE = app
//模板变量告诉qmake为这个应用程序生成哪种makefile。下面是可供使用的选择：TEMPLATE = app

\#要编译的源文件列表

SOURCES += \

​    main.cpp \

​    mywidget.cpp

\#要编译的头文件列表

HEADERS += \

​    mywidget.h
```

.pro文件的规则：

模板变量告诉qmake为这个应用程序生成哪种makefile。下面是可供使用的选择：**TEMPLATE** = app

>  app -建立一个应用程序的makefile。这是默认值，所以如果模板没有被指定，这个将被使用。
>
>  lib - 建立一个库的makefile。
>
>  vcapp - 建立一个应用程序的VisualStudio项目文件。
>
>  vclib - 建立一个库的VisualStudio项目文件。
>
>  subdirs -这是一个特殊的模板，它可以创建一个能够进入特定目录并且为一个项目文件生成makefile并且为它调用make的makefile。

- 指定生成的应用程序名： 

​	**TARGET** = QtDemo

-  工程中包含的头文件


​	**HEADERS** += include/painter.h

-  工程中包含的.ui设计文件


​	**FORMS** += forms/painter.ui

-  工程中包含的源文件


​	**SOURCES** += sources/main.cpp sources

-  工程中包含的资源文件


​	**RESOURCES** += qrc/painter.qrc

- **greaterThan(QT_MAJOR_VERSION, 4): QT += widgets**

​	**这条语句的含义是，如果QT_MAJOR_VERSION**大于4（也就是当前使用的Qt5及更高版本）需要增加widgets模块。如果项目仅需支持Qt5，也可以直接添加“QT += widgets”一句。不过为了保持代码兼容，最好还是按照QtCreator生成的语句编写。

- 配置信息


​	CONFIG用来告诉qmake关于应用程序的配置信息。

​	CONFIG += c++11 //使用c++11的特性（qt5.6以上版本默认使用C++11）

​	在这里使用“+=”，是因为我们添加我们的配置选项到任何一个已经存在中。这样做比使用“=”那样替换已经指定的所有选项更安全。

## 命名规范

Qt类名：单词首字母大写，单词和单词之间直接连接，无需连接字符 。

```
		MyClass，QPushButton
		class MainWindow
```

Qt中内置的类型，头文件和类命名同名。

```
		#include <QString>
		QSring str;
		#include <QWidget>
        QWidget w;
```

函数名字，变量名：首字母小写，之后单词首字母大写，无需连接字符

```
		void connectTheSignal();
```

类的成员变量设置函数用使用 set+成员变量名，获取成员变量的函数直接用成员变量名：

```
		//普通成员变量设置和获取
        void setText(QString text);
		QString text()const;
		//bool的成员变量设置和获取
		void setEnabled(bool enabled);
		bool isEnabled()const;Creator常用快捷键
```

##  **QtCreator常用快捷键**

运行  ctrl +R

编译  ctrl +B

帮助文档  F1 ，点击F1两次跳到帮助界面

跳到符号定义 F2 或者ctrl + 鼠标点击

注释 ctrl+/

字体缩放  ctrl + 鼠标滚轮

整行移动代码 ctrl + shift + ↑或↓

自动对齐  ctrl + i

同名之间的.h和.cpp文件跳转 F4

# 第一个Qt小程序

## 按钮的创建和父子关系

在Qt程序中，最常用的控件之一就是按钮了，首先我们来看下如何创建一个按钮

```c++
按钮上显示的文字#include <QPushButton>
QPushButton * btn = new QPushButton; //一个按钮就是一个QPushButton类的对象
  //设置父亲
  btn->setParent(this);//否则无法显示到窗口中的
  btn->setText("德玛西亚");//按钮上显示的文字
  btn->move(100,100);//移动位置
  //第二种创建
  QPushButton * btn2 = new QPushButton("孙悟空",this);
  //重新指定窗口大小
  this->resize(600,400);
  //设置窗口标题
  this->setWindowTitle("第一个项目");
  //限制窗口大小
  this->setFixedSize(600,400);
```

利用setParent函数或者按钮创建的时候通过构造函数传参，此时我们称两个窗口建立了**父子关系**。**在有父窗口的情况下，窗口调用show会显示在父窗口中，如果没有父窗口，那么窗口调用show显示的会是一个顶层的窗口（顶层窗口是能够在任务栏中找到的，不依赖于任何一个窗口而独立存在）**（按钮也是继承于QWidget，也属于窗口）。

对于窗口而言，我们可以修改左上角窗口的标题setWindowTitle，重新指定窗口大小：resize，或者设置固定的窗口大小setFixedSize；

## Qt窗口坐标体系

以左上角为原点（0,0），以向右为x轴正方向，以向下为y轴正方向。 

对于嵌套窗口，其坐标是**相对于父窗口**来说的。顶层窗口的父窗口就是屏幕。

## 对象树模型

**QObject**是Qt里边绝大部分类的**根类**

- QObject对象之间是以**对象树**的形式组织起来的。

> 当两个QObject（或子类）的对象建立了**父子关系**的时候。子对象就会加入到父对象的一个**成员变量**叫**children**（孩子）的list（**列表**）中。
>
> 当**父对象析构的时候**，这个列表中的**所有对象也会被析构**。

- **QWidget**是能够在屏幕上显示的**一切组件的父类**

> - **QWidget继承自QObject，因此也继承了这种对象树关系。一个孩子自动地成为父组件的一个子组件**。我们向某个窗口中添加了一个按钮或者其他控件（建立父子关系），当用户关闭这个窗口的时候，该窗口就会被析构，之前添加到他上边的按钮和其他控件也会被一同析构
> - 当然，**我们也可以手动删除子对象。当子对象析构的时候会发出一个信号destroyed，父对象收到这个信号之后就会从children列表中将它剔除。**自动调整屏幕显示，按钮在屏幕上消失

- 对象树中对象的顺序是未定义的，即销毁对象的顺序也是未定义的。
- 任何对象树中的 QObject对象 delete 的时候，如果这个对象有 parent，则自动将其从 parent 的children()列表中删除；如果有孩子，则自动 delete 每一个孩子。Qt 保证没有QObject会被 delete 两次，这是由析构顺序决定的。

如果QObject在栈上创建，Qt 保持同样的行为（正常）

```c++
{
  QWidget window;
  QPushButton quit("Quit", &window);
}
```

​	作为父组件的 window 和作为子组件的 quit 都是QObject的子类（事实上，它们都是QWidget的子类，而QWidget是QObject的子类）。这段代码是正确的，quit 的析构函数不会被调用两次，因为标准 C++要求，**局部对象的析构顺序应该按照其创建顺序的相反过程**。因此，这段代码在超出作用域时，会先调用 quit 的析构函数，将其从父对象 window 的子对象列表中删除，然后才会再调用 window 的析构函数。

但是：

```c++
{
  QPushButton quit("Quit");
  QWidget window;
  quit.setParent(&window);//情况又有所不同，析构顺序就有了问题
}
```

代码中，父对象的 window 首先被析构，因为它是最后一个创建的对象。在析构过程中，它会调用子对象列表中每一个对象的析构函数，也就是说， quit 此时就被析构了。然后，代码继续执行，在 window 析构之后，quit 也会被析构，因为 quit 也是一个局部变量，在超出作用域的时候当然也需要析构。但是，这时候已经是第二次调用 quit 的析构函数了，C++ 不允许调用两次析构函数，因此，程序崩溃了。

> **在 Qt 中，尽量在构造的时候就指定 parent 对象，并且大胆在堆上创建****

# 信号和槽机制

| **信号：各种事件**          |
| --------------------------- |
| **槽**： **响应信号的动作** |

当某个事件发生后，如某个按钮被点击了一下，它就会发出一个被点击的信号（signal）。

某个对象接收到这个信号之后，就会做一些相关的处理动作（称为槽slot）。

但是Qt对象不会无故收到某个信号，要想让一个对象收到另一个对象发出的信号，这时候需要建立连接（connect）

系统自带的信号和槽
自定义信号和槽
自定义信号使用条件
自定义槽函数使用条件
使用自定义信号和槽
信号和槽的拓展
Qt4版本的信号槽写法
Lambda表达式
局部变量引入方式
函数参数
选项Opt
函数返回值 ->retType
是函数主体{}
槽函数使用Lambda表达式
QMainWindow
菜单栏
工具栏
状态栏
停靠部件（也称为铆接部件、浮动窗口）
核心部件（中心部件）
使用UI文件创建窗口
UI设计窗口介绍
菜单栏
工具栏
状态栏
停靠部件
核心部件
UI文件原理
UI文件下使用信号和槽
转到槽
信号槽编辑器
资源文件
对话框QDialog
基本概念
标准对话框
自定义消息框
模态对话框
非模态对话框
消息对话框
标准文件对话框
布局管理器
系统提供的布局控件
利用widget做布局
常用控件
QLabel控件使用
显示文字 （普通文本、html）
显示图片
显示动画
QLineEdit
设置/获取内容
设置显示模式
其他控件
自定义控件
Qt消息机制和事件
事件
消息事件机制和信号槽机制的关系
event（）
事件过滤器
总结
绘图和绘图设备
QPainter
绘图设备
QPixmap、QBitmap、QImage
QPicture
文件操作
基本文件操作
二进制文件读写
文本文件读写
附录
附录1：Qt模块图