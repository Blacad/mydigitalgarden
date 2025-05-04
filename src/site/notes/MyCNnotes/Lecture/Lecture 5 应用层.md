---
{"dg-publish":true,"permalink":"/my-c-nnotes/lecture/lecture-5/","dgPassFrontmatter":true}
---


# 1 概述
---
- 应用进程通信方式
	- CS
	- BS
	- P2P
- 服务器进程工作方式
	- 循环方式(iterative mode）
	- 并发方式(concurrent mode)
	- 无连接循环方式服务
		-  使用无连接的UDP服务进程通常都工作在循环方式，即一个服务进程在同一时间只能向一个客户进程提供服务。(顺序服务)
	- 面向连接的并发方式服务
		- 面向连接的TCP服务进程通常都工作在并发服务方式，服务进程在同一时间可同时向多个客户进程提供服务。(并发服务)


# 2 域名系统
---
- 早期的域名采用Hosts.txt
- 改进Hosts.txt，采用了一种层次的、基于域的命名模式，并使用分布式数据库系统实现即DNS
- 域名系统（DNS，Domain Name System）是互联网重要的基础设施之一，向所有需要域名解析的应用提供服务，主要负责将可读性好的域名映射成IP地址
- Internet采用层次结构的命名树作为主机的名字，并使用分布式的域名系统 DNS。Internet的DNS是一个联机分布式数据库系统

- 域名服务器
	- 一个名字服务器所负责或管辖（有权限的）范围称为管辖区(zone) ，简称为区
	- 管辖区是域名“域”的子集。管辖区可以小于或等于域，但不可能大于域
	- 类别
		- 权威名字服务器(authoritative name server)
		- 递归解析器(recursive resolver)/递归服务器
	- 根服务器 root name server
		- 每个根服务器都知道所有的顶级域名服务器的域名及其IP地址
		- 根服务器并不直接把主机用户所查的域名转换成IP地址
		- 根服务器共有13套(不是13台机器)，这些根服务器相应的域名分别是： a.rootservers.net － m.rootservers.net
		- 更改根服务器数据只在a.rootservers.net上进行，然后同步到另外12套中，这样既能保证数据一致性，也提高了域名服务可靠性
		- 每套都可以有多个镜像(mirrored)根服务器，其内容定期与上述对应的根服务器同步。注意，同步需要一定的时间才能完成
	- 顶级域名字服务器 TLD name server
		- 顶级域(TLD)名字服务器负责管理在该顶级域名服务器注册的所有二级域名
	- 二级域名字服务器 second-level Domain name server --- 分zone
		- 每一个主机都必须在某个二级域名字服务器处注册登记。因此二级域名字服务器知道其管辖的主机名应当转换成什么IP地址
	- 递归解析器/递归服务器
- www.zju.edu.cn 四级.三级.二级.顶级
- 域名解析
	- ==DNS请求报文 --- UDP数据报, 端口号为53==
	- 主机向递归解析器/本地域名字服务器的查询一般采用递归查询
	- 递归解析器/本地域名字服务器向根服务器可以采用递归查询，但一般优先采用迭代查询
	- 递归查询是托管式的查询，迭代查询是自营式的查询
	- 主机优先向 本地域名字服务器查询，接着向根服务器查询(注意不是向二级域名服务器查询)
	- ![Pasted image 20250103153619.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103153619.png)
	- ![Pasted image 20250103154220.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103154220.png)
- 域名查询和响应
	- 资源记录部分是DNS报文格式的最后3个字段，只有在DNS响应报文中才出现 ，包括 回答问题区域字段、权威名字服务器区域字段、附加信息区域字段。这3个字段都采用资源记录的格式。
	- DNSSEC
	- ![Pasted image 20250103153858.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103153858.png)

- 域名系统高速缓存
	- 域名服务器广泛使用高速缓存，用来存放最近查询过的域名以及从何处获得域名映射信息的记录

- 域名系统隐私
	- QNAME


# 3 电子邮件
---
- 电子邮件系统体系结构
- 用户代理 与 传输代理
- 邮件传输
	- ==SMTP 基于 TCP 使用端口25==
	- 直接投递: 发送端直接到接收端
	- SMTP的3个阶段：连接建立、邮件传送、连接关闭
	- 命令/响应（以HTTP为例）
		- 命令: ASCII字符串
		- 响应: 状态码+短语
	- SMTP是一个简单的ASCII协议，邮件必须为7位ASCII
	- MIME
- 最后传递
	- ==POP3协议 TCP 端口110==![Pasted image 20250103154838.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103154838.png)
	- ==IMAP协议 端口143==![Pasted image 20250103154928.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103154928.png)
	- ![Pasted image 20250103155101.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103155101.png)
	- ![Pasted image 20250103154709.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103154709.png)
	- ![Pasted image 20250103154733.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103154733.png)
	- ![Pasted image 20250103154751.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103154751.png)
- Webmail![Pasted image 20250103155220.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103155220.png)
# 4 WWW
----
- WWW=World Wide Web=万维网
- HTTP服务器和客户端，以及它们之间执行的HTTP协议
- WWW体系结构与协议
	- 服务器
		- Web页面（HTML文档）：包含到多种对象或链接
		- Web对象（包括：静态对象和动态对象）：可以是 HTML文档、 图像文件、视频文件、声音文件、脚本文件等
		- 对象用URL（统一资源定位符）编址：协议类型://主机名:端口//路径和文件名
		- `说明：端口大多数情况会省略，浏览器会帮你补全端口`
	- 客户端
		- 发出请求、接收响应、解释HTML文档并显示
		- 有些对象需要浏览器安装插件

- WWW性能提升
	- 缓存
	- 多线程
	- 前端
- Web 对象
	- 静态对象与静态网页
	- 动态对象与动态网页
		- 动态Web
			- CGI --- 运行在server
				- ![Pasted image 20250103155815.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103155815.png)
			- 脚本语言+数据库技术 php、asp、aspx ---- 运行在server
				- ![Pasted image 20250103155751.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103155751.png)
				
				- ![Pasted image 20241212100750.png](/img/user/MyCNnotes/assets/Pasted%20image%2020241212100750.png)
			- 客户端动态网页 js ---- 浏览器内嵌引擎，客户端运行
			- AJAX 一种框架，使用js，将几种动态Web技术整合
			- ![Pasted image 20250103155941.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103155941.png)
	- 链接


## 4.1 HTTP

- 超文本传输协议==HTTP（ HyperText Transfer Protocol）在传输层通常使用TCP协议，缺省使用TCP的80端口==
- HTTP为无状态协议，服务器端不保留之前请求的状态信息
- HTTP 发展 HTTP 1.0 --- HTTP 3.0
- HTTP 1.x的发展
	- HTTP 1.0 执行时，由于 HTML中的图片也是 url，因此获取每一张图片我们都需要向该图片的所在的服务器建立连接，这样太慢
	- HTTP 1.1 增加持久连接的方式，这样对获取同一个服务器的图片时不用多次建立连接，但是一次请求和返回只能返回一个object
	- HTTP 1.1 pipeline 有增加流水线的功能，一次请求和返回可以包含多个objects
	- ![Pasted image 20250103160051.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103160051.png)
- HTTP 报文结构
	- 状态码![Pasted image 20250103160249.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103160249.png)
- Web 缓存技术 与 Web 代理
	- 浏览器缓存 --- 在浏览器主机保存用户访问过的服务器Web页副本 --- 客户端的缓存
		- 解决：保证Web页副本与原始服务器是一致的
	- Web代理服务器缓存 --- ISP安装Web代理缓存服务器，保存ISP客户访问过的服务器Web页副本，副本可以供ISP的所有客户访问，提高访问服务器的Web页效率 --- 中转站式的缓存![Pasted image 20250103160402.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103160402.png)
	- 启发式策略 和 询问式策略来看缓存的Web是否过期![Pasted image 20250103160448.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103160448.png)
	- ![Pasted image 20250103160543.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103160543.png)
- Web 安全与隐私
	- 每个请求头中包含关键字authorization，这样太麻烦了而且有一定危险性引入cookie
	- 在第一次连接建立时将cookie保存在用户磁盘，之后用户发送数据将cookie带上，服务器就知道是谁![Pasted image 20250103160857.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103160857.png)
	- cookie只是文本，可能能跟踪用户网络浏览痕迹，泄露用户隐私，但是不可能嵌入恶意可执行程序

# 5 流式音频和视频
---
- 常见流媒体服务
	- 点播
	- 直播
	- 实时交互
- 基本概念
	- 连续媒体（音视频）经压缩编码、数据打包后，经过网络发送给接收方；接收方对数据进行重组、解码和播放
	- 特性
		- 端到端时延约束
		- 时序性约束：流媒体数据必须按照一定的顺序连续播放
		- 具有一定程度的容错性：丢失部分数据包也可完成基本功能
- 数字音视频与编码
	- ==MPEG==视频压缩
		- 摄像机固定不变，演员慢慢走来走去：从前一帧中减去当前帧，对两帧之差运行JPEG算法
		- 摄像机在推拉移动：需要某种方法来补偿这种运动，这正是MPEG擅长的
	- MPEG的三种帧
		- 帧内编码帧（I帧）：包含了压缩的静止图片（帧内编码，用JPEG来压缩静止图像）
		- 预测帧（P帧）：是与前一帧的逐块差值（帧间编码，消除跨帧的冗余度）
		- 双向帧（B帧）：是与前一帧和后一帧的逐块差值（帧间编码）
		- 没有I帧，P帧和B帧就无法解码
- 流式存储媒体
	- ![Pasted image 20250103161506.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103161506.png)
	- 发送端以恒定速率产生数据分组，网络传输后需要应对网络传输的抖动特性![Pasted image 20250103161727.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103161727.png)
	- 客户端缓冲区![Pasted image 20250103161634.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103161634.png)

- 直播与实时音视频
	- 信令协议，对建立的连接起控制作用，如==RTSP==，既可在 TCP 上传送，也可在 UDP 上传送，本身并不传送数据，是一个多媒体播放控制协议![Pasted image 20250103161924.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103161924.png)
	- 数据分组传送协议，使音/视频能够以时延敏感属性传送，如==RTP/RTCP==，RTP实时应用提供端到端的数据传输，但不提供任何服务质量的保证，使用UDP；RTCP 是与 RTP 配合使用的控制协议，服务质量的监视与反馈、媒体间的同步、播组中成员的标识，使用UDP![Pasted image 20250103162045.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103162045.png)
	- WebRTC
	- ![Pasted image 20250103161815.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103161815.png)
- 流媒体动态自适应传输
	- DASH动态自适应流媒体传输协议
		- DASH中普遍使用的自适应码率ABR![Pasted image 20250103162232.png](/img/user/MyCNnotes/assets/Pasted%20image%2020250103162232.png)
	- SVC可扩展视频编码

# 6 内容分发
----
- 服务器群和Web代理
	- 单个大型服务器，单点故障、网络拥塞等问题
- 内容分发网络CDN 
	- 相当于是分布式的服务集群，例如杭州有个服务器、北京有个服务器，你在北京就用北京的，在杭州就用杭州的
	- 一种Web缓存系统，靠近网络边缘（用户）提供内容服务
	- 目前提供更丰富的服务，包括静态内容、流媒体、用户上传视频等
	- DNS重定向实现CDN

- 网络实现内容分发P2P
	- P2P文件分发协议：BitTorrent --- 可以理解成一份文件在下载过它的客户端上肯定都会有一份，那么当其他客户端请求该文件时，可以向不同的下载过该文件的客户端请求对应的文件
		- 文件被划分为256Kb大小的块
		- 具有种子(torrents)的节点发送或接收文件
	- 跟踪器tracker: 负责帮助节点获取其他节点的信息
	- 种子torrent: 交换文件块的节点
	- ==分布式哈希表（Distributed Hash Tables ，DHTs) 是一个完全分布式索引，可扩展到多客户端（或实体）==


# 7 其它应用层协议
----
- Telnet协议使用C/S方式，使用==TCP==连接通信，服务器进程默认监听==TCP23端口==
- FTP文件传输协议，使用C/S方式实现，使用==TCP==连接通信，主进程或称控制连接使用==TCP21端口==，数据传输进程使用==TCP20端口==
- TFTP类似停止-等待协议，每发送完一个文件块后就等待对方的确认，确认时应指明所确认的块编号，使用==UDP==，占用==UDP端口号69==
- SNMP网络管理系统，使用C/S方式，使用==UDP协议==，代理运行服务器端进程在==UDP端口161==，管理器运行客户端进程在==UPD端口162==