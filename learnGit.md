[教程地址-廖雪峰](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## 安装Git并配置
1. [官网下载](https://git-scm.com/downloads) 
2. 配置：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
注，`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## 创建版本库并添加文件
1. 选择一个合适的地方，创建一个空目录：
```
$ mkdir youefilename
$ cd youe
$ pwd
/Users/michael/learngit
```
`mkdir`用于创建新目录。
`cd`是进入指定目录。
`pwd`用于显示此目录，如果可以显示出`/Users/michael/learngit`则表示创建成功
2. 添加文件

* 版本控制系统只能追踪文本文件的改动，而图片视频等二进制文件，只能知道从100k编程120k，但具体改了啥，没法知道。注意，word就是二进制文件。
* 不要用记事本编辑文本文件。

新建一个文件，放到上述目录下，然后输入命令：
```
git add yourfile
git commit -m"add a new file yourfilename"
```
`git add`是添加文件到仓库。
`git commit`是提交文件到仓库，`-m`后面是对这次提交的说明。

## 查看历史版本并回退


## 工作区和暂存区
* 工作区（Working derictory)就是在电脑里可以看到的目录。
* 隐藏目录`.git`，不算工作区，是Git的版本库。
* 版本库里最重要的是称为stage或index的暂存区，还有自动创建的第一个分支`master`,以及指向它的指针`HEAD`。
* 前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
因此可以多次add,然后一次commit。
而且，必须每次提交修改都得先add,再commit。

