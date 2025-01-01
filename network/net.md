# 物理层
**数据**：数据是指传送信息的实体；数据传输方式可分为串行传输和并行传输。  

- 串行传输是指1比特1比特地按照时间顺序传输（远距离通信通常采用串行传输）。  
- 并行传输是指若干比特通过多条通信信道同时传输。  

**信号**：是数据的电气或电磁表现，是数据在传输过程中的存在形式。  

- 模拟数据（信号）：连续变化的数据（或信号）。  
- 数字数据（信号）：取值仅允许为有限的几个离散数值的数据（或信号）。  
- 一个码元就是一个脉冲信号！波特率指的就是1秒能发送多少个码元。  

**信道分类**：  

- 按传输信号形式：分为传送模拟信号的模拟信道和传送数字信号的数字信道。  
- 按传输介质的不同：分为无线信道和有线信道。  

**信道传输信号分类**：  

- 基带传输：基带信号将数字信号1和0直接用两种不同的电压表示，然后送到数字信道上传输。  
- 宽带传输：宽带信号将基带信号进行调制后形成频分复用模拟信号，然后送到模拟信道上传输。  

**通信方式分类**：  

- 单向通信：只有一个方向的通信而没有反方向的交互，仅需要一条信道。例如，无线电广播、电视广播就属于这种类型。  
- 半双工通信：通信的双方都可以发送或接收信息，但任何一方都不能同时发送和接收信息，此时需要两条信道。  
- 全双工通信：通信双方可以同时发送和接收信息，也需要两条信道。  

**奈氏准则**：规定在理想低通（没有噪声、带宽有限）的信道中，为了避免码间串扰，极限码元传输速率为2W波特，其中W是理想低通信道的带宽。  

**香农定理**：  
- 定义为信道的极限数据传输速率= W log2（1 + S/N）（单位为b/s）。  
  - W为信道的带宽，S为信道所传输信号的平均功率，N为信道内部的高斯噪声功率。S/N 为信噪比。  
  - 信噪比=10 log10（S/N）（单位为dB）。  
  - 信道的带宽或信道中的信噪比越大，信息的极限传输速率越高。  

- 对一定的传输带宽和一定的信噪比，信息传输速率的上限是确定的。只要信息传输速率低于信道的极限传输速率，就能找到某种方法来实现无差错的传输。  

- 奈氏准则只考虑了带宽与极限码元传输速率的关系，而香农定理不仅考虑到了带宽，也考虑到了信噪比。这从另一个侧面表明，一个码元对应的二进制位数是有限的。  

**编码**：把数据变换为数字信号的过程；  
**调制**：把数据变换为模拟信号的过程。  

**奈奎斯特定理**：在通信领域，带宽是指信号最高频率与最低频率之差，单位为Hz。因此，将模拟信号转换成数字信号时，假设原始信号中的最大频率为f ，那么采样频率f 必须大于或等于最大频率f 的两倍，才能保证采样后的数字信号完整保留原始模拟信号的信息。  

- 采样是指对模拟信号进行周期性扫描，把时间上连续的信号变成时间上离散的信号。  
- 根据采样定理，当采样的频率大于或等于模拟数据的频带带宽（最高变化频率）的两倍时，所得的离散信号可以无失真地代表被采样的模拟数据。  
- 量化是把采样取得的电平幅值按照一定的分级标度转化为对应的数字值并取整数，这样就把连续的电平幅值转换为了离散的数字量。采样和量化的实质就是分割和转换。  
- 编码是把量化的结果转换为与之对应的二进制编码。  

**电路交换**：  
- 在进行数据传输前，两个结点之间必须先建立一条专用（双方独占）的物理通信路径（由通信双方之间的交换设备和链路逐段连接而成），该路径可能经过许多中间结点。这一路径在整个数据传输期间一直被独占，直到通信结束后才被释放。  

- 电路交换技术分为三个阶段：连接建立、数据传输和连接释放。  

**报文交换**：  
- 数据交换的单位是报文，报文携带有目标地址、源地址等信息。报文交换在交换结点采用的是存储转发的传输方式。  

- 分组交换限制了每次传送的数据块大小的上限，把大的数据块划分为合理的小数据块，再加上一些必要的控制信息（如源地址、目的地址和编号信息等），构成分组（Packet）。  

- 传送数据量大，且传送时间远大于呼叫时，选择电路交换。电路交换传输时延最小。  
- 当端到端的通路有很多段的链路组成时采用分组交换传送数据较为合适。  
- 从信道利用率上看，报文交换和分组交换优于电路交换，其中分组交换比报文交换的时延小，尤其适合于计算机之间的突发式的数据通信。  

**数据报**：  
- 作为通信子网用户的端系统发送一个报文时，在端系统中实现的高层协议先把报文拆成若干带有序号的数据单元，并在网络层加上地址等控制信息后形成数据报分组（即网络层的PDU）。中间结点存储分组很短一段时间，找到最佳的路由后，尽快转发每个分组。不同的分组可以走不同的路径，也可以按不同的顺序到达目的结点。  

**虚电路**：  
- 虚电路方式试图将数据报方式与电路交换方式结合起来，充分发挥两种方法的优点，以达到最佳的数据交换效果。在分组发送之前，要求在发送方和接收方建立一条逻辑上相连的虚电路，并且连接一旦建立，就固定了虚电路所对应的物理路径。  
- 与电路交换类似，整个通信过程分为三个阶段：虚电路建立、数据传输与虚电路释放。  

**物理层的主要任务**可以描述为确定与传输媒体的接口有关的一些特性：  
- **机械特性**：指明接口所用接线器的形状和尺寸、引脚数目和排列、固定和锁定装置等。  
- **电气特性**：指明在接口电缆的各条线上出现的电压的范围。  
- **功能特性**：指明某条线上出现的某一电平的电压表示何种意义。  
- **过程特性**：或称规程特性。指明对于不同功能的各种可能事件的出现顺序。  

**中继器**：  
- 由于存在损耗，在线路上传输的信号功率会逐渐衰减，衰减到一定程度时将造成信号失真，因此会导致接收错误。因此需要中继器在传播途中修复信号失真。  

- 如果某个网络设备具有存储转发的功能，那么可以认为它能连接两个不同的协议。  

- 放大器和中继器都起放大作用，只不过放大器放大的是模拟信号，原理是将衰减的信号放大，而中继器放大的是数字信号，原理是将衰减的信号整形再生。  

- 集线器（Hub）实质上是一个多端口的中继器。  


# 数据链路层
​ 数据链路层在物理层提供服务的基础上向网络层提供服务，将物理层提供的可能出错的物理连接改造为逻辑上无差错的数据链路。基本任务是将源机器中来自网络层的数据传输到目标机器的网络层。
为网络层提供服务：
1.无确认的无连接服务
2.有确认的无连接服务
3.有确认的面向连接服务
封装成帧与透明传输：
帧构成：数据前后添加首部和尾部。帧长=数据长度+首部长度+尾部长度
帧定界：帧首部尾部包含控制信息，其中一个重要作用是确定帧的界限。
帧同步：接收方应能从接收到的二进制比特流中区分出帧的起始与终止。
最大传送单元（MTU）：为了提高帧的传输效率，应当使帧的数据部分的长度尽可能地大于首部和尾部的长度，但每种数据链路层协议都规定了帧的数据部分的长度上限——最大传送单元（MTU）
HDLC协议：用标识位F （01111110）来标识帧的开始和结束。
透明传输：不管所传数据是什么样的比特组合，都应当能在链路上传送。通过不同组帧方式实现透明传输。
流量控制
​ 由于收发双方各自的工作速率和缓存空间的差异，可能出现发送方的发送能力大于接收方的接收能力的现象，这样会导致帧的丢失导致出错。
​ 流量控制实际上就是限制发送方的数据流量，使其发送速率不超过接收方的接收能力。

流量控制在不同层，控制的对象不同。对于数据链路层来说，控制的是相邻两结点之间数据链路上的流量，而对于传输层来说，控制的则是从源端到目的端之间的流量。
在OSI体系结构中，数据链路层具有流量控制的功能。而在TCP/IP体系结构中，流 量控制功能被移到了传输层。

差错控制
​ 由于信道噪声等各种原因，帧在传输过程中可能会出现错误。用以使发送方确定接收方是否正确收到由其发送的数据的方法称为差错控制。
​ 位错指帧中某些位出现了差错。通常采用循环冗余校验（CRC）方式发现位错，通过自动重传请求（Automatic Repeat reQuest, ARQ）方式来重传出错的帧。
​ 帧错指帧的丢失、重复或失序等错误。在数据链路层引入定时器和编号机制，能保证每一帧最终都能有且仅有一次正确地交付给目的结点。

组帧
​ 为了使接收方能正确地接收并检查所传输的帧，发送方必须依据一定的规则把网络层递交的分组封装成帧

字符计数法是指在帧头部使用一个计数字段来标明帧内字符数。目的结点的数据链路层收到字节计数值时，就知道后面跟随的字节数，从而可以确定帧结束的位置（计数字段提供的字节数包含自身所占用的一个字节）。
问题：若计算字段出错，则失去划分帧边界依据，彻底失去帧同步

字符填充的首尾定界符法
​ 字符填充法使用特定字符来定界一帧的开始与结束。如下图所示，控制字符SOH放在帧的最前面，表示帧的首部开始，控制字符EOT表示帧的结束。为了使信息位中出现的特殊字符不被误判为帧的首尾定界符，可在特殊字符前面填充一个**转义字符(ESC)**来加以区分。从而实现透明传输。
注意，转义字符是ASCI码中的控制字符，是一个字符，而非“E”“S”“C”三个字符的组合

零比特填充的首尾标志法
​ 零比特填充法它使用一个特定的比特模式，即01111110来标志一帧的开始和结束。HDLC协议使用该方法。
​ 为了防止误判，发送方的数据链路层在信息位中遇到5个连续的“1”时，将自动在其后插入一个“0”；而接收方做该过程的逆操作，即每收到5个连续的“1"时，自动删除后面紧跟的“0”，以恢复原信息
零比特填充法很容易由硬件来实现，性能优于字符填充法。

