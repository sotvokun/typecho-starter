# typecho-starter

## 使用方法

### 0. 准备工作
使用命令行下载本项目，并移动到工作目录中
```shell
git clone https://github.com/sotvokun/typecho-starter
```
```shell
cd typecho-starter
```

### 1. 设置网站 URL
打开 `docker-compose.yml` 然后在 `- TYPECHO_SITE_URL=` 后面填入你的网站的链接。

### 2. 新建 `usr` 文件夹
新建一个文件夹并命名为 `usr`，并将其所属用户和所属组修改为 `www-data`。

如果您使用的是命令行界面，你可以使用使用以下的命令：
```shell
mkdir usr && chown -R www-data:ww-data usr/
```

### 3. 启动
```shell
docker-compose up -d
```

## 其他设置

### 设置对外访问的端口号 (默认:80)
如果你需要修改其对外访问的端口号，请修改 `ports` 中冒号前面的数字。

### 反向代理设置
如果你修改了端口号，并需要使用宿主机的 nginx 来反向代理。你可以使用以下的 nginx 配置：
```
server {
        listen 80;
        server_name svdu.me;

        location / {
                proxy_pass http://127.0.0.1:35001;

                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
}
```