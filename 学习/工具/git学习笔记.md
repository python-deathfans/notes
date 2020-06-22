## 第一章 初始化设置

```
git config --global user.name ""
git config --global user.email ""
```

+ 用户名和密码全部都是github上面的用户名和密码

+ 可以在**~/.gitconfig**查看所有配置

+ 设置**SSH Key**

  + GitHub上**连接已有仓库**时的认证，是通过使用了**SSH的公开密钥**认证方式进行的。

  + ```
    ssh-keygen -t rsa -C "email"
    ```

  + 在github中添加公钥

  + 测试是否添加公钥成功

    + ```
      ssh -T git@github.com
      ```

## 第二章 Git基本操作

+ **git init**
  + 初始化仓库
  + 要使用Git进行版本控制，首先需要初始化仓库，除非使用**git clone**克隆了一个仓库
+ **git status**
  + 显示本地仓库状态
+ **git add**
  + 向**暂存区**添加文件
+ **git commit**
  + 保存仓库的历史纪录
  + **-m 参数**，记述一行提交信息
+ **git log**
  + 查看提交日志
  + **指定文件**，查看该文件的提交日志
  + **-p** 该参数可以看某个文件的详细变化
+ **git diff**
  + 提交之前，使用命令 git diff HEAD
    + 查看两次提交的变化，这是一个好习惯

### 2.1 分支的操作

+ 多个并行作业时，需要用到分支。**master分支**是Git默认创建的分支，所有开发都是基于这个分支的
+ ![](https://pic.downk.cc/item/5eeff56214195aa594255374.png)

+ 不同的分支可以完成完全不同的工作，最后进行分支合并。合并到master分支
+ ![](https://pic.downk.cc/item/5eeff71314195aa59426784f.png)