违规编码法
​ 利用不会用到的编码方式作为帧的开始与终止。
​ 曼彻斯特编码方法将数据比特“1”编码成“高-低”电平对，将数据比特“0”编码成“低-高”电平对，而**“高-高”电平对和“低一低”电平对在数据比特中是违规**的（即没有采用）。
​ 可以借用这些违规编码序列来定界帧的起始和终止。局域网IEEE802标准就采用了这种方法。
​ 违规编码法不需要采用任何填充技术，便能实现数据传输的透明性，但它只适用于采用冗余 编码的特殊编码环境。
目前较常用的组帧方法是零比特填充法和违规编码法。
纠错编码
​ 纠错方法：在每个要发送的数据块上附加足够的冗余信息，使接收方能够推导出发送方实际送出的应该是什么样的比特串。
海明码：最常见的纠错编码，其原理是在有效信息位中加入几个校验位形成海明码，并把海明码的每个二进制位分配到几个奇偶校验组中。当某一位出错后，就会引起有关的几个校验位的值发生变化，这不但可以发现错位，而且能指出错位的位置，为自动纠错提供依据。
1.确定海明码的位数
设n为有效信息的位数，k为校验位的位数，则信息位n和校验位k应满足n+k≤2^k-1
2.确定校验位的分布
规定校验位Pi在海明位号2i-1的位置上，其余位信息位
3.分组以形成校验关系
每个数据位用多个校验位进行校验，但要满足条件：被校验数据位的海明位号等于校验该数据位的各校验位海明位号之和。校验位不需要再被校验。分组形成的校验关系如下。
4.校验位取值
校验位Pi的值为第i组（由该校验位校验的数据位）所有位求异或
5.海明码的校验原理
每个校验组分别利用校验位和参与形成该校验位的信息位进行奇偶校验检查，构成k个校验方程:
如果要检测 e 个错误，最小码距应该满足：D≥e+1 
如果要纠正 t 个错误，最小码距应满足：D≥2t+1
如果要检测 e 个错误同时纠正 t个错误，最小码距应该满足：D≥e+t+1,(e>=t)

滑动窗口机制
发送窗口：在任意时刻，发送方都维持一组连续的允许发送的帧的序号。
发送窗发送窗口用来对发送方进行流量控制，而发送窗口的大小WT，代表在还未收到对方确认信息的情况下发送方最多还可以发送多少个数据帧。口：在任意时刻，发送方都维持一组连续的允许发送的帧的序号。
接收窗口：接收方也维持一组连续的允许接收帧的序号。
接收窗口是为了控制可以接收哪些数据帧和不可以接收哪些帧。
在接收方，只有收到的数据帧的序号落入接收窗口内时，才允许将该数据帧收下。
若接收到的数据帧落在接收窗口之外，则一律将其丢弃。

单帧滑动窗口与停止-等待协议
在停止-等待协议中，源站每发送完一个帧就停止发送，等待对方的确认，在收到确认后再发送下一个帧。
超时计时器：每次发送一个帧就启动一个计时，超时计时器设置的重传时间应当比帧传输的平均RTT更长。
  发完一个帧后，必须保留它的副本。
  发送的帧交替地用0和1来标识，确认帧分别用ACK0和ACK1来表示，收到的确认帧有误时，重传已发送的帧
发送失败的三种情况：
数据帧丢失或检测到帧出错：数据帧丢失时，或者接收方检测到数据帧有错，不返回ACK，超时重传。
ACK丢失：接收方接收到数据帧，返回ACK时丢失，发送方超时重传。
ACK迟到：接收方收到数据帧后，返回ACK0，但是ACK到达时间超过重传时间，发送方重新发送数据，接收到ACK0时丢失，因为此刻等待ACK1的接收。
信道利用率U= 发送时间/（发送时间+往返时间+传输时间）

多帧滑动窗口与后退N帧协议（GBN）
在后退N帧式ARQ中，发送方无须在收到上一个帧的ACK后才能开始发送下一帧，而是可以连续发送帧。
​ 发送窗口大小>1，接收窗口大小=1。
发送方
上层的调用：上层要发送数据时，发送方先检查发送窗口是否己满，如果未满，则产生一个带序号的帧并将其发送；如果窗口已满发送方可以缓存这些数据，窗口不满时再发送帧。
收到了一个ACK：GBN协议中，对n号帧的确认采用累积确认的方式，标明接收方已经收到n号帧和它之前的全部帧。
超时事件：协议的名字为后退N帧/回退N帧，来源于出现丢失和时延过长帧时发送方的行为。就像在停等协议中一样，定时器将再次用于恢复数据帧或确认帧的丢失。如果出现超时，发送方重传所有己发送但未被确认的帧。
接收方
如果正确按序收到n号帧，那么接收方为n帧发送一个ACK，并将该帧中的数据部分交付给上层。
其余情况都丢弃帧，并为最近按序接收的帧重新发送ACK。
接收方无需缓存任何失序帧，只需要维护一个信息：expectedseqnum（下一个按序接收的帧序号）。
窗口大小
接收窗口为1，可以保证按序接收数据帧。
若采用n比特对帧编号，则其发送窗口的尺寸WT应满足 1＜W_T≤2^n-1  若发送窗口大于2^n-1 则会造成接收方无法分辨新帧和旧帧。
性能分析
优点：因连续发送数据帧而提高了信道利用率
缺点：在重传时必须把原来已经正确传送的数据帧重传，是传送效率降低。
​ 信道的传输质量很差导致误码率较大时，后退N帧协议不一定优于停止-等待协议。

信道划分介质访问控制
频分多路复用（FDM）  用户在相同时间占用不同频率带宽资源。每个子信道分配的带宽可不相同，但它们的总和必须不超过信道的总带宽。在实际应用中为了防止子信道之间的干扰，相邻信道之间需要加入“保护频带”。共享时间。
时分多路复用（TDM）  每一个时分复用的用户在每一个TDM帧占用固定序号的时隙，所有用户轮流占用信道。不会发生碰撞，TDM帧是在物理层传送的比特流所划分的帧，标志一个周期。共享空间
统计时分多路复用（STDM）每一个STDM帧中的时隙数小于连接在集中器上的用户数。各用户有了数据就随时发往集中器的输入缓存，然后集中器按顺序依次扫描输入缓存，把缓存中的输入数据放入STDM帧中，一个STDM帧满了就发出。STDM帧不是固定分配时隙，而是按需动态分配时隙。
波分多路复用（WDM）波分多路复用就是光的频分多路复用，在一根光纤中传输多种不同波长（频率）的光信号，由于波长（频率）不同，所以各路光信号互不干扰，最后再用波长分解复用器将各路波长分解出来。
----
码分多路复用（CDM）
码分多路复用是靠不同的编码来区分各路原始信号的一种复用方式。既共享信道的频率，又共享时间。
码分多址（CDMA）：每个比特时间再划分成m个短的时间槽，称为码片(Chip)，通常m的值是64或128。每个站点指派m位码片序列，发送1时发原码，0时发反码。各个站点码片序列相互正交。
CDMA原理：
假如站点A的码片序列被指派为00011011，则A站发送00011011就表示发送比特1，发送11100100就表示发送比特0。为了方便，按惯例将码片中的0写为-1，将1写为+1，因此A站的码片序列是-1-1-1+1+1-1+1+1。
令向量S表示A站的码片向量，令T表示B站的码片向量。两个不同站的码片序列正交，即向量S和T的规格化内积（Inner Product）为0：S⋅T= 0
任何一个码片向量和该码片向量自身的规格化内积都是1，任何一个码片向量和该码片反码的向量的规格化内积是-1
例：A站码片00011011、B站码片00101110；此时A、B站向量相乘内积为0。
当A站向C站发送数据1时，就发送了向量（-1-1-1+1+1-1+1+1）。
当B站向C站发送数据0时，就发送了向量（+1+1-1+1-1-1-1+1）。
两个向量到了公共信道上就进行叠加，实际上就是线性相加，得到S+T=(0 0 -2 2 0 -2 0 2)
到达C站后，想获得A站数据，就与A站码片S内积化，S ⋅ ( S + T ) = 1 S·(S+T)=1S⋅(S+T)=1，所以A站数据是1；同理，T ⋅ ( S + T ) = − 1 T·(S+T)=-1T⋅(S+T)=−1，所以B站发过来的向量是个反码向量，代表0。

CSMA协议
载波监听多路访问（CSMA）指的是每个站点在发送前都先监听一下共用信道，发现信道空闲后再发送。
监听：当几个站同时在总线上发送数据时，总线上的信号电压摆动值将会增大（互相叠加）。当一个站检测到的信号电压摆动值超过一定门限值时，就认为总线上至少有两个站同时在发送数据，表明产生了碰撞，即发生了冲突。
1-坚持 CSMA
坚持指的是对于监听信道忙之后的坚持。
思想：如果一个主机要发送消息，那么它先监听信道。空闲则直接传输，不必等待。忙则一直监听，直到空闲马上传输。如果有冲突（一段时间内未收到肯定回复），则等待一个随机长的时间再监听，重复上述过程。
优点：只要媒体空闲，站点就马上发送，避免了媒体利用率的损失。
缺点：假如有两个或两个以上的站点有数据要发送，冲突就不可避免。
非坚持CSMA
非坚持指的是对于监听信道忙之后就不继续监听。
思想：如果一个主机要发送消息，那么它先监听信道。空闲则直接传输，不必等待。忙则等待一个随机的时间之后再进行监听。
优点：采用随机的重发延迟时间可以减少冲突发生的可能性。
缺点：可能存在大家都在延迟等待过程中，使得媒体仍可能处于空闲状态，媒体使用率降低。
p-坚持 CSMA
P坚持指的是对于监听信道空闲的处理。
思想：如果一个主机要发送消息，那么它先监听信道。空闲则以p概率直接传输，不必等待；概率1-p等待到下一个时间槽再传输。忙则持续监听直到信道空闲再以p概率发送。若冲突则等到下一个时间槽开始再监听并重复上述过程。
优点：既能像非坚持算法那样减少冲突，又能像1-坚持算法那样减少媒体空闲时间的这种方案。
缺点：发生冲突后还是要坚持把数据帧发送完，造成了浪费。

CSMA/CD 协议
​ 载波监听多路访问/碰撞检测（CSMA/CD）协议是CSMA的改进方案，适用于总线形网络或半双工网络。
​ 碰撞检测就是边发送边监听，如果 监听到了碰撞，则立即停止数据发送，等待一段随机时间后，重新开始尝试发送数据。
工作流程：先听后发，边听边发，冲突停发，随机重发
1）适配器从网络中获得分组，封装成以太帧，缓存等待发送
2）适配器侦听信道，空闲则发送，忙则持续监听，直到空闲发送
3）发送过程中持续检测信道，若检测到碰撞，停止发连并发送一个拥塞信号
4）中止发送后，执行指数退避法确定重传时机
争议期：两端往返传播时延。只要经过2τ（传播时延）时间还没有检测到碰撞，就能肯定这次发送不会发生碰撞。
最小帧长=总线传播时延×数据传输速率×2
以太网规定取51.2μs为争用期的长度。对于10Mb/s的以太网，在争用期内可发送512bit，即64B。
如果只发送小于64B的帧，如40B的帧，那么需要在MAC子层中于数据字段的后面加入一个整数字节的填充字段，以保证以太网的MAC帧的长度不小于64B。

