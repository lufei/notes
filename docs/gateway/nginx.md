# Nginx

## 隐藏版本号

进入 nginx 配置文件的目录，编辑`nginx.conf`

在`http {}`里加上`server_tokens off;`

编辑 php-fpm 配置文件，如`fastcgi.conf`或`fcgi.conf`

```ini
#找到：
fastcgi_param SERVER_SOFTWARE nginx/$nginx_version;
#改为：
fastcgi_param SERVER_SOFTWARE nginx;
```

重载 nginx 配置即可

## 反向代理

### HTTP

```conf
# 至少需要一个 Server 节点，多个配置多行
upstream http_servers {
    # HTTP Server 的 IP 及 端口
    server 127.0.0.1:9501;
    server 127.0.0.1:9502;
}

server {
    # 监听端口
    listen 80; 
    # 绑定的域名
    server_name proxy.host.name;

    location / {
        # 将客户端的 Host 和 IP 信息一并转发到对应节点  
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        
        # 转发Cookie，设置 SameSite
        proxy_cookie_path / "/; secure; HttpOnly; SameSite=strict";
        
        # 执行代理访问真实服务器
        proxy_pass http://http_servers;
    }
}
```

- [配置 Websocket Wss 代理](/code/websocket.md)

## 伪静态

```conf
location / {
    if (!-e $request_filename) {
        rewrite ^/(.*)$ /index.php/$1 last;
        break;
    }
}

location ~ \.php/?.*$ {
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
    include fastcgi.conf;

    set $fastcgi_script_name2 $fastcgi_script_name;
    if ($fastcgi_script_name ~ "^(.+\.php)(/.+)$") {
        set $fastcgi_script_name2 $1;
        set $path_info $2;
    }
    fastcgi_param PATH_INFO $path_info;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name2;
    fastcgi_param SCRIPT_NAME $fastcgi_script_name2;
}
```