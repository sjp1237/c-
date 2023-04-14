# QT

## QT简介

1.1跨平台图形界面引擎

1.2优点

12.1接口简单，容易上手

1.2.2 一定程度上简化了内存回收



## 创建第一个qt项目

点击创建项目后，选择项目路径以及给项目起名称

- 项目名称中不能有空格和中文
- 创建的项目中不能有中文路径

默认创建有窗口类，QWidget，QMainWindow,QDialog

main函数

QApplication：应用程序对象，有且仅有一个



<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230331202305184.png" alt="image-20230331202305184" style="zoom:67%;" />

Widget基类,是一个空窗口

QMainWindow 包含菜单栏，工具栏等

QDialog是一个对话框

QDialog和QMainWindow继承QWidget



可以多创建一个窗口

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230331202653274.png" alt="image-20230331202653274" style="zoom:67%;" />1



```c++
#include<QApplication>//包含一个应用程序的类
在Qt中，应用程序对象，有且仅有一个
QApplication a(argc,argv);
```



```c
#include <QPushButton>  //调用按钮头文件
#include <QLineEdit>    //行编辑器

/*选择组合*/
QPushButton *bt;    //这里构造一个指针,按钮对象是 QPushButton
QLineEdit *le;      //行编辑器

Q_OBJECT 是一个宏，允许类中使用信号和槽的机制
命名规范
类名 首字母大写，单词和单词之间首字母大写
函数名 首字母小写，单词和单词之间小写
  快捷键：
   注释 ctrl+/
   运行 ctrl+r
   编译 ctrl+b
   查找 ctrl+f
   整行移动 ctrl+ shift +↑ 或者↓
   帮助文档 F1 第一次半屏慕 按两次全屏幕
   自动对齐 ctrl +i 自动对齐
   同名之间的.h 和.cpp 文件的来回切换 F4
    
```

## QT工程文件

```
.pro文件的解释
QT +=core gui // QT包含模块 gui图形模块
greaterThan(QT_NAJOR_VERSION,4):QT += vi dgets、//qt4版本，包含widget模块

TARGET =01_FirstProject //生成.exe文件的名称
TEHPLATE = app          //模板 应用程序模板	Applicaion
SOURCES += main. cppl  //源文件
   mywidget.cpp
HEADERS +=mgwidget.h  //头文件
```

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230331205724566.png" alt="image-20230331205724566" style="zoom:67%;" />1

- 



### QPushButton的创建

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230331212301130.png" alt="image-20230331212301130" style="zoom:67%;" />1



```c++
QPushButton* btn=new QPushButton;//创建一个按钮
btn->setParent(this);//将按钮设置进窗口里面
btn->setText("第一个按钮");//在按钮上面显示文本

//创建第二个按钮 按照控件的大小创建窗口
QPushButton* btn=new QPushButton("第二个按钮"，this);
//移动按钮
btn2->moe(100,100);//传入坐标
resize(600,400);//重置窗口大小

//设置窗口标题
setWindowTiles("第一个窗口标题");
//设置固定的窗口大小，防止拖拽
setFixedSize(600,400);
//重新设置按钮大小
btn2->resize(100,100);

```

## 对象树模型

![image-20230331214113542](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230331214113542.png)

当创建的对象在堆区的时候，如果指定的父亲是Object派生下来的类或者Qobect子类派生下来的类，可以不用管理释放操作，将对象放入到对象树中。





### 信号与槽

- 当信号被发射时,QT代码将回调与其相连接的槽函数
- 信号将由元对象处理moc自动翻译成C++代码
- 信号的声明不在cpp文件中,而在头文件中
- 槽函数是普通的C++成员函数,可以被正常调用
- 槽函数**可以有返回值,**也可以没有
- 槽函数的访问权限三种: **public slots、 private slots和 protected**
  **slots**。槽函数的存取权限决定了谁能够与其相关联
  - 信号槽的优点，松散耦合，信号接受端和发送端本身是没有关联的，通过connect给关联起来

```
connect(按钮指针，发送的信号(函数的地址）,信号的接收者，处理的槽函数);

```

![image-20230402200102768](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230402200102768.png)



排版类

//普通按钮
QPushButton *bt_test;
//工具栏按钮
QToolButton *bt_tool;
//单选按钮
QRadioButton *bt_radio1, *bt_radio2;
//复选按钮
QCheckBox *bt_check1, *bt_check2;(3) 输出部件
//标签（文字提示， 图片显示，动画显示。。。）
QLabel *lb_text;
QLabel *lb_pix;
QLabel *lb_gif;
//文本浏览器（解释html）
QTextBrowser *tb_test;
//日历
QCalendarWidget *cl_test;
//七段数码管
QLCDNumber *lcd_test;
//进度条
QProgressBar *pbr_test;