CSMA/CA协议
CSMA/CD协议无法用于无线局域网，因为其无法做到360°全面检测碰撞。会出现隐蔽站问题。
隐蔽站：当A和C都检测不到信号，认为信道空闲时，同时向终端B发送数据帧，就会导致冲突。
载波监听多路访问/碰撞避免（CSMA/CA）：协议的设计要尽量降低碰撞发生的概率。
工作原理：
1）发送数据前，先检测信道是否空闲。
2）空闲则发出RTS（request to send），RTS包括发射端的地址、接收端的地址、下一份数据将持续发送的时间等信息；信道忙则等待。
3）接收端收到RTS后，将响应CTS（clear to send）。CTS帧 ①给源站明确的发送许可；②指示其他站点在预约期内不要发送。
4）发送端收到CTS后，开始发送数据帧（同时预约信道：发送方告知其他站点自己要传多久数据）。
5）接收端收到数据帧后，将用循环冗余码CRC来检验数据是否正确，正确则响应ACK帧。
6）发送方收到ACK就可以进行下一个数据帧的发送，若没有则一直重传至规定重发次数为止（采用二进制指数退避:算法来确定随机的推迟时间）。
帧间间隔（IFS）：为了尽量避免碰撞，802.11规定，所有的站完成发送后，必须再等待一段很短的时间（继续监听）才能发送下一帧。
1）SIFS（短IFS）：最短的IFS，用来分隔属于一次对话的各帧，使用SIFS的帧类型有ACK帧、CTS帧、分片后的数据帧，以及所有回答AP探询的帧等。
2）PIFS（点协调IFS）：中等长度的IFS，在PCF操作中使用。
3）DIFS（分布式协调IFS）：最长的IFS，用于异步帧竞争访问的时延。

以太网逻辑上采用总线形拓扑结构，物理星型结构，以太网中的所有计算机共享同一条总线，信息以广播方式发送。为了保证数据通信的方便性和可靠性，以太网简化了通信流程并使用了 CSMA/CD方式对总线进行访问控制。
​ ①采用**无连接的工作方式，不对发送的数据帧编号，也不要求接收方发送确认，即以太网尽最大努力交付数据，提供的是不可靠服务**，对于差错的纠正则由高层完成；
​ ②发送的数据都使用曼彻斯特编码的信号，每个码元的中间出现一次电压转换，接收端利用这种电压转换方便地把位同步信号提取出来。

VLAN基本概念与基本原理
虚拟局域网（VLAN）可以把一个较大的局域网分割成一些较小的与地理位置无关，逻辑上的VLAN，而每个VLAN是一个较小的广播域。VLAN分割了广播域。
​ 802.3ac标准定义了支持VLAN的以太网帧格式的扩展，称为802.1Q帧。它在以太网帧中插入一个4字节的标识符（插入在源地址字段和类型字段之间），称为VLAN标签，用来指明发送该帧的计算机属于哪个虚拟局域网。
VLAN标签的前两个字节置为0x8100，表示这是一个802.1Q帧。在VLAN标签的后两个字节中，前4位没有用，后12位是该VLAN的标识符VID，它唯一标识了该802.1Q帧属于哪个VLAN。
​ VID的取值范围为0~4095，但0和4095都不用来表示VLAN，因此用于表示VLAN的有效VID取值范围为1~4094。12位的VID可识别4096个不同的VLAN。插入VID后，802.1Q帧的FCS必须重新计算。
​ IEEE 802.1Q帧是由交换机来处理的，而不是由用户主机来处理的。（即主机和交换机之间只交换普通的以太网帧）

广域网不等于互联网。互联网可以连接不同类型的网络（既可以连接局域网，又可以连接广域网），通常使用路由器来连接
​ 广域网与局域网有相同有不同，相似点如下：
广域网和局域网都是互联网的重要组成构件，从互联网的角度上看，二者平等（不是包含关系）
连接到一个广域网或一个局域网上的主机在该网内进行通信时，只需要使用其网络的物理地址

PPP协议
​ 点对点协议（Point–to-Point Protocol，PPP）是使用串行线路通信的面向字节的协议，该协议应用在直接连接两个结点的链路上。不可靠。
特点
1）PPP提供差错检测但不提供纠错功能，只保证无差错接收（通过硬件进行CRC校验）。它是不可靠的传输协议，因此也不使用序号和确认机制。
2）它仅支持点对点的链路通信，不支持多点线路。
3）PPP只支持全双工链路。
4）PPP的两端可以运行不同的网络层协议，但仍然可使用同一个PPP进行通信。
5）PPP是面向字节的，当信息字段出现和标志字段一致的比特组合时，PPP有两种不同的处理方法：若PPP用在异步线路（默认），则采用字符填充法；若PPP用在SONET/SDH等同步线路，则协议规定采用硬件来完成比特填充（和HDLC的做法一样）。

网桥
​ 两个或多个以太网通过网桥连接后，就成为一个更大的以太网，而原来的每个以太网就称为一个网段。网桥工作在链路层的MAC子层，可以使以太网各网段成为隔离开的碰撞域。
​ 网桥根据MAC帧的目的地址对帧进行转发和过滤。当网桥收到一个帧时，并不向所有接口转发此帧，而是先检查此帧的目的MAC地址，然后再确定将该帧转发到哪一个接口，或者是把它丢弃（即过滤）。
冲突域：在同一个冲突域中的每一个节点都能收到所有被发送的帧。简单的说就是同一时间只能有一台设备发送信息的范围。
广播域：网络中能接收任一设备发出的广播帧的所有设备的集合。简单的说如果站点发出一个广播信号，所有能接收到这个信号的设备范围称为一个广播域。

交换机的原理和特点
局域网交换机，又称以太网交换机，以太网交换机实质上就是一个多端口的网桥，工作在数据链路层。
以太网交换机的每个端口都直接与单台主机或另一个交换机相连，通常都工作在全双工方式。
原理：它检测从以太端口来的数据帧的源和目的地的MAC地址，然后与系统内部的动态查找表进行比较，若数据帧的MAC地址不在查找表中，则将该地址加入查找表中，并将数据帧发送给相应的目的端口。
交换机能经济地将网络分成小的冲突域，为每个工作站提供更高的带宽。
特点：
以太网交换机的每个端口都直接与单台主机相连（网桥的端口往往连接到一个网段），并且一般都工作在全双工方式。
以太网交换机同时连通多对端口，使每对相互通信的主机都能像独占通信媒体那样，无碰撞地传输数据。
以太网交换机是一种即插即用设备，其内部的帧的转发表是通过自学习算法自动地逐渐建立起来的。
以太网交换机由于使用专用的交换结构芯片，交换速率较高。
以太网交换机独占传输媒体的带宽。


# 网络层
互联网在网络层的设计思路是，向上只提供简单灵活的、无连接的、尽最大努力交付的数据报服务。也就是说，所传送的分组可能出错、丢失、重复、失序或超时，这就使得网络中的路由器比较简单，而且价格低廉。

使用物理层或数据链路层的中继系统时，只是把一个网络扩大了，而从网络层的角度看，它仍然是同一个网络，一般并不称为网络互连。因此网络互连通常是指用路由器进行网络互连和路由选择。路由器是一台专用计算机，用于在互联网中进行路由选择。

​ TCP/IP体系在网络互连上采用的做法是在网络层采用标准化协议，但相互连接的网络可以是异构的。

路由转发
​ 路由器主要完成两个功能：一是路由选择（确定哪一条路径）；二是分组转发（当一个分组到达时所采取的动作）。
路由选择：指按照复杂的分布式算法，根据从各相邻路由器所得到的关于整个网络拓扑的变化情况，动态地改变所选择的路由。
分组转发：指路由器根据转发表将用户的IP数据报从合适的端口转发出去。
路由表是根据路由选择算法得出的，而转发表是从路由表得出的。转发表的结构应当使查找过程最优化，路由表则需要对网络拓扑变化的计算最优化。在讨论路由选择的原理时，往往不去区分转发表和路由表，而是笼统地使用路由表一词。

拥塞控制
拥塞：在通信子网中，因出现过量的分组而引起网络性能下降的现象称为拥塞。
判断网络是否拥塞方法：观察网络的吞吐量与网络负载的关系
轻度拥塞状态：随着网络负载的增加，网络的吞吐量明显小于正常的吞吐量。
拥塞状态：网络的吞吐量随着网络负载的增大而下降。
死锁状态：网络的负载继续增大，而网络的吞吐量下降到零。
拥塞控制的作用是确保子网能够承载所达到的流量，这是一个全局性的过程，涉及各方面的 行为：主机、路由器及路由器内部的转发处理过程等。单一地增加资源并不能解决拥塞。
流量控制和拥塞控制的区别：
流量控制往往是指在发送端和接收端之间的点对点通信量的控制。流量控制所要做的是抑制发送端发送数据的速率，以便使接收端来得及接收。
而拥塞控制必须确保通信子网能够传送待传送的数据，是一个全局性的问题，涉及网络中所有的主机、路由器及导致网络传输能力下降的所有因素。
拥塞控制的方法：
开环控制：在设计网络时事先将有关发生拥塞的因素考虑周到，力求网络在工作时不产生拥塞。
这是一种静态的预防方法。一旦整个系统启动并运行，中途就不再需要修改。
开环控制手段包括确定何时可接收新流量、何时可丢弃分组及丢弃哪些分组，确定何种调度策略等。所有这些手段的共性是，在做决定时不考虑当前网络的状态。
闭环控制：事先不考虑有关发生拥塞的各种因素，采用监测网络系统去监视，及时检测哪里发生了拥塞，然后将拥塞信息传到合适的地方,以便调整网络系统的运行，并解决出现的问题。
闭环控制是基于反馈环路的概念，是一种动态的方法。

 路由算法和路由协议
 静态路由与动态路由
​ 路由器转发分组是通过路由表转发的，而路由表是通过各种算法得到的。从能否随网络的通信量或拓扑自适应地进行调整变化来划分，路由算法可以分为如下两大类。
静态路由算法（又称非自适应路由算法）。指由网络管理员手工配置的路由信息。
当网络的拓扑结构或链路的状态发生变化时，网络管理员需要手工去修改路由表中相关的静态路由信息。它不能及时适应网络状态的变化，对于简单的小型网络，可以采用静态路由。
动态路由算法（又称自适应路由算法）。指路由器上的路由表项是通过相互连接的路由器之间彼此交换信息，然后按照一定的算法优化出来的，而这些路由信息会在一定时间间隙里不断更新，以适应不断变化的网络，随时获得最优的寻路效果。

 距离-向量路由算法
 1.距离向量算法
  常见的距离-向量路由算法是RIP算法，每个路由器定期与所有相邻路由器交换整个路由表，更新路由项。
