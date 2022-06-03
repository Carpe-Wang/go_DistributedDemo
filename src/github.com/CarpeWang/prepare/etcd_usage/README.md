
## [put](https://github.com/Carpe-Wang/go_DistributedDemo/blob/main/src/github.com/CarpeWang/prepare/etcd_usage/demo2/main.go)
> put
```go
import (
	"context"
	"fmt"
	clientv3 "go.etcd.io/etcd/client/v3"
	"time"
)

func main() {
	var (
		config  clientv3.Config
		client  *clientv3.Client
		err     error
		kv      clientv3.KV
		putResp *clientv3.PutResponse
	)

	config = clientv3.Config{
		Endpoints:   []string{"101.43.141.65:2379"}, // 集群列表
		DialTimeout: 5 * time.Second,
	}

	// 建立一个客户端
	if client, err = clientv3.New(config); err != nil {
		fmt.Println(err)
		return
	}

	// 用于读写etcd的键值对
	kv = clientv3.NewKV(client)

	if putResp, err = kv.Put(context.TODO(), "/cron/jobs/job1", "bye", clientv3.WithPrevKV()); err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("Revision:", putResp.Header.Revision)
		if putResp.PrevKv != nil { // 打印hello
			fmt.Println("PrevValue:", string(putResp.PrevKv.Value))
		}
	}
}
```

## [get](https://github.com/Carpe-Wang/go_DistributedDemo/blob/main/src/github.com/CarpeWang/prepare/etcd_usage/demo2/main.go)
>get

```go
func main() {
	var (
		config  clientv3.Config
		client  *clientv3.Client
		err     error
		kv      clientv3.KV
		getResp *clientv3.GetResponse
	)

	config = clientv3.Config{
		Endpoints:   []string{"101.43.141.65:2379"}, // 集群列表就是服务器ip
		DialTimeout: 5 * time.Second,
	}

	// 建立一个客户端
	if client, err = clientv3.New(config); err != nil {
		fmt.Println(err)
		return
	}

	// 用于读写etcd的键值对
	kv = clientv3.NewKV(client)

	if getResp, err = kv.Get(context.TODO(), "name" /*clientv3.WithCountOnly()*/); err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(getResp.Kvs, getResp.Count)
	}
}
```
