这里使用 Nginx 反向代理解决 Wss 服务问题，即客户端通过 Wss 协议连接 Nginx 然后 Nginx 通过 Ws 协议和 Server 通讯；

也就是说 Nginx 负责通讯加解密，Nginx 到 Server 是明文的，Swoole 不用开启 ssl，而且还能隐藏服务器端口和负载均衡；

当然你也可以使用 Swoole Server 的 `ssl_cert_file` 和 `ssl_key_file` 配置选项。

```conf
server {
    #下面这个部分和正常配置 https 没有什么区别
    listen 443;
    server_name 域名;

    ssl on;

    #申请域名对应的证书
    ssl_certificate 你的证书.crt;
    ssl_certificate_key 你的密匙.key;

    ssl_session_timeout 5m;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 SSLv2 SSLv3;
    ssl_ciphers ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP;
    ssl_prefer_server_ciphers on;
    ssl_verify_client off;

    #反向代理 需要把后续.php相关的和重写index.php的部分删除
    location / {
        proxy_redirect off;
        proxy_pass http://127.0.0.1:9501; #转发到你本地的9501端口 对应 ws 的端口
        proxy_set_header Host $host;
        proxy_set_header X-Real_IP $remote_addr;
        proxy_set_header X-Forwarded-For $remote_addr:$remote_port;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade; #升级协议头
        proxy_set_header Connection upgrade;
    }
}
```

重载 Nginx 服务，如果没有错误，打开 [测试工具](http://wstool.qq52o.cn)，服务地址输入 `wss://域名`

无需添加端口号，点击开启连接，提示 `OPENED`，恭喜你 Wss 服务就可以了
