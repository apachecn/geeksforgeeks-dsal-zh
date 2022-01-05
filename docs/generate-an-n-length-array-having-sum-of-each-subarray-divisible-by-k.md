# 生成一个 N 长度阵列，每个子阵列的和可被 K 整除

> 原文:[https://www . geeksforgeeks . org/generate-an-n-length-array-having-sum-by-k-除尽/](https://www.geeksforgeeks.org/generate-an-n-length-array-having-sum-of-each-subarray-divisible-by-k/)

给定两个正整数 **N** 和 **K** ，任务是生成一个由 **N** 个不同整数组成的数组，使得构造的数组的每个子数组的元素之和可被 **K** 整除。

**示例:**

> **输入:** N = 3，K = 3
> **输出:** 3 6 9
> **解释:**
> 合成阵列的子阵列为{3}、{6}、{3，6}、{9}、{6，9}、{3，6，9}。所有这些子阵的和都可以被 k 整除
> 
> **输入:** N = 5，K = 1
> T3】输出: 1 2 3 4 5

**方法:**按照以下步骤解决问题:

1.  由于每个子阵列的元素之和需要被 **K** 整除，所以最理想的方法是构建一个数组，其中每个元素都是 **K** 的倍数。
2.  因此，迭代一个从 **i = 1** 到 **i = N** 的[循环](https://www.geeksforgeeks.org/java-for-loop-with-examples/)，对于 **i** 的每个值，打印 **K * i** 。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct an array
// with sum of each subarray
// divisible by K
void construct_Array(int N, int K)
{
    // Traverse a loop from 1 to N
    for (int i = 1; i <= N; i++) {

        // Print i-th multiple of K
        cout << K * i << " ";
    }
}

// Driver Code
int main()
{
    int N = 3, K = 3;
    construct_Array(N, K);
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

  // Function to construct an array
  // with sum of each subarray
  // divisible by K
  static void construct_Array(int N, int K)
  {

    // Traverse a loop from 1 to N
    for (int i = 1; i <= N; i++)
    {

      // Print i-th multiple of K
      System.out.print(K * i + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 3, K = 3;
    construct_Array(N, K);
  }
}

// This code is contributed by code hunt.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to construct an array
# with sum of each subarray
# divisible by K
def construct_Array(N, K) :

    # Traverse a loop from 1 to N
    for i in range(1, N + 1):

        # Pri-th multiple of K
        print(K * i, end = " ")

# Driver Code
N = 3
K = 3
construct_Array(N, K)

# This code is contributed by splevel62.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Function to construct an array
  // with sum of each subarray
  // divisible by K
  static void construct_Array(int N, int K)
  {

    // Traverse a loop from 1 to N
    for (int i = 1; i <= N; i++)
    {

      // Print i-th multiple of K
      Console.Write(K * i + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 3, K = 3;
    construct_Array(N, K);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to construct an array
// with sum of each subarray
// divisible by K
function construct_Array(N, K)
{
    // Traverse a loop from 1 to N
    for (let i = 1; i <= N; i++) {

        // Print i-th multiple of K
       document.write( K * i + " ");
    }
}

// Driver Code
    let N = 3, K = 3;
    construct_Array(N, K);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
3 6 9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)