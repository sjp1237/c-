### QWidget

QWidget 类是所有窗口类的父类 (控件类是也属于窗口类), **并且 QWidget 类的父类的 QObject**, 也就意味着所有的窗口类对象只要指定了父对象, 都可以实现内存资源的自动回收。



### 构造函数

```c++
// 构造函数
QWidget::QWidget(QWidget *parent = nullptr, Qt::WindowFlags f = Qt::WindowFlags());

//设置父对象
void QWidget::setParent(QWidget *parent);
void QWidget::setParent(QWidget *parent, Qt::WindowFlags f);
// 获取当前窗口的父对象, 没有父对象返回 nullptr
QWidget *QWidget::parentWidget() const;
```



### 窗口位置

```c++
// 得到相对于当前窗口父窗口的几何信息, 边框也被计算在内
QRect QWidget::frameGeometry() const;
// 得到相对于当前窗口父窗口的几何信息, 不包括边框
const QRect &geometry() const;
// 设置当前窗口的几何信息(位置和尺寸信息), 不包括边框
void setGeometry(int x, int y, int w, int h);
void setGeometry(const QRect &);

// 移动窗口, 重新设置窗口的位置
void move(int x, int y);
void move(const QPoint &);


```

示例：

点击按钮，移动窗口，获取窗口

```c++
void Widget::on_pushButton_clicked()
{
    move(10,10);
}

void Widget::on_pushButton_2_clicked()
{
    QRect rect=this->frameGeometry();
    qDebug()<<"左上角: "<<rect.topLeft()
    <<"右上角: "<<rect.topRight()
    <<"左下角: "<<rect.bottomLeft()
    <<"右下角: "<<rect.bottomLeft()
    <<"宽度:"<<rect.width()
    <<"高度: "<<rect.height();
}

void Widget::on_pushButton_3_clicked()
{
    int x=rand()%500;
    int y=rand()%500;
    int wid=width()+10;
    int higth=height()+10;
    setGeometry(x,y,wid,higth);
}
```

