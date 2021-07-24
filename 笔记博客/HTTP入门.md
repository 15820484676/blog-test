# HTTP Hyper Text Transfer Protocol 超文本传输协议
## IP
* 定位一台设备
* 封装数据报文 
* 外网IP和内网IP
* 特殊IP ：127.0.0.1 localhost都是表示自己。 0.0.0.0不表示任何设备
## 路由器的功能
* 路由器有两个IP 一个外网 一个内网
* 也叫网关，相当于连通器
* 内网要访问外网，得经过路由中专
* 外网无法访问内网，得经过路由中转
## 端口 port
* HTTP 80
* HTTPS 443
* FTP 21
* 65535个端口
* 0到1023号是留给系统用的 
* 如果端口被占用了 要么杀掉或者杀一个 
* 定位一个服务的
## 域名 
* 对IP的别称
* 一个域名可以对应不同IP 叫负债均衡
* 一个IP可以对于不同域名 叫共享主机
* 通过DNS连接起来(Domain Name System)域名系统
## URL 统一资源定位符
* 协议 + 域名 +端口+ 路径 + 查询参数 + 锚点
* 锚点不会传给服务器

## CURL
* curl -v http://baidu.com连接详细信息 
* 先进行TCP连接，连接后才发送HTTP请求

## 如何发请求
* curl命令
* chrome直接访问

## 如何做出一个响应
* 使用node.js编写服务端代码
* node server 监听端口
* 设置响应状态码： response.statusCode=200
* 设置响应头：response.setHeader('Content-Type:text/html')
* 设置响应体：response.write('内容')，可以追加内容
* console.log()进行调试

## HTTP基础概念
* 请求
请求动词  路径加查询参数 协议名/版本
Host:域名或IP
Accept:text/html
Content-Type:请求体的格式
回车
请求体

* 响应
协议名/版本 状态码 状态字符串  
Conent-Type:响应体的格式  
回车  
响应体  

* 常见状态码

## 用CURL构造请求
curl  -v -X POST -d 'text=3333' -H 'Accept: text/html'

## 云服务器
