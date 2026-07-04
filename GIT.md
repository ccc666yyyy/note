# GIT



### 桌面创建文件夹（主要用于复制github上的项目）

桌面右键open git bash here,在终端中输入命令：

`git clone 某个项目git链接`



### 自己新建项目，用git来管理

1. 打开文件夹，打开git终端，输入`git init`

2. 在工作区新建项目后，需要在git仓库中备份，提交命令:

`git add .`把文件放入暂存区

`git status`查看当前工作区和暂存区的状态，有哪些文件被修改了、哪些被暂存了

`git commit -m "对本次提交备注"`

到此提交已完成，可以使用`git log`查看提交历史信息

```
git log --oneline      # 简洁版，一行显示一个提交
git log --graph        # 用图形化方式显示分支历史[reference:20]
```

> git add命令的功能类似于鼠标选中要提交的文件，git add file.text中，file.text进入准备提交状态，因此要对那个文件进行提交应该先add那个文件--把文件加入暂存区

> ![image-20260704172707730](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260704172707730.png)



版本回退：
`git reset --hard commitID`

恢复上一次提交内容：

`git chetout HADE 文件名（eg.main.py)`

HADE表示当前分支

### 分支

创建分支：

`git branch 分支名`

切换分支：
`git swith 分支名`

`git chekout 分支名`

创建并切换到指定分支：

`git awith -c 新分支名`

`git chekout -b 新分支名`

删除分支（不能删除当前所在的分支）：

`git branch -d 分支名`

`git branch -D 分支名 `（强制删除）

合并分支：

> 不同分支相互独立

要先切换到目标分支

`git merge 分支名`(一个分支上的提交可以合并到另一个分支上)

### 本地项目推送到github仓库

git push

如果直接在github上修改了需要先`git pull`把github上的修改版拉到本地在进行推送