### fcntl函数

\#include <unistd.h>
\#include <fcntl.h> 
int fcntl(int fd, int cmd); 
int fcntl(int fd, int cmd, long arg); 
int fcntl(int fd, int cmd, struct flock *lock);



cmd值的F_GETFL和F_SETFL：
F_GETFL  取得**fd的文件状态标志**，如同下面的描述一样(arg被忽略)，在说明open函数时，已说明
了文件状态标志。不幸的是，三个存取方式标志 (**O_RDONLY , O_WRONLY , 以及O_RDWR**)并不各占1位。(这三种标志的值各是0 , 1和2，由于历史原因，这三种值互斥 — 一个文件只能有这三种值之一。) 因此首先必须用屏蔽字O_ACCMODE相与取得存取方式位，然后将结果与这三种值相比较。    
F_SETFL  设置给arg描述符状态标志，可以更改的几个标志是**：O_APPEND，O_NONBLOCK，O_SYNC 和 O_ASYNC**。而fcntl的文件状态标志总共有7个：**O_RDONLY , O_WRONLY , O_RDWR , O_APPEND , O_NONBLOCK , O_SYNC和O_ASYNC**

- 可更改的几个标志如下面的描述：
- O_NONBLOCK  非阻塞I/O，如果read(2)调用没有可读取的数据，或者如果write(2)操作将阻塞，则read或write调用将返回-1和EAGAIN错误
- O_APPEND   强制每次写(write)操作都添加在文件大的末尾，相当于open(2)的O_APPEND标志
- O_DIRECT   最小化或去掉reading和writing的缓存影响。系统将企图避免缓存你的读或写的数据。如果不能够避免缓存，那么它将最小化已经被缓存了的数据造成的影响。如果这个标志用的不够好，将大大的降低性能
- O_ASYNC   当I/O可用的时候，允许SIGIO信号发送到进程组，例如：当有数据可以读的时候