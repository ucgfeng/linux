```
https://wili.archlinux.org/title/Installation_guide
dhcpcd  联网
ping www.baidu.com
timedatectl set-ntp true  更新系统时间
生成快照
fdisk -l 硬盘分区
看显示的盘
fdisk /dev/sda  创建分区  
n  一直回车
p 查看
w 保存
mkfs.ext4 /dev/sda  格式化分区
mount /dev/sda1 /mnt 挂载分区

选择镜像源
vim /etc/pacman.d/mirrorlist
把中文的源放在第一
dd 剪切
p  粘贴
:wq
自动生成
reflector --country China --age 24 --sort rate --protocol https --save /etc/pacman.d/mirrorlist
reflector --c China  --sort rate  --save /etc/pacman.d/mirrorlist

物理机镜像生成后，执行
pacman -Syy
pacman -S archlinux-keyring

安装基础的linux包
pacstrap /mnt base base-devel linux linux-firmware dhcpcd
配置fstab
genfstab -L /mnt >> /mnt/etc/fstab
genfstab -U /mnt >> /mnt/etc/fstab
查看有没有成功
cat /mnt/etc/fstab
更换root时区
arch-chroot /mnt

设置时区
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

hwclock --systohc

安装软件
pacman -S vim dialog wpa_supplicant ntfs-3g networkmanager netctl

设置语言
vim /etc/locale.gen
把想要设置的语言注释放开
zh_CN.UTF-8 UTF-8
zh_HK.UTF-8 UTF-8
zh_TW.UTF-8 UTF-8
en_US.UTF-8 UTF-8

:wq

locale-gen
编辑文件
vim /etc/locale.conf
把语言设置成英语
i进入插入模式
Lang=en_US.UTF-8
ESC 
:wq
设置主机名字
vim /etc/hostname
i进入插入模式
输入自己想要的名字esc
:wq
编辑hosts
vim /etc/hosts
i进入插入模式
127.0.0.1 localhost
::1 localhost
127.0.1.1 主机名字.localdomain [主机名字]
esc
:wq

设置root 密码
passwd

cpu是inter
pacman -S intel-ucode

pacman -S os-prober ntfs-3g

pacman -S grub efibootmgr

grub-install --target=i386-pc /dev/sda
物理机  
grub-install --target=x86_64-efi --efi-directory=/boot --bootloadet-id=GRUB


grub-mkconfig -o /boot/grub/grub.cfg
物理机执行这个命令之前，
去/etc/defalut/grub文件中
把GRUB_DISABLE_OS_PROBER=false的注释去掉
update-grub


vim /boot/grub/grub.cfg
:q
exit
umount /mnt 取消挂载
reboot
装好了  快照

root
密码

安装kde
dhcpcd

ping www.baidu.com
申请交换文件
dd if=/dev/zero of=/swapfile bs=1M count=512 status=progress

chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile

vim /etc/fstab

i进入插入模式

/swapfile none swap defaults 0 0
esc
:wq

useradd -m -G wheel [username]全都是小写

passwd [username]

配置sudo
pacman -S sudo

ln -s /usr/bin/vim /usr/bin/vi

visudo

:/wheel
取消注释

:wq

su [username]
切换用户

sudo vim /etc/pacman.conf
:/multilib
取消注释
i进入插入模式
[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch
esc
:wq
sudo pacman -Syy
sudo pacman -S efibootmgr os-prober

sudo pacman -S archlinuxcn-keyring

安装驱动
```

![1656941506879](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656941506879.png)

```
安装显卡 驱动和openGL
sudo pacman -S nvidia nvidia-utils
sudo pacman -S xorg plasma kde-applications sddm network-manager-applet

sudo systemctl enable sddm
sudo systemctl disable netctl
sudo systemctl enable NetworkManager

exit
reboot
安装好kde
```

