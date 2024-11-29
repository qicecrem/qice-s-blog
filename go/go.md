并发：多线程在一个核的cpu上运行
并行：多线程在多个核的cpu上运行
Go可以充分发挥多核优势
协程：用户态，轻量级线程，栈KB级别
线程：内核态，线程可以跑多个协程，栈MB级别
通过通信共享内存
Channel：
  make（chan 元素类型，[缓冲大小]）
    无缓冲通道 make(chan int)
    有缓冲通道 make（chan int ，2）
WaitGroup：
   是Go语言中用于等待一组goroutine完成的同步原语。它的工作原理像是一个计数器
   Add(delta int)
  增加计数器的值
  必须在goroutine启动前调用
  可以一次添加多个计数

  Done()
减少计数器的值
相当于 Add(-1)
通常通过 defer 调用确保执行

Wait()
阻塞直到计数器变为0
用在主goroutine中等待其他goroutine完成

依赖管理：
GOPATCH：下载所有的依赖到源代码文件中
问题：无法实现package的多版本控制
Go Vendor
项目目录下增加vendor文件，所有依赖包副本放在￥ProgectRoot/vendor
依赖寻址方式 vendor =》GOPATH
通过每个项目引入一份依赖的副本，解决多个项目需要同一个package依赖的冲突问题
问题：
无法控制依赖的版本
Go Module
通过go.mod文件管理依赖包版本
通过go mod指令工具管理依赖包
go get example.org/pkg :
@update 默认
@none    删除依赖
@v1.1.2 tag版本，语义版本
@23dfdd5  特定的commit
@master 分支的最新commit

go mod：
init 初始化，创建go.mod文件
download 下载模块到本地缓存
tidy 增加需要的依赖，删除不需要的依赖

依赖管理三要素：
配置文件，描述依赖   go.mod
中心仓库管理依赖     Proxy
本地工具           go get/mod

编码原则
简单性
消除“多余的复杂性”，以简单清晰的逻辑编写代码
不理解的代码无法修复改进
可读性
代码是写给人看的，而不是机器
编写可维护代码的第一步是确保代码可读
生产力
团队整体工作效率非常重要

注释：
 公共符号始终要注释
 包中声明的每个公共的符号变量、常量、函数以及结构都需要添加注释
任何既不明显也不简短的公共功能必须予以注释
无论长度或复杂程度如何对库中的任何函数都必须进行注释

注释应该做的
注释应该解释代码作用
注释应该解释代码如何做的
注释应该解释代码实现的原因
注释应该解释代码什么情况会出错

性能优化建议：
slice 预分配内存  尽可能在使用make（）初始化切片时提供容量信息
map 预分配内存
不断向map中添加元素的操作会触发map的扩容
提前分配好空间可以减少内存拷贝和Rehash的消耗
建议根据实际需求提前预估好需要的空间
字符串处理 
使用+拼接性能最差，strings.Builder，bytes.Buffer 相近，strings.Buffer 更快分析
字符串在Go语言中是不可变类型，占用内存大小是固定的使用+每次都会重新分配内存
strings.Builder，bytes.Buffer底层都是byte数组内存扩容策略，不需要每次拼接重新分配内存
使用空结构体节省内存
空结构体 struct{} 实例不占据任何的内存空间可作为各种场景下的占位符使用
节省资源
空结构体本身具备很强的语义，即这里不需要任何值，仅作为占位符
实现Set，可以考虑用map来代替
对于这个场景，只需要用到map 的键，而不需要值
即使是将map的值设置为bool 类型，也会多占据1个字节空间
使用atomic包
锁的实现是通过操作系统来实现，属于系统调用 atomic操作是通过硬件实现，效率比锁高
sync.Mutex应该用来保护一段逻辑，不仅仅用于保护一个变量
对于非数值操作，可以使用atomic.Value，能承载一个interface{}

性能调优原则
要依靠数据不是猜测
要定位最大瓶颈而不是细枝未节
不要过早优化不要过度优化

