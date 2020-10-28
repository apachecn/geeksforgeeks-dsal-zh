# 从第二个数组

> 原文：[https://www.geeksforgeeks.org/find-just-strictly-greater-element-from-first-array-for-each-element-in-second-array/](https://www.geeksforgeeks.org/find-just-strictly-greater-element-from-first-array-for-each-element-in-second-array/)

中的每个元素开始，从第一个数组中严格查找更大的元素

给定两个包含 **N** 个元素的数组 **A []** 和 **B []** ，任务是为数组 **B []中的每个元素查找。** ，该元素严格大于数组 **A []** 中存在的元素。 如果不存在任何值，则打印“ null”。

**注意**：数组 A []中的值只能使用一次。

**示例**：

> **输入**：A [] = {0，1，2，3，4}，B [] = {0，1，1，2，2，3}
> **输出**：1 2 3 4 null
> **说明**：
> 迭代数组 B []中的每个元素：
> 严格大于 0 且存在于数组 A []中的值是 1\.
> 类似地，数组 A []中存在的严格大于 1 的值是 2。
> 类似地，由于数组 A []中存在的严格大于 1 的值是 3，因为 2 已经用于前面的 1。
> 类似地，数组 A []中存在的严格大于 2 的值是 4。
> 现在，数组中没有大于 2 的值。 3，因为先前的 2 已经使用 4。因此，将打印 null。
> 
> **输入**：A [] = {0，1，6，4，4，0，4，2，2，4，7}，B [] = {0，1，6，4，0，2 ，4，2，4，7}
> **输出**：1 2 7 6 2 4 null 4 null null

**方法**：的想法是使用[树集数据结构](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)。 但是由于树集不支持重复值，因此[哈希图](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)用于存储元素的频率。

*   [遍历数组 A []](https://www.geeksforgeeks.org/iterating-arrays-java/) 。

*   将数组 A []中的元素添加到树集中。

*   在哈希图中更新其[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)。

*   现在，对于数组 B []中的每个元素，通过使用树集的 **upper（）**函数，找到严格大于当前值的值。

*   现在，将哈希图中此数字的频率减少 1。

*   继续重复上述两个步骤，直到数字的频率变为 0。如果为 0，则该元素的所有出现次数都用光了。 因此，从树集中删除该元素。

下面是上述方法的实现：

```
// Java program to find the values
// strictly greater than the element
// and present in the array
import java.io.*;
import java.util.*;
public class GFG {
// Function to find the values
// strictly greater than the element
// and present in the array
public static void operations(
int n, long A[], long B[])
{
// Treeset to store the
// values of the array A
TreeSet<Long> tree
= new TreeSet<Long>();
[
// HashMap to store the frequencies
// of the values in array A
HashMap<Long, Integer> freqMap
= new HashMap<Long, Integer>();
// Iterating through the array
// and add values in the treeset
for ( int j = 0 ; j < n; j++) {
long x = A[j];
tree.add(x);
// Updating the frequencies
if (freqMap.containsKey(x)) {
freqMap.put(x, freqMap.get(x) + 1 );
}
else {
freqMap.put(x, 1 );
}
}
// Finding the strictly greater value
// in the array A[] using "higher()"
// function and also reducing the
// frequency of that value because it
// has to be used only once
[
[HTG10 7] for ( int j = 0 ; j < n; j++) {
long x = B[j];
// If the higher value exists
if (tree.higher(x) != null ) {
System.out.print(tree.higher(x) + " " );
[
// If the frequency value is 1
// then remove it from treeset
// because it has been used
// and its frequency becomes 0
if (freqMap.get(tree.higher(x)) == 1 ) {
tree.remove(tree.higher(x));
}
// Else, reducing the frequency
// by 1
else {
freqMap.put(
tree.higher(x),
freqMap.get(tree.higher(x))
[HTG16 2] 1 );
}
}
// If the value is not present
// then print null
else {
System.out.print( "null " );
}
}
}
// Driver code
public static void main(String args[])
{
的
int n = 12 ;
long A[] = new long [] { 9 , 5 , 100 , 4 ,
89 , 2 , 0 , 2 ,
89 , 77 , 77 , 77 };
long B[] = new long [] { 0 , 18 , 60 , 34 ,
50 , 29 , 4 , 20 ,
48 , 77 , 2 , 8 };
operations(n, A, B);
}
}
]
```

**Output:**

```
2 77 77 77 89 89 5 100 null null 4 9

```

**时间复杂度**：*O（N * log（N））*因为插入一个元素在树集中需要 log（N）。



* * *

* * *



