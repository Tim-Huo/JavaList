### 索引：

[https://blog.csdn.net/mysteryhaohao/article/details/51719871](https://blog.csdn.net/mysteryhaohao/article/details/51719871)

### 回表：

在流程中从非主键索引树搜索回到主键索引树搜索的过程。

### 覆盖索引：

覆盖索引是select的数据列只用从索引中就能够取得，不必读取数据行，换句话说查询列要被所建的索引覆盖。

### 为什么使用B+树，而不是其它树？

#### 二叉查找树：

节点随机构成，可能会退化成一个线性表。

#### AVL树（平衡二叉树）：

平衡二叉树的条件时左右子树不超过1，所以添加与删除需要多次左右旋转来保持平衡，比较耗时，适合插入删除比较少，查找多的情况。

#### 红黑树：

红黑树是一种平衡二叉树，数据多的时候会造成树的深度过大，IO读写过于频繁，进而导致效率低下。

### 判断Mysql是否使用了索引：

explain显示了MySQL如何使用索引来处理select语句以及连接表。

explain关键字的使用方法很简单，就是把它放在select查询语句的前面。

mysql查看是否使用索引，简单的看type类型就可以。如果它是all，那说明这条查询语句遍历了所有的行，并没有使用到索引。

![图片](https://uploader.shimo.im/f/X5wayTEoTyeoeaVU.png!thumbnail)

