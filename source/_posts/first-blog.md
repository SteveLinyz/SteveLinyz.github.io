---
title: Linux + Hexo + Github 搭建个人博客
date: 2021.6.27
cover: https://images.pexels.com/photos/691668/pexels-photo-691668.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
top_img: 'linear-gradient(20deg, #0062be, #925696, #cc426e, #fb0347)'

---



## 1.  安装Git

> [root@ ~]# yum install -y git  

## 2.  安装node.js

进入官网：http://nodejs.cn/download/ 

注意：一定要下载**最新版**

### 2.1 二进制包下载：

> [root@iZuf68enovvnl1qpz1bvdoZ software]# pwd
> /app/software
>
> [root@steve]# wget https://npm.taobao.org/mirrors/node/v16.4.0/node-v16.4.0-linux-x64.tar.xz

### 2.2 下载到software目录后解压：

> [root@iZuf68enovvnl1qpz1bvdoZ software]# tar xf node-v16.4.0-linux-x64.tar.xz 

### 2.3 添加node的环境变量，在最后一行加入PATH

> vi /etc/profile #最后一行加入PATH 
>
> export PATH=$PATH:/home/www/node-v16.4.0-linux-x64/bin

### 2.4 使/etc/profile里的配置立即生效

> source /etc/profile

### 2.5 查看版本信息

> [root@iZuf68enovvnl1qpz1bvdoZ bin]# ./node -v
> v16.4.0

### 2.6 创建软连接

> [root@uf68enovvnl1qpz1bvdoZ bin]# ln -s /app/software/node-v16.4.0-linux-x64/bin/node /usr/local/bin/node
> [root@uf68enovvnl1qpz1bvdoZ bin]# ln -s /app/software/node-v16.4.0-linux-x64/bin/npm /usr/local/bin/npm

使node 和 npm可以使用。

## 3.  hexo部署

### 3.1 安装hexo

> [root@iZuf68enovvnl1qpz1bvdoZ bin]# npm install hexo-cli -g

### 3.2 将 hexo 命令添加到全局，采用软连接方式

``` bash
[root@iZuf68enovvnl1qpz1bvdoZ bin]# ln -s /app/software/node-v16.4.0-linux-x64/lib/node_modules/hexo-cli/bin/hexo /usr/local/bin/hexo
```

### 3.3 init hexo

创建一个hexo目录，并初始化。

```bash 
[root@iZuf68enovvnl1qpz1bvdoZ software]# mkdir hexo
[root@iZuf68enovvnl1qpz1bvdoZ software]# cd hexo
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# hexo init
```

### 3.4 启动测试环境

```bash
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# hexo g
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# hexo s
NFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

### 3.5 遗留问题

启动后显示Hexo运行在http://localhost:4000中，但Windows下无法访问。

## 4. 新建一篇博客

## 5. 部署到github

### 5.1 new一个仓库

<img src="https://raw.githubusercontent.com/SteveLinyz/image-host-for-typora/master/img/20210627022222.png" alt="image-20210627022222438" style="zoom:80%;" />

两个名字需要一样，注意结尾名称。

### 5.2 开启Github pages

进入仓库 - settings - page ，已默认开启Github pages，选择一个主题，即可访问

> SteveLinyz.github.io

### 5.3 在github上部署SSH keys信息

为了能将个人博客服务器上的博客数据推送到 GitHub，达到数据永久保存效果，我们需要把博客服务器的 SSH keys 信息在 GitHub 上添加信任。

**首先，我们要在本地服务器上创建SSH-key信息:输入命令后一直回车。**

```bash
[root@iZuf68enovvnl1qpz1bvdoZ /]# ssh-keygen -t rsassh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:4SzlGFviy1NdMzshsnW9z7WXntRSEJe5k3Ipyd3Ycgk root@iZuf68enovvnl1qpz1bvdoZ
The key's randomart image is:
+---[RSA 2048]----+
|              . +|
|             E = |
|      o = o B *o*|
|     . @ * + Xo@+|
|      = S . o =o+|
|     . +     . +=|
|      +       .+=|
|       .      o.o|
|               o |
+----[SHA256]-----+
```

**之后查看SSH：**

```bash
[root@iZuf68enovvnl1qpz1bvdoZ ~]# cd .ssh/
[root@iZuf68enovvnl1qpz1bvdoZ .ssh]# cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCWK+X3w3ODYagL6FyhNREZWcWZY/3Y709GKYXVFZrXTsJx/zDVOtKKQW97WIX8Nw4/36jo6AY9jWKWwEyjiuTBQILmq9imowBHETVS5ETqbZlINY2oUmyfY9IVlBAJ/paERzQ2kik/8Fi5RralQddAQV9k3/L/tTHY1CPxS+W6zFksfH2kgvpDGZBK5PvCjKHxFaYnN5wBjfGt5HIbVoeHFlg8XMNCbwPBEPweDUWsAncfA4cJ+1doNdah0jcQM3LwVIsel2itEKnwq8WuHkR+DEGpRxA1Xon+tWNHvY9tnFWZf3/8jWY36W4EK5Rwqw2aELeVGvKnS4ybH7EPk7tP root@iZuf68enovvnl1qpz1bvdoZ
```

**添加SSH key到github上：**

Settings - SSH and GPG keys - new SSH key

<img src="https://raw.githubusercontent.com/SteveLinyz/image-host-for-typora/master/img/20210627022915.png" alt="image-20210627022915182" style="zoom:80%;" />

**连接测试：**

```bash
[root@iZuf68enovvnl1qpz1bvdoZ ~]# ssh -T git@github.com
The authenticity of host 'github.com (13.250.177.223)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
RSA key fingerprint is MD5:16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,13.250.177.223' (RSA) to the list of known hosts.
Hi SteveLinyz! You've successfully authenticated, but GitHub does not provide shell access.
```

这样就连接成功了。

**设置账号信息：**

```bahs
[root@iZuf68enovvnl1qpz1bvdoZ /]# cd app/software/hexo
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# git config --global user.name "SteveLinyz"
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# git config --global user.email "1143771616@qq.com"
```

这里的用户名和邮箱，应该和Github上的账户邮箱保持一致，防止之后同步的不一致。

### 5.4 Hexo部署到Github Pages

#### 5.4.1 _config.yml 配置修改

```bash
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# vim _config.yml
………………
# Deployment
## Docs: https://hexo.io/docs/deployment.html  # 修改或添加如下信息
deploy:
  type: git
  repo: git@github.com:SteveLinyz/stevelinyz.github.io.git
  branch: main
```

注意，github改版后默认分支都为main。

#### 5.4.2 安装扩展

部署到GitHub之前，还需要安装如下扩展：

```bash
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# npm install hexo-deployer-git --save
```

#### 5.4.3 部署到Github

```bahs
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# hexo d -g 
# 部署前，先生成静态文件  -g 可选
[root@iZuf68enovvnl1qpz1bvdoZ hexo]# hexo s
```

启动服务之后即可在GitHub page中看到更新文章。