(4) 输入部件类
//行编辑框
QLineEdit *le_test;
QCheckBox *ck_test;
//组合框
QComboBox *cmb_test;
//字体选择下拉框
QFontComboBox *fcb_test;
//文本编辑框
QTextEdit *te_test;
//自旋框
QSpinBox *sp_test;
QLCDNumber *lcd_test;
//旋钮
QDial *dl_test;
//滚动条
QScrollBar *sbr_test;
//滑动杆儿
QSlider *sd_test;



# 三、主窗口

## 3.1、基础窗口部件( QWidget)

基础窗口部件主要用于自定义窗QWidge堤提供一个基础窗口**,窗口并没有任何图形部件**。通过**指定图形部件的父对象来把图形部件放上基础窗口**,或是通过自动布局工具把图形部件放上基础窗口。



**布局管理器主要常用的三个类: QHBoXLayout、 QVBoxLayout、 QGridLayout**

- QHBOXLayout:水平布局
- QVBoxLayout:垂直布局
- QGrid Layout:网格布





## QMainWindow

QMainWindow.是一个为用户提供主窗口程序的类，包含一个菜单栏(menu bar)、多个工具栏(tool bars)、多个锚接部低(dock widgets)、一个状态栏(status bar)及一个中心部件(central widget)，是许多应用程序的基础，如文本编辑器，图片编辑器等。

![image-20230402200334258](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230402200334258.png)



```；
//菜单栏最多只能有一个
//创建菜单栏
QMemuBar* bar=MenuBar();
//将菜单栏放入到窗口里面
setMenuBar(bar);
//给菜单栏创建菜单
Qmemu* fileMenu=bar->addMenu("文件")；
//创建菜单项
fileMenu->addAction("新建");
//在新建和打开之间添加分割线
fileMen9u->addSepartor();
fileMenu->addAction("打开");

//工具栏 可以有多个
QToolBar* toolBar=new QToolBar(this);
tool->addSepartor();//添加分割线
//设置到窗口上面
addToolBar(toolBar);//添加工具栏，默认在最上面
//addToolBar(默认区域,toolBar);

QPushButton* btn=new QpushButton("aa",this);
//在工具栏中添加按钮
toolBar->addWidget(btn);


//状态栏
QstatusBar* stBar=statusBar();

setStatusBar(stBar);
QLabel* label=new QLabel("提示信息",this);
//铆接部件(浮动窗口)
stBar->addWidget(label);
QDockWidget* dockWidget=new QDockWIdget("浮动"，this);
//将浮动窗口设置在最下面，前提是必须要有中心部件
addDockWidget(Qt::BottmDockWidgetArea,dockWidget);
//设置中心部件 只能一个
QTextEdit* edit=new QTextEdit(this);
setCentralWidget(edit);


```

## 资源文件的添加jian

将文件放在拷贝到项目下

右键项目->添加新文件->QT Resource File->给资源文件起名

res生成 res.qrc

open in editor 编辑资源

添加前缀，添加文件

使用

“：+ 前缀名+文件名”



### 模态对话款和非模态对话框

模态对话款（不可以对其他窗口进行操作）

```c
connect(ui->actionNew,&QAction::triggered,[=](){
    QDialog dlg(this);
    dlg.resize(200,100);
    //弹出模块对话框
    dlg.exec();//如果对话框不关闭，则会进行阻塞
    
    //dlg2需要创建在堆上面，因为函数结束后 栈上对象都会被释放掉，所以是不会弹出窗口
    QDialog* dlg2=new QDialog(this);
    dlg2->setAttribute(QT::WA_DeleteOnClose);//55号 属性 当窗口关掉的时候，释放对象
    dlg2->show();//弹出非模态对话框
})
```



### QT文件处理

Qt中**使用QFile进行文件操作**，为了**简化操作文本及二进制数据**问题，Qt还提供了QTIextStream用来操作文本流、提供了操作数据流的QDataStream，**使用QTemporaryFile来操作临时文件、使用QFileInfo来操作文件信息**。

QFilel从QFileDevice继承出来，**QFileDevice定义了文件错误类型**、文件打开时的读写权限等;QFileDevicel从QIODevice继承出来，QIODevice中定义了读写接口;QIODevice从QObject继承出来，则其支持信号槽。

