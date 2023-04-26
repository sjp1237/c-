## C++常见的错误

### 1.

> invalid use of incomplete type [struct](https://so.csdn.net/so/search?q=struct&spm=1001.2101.3001.7020)

编译器不知道所用的struct 或者是class的具体实现 如： class A, class B: B.cpp 用到了A类的对象或者某个具体成员，没有包含A类的头文件。

也可能 class A，class B在同一个头文件，但是class A先定义，class B还没有定义出来，



### 

### 2.Segmentation fault  段错误

段错误应该就是访问了不可访问的内存，这个内存区要么是不存在的，要么是受到系统保护的



#### 



### 踩过的坑

- 头文件最好不要互相包含
- vscode进行gdb调试是不会在return 上进行停留
- errno错误码等于14为访问到了错误的地址