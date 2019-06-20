在select中如何理解<-time.After(time.Second * 3)
-----
理解
```
3秒内没有接受到数据，则执行该case
```
程序
```
package main

import (
	"fmt"
	"time"
)

//发送者
func sender(c chan int) {
	for i := 0; i < 100; i++ {
		c <- i
		if i >= 5 {
			time.Sleep(time.Second * 7)
		} else {
			time.Sleep(time.Second)
		}
	}
}

func main() {
	c := make(chan int)
	go sender(c)
	timeout := time.After(time.Second * 3)
	for {
		select {
		case d := <-c:
			fmt.Println(d)
		case <-timeout:
			fmt.Println("这是定时操作任务 >>>>>")
		case dd := <-time.After(time.Second * 3):
			fmt.Println(dd, "这是超时*****")
		}

		fmt.Println("for end")
	}
}
```
执行结果
```
0
for end
1
for end
2
for end
这是定时操作任务 >>>>>
3
for end
4
for end
5
for end
这是超时*****"
for end
这是超时*****"
for end
6
for end
这是超时*****"
for end
这是超时*****"
for end
7
for end
这是超时*****"
for end
这是超时*****"
for end
8
for end
这是超时*****"
for end
这是超时*****"
for end
```
[参考](https://studygolang.com/articles/10229)
