# 使用 Docker 快速部署网易云音乐代理服务器

## 涉及工具

- 服务器一台（能运行 docker 即可）
- 手机端需安装一个证书
- 代理软件一个（surge/quantumult(x)/shadowsocket/kitsunbi 等）


# 服务器端操作

## 安装 Docker
> apt install docker-ce docker-ce-cli containerd.io

或者
> wget -qO- https://get.docker.com/ | sh

### 安装完成后，执行 docker -v ，测试安装是否成功


## 运行 unblockneteasemusic 容器

> docker run -d --name ubmusic -p 8008:8080 nondanee/unblockneteasemusic -s -e https://music.163.com -p 8080:8081

*其中 --name 后面的 ubmusic 是名字，可以随便填写*
*第一个 -p 后面的 8008 是你的服务器代理端口，也可以任意修改。（记得完全组（防火墙）放行端口）*

### 使用 docker ps 命令查看容器是否正常运行

如果没问题的话，服务器端的操作就完成了。


# 手机端操作

## 证书安装与信任
证书地址(设备上点击链接应该会自动跳转)：
> https://raw.githubusercontent.com/nondanee/UnblockNeteaseMusic/master/ca.crt

（上面这个证书是 UnblockNeteaseMusic 作者的，如果不信任的话，这个软件也可以不用了，找其它方式）

在设置 > 通用 > 关于本机 > 证书信任设置，手动信任证书
官方教程：https://support.apple.com/zh-cn/HT204477

## 网易云音乐流量代理

### 代理方式
http

### 代理地址
服务器IP:端口(8008 或 修改后的端口)

比如：
140.238.1.170:8008
 (自用测试，随时失效)

### 网易云音乐流量转发
把 
> music.163.com, interface.music.163.com

这两个域名的流量代理到上面设置好的服务器上（就和代理 google/twitter 差不多，只不过把使用不同域名和服务器。）

具体参考各个代理软件的服务器添加和规则分流方式，软件都大同小异，就不一一详述了。


# 总结
服务器端：
运行两条指令
> wget -qO- https://get.docker.com/ | sh  *（如果已安装过 Docker 可以省略）*
> docker run -d --name ubmusic -p 8008:8080 nondanee/unblockneteasemusic -s -e https://music.163.com -p 8080:8081


手机端：
- 安装/信任证书
- 设置代理（添加代理服务器，添加分流规则）

Done!