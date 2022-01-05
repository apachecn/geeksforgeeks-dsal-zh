# 查询从给定数组中找到最长前缀的长度，该数组的所有元素都可以被 K 整除

> 原文:[https://www . geeksforgeeks . org/query-to-find-长度最长的前缀-从给定数组-具有所有元素-可被 k 整除/](https://www.geeksforgeeks.org/queries-to-find-the-length-of-the-longest-prefix-from-given-array-having-all-elements-divisible-by-k/)

给定一个由 **N** 元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个数组**Q【】**，每个查询的任务是找到最长前缀的长度，使得该前缀的所有元素都可以被 **K** 整除。

**示例:**

> **输入:** arr[] = {12，6，15，3，10}，Q[] = {4，3，2 }
> T3】输出:1 4 2
> T6】解释:
> 
> *   **Q[0]= 4:****arr[0]**(= 12)可被 **4** 整除。 **arr[1]** 不能被 **4** 整除。因此，可被 4 整除的最长前缀的长度是 1。
> *   **Q[1] = 3:** 能被 3 整除的最长前缀是{12，6，15，3}。因此，打印 4 作为所需的输出。
> *   Q[2] = 2:可被 2 整除的最长前缀是{12，6}。
> 
> **输入:** arr[] = {4，3，2，1}，Q[] = {1，2，3}
> **输出:** 4 1 0

**方法:**想法是观察如果数组的第一个 **i** 元素可以被给定的整数 **K** 整除，那么它们的 GCD 也会被 **K** 整除。按照以下步骤解决问题:

1.  在找到每个查询的答案之前，预先计算另一个数组 **g[]** 中该数组前缀的 [gcd](https://www.geeksforgeeks.org/gcd-two-array-numbers/) ，使得 **g[0] = arr[0]** 而对于其余元素 **g[i] = GCD(arr[i]，g[I–1])**。
2.  然后，对于数组 **Q[]** 中的每个元素，在数组 **g[]** 上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，找到可被 **Q[i]** 整除的 **g[]** 的最后一个索引。
3.  需要注意的是，该索引中的所有元素都将被 **K** 整除，因为直到该索引的所有元素的 [gcd](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 都将被 **K** 整除。
4.  打印最长前缀的长度。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find index of the last
// element which is divisible the given element
int binSearch(int* g, int st, int en, int val)
{
    // Initially assume the
    // index to be -1
    int ind = -1;
    while (st <= en) {

        // Find the mid element
        // of the subarray
        int mid = st + (en - st) / 2;

        // If the mid element is divisible by
        // given element, then move to right
        // of mid and update ind to mid
        if (g[mid] % val == 0) {
            ind = mid;
            st = mid + 1;
        }

        // Otherwise, move to left of mid
        else {
            en = mid - 1;
        }
    }

    // Return the length of prefix
    return ind + 1;
}

// Function to compute and print for each query
void solveQueries(int* arr, int* queries,
                  int n, int q)
{
    int g[n];

    // Pre compute the gcd of the prefixes
    // of the input array in the array g[]
    for (int i = 0; i < n; i++) {
        if (i == 0) {
            g[i] = arr[i];
        }
        else {
            g[i] = __gcd(g[i - 1], arr[i]);
        }
    }

    // Perform binary search
    // for each query
    for (int i = 0; i < q; i++) {
        cout << binSearch(g, 0, n - 1,
                          queries[i])
             << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 12, 6, 15, 3, 10 };

    // Size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Given Queries
    int queries[] = { 4, 3, 2 };

    // Size of queries
    int q = sizeof(queries) / sizeof(queries[0]);

    solveQueries(arr, queries, n, q);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find index of the last
// element which is divisible the given element
static int binSearch(int[] g, int st, int en, int val)
{

    // Initially assume the
    // index to be -1
    int ind = -1;
    while (st <= en)
    {

        // Find the mid element
        // of the subarray
        int mid = st + (en - st) / 2;

        // If the mid element is divisible by
        // given element, then move to right
        // of mid and update ind to mid
        if (g[mid] % val == 0)
        {
            ind = mid;
            st = mid + 1;
        }

        // Otherwise, move to left of mid
        else
        {
            en = mid - 1;
        }
    }

    // Return the length of prefix
    return ind + 1;
}

// Function to compute and print for each query
static void solveQueries(int []arr, int []queries,
                  int n, int q)
{
    int []g = new int[n];

    // Pre compute the gcd of the prefixes
    // of the input array in the array g[]
    for (int i = 0; i < n; i++)
    {
        if (i == 0) {
            g[i] = arr[i];
        }
        else {
            g[i] = __gcd(g[i - 1], arr[i]);
        }
    }

    // Perform binary search
    // for each query
    for (int i = 0; i < q; i++)
    {
        System.out.print(binSearch(g, 0, n - 1,
                          queries[i])
            + " ");
    }
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 12, 6, 15, 3, 10 };

    // Size of array
    int n = arr.length;

    // Given Queries
    int queries[] = { 4, 3, 2 };

    // Size of queries
    int q = queries.length;
    solveQueries(arr, queries, n, q);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import gcd as __gcd

# Function to find index of the last
# element which is divisible the
# given element
def binSearch(g, st, en, val):

    # Initially assume the
    # index to be -1
    ind = -1

    while (st <= en):

        # Find the mid element
        # of the subarray
        mid = st + (en - st) // 2

        # If the mid element is divisible by
        # given element, then move to right
        # of mid and update ind to mid
        if (g[mid] % val == 0):
            ind = mid
            st = mid + 1

        # Otherwise, move to left of mid
        else:
            en = mid - 1

    # Return the length of prefix
    return ind + 1

# Function to compute and print for each query
def solveQueries(arr, queries, n, q):

    g = [0 for i in range(n)]

    # Pre compute the gcd of the prefixes
    # of the input array in the array g[]
    for i in range(n):
        if (i == 0):
            g[i] = arr[i]
        else:
            g[i] = __gcd(g[i - 1], arr[i])

    # Perform binary search
    # for each query
    for i in range(q):
        print(binSearch(g, 0, n - 1,
                        queries[i]), end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 12, 6, 15, 3, 10 ]

    # Size of array
    n = len(arr)

    # Given Queries
    queries = [ 4, 3, 2 ]

    # Size of queries
    q = len(queries)

    solveQueries(arr, queries, n, q)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

// Function to find index of the last
// element which is divisible the given element
static int binSearch(int[] g, int st, int en, int val)
{

  // Initially assume the
  // index to be -1
  int ind = -1;
  while (st <= en)
  {

    // Find the mid element
    // of the subarray
    int mid = st + (en - st) / 2;

    // If the mid element is divisible by
    // given element, then move to right
    // of mid and update ind to mid
    if (g[mid] % val == 0)
    {
      ind = mid;
      st = mid + 1;
    }

    // Otherwise, move to left of mid
    else
    {
      en = mid - 1;
    }
  }

  // Return the length of prefix
  return ind + 1;
}

  // Recursive function to return
  // gcd of a and b
  static int gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a - b, b);

    return gcd(a, b - a);
  }

  // Function to compute and print for each query
  static void solveQueries(int[] arr, int[] queries,
                           int n, int q)
  {
    int[] g = new int[n];

    // Pre compute the gcd of the prefixes
    // of the input array in the array g[]
    for (int i = 0; i < n; i++)
    {
      if (i == 0)
      {
        g[i] = arr[i];
      }
      else
      {
        g[i] = gcd(g[i - 1], arr[i]);
      }
    }

    // Perform binary search
    // for each query
    for (int i = 0; i < q; i++)
    {
      Console.Write(binSearch(g, 0, n - 1,
                              queries[i]) + " ");
    }
  }

// Driver code
public static void Main()
{

    // Given array
    int[] arr = { 12, 6, 15, 3, 10 };

    // Size of array
    int n = arr.Length;

    // Given Queries
    int[] queries = { 4, 3, 2 };

    // Size of queries
    int q = queries.Length;
    solveQueries(arr, queries, n, q);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
//Javascript program for the above approach

//function for GCD
function __gcd( a, b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Function to find index of the last
// element which is divisible the given element
function binSearch(g, st, en, val)
{
    // Initially assume the
    // index to be -1
    var ind = -1;
    while (st <= en) {

        // Find the mid element
        // of the subarray
        var mid = st + parseInt((en - st) / 2);

        // If the mid element is divisible by
        // given element, then move to right
        // of mid and update ind to mid
        if (g[mid] % val == 0) {
            ind = mid;
            st = mid + 1;
        }

        // Otherwise, move to left of mid
        else {
            en = mid - 1;
        }
    }

    // Return the length of prefix
    return ind + 1;
}

// Function to compute and print for each query
function solveQueries(arr, queries, n, q)
{
    var g = new Array(n);

    // Pre compute the gcd of the prefixes
    // of the input array in the array g[]
    for (var i = 0; i < n; i++) {
        if (i == 0) {
            g[i] = arr[i];
        }
        else {
            g[i] = __gcd(g[i - 1], arr[i]);
        }
    }

    // Perform binary search
    // for each query
    for (var i = 0; i < q; i++) {
        document.write( binSearch(g, 0, n - 1, queries[i]) + " ");
    }
}

var arr = [ 12, 6, 15, 3, 10 ];

// Size of array
var n = arr.length;
// Given Queries
var queries = [ 4, 3, 2 ];
// Size of queries
var q = queries.length;
solveQueries(arr, queries, n, q);

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
1 4 2
```

***时间复杂度:**O(NlogN+QlogN)*
T5**辅助空间:** O(N)