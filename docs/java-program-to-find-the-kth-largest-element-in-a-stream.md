# 寻找流中第 K 大元素的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-find-the-kth-最大的流中元素/](https://www.geeksforgeeks.org/java-program-to-find-the-kth-largest-element-in-a-stream/)

给定一个无限长的整数流，在任意时间点找到第 k 个最大的元素。
**例:**

```
Input:
stream[] = {10, 20, 11, 70, 50, 40, 100, 5, ...}
k = 3

Output:    {_,   _, 10, 11, 20, 40, 50,  50, ...}
```

允许的额外空间为 0(k)。

在下面的文章中，我们讨论了寻找数组中第 k 大元素的不同方法。
[未排序数组中第 K 个最小/最大元素|集合 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)
[未排序数组中第 K 个最小/最大元素|集合 2(预期线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)
[未排序数组中第 K 个最小/最大元素|集合 3(最坏情况线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)
这里我们有一个流而不是整个数组，我们只允许存储 K 个元素。

一个**简单的解决方法**就是保持一个大小为 k 的数组，思路是保持数组的排序，这样在 O(1)时间内就可以找到第 k 个最大的元素(如果数组按递增顺序排序，我们只需要返回数组的第一个元素)
如何处理一个流的新元素？
对于流中的每个新元素，检查新元素是否小于当前第 k 个最大元素。如果是，那就忽略它。如果否，则从数组中移除最小的元素，并按排序顺序插入新元素。处理一个新元素的时间复杂度是 O(k)。

一个**更好的解决方案**是使用大小为 k 的自平衡二叉查找树。第 k 个最大的元素可以在 O(Logk)时间内找到。
如何加工新元素的流？
对于流中的每个新元素，检查新元素是否小于当前第 k 个最大元素。如果是，那就忽略它。如果没有，则从树中移除最小的元素并插入新元素。处理一个新元素的时间复杂度是 O(Logk)。

一个有效的解决方案是使用 k 大小的最小堆来存储 k 个最大的流元素。第 k 个最大的元素总是在根，可以在 O(1)时间找到。
如何加工新元素的流？
比较新元素与堆根。如果新元素较小，则忽略它。否则，用新元素替换根目录，并为修改后的堆的根目录调用 heapify。寻找第 k 大元素的时间复杂度是 O(Logk)。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

  /*
  using min heap DS

  how data are stored in min Heap DS
         1
       2   3
  if k==3 , then top element of heap
  itself the kth largest largest element

  */
  static PriorityQueue<Integer> min;
  static int k;

  static List<Integer> getAllKthNumber(int arr[])
  {

    // list to store kth largest number
    List<Integer> list = new ArrayList<>();

    // one by one adding values to the min heap
    for (int val : arr) {

      // if the heap size is less than k , we add to
      // the heap
      if (min.size() < k)
        min.add(val);

      /*
      otherwise ,
      first we  compare the current value with the
      min heap TOP value

      if TOP val > current element , no need to
      remove TOP , bocause it will be the largest kth
      element anyhow

      else  we need to update the kth largest element
      by removing the top lowest element
      */

      else {
        if (val > min.peek()) {
          min.poll();
          min.add(val);
        }
      }

      // if heap size >=k we add 
      // kth largest element
      // otherwise -1

      if (min.size() >= k)
        list.add(min.peek());
      else
        list.add(-1);
    }
    return list;
  }

  // Driver Code
  public static void main(String[] args)
  {
    min = new PriorityQueue<>();

    k = 4;

    int arr[] = { 1, 2, 3, 4, 5, 6 };

    List<Integer> res = getAllKthNumber(arr);

    for (int x : res)
      System.out.print(x + " ");
  }

    // This code is Contributed by Pradeep Mondal P
}
```

**输出:**

```
K is 3
Enter next element of stream 23
Enter next element of stream 10
Enter next element of stream 15
K'th largest element is 10
Enter next element of stream 70
K'th largest element is 15
Enter next element of stream 5
K'th largest element is 15
Enter next element of stream 80
K'th largest element is 23
Enter next element of stream 100
K'th largest element is 70
Enter next element of stream
CTRL + C pressed
```

详情请参考[流中第 K 大元素](https://www.geeksforgeeks.org/kth-largest-element-in-a-stream/)的完整文章！