​ 这种路由表包含：①每条路径的目的地（另一结点）。②路径的代价（也称距离）。
更新路由表的情况：
被通告一条新的路由，该路由在本结点的路由表中不存在，此时本地系统加入这条新的路由。
路由信息有一条较短的距离，发来的路由信息中有一条到达某个目的地的路由，该路由与当前使用的路由相比，有较短的距离。此时，就用经过发送路由信息的结点的新路由替换路由表中到达那个目的地的现有路由。
问题：大的通信子网导致大的更新报文，路由信息变得很大。
2.RIP（应用层 基于UDP）
RIP是一种分布式的基于距离向量的路由选择协议，其最大优点就是简单。
协议规定：
1）网络中的每一个路由器都要维护从它自己到其他每一个目的网络的距离记录（距离向量）
2）距离也称为跳数，规定从一路由器到直接连接的跳数为1。每经过一个路由器，跳数加1
3）RIP认为好的路由就是它通过的路由器的数目少，即优先选择跳数少的路径
4）RIP允许一条路径最多只能包含15个路由器（即最多允许15跳）距离等于16时，表示网络不可到达
5）RIP默认在任意两个使用RIP的路由器之间每30s广播一次RIP路由更新信息，动态维护路由表
6）在RIP中不支持子网掩码的RIP广播，RIP中每个网络的子网掩码必须相同。在RIP2中，支持变长子网掩码和CIDR
RIP的特点：
1）仅和相邻路由器交换信息。
2）路由器交换的信息是当前路由器所知道的全部信息，即自己的路由表。
3）按固定的时间间隔交换路由信息，如每隔30秒。
距离向量算法：每个路由表项目都有三个关键数据：< 目的网络 N ，距离 d ，下一跳路由器地址 X > 
1）对地址为X的相邻路由器发来的报文，修改此报文中的所有项目【'下一跳’的地址都改为X，把所有’距离’的值+1】
2）对修改后的报文中的每一个项目，进行以下步骤：
①当原来的路由表中没有目的网络N，则把该项目添加到路由表中
②当原来的路由表中有目的网络N，且下一跳路由器地址【是X】时，用收到的项目替换原路由表中的项目
③当原来的路由表中有目的网络N，且下一跳路由器地址【不是X】，若收到的项目中的距离d<路由表中的距离，用收到的项目替换原路由表中的项目，否则什么也不做
3）如果180s（默认超时时间是180s）没有收到相邻路由器的更新路由表，把此相邻路由器记为不可达路由，把距离置为16
RIP优点：实现简单、开销小、收敛过程较快
RIP缺点：好消息传得快，坏消息传得慢
1）RIP限制了网络的规模，它能使用的最大距离为15（16表示不可达）。
2）路由器之间交换的是路由器中的完整路由表，因此网络规模越大，开销也越大。
3）网络出现故障时，会出现慢收敛现象（即需要较长时间才能将此信息传送到所有路由器），使更新过程的收敛时间长。

链路状态路由算法
1.链路状态路由算法
链路状态路由算法要求每个参与该算法的结点都具有完全的网络拓扑信息，它们执行下述两项任务。
第一，主动测试所有邻接结点的状态。两个共享一条链接的结点是相邻结点，它们连接到同一条链路，或者连接到同一广播型物理网络。
第二，定期地将链路状态传播给所有其他结点（或称路由结点）。
典型的链路状态算法是OSPF算法
特征：
向本自治系统中所有路由器发送信息（洪泛法）。
洪泛法，即路由器通过所有端 口向所有相邻的路由器发送信息。可靠的洪泛法是在收到更新分组后要发送确认（收到重复的更新分组只需要发送一次确认）
发送的信息是与路由器相邻的所有路由器的链路状态。OSPF算法中，链路状态的“度量”主要用来表示费用、距离、时延、带宽等。
只有链路状态发生变化，才向所有路由器发送信息。
优点：
每个路由结点使用同样的原始状态数据独立的计算路径。
链路状态不加改变的传播，该算法易于查找故障。
仅运载来自单个结点关于直接链路的信息，其大小与网络中的路由结点数目无关，有更好的规模可伸展性。
链路状态路由算法可以用于大型的或路由信息变化聚敛的互联网环境。因为一个路由器的链路状态只涉及相邻路由器的连通状态，而与整个互联网的规模并无直接关系。
2.OSPF（网络层 基于ip）
特点：
1）OSPF对不同的链路可根据IP分组的不同服务类型（TOS）而设置成不同的代价。因此，OSPF对于不同类型的业务可计算出不同的路由，十分灵活。
2）如果到同一个目的网络有多条相同代价的路径，那么可以将通信量分配给这几条路径。这称为多路径间的负载平衡。
3）所有在OSPF路由器之间交换的分组都具有鉴别功能，因而保证了仅在可信赖的路由器之间交换链路状态信息。
4）支持可变长度的子网划分和无分类编址CIDR。
5）每个链路状态都带上一个32位的序号，序号越大，状态就越新。
OSPF的基本工作原理：
为了使OSPF能够用于规模很大的网络，OSPF将一个自治系统再划分为若干个更小的范围，叫做区域（area）。每一个区域都有一个32位的区域标识符（用点分十进制表示）。
划分区域后，洪泛法交换链路状态信息的范围局限于每一个区域，减少网络的通信量。在一个区域内部的路由器只知道本区域的完整网络拓扑，而不知道其他区域的网络拓扑的情况。每个区域路由器应不超200个。
OSPF采用层次结构的区域划分，使每个区域能够与其他区域通信。
在上层的区域叫做主干区域backbone area）。主千区域的标识符规定为0.0.0.0。主干区域的作用是用来连通其他在下层的区域。
从其他区域来的信息都由区域边界路由器（area border router）进行概括。如路由器R3，R4和R7。
在主干区域内的路由器叫做主干路由器（backbone router），如R3，R4，R5，R6和R7。
在主干区域内需要一个路由器和本自治系统外的其他自治系统交换路由信息。这样的路由器叫做自治系统边界路由器，如R6。
​ 采用层次划分后，使每一个区域内部交换路由信息的通信量大大减小，因而使OSPF协议能够用于规模很大的自治系统中。
OSPF分组类型：
1）问候分组，用来发现和维持邻站的可达性。
2）数据库描述分组，向邻站给出自己的链路状态数据库中的所有链路状态项目的摘要信息。
3）链路状态请求分组，向对方请求发送某些链路状态项目的详细信息。
4）链路状态更新分组，用洪泛法对全网更新链路状态。
5）链路状态确认分组，对链路更新分组的确认。
​ 通常每隔10秒，每两个相邻路由器要交换一次问候分组，以便知道哪些站可达。路由器刚开始工作时，OSPF让每个路由器使用数据库描述分组和相邻路由器交换本数据库中已有的链 路状态摘要信息。然后，路由器使用链路状态请求分组，向对方请求发送自己所缺少的某些链路 状态项目的详细信息。经过一系列的这种分组交换，就建立了全网同步的链路数据库。
OSPF链路状态路由算法：
1.每个路由器发现它的邻居结点【HELLO问候分组】，并了解邻居节点的网络地址。
2.设置到它的每个邻居的成本度量metric。
3.构造【DD数据库描述分组】，向邻站给出自己的链路状态数据库中的所有链路状态项目的摘要信息。
4.如果DD分组中的摘要自己都有，则邻站不做处理；如果有没有的或者是更新的，则发送【LSR链路状态请求分组】请求自己没有的和比自己更新的信息。
5.收到邻站的LSR分组后，发送【LSU链路状态更新分组】进行更新。
6.更新完毕后，邻站返回一个【LSAck链路状态确认分组】进行确认。
只要一个路由器的链路状态发生变化：
5.泛洪发送【LSU链路状态更新分组】进行更新。
6.更新完毕后，其他站返回一个【LSAck链路状态确认分组】进行确认
7.使用Dijkstra根据自己的链路状态数据库构造到其他节点间的最短路径

层次路由
网络规模扩大，路由器的路由表成比例地增大。这样会消耗大量资源，因此路由选择应按照层次的方式进行。
因特网将整个互联网划分为许多较小的自治系统（AS）（注意一个自治系统中包含很多局域网）。
每个自治系统有权自主地决定本系统内应采用何种路由选择协议。如果两个自治系统需要通信，那么就需要一种在两个自治系统之间的协议来屏蔽这些差异。因此将选择协议分为以下两种类型：
内部网关协议（IGP）：也称域内路由选择，指一个自治系统内部所使用的路由选择协议，具体的协议有RIP和OSPF等。
外部网关协议（EGP）：也称域间路由选择，指自治系统之间所使用的路由选择协议，在不同自治系统的路由器之间交换路由信息，并负责为分组在不同自治系统之间选择最优的路径。具体的协议有BGP。
使用层次路由时，OSPF将一个自治系统再划分为若干区域（Area），每个路由器都知道在本区域内如何把分组路由到目的地的细节，但不用知道其他区域的内部结构。因而使OSPF协议能够用于规模很大的自治系统中。
2.BGP（外部网关协议） 应用层 TCP封装
边界网关协议（Border Gateway Protocol，BGP）是不同自治系统的路由器之间交换路由信息的协议，是一种外部网关协议。
目的：力求寻找一条能够到达目的网络且比较好的路由（不能兜圈子）
困难：
互联网的规模太大，使得自治系统AS之间路由选择非常困难
自治系统AS之间的路由选择必须考虑有关策略。
交换过程：
BGP所交换的网络可达性的信息就是要到达某个网络所要经过的一系列AS。
当BGP发言人互相交换了网络可达性的信息后，各BGP发言人就根据所采用的策略从收到的路由信息中找出到达各AS的较好路由。
BGP的工作原理：
每一个自治系统的管理员要选择至少一个路由器（可多个）作为该自治系统的"BGP发言人”
一个BGP发言人与其他自治系统中的BGP发言人要交换路由信息，就要先建立TCP连接
然后在此连接上交换BGP报文以建立BGP会话，再利用BGP会话交换路由信息
当所有BGP发言人都相互交换网络可达性的信息后，各BGP发言人就可找出到达各个自治系统的比较好的路由
特点：
1）BGP协议交换路由信息的结点数量级是自治系统的数量级，比这些自治系统中的网络数少很多
2）每一个自治系统中BGP发言人（或边界路由器）的数目是很少的，这样自治系统之间的路由选择不会很复杂
3）BGP支持CIDR，BGP的路由表包括目的网络前缀、下一跳路由器，以及到达该目的网络所要经过的各个自治系统序列
4）在BGP刚运行时，BGP的邻站交换整个BGP路由表。但以后只需要在发生变化时更新有变化的部分
BGP-4的四种报文：
打开（Open）报文。用来与相邻的另一个BGP发言人建立关系。
更新（Update）报文。用来发送某一路由的信息，以及列出要撤销的多条路由。
保活（Keepalive）报文。用来确认打开报文并周期性地证实邻站关系。
通知（Notification）报文。用来发送检测到的差错。

