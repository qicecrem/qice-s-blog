请求行/状态行
请求头/响应头
请求体/响应体

HTPP1：队头阻塞 传输效率低 明文传输不安全
HTTP2： 多路复用  头部压缩 二进制协议
QUIC：基于UDP实现  解决队头阻塞 加密减少握手次数  支持快速启动
应用层设计：提供合理的api
  可理解性
  简单性
  冗余性
  兼容性
  可测性
  可见性
中间件设计：
  中间件需求：
    配合Handler实现一个完整的请求处理生命周期
    拥有预处理逻辑和后处理逻辑
    可以注册多中间件
    对上层模块用户逻辑模块易用
  洋葱模型：
    适合场景：
      日志记录
      性能统计
      安全控制
      事务处理
      异常处理
  调用链：
    适用场景：
       不调用Next：初始化逻辑且不需要在同一调用栈
       调用Next：后处理逻辑后需要在同一调用栈上
路由设计：
  框架路由实际上就是为URL匹配对应的处理函数
    静态路由：/a/b/c 
    参数路由：/a/:id/c  /*all
    路由修复：/a/b <-> /a/b/
    冲突路由及优先级：/a/b  ， /：id/
    匹配Http方法
    多处理函数：方便添加中间件 
  map[string]handlers
  前缀匹配树

协议层：抽象出合适的接口
网络层设计：网络模型
  BIO
  NIO（netpoll）





  Host管理
  主机表： 
     Host-> ip映射
    问题：
      流量和负载：用户规模指数级增长，文件大小越来越大，统一分发引起较大的网络流量和cpu负载
      名称冲突：无法保证主机名称的唯一性，同名主机添加导致服务故障
      时效性：分发靠人工上传，时效性太差
  使用域名系统替换hosts文件
    域名空间：
      域名空间被组织成树形结构
      名空间通过划分zone的方式进行分层授权管理
      全球公共域名空间仅对应一棵树根域名服务器：查询起点
      域名组成格式：[a-zA-Zo-9_-]，以点划分label
    顶级域gTLD：general Top-level Domains：.gov政府  .edu教育  .com商业  .mil军事  .org非盈利组织
域名购买与配置迁移：
  修改配置：清空etc/hosts
            配置/etc/resolv.conf中nameservers为公共DNS迁移原配置，通过控制台添加解析记录 
建设外部网站：
   方案：租赁一个外网ip，专用于外部用户访问门户网站，将www.example.com解析到外网ip 100.1.2.3，将该ip绑定到一台物理机上，并发布公网route，用于外部用户访问。

自建DNS服务器
  问题背景：
    内网域名的解析也得出公网去获取，效率低下
    外部用户看到内网ip 地址，容易被 hacker 攻击
    云厂商权威DNS容易出故障，影响用户体验
    持续扩大公司品牌技术影响力，使用自己的DNS系统
  DNS查询过程：

  DNS记录类型：
   A/AAAA：IP指向记录，用于指向IP，前者为IPv4记录，后者为IPv6记录
   CNAME：别名记录，配置值为别名或主机名，客户端根据别名继续解析以提取IP地址
   TXT：文本记录，购买证书时需要
   MX：邮件交换记录，用于指向邮件交换服务器
   NS：解析服务器记录，用于指定哪台服务器对于该域名解析
   SOA记录：起始授权机构记录，每个zone有且仅有唯一的一条SOA记录，SOA是描述zone属性以及主要权威服务器的记录

接入HTTPS协议
  对称加密和非对称加密
    对称加密：一份密钥
    非对称加密：公钥和私钥
  SSL的通信过程
   client random
   server random
   premaster secret
   加密算法协商
  证书链

接入全站加速
   静态加速 CDN
     解决服务器端的“第一公里”问题
     缓解甚至消除了不同运营商之间互联的瓶颈造成的影响
     减轻了各省的出口带宽压力
     优化了网上热点内容的分布
  动态加速 DCDN
    针对POST等非静态请求等不能在用户边缘缓存的业务，基于智能选路技术，从众多回源线路中择优选择一条线路进行传输
4层负载均衡
  基于IP+端口，利用某种算法将报文转发给某个后端服务器，实现负载均衡地落到后端服务器上。
  三个主要功能：
    解耦VIP和rs
    NAT
    防攻击：syn proxy
 常见的调度算法原理：
  RR轮询：Round Robin，将所有的请求平均分配给每个真实服务器RS 
  加权RR轮询：给每个后端服务器一个权值比例，将请求按照比例分配
  最小连接：把新的连接请求分配到当前连接数最小的服务器　
  五元组hash：根据sip、sport、proto、dip、dport对静态分配的服务器做散列取模
  缺点：当后端某个服务器故障后，所有连接都重新计算，影响整个hash 环
  一致性hash：只影响故障服务器上的连接session，其余服务器上的连接不受影响
  常见实现方式FULLNAT
    
7层负载均衡：
   Nginx
    模块化设计，较好的扩展性和可靠性
    基于master/worker架构设计
    支持热部署；可在线升级
    不停机更新配置文件、更换日志文件、更新服务器二进制
    较低的内存消耗：1万个keep-alive连接模式下的非活动连接仅消耗2.5M内存
 事件驱动模型


RPC框架
1.1本地函数的调用
  压栈->通过函数指针找到函数->执行函数->返回
1.2 远程函数的调用
  需要解决问题
    函数映射
    数据转换成字节流
    网络传输
1.3RPC概念模型
  User，User-Stub，RPC-Runtime，Server-Stub，Server
1.4 一次RPC的完整过程
 IDL (Interface description language)文件
 IDL通过一种中立的方式来描述接口，使得在不同平台上运行的对象和用不同语言编写的程序可以相互通信

 生成代码
 通过编译器工具把 IDL 文件转换成语言对应的静态库

 编解码
 从内存中表示到字节序列的转换称为编码，反之为解码，也常叫做序列化和反序列化

 通信协议
 规范了数据在网络中的传输内容和格式。除必须的请求/响应数据外，通常还会包含额外的元数据

 网络传输
 通常基于成熟的网络库走TCP/UDP传输

1.5RPC的好处
  单一职责，有利于分工协作和运维开发
  可扩展性强，资源使用率更优
  故障隔离，服务的整体可靠性更高

2.1 分层设计-以Apache Thrift为例
2.2 编解码层-数据格式
 语言特定的格式
 文本格式
 二进制编码
2.5编解码层-二进制编码 
  TLV编码
   -Tag：标签
   -Length 长度
   -Value 值
2.6 编解码层-选型
   兼容性（支持自动增加新的字段，而不影响老的服务，这将提高系统的灵活度）
   通用性（支持跨平台、跨语言）
   性能（从空间和时间两个维度来考虑，也就是编码后数据大小和编码耗费时长）
2.7协议层-概念
   特殊结束符（一个特殊字符作为每个协议单元结束的标示）
   变长协议（以定长加不定长的部分组成，其中定长的部分需要描述不定长的内容长度）
2.8 协议层-协议构造
LENGTH: 数据包大小，不包含自身
HEADER MAGIC: 标识版本信息，协议解析时候快速校验
SEQUENCENUMBER：表示数据包的 seqID，可用于多路复用，单连接内递增　
HEADER SIZE：头部长度，从第14个字节开始计算一直到PAYLOAD前
PROTOCOL ID: 编解码方式，有 Binary 和 Compact 两种
压缩方式，如 zlib 和 snappy
TRANSFORM ID:
INFO ID: 传递一些定制的 meta 信息
PAYLOAD: 消息体
2.9网络通信层-网络库
提供易用API
封装底层 Socket API 连接管理和事件分发
功能
协议支持：tcp、udp 和 uds 等优雅退出、异常处理等
性能
应用层 buffer减少 copy 高性能定时器、对象池等










