# Git 教程

## 常用命令
```bash
# 当前目录下创建git repository
git init

# 添加所有文件到暂存区
git add .

# 提交暂存区到仓库
git commit -m "<comment>"

# 远程同步
# 增加远程仓库
git remote add [shortname] [url]
"""
git remote add origin git@github.com:srhthu/Notes.git
url 为repository的网址后面加上.git
此命令相当于为远程仓库git@github.com:srhthu/Notes.git 起了一个别名 origin
"""

# 查看所有分支
git branch -r
"""
运行结果：
* master
  remotes/origin/master
master 为本地分支
remotes 表示远程分支
origin/master 为[远程仓库]/[仓库分支]
"""

# 推送本地分支到远程仓库
git push <repository> <refspec>
git push <repository> <src>:<dst>
"""
<repository> 远程仓库名/URL，在这里为origin
可以直接运行git push
"""
```

## 将本地仓库推到github新创建的仓库中
```
git remote add origin git@github.com:srhthu/gittest.git
git branch -M main
git push -u origin main
```