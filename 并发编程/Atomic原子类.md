### Atomic简介：

Atomic 是指一个操作是不可中断的。即使是在多个线程一起执行的时候，一个操作一旦开始，就不会被其他线程干扰。

### 基本类型

* AtomicInteger：整型原子类
* AtomicLong：长整型原子类
* AtomicBoolean ：布尔型原子类

AtomicInteger 类主要利用 CAS (compare and swap) + volatile来保证原子操作，调用了AtomicInteger 的方法调用了 Unsafe 类的 CAS 操作，从而避免 synchronized 的高开销，执行效率大为提升。

### 数组类型

* AtomicIntegerArray：整型数组原子类
* AtomicLongArray：长整型数组原子类
* AtomicReferenceArray ：引用类型数组原子类
### 引用类型

* AtomicReference：引用类型原子类
* AtomicMarkableReference：原子更新带有标记的引用类型。该类将 boolean 标记与引用关联起来。
* AtomicStampedReference ：原子更新带有版本号的引用类型。该类将整数值与引用关联起来，可用于解决原子的更新数据和数据的版本号，可以解决使用 CAS 进行原子更新时可能出现的 ABA 问题。
### 对象的属性修改类型

* AtomicIntegerFieldUpdater:原子更新整型字段的更新器
* AtomicLongFieldUpdater：原子更新长整型字段的更新器
* AtomicReferenceFieldUpdater：原子更新引用类型里的字段

