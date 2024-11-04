traceroute：找出中间经过了哪些路由器

数据结构sockaddr_in：
```
struct sockaddr_in {
    short int sin_family;       // 地址族
    unsigned short int sin_port; // 端口号（网络字节序）
    struct in_addr sin_addr;    // IP 地址
    unsigned char sin_zero[8];  // 保留的空字节
};
```
数据结构host_end：
```
struct hostent{
	char *h_name;         //正式主机名
	char **h_aliases;     //主机别名
	int h_addrtype;       //主机IP地址类型：IPV4-AF_INET
	int h_length;		  //主机IP地址字节长度，对于IPv4是四字节，即32位
	char **h_addr_list;	  //主机的IP地址列表
};	
#define h_addr h_addr_list[0]   //保存的是IP地址
```