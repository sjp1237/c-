	Git基础



### 获取本地仓库

- 要使用Git对我们的代码进行版本控制，首先需要获得本地仓库
- 在电脑的任意位置创建一个空目录（例如test)作为我们的本地Git仓库2）进入这个目录中，点击右键打开Git bash窗口
- 执行命令git init
- 如果创建成功后可在文件夹下看到隐藏的.git目录。
- 除了.git目录，其他的目录都是工作目录（工作区）



## 基础指令

Git工作目录下对于文件的修改(增加、删除、更新)会存在几个状态，这些修改的状态会随着我们执行Git的命令而发生变化。

![image-20230411201529702](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230411201529702.png)



```shell
git status  #查看当前目录下所有文件的状态
git add 文件名 #提交到暂存区
git commit -m "注释" #提交到仓库里面

git log #查看提交记录
--all 显示所有的分支
--pretty=oneline将提交信息显示为一行
--abbrev-commit使得输出的commitld更简短--graph 以图的形式显示
--graph 以图的形式显示

·作用:版本切换或版本回退
·命令形式: git reset --hard commitlD
commitID可以使用it-1og 或git log指令查看·如何查看已经删除的记录?

git reflog
。这个指令可以看到已经删除的提交记录

```

![image-20230411203348561](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230411203348561.png)1



## 设置指令别名

如果指令太长了，那么可以在 ~/.bashrc文件中给指令设置一个别名

如下：

```shell
git log --pretty=oneline --all --graph --abbrev-commit
```

我们可以在~/.bashrc文件中写入

```shell
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
```

设置完毕，执行指令

```shell
source ~/.bashrc 
```

在执行 git-log指令相当于执行

```shell
git log --pretty=oneline --all --graph --abbrev-commit
```

### 取消部分文件管理

在同一目录下，如果不想其中一些文件被管理，那么可以创建一个.gitstatus文件

```shell
*.a #目录下所有的.a文件都不会被跟踪
```



## 分支

几乎所有的版本控制系统都以某种形式支持分支。使用分支意味着你可以把你的工作从开发主线上分离开来进行重大的Bug修改、开发新的功能，以免影响开发主线。



### 查看本地分支

```shell
git branch 	 	#查看所有的分支
git branch sjp  #
#创建一个sjp分支
git check sjp   #切换到sjp分支
git check -b 分支名 #创建并切换分支
```

#### 合并分支

**将一个分支的提交到另一个分支上面**

```shell
git merge dev01#将dev01上的所有修改都合并到当前分支上面来， 一般切换为主分支
```

### 删除分支

```shell
git branch -d 分支名 #删除分支需要检查
git branch -D 分支名 #不做任何检查，强制删除
```

Head指向谁，谁就是当前的分支

![](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230411212552516.png)1



### 解决冲突

当两个分支上**对文件的修改可能会存在冲突**，例如**同时修改了同一个文件的同一行**，这时就需要手动解决冲突，解决冲突步骤如下:
1.处理文件中冲突的地方
⒉.**将解决完冲突的文件加入暂存区(add)3.提交到仓库(commit)**

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230411214250618.png" alt="image-20230411214250618" style="zoom:80%;" />1



### 开发分支使用原则和流程

几乎所有的版本控制系统都以某种形式支持分支。使用分支意味着你可以把你的工作从开发主线上分离开来进行重大的Bug修改、开发新的功能，以免影响开发主线。
在开发中，一般有如下分支使用原则与流程:
. master(生产)分支
线上分支，主分支，中小规模项目作为线上运行的应用对应的分支;. develop(开发)分支
是从master创建的分支，一般作为开发部门的主要开发分支，如果没有其他并行开发不同期上线要求，都可以在此版本进行开发，阶段开发完成后，需要是合并到master分支,准备上线。
. feature/xxxx分支
从develop创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完成后合并到develop分支。
 hotfix/xxxx分支，
从master派生的分支，一般作为线上bug修复使用，修复完成后需要合并到master、test、develop分支。·还有一些其他分支，在此不再详述，例如test分支(用于代码测试)、 pre分支(预上线分支)等等。

![image-20230412101634095](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412101634095.png)



### 仓库托管

![image-20230412103843176](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412103843176.png)

命令如下:

1. clone(克隆):**从远程仓库中克隆代码到本地仓库**
2. checkout(检出) :从本地仓库中检出一个仓库分支然后进行修订
3. add（添加)︰在提交前先将代码提交到暂存区
4. commit(提交)︰提交到本地仓库。本地仓库中保存修改的各个历史版本
5. fetch (抓取)︰从远程库，抓取到本地仓库，不进行任何的合并动作，一般操作比较少。
6. pull (拉取)︰从远程库拉到本地库，自动进行合并(merge)，然后放到到工作区，相当于fetch+merge
7. push(推送):**修改完成后，需要和团队成员共享代码时，将代码推送到远程仓库**



