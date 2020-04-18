# JUC

1. Arraylist 线程不安全，其方法没有添加 synchronized 修饰。改进：
   - 使用 Vector，Vector 线程安全，使用 synchronized
   - 使用 Collections.synchronizedList(new ArrayList<>())
   - 使用 new CopyOnWriteArrayList<>()，使用 lock 锁
2. HashSet 线程不安全，改进：
   - 使用 Collections.synchronizedSet(new HashSet<>())
   - 使用 new CopyOnWriteArraySet<Object>()
3. 

## Lock

1 同步队列
2 条件队列
3 不同的 acquireQueued
4 tryAcquire

ReentrantLock的底层是AQS，通过控制state完成一些锁特有的特性：重入、公平与非公平、读写锁(后面的文章会说明)
获取锁就是当前线程成功修改了AQS的volatile成员state
获取锁失败就进入到了AQS的等待队列（FIFO的双向无环链表），进入到等待队列之后开始自旋，当前节点的waitStatus=-1之后lockSupport.park()挂起自己，等待唤醒
获取锁的线程释放锁（state执行减操作），唤醒head节点之后第一个未取消的等待节点
head节点之后第一个未取消的等待节点被唤醒，判断prev是否为head 是head则尝试获取所，将自己设置为head节点，将原先老的head移除等待队列。

## CopyOnWriteArrayList

关键词：
1）线程安全的List
2）脏读
3）写时复制COW
4）底层volatile Object[] 初始0长度
5）读多写少场景

## ArrayBlockingQueue

BlockingQueue 不接受 null 元素
BlockingQueue 可以是限定容量的 没有的话就是Integer.MAX_VALUE
BlockingQueue 实现主要用于生产者-使用者队列，但它另外还支持 Collection 接口
BlockingQueue 实现是线程安全的

1）ArrayBlockingQueue是有界的阻塞队列，不接受null
2）底层数据接口是数组，下标putIndex/takeIndex，构成一个环形FIFO队列
3）所有的增删改查数组公用了一把锁ReentrantLock，入队和出队数组下标和count变更都是靠这把锁来维护安全的。
4）阻塞的场景：1获取lock锁，2进入和取出还要满足condition 满了或者空了都等待出队和加入唤醒，ArrayBlockingQueue我们主要是put和take真正用到的阻塞方法（条件不满足）。
5）成员cout /putIndex、takeIndex是共享的,所以一些查询方法size、peek、toString、方法也是加上锁保证线程安全，但没有了并发损失了性能。
6）remove(Object obj) 返回了第一个equals的Object

