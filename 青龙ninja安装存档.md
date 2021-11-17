# 安装说明
注：以下教程仅适用于Centos系统服务器初次安装青龙(arm服务器可能有一些兼容性问题)
___
### 前言

[qinglong作者仓库地址](https://github.com/whyour/qinglong.git)

[Ninja作者仓库地址](https://github.com/Waikkii/Waikiki_ninja/tree/master)
### 前置要求（不支持docker的服务器就不要往下看了-点名Euserv小鸡）

1.已安装docker-ce

2.选装docker-compose

#### 这里推荐以下方法快速安装
1.安装docker
```bash
sudo yum check-update
curl -sSL https://get.daocloud.io/docker | sh
sudo systemctl start docker
sudo systemctl status docker
sudo systemctl enable docker
```
2.安装docker-compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
```

### 搭建步骤

1.首先服务器防火墙放行5700-5701端口，然后ssh连接服务器

2.输入以下命令拉取部署青龙
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
3.开始配置青龙的登录信息和推送信息（此处如果推送配置报错可以先跳过，可在配置文件config.sh中或环境变量处添加）

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
7.浏览器输入你的服务器ip:5701即可进入ninja
如果无法进入可尝试重新ssh连接服务器，输入以下命令重启青龙容器。

```bash
docker restart qinglong
```

说明：Ninja配置文件在目录`ql/ninja/backend/.env`，可以按照自己需求并结合服务器性能自行修改。


# 依赖库
### （最好都装一下，另 jsdom、png-js、requests三个要都装上，不使用命令的话也可在青龙依赖管理安装）
```bash
cd && docker exec -it qinglong bash -c "apk add --no-cache build-base g++ cairo-dev pango-dev giflib-dev && cd scripts && npm install canvas --build-from-source"
docker exec -it qinglong bash -c "npm install -g typescript"
 
docker exec -it qinglong bash -c "npm install axios date-fns"
 
docker exec -it qinglong bash -c "npm install crypto -g"
 
docker exec -it qinglong bash -c "npm install jsdom"
 
docker exec -it qinglong bash -c "npm install png-js"
 
docker exec -it qinglong bash -c "npm install -g npm"
 
docker exec -it qinglong bash -c "pnpm i png-js"
 
docker exec -it qinglong bash -c "pip3 install requests"
 
docker exec -it qinglong bash -c "apk add --no-cache build-base g++ cairo-dev pango-dev giflib-dev && cd scripts && npm install canvas --build-from-source"
 
docker exec -it qinglong bash -c "apk add python3 zlib-dev gcc jpeg-dev python3-dev musl-dev freetype-dev"
 
docker exec -it qinglong bash -c "cd /ql/scripts/ && apk add --no-cache build-base g++ cairo-dev pango-dev giflib-dev && npm i && npm i -S ts-node typescript @types/node date-fns axios png-js canvas --build-from-source"
```
