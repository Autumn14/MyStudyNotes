# Nginx学习

## 1.概念：

正向代理是客户端的代理

**反向代理**是服务器的代理

**负载均衡**

iphash，可以解决session不共享的问题，实际上用Redis更好的解决

**动静分离**

## 2.安装

安装包解压

nginx.conf

## 3.常用命令

nginx
nginx -s stop
nginx -s quit 安全退出
nginx -s reload 重新加载配置文件
ps aux|grep nginx

## 4.配置结构

```
全局配置

events {
	worker_connections 1024;
}

http {
	http 配置
	
	upstream hello{
		//负载均衡配置 名字随便起
		server 127.0.0.1:8080 weight=1;
		server 127.0.0.1:8081 weight=1;
		
	}
	
	server {
		listen 80;
		server_name localhost
		//反向代理
		location / {
			root html;
			index index.html index.htm;
			proxy_pass http://hello
		}
	}
	
	server {
		listen 443;
		server_name localhost
		//代理
	}
}
```

