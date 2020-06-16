### CopyOnWriteArrayList（读写分离）:

**1****、读写分离**

写操作在一个复制的数组上进行，读操作还是在原始数组中进行，读写分离，互不影响。

写操作需要加锁，防止并发写入时导致写入数据丢失。

写操作结束之后需要把原始数组指向新的复制数组。

**2、适用场景**

CopyOnWriteArrayList 在写操作的同时允许读操作，大大提高了读操作的性能，因此很适合读多写少的应用场景。

但是 CopyOnWriteArrayList 有其缺陷：

* 内存占用：在写操作时需要复制一个新的数组，使得内存占用为原来的两倍左右；
* 数据不一致：读操作不能读取实时性的数据，因为部分写操作的数据还未同步到读数组中。

所以 CopyOnWriteArrayList 不适合内存敏感以及对实时性要求很高的场景。

### ConcurrentHashMap（线程安全的HashMap）:

ConcurrentHashMap 采用了分段锁（Segment），每个分段锁维护着几个桶（HashEntry），多个线程可以同时访问不同分段锁上的桶，从而使其并发度更高（并发度就是 Segment 的个数）。

JDK 1.7 使用分段锁机制来实现并发更新操作，核心类为 Segment，它继承自重入锁 ReentrantLock，并发度与 Segment 数量相等。

JDK 1.8 使用了 CAS 操作来支持更高的并发度，在 CAS 操作失败时使用内置synchronized。

### ConcurrentLinkedQueue（非阻塞队列）:

它是是非阻塞队列，节点是用volatile修饰的保障线程间可见，使用 CAS 非阻塞算法来实现线程安全。

**适用场景：**

如果对队列加锁的成本较高则适合使用无锁的 ConcurrentLinkedQueue 来替代。

### BlockingQueue（阻塞队列）：

阻塞队列。 BlockingQueue 提供了可阻塞的插入和移除的方法。当队列容器已满，生产者线程会被阻塞，直到队列未满；当队列容器为空时，消费者线程会被阻塞，直至队列非空时为止。

### ArrayBlockingQueue（有界阻塞队列，FIFO）:

ArrayBlockingQueue 是 BlockingQueue 接口的有界队列实现类，底层采用数组来实现。ArrayBlockingQueue 一旦创建，容量不能改变。其并发控制采用可重入锁来控制，不管是插入操作还是读取操作，都需要获取到锁才能进行操作。当队列容量满时，尝试将元素放入队列将导致操作阻塞;尝试从一个空队列中取一个元素也会同样阻塞。

ArrayBlockingQueue 默认情况下不能保证线程访问队列的公平性，如果保证公平性，通常会降低吞吐量。

### LinkedBlockingQueue（有无界阻塞队列，FIFO）：

LinkedBlockingQueue 底层基于单向链表实现的阻塞队列，可以当做无界队列也可以当做有界队列来使用，同样满足 FIFO 的特性，与 ArrayBlockingQueue 相比起来具有更高的吞吐量，为了防止 LinkedBlockingQueue 容量迅速增，损耗大量内存。通常在创建LinkedBlockingQueue 对象时，会指定其大小，如果未指定，容量等于 Integer.MAX_VALUE。

### PriorityBlockingQueue（无界阻塞队列，优先级）：

PriorityBlockingQueue 是一个支持优先级的无界阻塞队列，默认情况下元素采用自然顺序进行排序，PriorityBlockingQueue 并发控制采用的是 ReentrantLock，不可以插入 null 值。

### ConcurrentSkipListMap：

ConcurrentSkipListMap提供了一种线程安全的并发访问的排序映射表。内部是SkipList（跳表）结构实现，在理论上能够在O(log(n))时间内完成查找、插入、删除操作。


