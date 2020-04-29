## 设置语言环境

+ 点击小齿轮
+ 点击system setting
+ 点击 Language Support
+ 点击install ,选择chinese simplied

## 设置服务器镜像源

+ Ubuntu中大部分的软件安装和更新都是利用apt命令，从ubuntu的服务器直接安装的
+ ubuntu服务器是在国外，国内有很多镜像源
+ 方法
  + 点击系统设置
  + 点击软件安装源
  + 选择下载自 

## apt终端命令

+ apt 全称 **Advanced Package Tool**,是Ubuntu下的安装包管理工具

+ 大部分的软件安装、更新、卸载都是利用apt命令来实现的

+ 常用命令

  + sudo apt **install** 软件名
  + sudo apt **remove** 软件名
  + sudo apt **update** 
    + ·更新可用软件包**列表**

  + sudo apt **upgrade**
    + 更新已安装的**包**

+ apt与apt-get的区别
  + 两者都是ubuntu安装软件的命令
  + apt-get是ubuntu16之前 的命令
  + ubuntu16之后官方建议使用apt命令

## 软件安装

### deb格式的安装包如何安装

+ **sudo dpkg -i** <package.deb>
+ **sudo apt -f install** 解决依赖关系

### tar.gz安装包如何安装

+ tar zxvf xxx.tar.gz
  + 解压缩
+ ./configure
  + 检查编译
+ make
  + 生成用于编译的makefile文件
+ sudo make install
  + 编译之后，开始安装

+ make clean
  + 清理临时文件
+ make uninstall 
  + 卸载

## 文件目录结构

+ `/bin`
  + 存放一些可执行的命令或者指令
+ `/dev`
  + 主要存放Linux的外部设备，由于Linux中万物皆文件，所以访问设备和访问文件是一样的
+ `/etc`
  + 主要放配置文件
+ `/home`
  + 用户的主目录，每个新建的用户都有一个文件夹
+ /media
  + U盘或者光盘，都会挂载到这个目录下
+ /opt
  + 第三方软件的放置目录
+ /usr
  + 类似于windows里面的program files
+ **文件查找指令**
  + `find`
    + path -name filename    可以查找指定路径下面的某个文件
  + locate
    + filename      什么都会找出来
  + whereis
    + 通过软件名的方式找出文件所在的位置
  + which
    + 只可以搜搜可执行文件的路径

## 存储结构及磁盘划分

+ **物理设备命名规则**
  + 硬盘设备由大量的"**扇区**"组成，其中第一个扇区保存**主引导记录**(MBR)与**分区记录**。
  + **单个分区**容量为**512bytes**组成
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-23_15-35-30.png" style="zoom:80%;" />
  + 所以一般来说，会选用3个**主分区**加一个**扩展分区**，扩展分区可以划分无数个逻辑分区

+ **文件管理系统**
  + 作用是将硬盘合理的规划，使得用户能够在上面正常进行建立文件、读写、修改文件
  + 实际的文件保存在**block**中(大小可以是1k、2k、4k),以4k为例
    + 文件体积很小(1k),依然占用1个block,浪费了3k
    + 文件体积很大(5k),那么会占用2个block
+ **挂载硬件设备**
  + **挂载 操作**
    + 当用户需要使用硬盘设备或分区数据时，需要先将其与一个已经存在的目录文件**关联**。
    + **mount 文件系统 挂载目录**
  + 

## 基本指令

+ `cd`
  + change directory
  + cd    切换到家目录
  + cd ..  切换到上一级目录
  + cd -  切换到刚刚切换到的路径，相当于回看
+ `pwd`
  + 当前工作路径
  + 绝对路径
+ `ls`

  + 列出目录下面的文件和文件夹
  + **ls -l**
    + 以列表的形式显示文件的详细信息
    + 不显示隐藏文件
  + **ls -a**
    + 显示所有文件，包括隐藏文件
  + **ls -t**
    + 按照修改时间进行排序
  + **ls -lh**
    + 更人性化的方式显示
  + 可以使用`通配符`的形式进行显示
    + ***任意个字符**
    + **? 单个字符**
    + [characters]   匹配任意一个属于字符集的字符
    + [!characters]  匹配任意一个不属于字符集的字符
    + g*   文件名以g开头的文件
    + b*.txt   文件以b开头后缀是txt的文件
    + Data???  以Data开头后面是三个字符
    + [abc]*    以a或b或c开头的文件
    + BACKUP.[0-9] 
    + [[:alnum:]]    匹配任意一个字母或者数字
    + [[:alpha:]]     匹配任意一个字母
    + [[:digit:]]       匹配任意一个数字
    + [[:lower:]]     匹配任意一个小写字母
    + [[:upper:]]    匹配任意一个大写字母