```
登录进
进终端
sudo dhcpcd
ping www.baidu.com

改分辨率
sudo pacman -S virtualbox-guest-utils
sudo systemctl enable vboxservice.service

reboot

终端
安装中文字体
sudo pacman -S wqy-microhei wqy-microhei-lite wqy-bitmapfont wqy-zenhei ttf-arphic-ukai ttf-arphic-uming adobe-source-han-sans-cn-fonts noto-fonts-cjk

安装
sudo pacman -S git

git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si

sudo vim /etc/loacle.conf

i
LANG=zh_CN.UTF-8
:wq

reboot
换源网址
https://www.csdn.net/tags/MtTaMg0sMTM5NTk5LWJsb2cO0O0O.html

设置中添加语言简体中文
搜索language
添加简体中文，放第一位
重启 reboot

pacman -S firefox ark gwenview git wget packagekit-qt5 packagekit docker appstream-qt appstream man neofetch net-tools networkmanager openssh

只适用于vmware虚拟机
pacman -S gtkmm gtk2 gtkmm3 open-vm-tools xf86-input-vmmouse xf86-video-vmware

systemctl enable NetworkManager sddm vmtoolsd sshd
systemctl enable sddm.service NetworkManager sshd.service vmtoolsd
vim /etc/mkinitcpio.conf
MODULES=(vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx)
esc
:wq
mkinitcpio -p linux
只适用于vmware虚拟机到这里结束

pacman -S neofetch

neofetch

pacman -Syy

之前添加archlinuxcn源的时候
网站会提示安装 archlinuxcn-keyring
pacman -S archlinuxcn-keyring如果报错，用root用户执行以下命令
rm -rf /etc/pacman.d/gnupg
pacman-key --init
pacman-key --populate archlinux
pacman-key --populate archlinuxcn


pacman -S yay

安装网易云
yay -S netease-cloud-music


安装中文输入法
pacman -S ibus ibus-table ibus-table-chinese

卸载
root用户下
rm -rf /opt/apps
rm -rf /usr/share/applications/com.qq.office.deepin.desktop




```

- 另一个安装

```
archlinux官网  archlinux.org
最新的镜像2022-4-1
内核5.18.7 

中科大的ustc
archlinux-2022.07.01-x86_64.iso
最后一个是校验码
校验
windows10 微软商店下载windows terminal
get-filehash 路径\文件名  查看sha256校验码一致后开始安装 


虚拟机linux5 
编辑设置为uefi

```

![1656942807895](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656942807895.png)

```
60G
8G
编辑

设置大字体
setfont /usr/share/kbd/consolefonts/sun12*22.psfu.gz

停止reflector服务
禁止自动更新服务器列表
systemctl stop reflector.service

插入无线网卡
ip link
无线网络连接
iwctl
device list 进入命令行
station wlan0 scan  列出设备名 比如wlan0
station wlan0 get-networks   列出网张力
station wlan0 connect  连接网络名字  输入密码
exit或quit


ping www.baidu.com

同步网络时间
timedatectl set-ntp true
修改源，把中国的服务器地址排在前列

vim /etc/pacman.d/mirrorlist

ustc
:wq

pacman -Syyu

fdisk -l

fdisk /dev/sda

```

![1656943332110](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656943332110.png)

```
cfdisk /dev/sda


```

![1656943545613](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656943545613.png)

```
生成fstab
genfstab -U /mnt >> /mnt/etc/fstab
查看有没有成功
cat /mnt/etc/fstab
更换root时区
arch-chroot /mnt
设置主机名字
vim /etc/hostname
i进入插入模式
输入自己想要的名字esc
:wq
编辑hosts
vim /etc/hosts
i进入插入模式
127.0.0.1 localhost
::1 localhost
127.0.1.1 主机名字.localdomain [主机名字]
esc
:wq

设置语言为en_US.UTF-8 UTF-8

locale-gen

ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
设置硬件时间
hwclock --systohc
设置root 密码
passwd
编辑中国源
vim /etc/pacman.conf
[archlinuxcn]
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
Server = http://mirrors.163.com/archlinux-cn/$arch
:wq

pacman -Syyu

useradd -m -G wheel -s /bin/bash arch

安装cpu微码和引导软件
pacman -S amd-ucode grub efibootmgr os-prober


```

![1656944941278](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656944941278.png)

```
这里的安装软件包只适用于vmware虚拟机。实体机和其他虚拟机请匆安装
pacman -S gtkmm gtk2 gtkmm3 open-vm-tools xf86-input-vmmouse xf86-video-vmware

systemctl enable NetworkManger sddm vmtoolsd sshd

vim /etc/mkinitcpio.conf
MODULES=(vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx)

mkinitcpio -p linux使上面配置文件生效

exit

umount -R /mnt

reboot


pacman -S neofetch

neofetch


```

![1656945494827](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656945494827.png)

![1656945565072](C:\Users\Ucg\AppData\Roaming\Typora\typora-user-images\1656945565072.png)

```
ip a

或ifconfig

安装 net-tools才能使用 ifconfig

```
