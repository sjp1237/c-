## Linux常用指令



##### 查看线程

ps elf





### linux之间怎么传文件

```shell
确认两台机子都有命令scp后，使用scp可以实现传递文件
命令格式
scp -P端口 用户名@ip地址:/远程机子目录/文件 /本地目录/文件

示例:
scp -P1234 root@192.168.1.10:/tmp/a.txt /tmp/.
```

