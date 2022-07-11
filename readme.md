@[toc]

---


# 一、安装

[windows](https://git-scm.com/downloads)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731161501850.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)
具体安装过程中的解释：[Windows系统Git安装教程（详解Git安装过程）](https://www.cnblogs.com/xueweisuoyong/p/11914045.html)

---

linux：
```bash
apt-get install git
```
# 二、使用

运行Git Bash，语法是linux的终端，`ls`、`mkdir`之类的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731162317260.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731164835961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)

## 1.配置config（第一次初始化）
### 1.1.设置
比如`Gitee`码云，你会有两个关键的信息要填写，一个是你的账号名字，一个是你的邮箱。这两个和你使用`git`来链接到`gitee`等之上有关。

```bash
$ git  config --global  user.name  '注册的用户名';
$ git  config --global  user.email  '注册时候的邮箱';
```
### 1.2.检查是否配置成功：
```bash
$ git config --list
user.name=Scott Chacon
user.email=schacon@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...

$ git config user.name
Scott Chacon
```

## 2.创建仓库
### 2.1.先在网站创建
git只是个提交工具，将本地仓库的代码提交到远程仓库中。**所以你得先在网站上创建一个远程仓库**，这让git知道提交到哪里。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731162649905.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)
这个链接就是提交到的远程仓库。

### 2.2.创建本地仓库
#### 2.2.1.先创建一个目录
```bash
mkdir XXX
cd XXX
```
这就是本地仓库，**本地仓库就是个文件夹**，将git要提交/下载下来的东西放到这里去。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731162815381.png)

#### 2.2.2.git化文件夹
怎么让这个普通的文件夹，变成git的仓库呢？
用这个命令生成一个`.git`配置来允许git来管理它，所有 Git 需要的数据和资源都存放在这个目录中。
```bash
$ git init
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731163157466.png)
## 3.本地提交

### 3.1.查看工作区的文件
工作区文件就是就是工作目录（`.git`的父级目录）下除了`.git`的文件。

比如，我在文件夹下创建了个`click.py`或者将别的地方的`click.py`移动到这里。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731164658929.png)
```bash
$ git status
```
这条命令显示还没有提交到缓存区的工作区的文件，用来查看是否还有文件未提交。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731164926187.png)
### 3.2.add到暂存区
```bash
$ git add 'click3.py'
```
注：使用`git add -A`或`git add . `（`.`是说本目录下的全部文件）可以提交当前仓库的所有改动。

对应`git rm --cached xxx`取消放入暂存区。

### 3.3.commit到本地仓库
将缓存区里的文件都commit到本地仓库`.git`中。

PS：为什么要提交？这个文件夹里不是有吗？
本地仓库又名版本库，提交是让Git来管理的意思，在`.git`的里面的信息变动。提交后的文件被Git管理起来，对文件的修改、删除，Git都能跟踪，可以比较不同、可以还原。

```bash
$ git commit -m "备注信息"
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731170040668.png)

可以使用`git log`来查看提交记录。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731170252254.png)
### 3.5.删除、移动（重命名）文件
如果只是简单地从工作目录中手工删除`rm xxx`文件，运行 `git status` 时就会在 `Changes not staged for commit`的提示。**因为你没有告诉git你的变动**，git本地仓库中还保留着该文件。

1. 【删除git本地仓库中，并删除工作区中】
```bash
git rm xxx
```

2. 【删除git本地仓库中没有，只是提交到暂存区的，并删除工作区的】
```bash
git rm -f xxx
```
PS：如果git本地仓库中有，也提交到暂存区的。那么删除后，暂存区中的和本地仓库中的都没得。

3. 【把文件从暂存区域移除，但仍然希望保留在当前工作目录中：就是取消放入暂存区】
```bash
git rm --cached xxx
```
对应的，用`git add xxx`再添加到暂存区

4. 【暂存区和本地仓库中都没有的：一般是新建在工作区的，才可以直接删除】
```bash
rm xxx
```

## 5.远程仓库
### 5.1.创建公钥（第一次初始化）
```bash
ssh-keygen -t rsa -C 'your email'
```
接着按3个回车就行
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731171355283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)
可以看到公钥`id_rsa`（私有秘钥）和`id_rsa.pub`（公有密钥）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731171425816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)
打开`id_rsa.pub`（公有密钥），复制里面的内容。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731171627233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NhbmRhbHBob240ODY5,size_16,color_FFFFFF,t_70)
标题随便起，只是用于区分而已，如同图片中的`Foast`。
将复制的公钥内容粘贴在公钥中，确定就ok。

### 5.2.git remote
1. 【将本地仓库与远端仓库建立一个链接】
```bash
git remote add 给远程仓库的命名 远程仓库的地址
```

给远程仓库的命名不要重复。因为可能需要本地仓库会推送到多个远程仓库。


