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