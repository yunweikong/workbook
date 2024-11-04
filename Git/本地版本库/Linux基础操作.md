在现今的软件开发中，`Linux`系统及其命令行的使用，已经是一项必不可少的技能。虽然有其他基于`Git`的图形化软件，但是`Git`只能通过命令行进行操作。因此，掌握一些基础的`Linux`操作命令很有必要。

###### 创建某个目录

有时我们需要创建目录，这时就需要使用命令`mkdir`。通过`mkdir`，可以在指定的目录下创建文件夹，其用法如下：

-   在当前目录下，创建目录`helloGit`: 　　`mkdir helloGit`
-   在`/home`目录下，创建目录`helloGit`： 　　`mkdir /home/helloGit`

`mkdir`的其他高级用法请参考其他`Linux`资料。

###### 创建文件

创建文件可以使用命令`touch`，其用法如下:

-   在当前目录下，创建文件`helloGit.txt`： 　　　`touch helloGit.txt`
-   在`/home`目录下，创建文件`helloGit.txt`： 　　　`touch /home/helloGit.txt`

###### 进入目录

进入某个目录，需要用到命令`cd`，其用法如下：

-   进入`helloGit`目录： 　　　`cd helloGit`

这样的用法默认了`helloGit`目录，存在于当前目录下。也可以在`cd`命令中，直接指定进入当前目录： 　　　 `cd ./helloGit`

-   进入`/home/helloGit`目录： 　　　`cd /home/helloGit`
    
-   返回到上一级目录： 在`Linux`系统下，上一级目录可以用‘..’代替，如：
    
    1.  `#进入上一级目录`
    2.  `cd ..`
    3.  `#进入上一级目录的再上一级目录`
    4.  `cd ../../`
    5.  `#进入上一级目录下的helloGit`
    6.  `cd ../helloGit`

`grep -r（递归地） "..." ./document`在某个目录下递归地收缩


##### 使用Git前的准备

###### 安装

`Git`可以使用源码安装，具体的安装过程请参考`Git`官网教程或者`Github`上`Git`仓库的[用户指南](https://github.com/git/git)。 但对于初学用户，还是建议大家直接安装。

-   `Linux`下安装：
    
    1.  `#Fedora下安装`
    2.  `yum install git-core`
    3.  `#Ubuntu等Debian类体系结构系统下`
    4.  `apt-get install git`
    
-   `Mac`上安装： 　　 在 `Mac` 上安装 `Git` 有两种方式。可以使用图形化的 `Git` 安装工具，网址为[图形化`Git`工具安装地址](http://sourceforge.net/projects/git-osx-installer/)；另一种是通过[`MacPorts`](http://www.macports.org/) 安装。如果已经装好了 `MacPorts`，请用下面的命令安装 `Git`： `sudo port install git-core +svn +doc +bash_completion +gitweb`
    
-   `Windows`下安装： 　　在 `Windows` 上安装 `Git`，可以使用`msysGit` 的项目提供的安装包，可以到 `GitHub` 的页面上，下载 `exe` 安装文件并运行： 　　`http://msysgit.github.com/` 完成安装之后，就可以使用命令行的 `git` 工具了。建议大家最好使用`Unix`风格的`shell`来运行`Git`。另外，`Linux`也有其他图形化的`Git`工具，如`Tortoisegit`。不过，还是建议大家直接使用`shell`来运行`Git`。
    

###### Git配置

由于`Git`是一个分布式的版本控制系统，所以当利用它进行分工协作时，必须区分不同的机器。这一点可以通过配置机器的名字和邮箱完成。`Git`初始使用时，也会提示进行配置。配置命令如下：

1.  `$ git config --global user.name "Your Name"`
2.  `$ git config --global user.email "email@example.com"`

在实际的使用过程中，可以将`“Your Name”`、`“email@example”`替换为自己实际的名字和邮箱。

###### 如何创建一个本地版本库

首先，我们需要创建一个目录，做为我们的本地版本库，然后使用`git init`命令，将其初始化为一个本地版本库，如下：

1.  `#在/home目录下，创建repo目录`
2.  `mkdir /home/repo`

4.  `#进入repo目录`
5.  `cd /home/repo`

7.  `#将repo初始化为一个本地版本库`
8.  `git init`

通过上述命令，即可在`/home`目录下，创建`repo`目录，并将其初始化为一个版本库。