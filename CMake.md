Cmake

Cmake是一个跨平台的编译工具，可以用简单语句来描述所有平台的安装

Cmake可以说是已经成为大部分C++开源项目标配



<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230409105821422.png" alt="image-20230409105821422" style="zoom:67%;" />1

基本语法

指令（参数1 参数2）

参数是用分号或者空格分隔开

指令是大小写无关，参数和变量是大小写相关的

add_excutable(hello  main.cpp hello.cpp)

变量使用${},但是在IF控制语句中是直接使用变量名



## 重要指令和CMake常用变量

重要指令

cmake_minimum_required -指定CMake的最小版本

```cmake
cmake_minimum_required(VERSION 2.8.3)#指定CMake的最小版本要求为2.8.3
project(工程名[c][java])#定义工程名，并可指定工程支持的语言
project(main[c][java])#main，且支持的语言为c和java

set(SRC main.cpp hello.cpp)#显示定义变量，其值为main.cpp hello.cpp
include_directories()#向工程中添加多个特定的头文件搜索路径  -->相当于指定g++编译器中的-i选项
#将/usr/include/myincludefolder ./include添加到头文件的搜索路径中
include_directories(/usr/include/myincludefolder ./include)

link_directories() -#向工程中添加多个特定库文件的搜索路径  -->相当于指定g++编译器中的-L选项
link_directories(/usr/lib/mylibfolder ./lib) #将/usr/lib/mylibfolder ./lib添加到库文件的搜索路径中
add_library(库文件 SHARED|STATIC source)-#生成库文件

add_library(hello SHARED ${SRC})-#将SRC变量生成一个libhello.so的动态库
add_library(hello STATIC ${SRC})-#将SRC变量生成一个libhello.a的动态库

add_compile_option() -#添加编译参数
add_compile_option(-wall -std=c++11)#添加编译参数 -Wall -std=c++11
add_executable(main main.cpp) #编译main.cpp生成可执行文件main

target_link_libraries() #为target添加需要链接的共享库

target_link_libraries(main hello)#将hello动态库添加需要链接的共享库中

add_subdirectory(src) #向当前工程添加存放源文件的子目录，并可以指定中间二进制和目标二进制存放的位置。
arr_subdirectory(src) #添加src子目录，src中需有一个CMakeLists.txt

```



## CMake常用变量

- CMAKE_C_FLAGS gcc编译选项
- CMAKE_CXX_FLAGES g++编译选项

```cmake
	#在CMAKE_CXX_FLAGES 中选项后追加-std=c++11
	set(CMAKE_CXX_FLAGES ,"${CMAKE_CXX_FLAGES} -std=c++11")

```

CMAKE_BUILD_TYPE 编译类型（Debug,Release)

```cmake
#设定编译类型为debug
set(CMAKE_BUILD_TYPE  Debug);
```

CMAKE_C_COMPILER:指定C编译器

CMAKE_CXX_COMPILER：指定C++编译器





## CMAKE编译工程

CMake目录结构：项目主目录存在一个CMakeLists文件

两种方式设置编译规则：

- 包含源文件的子文件夹包含CMakeLists.txt文件，主目录的CMakeLists.txt通过add_subdirectory添加子目录即可
- 包含源文件的子文件夹未包含CMakeLists.txt文件，子目录编译规则体现在主目录的CMakeLists.txt中。

## 编译流程

在linux平台下使用CMake构建C/C++工程的流程如下：

1. 手动编写CmakeLists.txt
2. 执行cmake PATH 生成Makefile（PATH是顶层CMakeLists.txt所在的目录)
3. 执行命令make进行编译



### 两种构建方式

#### 内部构建：不推荐使用

内部构建会在同级目录下产生一堆中间件文件，这些中间文件并不是我们想要的，和工程文件放在一起会显得杂乱无章。

```shell
##内部构建
#在当前目录下，编译本目录CMakeLists.txt 生成Makefile和其他文件
cmake .
#执行make指令，生成target
make
```

#### 外部构建

将编译文件和源文件放到不同的目录下

```shell
#将编译输出文件与源文件放到不同的目录下
#在当前目录下，创建build文件夹
mkdir build
#进入到build文件夹中
cd build
#编译上级目录的CMakeLists.txt,生成Makefile和其他文件
cmake ..
#执行make命令，生成target
make
```



## 6.5【实战】CMake代码实战







### VsCode配置C++调试信息