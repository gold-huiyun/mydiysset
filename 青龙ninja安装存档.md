# 安装说明
注：以下教程仅适用于Centos系统服务器初次安装青龙(arm服务器可能有一些兼容性问题)
___
### 前言

[qinglong作者仓库地址](https://github.com/whyour/qinglong.git)

[Ninja作者仓库地址](https://github.com/Waikkii/Waikiki_ninja/tree/master)
### 前置要求（不支持docker的服务器就不要往下看了-点名Euserv小鸡）
```bash
1.已安装docker-ce
2.选装docker-compose
```






### 搭建步骤

1.首先服务器防火墙放行5700-5701端口，然后ssh连接服务器

2.输入命令
```bash
docker run -dit \
   -v $PWD/ql/config:/ql/config \
   -v $PWD/ql/log:/ql/log \
   -v $PWD/ql/db:/ql/db \
   -v $PWD/ql/repo:/ql/repo \
   -v $PWD/ql/raw:/ql/raw \
   -v $PWD/ql/scripts:/ql/scripts \
   -v $PWD/ql/jbot:/ql/jbot \
   -v $PWD/ql/ninja:/ql/ninja \
   -p 5700:5700 \
   -p 5701:5701 \
   --name qinglong \
   --hostname qinglong \
   --restart unless-stopped \
   whyour/qinglong:latest
```   
3.开始配置青龙的登录信息和推送信息（此处如果报错可以跳过）

打开浏览器访问宿主机ip的5700端口即可
例如http://127.0.0.1:5700
即你的ip:5700


4.进入青龙容器

```bash
docker exec -it qinglong bash
```

5.拉取配置ninja
```bash
git clone -b master https://ghproxy.com/https://github.com/Waikkii/waikiki_ninja.git /ql/ninja
cd /ql/ninja/backend
pnpm install
cp .env.example .env
pm2 start
cp sendNotify.js /ql/scripts/sendNotify.js
```
6.进入青龙面板打开配置文件，将以下代码粘贴到`extra.sh`并保存
```bash
cd /ql/ninja/backend
git checkout .
git pull
pnpm install
pm2 start
cp sendNotify.js /ql/scripts/sendNotify.js
```
8.浏览器输入你的服务器ip:5701进入ninja
如果无法进入可尝试重新ssh连接服务器，输入以下命令重启青龙容器。

```bash
docker restart qinglong
```

说明：Ninja配置文件在目录`ql/ninja/backend/.env`，可以按照自己需求并结合服务器性能自行修改。
