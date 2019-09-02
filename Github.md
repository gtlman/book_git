# <center>Github</center>
## 介绍
自从被微软入股之后，现在每个人可以拥有无限的Git的远程私人/公开仓库了，是程序员的好伙伴

## 绑定Githup
### 创建SSHkey作为机器身份辨别的密钥
1. windows下，打开cmd执行命令：`ssh-keygen -t rsa -C "youremail@example.com"`，非专业用的话直接一路认就行，然后进入到`用户目录`下的`.ssh`目录，看到生成了`id_rsa`和`id_rsa.pub`两个文件，前文件私钥，后文件钥
2. linux下，执行命令：`ssh-keygen -t rsa -C "youremail@example.com"`，`/root`下会生成`.ssh`目录，看里面生成了`id_rsa`和`id_rsa.pub`两个文件

### 将SSH公钥添加到GitHub账号
打开GitHub网页版，找到`setting`（用户设置），在左侧找到`SSH and GPG keys`，点击`New SSH key`添加SSH公钥，然后打开上面创建的公钥文件，将内容复制到上面即可

## 关联GitHub远程仓库
### 远程仓库为空，本地推送到远程仓库
1. 在GitHub那里创建一个空的版本仓库（此时GitHub会贴心地给出后面两个命令的提示，可以直接复制）
2. 在本地版本库执行：`git remote add origin git@server-name:path/repo-name.git`绑定本地版本库和远程版本库
3. 在本地版本库执行：`git push -u origin <branchX>`,对于空的远程库`-u`参数会把当前的`branch`跟远程库的`branchX`绑定，以后本地`branch`和远程`branchX`的交互命令可以简化为`git push`或者`git pull`

### 本地为空，克隆远程库到本地
命令格式：`git clone -b branch-name git@server-name:path/repo-name.git`
在GitHub项目页面提供了`clone or download`的按钮，可以直接复制clone命令或者下载zip包到本地
克隆下来的版本库已经与远程仓库绑定