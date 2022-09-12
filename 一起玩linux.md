# 一起玩linux

*<u>**装双系统一定备份好数据***</u>

自由开源的操作系统与win和mac都不一样

只是一个内核，衍生出发行版

linux  三个系列

- ubuntu 基于debian ，deepin  包管理器deb
- centos  ,fedora（red hit）   rpm
- Archlinux    majaro    优点：新快全

archlinux  wiki，论坛

linux中桌面环境是可以换的。

## manjaro-cinnamon桌面

![1657366559169](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1657366559169.png)

在这里面设置语言为中文

先升级sudo pacman -Syy

再装下中文字体

查询软件（文泉意） pacman -Ss wqy

sudo pacman -S wqy-microhei

查看linux内核版本

uname -a

pacman -Ss heards

sudo pacman -S linux515-headers

终端中$一般用户

#root用户，exit退出root用户

前面用户名，后面机器名。

~代表用户目录

pwd查看当前目录，print work directory

在linux中根，root用户叫根，也叫根目录

ls 打印当前目录  list

clear清屏

### pacman

```
在命令行怎么装软件  package manager 简称pacman
pacman -Ss xxx  搜索软件
whoami查看当前用户
pacman -Ss code
sudo pacman -S code

下载的慢源问题。。。
换源
用txt，打开
sudo xed /etc/pacman.conf
在浏览器找到清华源，复制到文件里面
更新
更新源		sudo pacman -Syy 
更新系统	sudo pacman -Syu 

搜索		pacman -Ss archlinuxcn

安装密钥	sudo pacman -S archlinuxcn-keyring

查看已安装软件 pacman -Q  xxx/pacman -Q | grep xxx 

删除全部依赖	pacman -Rsunc xxx 

查看系统剩余空间 df -h(按M显示) （disk filesystem）
清屏 clear ^L 

```

### file

``` 
蓝色的代表文件夹，白色的是文件，
跳转	 cd /etc/（change drirectory）
复制	cp source target 从source 复制到target(copy)
移动	mv source target 从source移动到target (move)
删除 rm -f （remove）
查看 cat正序查看  tac倒序查看  less
创建文件  touch name（空文件）
查找命令的路径  which xxx
打印 echo ~
上次使用的目录 -
当前目录  .
上级目录  ..
切换目录  cd
显示当前目录 pwd (print working directory)
目录内容 ls -l
创建文件夹  mkdir 只能创建一级
mkdir -p a/b/c 能创建三级
删除 rmdir 只能删除空目录文件夹
rm -r 递归删除，慎用
find xxx -name 'ooo'  查找xxx目录下的ooo名字文件或文件夹
find xxx -name 'ooo' -type f 查文件
find xxx -name 'ooo' -type d 查文件夹
locate 快速定位件的路径，它会从系统文件名和路径的数据库中查，效率更快一点，使用locate前先执行
updatedb 更新数据库
which 查找环境变量中命令所在的目录 例 which vim / which java
whereis 查找命令，源码 ，man手册页所在的目录  whereis vim
grep 过滤查找，通常和管道符一块使用，将前一个命令的结果输出给后面的文件处理
cat hello | grep java
gzip 文件名， 压缩文件
gzip -d 文件名.gz 解压文件
gzip -r aaa 把aaa文件夹下面所有的文件都压缩
tar -czvf 名字 文件夹名 压缩文件夹  tar -czvf aaa.tar.gz aaa
tar -zxvf aaa.tar.gz -C /usr  把aaa.tar.gz 解压到/usr文件夹下
```

![1657420511833](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1657420511833.png)

修改虚拟机硬盘大小

```
查看不需要的包 pacman -Qtd
pacman -Scc 删除缓存
```

## 进程

通过ps命令可以查看当前系统中运行的进程状态

```
ps -a 显示所有进程信息
	u 以用户格式显示进程信息
	x 显示后台进程运行的参数
ps -aux 
```

![1658669076939](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1658669076939.png)

```
kill -9 pid 强制杀掉 pid为进程id
kill -15 pid  优雅杀掉，有可能杀不掉
kill -all pid  包括子进程
```



### archlinux

- qq



```
archlinux用 的这个archlinuxcn仓库
[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch
yay 16
deepin-wine-qq
```

- 微信

![1657432922734](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1657432922734.png)

```
deepin-wine-wechat
解决中文乱码
https://juejin.cn/post/6921294885907759112

```

ip

```
ip addr  查看ip地址
/etc/sysconfig/network-scripts/ifcfg-ens33
BOOTPROTU=static
最后一行添加ip
IPADDR=192.168.XX.XX
NETMASK=2255.255.255.0
GETEWAY=192.168.XX.2
DNS=GETEWAY的地址

改完后重启

ping www.baidu.com
^C

宿主机和虚拟机都要能ping通

/etc/hostname  更改name
```

