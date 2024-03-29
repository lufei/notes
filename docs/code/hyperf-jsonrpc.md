# Hyperf JsonRPC

如何启用 Hyperf 的 JSON RPC 服务端，具体请查看文档的 [JSON RPC 服务](https://hyperf.wiki/2.0/#/zh-cn/json-rpc) 部分

客户端可以参考[JSON-RPC 2.0 Specification](https://www.jsonrpc.org/specification)

## HTTP

以下为简单调用 JsonRpcHTTP 的示例代码

```php
<?php
$ch = curl_init();
$url = 'http://127.0.0.1:9504';
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

## Tcp

以下为简单调用 JsonRpcTcp 的示例代码

```php
<?php
const RPC_EOF = "\r\n";

function request($host, $method, $param, $id = '') {
	$fp = stream_socket_client($host, $errno, $errstr);
	if (!$fp) {
		throw new Exception("stream_socket_client fail, errno={$errno} errstr={$errstr}");
	}

	$req = [
		"jsonrpc" => '2.0',
		"method" => $method,
		'params' => $param,
		'id' => $id,
	];
	$data = json_encode($req) . RPC_EOF;
	fwrite($fp, $data);

	$result = '';
	while (!feof($fp)) {
		$tmp = stream_socket_recvfrom($fp, 1024);

		if ($pos = strpos($tmp, RPC_EOF)) {
			$result .= substr($tmp, 0, $pos);
			break;
		} else {
			$result .= $tmp;
		}
	}

	fclose($fp);
	return json_decode($result, true);
}

$ret = request('tcp://127.0.0.1:9503', "calculator/add",  [1, 2]);
var_dump($ret);
```
