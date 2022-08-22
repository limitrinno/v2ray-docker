# v2ray-docker
基于Docker(centos7.9)搭建的ws+tls(cloudflare)的v2ray

# Docker Install
- Hello World!

# Docker Install Centos

```
docker run -itd --name=v2ray --network=host --restart=always centos:centos7.9.2009
docker exec -it v2ray bash
```

# Acme - Cloudflare - SSL
- Cloudflare Api Tokens
- https://dash.cloudflare.com/profile/api-tokens

```
cd ~ && wget -N --no-check-certificate https://raw.githubusercontent.com/limitrinno/v2ray-docker/main/acme1key.sh && bash acme1key.sh
```
脚本有提示，自行操作吧。

# Docker 下安装nginx

```
yum -y install epel-release && yum -y install nginx wget vim
```

## 一顿操作
- mkdir -p /etc/nginx/ssl && mkdir -p /www/v2
- cd ~ && mv private.key cert.crt /etc/nginx/ssl/
- wget -P /etc/nginx/conf.d/ --no-check-certificate https://raw.githubusercontent.com/limitrinno/v2ray-docker/main/v2.conf
- vi /etc/nginx/conf.d/v2.conf 修改提示的内容

# Docker 下安装v2ray
```
cd ~
curl -O https://raw.githubusercontent.com/limitrinno/v2ray-docker/main/install-release.sh
curl -O https://raw.githubusercontent.com/limitrinno/v2ray-docker/main/install-dat-release.sh
bash install-release.sh
bash install-dat-release.sh
systemctl restart v2ray && systemctl enable v2ray
rm -rf install-releases.sh install-dat-release.sh
```

# 下载配置文件
```
rm -rf /usr/local/etc/v2ray/config.json
wget -P /usr/local/etc/v2ray/ --no-check-certificate https://raw.githubusercontent.com/limitrinno/v2ray-docker/main/config.json
```

# 启动 - 自行根据配置填入
```
nohup /usr/local/bin/v2ray -config /usr/local/etc/v2ray/config.json > /dev/null 2&>1 &
```
