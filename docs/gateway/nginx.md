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