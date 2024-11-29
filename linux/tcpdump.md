# tcpdump 基本用法
### 抓取所有网络数据包
``` 
 sudo tcpdump
```
可以按Ctrl+C来停止抓包

### 指定网络接口  
如果要抓取指定网络接口上的数据包，可以通过 -i 参数来指定接口。例如，抓取eth0接口上的数据包：
```
sudo tcpdump -i eth0
```
### 显示数据包详情
```
显示数据包详情
```
### 保存抓包结果到文件  
可以使用-w参数来将抓包结果保存到文件中，例如：  
```
sudo tcpdump -i eth0 -w capture.pcap
```
### 查看抓包结果
使用tcpdump抓包后，可以使用以下命令来查看抓包结果：  
```
tcpdump -r capture.pcap 
```
### 过滤数据包
可以使用过滤表达式来过滤感兴趣的数据包。例如，只查看目标IP地址为192.168.1.1的数据包：
```
sudo tcpdump -i eth0 dst host 192.168.1.1
```
### 监听指定端口
可以通过指定端口来监听网络数据包。例如，监听80端口的HTTP请求：
```
sudo tcpdump -i eth0 port 80
```
