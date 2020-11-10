# 使用给定元素替换索引`P`处的元素后，打印不同数组元素的数量

> 原文：[https://www.geeksforgeeks.org/queries-to-print-count-of-distinct-array-elements-after-replacing-element-at-index-p-by-a-given-element/](https://www.geeksforgeeks.org/queries-to-print-count-of-distinct-array-elements-after-replacing-element-at-index-p-by-a-given-element/)

给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，其中包括`N`个整数和 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)`query[][]`，其中`Q`个查询，格式为`{p, x}`，每个查询的任务是将`p`位置的元素替换为`x`并打印数组中存在的不同元素的[计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)。

**示例**：

> **输入**：`Q = 3, arr[] = {2, 2, 5, 5, 5, 4, 6, 3}, query[][] = {{1, 7}, {6, 8} , {7, 2}}`
>
> **输出**：`{6, 6, 5}`
>
> **说明**：
>
> 每个查询之后的总不同元素（基于 索引）：
>
> 查询 1：`p = 1`且`x = 7`。因此，`arr[1] = 7`且`arr []`变为`{7, 2, 5, 5, 4, 6, 3 }`。 因此，不同的元素为 6。
>
> 查询 2：`p = 6`和`x = 8`。因此，`arr[6] = 8`且`arr []`变为`{7, 2, 5, 5, 4, 4, 8}`。 因此，不同的元素为 6。
>
> 查询 3：`p = 7`和`x = 2`。因此，`arr[7] = 2`且`arr []`变为`{7, 2, 5, 5, 4, 4, 8}`。 因此，不同的元素为 5。
> 
> **输入**：`Q = 2, arr[] = {1, 1, 1, 1}, 查询[] [] = {{2, 2}, {3, 3}}`
>
> **输出**：`{2, 3}`
>
> **解释**：
>
> 每次查询（基于索引的索引）后的总不同元素：
>
> 查询 1 ：`p = 2`且`x = 2`。因此，`arr[2] = 2`且`arr[]`变为`{1,2,1,1}`。 因此，不同的元素为 2。
>
> 查询 2：`p = 3`且`x = 3`。因此，`arr[3] = 3`且`arr[]`变为`{1,2,3,1}`。 因此，不同的元素为 3。

**朴素的方法**：最简单的方法是为每个查询更新给定的数组，然后[将更新后的数组的所有元素插入](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)到 [Set](https://www.geeksforgeeks.org/set-in-java/) 中。 将集合的[大小打印为不同数组元素](https://www.geeksforgeeks.org/setsize-c-stl/)的[个计数。](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

下面是上述方法的实现：

## Java

```java

// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to the total number
    // of distinct elements after each
    // query update
    static void Distinct(int arr[], int n,
                         int p, int x)
    {
        // Update the array
        arr[p - 1] = x;

        // Store distinct elements
        Set<Integer> set = new HashSet<>();

        for (int i = 0; i < n; i++) {
            set.add(arr[i]);
        }

        // Print the size
        System.out.print(set.size() + " ");
    }

    // Function to print the count of
    // distinct elements for each query
    static void updateArray(
        int arr[], int n,
        int queries[][], int q)
    {
        // Traverse the query
        for (int i = 0; i < q; i++) {

            // Function Call to update
            // each query
            Distinct(arr, n, queries[i][0],
                     queries[i][1]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 2, 2, 5, 5, 4, 6, 3 };

        int N = arr.length;

        int Q = 3;

        // Given queries
        int queries[][]
            = new int[][] { { 1, 7 },
                            { 6, 8 },
                            { 7, 2 } };

        // Function Call
        updateArray(arr, N, queries, Q);
    }
}

```

## C#

```cs

// C# program for the 
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to the total number
// of distinct elements after each
// query update
static void Distinct(int []arr, int n,
                     int p, int x)
{
  // Update the array
  arr[p - 1] = x;

  // Store distinct elements
  HashSet<int> set = 
          new HashSet<int>();

  for (int i = 0; i < n; i++) 
  {
    set.Add(arr[i]);
  }

  // Print the size
  Console.Write(set.Count + " ");
}

// Function to print the count of
// distinct elements for each query
static void updateArray(int []arr, int n,
                        int [,]queries, int q)
{
  // Traverse the query
  for (int i = 0; i < q; i++) 
  {
    // Function Call to update
    // each query
    Distinct(arr, n, queries[i, 0], 
             queries[i, 1]);
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int[] arr = {2, 2, 5, 5, 
               4, 6, 3};

  int N = arr.Length;
  int Q = 3;

  // Given queries
  int [,]queries = new int[,] {{1, 7},
                               {6, 8}, 
                               {7, 2}};

  // Function Call
  updateArray(arr, N, queries, Q);
}
}

// This code is contributed by gauravrajput1

```

**输出**： 

```
6 6 5

```

**时间复杂度**：`O(Q * N)`

**辅助空间**：`O(n)`

**高效方法**：为了优化上述方法，其思想是将每个数组元素的[频率存储在](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，然后遍历每个查询并打印大小 每次更新后的映射。 请按照以下步骤解决问题：

*   [将每个元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)`M`中。

*   对于每个查询`{p, x}`，执行以下步骤：

    *   在`Map M`中将`arr[p]`的频率降低`1`的频率。 如果其频率降低到`0`，请从`Map`中删除该元素。

    *   更新`arr[p] = x`，并在**映射**中将`x`的频率增加`1`。 否则，在**映射**中添加元素`x`，将其频率设置为`1`。

*   对于上述步骤中的每个查询，将**映射**的大小打印为不同数组元素的[计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to store the frequency
    // of each element in the Map
    static void store(int arr[], int n,
                      HashMap<Integer,
                              Integer>
                          map)
    {
        for (int i = 0; i < n; i++) {

            // Store the frequency of
            // element arr[i]
            if (!map.containsKey(arr[i]))
                map.put(arr[i], 1);
            else
                map.put(arr[i],
                        map.get(arr[i]) + 1);
        }
    }

    // Function to update an array and
    // map & to find the distinct elements
    static void Distinct(int arr[], int n,
                         int p, int x,
                         HashMap<Integer,
                                 Integer>
                             map)
    {

        // Decrease the element if it
        // was previously present in Map
        map.put(arr[p - 1],
                map.get(arr[p - 1]) - 1);

        if (map.get(arr[p - 1]) == 0)
            map.remove(arr[p - 1]);

        // Add the new element to map
        if (!map.containsKey(x)) {
            map.put(x, 1);
        }
        else {
            map.put(x, map.get(x) + 1);
        }

        // Update the array
        arr[p - 1] = x;

        // Print the count of distinct
        // elements
        System.out.print(map.size() + " ");
    }

    // Function to count the distinct
    // element after updating each query
    static void updateQuery(
        int arr[], int n,
        int queries[][], int q)
    {
        // Store the elements in map
        HashMap<Integer, Integer> map
            = new HashMap<>();

        store(arr, n, map);

        for (int i = 0; i < q; i++) {

            // Function Call
            Distinct(arr, n, queries[i][0],
                     queries[i][1], map);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 2, 2, 5, 5, 4, 6, 3 };

        int N = arr.length;
        int Q = 3;

        // Given Queries
        int queries[][]
            = new int[][] { { 1, 7 },
                            { 6, 8 },
                            { 7, 2 } };

        // Function Call
        updateQuery(arr, N, queries, Q);
    }
}

```

**输出**： 

```
6 6 5

```

**时间复杂度**：`O(N + Q)`

**辅助空间**：`O(n)`



* * *

* * *



