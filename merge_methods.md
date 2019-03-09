# 关于Git中分支合并的操作
考虑到要建立不同分分支，因此在在主分支master下，添加.gitignore文件，接下来按如下步骤进行
* 初始化Git和基础文件
```
git add --all
git commit -m "init project"
```
* 首先在主分支下建立新分支test1
```
git cehckout master
git branch test1
git checkout test1
```
* 切换到分支test1，(需要在编写程序前切换，文件才在test1分支中记录）添加文件（此时在test1分支上编写程序，编写完成后进行文件添加和提交）
```
git add --all #or git add filename
git commit -m "coding test1.c"
```
* 切换到主分支下，编写程序master.c，添加并提交
```
git add master.c
git commit -m "coding master.c"
```
* 新建分支，并切换到分支，编写程序
```
git branch test2
git checkout test2
git add test2.c
git commit -m "coding test2.c"
```
* 合并分支test1和master，先切换到主分支，在合并（无冲突）
```
git checkout master
git merge test1 # 此处需要提交合并消息
git branch -d test1 #删除无用分支
```
* 接着合并test2分支
```
git checkout master
git merge test2
git branch -d test2
```
*接下来演示有在冲突下的分支合并*
* 首先在主分支master下建立新分支test3，并切换到特色test3分支
```
git branch test3
git checkout test3 #
```
* 制造冲突，在分支test3下，删除test1.c，新建文件test1.py，并添加/提交
```
git add test1.py
git commit -m "coding test1.py on python"
```
* 在主分支下修改文件test1.c，并添加、提交
```
git checkout master
git add test1.c
git commit -m "add coding in test1.c"
```
* 切换到主分支合并，Git会提示文件冲突
```
git checkout master
git merge test3
```
* 此时可以通过`git status`查看需要进行的操作，如果需要保留这两个分支上的文件，执行如下
```
git add test1.c
git add test1.py
git commit #此时会弹出窗口提交合并消息
```
*当然在合并过程中可以用`git mergetool`解决合并中的问题*