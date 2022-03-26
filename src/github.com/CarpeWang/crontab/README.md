# worker

woker的功能：

任务同步：监听ETCD中的/cron/jobs目录变化。

任务调度：基于cron表达式计算，触发过期任务。

任务执行：协程池并发执行多任务，基于ETCD分布式锁抢占。

日志捕获：捕获任务执行输出，并且保存在MONGDB中。



# ETCD

保存到ETCD中的任务，会实时同步到所有的worker中。

```结构```

/cron/jobs/->任务名{

    name //任务名
    command //命令
    cronExpr//cron表达式

}


# MONGDB

JobName：任务名

Command：命令

err：相关错误

output：执行输出

startTime：开始时间

endTime：结束时间。
