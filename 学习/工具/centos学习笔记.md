## 文件目录



## 实用指令

+ **帮助指令**
  + man command
  + help command
+ **cat**
  + 把文件中的内容读取出来
  + `-n`    显示行号
+ **more**
  + 分页显示
  + 通常和管道符结合使用
+ **less**
  
  + 主要用于大型文件查看，加载的比较快
+ **》**
  
  + 覆盖写入
+ **》》**
  
  + 追加写入
+ **echo**
  + 将内容输出到控制台
  + echo $PATH
+ **head**
  + 默认显示前10行
  + -n num  显示前num行
+ **tail**
  
  + 同上
+ **ln -s [源文件目录]  连接名**
  + `软连接`
  + 类似于win下面的快捷方式
+ **history**
+ **find**
  + `find path -name` 文件名(可以使用通配符）
  + `find path -user` 文件名
  + `find / -size +20M`   查找大于20M的文件
+ **locate**
  + 必须先使用updatedb创建一下查询数据库
  + locate 文件名
+ **grep**
  + -n 显示行号
  + -i 忽略大小写
+ **|管道符号**
  
  + 可以将前面的一个指令的输出作为后一个指令的输入
+ **tar指令**
  + `zcvf`
    + 打包
  + `xzvf`
    + 解压缩
    + -C  可以指定解压目录，前提是目录存在
+ **组管理和权限管理**
  + 基本介绍
    + 每个用户至少属于一个组
    + /etc/group 组的信息放在这个目录下
  + 文件/目录所有者
    + 查看文件所有者
      + ls -ahl
    + `chown 用户名 文件名`
      + 改变文件的所有者
    + `chgrp 组名 文件名`
      + 改变文件的所在组
    + usermod
      + 可以用来修改用户账户
      + -d   修改登录目录
      + -g    修改用户所在组
    + groupmod
      + 修改用户组的属性
  + 查看用户和组
    + cat /etc/passwd
    + cat /etc/group
  + 权限
    + `rwx作用到文件`
      + r 可以读取查看
      + w 代表可写，可以修改，不代表可以删除文件。删除文件的前提是对文件所在的目录有写的权限
      + x 代表可以执行文件
    + `rwx作用到目录`
      + r:可以查看目录内容,ls
      + w:可以修改删除创建重命名目录
      + x: 可以进入该目录
    + chmod
      + chmod u+w 文件名
      + chmod g-r 文件名
      + chmod o -rwx 文件名
      + chmod a-w 文件名 
+ **任务调度**
  + crontab -e
    
    + 编辑任务
  + crontab -l
    
    + 查询任务
  + crontab -r
    
  + 删除任务
  + 步骤如下：
    + 编辑任务，如果只是简单的任务，可以不用写脚本，可以直接在crontab中直接编辑，如果是比较复杂的任务，需要自己写一个脚本
  
      

## 进程管理

+ ps
  + process status

+ ps aux
  + a 前端显示所有启动进程信息
  + u 以用户的格式显示进程信息
  + x 显示后台运行的参数
+ 终止进程
  + kill pid -9 强制杀死
  + killall 进程名称，也可以使用通配符匹配

+ pstree
  + -p
    + 显示进程的进程号
  + -u
    + 用户id的形式显示

+ 服务管理(service)
  + service 服务名 [start|restart|reload|stop|status]
+ chkconfig --list
  + 查看自启动列表
+ 服务监控
  + 动态监控
    + top
  + 监控网络状态
    + netstat

## 磁盘查询

+ 磁盘整体情况
  + df -lh
+ 查询指定目录的磁盘占用情况
  + du -ach
+ 常用指令
  +  ls -l grep "-&" wc -l /home   统计home文件夹下的文件个数



## 网络配置

+ 指定固定的ip
  + vi /etc/sysconfig/network-scripts/ifcfg-