# ipv4
### 分组格式
一个IP分组由首部和数据部分组成。首部长度20B固定，后面有可选字段，长度可变。
版本：指IP协议的版本，目前广泛使用的版本号为4。
首部长度：单位是4B，最小为5，表示20B，最大是15，表示60B。
区分服务：指示期望获得哪种类型的服务。
总长度：首部+数据，单位是1B。
标识：16位，用于IP分片，同一数据报的分片使用同一标识。
标志：3位，只有后两位有意义，中间位DF，DF=1，禁止分片；DF=0，允许分片。最低位MF，MF=1，后面“还有分片”；MF=0，代表最后一片/没分片。
片偏移：指出较长分组分片后，某片在原分组中的相对位置；以8B位单位。除了最后一个分片，每个分片数据部分长度一定是8B的整数倍。
生存时间（TTL）：IP分组的保质期。经过一个路由器-1变成0则丢弃。
协议：数据部分的协议，占8位。
首部检验和：16位，只检验首部。
源IP地址和目的IP地址：32位。
可选字段：0~40B，用来支持排错测量以及安全等措施
填充：全0，把首部补成4B的整数倍
### ip数据分片
最大传送单元（MTU）：一个链路层数据报能承载的最大数据量。以太网的MTU是1500字节。
当IP数据报的总长度大于链路MTU时，就需要将IP数据报中的数据分装在多个较小的IP数据报中，这些较小的数据报称为片。 片在目的地的网络层被重新组装。
P分片利用首部的标识、标志和片偏移三部分完成。
标识：创建IP数据报时，源主机为其加一个标识号，同一个数据报分片后，每片具有相同的标识。
标志：共3位，只有后两位有意义，
    中间位DF（Don’t Fragment），DF=1，禁止分片；DF=0，允许分片。
    最低位MF（More Fragment），MF=1，后面“还有分片”；MF=0，代表最后一片/没分片。
片偏移：指出数据报分片后某片在原分组中的相对位置，以8B位单位。除了最后一个分片，每个分片数据部分长度一定是8B的整数倍。

### ipv4地址
IP地址由网络号和主机号组成。
网络号标志主机（或路由器）所连接到的网络。一个网络号在整个因特网唯一。
主机号标志该主机（或路由器）自身。一台主机号在相同网络号范围是唯一的。
A类 前8位，第一位为0   用于大型网络
B类 前16位  前两位为10  用于中型网络
C类 前24位  前三位为110  用于小型网络
D类 前4位为1110  用于多播
E类 前4位为1111  用于保留使用

主机号全为0，表示该网络本身。
主机号全为1，表示该网络的广播地址，又称直接广播地址。
127.*.*.* 保留为环回自检（Loopback Test）地址，此地址表示任意主机本身，目的地址为环回地址的P数据报永远不会出现在任何网络上。
32位全为0，即0.0.0.0表示本网络上的本主机。
32位全为1，即255.255.255.255表示整个TCP/iP网络的广播地址，又称受限广播地址。实际使用时，由于路由器对广播域的隔离，255.255.255.255等效为本网络的广播地址。
IP地址特点：
IP地址是一种分等级的地址结构。其好处如下：
 ①在分配IP地址时只分配网络号，而主机号则由得到该网络的单位自行分配，方便了 IP地址的管理；
 ②路由器仅根据目的主机所连接的网络号来转发分组，减小了路由表所占的存储空间。
IP地址是标志一台主机（或路由器）和一条链路的接口。

当一台主机同时连接到两个网络时，该主机就必须同时具有两个相应的IP地址，每个IP地址的网络号必须与所在网络的网络号相同，且这两个IP地址的主机号是不同的。
IP网络上的一个路由器必然至少应具有两个IP地址（路由器每个端口必须至少分配一个IP地址）。
 用网桥连接的若干LAN仍然是同一个网络（同一个广播域），因此该LAN中所有主机的IP地址的网络号必须相同，但主机号必须不同。
 在IP地址中，所有分配到网络号的网络（无论是LAN还是WAN）都是平等的。
 在同一个局域网上的主机或路由器的IP地址中的网络号必须是一样的。
由于广泛使用无分类IP地址进行路由选择，这种传统分类的IP地址已成为历史。

### 网络地址转换
​ 网络地址转换（NAT）是指通过将专用网络地址（如Intranet）转换为公用地址（如Internet），从而对外隐藏内部管理的IP地址。其优势如下：
 它使得整个专用网只需要一个全球IP地址就可以与因特网连通。
 由于专用网本地IP地址是可重用的，所以NAT大大节省了IP地址的消耗。
 它隐藏了内部网络结构，从而降低了内部网络受到攻击的风险。
为了网络安全，划出了部分IP地址为私有IP地址。其特点如下：
 私有IP只用于LAN，不用于WAN连接。因此私有IP地址不能直接用于Internet，必须通过网关利用NAT把私有IP地址转换为Internet中合法的全球IP地址后才能用于Internet。
 私有IP地址被LAN重复使用。有效地解决了P地址不足的问题。
私有IP地址网段如下
A类：1个A类网段，即10.0.0.0~10.255.255.255。
B类：16个B类网段，即172.16.0.0~172.31.255.255。
C类：256个C类网段，即192.168.0.0~192.168.255.255。
在因特网中的所有路由器，对目的地址是私有地址的数据报一律不进行转发。
这种采用私有 IP地址的互联网络称为专用互联网或本地互联网。私有IP地址也称可重用地址。
​使用NAT时需要在专用网连接到因特网的路由器上安装NAT软件，NAT路由器至少有一个有效的外部全球IP地址。使用本地地址的主机和外界通信时，NAT路由器使用NAT转换表进行本地IP地址和全球IP地址的转换
NAT转换表存放着{ 本地IP地址:端口 } 到{全球IP地址:端口 } 的映射。该端口号是逻辑上的端口。
普通路由器在转发P数据报时，不改变其源P地址和目的P地址。而NAT路由器在转发IP数据报时，一定要更换其IP地址（转换源P地址或目的IP地址）。
普通路由器仅工作在网络层，而NAT路由器转发数据报时需要查看和转换传输层的端口号。

### 子网划分
由于两级IP地址有以下缺点，于是在IP增加子网号段：
 IP地址空间的利用率有时很低
 给每个物理网络分配一个网络号会使路由表变得太大而使网络性能变坏
 两级的IP地址不够灵活。
子网划分：增加子网号段，使两级IP变成三级IP地址。基本思路如下
 子网划分纯属一个单位内部的事情。单位对外仍然表现为没有划分子网的网络。
 从主机号借位作为子网号；三级IP地址结构如下：
   IP地址={<网络号>,<子网号>,<主机号>}
  凡是从其他网络发送给本单位某台主机的IP数据报，仍然是根据IP数据报的目的网络号先找到连接到本单位网络上的路由器。然后该路由器在收到IP数据报后，按目的网络号和子网号找到目的子网。最后把IP数据报直接交付给目的主机。
性质：
  子网中的主机号为全0或全1的地址都不能被指派
  子网中的主机号全0的地址为子网的网络号，主机号全1的地址为子网的广播地址

### 子网掩码
为了告诉主机或路由器对网络进行了子网划分，使用子网掩码来表达对原网络中主机号的借位。
​子网掩码是一个与IP地址相对应的、长32bit的二进制串，它由一串1和跟随的一串0组成。1对应于IP地址中的网络号及子网号，而0对应于主机号。
规定所有网络必需使用子网掩码，不划分采用默认子网掩码：
  A类：255.0.0.0
  B类：255.255.0.0
  C类：255.255.255.0
注意：
1）一个主机在设置IP地址信息的同时，必须设置子网掩码
2）同属于一个子网的所有主机以及路由器的相应端口，必须设置相同的子网掩码
3）路由器的路由表中，所包含的信息其主要内容必须有：目的网络地址、子网掩码、下一跳地址

### 无分类编址CIDR
无分类域间路由选择CIDR是在变长子网掩码的基础上提出的一种消除传统A、B、C类网络划分，并且可以在软件的支持下实现超网构造的一种IP地址的划分方法。 IP地址结构如下：
  IP::={<网络前缀>,<主机号>}
CIDR地址块中的地址数一定是2的整数次幕，实际可指派的地址数通常为2N-2；N表示主机号的位数，主机号全0代表网络号，主机号全1为广播地址。
​ CIDR记法：IP地址后加上“/”，然后写上网络前缀（可以任意长度）的位数。
```
例如，对于128.14.32.5/20这个地址，它的掩码是20个连续的1和后续12个连续的0，通过逐位相“与”的方法可以得到该地址的网络前缀（或直接截取前20位）
```
构成超网：将多个子网聚合成一个较大的子网，叫做构成超网，或路由聚合。
路由聚合使得路由表中的一个项目可以表示多个原来传统分类地址的路由，有利于减少路由器之间的信息的交换，从而提高网络性能。
方法：将网络前缀缩短（所有网络地址取交集）。
 例如，网络1的地址块是206.1.0.0/17；网络2的地址块是206.1.128.0/17。
 可以看出两个网络前16位相同，第17位分别是0和1，因此可以聚合成更大地址块206.1.0.0/16。
​最长前缀匹配：使用CIDR时，查找路由表可能得到几个匹配结果（跟网络掩码按位相与），应选择具有最长网络前缀的路由。前缀越长，地址块越小，路由越具体。
CIDR查找路由表的方法：为了更加有效地查找最长前缀匹配，通常将无分类编址的路由表存放在一种层次式数据结构中，然后自上而下地按层次进行查找。这里最常用的数据结构就是二叉线索。

### 网络层转发分组的过程
分组转发都是基于目的主机所在网络的，这是因为互联网上的网络数远小于主机数，可以极大地压缩转发的大小。当分组到达路由器后，路由器根据目的IP地址的网络前缀来查找转发表，确定下一跳应当到哪个路由器。
分组转发算法如下
1）从收到的IP分组的首部提取目的主机的IP地址D（即目的地址）。
2）若查找到特定主机路由（目的地址为D），就按照这条路由的下一跳转发分组；否则从转发表中的下一条（即按前缀长度的顺序）开始检查，执行步骤3）。
3）将这一行的子网掩码与目的地址D进行按位与运算。若运算结果与本行的前缀匹配，则查找结束，按照“下一跳”指出的进行处理（或者直接交付本网络上的目的主机，或通过指定接口发送到下一跳路由器）。否则，若转发表还有下一行，则对下一行进行检查，重新执行步骤3）。否则，执行步骤4）。
4）若转发表中有一个默认路由，则把分组传送给默认路由；否则，报告转发分组出错。

### 地址解析协议（ARP）
​ *地址解析协议（ARP）*作用是完成IP地址到MAC地址的映射。
​ARP表：局域网上各主机和路由器的IP地址到MAC地址的映射表，称ARP表。使用ARP来动态维护ARP表。
工作原理：
 主机A欲向本局域网上的某台主机B发送IP数据报时，先在其ARP高速缓存中查看有无主机B的IP地址。
   如果有，就可查出其对应的硬件地址，再将此硬件地址写入MAC帧，然后通过局域网将该MAC帧发往此硬件地址。
   如果没有，那么就通过使用目的MAC地址为FFFF-FF-FF-FF-FF的帧来封装并广播ARP请求分组（广播发送），使同一个局域网里的所有主机都收到此ARP请求。
  主机B收到该ARP请求后，向主机A发出ARP响应分组（单播发送），分组中包含主机B的IP与MAC地址的映射关系，主机A收到ARP响应分组后就将此映射写入ARP缓存，然后按查询到的硬件地址发送MAC帧。
   
