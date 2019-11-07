如何使用 Hyperf 的 JSON RPC 服务，具体请查看文档的 [JSON RPC 服务](https://hyperf.wiki/#/zh/json-rpc) 部分

以下为简单调用示例代码

```php
<?php
$ch = curl_init();
$url = 'http://localhost:9504';
$pra = '{
  "jsonrpc": "2.0",
  "method": "calculator/add",
  "params": {
  	"a": 1,
  	"b": 2
  },
  "id": "1"
}';

$pra2 = '{
  "jsonrpc": "2.0",
  "method": "calculator/add",
  "params": [1, 2],
  "id": "1"
}';

$options = [
	CURLOPT_URL => $url,
	CURLOPT_RETURNTRANSFER => 1,
];
curl_setopt_array($ch, $options);

//curl_setopt($ch, CURLOPT_POSTFIELDS, $pra);
curl_setopt($ch, CURLOPT_POSTFIELDS, $pra2);

$data = curl_exec($ch);
curl_close($ch);
var_dump(json_decode($data, true));
```