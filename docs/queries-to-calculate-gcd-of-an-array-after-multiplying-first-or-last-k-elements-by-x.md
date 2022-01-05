# 第一个或最后一个 K 元素乘以 X 后计算数组 GCD 的查询

> 原文:[https://www . geeksforgeeks . org/query-to-compute-gcd-of-of-array-乘-first-or-last-k-elements-by-x/](https://www.geeksforgeeks.org/queries-to-calculate-gcd-of-an-array-after-multiplying-first-or-last-k-elements-by-x/)

给定由 **N** 正整数和 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)T8】组成的[数组**arr【】】**查询 **{a，K，X}** 类型的【】【】[] ，如果 **a** 的值为 **1** ，则先将 **K** 数组元素乘以 **X** 。否则，将最后一个 **K** 数组元素乘以 **X** 。任务是在对原始数组进行每次查询后，计算数组的](https://www.geeksforgeeks.org/array-data-structure/) [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

**示例:**

> **输入:** arr[] = {2，3，4，8}，查询[][3] = {{1，2，2}，{2，4，5}}
> **输出:** 2 5
> **解释:**
> **查询 1:** 给定的查询是{1，2，2}。将前 2 个数组元素乘以 2 后，arr[]修改为{4，6，4，8}。修改后数组的 GCD 为 2。
> **查询 2:** 给定的查询是{2，4，5}。将最后 4 个元素数组元素乘以 5 后，arr[]修改为{10，15，20，40}。更新后数组的 GCD 为 5。
> 
> **输入:** arr[] = {4，12，4，9}，查询[][3] = {{1，3，3}，{2，4，1}}
> **输出:** 3 1

**天真方法:**最简单的方法是通过执行每个查询来更新给定的数组，然后找到更新后的数组的 [GCD。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

***时间复杂度:** O(N * Q * log(M))，其中 **M** 是数组中存在的最大元素。*
***辅助空间:** O(N)*

**高效方法:**通过存储给定数组的前缀和后缀 GCD 数组，并按照以下步骤在 **O(1)** 时间内求解每个查询，可以优化上述方法:

*   初始化一个大小为 **N** 的数组**前缀[]** 和**后缀[]** ，以存储给定数组的前缀和后缀 GCD 数组。
*   [从前到后遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，找到每个索引处的前缀和后缀 GCD，分别存储在**前缀[]** 和**后缀[]** 中。
*   现在，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **查询[]** ，对于每个查询 **{a，K，X}** 执行以下操作:
    *   如果 **K** 的值为 **N** ，则打印**前缀【N–1】* X**的值作为结果。
    *   如果 **a** 的值为 **1，**则查找**前缀【K–1】* X**和**后缀【K】**的 **GCD** ，结果为**前缀【K–1】* X**是第一个 **K** 号的新 GCD，**后缀【K+1】**是剩余数组元素的 GCD。
    *   如果 **a** 的值为 **2、**，则查找**前缀【N–K–1】**和**后缀【N–K】* X**的 GCD，结果**前缀【N–K–1】* X**是第一个 **K** 号的新 GCD，**后缀【N–K】**是剩余数组元素的 GCD。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the GCD after performing
// each query on array elements
void findGCDQueries(int arr[], int N,
                    int Queries[][3],
                    int Q)
{
    // Stores prefix array and suffix
    // array
    int prefix[N], suffix[N];

    prefix[0] = arr[0];
    suffix[N - 1] = arr[N - 1];

    // Build prefix array
    for (int i = 1; i < N; i++) {
        prefix[i] = __gcd(prefix[i - 1],
                          arr[i]);
    }

    // Build suffix array
    for (int i = N - 2; i >= 0; i--) {
        suffix[i] = __gcd(suffix[i + 1],
                          arr[i]);
    }

    // Traverse queries array
    for (int i = 0; i < Q; i++) {

        int a = Queries[i][0];
        int K = Queries[i][1];
        int X = Queries[i][2];

        // Edge Case when update is
        // is required till the end
        if (K == N) {
            cout << prefix[N - 1] * X;
            continue;
        }

        // Edge Case when update is
        // is required till the front
        if (a == 1) {
            cout << __gcd(prefix[K - 1] * X,
                          suffix[K]);
        }

        // Find the resultant operation
        // for each query
        else {
            cout << __gcd(suffix[N - K] * X,
                          prefix[N - K - 1]);
        }

        cout << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Queries[][3] = {
        { 1, 2, 2 },
        { 2, 4, 5 }
    };
    int Q = sizeof(Queries)
            / sizeof(Queries[0]);

    findGCDQueries(arr, N, Queries, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Recursive function to return gcd of a and b
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

  // Function to find the GCD after performing
  // each query on array elements
  static void findGCDQueries(int arr[], int N,
                             int Queries[][],
                             int Q)
  {

    // Stores prefix array and suffix
    // array
    int prefix[] = new int[N], suffix[] = new int[N];

    prefix[0] = arr[0];
    suffix[N - 1] = arr[N - 1];

    // Build prefix array
    for (int i = 1; i < N; i++) {
      prefix[i] = gcd(prefix[i - 1],
                      arr[i]);
    }

    // Build suffix array
    for (int i = N - 2; i >= 0; i--) {
      suffix[i] = gcd(suffix[i + 1],
                      arr[i]);
    }

    // Traverse queries array
    for (int i = 0; i < Q; i++) {

      int a = Queries[i][0];
      int K = Queries[i][1];
      int X = Queries[i][2];

      // Edge Case when update is
      // is required till the end
      if (K == N) {
        System.out.print(prefix[N - 1] * X);
        continue;
      }

      // Edge Case when update is
      // is required till the front
      if (a == 1) {
        System.out.print(gcd(prefix[K - 1] * X,
                             suffix[K]));
      }

      // Find the resultant operation
      // for each query
      else {
        System.out.print(gcd(suffix[N - K] * X,
                             prefix[N - K - 1]));
      }

      System.out.print(" ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 2, 3, 4, 8 };
    int N = arr.length;
    int Queries[][] = {
      { 1, 2, 2 },
      { 2, 4, 5 }
    };
    int Q = Queries.length;

    findGCDQueries(arr, N, Queries, Q);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import gcd

# Function to find the GCD after performing
# each query on array elements
def findGCDQueries(arr, N, Queries, Q):

    # Stores prefix array and suffix
    # array
    prefix = [0 for i in range(N)]
    suffix = [0 for i in range(N)]

    prefix[0] = arr[0]
    suffix[N - 1] = arr[N - 1]

    # Build prefix array
    for i in range(1,N,1):
        prefix[i] = gcd(prefix[i - 1], arr[i])

    # Build suffix array
    i = N - 2
    while(i>= 0):
        suffix[i] = gcd(suffix[i + 1], arr[i])
        i -= 1

    # Traverse queries array
    for i in range(Q):
        a = Queries[i][0]
        K = Queries[i][1]
        X = Queries[i][2]

        # Edge Case when update is
        # is required till the end
        if (K == N):
            print(prefix[N - 1] * X,end = " ")
            continue

        # Edge Case when update is
        # is required till the front
        if (a == 1):
            print(gcd(prefix[K - 1] * X,suffix[K]),end = " ")

        # Find the resultant operation
        # for each query
        else:
            print(gcd(suffix[N - K] * X, prefix[N - K - 1]),end = " ")

# Driver Code
if __name__ == '__main__':
    arr =  [2, 3, 4, 8]
    N = len(arr)
    Queries = [[1, 2, 2], [2, 4, 5]]
    Q = len(Queries)
    findGCDQueries(arr, N, Queries, Q)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Recursive function to return gcd of a and b
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

  // Function to find the GCD after performing
  // each query on array elements
  static void findGCDQueries(int []arr, int N,
                             int [,]Queries,
                             int Q)
  {

    // Stores prefix array and suffix
    // array
    int []prefix = new int[N];
    int []suffix = new int[N];

    prefix[0] = arr[0];
    suffix[N - 1] = arr[N - 1];

    // Build prefix array
    for (int i = 1; i < N; i++) {
      prefix[i] = gcd(prefix[i - 1],
                      arr[i]);
    }

    // Build suffix array
    for (int i = N - 2; i >= 0; i--) {
      suffix[i] = gcd(suffix[i + 1],
                      arr[i]);
    }

    // Traverse queries array
    for (int i = 0; i < Q; i++) {

      int a = Queries[i,0];
      int K = Queries[i,1];
      int X = Queries[i,2];

      // Edge Case when update is
      // is required till the end
      if (K == N) {
        Console.Write(prefix[N - 1] * X);
        continue;
      }

      // Edge Case when update is
      // is required till the front
      if (a == 1) {
        Console.Write(gcd(prefix[K - 1] * X,
                          suffix[K]));
      }

      // Find the resultant operation
      // for each query
      else {
        Console.Write(gcd(suffix[N - K] * X,
                          prefix[N - K - 1]));
      }

      Console.Write(" ");
    }
  }

  // Driver Code
  public static void Main(string[] args)
  {

    int []arr = { 2, 3, 4, 8 };
    int N = arr.Length;
    int [,]Queries = {
      { 1, 2, 2 },
      { 2, 4, 5 }
    };
    int Q = Queries.GetLength(0);

    findGCDQueries(arr, N, Queries, Q);
  }
}

// This code is contributed by AnkThon.
```

## java 描述语言

```
<script>

    // JavaScript program to implement the above approach

    // Recursive function to return gcd of a and b
    function gcd(a, b)
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

    // Function to find the GCD after performing
    // each query on array elements
    function findGCDQueries(arr, N, Queries, Q)
    {

      // Stores prefix array and suffix
      // array
      let prefix = new Array(N), suffix = new Array(N);

      prefix[0] = arr[0];
      suffix[N - 1] = arr[N - 1];

      // Build prefix array
      for (let i = 1; i < N; i++) {
        prefix[i] = gcd(prefix[i - 1],
                        arr[i]);
      }

      // Build suffix array
      for (let i = N - 2; i >= 0; i--) {
        suffix[i] = gcd(suffix[i + 1],
                        arr[i]);
      }

      // Traverse queries array
      for (let i = 0; i < Q; i++) {

        let a = Queries[i][0];
        let K = Queries[i][1];
        let X = Queries[i][2];

        // Edge Case when update is
        // is required till the end
        if (K == N) {
          document.write(prefix[N - 1] * X);
          continue;
        }

        // Edge Case when update is
        // is required till the front
        if (a == 1) {
          document.write(gcd(prefix[K - 1] * X,
                               suffix[K]));
        }

        // Find the resultant operation
        // for each query
        else {
          document.write(gcd(suffix[N - K] * X,
                               prefix[N - K - 1]));
        }

        document.write(" ");
      }
    }

    let arr = [ 2, 3, 4, 8 ];
    let N = arr.length;
    let Queries = [
      [ 1, 2, 2 ],
      [ 2, 4, 5 ]
    ];
    let Q = Queries.length;

    findGCDQueries(arr, N, Queries, Q);

</script>
```

**Output**

```
2 5
```

***时间复杂度:** O((N + Q)* log M，其中 **M** 是数组的最大元素。*
***辅助空间:** O(N)*