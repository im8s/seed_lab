---
show: step
version: 0.1
enableO_checker: true
---

#LINUX系统监控常用命令（一）

##一、实验简介
`系统监控的重要性`

　我们的系统一旦上线跑起来我们自然希望它一直相安无事，不要宕机，不要无响应，不要慢腾腾的。但是这不是打开机器电源然后放任不管就可以得到的。所以我们要监视系统的运行状况，发现问题及时处理。
　对于系统和网络管理员来说每天监控和调试Linux系统的性能问题是一项繁重的工作。监控和保持系统启动并运行是很不容易的一件事。接下来介绍部分linux的系统监控命令。

`建议切换到字符界面，比较流畅`
##二、命令介绍

下面来学习 linux 下常用的惊恐命令。

### 2.1 CPU监控top

 　Linux下的Top命令是一个性能监控程序，许多系统管理员常常用它来监控Linux性能，在许多Linux或者类Unix操作系统里都有这个命令。Top命令用于按一定的顺序显示所有正在运行而且处于活动状态的实时进程，而且会定期更新显示结果。这条命令显示了CPU的使用率、内存使用率、交换内存使用大小、高速缓存使用大小、缓冲区使用大小，进程PID、所使用命令以及其他。它还可以显示正在运行进程的内存和CPU占用多的情况。

```
$ top
```
操作截图：

