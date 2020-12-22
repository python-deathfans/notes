## Github基础知识

+ 仓库
  + 想要在github上开源一个项目，必须建立一个仓库，用仓库存放项目代码，一个项目对应一个仓库

+ 收藏(star)
  + 收藏仓库，下次方便检索

+ fork(复制或者克隆仓库)
  + 独立存在
  + pull request -> 等待作者通过
  + 若作者同意，则可以合并到仓库中

+ 发起请求（pull request）
  + 向forked的那个项目里面发起一个请求，更新代码
  + 仓库管理员会收到你的请求，如果感觉不错，可以合并到仓库中

+ 关注(watch)
  + 关注的人发动态会看到通知
  + 或者项目更新的时候可以看到

+ 事务卡片(issue)
  + 发现代码bug

## Git常用指令

+ git init     
  + 初始化git仓库
+ git status 
  + 文件状态，可以看看文件在什么地方
+ git add file
  + 把文件从工作区提交到暂存区
+ git commit -m '命令描述'    
  + 提交到本地仓库
+ git log
  + 可以查看所有产生的commit记录
+ **git branch a**
  + 新建一个分支，内容和主分支一样
+ **git checkout a**  
  + 表示把分支切换到a分支
+ **git checkout -b a**   
  + 表示新建一个分支然后切换到这个分支
+ **git merge  a**
  + 合并分支a到主分支master
  + 前提是现在就在主分支，如果不在，git checkout master
+ **git branch -d a**
  + 删除分支
+ **git branch -D a**
  + 强制删除分支a
+ **git tag**
  + 给代码打上标签，方便日后查看bug
+ **git push origin master**   
  + 把代码从本地提交到master分支
+ **git clone 仓库地址**    
  + 把别人仓库文件下载到本地
+ **git remote -v**
  + 查看关联的远程仓库
+ git config --list    查看设置
+ git commit -m ''-a   提交文件夹下面所有的文件
+ git add .     表示添加新文件和新编辑的文件
+ git  add -u   表示添加编辑或者删除的文件，不包括新添加的文件

## 向github提交代码

+ 利用SSH
  + 生成SSH key
    + ssh-keygen -t rsa
    + 生成两个文件，一个是id_rsa是密钥,id_rsa.pub是公钥
    + linux 文件在~/.ssh
    + win文件在/c/Documents and Setting/username/.ssh
  + 把公钥内容添加到github,这样就可以和本地密钥进行匹配了
    + git -T git@github.com    进行验证，是否添加成功
  + git pull origin master
  + git push origin master
    + 一般是push之前，先pull一下,这样可以防止冲突
  + 提交代码
    + git clone git@github.com:python-deathfans/study-notes.git
    + 我们可以把clone理解成高级点的复制，这样项目本身就是一个Git仓库了，不需要执行git init,甚至已经关联了远程的仓库，这样的话，只需要添加文件，然后git push origin master就好了
    + 这种情况适用于换了一台电脑，想要继续给仓库push文件。
  + 提交代码之前
    + git config -global user.name
    + git config -gloabal user.email

## 基本配置

+ git config -global user.name
+ git config -gloabal user.email
+ alia  别名
  + git config --global alias.psm 'push origin master'
  + git config --global alias.plm 'pull origin master'



## 常见问题及解决方法

> > error: failed to push some refs to 'git@github.com:....." Updates were rejected because the remote contains work that you do not have locally.
> >
> > 解决方法：
> >
> > 			git pull origin master   全部拉下来
> > 			git push -u origin master	这样就解决了

> > 解决方法：
> >
> > ​	git push -u origin master -f



## Git分支介绍

+ 什么是分支
  + 可以这么理解，几个人一起去旅行，中间走到一个**三岔口**，每条路可能有不同的风景，你们约定 3 天之后在某地汇聚，然后各自出发了。而这**三条分叉路就可以理解成你们各自的分支**，而等你们汇聚的时候
    相当于把你们的分支进行了合并。
+ 常用操作
  + git branch develop
    + 新建一个叫做develop的分支
    + 内容和当前所在的分支是一样的
  + git checkout develop
    + 切换到develop的分支
  + git checkout -b develop
    + 新建并切换到develop分支
  + git push origin develop
    + 把develop分支推送到远程仓库
  + git branch
    + 查看本地分支
  + git branch -r
    + 查看远程分支列表
  + git branch -d develop
    + 删除本地分支

## 知识补充

![](https://pic.downk.cc/item/5fe16eb33ffa7d37b316bb75.png)

+ **git branch**
  + 查看当前所在分支并显示所有分支
+ **git branch -a**
  + 显示本地仓库与远程仓库的所有分支

