## 基本操作

+ git status
  + 查看仓库状态
+ git add
  + 向暂存区添加文件
  + 暂存区是提交之前的一个临时区域
+ git commit
  + 保存仓库的历史记录
+ git log
  + 查看提交日志
  + 跟上文件，可以查看某个文件的提交日志。

养成一个好习惯，git commit之前，先执行**git diff HEAD**,查看本次提交与上次提交之间有什么差别。

## 分支

> 进行并行作业的时候，会使用到分支。

+ git branch
  + 显示所有分支
+ git checkout -b
  + 创建并切换分支
+ **git checkout branch**
  + 当前分支**切换**为branch
+ 主干分支
  + 合并的终点。通常将master分支作为主干分支。主干分支中没有开发一半的代码，可以随时供他人查看
+ git merge
  + 合并分支
  + 首先需要切换到**合并到的分支**
    + git checkout master
  + git merge --no-off feature-A
+ git log --graph
  + 以图表形式查看分支

## 推送至远程仓库

+ git remote add origin git@github.com:dfsdfsf.git
  + 添加远程仓库
  + Git自动将。。。远程仓库的名字设置为origin
+ git push -u origin master
  + 推送到远程仓库
  + 将当前修改的内容推送到远端仓库origin的master分支

## 下载远端仓库

+ git clone .....
  + 将远端仓库内容下载到本地
+ git branch -a
  + 查看本地和远端的所有分支
+ git pull
  + 获取最新的远端仓库分支