![1-2.1-1](https://doc.shiyanlou.com/userid42227labid972time1430721156300/wm)

在图中依次可以看到进程PID,进程用户，CPU使用率，内存使用率、交换内存使用大小等等信息。top命令提供了实时的对系统处理器的状态监视.它将显示系统中CPU最“敏感”的任务列表.

 通过man top可以查看到详细的top命令使用方式。
```
$ man top
```

操作截图：

![1-2.1-2](https://doc.shiyanlou.com/userid42227labid972time1430721622675/wm)

### 2.2 虚拟内存监控vmstat

   Linux 的 VmStat 命令用于显示虚拟内存、内核线程、磁盘、系统进程、I/O 块、中断、CPU 活动 等的统计信息。

   一般vmstat工具的使用是通过两个数字参数来完成的，第一个参数是采样的时间间隔数，单位是秒，第二个参数是采样的次数，
```
$ vmstat 2 1

$ vmstat 2 2
```

操作截图：

![1-2.2-1](https://doc.shiyanlou.com/userid42227labid972time1430722488865/wm)


如果要求vmstat每2秒采集数据，一直采集，直到结束程序（Ctrl+c）。则省略采集次数：
```
$ vmstat 2  
```

测试参数讲解：
```
r  ：表示运行队列，如果运行队列过大，表示你的CPU很繁忙，一般会造成CPU使用率很高

b  ：表示阻塞的进程数

swpd ：虚拟内存已使用的大小，如果大于0，表示你的机器物理内存不足了，如果不是程序内存泄露的原因，那么你该升级内存了或者把耗内存的任务迁移到其他机器

free  ：空闲的物理内存的大小

buff  ： 系统占用的缓存大小

cache ：直接用来记忆我们打开的文件,给文件做缓冲

si  ：每秒从磁盘读入虚拟内存的大小，如果这个值大于0，表示物理内存不够用或者内存泄露了

us ：用户CPU时间

sy ：系统CPU时间

so ： 每秒虚拟内存写入磁盘的大小，如果这个值大于0，同上。

sy ： 系统CPU时间，如果太高，表示系统调用时间长，例如是IO操作频繁。  

id  ： 空闲 CPU时间，一般来说，id + us + sy = 100  

wa: IO等待时间百分比 wa的值高时，说明IO等待比较严重，这可能由于磁盘大量作随机访问造成，也有可能磁盘出现瓶颈（块操作）。 id: 空闲时间百分比

```

###2.3 列出打开的文件：lsof

它常用于以列表的形式显示所有打开的文件和进程。打开的文件包括磁盘文件、网络套接字、管道、设备和进程。使用这条命令的主要情形之一就是在无法挂载磁盘和显示正在使用或者打开某个文件的错误信息的时候。使用这条命令，你可以很容易地看到正在使用哪个文件。
```
$ lsof 
```

操作截图：

![1-2.3](https://doc.shiyanlou.com/userid42227labid972time1430723481770/wm)

此命令运行的结果较长，截图部分。

###2.4 网络包分析器：tcpdump 

　Tcpdump是最广泛使用的网络包分析器或者包监控程序之一，它用于捕捉或者过滤网络上指定接口上接收或者传输的TCP/IP包。它还有一个选项用于把捕捉到的包保存到文件里，以便以后进行分析。
　
   -h：查看命令帮助
    
   -i：网络接口

 -c ：需要输出包数量
    

```
$ sudo apt-get update

$ sudo apt-get install tcpdump 

$ tcpdump -h

$ sudo tcpdump -i eth0 -c 3 

```

操作截图：


![1-2.4](https://doc.shiyanlou.com/userid42227labid972time1430724440342/wm)


###2.5 网络状态统计：netstat

　　Netstat是一个用于监控进出网络的包和网络接口统计的命令行工具。它是一个非常有用的工具，系统管理员可以用来监控网络性能，定位并解决网络相关问题。
　　
　－ｈ： 查看帮助
　－ｒ：
　－ｉ：查看网络接口
　　
```
$ netstat -h

$ netstat -r

$ netstat -i　

```
操作截图：

![1-2.5-1](https://doc.shiyanlou.com/userid42227labid972time1430725014841/wm)

![1-2.5-2](https://doc.shiyanlou.com/userid42227labid972time1430725052309/wm)


###2.6 进程监控：Htop 

　　Htop 是一个非常高级的交互式的实时linux进程监控工具。 它和top命令十分相似，但是它具有更丰富的特性，例如用户可以友好地管理进程，快捷键，垂直和水平方式显示进程等等。 Htop是一个第三方工具，它不包含在linux系统中，你需要使用管理工具去安装它。


```
$ sudo apt-get install htop

$ htop
```

![1-2.6-1](https://doc.shiyanlou.com/userid42227labid972time1430725413865/wm)

###2.7 监控Linux磁盘I/O ：iotop

　iotop命令同样也非常类似于top命令和Htop程序，不过它具有监控并显示实时磁盘I/O和进程的统计功能。在查找具体进程和大量使用磁盘读写进程的时候，这个工具就非常有用。
　
　  这个命令只有在kernelv2.6.20及以后的版本中才有。python版本需要 python2.7及以上版本。由于系统原因，实验环境并不支持此命令。此处仅做介绍。

###2.8 输入/输出统计：iostat

　　iostat是一个用于收集显示系统存储设备输入和输出状态统计的简单工具。这个工具常常用来追踪存储设备的性能问题，其中存储设备包括设备、本地磁盘，以及诸如使用NFS等的远端磁盘。
```
$ sudo apt-get install sysstat

$ iostat
```

操作截图：

![1-2.8-1](https://doc.shiyanlou.com/userid42227labid972time1430728053366/wm)

各项含义：
avg-cpu段:
```
%user: 在用户级别运行所使用的CPU的百分比.

%nice:优先进程消耗的CPU时间，占所有CPU的百分比.

%system: 在系统级别(kernel)运行所使用CPU的百分比.

%iowait: CPU等待硬件I/O时,所占用CPU百分比.

%steal: 管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比.

%idle: CPU空闲时间的百分比.
```
Device段:
```
tps: 每秒钟发送到的I/O请求数.

KB_read /s: 每秒读取的block数.

KB_wrtn/s: 每秒写入的block数.

KB_read:  启动到现在 读入的block总数.

KB_wrtn:  启动到现在写入的block总数.
```

查看帮助：

```
$ man iostat
```


###2.9 实时局域网IP监控：IPTraf

   IPTraf是一个在Linux控制台运行的、开放源代码的实时网络（局域网）监控应用。它采集了大量信息，比如通过网络的IP流量监控，包括TCP标记、ICMP详细信息、TCP/UDP流量分离、TCP连接包和字节数。同时还采集有关接口状态的常见信息和详细信息：TCP、UDP、IP、ICMP、非IP，IP校验和错误，接口活动等。
```
$ sudo apt-get install iptraf

$ sudo iptraf
```

操作截图（**注意图片中下面的提示操作信息。**）：

![1-2.9-1](https://doc.shiyanlou.com/userid42227labid972time1430728942721/wm)

![1-2.9-2](https://doc.shiyanlou.com/userid42227labid972time1430728963781/wm)


查看命令帮助信息,根据需要选择合适的参数，进行监控。此处便不再赘述命令参数：
```
$ sudo iptraf -h
```


###参考文档：

1.http://www.bitscn.com/os/linux/201405/199059.html

