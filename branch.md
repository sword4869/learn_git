> add a branch
```bash
# git branch <branch>
$ git branch orange
```
创建分支的效果相当于虚拟机的快照。
PS：注意是对当前的 **commit到本地仓库中的** 的文件进行镜像。

> show branch

```bash
$ git branch
* main
  orange
```
`git branch`列出的分支前带`*`号的表示当前分支。

> switch to a certain branch
```bash
$ git checkout orange
Switched to branch 'orange'
M       branch.md
M       config.md
D       renmote.md
```
当你切换到某分支时，工作目录下的文件就是那个分支 **commit到本地仓库中的** 的文件。



```bash
# add a branch and switch to it
$ git checkout -b <branch>
```

> delete a branch
```bash
git branch -d 分支名字(同当前分支一样，即merge过的)
git branch -D 分支名字(同当前分支不一样，强制删除)
```

> rename a branch

```bash
$ git branch -M main
```
```
-M: 
Shortcut for --move --force.

-m/--move:
Move/rename a branch, together with its config and reflog.

-f/--force
Reset <branchname> to <startpoint>, even if <branchname> exists already. Without -f, git branch refuses to change an existing branch. In combination with -d (or --delete), allow deleting the branch irrespective of its merged status, or whether it even points to a valid commit. In combination with -m (or --move), allow renaming the branch even if the new branch name already exists, the same applies for -c (or --copy).
```

i.e. 想要重命名已存在的分支，重命名是`-m`，而修改已存在需要`--force`，`-M = -m -f`。

### 4.2.融合分支
```bash
git merge 分支名字
```
将某分支 **合并到当前分支** 中去。

融合效果：以某分支为主，而不是当前分支！
- 某分支中有的，当前分支中没有：则添加到当前分支。
- √某分支中没有的，当前分支中有：则**删除**当前分支中的。
- 某分支中有的，当前分支中没有：如无不同，则无事。如有不同，则冲突。

使用`git diff`查看冲突之处。会用`-`、`+`和红绿颜色标识。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801101916608.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)

