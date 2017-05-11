# Nginx

## server 字段

**动态转发**  
```conf
server {
    listen 80;
    server_name im-server.plusman.cn;

    # = / 用于精确匹配，遇到立即终止
    location / {
        proxy_pass http://127.0.0.1:7078;

        # https://github.com/socketio/socket.io/blob/master/examples/cluster-nginx/nginx/nginx.conf
        # enable WebSockets
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```
**静态文件服务**  
```conf
server {
    listen 80;
    server_name swagger.plusman.cn;

    location / {
        root /home/ubuntu/tool/swagger-ui/dist;
    }
}
```

**https 服务配置**  
[Let's Encrypt，免费好用的 HTTPS 证书](https://imququ.com/post/letsencrypt-certificate.html)  
```conf
server {
    listen 80;
    server_name www.plusman.cn plusman.cn;

    location ^~ /.well-known/acme-challenge/ {
        alias /root/ssl/challenges/;
        try_files $uri =404;
    }

    location / {
        rewrite ^/(.*)$ https://plusman.cn/$1 permanent;
    }
}

server {
    listen 443 ssl;
    server_name www.plusman.cn plusman.cn;

    ssl_certificate /root/ssl/chained.pem;
    ssl_certificate_key /root/ssl/domain.key;

    location / {
        root /root/gitbook/plusmancn.github.com/_book;
    }
}
```

## 403 
请检查 `nginx user`
