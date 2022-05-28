---
layout: post
title: 利用 SMB 协议进行 Time Machine 备份
categories: 网络技术与技巧
banner:
  image: ./assets/images/banners/macos-big-sur-system-prefs-tm.jpg
  opacity: 0.618
  background: "#000"
  height: "50vh"
  min_height: "50vh"
  heading_style: "font-size: 2.25em; font-weight: bold; "
  subheading_style: "color: gold"
tags: [SMB]    
---

### 前言
>macOS 为用户提供了便捷的系统备份功能：Time Machine 
一般而言，Time Machine 需要你连接一块硬盘到你的 Mac 上才能够启动。当然，你可以通过「有线连接」和「无线连接」的方式进行备份。本文将介绍除了使用 NAS 以外，你还可以在任何能够使用 SMB 协议的设备上创建你的「时间机器」。

> 首先，SMB 协议是一种能够将本机电脑上的文件夹分享到局域网内其他设备上的一种协议。你可以简单的理解为是一种文件共享的协议，并且这个协议广泛的使用于多种设备中，常见的桌面端操作系统（Windows、macOS、Linux）都能使用这个协议。我们要做的就是通过这个协议，将主机上的某个文件共享到你的 Mac 上，然后在那上面创建备份。所以，我们需要的具体步骤就是：

* 通过 SMB 分享一个文件夹；
* 在 Mac 上加载这个文件夹；
* 利用这个文件夹创建备份。

## 一、通过 SMB 分享一个文件夹

  

这一步，我们需要做的事，具体而言就是：

* 开启 SMB 服务；
* 配置一个文件夹进行共享；

> 所以，正如标题里写的，无论是树莓派这种 Linux 设备，还是 Windows 设备，你都可以开启 SMB 服务，进行局域网内的文件的共享。所以，如果你有一台 Linux 设备，你可以参考下面的树莓派的步骤，如果你有一台 Windows 设备，可以参考 Windows 的步骤。  

### 树莓派上开启 SMB 服务


首先，更新源：

```bash
sudo apt-get update
```

第二步，安装 samba 服务：

```bash
sudo apt-get install samba samba-common-bin
```

第三步，修改 SMB 的配置，这里使用 vim 进行编辑：

```bash
sudo vim /etc/samba/smb.conf
```

![](https://cdn.sspai.com/2019/11/23/7b9395b2e9eb4aabfb47c5459f45bd6c.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

配置内是有内容的哦

  

在配置文件的最后添加：

```yaml
[pi]

    path = /home/pi/

    valid users = pi

    browseable = Yes

    writeable = Yes

    writelist = pi

    create mask = 0777

    directory mask = 0777
```

保存退出后，重启一下 samba 服务

```bash
sudo /etc/init.d/samba restart
```

最后一步，就是添加 `pi` 用户为 `Samba`用户，这一步，会让你设置共享时的密码。

```bash
sudo smbpasswd -a pi
```

### WINDOWS 上开启 SMB 服务

  

Windows 上做 Smb 共享会方便很多，首先在一个磁盘空间比较富裕的地方，创建一个文件夹，然后右键，属性，打开「共享」栏：

![](https://cdn.sspai.com/2019/11/23/23c0c28cb51880bef610ede08b1234d8.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

然后点击共享，弹出用户设置界面：  

![](https://cdn.sspai.com/2019/11/23/a2cfa5b03109b2b77aa9050f562bcfab.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

设置共享的账户，以及权限设置为「读和写」，一般而言推荐在这里新建一个专门的共享账户，账户和密码就是届时需要在mac上输入的账户和密码：  

![](https://cdn.sspai.com/2019/11/23/ce8d4daeb33afde744e01c881e84111c.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

账户设置完成后，点击「共享」即可：  

![](https://cdn.sspai.com/2019/11/23/6f889deb4625822687e41e133c8b42a0.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

点击完成，这个文件就已经能够在局域网访问了。这里做个简单的提醒，部分Windows设备的防火墙设置，会禁用共享，可以先通过关闭防火墙的方式来排除是不是防火墙的问题，再通过对应规则的设置，重新开启防火墙即可。

## 二、在 Mac 上加载这个文件夹

  

这个时候，打开你的 finder，应该能够在「位置这一栏」下看到树莓派，或者你的 Windows 设备的名字了。点击后，就能看到你共享的文件夹了。

![](https://cdn.sspai.com/2019/11/23/ac1131d18f435f660c6fd4fbdb745812.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

如果没有看到，那么通过右键 finder 图标，点击「连接服务器」，输入：`smb://设备的IP地址/共享的文件夹名称` 的方式连接，在输入账号密码后，也能够连接上这个文件夹。正确连接后，就说明其他设备上的硬盘，已经能够为你的 Mac 所用了。

接下来我们就要进行最后一个步骤，创建一个「时间机器」了！

## 三、 利用这个文件夹创建备份

当你兴奋的打开你的 Time Machine 设置，点击「选择备份磁盘」时，看到却是：

![](https://cdn.sspai.com/2019/11/23/1e226958579b11834899c57dea4eb640.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

_是的，并没有你想要的那个文件夹_

  

接下来，我们要做的，其实是创建一个磁盘镜像文件，然后将这个磁盘镜像文件挂载到你的 Mac 上，作为一个「虚拟硬盘」，然后利用这个「虚拟硬盘」进行备份。具体的：

### （一） 创建一个空白映像：

  

打开「磁盘工具」，选择菜单栏中的 「新建映像」，选择「空白映像…」，然后如图所示，填入信息：

![](https://cdn.sspai.com/2019/11/23/a1423b8bf9d17375318cce2283a051fc.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

其中「大小」可以根据你实际需求来填写1 。

### （二） 将此这个空白映像拷贝到你的 SMB 共享文件夹中：

  

在 finder 中先推出这个磁盘（他现在是在你保存的位置上，如果你的设置如上图，那么这个磁盘就是在桌面），然后在保存的位置中，将这个磁盘文件拖入 SMB 共享文件夹的对应位置：

![](https://cdn.sspai.com/2019/11/23/3d74c204143d6e2bede0f8f9684cd1ed.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

  

### （三） 挂载这个磁盘

双击在 SMB 共享文件夹中的这个映像文件，然后他就会挂在在你的 Mac 上：

![](https://cdn.sspai.com/2019/11/23/7efcb6b7ab734d30c9f38b0f2165452f.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

最后，通过 terminal 将这个磁盘设置为 TimeMachine 的备份磁盘：

```bash
sudo tmutil setdestination /Volumes/TimeMachine
```

这里的 `/Volumes/TimeMachine` 就是这个磁盘的挂载点，一般而言就是 `/Volumes/` + 磁盘的名称，如果你不是很确定，可以在磁盘工具中，选择这个磁盘，点击右键，选择「显示简介」，看到挂载信息：

![](https://cdn.sspai.com/2019/11/23/686bfb6c3be4bdcd3bbc0d883dbfb8dc.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

输入完命令后，再输入你的Mac密码，即可成功挂载。当你再次打开 TimeMachine 时，已经可以开始备份了。  

![](https://cdn.sspai.com/2019/11/23/236ed5d522549b601045d81b988ca7c4.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

  