性能分析工具 pprof使用
搭建 pprof实践项目 
https://github.com/wolfogre/go-pprof-practice 
项自提前理入了一些炸弹代码，产生可观测的性能问题

pprof是Go语言内置的性能分析工具，它可以帮助我们分析程序的CPU使用情况、内存分配等。通过pprof，我们可以生成和查看性能分析数据，找到程序中的性能瓶颈，进而进行优化。
pprof是Go语言标准库的一部分，因此在安装Go语言时会自动包含pprof工具。基本的使用步骤如下：导入net/http/pprof包
在程序中启动HTTP服务，监听分析数据：
编译并运行你的Go程序：
生成分析文件：go tool pprof http://localhost:6060/debug/pprof/profile?seconds=30
 CPU性能分析
go tool pprof命令执行完成后会生成CPU性能分析文件保存到本地，并自动进入分析操作的终端界面。退出后可以使用pprof工具再次进行查看：
进入pprof的交互界面后，可以使用以下命令进行分析：
top：显示消耗CPU时间最多的函数。
list function_name：显示特定函数的详细信息。
web：生成火焰图并在浏览器中查看。
除了CPU分析外，pprof还可以生成内存使用情况的分析文件：go tool pprof http://localhost:6060/debug/pprof/heap
 cpu:
 go tool pprof "http://localhost:6060/debug/pprof/profile?seconds=10"
 命令：topN 查看占用资源最多的函数
      flat 当前函数本身的执行耗时
      flat% flat占cpu总时间的比例
      sum% 上面每一行那的flat%总和
      cum 指当前函数加上其调用函数的总耗时
      cum% cum占cpu总时间的比例
    flat==cum，函数没有调用其他函数
    flat==0 ，函数中只有其他函数的调用
      web  调用关系可视化
Heap 堆内存：
go tool pprof -http=:8080 "http://localhost:6060/debug/pprof/heap"
alloc_objects：程序累计申请的对象数 
inuse_objects：程序当前持有的对象数 
alloc_space：程序累计申请的内存大小
inuse_space：程序当前占用的内存大小

goroutine-协程
go tool pprof -http=:8080 "http://localhost:6060/debug/pprof/goroutine"
火焰图：
由上到下表示调用顺序
每一块代表一个函数，走越长代表占用CPU的时间更长
火焰图是动态的，支持点击块进行分析
mutex-锁
go tool pprof -http=:8080 "http://localhost:6060/debug/pprof/mutex"
block-阻塞
go tool pprof -http=:8080 "http://localhost:6060/debug/pprof/block"

pprof-采样过程和原理
 cpu
    采样对象：函数调用和它们占用的时间
    采样率：100次/秒，固定值
    采样时间：从手动启动到手动结束
    操作系统
     每10ms向进程发送一次SIGPROF信号 
    进程
     每次接收到SIGPROF会记录调用堆栈
    写缓冲
     每100ms读取已经记录的调用栈并写入输出流

Heap-堆内存
  采样程序通过内存分配器在堆上分配和释放的内存，记录分配/释放的大小和数量
  采样率：每分配512KB记录一次，可在运行开头修改，1为每次分配均记录
  采样时间：从程序运行开始到采样时
  采样指标：alloc_space，alloc_objects,inuse_space，inuse_objects 
  计算方式：inuse=alloc-free
  
Goroutine-协程 & ThreadCreate-线程创建
Goroutine
  记录所有用户发起且在运行中的goroutine（即入口非runtime开头的）runtime.main的调用栈信息
ThreadCreate
  记录程序创建的所有系统线程的信息
 Goroutine ： Stop The World --> 遍历allg切片 --> 输出创建g的堆栈 -- > Start TheWorld
 ThreadCreate:  Stop The World --> 遍历allm链表 --> 输出创建m的堆栈 --> Start The World

Block-阻塞& Mutex-锁
 阻塞操作
   采样阻塞操作的次数和耗时
   采样率：阻塞耗时超过阈值的才会被记录 1为每次阻塞均记录
锁竞争
   采样争抢锁的次数和耗时
   采样率：只记录固定比例的锁操作，1为每次加锁均记录














