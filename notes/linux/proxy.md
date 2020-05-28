# proxy 相关

### 一、curl 使用代理

```
curl -O XX --socks5 127.0.0.1:1080
```

### 二、wget 使用代理

##### 1、修改环境变量

```
export http_proxy=http://127.0.0.1:1080
```

##### 2、修改 /etc/wgetrc 或 ~/.wgetrc

```
#You can set the default proxies for Wget to use for http, https, and ftp.
# They will override the value in the environment.
https_proxy = http://127.0.0.1:1080/
http_proxy = http://127.0.0.1:1080/
ftp_proxy = http://127.0.0.1:1080/

# If you do not want to use proxy at all, set this to off.
use_proxy = on
```

##### 3、使用 -e

```
wget -e "http_proxy=http://127.0.0.1:1080"
```

##### 4、安装 tsocks

```
apt-get -y install tsocks
```

```
vim /etc/tsocks.conf
server = 127.0.0.1
server_type = 5
server_port = 1080
```

```
tsocks wget http://*
```

### 三、docker 使用代理

```
cat /etc/systemd/system/docker.service.d/http-proxy.conf

[Service]
Environment="HTTP_PROXY=http://127.0.0.1:1080"
Environment="HTTPS_PROXY=http://127.0.0.1:1080"
Environment="NO_PROXY=localhost,127.0.0.1"
```

```
systemctl daemon-reload
systemctl restart docker
```

### 四、git 代理

```
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

### 五、linux 代理

```
export http_proxy=socks5://127.0.0.1:1080
export https_proxy=socks5://127.0.0.1:1080
export ftp_proxy=http://127.0.0.1:1080
export no_proxy=localhost,127.0.0.1
```

```
# 强制终端中的 wget、curl 等都走 SOCKS5 代理
export ALL_PROXY=socks5://127.0.0.1:1080
```
