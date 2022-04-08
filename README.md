# x-ui được việt hoa bởi Trạm Sách 

# x-ui
xray panel with multi-protocol multi-user support

# Features
- System status monitoring
- Support multi-user multi-protocol, web page visualization operation
- Supported protocols: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Support to configure more transmission configurations
- Traffic statistics, limit traffic, limit expiration time
- Customizable xray configuration templates
- Support https access panel (bring your own domain name + ssl certificate)
- For more advanced configuration items, see the panel for details

# Instal and Update
```
bash <(curl -Ls https://raw.githubusercontent.com/tramsach/x-ui/main/install.sh)
```

## Manual install & upgrade
1. First download the latest compressed package from https://github.com/vaxilu/x-ui/releases, generally choose `amd64` architecture
2. Then upload the compressed package to the `/root/` directory of the server, and use the `root` user to log in to the server

> If your server cpu architecture is not `amd64`, replace `amd64` in the command with another architecture

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## 使用docker安装

> 此 docker 教程与 docker 镜像由[Chasing66](https://github.com/Chasing66)提供

1. 安装docker
```shell
curl -fsSL https://get.docker.com | sh
```
2. 安装x-ui
```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```
>Build 自己的镜像
```shell
docker build -t x-ui .
```

## 建议系统
- CentOS 7+
- Ubuntu 16+
- Debian 8+

# 常见问题

## 从 v2-ui 迁移
首先在安装了 v2-ui 的服务器上安装最新版 x-ui，然后使用以下命令进行迁移，将迁移本机 v2-ui 的`所有 inbound 账号数据`至 x-ui，`面板设置和用户名密码不会迁移`
> 迁移成功后请`关闭 v2-ui`并且`重启 x-ui`，否则 v2-ui 的 inbound 会与 x-ui 的 inbound 会产生`端口冲突`
```
x-ui v2-ui
```

## issue 关闭
各种小白问题看得血压很高

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
