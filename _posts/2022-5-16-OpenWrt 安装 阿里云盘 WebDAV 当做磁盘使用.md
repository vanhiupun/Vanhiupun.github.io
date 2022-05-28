---
layout: post
title: OpenWrt 安装 阿里云盘 WebDAV 当做磁盘使用
categories: 网络技术与技巧
banner:
  image: ./assets/images/banners/aliyundrive.png
  opacity: 0.618
  background: "#000"
  height: "50vh"
  min_height: "50vh"
  heading_style: "font-size: 2.45em; font-weight: bold; "
  subheading_style: "color: gold"
sitemap: true
tags: [阿里云盘, OpenWrt, WebDAV]
---

#### 前言
众所周知 OpenWrt 可以挂载 阿里云盘 WebDAV 服务，主要使用场景为配合支持 WebDAV 协议的客户端 App 如 Infuse、nPlayer 等实现在电视上直接观看云盘视频内容，或挂载电脑当做本地支持使用，支持上传文件，但受限于 WebDAV 协议不支持文件秒传。由于不限速，那么我们就挂载到电脑上当做本地磁盘使用

**友情提示：不要存在暴露、色情、违法软件到网盘，因阿里云盘有内容风控识别，所以会导致封号，请注意！！！**

### 插件安装
#### openwrt
[GitHub Releases](https://github.com/messense/aliyundrive-webdav/releases) 中有预编译的 ipk 文件， 目前提供了 `aarch64/arm/mipsel/x86_64/i686` 等架构的版本，可以下载后使用 opkg 安装，以 nanopi r4s 为例：
```
wget https://github.com/messense/aliyundrive-webdav/releases/download/v1.3.2/aliyundrive-webdav_1.3.2-1_aarch64_generic.ipk
wget https://github.com/messense/aliyundrive-webdav/releases/download/v1.3.2/luci-app-aliyundrive-webdav_1.3.2_all.ipk
wget https://github.com/messense/aliyundrive-webdav/releases/download/v1.3.2/luci-i18n-aliyundrive-webdav-zh-cn_1.3.2-1_all.ipk
opkg install aliyundrive-webdav_1.3.2-1_aarch64_generic.ipk
opkg install luci-app-aliyundrive-webdav_1.3.2_all.ipk
opkg install luci-i18n-aliyundrive-webdav-zh-cn_1.3.2-1_all.ipk
```

>Tips: 不清楚 CPU 架构类型可通过运行 opkg print-architecture 命令查询。

>将上述代码第1行和第4行的文件名更换同架构类型的文件名即可

![](/assets/images/aliyundrive/openwrt.png)

#### Koolshare 梅林固件
GitHub Releases 中有预编译包 `aliyundrivewebdav-merlin-arm*.tar.gz`， 目前提供了旧的 arm380 和兼容 arm384/386 固件的版本，可在下载后在软件中心离线安装。
![](/assets/images/aliyundrive/merlin.png)

### 获取 refresh_token
- 自动获取: 登录[阿里云盘](https://www.aliyundrive.com/drive/)后，控制台粘贴
`JSON.parse(localStorage.token).refresh_token`
![](/assets/images/aliyundrive/json.png)

- 手动获取: 登录[阿里云盘](https://www.aliyundrive.com/drive/)后，可以在`开发者工具 -> Application -> Local Storage` 中的 `token` 字段中找到。

注意：不是复制整段 JSON 值，而是 JSON 里 `refresh_token` 字段的值，如下图所示红色部分：
![](/assets/images/aliyundrive/refresh_token.png)

### 设置插件
进入 OpenWrt 管理后台，
- 找到 阿里云盘 WebDAV 管理页，进入后不着急勾选启用，
- 先填写上面获取的 Refresh Token 密钥，
> 云盘根目录 / 就是访问网盘下所有资源，如果你想只访问某个文件夹，那么就设置为 /文件名，比如：/电影，演示默认设置 / 。
- 主机地址填写你 OpenWrt 的地址，比如：192.168.2.1，端口设置不要默认 8080，因 OpenWrt 很多插件都是用了 8080 端口会导致冲突，而出现阿里云盘无法使用，如下图：
![](/assets/images/aliyundrive/webdav.png)
  
- 如果不开启 阿里云相册与云盘服务 domainId，那么 TLS 证书文件路径 和 TLS 私钥文件路径 就无需设置，用户名 和 密码 内网使用可以不设置，其他默认，删除文件不放入回收站可以根据自己需求进行勾选，然后选择启用，保存&设置，通过`192.168.2.1:8080`访问，如果访问成功，那么就设置成功了，如下图
![](/assets/images/aliyundrive/web.png)

如果无法访问，那么更换端口尝试访问，更换端口后还是无法访问，可以查看日志确认错误进行解决，如不会解决，留言给我，我看到会回复给你解决方法。

### 使用Infuse连接阿里云盘的Webdav服务

进入Infuse-新增文件来源-添加webdav 如下图
![](/assets/images/aliyundrive/infuse.png)

#### 连接成功
![](/assets/images/aliyundrive/j1.png)
![](/assets/images/aliyundrive/j2.png)