---
layout: post
title: 甲骨文VPS开启root用户登录、打开防火墙和安装xui面板附上ssl和安装bbr加速
categories: 网络技术与技巧
banner:
  image: ./assets/images/banners/jgw.jpg
  opacity: 0.618
  background: "#000"
  height: "50vh"
  min_height: "50vh"
  heading_style: "font-size: 2.45em; font-weight: bold; "
  subheading_style: "color: gold"
sitemap: true
tags: [甲骨文VPS]
---

#### 甲骨文VPS开启root用户登录

SSH连接上甲骨文VPS

Centos的用户名为``opc``,Ubuntu的用户名为``ubuntu``

输入下面的脚本回车切换root用户

```zsh
sudo -i
```

切换为root用户后输入下面的命令修改root密码登录(下面中文换成你的密码)

```zsh
echo root:你设置的密码 |sudo chpasswd root
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
sudo service sshd restart
```

所有命令执行完成后就可以通过root用户登录甲骨文vps了

#### 甲骨文关闭防火墙-root用户

##### centos系统
```zsh
#停止firewall
systemctl stop firewalld.service
#禁止firewall开机启动
systemctl disable firewalld.service
#关闭iptables
service iptables stop
#去掉iptables开机启动
systemctl disable firewalld</code>
```

##### ubuntu系统
```zsh
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -F
```

#### 甲骨文vps安装x-ui

##### 安装更新环境
```zsh
#Debian/Ubuntu系统执行以下命令
apt update -y && apt install -y curl && apt install -y socat
#CentOS系统执行以下命令
yum update -y && yum update -y && yum install -y socat
```

##### 执行以下命令安装或更新x-ui
```zsh
bash &lt;(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```
安装完成后就可以输入ip:54321访问x-ui面板了,默认账号密码为admin,admin

#### 甲骨文申请SSL(请先将域名解析到vps的ip地址)

##### 运行Acme脚本
```zsh
curl https://get.acme.sh | sh
```

##### 申请证书及密钥（将下面的命令中的中文替换成你的域名，下面的xxxx@gmail.com可以换成你的邮箱也可以不用换）
```zsh
~/.acme.sh/acme.sh --register-account -m xxxx@gmail.com
~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone
```

##### 下载证书和密钥（将下面的命令中的中文换成你的域名,证书路径为/root/cert.crt,密钥路径为/root/private.key）
```zsh
~/.acme.sh/acme.sh --installcert -d 你的域名 --key-file /root/private.key --fullchain-file /root/cert.crt
```
证书下载好后可以在x-ui后台加上证书和密钥，然后通过域名访问的就可以使用ssl了

#### 甲骨文vps安装BBR加速
执行下面的命令，然后根据自己的选择安装，建议不要安装BBRPlus,可能会被封号
```zsh
wget -O tcpx.sh "https://git.io/JYxKU" &amp;&amp; chmod +x tcpx.sh &amp;&amp; ./tcpx.sh
```

```zsh
shutdown -r now
```