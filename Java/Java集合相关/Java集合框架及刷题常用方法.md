> 集合：集合是储存对象的长度可变的容器，主要分为单列集合`java.util.Collection`和双列集合`java.util.Map`

# 1 单列集合

![collection](.\img\collection.png)



### (1) Collection的方法

```java
Collection：单列集合类的根接口，用于存储一系列符合某种规则的元素，它有两个重要的子接口，分别是java.util.List和java.util.Set。其中，List的特点是元素有序、元素可重复。Set的特点是元素无序，而且不可重复。其中List常用有 Vector集合，ArrayList集合 、LinkedList集合 。Set常用有TreeSet和HashSet，LinkedHashSet。

适用于集合的方法
public boolean add(E e)： 把给定的对象添加到当前集合中 ，返回是否添加成功

public boolean remove(E e): 把给定的对象在当前集合中删除。

public void clear() :清空集合中所有的元素。

public boolean contains(E e): 判断当前集合中是否包含给定的对象。

public boolean isEmpty(): 判断当前集合是否为空。

public int size(): 返回集合中元素的个数。

public Object[] toArray(): 把集合中的元素，存储到数组中。默认传回的是 Object[] 通过增加参数 toArray（new String [n]） 可以传回 包装类数组，但不能直接生成基本类型的数组 如int[];
```



## (2) List 元素存取有序、有索引、可重复

####  适用List的方法

```java
public void add(int index, E element): 将指定的元素，添加到该集合中的指定位置上。
public E get(int index):返回集合中指定位置的元素。
public E remove(int index): 移除列表中指定位置的元素, 返回的是被移除的元素。
public E set(int index, E element):用指定元素替换集合中指定位置的元素,返回值的更新前的元素。
```

#### ArrayList集合

```java
java.util.ArrayList集合底层结构为动态数组，初始容量10，超出自动扩容。元素增删慢，查找快。

没有什么单独方法，与List通用方法一致。
```

#### Vector

```java
Vector实现了可变数组，与ArrayList类似 ，但Vector是线程安全的。子类为Stack。
```

#### Stack

```java
Stack的常用方法

E push(E item) 把项压入堆栈顶部。
E pop() 移除堆栈顶部的对象，并作为此函数的值返回该对象。
E peek() 查看堆栈顶部的对象，但不从堆栈中移除它。
boolean empty() 测试堆栈是否为空。
int search(Object o) 返回对象在堆栈中的位置，以 1 为基数。
```

#### LinkedList集合

```java
java.util.LinkedList集合数据存储的结构是链表结构。底层为双向链表，方便元素添加、删除的集合。常用于模拟队列、双端队列，堆栈 。

常用方法

LinkedList(Collection<? extends E> c) 通过复制方式生成一个新链表，可用于回溯算法保存路径。

get(int index)按照下标获取元素。

peek()获取第一个元素，但是不移除。

——————模拟双端链表的方法————————————

peekFirst()获取第一个元素，但是不移除；

peekLast()获取最后一个元素，但是不移除；

getFirst()获取第一个元素。

getLast()获取最后一个元素。

public void addFirst(E e):将指定元素插入此列表的开头。

public void addLast(E e):将指定元素添加到此列表的结尾。

public E removeFirst():移除并返回此列表的第一个元素。

public E removeLast():移除并返回此列表的最后一个元素。

public E getFirst():返回此列表的第一个元素。

public E getLast():返回此列表的最后一个元素。

——————模拟堆栈的方法————————

public E pop():从此列表所表示的堆栈处弹出一个元素。

public void push(E e):将元素推入此列表所表示的堆栈。

备注：增删改查 不写明First Last，使用List的通用方法则默认操作第一个元素如get(),remove()。

add/offer、 poll/romove 、peek/element的区别

队列满时， offer()返回false， add()会抛出一个异常

队列为空时， poll()返回null remove（）抛出一个异常

队列为空时，peek() 返回 null ，而 element() 抛出一个异常
```



## (3) Set

> 在JDK1.8之前，哈希表底层采用数组+链表实现，即使用链表处理冲突，同一hash值的链表都存储在一个链表里。但是当位于一个桶中的元素较多，即hash值相等的元素较多时，通过key值依次查找的效率较低。而JDK1.8中，哈希表存储采用数组+链表+红黑树实现，当链表长度超过阈值（8）时，将链表转换为红黑树，这样大大减少了查找时间。

#### HashSet

```java
HashSet集合，采用哈希表结构存储数据，保证元素唯一性的方式依赖于：hashCode()与equals()方法。

常用方法与集合通用方法一致。

public boolean add(E e)： 把给定的对象添加到当前集合中 ，返回是否添加成功
public boolean remove(E e): 把给定的对象在当前集合中删除。
public void clear() :清空集合中所有的元素。
public boolean contains(E e): 判断当前集合中是否包含给定的对象。
public boolean isEmpty(): 判断当前集合是否为空。
public int size(): 返回集合中元素的个数。
```

#### LinkedHashSet

```java
HashSet下面有一个子类LinkedHashSet，它是链表和哈希表组合的一个数据存储结构。
```

#### TreeSet

```java
TreeSet底层为TreeMap，提供了有序的Set集合。
```



# 2 双列集合

![map](.\img\map.png)



> Java提供了专门的集合类用来存放K-V映射关系的对象，即`java.util.Map`接口。`Map`中的集合不能包含重复的键，值可以重复；每个键只能对应一个值。



#### HashMap

```java
HashMap<K,V>：存储数据采用的哈希表结构，元素的存取顺序不能保证一致。由于要保证键的唯一、不重复，需要重写键的hashCode()方法、equals()方法。
LinkedHashMap<K,V>：HashMap下有个子类LinkedHashMap，存储数据采用的哈希表结构+链表结构。通过链表结构可以保证元素的存取顺序一致，某些算法题中可以借此提高一点点效率；通过哈希表结构可以保证的键的唯一、不重复，需要重写键的hashCode()方法、equals()方法。
```



#### Map集合常用的方法

```java
public V put(K key, V value): 把指定的键与指定的值添加到Map集合中。key已经存在则新的value会覆盖旧的。

public V remove(Object key): 把指定的键 所对应的键值对元素 在Map集合中删除，返回被删除元素的值。

public V get(Object key) 根据指定的键，在Map集合中获取对应的值。

boolean containsKey(Object key) 判断集合中是否包含指定的键。
```



#### 遍历Map常用的方法

````java
public Set keySet()`: 获取Map集合中所有的键，存储到Set遍历中。

public Set<Map.Entry<K,V>> entrySet(): 获取到Map集合中所有的键值对对象的集合(Set集合)。

public K getKey()：获取Entry对象中的键。

public V getValue()：获取Entry对象中的值。
