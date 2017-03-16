# Nginx

## server 字段

**动态转发**  
```shell
server {
    listen 80;
    server_name im-server.plusman.cn;

    # = / 用于精确匹配，遇到立即终止
    location / {
        proxy_pass http://127.0.0.1:7078;
    }
}
```
**静态文件服务**  
```shell
server {
    listen 80;
    server_name swagger.plusman.cn;

    location / {
        root /home/ubuntu/tool/swagger-ui/dist;
    }
}
```
