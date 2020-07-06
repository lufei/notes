## 快捷键

1. `Command + Shift + A`

在 Windows 中的是 `Ctrl + Shift + A`，弹出一个动作查询窗口，输入操作或者工具的关键词就可以执行操作或打开工具

比如：需要打开 Terminal 工具，那么在窗口输入 ter ，按下`Enter`键，
那么就能打开 Terminal工具。

## Live Templates

快捷生成代码块、注释等。

设置 -> Editor -> Live Templates

![Live Templates](//cdn.jsdelivr.net/gh/lufeidot/notes@master/docs/images/phpstorm/LiveTemplates.png)

## REST Client

点击 PhpStorm 上方的工具栏，找到 Tools 、 HTTP Client 、Test RESTful Web Service 点开后如图：

![REST Client](//cdn.jsdelivr.net/gh/lufeidot/notes@master/docs/images/phpstorm/rest-client.png)

和 PostMan 类似，我们可以选择对应的请求方式、域名地址、接口路径

点击 Run 图标即可

## 设置FTP自动同步文件

1. 添加一个FTP服务器

`工具栏 -> Tools -> Deployment -> Configuration`

点击+号添加一个服务器，填写对应的连接信息

![](//cdn.jsdelivr.net/gh/lufeidot/notes@master/docs/images/phpstorm/add-ftp-server.png)

2. 添加项目路径

这里需要设置项目路径，否则下一步设置自动上传时会报错`Default server mservice has no valid mappings. Automatic upload is not enabled`

点击`Mappings`，填写对应的项目路径

![](//cdn.jsdelivr.net/gh/lufeidot/notes@master/docs/images/phpstorm/add-ftp-mappings.png)

`Local path`为本地的项目路径，默认是当前目录  
`Deployment path`为远端ftp服务器对应的路径，这里需要注意的是此路径会拼接上一步中的`Root path`，即我上传到ftp服务器的路径为：`/root/luffy/swool`

3. 设置FTP自动上传

`工具栏 -> Tools -> Deployment -> Automatic Upload`

到此，今后编辑文件后按 Ctrl+S (MAC：command + S)保存文件，即可自动将文件上传到FTP服务器了