### 动态主机配置协议（DHCP）
动态主机配置协议(Dynamic Host Configuration Protocol, DHCP)常用于给主机动态分配IP地址。
工作原理：应用层协议，使用客户/服务器方式，客户端和服务端通过广播方式进行交互，基于UDP。
  1）需要IP地址的主机在启动时向DHCP服务器广播发送发现报文，这时该主机成为DHCP客户
  2）本地网络上所有主机都能收到此广播报文，但只有DHCP服务器才回答此广播报文。DHCP服务器先在其数据库中查找该计算机的配置信息
  3）若找到，则返回找到的信息。若找不到，则从服务器的IP地址池中取一个地址分配给该计算机。DHCP服务器的回答报文叫做提供报文
DHCP特点：
 DHCP允许网络上配置多台DHCP服务器，当DHCP客户机发出“DHCP发现”消息时，有可能收到多个应答消息。这时，DHCP客户机只会挑选其中的一个，通常挑选最先到达的。
 DHCP服务器分配给DHCP客户的IP地址是临时的，因此DHCP客户只能在一段有限的时间内使用这个分配到的IP地址。DHCP称这段时间为租用期。租用期的数值应由DHCP服务器自己决定，DHCP客户也可在自己发送的报文中提出对租用期的要求。
 DHCP的客户端和服务器端需要通过广播方式来进行交互，原因是在DHCP执行初期，客户端不知道服务器端的IP地址，而在执行中间，客户端并未被分配IP地址，从而导致两者之间的通信必须采用广播的方式。采用UDP而不采用TCP的原因也很明显：TCP需要建立连接，如果连对方的IP地址都不知道，那么更不可能通过双方的套接字建立连接。
 DHCP是应用层协议，因为它是通过客户/服务器模式工作的，DHCP客户端向DHCP服务器请求服务，而其他层次的协议是没有这两种工作方式的。

### 网际控制报文协议（ICMP）
网际控制报文协议（Internet Control Message Protocol，ICMP）提高IP数据报交付成功的机会。
ICMP是网络层协议。ICMP报文作为IP层数据报的数据，加上数据报的首部，组成IP数据报发送出去。
​ICMP分为两类，即ICMP差错报告报文和ICMP询问报文。
ICMP差错报告报文：用于目标主机或到目标主机路径上的路由器向源主机报告差错和异常情况。
  ICMP差错报告报文可分为以下5类：
  终点不可达。当路由器或主机不能交付数据报时，就向源点发送终点不可达报文。
  源点抑制。当路由器或主机由于拥塞而丢弃数据报时，就向源点发送源点抑制报文。
  时间超过。当路由器收到生存时间（TTL）为零的数据报时，除丢弃该数据报外，还要向源点发送时间超过报文。当终点在预先规定的时间内不能收到一个数据报的全部数据报片时，就把已收到的数据报片都丢弃，并向源点发送时间超过报文。
  参数问题。当路由器或目的主机收到的数据报的首部中有的字段的值不正确时，就丢弃该数据报，并向源点发送参数问题报文。
  改变路由（重定向）。路由器把改变路由报文发送给主机，让主机知道下次应将数据报发送给另外的路由器（可通过更好的路由）。
ICMP询问报文：共有以下几类，常用的是前两类。
     回送请求和回答报文：主机或路由器向特定目的主机发出的询问，收到此报文的主机必须给源主机或路由器发送ICMP回送回答报文。测试目的站是否可达以及了解其相关状态。
     时间戮请求和回答报文：请主机或路由器回答当前的日期和时间。用来进行时钟同步和测量时间。
     掩码地址请求和回答报文
     路由器询问和通告报文
  PING：测试两个主机之间的连通性，使用了ICMP回送请求和回答报文。工作在应用层。
  Traceroute: 跟踪一个分组从源点到终点的路径, 使用了ICMP时间超过差错报告报文; 工作在网络层。


### Ip组播
为了能够支持像视频点播和视频会议这样的多媒体应用，网络必须实施某种有效的组播机制。
组播：是让源计算机一次发送的单个分组可以抵达用一个组地址标识的若干目标主机，并被它们正确接收。
组播基于UDP协议。当主机想利用组播将单个数据发送给一组主机，源主机把数据发给一个组播地址，组播地址可以标识一组地址。网络把这个数据的副本投递给该组中的每台主机。主机可以同时属于多个组。
组播基于UDP协议。当主机想利用组播将单个数据发送给一组主机，源主机把数据发给一个组播地址，组播地址可以标识一组地址。网络把这个数据的副本投递给该组中的每台主机。主机可以同时属于多个组。
在IPv4中，每个组播组都有一个D类地址，要给该组发送的计算机使用这个地址作为目标地址。
主机使用**IGMP（因特网组管理协议）**加入组播组。
主机组播时仅发送一份数据，只有数据在传送路径出现分岔时才将分组复制后继续转发。因此，对发送者而言，数据只需发送一次就可发送到所有接收者，大大减轻了网络的负载和发送者的负担。组播需要路由器的支持才能实现，能够运行组播协议的路由器称为组播路由器。

IP组播地址
 IP组播使用D类地址格式。D类地址的前四位是1110，因此D类地址范围是224.0.0.0~239.255.255.255。每个D类IP地址标志一个组播组。
 IP组播可以分为两种：
 一种只在本局域网上进行硬件组播
 另一种则在因特网的范围内进行组播
 在因特网上进行组播的最后阶段，还是要把组播数据报在局域网上用硬件组播交付给组播组的所有成员。
 硬件组播
 组播IP地址也需要相应的组播MAC地址在本地网络中实际传送帧。

 IGMP网际组管理协议 网络层协议 基于IP
 目的：IGMP协议让组播路由器知道本局域网上是否有主机（的进程）参加或退出了某个组播组。
 工作阶段：
 1、某主机要加入组播组，向组播地址发送IGMP报文，声明自己要加入组播
  本地组播路由器收到报文，转发给因特网其他组播路由器
2、本地组播路由器周期性探询本地局域网上的主机，以便知道这些主机是否还是组播组的成员。
  只要有一个主机对某个组响应，那么组播路由器就认为这个组是活跃的；如果经过几次探询后没有一个主机响应，组播路由器就认为本网络上的没有此组播组的主机，因此就不再把这组的成员关系发给其他的组播路由器。
组播路由器知道的成员关系只是所连接的局域网中有无组播组的成员。

组播路由选择协议
目的：组播路由选择协议目的是找出以源主机为根节点的组播转发树。
组播路由协议目的是找出以源主机为根节点的组播转发树。
构造树可以避免在路由器之间兜圈子。
在组播转发树上的路由器不会收到重复的组播数据报
对不同的多播组对应于不同的多播转发树；同一个多播组，对不同的源点也会有不同的多播转发树。
算法：
基于链路状态的路由选择
基于距离-向量的路由选择
协议无关的组播（PIM）

网络层设备
冲突域和广播域
冲突域是指连接到同一物理介质上的所有结点的集合，这些结点之间存在介质争用的现象。
广播域是指接收同样广播消息的结点集合。也就是说，在该集合中的任何一个结点发送一个广播帧，其他能收到这个帧的结点都被认为是该广播域的一部分。
路由器的组成和功能
 路由器转发
   当源主机要向目标主机发送数据报时，路由器先检查源主机与目标主机是否连接在同一个网络上。
   如果源主机和目标主机在同一个网络上，那么直接交付而无须通过路由器。
   如果源主机和目标主机不在同一个网络上，那么路由器按照转发表（路由表）指出的路由将数据报转发给下一个路由器，这称为间接交付。
  路由器结构
    路由选择：根据所选定的路由选择协议构造出路由表，同时经常或定期地和相邻路由器交换路由信息而不断地更新和维护路由表
    交换结构：根据转发表（路由表得来）对分组进行转发
    分组转发：若收到RIP/OSPF分组等，则把分组送往路由选择处理机；若收到数据分组，则查找转发表并输出
    输入端口：输入端口中的查找和转发功能在路由器的交换功能中是最重要的。当一个分组正在查找转发表时，后面又紧跟着从这个输入端口收到另一个分组。
    输出端口：若路由器处理分组的速率赶不上分组进入队列的速率，则队列的存储空间最终必定减少到零，这就使后面再进入队列的分组由于没有存储空间而只能被丢弃。
   路由器中的输入或输出队列产生溢出是造成分组丢失的重要原因。


# 传输层
### 传输层的功能
 端到端通信
  传输层提供进程和进程（端到端）之间的逻辑通信。与网络层的区别是，网络层提供的是主机之间的逻辑通信。应用进程之间的通信又称端到端的逻辑通信。
复用和分用
   复用是指发送方不同的应用进程都可以使用同一个传输层协议传送数据
   分用是指接收方的传输层在剥去报文的首部后能够把这些数据正确交付到目的应用进程
差错检测
 传输层检验首部与数据部分；网路层只检验首部。
提供两种不同的传输协议
  面向连接的传输控制协议TCP：可靠，面向连接，时延大，适用于大文件
  无连接的用户数据报协议UDP：不可靠，无连接，时延小，适用于小文件。
传输层的寻址与端口
  端口的作用
     端口能够让应用层的各种应用进程将其数据通过端口向下交付给传输层，以及让传输层知道应当将其报文段中的数据向上通过端口交付给应用层相应的进程。
     端口是传输层服务访问点（TSAP），它在传输层的作用类似于IP地址在网络层的作用或MAC地址在数据链路层的作用，只不过IP地址和MAC地址标识的是主机，而端口标识的是主机中的应用进程。
     数据链路层的SAP是MAC地址，网络层的SAP是IP地址，传输层的SAP是端口。
     在协议栈层间的抽象的协议端口是软件端口，它与路由器或交换机上的硬件端口是完全不同的概念。硬件端口是不同硬件设备进行交互的接口，而软件端口是应用层的各种协议进程与传输实体进行层间交互的一种地址。传输层使用的是软件端口。
  端口号
    应用进程通过端口号进行标识，端口号长度为16bit，能够表示65536（216）个不同的端口号
    端口号只具有本地意义，即端口号只标识本计算机应用层中的各进程，在因特网中不同计算机的相同端口号是没有联系的。根据端口号范围可将端口分为两类：
      服务器端使用的端口号：它又分为两类，最重要的一类是熟知端口号，数值为0~1023，IANA（互联网地址指派机构）把这些端口号指派给了TCP/IP最重要的一些应用程序，让所有的用户都知道。

      另一类称为登记端口号，数值为1024~49151。它是供没有熟知端口号的应用程序使用的，使用这类端口号必须在LANA登记，以防止重复。

      客户端使用的端口号：数值为49152~65535。由于这类端口号仅在客户进程运行时才动态地选择，因此又称短暂端口号（也称临时端口）。通信结束后，刚用过的客户端口号就不复存在，从而这个端口号就可供其他客户进程以后使用。
  套接字
     在网络中通过IP地址来标识和区别不同的主机，通过端口号来标识和区分一台主机中的不同应用进程，端口号拼接到IP地址即构成套接字Socket。套接字，实际上是一个通信端点，即
           套接字Socket=（IP地址：端口号）
      它唯一地标识网络中的一台主机和其上的一个应用（进程）。
      
      在网络通信中，主机A发给主机B的报文段包含目的端口号和源端口号，源端口号是“返回地址”的一部分，即当B需要发回一个报文段给A时，B到A的报文段中的目的端口号便是A到B的报文段中的源端口号（完全的返回地址是A的P地址和源端口号）。

