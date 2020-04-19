## 腾讯 url.cn

!> `url.cn`加了`csrf`，等有人研究了再修改吧

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

## 腾讯微信 w.url.cn

原理是使用微信公众号提供的接口转换短接口，可以使用测试公众号进行调用

* 申请测试号，[点击前往](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login)
* 获取`appID`、`appsecret`，对应下面代码的`$appid`和`$secret`
* 调用即可

!> 可以增加一个缓存`AccessToken`的操作，示例代码未提供

```php
$url = "https://qq52o.me";
$appid = "";
$secret = "";

$token = getAccessToken($appid, $secret);
$data = [
    "action" => "long2short",
    "long_url" => $url,
];
$res = curlRequest("https://api.weixin.qq.com/cgi-bin/shorturl?access_token={$token}", json_encode($data), true);
var_dump($res);

function getAccessToken($appid, $secret)
{
    $url = "https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid={$appid}&secret={$secret}";
    $tokenJson = curlRequest($url);
    $tokenArr = json_decode($tokenJson,true);
    if(isset($tokenArr['errcode'])) {
        return "";
    }
    // 此处应该缓存 可以自己提供一个api 使用redis缓存2个小时
    $accessToken = $tokenArr['access_token'];
    return $accessToken;
}

function curlRequest($url, $params = false, $ispost = 0)
{
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
    curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 2);
    curl_setopt($ch, CURLOPT_HTTPHEADER, array ('Content-Type: application/json'));
    if ($ispost) {
        curl_setopt($ch, CURLOPT_POST, true);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $params);
        curl_setopt($ch, CURLOPT_URL, $url);
    } else {
        if ($params) {
            curl_setopt($ch, CURLOPT_URL, $url.'?'.$params);
        } else {
            curl_setopt($ch, CURLOPT_URL, $url);
        }
    }
    $response = curl_exec($ch);
    if ($response === false) {
        return curl_error($ch);
    }
    curl_close($ch);
    return $response;
}
```