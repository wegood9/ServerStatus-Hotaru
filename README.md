# ServerStatus-Hotaru
云探针、多服务器探针、云监控、多服务器云监控

基于ServerStatus-Toyo最新版本稍作修改，不太会脚本什么的，前端也垃圾。见谅

Test v0.014：图片来源：Pixiv：72725286

## 特性

模板来自：<https://www.hostloc.com/thread-494384-1-1.html>

稍作修改。

加入每个服务器的自定义链接，以便快速跳转到该服务器（测速、Looking Glass等用途）。

多了个Region调用国旗。所以用原来Toyo版的需要稍作修改

## 一键安装

仅推荐CentOS/Debian x86/x86_64系统使用，不保证所有系统可用性
完成后最好手动检查服务端配置文件

```
wget https://raw.githubusercontent.com/wegood9/ServerStatus-Hotaru/master/status.sh
bash status.sh s
```
具体请参见：https://www.cokemine.com/serverstatus-hotaru.html

## 手动安装

### 下载代码
```
https://github.com/wegood9/ServerStatus-Hotaru.git
```
### 编译服务端
```
cd ServerStatus-Hotaru/server
make
./sergate
```
如果没有错误提示，按ctrl+c关闭即可；如果有错误提示，检查35601端口是否被占用
### 修改配置文件
按照需求编辑config.json
```
{"servers":
	[
		{
			"username": "s01",
			"password": "your password",
			"name": "Mainserver 1",
			"type": "Dedicated Server",
			"host": "No",
			"location": "America",
			"disabled": false,
			"region": "US",
			"link": ""
		},
	]
}       
```
### 运行服务端
拷贝ServerStatus-Hotaru/web到你的网站目录下，例如：
```
cp -r ServerStatus-Hotaru/web/* /home/wwwroot/default
```
主程序有以下命令行选项可用：
```
    -h, --help            Show this help message and exit
    -v, --verbose         Verbose output
    -c, --config=<str>    Config file to use
    -d, --web-dir=<str>   Location of the web directory
    -b, --bind=<str>      Bind to address
    -p, --port=<int>      Listen on port
```
web-dir参数修改成自己网站的路径，默认监听35601端口
```
./sergate --config=config.json --web-dir=/home/wwwroot/default   
```
这样就完成了，不过更推荐使用init.d或systemd来管理
### 运行客户端
编辑client/status-client.py中的ip、用户名和密码
```
python status-client.py
```
### 使用init.d管理服务端/客户端
init.d脚本已于ServerStatus-Hotaru/service中提供，自行修改相关路径
例如：
```
$ vi ServerStatus-Hotaru/service/server_status_server_debian
# cp ServerStatus-Hotaru/service/server_status_server_debian /etc/init.d/status-server
# chmod +x /etc/init.d/status-server
# chkconfig --add status-server
# chkconfig status-server on
```
## 服务段配置修改方法

配置文件：/usr/local/ServerStatus/server/config.json备份并自行添加Region、Link

![](https://i.loli.net/2019/02/07/5c5bca12df8b0.png)


## 效果演示(原版本）

此版本节点名可定义为对应的自定义链接，请自行脑补
![](https://i.loli.net/2019/04/05/5ca74fb05338f.png)

![](https://i.loli.net/2019/04/05/5ca74fc86db96.png)

当然前端可以自己自定义。

## 相关开源项目 ： 
* ServerStatus-Toyo：https://github.com/ToyoDAdoubiBackup/ServerStatus-Toyo
* ServerStatus：https://github.com/BotoX/ServerStatus
* mojeda: https://github.com/mojeda 
* mojeda's ServerStatus: https://github.com/mojeda/ServerStatus
* BlueVM's project: http://www.lowendtalk.com/discussion/comment/169690#Comment_169690
