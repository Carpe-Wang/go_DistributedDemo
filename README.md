# go_distributedDemo

涉及的系统调用

    pipe():创建两个文件描述符，fd[0]可读，fd[1]可写。
    
    fork():创建子进程，fd[1]被继承到子进程（拿到子进程写入端）。
    
    dup2():重定向到子进程stdout/stderr到fd[1]。
    
    exec():在当前进程内，加载并执行二进制程序。
    
    
通过Command类执行人物
定义在os/exec包。
封装上述底层细节。
    Cron的标准表达格式
    
    分(0-59)
    
    时(0-23)
    
    日(1-31)
    
    月(1-12)
    
    星期(0-7)
    
    
Command--->shell

Cron常见命令

    每隔5分钟执行一次:*/5**** echo hello >/temp/x.log。。。注意执行流程，是时间均分，这是一个基础。
    
    第1-5分钟执行一次:1-5 * * * */usr/bin/go/data/main.go。
    
    每天10点，22点整点执行1次:0 10,22 *** echo byte |tail -1。


Cron调度原理
    例如当前时间为2022年3月22日，14:37:00，对应执行流程为Cron 30 ****
    
    先把这个案例梳理完善，下次调度时间为：15:30分。可以参考Cronexpr
    
    parse()：解析校验cron表达式。
    
    next():根据当前时间计算下次执行时间 。


ETCD原理
    核心特性：
    
      将数据存储到高可用的k-v。
      
      允许应用时监听k-v变化。
      
      容忍单点故障，对应网络分区。
      
    k8s：
    
      etcd：
        
        服务发现
        
        配置同步
        
        集群状态存储


etcd和Raft的关系
      
      Raft是一个强一致的同步集群日志同步算法
      
      etcd是利用Raft算法实现集群中同步k-v


简单原理图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/276927d733844de9bd3174031ec03abd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2FycGUtV2FuZw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


