# 基本配置
## 生成密钥
```bash
ssh-keygen -o
```



## 配置全局用户
```bash
git config --global user.email "your email"
git config --global user.name "your name"

# 查看配置信息
git config --global --list
```

> 注：这里的 `--global`相对应的有`--local`，local代表当前目录下的git
>



# 基本操作
## 初始化项目
在项目的根目录下

```bash
git init
```



## 创建并切换到一个分支
```bash
git checkout -b <branchname>
```



## 查看有哪些分支
```bash
git branch
```



可选参数：

> -r: 查看远程分支
>



## 将某个目录下的所有文件加入到分支
```bash
git add dir1/dir2/.
```



如果是当前目录

```bash
git add .
```



## 提交代码
```bash
git commit -m "<msg>"
```



> -m: 后面跟一条消息，表示这次提交的提示
>



## 查看已经提交的目录下某个文件夹
```bash
git ls-tree -d <branchname> <dir1/dir2/>
```



可选参数

> --name-only: 只查看文件夹名
>



## 查看当前目录下的远程地址
```bash
git remote -v
```



## 提交代码到远程
```bash
git push origin <branch name>
```



```bash
git push -u origin <branch name>
```

> -u --set-upstream的缩写，之后push, pull都默认这个分支
>



## 删除远程分支
```bash
git push origin --delete <branch name>
```



## 远程分支拉取到本地
```bash
git checkout -b <branch name> origin/<remote branch name>
```



## 取消上一次提交
但是修改还在占存区

```bash
 git reset --soft HEAD^
```



## 恢复某个文件
```bash
git checkout <commit-id> <path/file-name>
```



## 不在跟踪某个文件
```bash
git update-index --assume-unchanged <文件路径>
```

