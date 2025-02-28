---
title: Arch Linux 安装记录
tags: [Linux]
categories: [应用系统]
index_img: /img/archlinux.jpg
date: 2021-08-24 10:00:00
---

本人安装 Arch Linux 时的参考及步骤

主要包含：启动盘制作到磁盘分区到最后驱动安装和最后图形界面安装（针对 Windows 转 Linux，UEFI 方式）

<!--more-->

<a href="https://smms.app/image/rIHG7V4ZFjv9aPD" target="_blank"><img src="https://s2.loli.net/2022/12/30/rIHG7V4ZFjv9aPD.png" /></a>

## 参考

因为是按着步骤装的，所以先把参考搬出来

> [【超详细教程】Arch Linux真机安装教程 - 从命令行到图形界面 | 2021年3月](https://www.bilibili.com/video/BV1Av411a7xe?share_source=copy_web)

## 装前须知

这个可能会成为一个坑，特别是不太了解操作系统或者相关东西的人（比如我），容易完了留麻烦，所以先说

怎么回事呢，是这样的，我电脑的储存空间一直是我的心头病，我只有一个 256G 的 SSD，在 Windows 下划分成了 C 盘和 D 盘俩分区，然后一直把 100G 的 C 盘作为系统盘，每次重装系统都只会影响到这个盘的文件，而我的 D 盘得以保全。所以我准备这次也对我的 C 盘动手，想着这样能保全我 D 盘的重要文件。

但是装系统的时候出现了两个问题：

一是原 Windows 的磁盘分区比较神奇，除了 C D 两盘的区域外还有几个分区，具体用处我不是很清楚，正好呢，我格式化除 D 盘的分区时发现，其他分区居然不是连续的，在物理上，D 盘扇叶后，还有 901.3MB 的空间，这可能会影响到你的磁盘分区和挂载

二是，Windows 支持的磁盘格式一般是 FAT32 或者 NTFS，然而 Linux 不支持 NTFS，这会导致什么呢：

<img src="https://s2.loli.net/2022/12/30/Sdv2kXG69Nr5E8q.png">

那有没有解决办法呢？目前我能找到的都需要格式化x，以宿舍不到 5MB 的网速把我这 100 来 G 的文件上传格式化后又下载下来可能不是一两天能解决的。

所以装 Linux 前请一定注意以上问题。

### 我的硬件

<a href="https://smms.app/image/12CauNSfHW6iDvQ" target="_blank"><img src="https://s2.loli.net/2022/12/30/12CauNSfHW6iDvQ.png" /></a>

常用操作：Ctrl + L 清屏，很好用

## 下镜像

> https://archlinux.org/download/

- 推荐

<a href="https://smms.app/image/mFKZ6fPeWAo48wl" target="_blank"><img src="https://s2.loli.net/2022/12/30/mFKZ6fPeWAo48wl.png" /></a>

- 也可前往其他中国镜像地址下载

<a href="https://smms.app/image/fsz3FpBRJoqSM7X" target="_blank"><img src="https://s2.loli.net/2022/12/30/fsz3FpBRJoqSM7X.png" /></a>

## 制作启动盘

有推荐使用 Rufus 我用了下，发现做出来的启动盘有点问题，我的电脑找不着，所以用的视频里提到的工具：Etcher

工具使用比较简单，只需要注意推荐 8G 以上的 U 盘

找到对应 U 盘（一定看清别搞错了）和镜像文件（.iso）然后一键完成

## 进入镜像

打开百度，搜索自己机型对应进入 BIOS 的键（我的是 F2），关机，进入 BIOS

Boot -> Security Boot 更改为 Disabled

打开百度，搜索自己机型对应进入启动项的键（我的是 F10），关机，进入启动项，找到 U 盘，进入镜像

## 连网

```bash
$ iwctl
```

进入 iwd

```bash
$ device list
```

查看无线网卡，比如 wlan0

```bash
$ station wlan0 scan
```

进行扫描

```bash
$ station wlan0 get-networks
```

查看扫描到的网络

```bash
$ station wlan0 connect [Network name]
```

连接网络，根据提示输入密码（如果需要）

Ctl+C 或者输入 exit 退出 iwd

退出 iwd 后可使用 ping 来检查有无网络

## 验证启动模式

```bash
$ ls /sys/firmware/efi/efivars/
```
视频里讲说有很多如果里面有很多东西，那么说明有 UEFI，未考证准确性

## 同步时间

```bash
$ timedatectl set-ntp true
```

可以通过以下方式查看

```bash
$ timedatectl status
```

## 磁盘分区

```bash
$ lsblk
```

列出块设备信息

我就一个 256G 的 SSD，lsblk下显示的 nvme0n1（nvme应该是某接口规范的缩写）

印象里 Windows 给分了 6 个区，我的 nvme0n1p2 是 C 盘，nvme0n1p3 是 D 盘

所以要将除了 nvme0n1p3 外的都给清了，连续的分区会自动合并

我们使用 gdisk 命令，比如：

```bash
$ gdisk /dev/nvme0n1p1
Command(? for help): x
Expert command(? for help): z
(Y/N): y
(Y/N): y
```

当然，如果你不像我只有一个固态，而是有很多，而且你拿来做系统盘的这个盘又没有存重要文件或者已经备份，那么你完全可以直接清顶层（比如 nvme0n1）

为了方便，以下以完全清除 nvme0n1 来进行

```bash
$ cgdisk /dev/nvme0n1
```

进入这个 cgdisk 分区工具（当然也有别的，只是觉得这个好理解）

### [ New ]

具体操作可参考[推荐视频](https://www.bilibili.com/video/BV1Av411a7xe?share_source=copy_web)，下表列出主要配置

<table>
<thead>
<tr>
<th>First sector</th>
<th>Size</th>
<th>Hex code</th>
<th>name</th>
</tr>
</thead>
<tbody><tr>
<td>default</td>
<td>一般300MiB(1024MiB)</td>
<td>ef00</td>
<td>boot</td>
</tr>
<tr>
<td>default</td>
<td>(4GiB)</td>
<td>8200</td>
<td>swap</td>
</tr>
<tr>
<td>default</td>
<td>(30GiB)</td>
<td>default</td>
<td>root</td>
</tr>
<tr>
<td>default</td>
<td>default</td>
<td>default</td>
<td>home</td>
</tr>
</tbody></table>

有几点说明：

1. 括号内为我的配置

2. boot（启动分区） 和 swap（交换分区）的 Hex code 一般来说应该是一样的，如果你不清楚，可以在填写时输入 L 回车查询

    <a href="https://smms.app/image/bjqLhdD3pkZmaBz" target="_blank"><img src="https://s2.loli.net/2022/12/30/bjqLhdD3pkZmaBz.png" /></a>

    + efi：查询 boot 的 Hex code
    + swap：查询 swap 的 Hex code

3. swap 的 Size 参考下表（我是 8G 内存，可以设 3 GiB，我凑个偶数）

    <a href="https://smms.app/image/hGam5qTlXQgJwEb" target="_blank"><img src="https://s2.loli.net/2022/12/30/hGam5qTlXQgJwEb.png" /></a>

    至于 swap 是干嘛的，其实就是拿来补你内存的，内存使用满了，可以拿一部分 swap 分区的内存来补

    > swap分区，即交换区，swap空间的作用可简单描述为：当系统的物理内存不够用的时候，就需要将物理内存中的一部分空间释放出来，以供当前运行的程序使用

4. 理论上 root 和 home 分区可以合为一个分区，这里为了方便管理，所以分成两个

5. 如果你装软件装的多，请一定给 root 分区多一点空间，这是血的教训，我这给的 30GiB 对我来说根本不够（推荐你翻个倍，或者你盘够大，给的更多也没关系，你可以把 root 看成 Windows 下的 C 盘，而且所有应用都装 C 盘下，home 就是 D 盘，放你个人文件的地方）

6. 再说一遍，**如果你装软件多，请一定给 root 多一点空间**

{% note primary %}
2022年12月30日注：一定一定多给点，我本以为之前给得够多了，但是发现其实并不够。其实在Linux下可能就自己下的什么视频啥的占了点home的空间，各种奇奇怪怪的软件下下来是放root里的，所以还是给多点吧。
{% endnote %}

### [ Write ]
yes

### [ Quit ]

## 磁盘挂载

挂载前要先对分好的分区**格式化**

假设 n1p1 是你的 boot，n1p2 是 swap，n1p3 是 root，n1p4 是 home

```bash
$ mkfs.fat -F32 /dev/nvme0n1p1
$ mkswap /dev/nvme0n1p2
$ swapon /dev/nvme0n1p2
$ mkfs.ext4 /dev/nvme0n1p3
$ mkfs.ext4 /dev/nvme0n1p4
```

挂载

```bash
$ mount /dev/nvme0n1p3 /mnt
$ mkdir /mnt/boot
$ mount /dev/nvme0n1p1 /mnt/boot
$ mkdir /mnt/home
$ mount /dev/nvme0n1p4 /mnt/home
```

如果你不准备将 root 和 home 分开，那么就没有最后两步

## 修改 pacman 镜像

文件编辑器可以选择 nano 或者 vim，看个人喜好，这里使用 vim

```bash
$ vim /etc/pacman.d/mirrorlist
```

该文件存放了 pacman 的镜像地址，pacman 使用镜像的方式是从上到下，所以有的教程会让你把中国镜剪切到最前，这里不这样做，用一个更好的方法

```bash
$ pacman -Sy
$ reflector --verbose --latest 15 --sort rate --save /etc/pacman.d/mirrorlist
```

pacman -Sy 先同步一下

reflector 是个同步脚本

> Reflector 是一个 Python 脚本；它可以从 Arch Linux Mirror Status 页面获取最新的镜像列表，然后筛选出最新的镜像并按速度排序，最后将结果写入到 /etc/pacman.d/mirrorlist 文件。

这里稍微解释一下各个参数的含义：

- `--verbose`：log 到终端
- `--latest 15`：最近 15 个
- `--sort rate`：按速率排序
- `--save /etc/pacman.d/mirrorlist`：保存到该文件
- 其实这里可以再加一个 `country China` 来选择中国源

## 安装系统及固件

```bash
$ pacstrap -i /mnt linux linux-headers linux-firmware base base-devel vim intel-ucode
```

说明：

- `vim` 也可换成 `nano` 或者一起装上
- `intel-ucode` 取决于你的处理器类型，如果你是 AMD，那么 `amd-ucode`

## 进入系统

```bash
$ genfstab -U -p /mnt >> /mnt/etc/fstab
$ arch-chroot /mnt
```

如果你发现终端行头变成了比如：`[root@archiso /]#`，那么说明你已经进入了系统

进入系统第一件事，同步一下

```bash
$ pacman -Syy
```

### 然后配置系统时区

```bash
$ ln -s /usr/share/zoneinfo/Asia/Shanghai > /etc/localtime
$ hwclock --systohc
```

### 然后语言配置

```bash
$ vim /etc/locale.gen
```

进入该文件后，将 `en_US.UTF-8 UTF-`8 和 `zh_CN.UTF-8 UTF-8` 前面的 `#` 删掉（取消注释）

`:wq`退出

```bash
$ locale-gen
$ echo LANG=en_US.UTF-8 > /etc/locale.conf
$ export LANG=en_US.UTF-8
```

网络配置

```bash
$ vim /etc/hostname
```

这里输入一个名字，按个人喜好，这里以 arch-name 为例

:wq 退出

```bash
$ vim /etc/hosts
```

写入以下内容：

```text
127.0.0.1    localhost
::1            localhost
127.0.1.1    arch-name.localdomain    arch-name
```

`:wq` 退出

### 然后添加用户

```bash
$ passwd
# 两次输入密码
$ useradd -m -g users -G wheel,storage,power -s /bin/bash archuser
$ passwd archuser
# 两次输入密码
```

这里的 `archuser` 是你的用户名，可以自行填写

### 修改 sudo 文件

```bash
$ EDITOR=vim visudo
```

去掉 `Uncomment to allow members of group wheel to execute any command` **下一行** `%wheel ALL=(ALL) ALL` 前面的 #

<a href="https://smms.app/image/9wDc51X6fYEAlvh" target="_blank"><img src="https://s2.loli.net/2022/12/30/9wDc51X6fYEAlvh.png" /></a>

再在文件最后添加 `Defaults rootpw`

`:wq` 退出

## 安装启动器

```bash
$ bootctl install
$ vim /boot/loader/entries/arch.conf
```

写入以下内容

```bash
title My Arch Linux
linux /vmlinuz-linux
initrd /intel-ucode.img
initrd /initramfs-linux.img
```

第二行如果使用长期支持内核则写 `linux /vmlinuz-linux-lts`

`:wq` 退出

```bash
$ echo "options root=PARTUUID=$(blkid -s PARTUUID -o value /dev/nvme0n1p3) rw" >> /boot/loader/entries/arch.conf
```

上面这个语句会帮你补充 arch.conf 内的最后一行

## 开启 32 位支持（可选）

如果你没有 32 位应用支持需求，则直接下一步（我没有）

{% note primary %}
2022年12月30日注：现在看来，还是有一些需求的，但是到时候开也没问题
{% endnote %}

```bash
$ systemctl enable fstrim.timer
$ vim /etc/pacman.conf
```

去掉 `[multilib]` 和 `Include = /etc/pacman.d/mirrorlist` 前的 `#`

`:wq` 退出

然后同步一下

```bash
$ pacman -Syy
```

## 安装各种工具、驱动

### 网络、声音、蓝牙、文件后台

```bash
$ pacman -S networkmanager network-manager-applet dialog wpa_supplicant dhcpcd
```

启用

```bash
$ systemctl enable NetworkManager
```

继续

```bash
$ pacman -S mtools dosfstools  bluez bluez-utils cups xdg-utils xdg-user-dirs alsa-utils pulseaudio pulseaudio-bluetooth reflector openssh
```

### 显卡

这里以我的配置来（不开启 32 位支持，intel，NVIDIA），32 位及 AMD 相关请参考[推荐视频](https://www.bilibili.com/video/BV1Av411a7xe?share_source=copy_web)

```bash
$ pacman -S xf86-video-intel mesa libva-mesa-driver mesa-vdpau nvidia dkms libglvnd nvidia-utils opencl-nvidia nvidia-settings
```

### 显卡驱动配置

```bash
$ vim /etc/mkinitcpio.conf
```

将 `MODULES=()` 修改为 `MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)`，顺序不能错

`:wq` 退出

```bash
$ mkdir /etc/pacman.d/hooks
$ vim /etc/pacman.d/hooks/nvidia.hook
```

输入以下内容

```bash
[Trigger]
Operation=Install
Operation=Upgrade
Operation=Remove
Type=Package
Target=nvidia
Target=linux

[Action]
Depends=mkinitcpio
When=PostTransaction
Exec=/usr/bin/mkinitcpio -P
```

`:wq` 退出

```bash
$ vim /boot/loader/entries/arch.conf
```

在 `options` 这一行的**后面**添加：`nvidia-drm.modeset=1`

如果你是 AMD，那么添加 `amdgpu.dmp=0 amdgpu.noretry=0`

`:wq` 退出

## 安装图形界面（以 KDE 为例）

### 装 xorg 窗口系统

```bash
$ pacman -S xorg konsole
```

视频里推荐装个 `xterm` 然后进了图形界面后又用 `xterm` 装了 `konsole`，那为什么不直接在这装 `konsole` 呢

（一定要装一个终端，不论你是装 `xterm` 还是 `konsole`，不然进去发现没有，又得插 U 盘挂载进系统然后装，很麻烦）

### 装 KDE

```bash
$ pacman -S sddm plasma
```

## 重启

```bash
$ exit
```

退出系统

```bash
$ umount -R /mnt
```

取消挂载

```bash
$ reboot
```

重启

输入密码，你就进入图形界面的桌面了

至此，装系统到图形界面应该就算结束了，但为了接下来的使用，装一些基本的软件

## 装基本软件

打开 konsole

```bash
$ sudo pacman -S neofetch dolphin firefox ark p7zip git wget kate bashtop
```

`neofetch` 就是最开始我看系统和硬件信息的工具

`dolphin` 是文件管理器

<a href="https://smms.app/image/nw2oZm1E8VvAayz" target="_blank"><img src="https://s2.loli.net/2022/12/30/nw2oZm1E8VvAayz.png" /></a>

`firefox` 在 Linux 下支持的比较好

`ark` 和 `p7zip` 是压缩管理器

`git` 和 `wget` 广为流传

`kate` 是文件编辑器

<a href="https://smms.app/image/7nOzy4YueTBVabo" target="_blank"><img src="https://s2.loli.net/2022/12/30/7nOzy4YueTBVabo.png" /></a>

`bashtop` 是终端进程管理器

<a href="https://smms.app/image/gXJ5SPp9tW2Nmoi" target="_blank"><img src="https://s2.loli.net/2022/12/30/gXJ5SPp9tW2Nmoi.png" /></a>

## 后话

接下来规划出一期 Linux 美化，一期 Linux 常用软件推荐。