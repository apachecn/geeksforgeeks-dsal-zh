# 设计用于 LRU 缓存

> 原文：[https://www.geeksforgeeks.org/design-a-data-structure-for-lru-cache/](https://www.geeksforgeeks.org/design-a-data-structure-for-lru-cache/)

的数据结构

为 [LRU 缓存](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)设计数据结构。 它应支持以下操作**：获取**和**设置**。

**get（key）** –如果密钥存在于缓存中，则获取密钥的值（始终为正），否则返回-1。

**set（key，value）** –如果密钥不存在，则设置或插入值。 当缓存达到其容量时，它应在插入新项目之前使最近最少使用的项目无效。

例子：

> //假设我们有一个容量为 2 的 LRU 缓存。
> LRUCache cache = new LRUCache（2）;
> 
> cache.set（1，10）; //它将在缓存中存储值为 10 的键（1）。
> cache.set（2，20）; //它将在缓存中存储值为 20 的键（2）。
> cache.get（1）; //返回 10
> cache.set（3，30）; //退出键 2，并将值 30 的键（3）存储在缓存中。
> cache.get（2）; //返回-1（未找到）
> cache.set（4，40）; //退出键 1，并将值 40 的键（4）存储在高速缓存中。
> cache.get（1）; //返回-1（未找到）
> cache.get（3）; //返回 30
> cache.get（4）; //返回 40

**询问**：Adob​​e，Hike 等多家公司。

**解决方案**：

**1.暴力破解方法**：

我们将保留一个节点数组，每个节点将包含以下信息：

```
class Node {
int key;
int value;
[
// it shows the time at which the key is stored.
// We will use the timeStamp to find out the
// least recently used (LRU) node.
int timeStamp;
public Node( int key, int value)
{
this .key = key;
this .value = value;
// currentTimeStamp from system
this .timeStamp = currentTimeStamp;
}
}
```

数组的大小将等于给定的缓存容量。

**（a）**对于**，请获取** **（int 键）**：我们可以简单地遍历数组，并将每个节点的键与给定键进行比较，然后返回值 存储在该键的节点中。 如果找不到任何这样的节点，则简单地返回-1。

时间复杂度： **`O(n)`**

**（b）**对于**，设置** **（int 键，整数值）**：如果数组已满，则必须从数组中删除一个节点。 为了找到 LRU 节点，我们将遍历数组并找到 timeStamp 值最小的节点。 我们将简单地在 LRU 节点的位置插入新节点（具有新的键和值）。

如果数组未满，我们可以简单地在数组的最后一个当前索引处在数组中插入一个新节点。

时间复杂度： **`O(n)`**

**2.优化方法**：

解决此问题的关键是使用双链表，该链表使我们能够快速移动节点。

LRU 缓存是键和双链接节点的哈希映射。 哈希映射使 get（）的时间为`O(1)`。 双向链接节点列表使节点添加/删除操作为`O(1)`。

**使用双链表和 HashMap 的 Java 代码**：

```
import java.util.HashMap;
class Node {
int key;
int value;
Node pre;
Node next;
的
public Node( int key, int value)
{
this .key = key;
this .value = value;
}
}
class LRUCache {
private HashMap<Integer, Node> map;
private int capicity, count;
private Node head, tail;
public LRUCache( int capacity)
{
[HTG5 6] .capicity = capacity;
map = new HashMap<>();
head = new Node( 0 , 0 );
tail = new Node( 0 , 0 );
head.next = tail;
]          tail.pre = head;
head.pre = null ;
tail.next = null ;
count = 0 ;
}
public void deleteNode(Node node)
{
node.pre.next = node.next;
node.next.pre = node.pre;
}
public void addToHead(Node node)
{
node.next = head.next; [
node.next.pre = node;
node.pre = head;
head.next = node;
}
[HTG126
// This method works in O(1)
public int get( int key)
{
if (map.get(key) != null ) {
Node node = map.get(key);
int result = node.value;
deleteNode(node);
addToHead(node);
System.out.println( "Got the value : " +
result + " for the key: " + key);
return result;
}
System.out.println( "Did not get any value" +
" for the key: " + key);
return - 1 ;
}
// This method works in O(1)
public void set( int ] key, int value)
{
System.out.println( "Going to set the (key, " +
"value) : (" + key + ", " + value + ")" );
if (map.get(key) != null ) {
Node node = map.get(key);
node.value = value;
deleteNode(node);
addToHead(node);
}
else {
Node node = new Node(key, value);
map.put(key, node);
if (count < capicity) {
count++;
addToHead(node);
}
else {
map.remove(tail.pre.key);
deleteNode(tail.pre);
addToHead(node);
}
}
}
}
public class TestLRUCache {
public static void main(String[] args)
{
System.out.println( "Going to test the LRU " +
" Cache Implementation" );
LRUCache cache = new LRUCache( 2 );
// it will store a key (1) with value
// 10 in the cache.
cache.set( 1 , 10 );
// it will store a key (1) with value 10 in the cache.
cache.set( 2 , 20 );
System.out.println( "Value for the key: 1 is " +
cache.get( 1 )); // returns 10
// evicts key 2 and store a key (3) with
// value 30 in the cache.
cache.set( 3 , 30 );
System.out.println( "Value for the key: 2 is " +
cache.get( 2 )); // returns -1 (not found)
// evicts key 1 and store a key (4) with
// value 40 in the cache.
cache.set( 4 , 40 );
System.out.println( "Value for the key: 1 is " +
cache.get( 1 )); // returns -1 (not found)
System.out.println( "Value for the key: 3 is " +
[H TG350] 3 )); // returns 30
System.out.println( "Value for the key: 4 is " +
cache.get( 4 )); // return 40
}
}
```

**Output:**

```
Going to test the LRU  Cache Implementation
Going to set the (key, value) : (1, 10)
Going to set the (key, value) : (2, 20)
Got the value : 10 for the key: 1
Value for the key: 1 is 10
Going to set the (key, value) : (3, 30)
Did not get any value for the key: 2
Value for the key: 2 is -1
Going to set the (key, value) : (4, 40)
Did not get any value for the key: 1
Value for the key: 1 is -1
Got the value : 30 for the key: 3
Value for the key: 3 is 30
Got the value : 40 for the key: 4
Value for the key: 4 is 40

```

**Java 中使用 LinkedHashMap 的另一种实现**：

**removeEldestEntry** （）被重写，以强加一个在大小超出容量时删除旧映射的策略。

```
import java.util.LinkedHashMap;
import java.util.Map;
class LRUCache {
private LinkedHashMap<Integer, Integer> map;
private final int CAPACITY;
public LRUCache( int capacity)
{
CAPACITY = capacity;
map = new LinkedHashMap<Integer, Integer>(capacity, 0 .75f, true ) {
protected boolean removeEldestEntry(Map.Entry eldest)
{
return size() > CAPACITY;
}
};
}
// This method works in O(1)
public int get( int key)
{
System.out.println( "Going to get the value " +
"for the key : " + key);
return map.getOrDefault(key, - 1 );
}
// This method works in O(1)
public void set( int key, int value)
{
System.out.println( "Going to set the (key, " +
"value) : (" + key + ", " + value + ")" );
map.put(key, value);
}
}
public class TestLRUCacheWithLinkedHashMap {
public static void main(String[] args)
]      {
System.out.println( "Going to test the LRU " +
" Cache Implementation" );
[ H T G121] new LRUCache( 2 );
// it will store a key (1) with value
// 10 in the cache.
cache.set( 1 , 10 );
// it will store a key (1) with value 10 in the cache.
cache.set( 2 , 20 );
System.out.println( "Value for the key: 1 is " +
cache.get( 1 )); // returns 10
// evicts key 2 and store a key (3) with
// value 30 in the cache.
cache.set( 3 , 30 );
System.out.println( "Value for the key: 2 is " +
cache.get( 2 )); // returns -1 (not found)
// evicts key 1 and store a key (4) with
[HTG18 0]
cache.set( 4 , 40 );
System.out.println( "Value for the key: 1 is " +
cache.get( 1 )); // returns -1 (not found)
System.out.println( "Value for the key: 3 is " +
cache.get( 3 )); // returns 30
System.out.println( "Value for the key: 4 is " +
cache.get( 4 )); // return 40
[
}
}
```

**Output:**

```
Going to test the LRU  Cache Implementation
Going to set the (key, value) : (1, 10)
Going to set the (key, value) : (2, 20)
Going to get the value for the key : 1
Value for the key: 1 is 10
Going to set the (key, value) : (3, 30)
Going to get the value for the key : 2
Value for the key: 2 is -1
Going to set the (key, value) : (4, 40)
Going to get the value for the key : 1
Value for the key: 1 is -1
Going to get the value for the key : 3
Value for the key: 3 is 30
Going to get the value for the key : 4
Value for the key: 4 is 40

```

您可以在中找到 C++代码



* * *

* * *



