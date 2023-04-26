## send

当程序执行send函数发送数据时，如果遇到关闭的[socket](https://so.csdn.net/so/search?q=socket&spm=1001.2101.3001.7020)，则系统底层会抛出一个SIGPIPE信号。这个信号的默认处理方式是退出当前进程。