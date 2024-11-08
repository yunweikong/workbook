#### 克隆操作

克隆，顾名思义，就是要获取远程版本库的完整拷贝。通过克隆操作，你可以将整个远程版本库的各种细节复制到本地，并且会建立起本地版本库和远程版本库的对应关系。

克隆操作需要用到的命令是`git clone`，它的具体用法如下所示：

1.  `git clone https://sample.git`

通过这样的操作，就能将远程版本库复制到本地了，而且会默认克隆到`sample`文件夹下（对应于远程版本库地址中指定的`sample`）。同时，你也可以根据需要，指定克隆到其他目录下，其命令格式为：

1.  `git clone xxx.git "指定目录"`

这样就能将代码都复制到指定目录下。

#### 添加远程版本库
添加远程版本库需要用到的命令是`git remote add`，其命令格式为：

1.  `git remote add “远程仓库名” “远程仓库地址”`

使用示例如下：

1.  `git remote add origin https://sample.git`

这样就将`https://sample.git`添加为远程仓库，并将其命名为`origin`。

#### 推送本地内容
推送本地内容时，会将所有未推送至远程仓库的内容，都提到远程仓库。它用到的命令是`git push`，使用方法如下：

1.  `git push 远程仓库名 本地分支名 远程分支名`

具体的使用方法如下：

1.  `git push origin master master`

这样就将本地分支的内容，推送到远程仓库`origin`的`master`分支了。 `git push`的另外一种用法如下：

1.  `git push -u 远程仓库名 本地分支名 远程分支名`

`-u`参数的作用是，建立起本地`master`分支和远程`master`分支之间的对应关系，下一次如果再推送`master`分支，就可以忽略远程分支名了，如下所示：

1.  `#初次推送`
2.  `git push -u origin master master`
3.  `#再次推送`
4.  `git push origin master`


#### 拉取远程仓库的内容到本地
拉取远程仓库的内容到本地，需要使用`git pull`命令，其命令格式为：

1.  `git pull 远程主机名 远程分支名 本地分支名`

其使用示例如下：

1.  `#将远程仓库origin的master分支的内容拉取到本地master分支`
2.  `git pull origin master:master`

但是，在使用过程中，也可能会出现一种情况：远程分支和本地分支对同一内容做了修改，这就会导致将远程分支的修改，合并到本地分支的时候发生冲突。这个时候，可以选择解决冲突，然后合并（解决冲突会在后续的实训中介绍）。也可以选择直接强制拉取，使用远程分支的修改，覆盖本地分支的修改。强制拉取需要用到`-f`参数，语法格式如下：

1.  `git pull 远程主机名 远程分支名 本地分支名 -f`

具体的使用示例如下：

1.  `#将远程仓库origin的master分支的内容拉取到本地master分支`
2.  `git pull origin master:master -f`




#### Git服务器

在团队开发中，我们必须选用一台主机做为`Git`服务器来存放远程版本库。这样团队中的每个开发者，就可以基于一个共同的远程版本库进行开发。目前提供代码托管（即可以将远程版本库存放于其上的）的平台有`Github`、码云等，同时我们也可以搭建一台私有的运行`Git`的服务器，来做为远程`Git`服务器。`Github`等平台的使用，及本地`Git`服务器的搭建，会在后续的实训中具体介绍。本地`Git`服务器，可以配置不同的连接方式，如`shell`、`git`或`bash`。为了给挑战者提供一个便利的实训环境，我们为每个人配置了一台本地`Git`服务器，并允许以`bash`方式进行操作，即可以通过类似于`/home/sample.git`这种形式的地址，做为远程仓库地址进行操作，而不是像`https://sample.git`这种形式。