以下内容皆使用 PhpStorm 作为演示

## 快速启动/重启/停止服务

1. 点击 PhpStorm 右上角 Run 按钮旁边的`Add Configurations`

2. 点击 + 号添加一个`PHP Script`，填写对应的信息

![添加脚本](../images/debug/hyperf-1.png)

对应信息说明：

```
Name：脚本名称，这里我们取名叫 Hyperf

File：脚本路径，我们选择 Hyperf 目录下，bin文件夹下的hyperf.php，路径为：YourProject/bin/hyperf.php
Arguments：脚本参数，这里我们填写 start 开启命令就行了，如果有需要可以写一些别的

Command Line
Interpreter options：解释器选项，这里默认不填写。如果你不想修改 php.ini 关闭短名称，可以填写-d swoole.use_shortname=Off
Custom Working directory：自定义工作目录，这里默认不填写
Environment variables：环境变量，这里默认不填写

Before launch：Activate tool window
启动前，我们需要做的事，默认不填写
```

3. 点击 Apply 保存即可，选中刚才配置的 Hyperf 脚本

![选中脚本](../images/debug/hyperf-2.png)

4. 选中后在需要启动 Hyperf 服务时可以直接点击 Run 图标即可

![一键执行](../images/debug/hyperf-3.png)

也可以直接点击一键重启和关闭

## REST Client

点击 PhpStorm 上方的工具栏，找到 Tools 、 HTTP Client 、Test RESTful Web Service 点开后如图：

![REST Client](../images/debug/hyperf-4.png)

和 PostMan 类似，我们可以选择对应的请求方式、域名地址、接口路径

点击 Run 图标即可