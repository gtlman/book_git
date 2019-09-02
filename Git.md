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