### UDP
UDP仅在IP的数据报服务之上增加了两个最基本的服务：复用和分用以及差错检测。
  特点：
    UDP是无连接的，减少开销和发送数据之前的时延。
    UDP使用最大努力交付，即不保证可靠交付。
    UDP是面向报文的，适合一次性传输少量数据的网络应用，
    UDP无拥塞控制，适合很多实时应用。
    分组首部开销小。TCP有20B的首部开销，而UDP仅有8B的开销。
    UDP支持一对一、一对多、多对一和多对多的交互通信。
UDP的首部格式
  源端口：源端口号。在需要对方回信时选用，不需要时可用全0。
  目的端口：目的端口号。这在终点交付报文时必须使用到。
  长度：单位字节，UDP数据报的长度（包括首部和数据），其最小值是8（仅有首部）。
  校验和：检测UDP数据报在传输中是否有错。有错就丢弃。该字段是可选的，当源主机不想计算校验和时，则直接令该字段为全0。
​ 当传输层从IP层收到UDP数据报时，就根据首部中的目的端口，把UDP数据报通过相应的端口上交给应用进程。
如果接收方UDP发现收到的报文中的目的端口号不正确（即不存在对应于端口号的应用进程），那么就丢弃该报文，并由ICMP发送“端口不可达”差错报文给发送方。

UDP校验
  在计算校验和时，要在UDP数据报之前增加12B的伪首部，伪首部并不是UDP的真正首部。只是在计算校验和时，临时添加在UDP数据报的前面，得到一个临时的UDP数据报。校验和就是按照这个临时的UDP数据报来计算的。伪首部既不向下传送又不向上递交，而只是为了计算校验和。
   UDP校验和的计算方法和IP数据报首部校验和的计算方法相似。但不同的是，IP数据报的校验和只检验IP数据报的首部，但UDP的校验和则检查首部和数据部分。
  检验过程：
  发送方首先把全零放入校验和字段并添加伪首部，然后把UDP数据报视为许多16位的字串接起来。
  若UDP数据报的数据部分不是偶数个字节，则要在数据部分末尾填入一个全零字节（但此字节不发送）。
  然后按二进制反码计算出这些16位字的和，将此和的二进制反码写入校验和字段，并发送。
  接收方把收到的UDP数据报加上伪首部（如果不为偶数个字节，那么还需要补上全零字节）后，按二进制反码求这些16位字的和。
  当无差错时其结果应为全1，否则就表明有差错出现，接收方就应该丢弃这个UDP数据报。
二进制反码运算求和：将所有的字相加，如果相加过程中最高位产生了进位，就将进位加到最低位上，这叫做回卷。

### TCP
TCP是在不可靠的IP层之上实现的可靠的数据传输协议，它主要解决传输的可靠、有序、无丢失和不重复问题。
 特点：
  TCP是面向连接（虚连接）的传输层协议
  每一条TCP连接只能有两个端点，每一条TCP连接只能是点对点的
  TCP 提供可靠交付的服务，保证传送的数据无差错、不丢失、不重复且有序
  TCP提供全双工通信，两端都有发送缓存和接受缓存。
     发送缓存用来暂时存放以下数据：①发送应用程序传送给发送方TCP准备发送的数据；②TCP已发送但尚未收到确认的数据。
     接收缓存用来暂时存放以下数据：①按序到达但尚未被接收应用程序读取的数据；②不按序到达的数据。
  TCP是面向字节流的。虽然应用程序和TCP的交互是一次一个数据块（大小不等），但TCP把应用程序交下来的数据仅仅看成是一连串的无结构的字节流。
TCP报文段
   TCP传送的数据单元称为报文段。TCP报文段既可以用来运载数据，又可以用来建立连接、释放连接和应答。
    一个TCP报文段分为首部和数据两部分，整个TCP报文段作为IP数据报的数据部分封装在IP数据报中，其首部的前20B是固定的。TCP首部最短为20B，后面有4N字节是根据需要而增加的选项，长度为4B的整数倍。
      源端口和目的端口：各占2个字节，分别写入源端口号和目的端口号
      序号：在一个TCP连接中传送的字节流中的每一个字节都按顺序编号，本字段表示本报文段所发送数据的第一个字节的序号。
      序号：在一个TCP连接中传送的字节流中的每一个字节都按顺序编号，本字段表示本报文段所发送数据的第一个字节的序号。
      确认号：期望收到对方下一个报文段的第一个数据字节的序号。若确认号为N，则证明到序号N-1为止的所有数据都已正确收到。
      数据偏移（首部长度）：TCP报文段的数据起始处距离TCP报文段的起始处有多远，以4B位单位，即1个数值是4B。
      保留。占6位，保留为今后使用，但目前应置为0。
      控制位：
        紧急位URG：URG=1时，标明此报文段中有紧急数据，是高优先级的数据，应尽快传送，不用在缓存里排队，配合紧急指针字段使用。
        确认位ACK：ACK=1时确认号有效，在连接建立后所有传送的报文段都必须把ACK置为1。
        推送位PSH：PSH=1时，接收方尽快交付接收应用进程，不再等到缓存填满再向上交付。
        复位RST：RST=1时，表明TCP连接中出现严重差错，必须释放连接，然后再重新建立传输链接。
        同步位SYN：SYN=1时，表明是一个连接请求/连接接受报文。
        终止位FIN：FIN=1时，表明此报文段发送方数据已发完，要求释放连接
      窗口：指的是发送本报文段的一方的接收窗口，即现在允许对方发送的数据量。
      检验和：检验首部+数据，检验时要加上12B伪首部，第四个字段为6。
      紧急指针：URG=1时才有意义，指出本报文段中紧急数据的字节数（紧急数据在报文段数据的最前面）。
      选项：长度可变。最大报文段长度MSS、窗口扩大、时间戳、选择确认。
      填充：这是为了使整个首部长度是4B的整数倍。
TCP连接管理
TCP是面向连接的协议，因此每个TCP连接都有三个阶段：连接建立、数据传送和连接释放。TCP连接的管理就是使运输连接的建立和释放都能正常进行。  
   1.TCP连接的建立
    TCP连接的建立采用客户/服务器模式。主动发起连接建立的应用进程称为客户（Client），而被动等待连接建立的应用进程称为服务器
    TCP连接的端口即为套接字(Socket)或插口，每条TCP连接唯一地被通信的两个端点（即两个套接字）确定。
    连接建立过程经历3个步骤，称为三次握手。
    连接建立前，A、B创建传输控制模块TCB，服务器进程处于LISTEN（收听）状态，等待客户的连接请求。
    1）客户机先向服务器发送一个连接请求报文段。它不含应用层数据，其首部中的SYN标志位=1，另外，客户机要随机选择一个起始序号seq=x。TCP客户进程进入SYN-SENT（同步已发送）状态。
    2）服务器收到连接请求报文段后，如同意就向客户机发确认，并为该连接分配缓存和变量。
    其中，SYN和ACK=1，确认号字段的值ack=x+1，并且服务器随机产生起始序号seq=y，确认报文段同样不包含应用层数据。TCP服务器进程进入SYN-RCVD（同步收到）状态。
    3）当客户机收到确认报文段后，还要向服务器给出确认，并且也要给该连接分配缓存和变量。
    其中ACK标志位=1，序号字段seq=x+1，确认号字段ack=y+1，该报文段可以携带数据，如果不携带数据则不消耗序号。TCP客户进程进入ESTABLISHED（已建立连接）状态。
  要A第三次确认，是为了防止己失效的连接请求报文段突然又传送到了B，因而产生错误。防止第一次发送的连接请求报文段滞后到达，A在接收到B的确认就开始传送数据，而B确以为建立了新的连接而无法接收，导致数据丢失。
   服务器端的资源是在完成第二次握手时分配的，而客户端的资源是在完成第三次握手时分配的，这就使得服务器易于受到SYN洪泛攻击
   2.TCP连接的释放
  TCP连接释放的过程通常称为四次握手。
  1）客户端发送连接释放报文段，停止发送数据，主动关闭TCP连接。FIN=1，seq=u，它等于前面已传送过的数据的最后一个字节的序号加1。TCP客户进程进入FIN-WAIT-1（终止等待1）状态。
  2）服务器端回送一个确认报文段，ACK=1，seq=v，ack=u+1，客户到服务器这个方向的连接就释放了，TCP连接处于半关闭状态。服务器进入CLOSE-WAIT（关闭等待）状态。客户收到后进入FIN-WAIT-2（终止等待2）状态。
  3）服务器端发完数据，就发出连接释放报文段，主动关闭TCP连接。FIN=1，ACK=1，seq=w，ack=u+1。服务器进入LAST-ACK（最后确认）状态。
  4）客户端回送一个确认报文段，ACK=1, seq=u+1, ack=w+1，客户进入进入到TIME-WAIT（时间等待）状态。再等到时间等待计时器设置的2MSL（最长报文段寿命）后，连接彻底关闭。客户机和服务器进入CLOSED（连接关闭）状态。
    为什么A在TIME-WAIT状态必须等待2MSL的时间呢？
     第一，为了保证A发送的最后一个ACK报文段能够到达B。
     第二，防止“已失效的连接请求报文段”出现在本连接中。
   除时间等待计时器外，TCP还设有一个保活计时器（keepalive timer）。
    就是使用保活计时器。服务器每收到一次客户的数据，就重新设置保活计时器，时间的设置通常是两小时。若两小时没有收到客户的数据，服务器就发送一个探测报文段，以后则每隔75秒钟发送一次。若一连发送10个探测报文段后仍无客户的响应，服务器就认为客户端出了故障，接着就关闭这个连接。

