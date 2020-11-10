# Java 中的`HashSet`与`TreeSet`

> 原文：[https://www.geeksforgeeks.org/hashset-vs-treeset-in-java/](https://www.geeksforgeeks.org/hashset-vs-treeset-in-java/)

*   **速度和内部实现**：

    [HashSet](http://www.geeksforgeeks.org/hashset-in-java/) : For operations like search, insert and delete. It takes constant time for these operations on average. HashSet is faster than TreeSet. HashSet is Implemented using a [hash table](https://www.geeksforgeeks.org/hashing-set-1-introduction/).

    [`TreeSet`](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)：`TreeSet`以`O(log n)`进行搜索，插入和删除，它高于`HashSet`。 但是`TreeSet`保留排序的数据。 此外，它支持诸如`high()`（返回最小的更高元素），`floor()`，`ceiling()`等操作。这些操作在`TreeSet`中也是`O(log n)`，在`HashSet`中不受支持。 使用自平衡二分搜索树（[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)）实现`TreeSet`。 `TreeSet`由 Java 中的`TreeMap`支持。

*   **排序**

    `HashSet`中的元素未排序。 `TreeSet`按照 Java 中的`Comparable`或`Comparator`方法定义的排序顺序维护对象。 默认情况下，`TreeSet`元素以升序排序。 它提供了多种方法来处理有序集，例如`first()`，`last()`，`headSet()`，`tailSet()`等。

*   **空对象**

    `HashSet`允许空对象。 `TreeSet`不允许使用`null`对象并引发`NullPointerException`，为什么，因为`TreeSet`使用`compareTo()`方法比较键，而`compareTo()`会引发`java.lang.NullPointerException`。

*   **比较**

    `HashSet`使用[`equals()`](https://www.geeksforgeeks.org/overriding-equals-method-in-java/)方法比较集合中的两个对象并检测重复项。 `TreeSet`使用`compareTo()`方法实现相同目的。

    如果`equals()`和`compareTo()`不一致，即，对于两个相等的对象，`equals`应该返回`true`，而`compareTo()`应该返回零，这将打破`Set`接口的协定，并允许在集合实现中重复，如`TreeSet`。

如果要排序的集合，最好将元素添加到`HashSet`，然后将其转换为`TreeSet`，而不是创建`TreeSet`并向其中添加元素。

`HashSet`示例：

```
// Java program to demonstrate working of
// HashSet
import java.util.HashSet;
class HashSetDemo {
public static void main(String[] args)
{
// Create a HashSet
HashSet<String> hset = new HashSet<String>();
// add elements to HashSet
hset.add( "geeks" );
hset.add( "for" );
hset.add( "practice" );
hset.add( "contribute" );
HTG100]
// Displaying HashSet elements
System.out.println( "HashSet contains: " );
for (String temp : hset) {
System.out.println(temp);
}
}
}
```

**输出**：

```
HashSet contains: 
practice
geeks
for
contribute

```

**树集示例**

```
// Java program to demonstrate working of
// TreeSet.
import java.util.TreeSet;
class TreeSetDemo {
[
public static void main(String[] args)
{
// Create a TreeSet
TreeSet<String> tset = new TreeSet<String>();
// add elements to HashSet
tset.add( "geeks" );
tset.add( "for" );
tset.add( "practice" );
tset.add( "contribute" );
HTG100]
// Displaying TreeSet elements
System.out.println( "TreeSet contains: " );
for (String temp : tset) {
System.out.println(temp);
}
}
}
```

**输出**：

```
TreeSet contains: 
contribute
for
geeks
practice

```

什么时候比`HashSet`更倾向`TreeSet`？

1.  需要排序的唯一元素而不是唯一元素。 `TreeSet`给定的排序列表始终按升序排列。

2.  `TreeSet`比`HashSet`具有更大的局部性。如果两个条目按顺序靠近，则`TreeSet`将它们在数据结构中并因此在内存中彼此靠近放置，而`HashSet`则将条目分布在整个内存中，而不管它们与之关联的键如何。

3.  `TreeSet`在下面使用红黑树算法对元素进行分类。 当需要频繁执行读/写操作时，`TreeSet`是一个不错的选择。

4.  [`LinkedHashSet`](https://www.geeksforgeeks.org/linkedhashset-class-in-java-with-examples/)是这两者之间的另一个数据结构。 它提供类似于`HashSet`的时间复杂性，并保持插入顺序（请注意，这不是排序顺序，而是元素插入的顺序）。



* * *

* * *



