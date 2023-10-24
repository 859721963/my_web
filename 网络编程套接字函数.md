# my_web 网络编程笔记
### setsockpt函数
****函数原型：int setsockopt(int sockFd, int level, int optname, const void *optval, socklen_t optlen);****

##### 1.sockFD：将要被设置或者获取选项的套接字。

##### 2.level：选项定义的层次；支持SOL_SOCKET、IPPROTO_TCP、IPPROTO_IP和IPPROTO_IPV6。一般设成SOL_SOCKET以存取socket层。
	SOL_SOCKET:通用套接字选项.
	IPPROTO_IP:IP选项.IPv4套接口
	IPPROTO_TCP:TCP选项.
	IPPROTO_IPV6: IPv6套接口

##### 3.optname：欲设置的选项。

![optname具体数值](https://github.com/859721963/my_web/assets/136427248/49833d9a-a286-49e6-aedd-9a1102aec393)

***SO_REUSEADDR（端口复用）参数单独说明***：
	optname选项之一：允许套接口和一个已在使用中的地址捆绑。
	SO_REUSEADDR提供如下四个功能：
	允许启动一个监听服务器并捆绑其众所周知端口，即使以前建立的将此端口用做他们的本地	端口的连接仍存在。这通常是重启监听服务器时出现，若不设置此选项，则bind时将出错。
	允许在同一端口上启动同一服务器的多个实例，只要每个实例捆绑一个不同的本地IP地址即	可。对于TCP，我们根本不可能启动捆绑相同IP地址和相同端口号的多个服务器。
	允许单个进程捆绑同一端口到多个套接口上，只要每个捆绑指定不同的本地IP地址即可。这	一般不用于TCP服务器。
	允许完全重复的捆绑：当一个IP地址和端口绑定到某个套接口上时，还允许此IP地址和端口	捆绑到另一个套接口上。一般来说，这个特性仅在支持多播的系统上才有，而且只对UDP套	接口而言（TCP不支持多播）。
SO_REUSEPORT有如下语义：
	此选项允许完全重复捆绑，但仅在想捆绑相同IP地址和端口的套接口都指定了此套接口选项才行。
	如果被捆绑的IP地址是一个多播地址，则SO_REUSEADDR和SO_REUSEPORT等效。

此选项允许完全重复捆绑，但仅在想捆绑相同IP地址和端口的套接口都指定了此套接口选项才行。
如果被捆绑的IP地址是一个多播地址，则SO_REUSEADDR和SO_REUSEPORT等效。

##### 4.optval： 对于setsockopt()，指针，指向存放选项待设置的新值的缓冲区。获得或者是设置套接字选项.根据选项名称的数据类型进行转换。
##### 5.optlen：optval缓冲区长度。
