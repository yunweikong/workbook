网络的其他三层都在内核空间中实现，而应用层一般在用户空间中实现。
- 列举一些应用层协议
	- ping是应用层程序而非协议，利用ICMP报文检测网络连接，调试网络环境
	- telnet协议是远程登陆协议
	- OSPF(Open Shortest Path First开发路径最短优先)协议：动态路由更新协议，用于路由器间的通信，告知对方各自的路由信息
	- DNS(Domain Name Service)协议
- 应用层可以跳过传输层直接使用网络层服务，如ping和OSPF。我们可以用过/etc/services文件查看所有的知名应用层协议和它们能使用的传输层服务

* 封装encapsulation：TCP message segment/UDP datagram；IP datagram；frame（ethernet frame以太网帧，token ring frame令牌环帧）
* 分片fragment：MTU(Max Transmit Unit帧的最大传输单元)
* 解封装decapsulation

- Multiplexing 多路复用
- Demultiplexing 多路分解/分用：根据某些标识（如端口号）将接收到的数据包分配到不同的进程或应用的过程
	- 帧的类型；IP datagram通过16位protocol协议字段区分ICMP/UDP/TCP；端口号port number区分上层应用程序

- **ARP协议**：实现任意网络层地址到任意物理地址的转换
	- 在以太网中，主机向自己所在的网络广播一个ARP请求（目标机器网络地址），目标机器将予以包含自己物理地址的ARP应答
	- ARP维护一个高速缓存，包含经常访问/最近访问的一些映射
		- *Linux下可以使用 arp 命令查看和修改ARP高速缓存* 
- **DNS服务**：

##### Web服务器
- 代理服务器：正向代理，反向代理，透明代理
	- 透明代理通常部署在网络的入口点，例如路由器、网关或防火墙上。它会截获所有通过的网络流量，并根据预设规则进行处理。
		- 内容过滤、**缓存**、监控和审计、访问控制、负载均衡
	- 透明代理通常使用Squid、Nginx或iptables等工具设置。
- 服务脚本和`systemd`单元文件是管理Linux系统上服务器程序和服务的重要工具。通过编写和配置这些文件，可以方便地启动、停止、重启和检查服务的状态，从而确保系统的稳定和可靠运行。随着`systemd`在大多数Linux发行版中的普及，学习和掌握`systemd`的用法显得尤为重要。

* 连接方式：客户端`->`代理服务器(局域网内)`->`网关（路由）`->`目标服务器
	* 需要指出的是，虽然IP数据报是先发送到路由器再由其转发到目标主机，但其头部的IP是始终不变的（一种例外是源路由选择）。但帧头部的源端物理地址和目的端物理地址在转发过程中一直在变换
	* 如果`/etc/hosts`文件中能找到IP地址，就用该地址；否则求助DNS
		* 用户可以通过修改`/etc/host.conf`文件来自定义系统解析主机名的方法和顺序
		* 这个本地名称查询服务被提出于`RFC 1123`
* wget访问某Web服务器时，它先读取环境变量`http-proxy`，试图通过代理服务器访问。

- [HTTP请求方法](https://www.runoob.com/http/http-methods.html)：GET, HEAD, POST, PUT ,DELETE, TRACE, OPTIONS, CONNEXT, PATCH
	- HEAD, GET, OPTIONS, TRACE是安全的方法，而POST, PUT, DELETE, PATCH则影响服务器上的资源；其中只有POST不是幂等的，多次相同请求仍影响服务器资源
	- 第一行请求行：`HTTP方法 请求URI HTTP版本`
		- 请求行中的URI可以是相对URL。`GET /index.html HTTP/1.1`
		- 对于绝对URI（包含协议和主机名的完整URL），通常出现在代理服务器的请求中，而不是直接向目标服务器的请求中。`GET http://www.baidu.com/index.html HTTP/1.0`
			- `http`是`scheme`，即获取目标资源需要使用的应用层协议；其他常见的有：`ftp`, `ftsp`, `file`…；`/index.html`指定资源文件的名称（服务器根目录，即站点根目录中的文件，不是文件系统根目录）
	- HTTP请求的头部字段
		- 一个HTTP请求可以包含多个头部字段，每一行都是一个头部字段，顺序是任意的
		- `HOST: www.baidu.com`目标主机名，HTTP请求必须包含。
		- `User-Agent:`客户端的发起程序`Wget/1.12(linux-gnu)`, `User-Agent: curl/7.68.0`
		- `Connection: close`在执行wget命令时传入的，意味处理完毕后关闭连接
	- 头部结束，空行`\r\n`
	- 接下来是body内容
		- 如果消息体非空，则头部必须包含消息体长度字段`Content-Length`
- `Connection`字段指示了长连接/短连接方式，长连接可以大大提高性能

- HTTP应答：
	- 第一行是状态行：`HTTP版本 状态码 状态信息`
		- `HTTP版本`一般与客户端相同，[状态码和状态信息](https://www.runoob.com/http/http-status-codes.html)
	- HTTP响应的头部字段，和HTTP请求字段相同
	- 空行
	- 接下来是body内容