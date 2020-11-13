# 用 Java 中的单链接实现自己的哈希表

> 原文：[https://www.geeksforgeeks.org/implementing-our-own-hash-table-with-separate-chaining-in-java/](https://www.geeksforgeeks.org/implementing-our-own-hash-table-with-separate-chaining-in-java/)

每个数据结构都有其自己的特殊特性，例如，当需要快速搜索元素（在`log(n)`中）时，将使用 BST。 当需要在恒定时间内获取最小或最大元素时，将使用堆或优先级队列。 类似地，哈希表用于在固定时间内获取，添加和删除元素。 任何人都必须先了解哈希表的工作，然后再进行实现。 因此，这是哈希表工作的简要背景，还应注意，尽管 Java 中的`HashTable`是线程安全的，而`HashMap`不是线程安全的，但我们将互换使用哈希映射和哈希表术语。

我们将要实现的代码位于[链接 1](https://github.com/ishaan007/Data-Structures/blob/master/HashMaps/Map.java) 和[链接 2](https://github.com/ishaan007/Data-Structures/blob/master/HashMaps/HashNode.java)。

但强烈建议您必须完全阅读此博客，并尝试破译实现哈希映射所涉及的内容，然后再尝试自己编写代码。

**背景**

每个哈希表都以（键，值）组合的形式存储数据。 有趣的是，每个键在哈希表中都是唯一的，但是值可以重复，这意味着其中的不同键的值可以相同。 现在，当我们在数组中观察到要获取值时，我们提供了与该数组中的值相对应的位置/索引。 在哈希表中，我们使用键来获取与该键对应的值，而不是索引。 现在整个过程描述如下：

每次生成键。 键被传递给哈希函数。 每个哈希函数都有**哈希码和压缩器**两部分。

*哈希码是一个整数*（随机或非随机）。 在 Java 中，每个对象都有其自己的哈希码。 我们将在哈希函数中使用由 JVM 生成的哈希码，并根据哈希表的大小对哈希码进行模（`%`）压缩，以压缩哈希码。 *因此，在我们的实现中，模运算符就是压缩器。*

整个过程确保对于任何键，我们在哈希表的大小内获得一个整数位置以插入相应的值。

因此，该过程很简单，用户将一组（键，值）对设置为输入，并根据哈希函数生成的值生成索引，以存储对应于特定键的值。 因此，每当我们需要获取与仅`O(1)`的键相对应的值时。

当引入哈希冲突的概念时，这张照片就变得如此玫瑰色和完美。 想象一下，对于不同的键值，现在在哈希表的同一块中分配了与其他某个先前键对应的先前存储的值。 我们当然不能替代它。那将是灾难性的！ 为解决此问题，我们将使用单独的链接技术，请注意，还有其他开放式寻址技术，例如双哈希和线性探测，其效率与单链接的效率几乎相同，您可以在[链接 1](http://geeksquiz.com/hashing-set-1-introduction/)、[链接 2](http://geeksquiz.com/hashing-set-2-separate-chaining/)、[链接 3](http://geeksquiz.com/hashing-set-3-open-addressing/)。

现在，我们要做的是创建一个与哈希表的特定存储桶相对应的链表，以容纳与映射到同一存储桶的不同键相对应的所有值。

![](img/aee40d882c5503b38106e4a1df1f23ac.png)

现在可能存在一种情况，所有键都映射到同一个存储桶，并且我们从一个存储桶中获得了一个`n`（哈希表的大小）大小的链表，所有其他存储桶为空，这是最糟糕的情况，哈希表充当链表并且搜索为`O(n)`。那么我们该怎么办？

**负载系数**

如果`n`是我们决定先装满的铲斗总数，那么说 10 个，而现在假设装满了 7 个，那么负载系数是`7/10 = 0.7`。

**在我们的实现中**，每当我们向哈希表添加键值对时，我们都会检查负载因子（如果负载因子大于 0.7），则将哈希表的大小加倍。

**实现**

**哈希节点的数据类型**

我们将尝试制作通用映射，而不会对键的数据类型和值施加任何限制。 同样，每个哈希节点都需要知道链表中指向的下一个节点，因此还需要下一个指针。

我们计划保留在哈希映射中的功能是：

*   `get(K key)`：如果`HT`中存在键，则返回与键相对应的值（`HT`有效）。

*   `getSize()`：返回`HT`的大小。

*   `add()`：将新的有效键，值对添加到`HT`，如果已经存在则更新值。

*   `remove()`：删除键值对。

*   `isEmpty()`：如果大小为零，则返回`true`。

```
ArrayList<HashNode<K, V>> bucket = new ArrayList<>();
```

**辅助功能**实现为获取键的索引，以避免其他功能（如获取，添加和删除）中的冗余。 此函数使用内置的 Java 函数生成哈希码，然后按`HT`的大小压缩哈希码，以使索引在`HT`的大小范围内。

`get()`

`get`函数仅将键作为输入，如果表中存在该键，则返回相应的值，否则返回`null`。 步骤如下：

*   检索输入键以在`HT`中找到索引。

*   遍历与`HT`对应的喜欢的列表，如果找到该值，则返回它；否则，如果完全遍历该列表而不返回它，则意味着该值不存在于表中并且无法获取，因此返回`null`。

`remove()`

*   使用辅助函数获取与输入键对应的索引。

*   遍历链表的过程类似于在`get()`中，但是这里的特殊之处在于，在删除键的同时还需要找到它，并且出现两种情况。

*   如果要删除的键位于链表的开头。

*   如果要删除的键不在头部，而是在其他地方。

`add()`

现在是整个实现中最有趣和最具挑战性的功能。有趣的是，当负载系数高于我们指定的值时，我们需要动态增加列表的大小。

*   就像删除遍历和添加的步骤一样，两种情况（在头点或非头点添加）保持不变。

*   如果负载系数大于 0.7，则接近终点。

*   我们将数组列表的大小加倍，然后对现有键进行递归调用`add`函数，因为在我们的情况下，生成的哈希值使用数组的大小来压缩我们使用的内置 JVM 哈希码，因此我们需要为现有索引获取键的新索引。 了解这一点非常重要，请重新阅读本段，直到您了解`add`函数中正在发生的事情。

如果对应于特定存储桶的链表往往变得太长，Java 会在其自己的哈希表实现中使用二分搜索树。

```java
// Java program to demonstrate implementation of our 
// own hash table with chaining for collision detection 
import java.util.ArrayList; 
  
// A node of chains 
class HashNode<K, V> 
{ 
    K key; 
    V value; 
  
    // Reference to next node 
    HashNode<K, V> next; 
  
    // Constructor 
    public HashNode(K key, V value) 
    { 
        this.key = key; 
        this.value = value; 
    } 
} 
  
// Class to represent entire hash table 
class Map<K, V> 
{ 
    // bucketArray is used to store array of chains 
    private ArrayList<HashNode<K, V>> bucketArray; 
  
    // Current capacity of array list 
    private int numBuckets; 
  
    // Current size of array list 
    private int size; 
  
    // Constructor (Initializes capacity, size and 
    // empty chains. 
    public Map() 
    { 
        bucketArray = new ArrayList<>(); 
        numBuckets = 10; 
        size = 0; 
  
        // Create empty chains 
        for (int i = 0; i < numBuckets; i++) 
            bucketArray.add(null); 
    } 
  
    public int size() { return size; } 
    public boolean isEmpty() { return size() == 0; } 
  
    // This implements hash function to find index 
    // for a key 
    private int getBucketIndex(K key) 
    { 
        int hashCode = key.hashCode(); 
        int index = hashCode % numBuckets; 
        return index; 
    } 
  
    // Method to remove a given key 
    public V remove(K key) 
    { 
        // Apply hash function to find index for given key 
        int bucketIndex = getBucketIndex(key); 
  
        // Get head of chain 
        HashNode<K, V> head = bucketArray.get(bucketIndex); 
  
        // Search for key in its chain 
        HashNode<K, V> prev = null; 
        while (head != null) 
        { 
            // If Key found 
            if (head.key.equals(key)) 
                break; 
  
            // Else keep moving in chain 
            prev = head; 
            head = head.next; 
        } 
  
        // If key was not there 
        if (head == null) 
            return null; 
  
        // Reduce size 
        size--; 
  
        // Remove key 
        if (prev != null) 
            prev.next = head.next; 
        else
            bucketArray.set(bucketIndex, head.next); 
  
        return head.value; 
    } 
  
    // Returns value for a key 
    public V get(K key) 
    { 
        // Find head of chain for given key 
        int bucketIndex = getBucketIndex(key); 
        HashNode<K, V> head = bucketArray.get(bucketIndex); 
  
        // Search key in chain 
        while (head != null) 
        { 
            if (head.key.equals(key)) 
                return head.value; 
            head = head.next; 
        } 
  
        // If key not found 
        return null; 
    } 
  
    // Adds a key value pair to hash 
    public void add(K key, V value) 
    { 
        // Find head of chain for given key 
        int bucketIndex = getBucketIndex(key); 
        HashNode<K, V> head = bucketArray.get(bucketIndex); 
  
        // Check if key is already present 
        while (head != null) 
        { 
            if (head.key.equals(key)) 
            { 
                head.value = value; 
                return; 
            } 
            head = head.next; 
        } 
  
        // Insert key in chain 
        size++; 
        head = bucketArray.get(bucketIndex); 
        HashNode<K, V> newNode = new HashNode<K, V>(key, value); 
        newNode.next = head; 
        bucketArray.set(bucketIndex, newNode); 
  
        // If load factor goes beyond threshold, then 
        // double hash table size 
        if ((1.0*size)/numBuckets >= 0.7) 
        { 
            ArrayList<HashNode<K, V>> temp = bucketArray; 
            bucketArray = new ArrayList<>(); 
            numBuckets = 2 * numBuckets; 
            size = 0; 
            for (int i = 0; i < numBuckets; i++) 
                bucketArray.add(null); 
  
            for (HashNode<K, V> headNode : temp) 
            { 
                while (headNode != null) 
                { 
                    add(headNode.key, headNode.value); 
                    headNode = headNode.next; 
                } 
            } 
        } 
    } 
  
    // Driver method to test Map class 
    public static void main(String[] args) 
    { 
        Map<String, Integer>map = new Map<>(); 
        map.add("this",1 ); 
        map.add("coder",2 ); 
        map.add("this",4 ); 
        map.add("hi",5 ); 
        System.out.println(map.size()); 
        System.out.println(map.remove("this")); 
        System.out.println(map.remove("this")); 
        System.out.println(map.size()); 
        System.out.println(map.isEmpty()); 
    } 
} 
```

输出：

```
3
4
null
2
false
```

完整代码位于 [https://github.com/ishaan007/Data-Structures/blob/master/HashMaps/Map.java](https://github.com/ishaan007/Data-Structures/blob/master/HashMaps/Map.java)

本文由 **Ishaan Arora** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以撰写文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