+ `touch`

  + **创建文件，如果不存在**
  + 修改文件的**最后修改时间**，如果存在
+ `cp`
  + 复制文件
  + **cp old new**
  + **cp -i old new**  交互信息
  + **cp -R folder1/ folder2/**
  + 支持模糊匹配
+ `mv`
  + 移动文件
  + mv file1 folder1/
  + mv file2 file2rename   重命名
+ clear

  + 清屏
+ `mkdir`

  + **mkdir -p a1/b2/c3**  创建一系列目录,**递归创建**
  + 如果目录下有同名的文件，则无法创建同名的目录
+ `rmdir`

  + 移除`空`文件夹
+ `rm`

  + **删除之后，不能恢复**
  + **rm -i file**    交互信息
  + rm -f 文件 **没有任何提示信息**
  + **rm -r folder**   删除文件夹
    + recursive
  + rm *

      + 删除目录下面所有的文件
+ `nano`

  + 编辑文件
+ `gedit`

  + 编辑文件
+ `cat`
    + 查看或者合并文件内容
      + cat t.py `>` t1.py
        + **类似于重写**
        + 如果t1.py不存在，则效果是显示t.py中的内容
      + 如果后面跟着多个文件，可以进行顺序的合并
    + cat t.py `>>` t1.py
      + **追加信息到**t1.py
    + cat **-b** file
      + 空行不编号
    + cat **-n** file
      + 所有行都进行编号
+ `more`
    + 文件太多的时候可以**自动分屏**显示
    + 这个是和cat最明显的区别
+ `grep`
  + 搜索**文件内容**
  + grep -n " ds" xx.txt
    + -n 代表显示行号
    + -i  不区分大小写
    + -v 取反
+ `echo`
  + 在**终端中显示**参数指定的文字，通常会和`重定向`联合使用
  + 字符展开
    + echo this is a test
  + 路径展开
    + echo *
      + 打印出当前路径下的文件
    + echo D*
      + 打印出当前路径下以D开头的文件
  + echo $PATH
    + 列出环境变量的值
  + 给环境变量增加值
    + PATH=$PATH:值(路径)
  + export 变量名
    + 可以把变量名变成全局变量，所有用户均可以访问到
+ `重定向`
  + 将本应该在终端的内容**写入/追加**到指定的文件中
  + 一个大于号表示**写入**
  + 两个大于号表示**追加**
+ `分屏`
  + more 文件名
+ `管道 |`
  + 可以把**第一个命令**的**输出结果**传递到**第二个命令**进行操作
  + 后面常跟的命令：`more` 、`grep`
+ `软连接`
  + ln -s 源文件 目标文件
    + 源文件删除，目标文件就没法访问
+ `查找文件 find`
  + find [路径] -name “*.py”
    + 查找路径下面以.py结尾的文件
+ `起别名 alias`
    + alias 别名=“命令”
    + unalias 别名
    + alias cp="cp -i"
+ `tree`
  + 以树状结构显示文件目录信息
+ `打包压缩`

  + **tar** 是Linuz中最常用的**备份工具**，此命令可以把一系列文件**打包到一个大文件**中，也可以把一个打包的大文件**恢复成一系列文件**
    + tar -cvf 打包文件.tar 被打包的文件/路径。
    + tar -xvf 打包文件.tar **解包命令**
  + **tar与gzip**命令结合可以使用实现文件的**打包和压缩**
    + tar 只负责打包文件，但不压缩
    + 用gzip压缩tar打包后的文件，扩展名一般用 xxx.**tar.gz**
  + **tar -czvf 打包文件.tar.gz 被压缩的文件/路径**
  + **tar -xzvf 打包文件.tar.gz**
  + **tar -zxvf 打包文件.tar.gz -C 目标路径**

## 其他命令

+ **查找文件**
  + `find` 路径 -name "filename"
  + 不加路径默认是当前路径
+ **软连接**
  + 类似快捷方式
  + ln -s 源文件`完整路径` 链接文件名
  + 如果使用相对路径，当连接文件移动之后，连接就会失效
+ **打包压缩**
  + **可以使用通配符**
  + 打包
    + tar -cvf 打包文件.tar 路径
    + tar -xvf 打包文件.tar
  + 压缩
    + tar -zcvf  打包文件.tar.gz 文件路径
    + tar -zxvf 打包文件.tar.gz -C 目标路径

## 远程管理命令

+ `shut down`
  + **一分钟之后关闭电脑**
+ `shut down -r`
  + 一分钟之后重启
+ `shut down -r now`
  + 立刻重启
+ `shut down -c`
    + 取消关机命令
  + `reboot`

- `网卡`

  - 专门负责网络通讯的**硬件设备**

- `ip地址`

  - 设置在网卡上的地址信息

- `ifconfig`

  - 查看计算机当前的**网卡配置信息**

- `ping`

  - 检测到**目标ip**地址的链接是否正常
  - 检测**本地网卡**是否工作正常
    - ping 127.0.0.1

- `ssh`

  - **secure shell**

    - 数据传输是加密和压缩的

  - `域名`

    - DNS解析，把ip地址解析成域名

  - `端口号`

    - 通过端口号，可以找到计算机中的**程序**

    - | 序号 | 服务      | 端口 |
      | ---- | --------- | ---- |
      | 01   | SSH服务器 | 22   |
      | 02   | Web服务   | 80   |
      | 03   | HTTPS     | 443  |
      | 04   | FTP服务器 | 21   |

  - 简单使用

    - **sudo apt install openssh-server**
    - **ssh [-p port] user@remote**

  - 无密码ssh另一台主机

    - ssh-keygen
    - ssh-copy-id -i .ssh/id_rsa.pub 用户名@ip地址
    - ssh user@remote

- `scp`

  - **secure copy**
  - scp -P port 01.py user@remote:Desktop/01.py
    - 拷贝文件
  - scp -P port user@remote:Desktop/01.py  01.py
  - scp -r demo user@remote:Desktop
    - 拷贝文件夹



## 用户权限

+ `ls-l`
  + **r** 可读
  + **w** 可写
  + **x** 可执行
  + 前三个   **文件拥有者**  权限
  + 中间三个 **组内者**   权限
  + 最后三个  **其他用户** 权限

+ `chmod`

  + chmod +(-)r(w\x) file
    + 如果文件夹没有**可执行权限**，则无法查看文件夹内的信息，ls cd命令都会失效 
    + 没有可读权限的话，没法使用ls命令

  + chmod u+r t1.py
    - user对于t1.py加上可读的权限

  - chmod u-r t1.py
    - user对于t1.py去掉可读的权限
  - chmod g+r t1.py
  - chmod a+r t1.py
  - 还可以使用数字进行修改权限

+ `组管理`
  + `sudo groupadd`
  + `sudo  groupdel`
  + cat /etc/group   查看是否成功
  + chgrp -R dev Python学习/
    + 递归的改变文件所属的组

+ `用户管理`

  + **sudo useradd -m -g**
    + -m 自动建立用户家目录
    + -g 指定用户所在的组
  + **sudo passwd 用户名**
    + 设置用户密码
  + userdel -r 用户名
    + -r 自动删除用户家目录
  + `who`

    + 当前登录的所有用户
  + `whoami`
    + 打印用户名
  + `su 切换用户`

    + su 用户名

    + exit 表示退出用户 或者 ctrl+d

## 系统信息

+ `date`
  + 查看系统时间
+ `cal`
  + 日历（一月）
  + cal -y 全年
+ `df -h`
  + disk free 显示磁盘剩余空间
+ `du -h`
  + 显示目录下的文件大小
+ 进程
  + 程序和进程的区别
  + `ps`  process status  进程状态
    + `ps aux`    查看进程的详细状态
    + ps au  `常用这个命令`
  + `top`  
    + 动态显示进程的信息 
    + 3s刷新一次
    + `q退出`
  + `kill` 
    + 终止指定代号的进程
    + [-9] 强制停止
    + kill -9 pid
+ **service**
  + 用来查看服务状态的指令
  + service  (空格)--status -all
    + 查看当前所有服务
  + service 服务名　start
  + service 服务名　stop
  + service 服务名　restart
  + service 服务名　status

## 定时任务

+ at

  + 一次性定时任务

  + 需要手动安装　　sudo apt install at

  + service atd status    查看启动状态

  + ```
    at 时间点(now+1min)  ## 设置任务执行时间
    at > 执行命令		 ## 任务的动作
    at > <EOF>			## ctrl+d发起任务
    ```

  + at -l  查看列表

  + at -c 任务号　　#查看任务内容

  + at -r r 任务号       # 取消任务执行

+ crontab

  + 每天定时任务计划执行
  + 必须开启cron服务



## 远程连接

### windows远程linux-putty(ssh)

+ 在Linux安装 **sudo apt install openssh-server**
+ 在windows安装**putty**
+ **Linux terminal sudo apt install net-tools**
+ ifconfig,找到linux的inet ip
+ 填入到putty
+ 输入用户名和密码
+ 即可进入到linux的terminal
+ `注：这个只能进入到terminal,没法进行可视化窗口的显示，这些需要用到其他的软件`

### 可视化链接到linux

+ teamviewer
  + 通过外网的方式进行连接
  + 速度可能不是很快，取决于外网的网速

+ VNC
  + 局域网内部进行使用
  + 同一个路由器下面
  + linux
    + sudo apt install x11vnc
    + x11vnc -storepasswd
    + x11vnc -usepw -forever

  + windows
    + TightVNC
    + RealVNC

## 局域网多台电脑共享文件

+ linux
  + 创建新的文件夹
  + 右键 local network share
  + 点击share this folder
  + 点击allow others to create and delete files
  + sudo useradd bulabula
  + sudo smbpasswd -a bulabula
  + service iptables stop

+ win
  + 找到网络
  + 输入//linuxip

## vi -- 终端中的编辑器

+ vi visual interface
+ 特点
  + 不支持鼠标操作
  + 没有菜单
  + 只有命令

+ **vi 文件名**
  + 如果存在，就可以打开
  + 如果不存在，就会新建

+ 打开文件并且定位行
  + **vi 文件名 +linenum**
  + vi 文件名 +  定位到文件末尾
  + vi 文件名  定位到开头

+ 移动命令
  
+ hjkl
  
+ yy
  
+ 复制光标所在行
  
+ `vim`
  + vi improved
  
  + 编辑器之神
  
  + 启动vim进入的是命令模式（也称为**Normal模式**），在命令模式下输入英文字母`i`会进入编辑模式（**Insert模式**），屏幕下方出现`-- INSERT --`提示；在编辑模式下按下`Esc`会回到**命令模式**。
  
  + **wq** 保存并退出
  
  + **q!**强制退出，不保存
  
  + **命令模式常用的快捷键**
  
    + | 命令    | 作用                           |
      | ------- | ------------------------------ |
      | dd      | 删除(剪切)光标所在的行         |
      | 5dd     | 删除(剪切)从光标开始的5行      |
      | yy      | 复制光标所在的整行             |
      | 5yy     | 复制从光标开始的5行            |
      | p       | 将之前删除或者复制的文字粘贴来 |
      | /字符串 | 在文本中从上到小搜索该字符串   |
      | ?字符串 | 在文本中从下到上搜索该字符串   |
  
  + **末行模式常用命令**
  
    + | 命令      | 作用         |
      | --------- | ------------ |
      | :w        | 保存         |
      | :q        | 退出         |
      | :q!       | 强制推出     |
      | :wq!      | 强制保存推出 |
      | :set nu   | 显示行号     |
      | :set nonu | 不显示行号   |
      | :命令     | 执行命令     |
      | :整数     | 跳转到该行   |

## 软连接

+ 类似于windows快捷方式
+ ln -s 文件的完整路径 快捷方式名称
  + 没有-s,建立的是硬链接
  + 使用的是绝对路径，不能使用相对路径

## Tips

+ 好多服务或者软件都是d结尾，d代表的是deamon　守护进程
+ 守护进程是运行在linux服务器后台的一种服务
+ 放大终端字体：ctrl+shift++
+ 缩小终端字体:ctrl + -