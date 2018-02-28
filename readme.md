# v2ray
[![build](https://github.com/nanqinlang/SVG/blob/master/build%20passing.svg)](https://github.com/nanqinlang/v2ray)
[![language](https://github.com/nanqinlang/SVG/blob/master/language-shell-blue.svg)](https://github.com/nanqinlang/v2ray)
[![author](https://github.com/nanqinlang/SVG/blob/master/author-nanqinlang-lightgrey.svg)](https://github.com/nanqinlang/v2ray)
[![license](https://github.com/nanqinlang/SVG/blob/master/license-GPLv3-orange.svg)](https://github.com/nanqinlang/v2ray)

一个 websocket+tls+nginx+cloudflare 的 v2ray 模板（A template with websocket+tls+nginx+cloudflare of v2ray）

其中：
- nginx：v1.13.6，编译参数自行查看
- v2ray：v3.10-linux-64

## 服务端
获取文件：
```bash
download(){
	cd /home
	wget https://raw.githubusercontent.com/nanqinlang/v2ray/master/nginx.tar.gz && tar -zxf nginx.tar.gz && rm nginx.tar.gz
	wget https://raw.githubusercontent.com/nanqinlang/v2ray/master/v2ray.tar.gz && tar -zxf v2ray.tar.gz && rm v2ray.tar.gz
	chmod -R +x /home/nginx  &&  chmod -R +x /home/v2ray
}
```

然后，你要修改 `/home/nginx/conf/nginx-v2ray.conf` 和 `/home/v2ray/config_server.json` 这两个配置文件的`中文部分`的字符（按照注释修改）

配置文件改好后，启动服务端：
```bash
start(){
	# 启动 nginx
	/home/nginx/sbin/nginx

	# 启动 v2ray
	cd /home/v2ray && nohup ./v2ray -config config_server.json &
}
```

运行 `ps -A`，看到进程里有 nginx 和 v2ray 就对了。

然后 `cloudflare cdn websocket` 你自己去加。


## 客户端
反正客户端的配置文件就是 `config_client.json`，记得也要修改其中的`中文部分`。

这里介绍下 win 客户端的步骤：
1. 去 https://github.com/v2ray/v2ray-core/releases 下载 win 平台的压缩包，解压，删掉 config.json
2. 修改本项目的 config_client.json 后，重命名为 `config.json` 放到 v2ray 目录下
3. 双击 v2ray.exe，弹出窗口 "[Warning] Core: V2Ray started"