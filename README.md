# ringbuffer，双向环形链表

* 双向环形链表buf其结构类似于一个手串，手串上的珠子就可以当做是一个节点，每个节点可以是一个固定大小的数组
* 双向环形链表buf上分别有两个读写指针readCell和writeCell，指向将要进行读写操作的cell，负责进行数据读写
* readCell永远追赶writeCell，当追上时，代表写满了，进行扩容操作
* 扩容操作即在写指针的后面插入一个新建的空闲cell
* 缩容操作修改链表指向即可，让buf恢复原样，仅保持两个cell即可，其他cell由于不再被引用，会被GC自动回收
* 在链表写入(Write)和读取(Read)时用原子操作修改链表有效数据长度count

## 安装使用

```go
$ go get -u github.com/zngw/ringbuffer
```