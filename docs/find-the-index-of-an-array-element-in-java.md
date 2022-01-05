# 在 Java 中找到数组元素的索引

> 原文:[https://www . geesforgeks . org/find-Java 中数组元素的索引/](https://www.geeksforgeeks.org/find-the-index-of-an-array-element-in-java/)

给定一个由 N 个元素和 K 个元素组成的数组，在 Java 中找到一个数组元素的索引。
示例:

```
Input: a[] = { 5, 4, 6, 1, 3, 2, 7, 8, 9 }, K = 5
Output: 0

Input: a[] = { 5, 4, 6, 1, 3, 2, 7, 8, 9 }, K = 7
Output: 6
```

可以使用下面提到的方法来搜索 N 个整数数组中的元素。

1.  [**【线性搜索】**](https://www.geeksforgeeks.org/linear-search/) **:在一个数组中做线性搜索，元素可以在 O(N)复杂度中找到。
    下面是线性搜索方法的实现:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of
// an element in N elements
import java.util.*;
public class index {

    // Linear-search function to find the index of an element
    public static int findIndex(int arr[], int t)
    {

        // if array is Null
        if (arr == null) {
            return -1;
        }

        // find length of array
        int len = arr.length;
        int i = 0;

        // traverse in the array
        while (i < len) {

            // if the i-th element is t
            // then return the index
            if (arr[i] == t) {
                return i;
            }
            else {
                i = i + 1;
            }
        }
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] my_array = { 5, 4, 6, 1, 3, 2, 7, 8, 9 };

        // find the index of 5
        System.out.println("Index position of 5 is: "
                           + findIndex(my_array, 5));

        // find the index of 7
        System.out.println("Index position of 7 is: "
                           + findIndex(my_array, 7));
    }
}
```

**Output:** 

```
Index position of 5 is: 0
Index position of 7 is: 6
```

[**2。**二分搜索法](https://www.geeksforgeeks.org/binary-search/)T4:二分搜索法也可以用来查找数组中数组元素的索引。但是二分搜索法只能在阵是 ***排序*** 的情况下使用。Java 为我们提供了一个[内置函数](https://www.geeksforgeeks.org/arrays-binarysearch-java-examples-set-1/)，可以在 Java 的 Arrays 库中找到，如果元素存在，它将返回索引，否则返回-1。复杂度为 0(对数 n)。
以下是二分搜索法的执行情况。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of
// an element in N elements
import java.util.Arrays;

public class index {

    // Function to find the index of an element
    public static int findIndex(int arr[], int t)
    {

        int index = Arrays.binarySearch(arr, t);
        return (index < 0) ? -1 : index;
    }
    // Driver Code
    public static void main(String[] args)
    {
        int[] my_array = { 1, 2, 3, 4, 5, 6, 7 };

        // find the index of 5
        System.out.println("Index position of 5 is: "
                           + findIndex(my_array, 5));

        // find the index of 7
        System.out.println("Index position of 7 is: "
                           + findIndex(my_array, 7));
    }
}
```

**Output:** 

```
Index position of 5 is: 4
Index position of 7 is: 6
```

**3** [**。番石榴:**](https://www.geeksforgeeks.org/guava-library-java/) 番石榴是谷歌开发的一个开源的、基于 Java 的库。它为集合、缓存、原语支持、并发性、公共注释、字符串处理、输入/输出和验证提供了实用方法。番石榴提供了几个与原始相关的实用类，比如 int 表示 int，Longs 表示 long，double 表示 double 等。每个实用程序类都有一个 **indexOf()** 方法，该方法返回数组中元素第一次出现的索引。
下面是番石榴的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of
// an element in N elements
import java.util.List;
import com.google.common.primitives.Ints;
public class index {
    // Function to find the index of an element using
    public static int findIndex(int arr[], int t)
    {
        return Ints.indexOf(arr, t);
    }
    // Driver Code
    public static void main(String[] args)
    {
        int[] my_array = { 5, 4, 6, 1, 3, 2, 7, 8, 9 };
        System.out.println("Index position of 5 is: "
                           + findIndex(my_array, 5));
        System.out.println("Index position of 7 is: "
                           + findIndex(my_array, 7));
    }
}
```

**Output:** 

```
Index position of 5 is: 0
Index position of 7 is: 6
```

**4。**[**Stream API:**](https://www.geeksforgeeks.org/stream-in-java/)Stream 是 Java 8 中引入的新抽象层。使用 stream，您可以以类似于 SQL 语句的声明方式处理数据。该流表示来自支持聚合操作的源的对象序列。为了找到一个元素的索引，Stream 包提供了一个实用程序 IntStream。利用数组的长度，我们可以得到从 0 到 n-1 的数组索引的 IntStream，其中 n 是数组的长度。
下面是流应用编程接口方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of
// an element in N elements
import java.util.stream.IntStream;
public class index {

    // Function to find the index of an element
    public static int findIndex(int arr[], int t)
    {
        int len = arr.length;
        return IntStream.range(0, len)
            .filter(i -> t == arr[i])
            .findFirst() // first occurrence
            .orElse(-1); // No element found
    }
    public static void main(String[] args)
    {
        int[] my_array = { 5, 4, 6, 1, 3, 2, 7, 8, 9 };
        System.out.println("Index position of 5 is: "
                           + findIndex(my_array, 5));
        System.out.println("Index position of 7 is: "
                           + findIndex(my_array, 7));
    }
}
```

**Output:** 

```
Index position of 5 is: 0
Index position of 7 is: 6
```

**5。使用数组列表**

在这种方法中，我们将数组转换成数组列表，然后我们将使用数组列表的 indexOf 方法来获取元素的索引。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

public class GFG {

    public static int findIndex(int arr[], int t)
    {
        // Creating ArrayList
        ArrayList<Integer> clist = new ArrayList<>();

        // adding elements of array
        // to ArrayList
        for (int i : arr)
            clist.add(i);

        // returning index of the element
        return clist.indexOf(t);
    }

    // Driver program
    public static void main(String[] args)
    {
        int[] my_array = { 5, 4, 6, 1, 3, 2, 7, 8, 9 };
        System.out.println("Index position of 5 is: "
                           + findIndex(my_array, 5));
        System.out.println("Index position of 7 is: "
                           + findIndex(my_array, 7));
    }
}
```

**输出:**

```
Index position of 5 is: 0
Index position of 7 is: 6
```

**6。使用递归**

我们将使用递归来找到给定元素的第一个索引。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    public static int index(int arr[], int t, int start)
    {

        // base case when
        // start equals the length of the
        // array we return -1
        if(start==arr.length)
            return -1;

        // if element at index start equals t
        // we return start
        if(arr[start]==t)
            return start;

        // we find for the rest
        // position in the array
        return index(arr,t,start+1);
    }

    public static int findIndex(int arr[], int t)
    {
        return index(arr,t,0);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] my_array = { 5, 4, 6, 1, 3, 2, 7, 8, 9 };
        System.out.println("Index position of 5 is: "
                + findIndex(my_array, 5));
        System.out.println("Index position of 7 is: "
                + findIndex(my_array, 7));
    }
}
```

**输出:**

```
Index position of 5 is: 0
Index position of 7 is: 6
```