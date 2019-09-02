# <center>Git</center>
## 简介
Linux（没错，就是现在LINUX的开源作者），因为大神对SVN和CVS很不满意，所以自己写了一个版本管理工具。

讲到版本管理工具，就不得不提到两种模式：集中式和分布式。

集中式就是正本放在某台中央服务器上，开发人员要打代码的时候就去下载。

分布式则没有所谓的中央服务器，每个人电脑上的都是一个完整的版本库，那问题来了？A和B两人都对文件C进行了修改时怎么办呢？他们只需将各自的修改推送给对方即可，不过一般也会有一个“中央服务器”来作为中转站（例如Github仓库）

## Git安装
1. 官网下载https://git-scm.com/downloads
2. 配置本地Git身份
```
git config --global user.name "Your Name"           #配置用户名
git config --global user.email "email@example.com"  #配置邮箱
```

## 版本库结构&Git工作原理
### （版本库repository）结构
1. 工作区 working directory
2. 暂存区 stage
3. 分支 branch

### 工作原理
1. 版本库会追踪工作区下所有文件的文件写操作（UPDATE, DELETE, ADD)`ps：只能追踪UTF8 with BOM的文本文件，图片这类二进制文件只能追踪文件大小是否变化`
2. 执行`git add <file>` 会将写操作添加到暂存区中
3. 再执行`git commit -m "备注"`会将暂存区中的写操作提交到版本库的当前分支上（相当于游戏中的SAVE）

## Git命令
### 创建版本库
在目标目录下执行`git init`，会生成.git隐藏目录，该目录就是该版本库文件

### 查看版本库状态
在工作区下执行`git status`，会返回当前工作区的状态

### 查看文件修改内容
`git diff <filename>`：以linux的diff格式显示文件的修改内容

### 提交工作区的修改到暂存区
`git add <filename>`：将filename的写操作提交到暂存区

### 提交文件删除操作
`git rm <filename>`：将filename的删除操作提交到暂存区

### 提交暂存区的修改到当前分支
`git commit -m "备注"`：将暂存区中的写操作提交到当前分支

### 查看分支的提交日志
`git log`：查看文件修改记录，返回修改者身份，Git ID，以及备注信息

### 读档（Load Game）
`git reset`：有两种方式
1. 根据Git ID进行读档，`git rest GitID`，不过Git ID很难记忆，常用的是第二种读档方式
2. 读取前面第X个档，`git reset Head~X`

### 撤销修改
修改有三种状态：
1. 未提交到stage：只能直接读取当前branch的最新版本，`git reset HEAD~0`
2. 已提交到stage，但未提交到branch：可以恢复到上一次`git add`的状态，`git checkout -- <filename>`
3. 已提交到branch：只能读取前一个档，`git reset HEAD~1`

## 分支管理
### 介绍
在工作中，我们往往是各自负责一个模块的功能的开发，因为一个不完整的代码可能会导致无法运行或者其他的错误，为了不影响到其他人的开发，版本管理工具提供了“分支管理”功能，每个人先创建一个独立分支，再在这个分支上进行独立开发，开发完毕再合并到主分支上。

其实SVN也有这个功能，只不过它创建和删除分支的速度实在是太慢了，而Git却能在一秒钟内完成！

### 分支操作
1. 创建分支：`git branch <branch>`
2. 切换分支：`git checkout <branch>`
3. 创建并切换分支：`git checkout -b <branch>`
4. 删除分支：`git checkout -d <branch>`
5. 将分支合并到主分支上：`git merge <branch>`

### Fast-forward快进模式
如果在分支合并的时候没有出现冲突，那么就会看到返回状态表示`Fast-forward`(快进模式)

这里铺垫一个知识点，Git的`HEAD`就像一个指针，指向当前所处分支最新版本，`Master`其实也是一个指针，不过指向的则是主分支。

快进模式其实就是版本库直接把Master指针指向branch指针所指分支。这就是为什么Git在分支管理上的操作速度如此之快的原因！

### 分支冲突
上面合并分支的时候，master分支是不变的，那假如，master和branch分支都发生了改变，两条分支分叉了呢？Git又会如何处理这种分支合并？

Git会尝试合并，假如出现了两个分支都对同一个文件进行了修改的冲突，Git就会提示冲突文件，并且将不同的修改呈现在冲突的文件中（打开文件就能看到了），你需要确认最终的文件内容并且提交即可（此时的分支处于Merge状态，只能使用git add和git commit将冲突文件全部提交之后，才算完成Merge，你也可以通过git merge --abort退出合并）。