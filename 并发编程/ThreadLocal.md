ThreadLocal是一个关于创建线程局部变量的类。

通常情况下，我们创建的变量是可以被任何一个线程访问并修改的。而使用ThreadLocal创建的变量只能被当前线程访问，其他线程则无法访问和修改。

### 实现原理

* 首先获取当前线程
* 利用当前线程作为句柄获取一个ThreadLocalMap的对象
* 如果上述ThreadLocalMap对象不为空，则设置值，否则创建这个ThreadLocalMap对象并设置值。
```java
public void set(T value) {
    Thread t = Thread.currentThread();
    ThreadLocalMap map = getMap(t);
    if (map != null)
        map.set(this, value);
    else
        createMap(t, value);
}
```
### ThreadLocal的实例存放在哪里？

ThreadLocal实例实际上也是被其创建的类持有（更顶端应该是被线程持有）。而ThreadLocal的值其实也是被线程实例持有。

它们都是位于堆上，只是通过一些技巧将可见性修改成了线程可见。

