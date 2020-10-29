# 负载因子和哈希值

> 原文：[https://www.geeksforgeeks.org/load-factor-and-rehashing/](https://www.geeksforgeeks.org/load-factor-and-rehashing/)

先决条件：[哈希介绍](https://www.geeksforgeeks.org/hashing-set-1-introduction/)和[通过单独链接](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)的冲突处理

### 哈希如何工作：

要将键（K）–值（V）对的**插入**，则需要 2 个步骤：

1.  使用哈希函数将 K 转换为小整数（称为其哈希码）。

2.  哈希码用于查找索引（hashCode％arrSize），并且首先在该索引处的整个链表（单独链接）中搜索 K 的存在。

3.  如果找到，则会更新其值；如果未找到，则 K-V 对将作为新节点存储在列表中。

### 复杂度和负载系数

*   对于**第一步**，花费的时间取决于 K 和哈希函数。

    例如，如果键是字符串“ abcd”，则其哈希函数可能取决于字符串的长度。 但是，对于非常大的 n 值（映射中的条目数，键的长度），与 n 相比几乎可以忽略不计，因此可以认为哈希计算是在恒定时间进行的，即 **`O(1)`[** 。

*   对于**第二步**，需要遍历该索引处存在的 K-V 对列表。 为此，最坏的情况可能是所有 n 个条目都位于同一索引处。 因此，时间复杂度将为 **`O(n)`**。 但是，已经进行了足够的研究来使哈希函数将键均匀地分布在数组中，因此几乎永远不会发生这种情况。

*   因此，平均为**，如果有 n 个条目并且 b 是数组的大小，则每个索引上将有 n / b 个条目。 此值 n / b 称为**负载系数**，它表示映射上的负载。**

*   该负载因数需要保持较低，以使一个索引处的条目数减少，并且复杂度几乎恒定，即`O(1)`。

### 重新哈希：

顾名思义，**重新哈希表示再次哈希**。 基本上，当负载系数增加到大于其预定值时（负载系数的默认值为 0.75），复杂度就会增加。 因此，要克服此问题，将增加数组的大小（将其加倍），并再次对所有值进行哈希处理，并将其存储在新的两倍大小的数组中，以保持较低的加载因子和较低的复杂度。

##### 为什么要重新哈希处理？

因为每当将键值对插入到映射中时，负载因子都会增加，因此进行了哈希处理，这意味着时间复杂度也如上所述增加了。 这可能无法给出`O(1)`所需的时间复杂度。

因此，必须进行重新哈希处理，增加 bucketArray 的大小，以减少负载因子和时间复杂度。

##### 重新哈希如何完成？

重新哈希处理可以如下进行：

*   对于在映射上每次添加新条目的情况，请检查负载系数。

*   如果大于预定义的值（如果未提供默认值，则为 0.75），然后重新进行哈希处理。

*   对于 Rehash，请创建一个新数组，其大小是以前的两倍，并使其成为新的 bucketarray。

*   然后遍历旧的 bucketArray 中的每个元素，并为每个元素调用 insert（），以将其插入新的更大的 bucket 数组中。

### 实施重新哈希处理的程序：

```
// Java program to implement Rehashing
import java.util.ArrayList;
class Map<K, V> {
class MapNode<K, V> {
K key;
V value;
MapNode<K, V> next;
public MapNode(K key, V value)
{
this.key = key;
this.value = value;
next = null;
}
}
// The bucket array where
// the nodes containing K-V pairs are stored
ArrayList<MapNode<K, V> > buckets;
// No. of pairs stored - n
int size;
// Size of the bucketArray - b
int numBuckets;
// Default loadFactor
final double DEFAULT_LOAD_FACTOR = 0.75;
public Map()
{
numBuckets = 5;
buckets = new ArrayList<>(numBuckets);
for (int i = 0; i < numBuckets; i++) {
// Initialising to null
buckets.add(null);
}
System.out.println("HashMap created");
System.out.println("Number of pairs in the Map: " + size);
System.out.println("Size of Map: " + numBuckets);
System.out.println("Default Load Factor : " + DEFAULT_LOAD_FACTOR + "\n");
}
private int getBucketInd(K key)
{
// Using the inbuilt function from the object class
int hashCode = key.hashCode();
// array index = hashCode%numBuckets
return (hashCode % numBuckets);
}
public void insert(K key, V value)
{
// Getting the index at which it needs to be inserted
int bucketInd = getBucketInd(key);
// The first node at that index
MapNode<K, V> head = buckets.get(bucketInd);
// First, loop through all the nodes present at that index
// to check if the key already exists
while (head != null) {
// If already present the value is updated
if (head.key.equals(key)) {
head.value = value;
return;
}
head = head.next;
}
// new node with the K and V
MapNode<K, V> newElementNode = new MapNode<K, V>(key, value);
// The head node at the index
head = buckets.get(bucketInd);
// the new node is inserted
// by making it the head
// and it's next is the previous head
newElementNode.next = head;
buckets.set(bucketInd, newElementNode);
System.out.println("Pair(" + key + ", " + value + ") inserted successfully.\n");
// Incrementing size
// as new K-V pair is added to the map
size++;
// Load factor calculated
double loadFactor = (1.0 * size) / numBuckets;
System.out.println("Current Load factor = " + loadFactor);
// If the load factor is > 0.75, rehashing is done
if (loadFactor > DEFAULT_LOAD_FACTOR) {
System.out.println(loadFactor + " is greater than " + DEFAULT_LOAD_FACTOR);
System.out.println("Therefore Rehashing will be done.\n");
// Rehash
rehash();
System.out.println("New Size of Map: " + numBuckets + "\n");
}
System.out.println("Number of pairs in the Map: " + size);
System.out.println("Size of Map: " + numBuckets + "\n");
}
private void rehash()
{
System.out.println("\n***Rehashing Started***\n");
// The present bucket list is made temp
ArrayList<MapNode<K, V> > temp = buckets;
// New bucketList of double the old size is created
buckets = new ArrayList<MapNode<K, V> >(2 * numBuckets);
for (int i = 0; i < 2 * numBuckets; i++) {
// Initialised to null
buckets.add(null);
}
// Now size is made zero
// and we loop through all the nodes in the original bucket list(temp)
// and insert it into the new list
size = 0;
numBuckets *= 2;
for (int i = 0; i < temp.size(); i++) {
// head of the chain at that index
MapNode<K, V> head = temp.get(i);
while (head != null) {
K key = head.key;
V val = head.value;
// calling the insert function for each node in temp
// as the new list is now the bucketArray
insert(key, val);
head = head.next;
}
}
System.out.println("\n***Rehashing Ended***\n");
}
public void printMap()
{
// The present bucket list is made temp
ArrayList<MapNode<K, V> > temp = buckets;
System.out.println("Current HashMap:");
// loop through all the nodes and print them
for (int i = 0; i < temp.size(); i++) {
// head of the chain at that index
MapNode<K, V> head = temp.get(i);
while (head != null) {
System.out.println("key = " + head.key + ", val = " + head.value);
head = head.next;
}
}
System.out.println();
}
}
public class GFG {
public static void main(String[] args)
{
// Creating the Map
Map<Integer, String> map = new Map<Integer, String>();
// Inserting elements
map.insert(1, "Geeks");
map.printMap();
map.insert(2, "forGeeks");
map.printMap();
map.insert(3, "A");
map.printMap();
map.insert(4, "Computer");
map.printMap();
map.insert(5, "Portal");
map.printMap();
}
}
```

**Output:**

```
HashMap created
Number of pairs in the Map: 0
Size of Map: 5
Default Load Factor : 0.75

Pair(1, Geeks) inserted successfully.

Current Load factor = 0.2
Number of pairs in the Map: 1
Size of Map: 5

Current HashMap:
key = 1, val = Geeks

Pair(2, forGeeks) inserted successfully.

Current Load factor = 0.4
Number of pairs in the Map: 2
Size of Map: 5

Current HashMap:
key = 1, val = Geeks
key = 2, val = forGeeks

Pair(3, A) inserted successfully.

Current Load factor = 0.6
Number of pairs in the Map: 3
Size of Map: 5

Current HashMap:
key = 1, val = Geeks
key = 2, val = forGeeks
key = 3, val = A

Pair(4, Computer) inserted successfully.

Current Load factor = 0.8
0.8 is greater than 0.75
Therefore Rehashing will be done.

***Rehashing Started***

Pair(1, Geeks) inserted successfully.

Current Load factor = 0.1
Number of pairs in the Map: 1
Size of Map: 10

Pair(2, forGeeks) inserted successfully.

Current Load factor = 0.2
Number of pairs in the Map: 2
Size of Map: 10

Pair(3, A) inserted successfully.

Current Load factor = 0.3
Number of pairs in the Map: 3
Size of Map: 10

Pair(4, Computer) inserted successfully.

Current Load factor = 0.4
Number of pairs in the Map: 4
Size of Map: 10

***Rehashing Ended***

New Size of Map: 10

Number of pairs in the Map: 4
Size of Map: 10

Current HashMap:
key = 1, val = Geeks
key = 2, val = forGeeks
key = 3, val = A
key = 4, val = Computer

Pair(5, Portal) inserted successfully.

Current Load factor = 0.5
Number of pairs in the Map: 5
Size of Map: 10

Current HashMap:
key = 1, val = Geeks
key = 2, val = forGeeks
key = 3, val = A
key = 4, val = Computer
key = 5, val = Portal

```



* * *

* * *



