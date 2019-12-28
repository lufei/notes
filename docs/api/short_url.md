## 腾讯 url.cn

请求地址：`https://vip.video.qq.com/fcgi-bin/comm_cgi`  
请求参数：`name，need_short_url，url`  
示例：
```
https://vip.video.qq.com/fcgi-bin/comm_cgi?name=short_url&need_short_url=1&url=https://notes.qq52o.me
```

请求方式：`GET`  
返回类型：`JSON`  
返回值：
```json
QZOutputJson=({
   "msg" : "ok",
   "qrcode" : "",
   "ret" : 0,
   "short_url" : "https://url.cn/5zo7b5d"
}
);
```