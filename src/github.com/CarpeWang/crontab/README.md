# worker

woker的功能：

任务同步：监听ETCD中的/cron/jobs目录变化。

任务调度：基于cron表达式计算，触发过期任务。

任务执行：协程池并发执行多任务，基于ETCD分布式锁抢占。
