### git上传项目到gitee的操作步骤

1 git init
先进入项目文件夹使用 git init 命令，把这个目录变成git可管理仓库即版本库repository

2 git add .
把文件添加到版本库中，将本地项目使用 git add . 加入到缓存区stage,不要忘记add 后的“.”，意为将目录中的所有文件都添加到缓存区
add是把当前分支的变更暂存起来，但不生成版本

3 git commit -m "firstcommit"
git commit -m 命令生成版本，并告诉git将缓存区文件提交到本地分支，后面引号中的内容为提交说明

4 git remote add origin 你的远程库地址
关联到远程仓库，例如：
git remote add origin https://gitee.com/jinronga/study-notes.git
其实是先remote添加了远程仓库，然后把自己的本地分支关联到某个仓库的某个分支

5.git pull --rebase origin master   代码合并
获取远程仓库与本地仓库的合并（如果远程仓库不为空，则必须进行这一步）

6 git push -u origin master
把本地仓库的内容推送到远程仓库，使用git push实际上是把当前分支推送到远程仓库的关联分支里

7 git status
查看状态

使用 git pull origin master 命令，将码云上的仓库pull到本地文件夹







本地没有ReadMe文件，那么就在本地生成一个：

git pull --rebase origin master ????本地生成ReadMe文件
git push origin master

two：
**强制**上传覆盖远程文件，
git push -f origin master

