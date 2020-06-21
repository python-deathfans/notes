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

      