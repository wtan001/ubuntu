##环境ubuntu 16.04.1

首先更新软件源

	apt-get update
	
然后安装PIP环境

	apt-get install phython-pip
	
直接安装shadowsocks

	pip install shadowsocks
	
新建文件存放脚本

	vim /etc/shadowsocks.json
	
在编辑器里写入代码

	{
		"server":"server_ip",
		"server_port":8388,
		"local_address":"127.0.0.1",
		"local_port":1080,
		"password":"mypassowrd",
		"timeout":300,
		"method":"rc4-md5"
	}
	
_备注：可选择的加密方式有“bf-cfb”, “aes-256-cfb”, “des-cfb”, “rc4″, 等等。_

如果需要配置多个用户，可以这样设置

	{
		"server":"server_ip",
		"port_password":{
			"端口1":"密码1",
			"端口2":"密码2"
		},
		"timeout":300,
		"method":"rc4-md5",
		"fast_open": false
	}
	
赋予文件权限

	chmod 755 /etc/shadowsocks.json

安装加密方式插件

	apt–get install python–m2crypto

使用配置文件运行shadowsocks服务器

	ssserver -c /etc/shadowsocks.json -d start

开机自动运行，编辑/etc/rc.local

	vi /etc/rc.local

在 exit 0 这一行的上边加入如下

	/usr/local/bin/ssserver –c /etc/shadowsocks.json

或者 不用配置文件 直接加入命令启动如下：

		/usr/local/bin/ssserver -p 8388 -k password -m aes-256-cfb -d start


