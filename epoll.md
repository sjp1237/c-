 epoll

```c
#include <sys / epoll.h>
 
nfd = epoll_creat(max_size);
//max_size参数将被忽略，但必须大于零

```



```c
epoll_ctl 接口是用来 维护 epoll 对象中红黑树的节点，epoll_ctl可以在红黑树中添加，删除，修改节点。
   int epoll_ctl(int epfd, int op, int fd, struct epoll_event *event);

```

> **epfd：eppoll**对象的文件描述符
> op:选择修改epoll中红黑树的方式，如下：
>   EPOLL_CTL_ADD：往红黑树中插入节点
>   EPOLL_CTL_MOD：修改红黑树中的节点的信息。
>   EPOLL_CTL_DELL：删除红黑树中节点。
>
> 如果socket已经添加到epoll对象中，则不能再一次将socket添加到epoll对象，只能修改socket中的节点信息





events的常用取值如下：

- EPOLLIN：表示对应的文件描述符可以读（包括对端SOCKET正常关闭）。
- EPOLLOUT：表示对应的文件描述符可以写。
- EPOLLPRI：表示对应的文件描述符有紧急的数据可读（这里应该表示有带外数据到来）。
- EPOLLERR：表示对应的**文件描述符发生错误**。
- EPOLLHUP：表示**对应的文件描述符被挂断，即对端将文件描述符关闭**了。
- EPOLLET：将epoll的工作方式设置为边缘触发（Edge Triggered）模式。
- EPOLLONESHOT：只监听一次事件，当监听完这次事件之后，如果还需要继续监听该文件描述符的话，需要重新将该文件描述符添加到epoll模型中
-  EPOLLRDHUP ：表示对端连接断开触发的 epoll 事件会包含 EPOLLIN | EPOLLRDHUP，即 0x2001。有了这个事件，**对端断开连接的异常就可以在底层进行处理**了，不用再移交到上层（即通过recv的返回值进行判断）。



epoll_event

![img](https://img-blog.csdnimg.cn/2ae44bc55ab84a368a4fba05adbabb71.png)