TCP可靠传输
   TCP的任务是在IP层不可靠的、尽力而为服务的基础上建立一种可靠数据传输服务。TCP使用了校验、序号、确认和重传等机制来达到这一目的。
   可靠，指的是保证接收方进程从缓存区读出的字节流与发送方发出的字节流是完全一样的。
  1.序号
    TCP连接中传送的数据流中的每一个字节都编上一个序号。序号字段的值则指的是本报文段所发送的数据的第一个字节的序号。
  2.确认
    TCP首部的确认号是期望收到对方的下一个报文段的数据的第一个字节的序号。
    TCP默认使用累计确认，即TCP只确认数据流中至第一个丢失字节为止的字节
  3.重传
    有两种事件会导致TCP对报文段进行重传：超时和冗余ACK
   超时重传
     TCP每发送一个报文段，就对这个报文段设置一次计时器。只要计时器设置的重传时间到期但还没有收到确认，就要重传这一报文段。
     TCP采用自适应算法，动态改变重传时间RTTs（加权平均往返时间）
   冗余ACK（冗余确认
     TCP规定每当比期望序号大的失序报文段到达时，发送一个冗余ACK，指明下一个期待字节的序号。
     TCP规定每当比期望序号大的失序报文段到达时，发送一个冗余ACK，指明下一个期待字节的序号。
    当发送方收到对同一个报文段的3个冗余ACK时，就可以认为跟在这个被确认报丈段之后的报文段已经丢失。
TCP流量控制
  TCP提供流量控制服务来消除发送方（发送速率太快）使接收方缓存区溢出的可能性。TCP提供一种基于滑动窗口协议的流量控制机制。
  滑动窗口：
    接收窗口rwnd：接收端维护，接收端当前的接收缓存大小。
    拥塞窗口cwnd：发送端维护，发送端根据当前网络的拥塞程度而确定的窗口值。
    发送窗口：由发送端维护，发送端在接收到下一个确认前能够发送的最大字节数。
    发送窗口=min（接收窗口，拥塞窗口）
  在通信过程中，接收方根据自己接收缓存的大小，动态地调整发送方的发送窗口大小，即接收窗口rwnd（接收方设置确认报文段的窗口字段来将rwnd通知给发送方），发送方的发送窗口取接收窗口rwnd和拥塞窗口cwnd的最小值。TCP的窗口单位是字节，不是报文段
传输层和数据链路层的流量控制的区别是：
   传输层定义端到端用户之间的流量控制，数据链路层定义两个中间的相邻结点的流量控制。
   数据链路层的滑动窗口协议的窗口大小不能动态变化，传输层的则可以动态变化。
TCP拥塞控制
  拥塞控制是指防止过多的数据注入网络，保证网络中的路由器或链路不致过载，是全局性过程。出现拥塞时，端点并不了解拥塞发生的细节，对通信连接的端点来说，拥塞往往表现为通信时延的增加。
因特网建议标准定义了进行拥塞控制的4种算法：慢开始、拥塞避免、快重传和快恢复
  1.慢开始和拥塞避免
   慢开始：
     1）先令拥塞窗口cwnd=1（即一个最大报文段长度MSS）
     2）在每收到一个对新的报文段的确认后，将cwnd加1，即增大一个MSS（拥塞窗口加倍）
   拥塞避免：
    1）发送端的拥塞窗口cwnd每经过一个往返时延RTT就增加一个MSS的大小，而不是加倍，使cwnd按线性规律缓慢增长（即加法增大）
    2）当出现一次超时（网络拥塞）时，则令慢开始门限ssthresh等于当前cwnd的一半（即乘法减小）
       当cwnd<ssthresh时，使用慢开始算法。
       当cwnd>ssthresh时，停止使用慢开始算法而改用拥塞避免算法。
       当cwnd=ssthresh时，既可使用慢开始算法，又可使用拥塞避免算法（通常做法）。
  2.快重传和快恢复
  快重传和快恢复算法是对慢开始和拥塞避免算法的改进。
    快重传：收到3个重复的确认执行快重传算法。
    快恢复：当发送端收到连续三个冗余ACK时，就执行“乘法减小"算法，把慢开始门限ssthresh设置为出现拥塞时发送方cwnd的一半。与慢开始（将拥塞窗口cwnd设置为1）不同之处是它把cwnd的值设置为慢开始门限ssthresh改变后的数值，然后开始执行拥塞避免算法（加法增大），使拥塞窗口缓慢地线性增大
在流量控制中，发送方发送数据的量由接收方决定，而在拥塞控制中，则由发送方自己通过检测网络状况来决定。实际上，慢开始、拥塞避免、快重传和快恢复几种算法是同时应用在拥塞控制机制中。
   在TCP连接建立和网络出现超时时，采用慢开始和拥塞避免算法；
   当发送方接收到冗余ACK时，采用快重传和快恢复算法。


# 应用层
### 网络应用模型
#### 客户/服务器模型
在客户/服务器（Client/Server，C/S）模型中，有一个总是打开的主机称为服务器，它服务于许多来自其他称为客户机的主机请求。
1.服务器：提供计算服务的设备
 特点：-永久的提供服务； -永久性访问地址/域名
2.客户机：请求计算服务的主机。
  特点：
    1）与服务器通信，使用服务器提供的服务
    2）间歇性接入网络
    3）可能使用动态IP地址
    4）不与其他客户机直接通信
主要特点：
  1）网络中各计算机的地位不平等，服务器可以通过对用户权限的限制来达到管理客户机的目的，使它们不能随意存储/删除数据，或进行其他受限的网络活动。
  2）客户机相互之间不直接通信。
  3）可扩展性不佳。受服务器硬件和网络带宽的限制，服务器支持的客户机数有限。
### P2P模型
在P2P模型中，各计算机没有固定的客户和服务器划分。相反，任意一对计算机一一称为对等方（Peer），直接相互通信。每个结点既作为客户访问其他结点的资源，也作为服务器提供资源给其他结点访问。
特点：
   不存在永远在线的服务器，每个主机既可以提供服务，也可以请求服务
   任意端系统/节点之间可以直接通讯，多个客户机之间可以直接共享文档
   节点间歇性接入网络，节点可能改变IP地址
   多个客户机之间可以直接共享文档
   可扩展性好
   网络健壮性强
缺点：
  在获取服务的同时，还要给其他结点提供服务，因此会占用较多的内存，影响整机速度。
### 域名系统（DNS）
域名系统（Domain Name System，DNS）是因特网使用的命名系统，用来把便于人们记忆的具有特定含义的主机名（www.baidu.com）转换为便于机器处理的IP地址。
DNS系统采用客户/服务器模型，其协议运行在UDP之上，使用53号端口。
DNS分为3部分：层次域名空间、域名服务器和解析器。
1.层次域名空间
   因特网采用层次树状结构的命名方法。采用这种命名方法，任何一个连接到因特网的主机或路由器，都有一个唯一的层次结构名称，即域名（Domain Name）。 
  从语法上讲，每一个域名都由标号（label）序列组成，而各标号之间用点隔开。
  1）标号
  标号中的英文不区分大小写
  标号中除连字符"-"外不能使用其他的标点符号   
  每一个标号不超过63个字符，多标号组成的完整域名最长不超过255个字符
  级别最低的域名写在最左边，而级别最高的顶级域名写在最右边
  2）域名树
  根：域名树最上面的是根，但没有对应的名字。它用一个点（.）表示，也称为根域或根区
  顶级域名（Top Level Domain，TLD）分为如下三大类：
     国家顶级域名：cn，us，uk
     通用顶级域名：com，net，org，gov，int，aero，museum，travel
     基础结构域名/反向域名：arpa
  二级域名：
  类别域名：ac，com，edu，gov，mil，net，org
  行政区域名：用于我国各省、自治区、直辖市bj，js
  自己注册的域名：cctv，google
 凡是在顶级域名com下注册的单位都获得了一个二级域名
  三级域名：www、mail
2.域名服务器
1）根域名服务器是最高层次的域名服务器，所有的根域名服务器都知道所有的顶级域名服务器的IP地址。任何本地域名服务器，若无法解析一个域名，就先求助于根域名服务器。通常不直接把待查询的域名直接转换成IP地址，而是告诉本地域名服务器下一步应找哪个顶级域名服务器进行查询
2）顶级域名服务器
   负责管理在该顶级域名服务器注册的所有二级域名。
   收到DNS查询请求时，就给出相应的回答（可能是最后的结果，也可能是下一步应当查找的域名服务器的IP地址）
3）授权域名服务器（权限域名服务器）
   负责一个区的域名服务器。每台主机都必须在授权域名服务器处登记，授权域名服务器总是能够将其管辖的主机名转换为该主机的地址。  
4）本地域名服务器
   当一个主机发出DNS查询请求时，这个查询请求报文就发给本地域名服务器
### 文件传输协议 FTP
文件传输协议（File Transfer Protocol，FTP）是因特网上使用得最广泛的文件传输协议。基于TCP，可靠传输。基于客户/服务器（C/S）的协议。
FTP提供交互式的访问，允许客户指明文件的类型与格式，并允许文件具有存取权限。它屏蔽了各计算机系统的细节，因而适合于在异构网络中的任意计算机之间传送文件。
FTP在工作时使用两个并行的TCP连接：一个是控制连接（服务器端口号21），一个是数据连接（服务器端口号20）。使用两个不同的端口号可以使协议更容易实现。控制连接始终保持；数据连接保持一会。
1.控制连接
  服务器监听在21号端口，等待客户连接用来传输控制信息（如连接请求、传送请求）。控制信息都是以7位ASCII 格式传送的。
  FTP客户发出的传送请求，通过控制连接发送给服务器端的控制进程，但控制连接并不用来传送文件。在整个会话期间一直保持打开状态。
2.数据连接
  服务器端的控制进程在接收到FTP客户发送来的文件传输请求后就创建“数据传送进程”和“数据连接”。
  用来连接客户端和服务器端的数据传送进程，数据传送进程完成文件的传送，在传送完毕后关闭“数据传送连接”结束运行。
  数据连接有两种传输模式：主动模式PORT和被动模式PASV。
    主动模式PORT：
    客户端连接到服务器的21端口，登录成功后要读取数据时，客户端随机开放一个端口，并发送命令告知服务器，服务器收到PORT命令和端口号后，通过20端口和客户端开放的端口连接，发送数据。
    被动模式PASV：
    客户瑞要读取数据时，发送PASV命令到服务器，服务器在本地随机开放一个端口，并告知客户端，客户端再连接到服务器开放的端口进行数据传输。
### 电子邮件
电子邮件是一种异步通信方式，通信时不需要双方同时在场。电子邮件把邮件发送到收件人使用的邮件服务器，并放在其中的收件人邮箱中，收件人可以随时上网到自己使用的邮件服务器进行读取。
1.组件构成
  用户代理（UA）：用户与电子邮件系统的接口。用户代理向用户提供一个很友好的接口来发送和接收邮件，用户代理至少应当具有撰写、显示和邮件处理的功能。通常情况下，用户代理就是一个运行在PC上的程序（电子邮件客户端软件），常见的有Outlook和Foxmail等。

  邮件服务器：它的功能是发送和接收邮件，同时还要向发信人报告邮件传送的情况（已交付被拒绝、丢失等）。邮件服务器采用客户服务器方式工作，但它必须能够同时充当客户和服务器。

  邮件发送协议和读取协议：邮件发送协议用于用户代理向邮件服务器发送邮件或在邮件服务器之间发送邮件，如SMTP；邮件读取协议用于用户代理从邮件服务器读取邮件，如POP3。

 