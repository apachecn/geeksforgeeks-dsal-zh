# 对具有单个设置位的给定范围内的数组元素进行计数的查询

> 原文:[https://www . geeksforgeeks . org/query-to-count-array-elements-from-给定范围-具有单个设置位/](https://www.geeksforgeeks.org/queries-to-count-array-elements-from-a-given-range-having-a-single-set-bit/)

给定一个由正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个由查询组成的数组**Q【】【】**，每个 i <sup>次</sup>查询的任务是从只有一个设置位的范围**【Q[I][0]、Q[I][1]】**中计数数组元素。

**示例:**

> **输入:** arr[] = {12，11，16，8，2，5，1，3，256，1}，查询[][] = {{0，9}，{4，9}}
> **输出:** 6 4
> **解释:**
> 在索引[0，9]的范围内，元素 arr[2] (= 16)、arr[3](= 8)、arr[4]( = 2)、arr[6](= 1)、arr
> 在[4，9]范围内，元素 arr[4] (= 2)、arr[6](= 1)、arr[8](= 256)、arr[9] (= 1)只有 1 个设置位。
> 
> **输入:** arr[] = {2，1，101，11，4}，查询[][] = {{2，4}，{1，4}}
> **输出:** 1 2

**天真方法:**每个查询最简单的方法是迭代范围**【l，r】**，并使用[布莱恩·克尼根的算法](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)计算只有一个集合位的数组元素的数量。

***时间复杂度** : O(Q * N*logN)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

*   初始化一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来存储只有一个设置位的元素数量。
*   第 I**个**索引存储到第 i <sup>个</sup>索引为止只有一个设置位的数组元素的计数。
*   对于每个查询 **(i，j)** ，返回**pre[j]–pre[I–1]**，即([包含-排除原则](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/))。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// only one bit is set or not
int check(int x)
{
    if (((x) & (x - 1)) == 0)
        return 1;
    return 0;
}

// Function to perform Range-query
int query(int l, int r, int pre[])
{
    if (l == 0)
        return pre[r];
    else
        return pre[r] - pre[l - 1];
}

// Function to count array elements with a
// single set bit for each range in a query
void countInRange(int arr[], int N,
                  vector<pair<int, int> > queries, int Q)
{
    // Initialize array for Prefix sum
    int pre[N] = { 0 };
    pre[0] = check(arr[0]);

    for (int i = 1; i < N; i++) {
        pre[i] = pre[i - 1] + check(arr[i]);
    }

    int c = 0;
    while (Q--) {
        int l = queries.first;
        int r = queries.second;
        c++;
        cout << query(l, r, pre) << ' ';
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 12, 11, 16, 8, 2, 5, 1, 3, 256, 1 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given queries
    vector<pair<int, int> > queries
        = { { 0, 9 }, { 4, 9 } };

    // Size of queries array
    int Q = queries.size();

    countInRange(arr, N, queries, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;
import java.io.*;
import java.math.*;
public class GFG
{

  // Function to check whether
  // only one bit is set or not
  static int check(int x)
  {
    if (((x) & (x - 1)) == 0)
      return 1;

    return 0;
  }

  // Function to perform Range-query
  static int query(int l, int r, int[] pre)
  {
    if (l == 0)
      return pre[r];
    else
      return pre[r] - pre[l - 1];
  }

  // Function to count array elements with a
  // single set bit for each range in a query
  static void countInRange(int[] arr, int N,  ArrayList<Pair> queries,
                           int Q)
  {

    // Initialize array for Prefix sum
    int[] pre = new int[N];
    pre[0] = check(arr[0]);
    for(int i = 1; i < N; i++)
    {
      pre[i] = pre[i - 1] + check(arr[i]);
    }  
    int c = 0;
    int q = 0;   
    while (q < Q)
    {
      int l = queries.get(q).item1;
      int r = queries.get(q).item2;
      c++;
      q++;
      System.out.print(query(l, r, pre) + " ");
    }
  }

  // A Pair class for handling queries in JAVA
  // As, there is no in-built function of Tuple
  static class Pair
  {
    int item1, item2;
    Pair(int item1, int item2)
    {
      this.item1 = item1;
      this.item2 = item2;
    }
  }

  // Driver code
  public static void main(String args[])
  {

    // Given array
    int[] arr = { 12, 11, 16, 8, 2,
                 5, 1, 3, 256, 1 };

    // Size of the array
    int N = arr.length;

    // Given queries
    ArrayList<Pair> queries = new ArrayList<Pair>();
    queries.add(new Pair(4,9));
    queries.add(new Pair(0,9));

    // Size of queries array
    int Q = queries.size();    
    countInRange(arr, N, queries, Q);
  }
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check whether
# only one bit is set or not
def check(x):
    if (((x) & (x - 1)) == 0):
        return 1
    return 0

# Function to perform Range-query
def query(l, r, pre):
    if (l == 0):
        return pre[r]
    else:
        return pre[r] - pre[l - 1]

# Function to count array elements with a
# single set bit for each range in a query
def countInRange(arr,  N, queries, Q):

    # Initialize array for Prefix sum
    pre = [0] * N
    pre[0] = check(arr[0])
    for i in range(1, N):
        pre[i] = pre[i - 1] + check(arr[i])
    c = 0
    while (Q > 0):
        l = queries[0]
        r = queries[1]
        c += 1
        print(query(l, r, pre), end=" ")
        Q -= 1

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [12, 11, 16, 8, 2, 5, 1, 3, 256, 1]

    # Size of the array
    N = len(arr)

    # Given queries
    queries = [[0, 9], [4, 9]]

    # Size of queries array
    Q = len(queries)

    countInRange(arr, N, queries, Q)

    # this code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check whether
// only one bit is set or not
static int check(int x)
{
    if (((x) & (x - 1)) == 0)
        return 1;

    return 0;
}

// Function to perform Range-query
static int query(int l, int r, int[] pre)
{
    if (l == 0)
        return pre[r];
    else
        return pre[r] - pre[l - 1];
}

// Function to count array elements with a
// single set bit for each range in a query
static void countInRange(int[] arr, int N,
                         List<Tuple<int, int>> queries,
                         int Q)
{

    // Initialize array for Prefix sum
    int[] pre = new int[N];
    pre[0] = check(arr[0]);

    for(int i = 1; i < N; i++)
    {
        pre[i] = pre[i - 1] + check(arr[i]);
    }

    int c = 0;
    int q = 0;

    while (q < Q)
    {
        int l = queries[q].Item1;
        int r = queries[q].Item2;
        c++;
        q++;
        Console.Write(query(l, r, pre) + " ");
    }
}

// Driver code
static void Main()
{

    // Given array
    int[] arr = { 12, 11, 16, 8, 2,
                  5, 1, 3, 256, 1 };

    // Size of the array
    int N = arr.Length;

    // Given queries
    List<Tuple<int,
               int>> queries = new List<Tuple<int,
                                              int>>();
    queries.Add(new Tuple<int, int>(0, 9));
    queries.Add(new Tuple<int, int>(4, 9));

    // Size of queries array
    int Q = queries.Count;

    countInRange(arr, N, queries, Q);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check whether
// only one bit is set or not
function check(x)
{
    if (((x) & (x - 1)) == 0)
        return 1;
    return 0;
}

// Function to perform Range-query
function query(l, r, pre)
{
    if (l == 0)
        return pre[r];
    else
        return pre[r] - pre[l - 1];
}

// Function to count array elements with a
// single set bit for each range in a query
function countInRange(arr, N, queries, Q)
{
    // Initialize array for Prefix sum
    var pre = Array(N).fill(0);
    pre[0] = check(arr[0]);

    for (var i = 1; i < N; i++) {
        pre[i] = pre[i - 1] + check(arr[i]);
    }

    var c = 0;
    while (Q--) {
        var l = queries[0];
        var r = queries[1];
        c++;
        document.write( query(l, r, pre) + ' ');
    }
}

// Driver Code

// Given array
var arr = [12, 11, 16, 8, 2, 5, 1, 3, 256, 1];

// Size of the array
var N = arr.length;

// Given queries
var queries
    = [[0, 9], [4, 9 ]];

// Size of queries array
var Q = queries.length;

countInRange(arr, N, queries, Q);

</script>
```

**Output:** 

```
6 4
```

***时间复杂度:**O(N * log(max(arr[I])】*
***辅助空间:** O(N)*