> 前面我们已经知道了Git中存在两种类型的仓库，即本地仓库和远程仓库。那么我们如何搭建Git远程仓库呢?我们可以借助互联网上提供的一些代码托管服务来实现，其中比较常用的郁GitHub、码云、GitLab等。
> gitHub ( 地址: https: //github.com/ )是一个面向开源及私有软件项目的托管平台，因为只支持Git作为唯一的版本库格式进行托管，故名gitHub
> 码云（地址: https://gitee.com/ ）是国内的一个代码托管平台，由于服务器在国内，所以相比于GitHub，码云速度会更快
> GitLab(地址: https: / / about.gitlab.com/〉是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并在此基础上搭建起来的web服务，一般用于在企业、学校等内部网络搭建git私服。





### 关联远程仓库

![image-20230412105020401](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412105020401.png)



将本地仓库推送到远程仓库，需要验证用户信息

1.验证远程仓库的用户名和密码

2.配置公钥和私钥



### git出现Permission denied的解决办法

![image-20230412205051594](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412205051594.png)

对应的.git目录是没有权限在目录下创建文件的。

那么就需要考虑到目录权限的问题。（切换用户，或者设置目录的权限）



### 远程连接

**此操作是先初始化本地库，然后与已创建的远程库进行对接。**

命令: 

git remote add<远端名称><仓库路径>
。远端名称，默认是orgin，取决于远端服务器设置。仓库路径，从远端服务器获取此URL
。例如: git remote add origin git@gitee.com:czbk_zhang_meng/git_test.git



> git remote  查看远程仓库	
>
> git remote remove origin 删除远程仓库



查看本地仓库所关联的远程仓库

> [root@iZwz97d32td9ocseu9tkn4Z webserver]# git remote -v
> origin  git@github.com:sjp1237/webserver.git (fetch)
> origin  git@github.com:sjp1237/webserver.git (push)

### 推送到远程仓库

·命令: git push [-f] [--set-upstream][远端名称[本地分支名][:远端分支名]]

-f： 表示强制覆盖

。如果远程分支名和本地分支名称相同，则可以只写本地分支

- git push origin master
o-set-upstream推送到远端的同时并且建立起和远端分支的关联关系。
git push --set-upstream origin master:master 将本地master分支与远端的master分支对应
。如果当前分支已经和远端分支关联，则可以省略分支名和远端名。
- git push将master分支推送到已关联的远端分支。



### 删除远程仓库的文件

```shell
git rm --cached xxx
git commit -m "remove file from remote"
git push -u origin master
```

如何查看linux下的SSH-key

> 1.首先，你得在root目录下 cd /root



> 2.cd ~/.ssh #进入.ssh目录

![image-20230412161336806](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412161336806.png)



**进入id_rsa.pub文件**，并将id_rsa.pub文件中内容给复制下来，然后登录到github上，并将id_rsa.pub给设置到github上



****

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412161042245.png" alt="image-20230412161042245" style="zoom:80%;" />



<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412161118281.png" alt="image-20230412161118281" style="zoom:80%;" />





![img](https://img-blog.csdnimg.cn/2020060310174263.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1dfMzE3,size_16,color_FFFFFF,t_70)



git branch -vv 查看本地分支和远端分支的对应关系

> git push --set-upstream origin master
>





### 克隆远程仓库

如果想使用一个远端的仓库，那么可以直接将该仓库克隆到本地仓库与之关联起来。

git clone 远程仓库的地址 本地目录

本地目录可以省略，没有会自动生成一个目录



### 从远程仓库抓取和拉取

> 远程分支和本地的分支一样，我们可以进行merge操作，只是需要先把远端仓库里的更新都下载到本地，再进行操作。
> 抓取命令: git fetch [remote name] [branch name]
> **抓取指令就是将仓库里的更新都抓取到本地，不会进行合并**。如果不指定远端名称和分支名，则抓取所有分支。

- 拉取命令: git pull [remote name] [branch name]
- 拉取指令就是将远端仓库的修改拉到本地并自动进行合并，等同于fetch+merge。如果不指定远端名称和分支名，则抓取所有并更新当前分支。





### 解决合并冲突

在一段时间，A、B用户修改了同一个文件，且修改了同一行位置的代码，此时会发生合并冲突。
A用户在本地修改代码后优先推送到远程仓库，此时B用户在本地修订代码，提交到本地仓库后，也需要推送到远程仓库，此时B用户晚于A用户，**故需要先拉取远程仓库的提交，经过合并后才能推送到远端分支,**如下图所示。

![image-20230412164655509](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20230412164655509.png)