e.g.上传到多个远程仓库的例子：Alpha和Beta就是别名不要重复的意思，要不然push不知道push到哪个远程仓库。
```bash
$ git remote add Alpha your_first_git_address	# 将第一个git address命名为Alpha
$ git push -u Alpha master
$　git remote add Beta your_second_git_address	# 将第二个git address命名为Beta
$ git push -u Beta master
```
2. 【要查看当前配置有哪些远程仓库，可以用命令】
```bash
# -v表示显示详细参数
git remote [-v]
```
e.g.
```bash
$ git remote
origin
$ git remote -v
origin    git@github.com:tianqixin/runoob-git-test.git (fetch)
origin    git@github.com:tianqixin/runoob-git-test.git (push)
```

3. 【删除与某个远程仓库的链接】
```bash
git remote rm 远程仓库别名
```
### 5.3.push
1. 【将本地某分支指定推送到远程某分支】
```bash
git push <远程主机名> <本地分支名>:<远程分支名>
```
将`本地的分支`推送到`远程仓库`的`远程分支名`。

2. 【将本地某分支指定推送到远程，更新或创建】
```bash
git push <远程主机名> <本地分支名>
```
将`本地的分支`推送到`远程仓库`的`同本地分支名`。
两种情况：远程仓库有，则更新。没有，则创建一个新的分支，名同本地分支名。

3.  【删除远程仓库的某远程分支】
```bash
git push <远程主机名> :<远程分支名>
```
注意：`:`前前是空格。
```bash
# 例如
git push origin :master
# 等同于
git push origin --delete master
```
4. 【将本地当前分支指定推送】
```bash
git push <远程主机名>
```
将`当前分支`推送到`远程仓库`。

5. 【将某分支指定推送并默认化】
```bash
git push -u <远程主机名> <本地分支名>
```
将`本地的分支`推送到`远程仓库`，同时指定`远程仓库`为`默认的远程仓库`，后面就可以不加任何参数使用`git push`了。

6. 【将当前分支推送到默认远程仓库】
```bash
git push
```
只有当默认指定`远程仓库`后，才能使用！


### 5.4.clone
通过HTTPS协议克隆
```bash
git clone https://gitee.com/xxx.git
```
通过SSH协议克隆
```bash
git clone git@gitee.com:xxx.git
```

例：不用特地创建一个文件夹了，clone下来默认直接以远程仓库名为名创建一个文件夹。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731174229921.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200731174147400.png)
### 5.5.fetch和merge分支
#### 5.5.1.fetch
```bash
git fetch <远程主机名> <远程分支名>
```
结果是在本地仓库创建一个本地分支`<远程主机名>/<远程分支名>`中。但并不会在`git branch`中显示。
e.g.
```bash
$ git fetch origin master
 * branch            master     -> FETCH_HEAD
   d48f66c..ee96b01  master     -> origin/master

# 但并不会在`git branch`中显示。
$ git branch
* master
```
#### 5.5.2. merge
```bash
git merge <远程主机名>/<远程分支名>
```
合并名为`<远程主机名>/<远程分支名>`的分支到当前所在分支。

e.g.
```bash
$ git merge origin/master
```
#### 5.5.3. pull

基本用法：```git pull <远程主机名> <远程分支名>:<本地分支名>```。

- 例如执行下面语句：```git pull origin master:brantest```，将远程主机origin的master分支拉取过来，与本地的brantest分支合并。
- 后面的冒号可以省略：```git pull origin master```。表示将远程origin主机的master分支拉取过来和本地的当前分支进行合并。

```git pull = git fetch + git merge```。上面的pull操作用fetch表示为：
```bash
git fetch origin master
git merge origin/master
```
相比起来git fetch更安全一些，因为在merge前，我们可以查看更新情况，然后再决定是否合并。

### 5.6.更新
#### 5.6.1.正常更新
```bash
git add *
git commit -m "xxx"
git push origin master
```
#### 5.6.2.强制更新（合并冲突的问题）
（1） 使用此命令告诉 git 允许不相关历史合并 这样就能把远程文件拉取回来。执行此命令后会有一个提示，要求说明为何要讲两个不相关的分支合并，输入信息后保存即可。
```bash
git pull origin master –allow-unrelated-histories
git push origin master
```
（2）强制将本地文件推送至远程，**这样会将远程仓库的master分支的历史文件都清掉**。从而不会产生因为合并冲突的问题.
PS：建议使用此命令前备份一个远程分支：先本地创建一个分支，拉去远程分支，再push一个新的分支，最后再push到那原来的分支。
```bash
git push origin master -f
```
（3）push到一个新的远程分支。

# 三、常用流程
## 1. 将本地写好的东西提交到空的远程仓库
```bash
git init	# 在本地写好的东西的文件夹中
git add *
git commit -m ''
git remote add origin https://xxx.git
git push -u orgin master
```
之后每次就可以直接`git push`

## 2. 将本地写好的东西提交到有东西的远程仓库
```bash
git clone	# 先在一个随便的文件夹下
...			# 进入下好的文件夹下，将本地写好的东西复制到这里
git add *		
git commit -m ''
git push	# 已经将远程仓库默认了
```
---

# Reference
[Git使用教程：最详细、最傻瓜、最浅显、真正手把手教！](https://blog.csdn.net/u011535541/article/details/83379151)
