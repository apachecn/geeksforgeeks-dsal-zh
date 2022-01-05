# 距离阵列至少 K 距离的一对的最小和

> 原文:[https://www . geeksforgeeks . org/距阵列至少 k 距离的最小对和/](https://www.geeksforgeeks.org/minimum-sum-of-a-pair-at-least-k-distance-apart-from-an-array/)

给定一个大小为 **N** 的整数**A【】**的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，任务是找出任意一对至少有 **K** 个索引的数组元素所能得到的最小和。

**示例:**

> **输入:** A[] = {1，2，3，4，5，6}，K = 2
> **输出:** 4
> **说明:**
> 可以得到的最小和是距离为 2 的 1 和 3 相加。
> **输入:** A[] = {4，2，5，4，3，2，5}，K = 3
> **输出:** 4
> **说明:**
> 可以得到的最小和是距离为 4 的 2 和 2 相加。

**天真方法:**
解决问题最简单的方法就是对每一个**I<sup>th</sup>T8】的索引**【I+K，N–1】**进行迭代，找到最小元素，比如 *min* 。检查 **min + A[i]** 是否小于目前获得的最小和，并相应更新 **minimum_sum** 。最后，打印**最小 _ 总和**。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// sum of two elements that
// are atleast K distance apart
void findMinSum(int A[], int K, int n)
{
    int minimum_sum = INT_MAX;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {

        // Initialize the min value
        int mini = INT_MAX;

        // Iterate from i + k to N
        for(int j = i + K; j < n; j++)

            // Find the minimum
            mini = min(mini, A[j]);

        if (mini == INT_MAX)
            continue;

        // Update the minimum sum
        minimum_sum = min(minimum_sum,
                          A[i] + mini);
    }

    // Print the answer
    cout << (minimum_sum);
}

// Driver Code
int main()
{
    int A[] = { 4, 2, 5, 4, 3, 2, 5 };
    int K = 3;
    int n = sizeof(A) / sizeof(A[0]);

    findMinSum(A, K, n);
    return 0;
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.util.*;
class GFG {

    // Function to find the minimum
    // sum of two elements that
    // are atleast K distance apart
    public static void
    findMinSum(int A[], int K)
    {
        // Length of the array
        int n = A.length;

        int minimum_sum
            = Integer.MAX_VALUE;

        // Iterate over the array
        for (int i = 0; i < n; i++) {

            // Initialize the min value
            int min = Integer.MAX_VALUE;

            // Iterate from i + k to N
            for (int j = i + K; j < n; j++)

                // Find the minimum
                min = Math.min(min, A[j]);

            if (min == Integer.MAX_VALUE)
                continue;

            // Update the minimum sum
            minimum_sum = Math.min(minimum_sum,
                                   A[i] + min);
        }

        // Print the answer
        System.out.println(minimum_sum);
    }

    // Driver Code
    public static void
        main(String[] args)
    {

        int A[] = { 4, 2, 5, 4, 3, 2, 5 };
        int K = 3;

        findMinSum(A, K);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
import sys

# Function to find the minimum
# sum of two elements that
# are atleast K distance apart
def findMinSum(A, K):

    # Length of the array
    n = len(A);

    minimum_sum = sys.maxsize;

    # Iterate over the array
    for i in range(n):

        # Initialize the min value
        minimum = sys.maxsize;

        # Iterate from i + k to N
        for j in range(i + K, n, 1):

            # Find the minimum
            minimum = min(minimum, A[j]);

        if (minimum == sys.maxsize):
            continue;

        # Update the minimum sum
        minimum_sum = min(minimum_sum, A[i] + minimum);

    # Prthe answer
    print(minimum_sum);

# Driver Code
if __name__ == '__main__':
    A = [4, 2, 5, 4, 3, 2, 5];
    K = 3;

    findMinSum(A, K);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to find the minimum
  // sum of two elements that
  // are atleast K distance apart
  public static void findMinSum(int []A,
                                int K)
  {
    // Length of the array
    int n = A.Length;

    int minimum_sum = int.MaxValue;

    // Iterate over the array
    for (int i = 0; i < n; i++)
    {

      // Initialize the min value
      int min = int.MaxValue;

      // Iterate from i + k to N
      for (int j = i + K; j < n; j++)

        // Find the minimum
        min = Math.Min(min, A[j]);

      if (min == int.MaxValue)
        continue;

      // Update the minimum sum
      minimum_sum = Math.Min(minimum_sum,
                             A[i] + min);
    }

    // Print the answer
    Console.WriteLine(minimum_sum);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []A = { 4, 2, 5, 4, 3, 2, 5 };
    int K = 3;

    findMinSum(A, K);
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
    // Javascript program to implement
      // the above approach

    // Function to find the minimum
    // sum of two elements that
    // are atleast K distance apart
    function findMinSum(A, K, n)
    {
        let minimum_sum = Number.MAX_VALUE;

        // Iterate over the array
        for(let i = 0; i < n; i++)
        {

            // Initialize the min value
            let mini = Number.MAX_VALUE;

            // Iterate from i + k to N
            for(let j = i + K; j < n; j++)

                // Find the minimum
                mini = Math.min(mini, A[j]);

            if (mini == Number.MAX_VALUE)
                continue;

            // Update the minimum sum
            minimum_sum = Math.min(minimum_sum,
                              A[i] + mini);
        }

        // Print the answer
        document.write(minimum_sum);
    }

    let A = [ 4, 2, 5, 4, 3, 2, 5 ];
    let K = 3;
    let n = A.length;

    findMinSum(A, K, n);

    // This code is conytributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**
使用 [**后缀数组**](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/) 可以优化上述方法。请遵循以下步骤:

*   初始化一个后缀数组(比如说**后缀[]** ，其中**后缀[i]** 存储从索引 **N-1 到 i** 的所有元素的最小值。
*   对于任何第 i <sup>个</sup>索引，相距 **K** 距离的最小元素存储在后缀数组中的索引 **i + K** 处。
*   对于范围从 **0 到 N–1**的 **i** ，检查**A【I】+后缀【I+k】**<**minimum _ sum**是否存在，并相应更新 **minimum_sum** 。
*   最后打印 **minimum_sum** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
//the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// sum of two elements that
// are atleast K distance apart
void findMinSum(int A[], int K, int len)
{

  // Length of the array
  int n = len;
  int suffix_min[n] = {0};

  suffix_min[n - 1] = A[n - 1];

  // Find the suffix array
  for (int i = n - 2; i >= 0; i--)
    suffix_min[i] = min(suffix_min[i + 1], A[i]);

  int min_sum = INT_MAX;

  // Iterate in the array
  for (int i = 0; i < n; i++)
  {
    if (i + K < n)

      // Update minimum sum
      min_sum = min(min_sum, A[i] +
                    suffix_min[i + K]);
  }

  // Print the answer
  cout << min_sum;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3, 4, 5, 6 };
    int K = 2;
    int n = sizeof(A) / sizeof(A[0]);
    findMinSum(A, K, n);
    return 0;
}

// This code is contributed by Rohit_ranjan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.util.*;
class GFG {

    // Function to find the minimum
    // sum of two elements that
    // are atleast K distance apart
    public static void
    findMinSum(int A[], int K)
    {

        // Length of the array
        int n = A.length;
        int suffix_min[] = new int[n];

        suffix_min[n - 1] = A[n - 1];

        // Find the suffix array
        for (int i = n - 2; i >= 0; i--)
            suffix_min[i]
                = Math.min(suffix_min[i + 1],
                           A[i]);

        int min_sum = Integer.MAX_VALUE;

        // Iterate in the array
        for (int i = 0; i < n; i++) {

            if (i + K < n)

                // Update minimum sum
                min_sum = Math.min(
                    min_sum, A[i]
                                 + suffix_min[i + K]);
        }

        // Print the answer
        System.out.println(min_sum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 1, 2, 3, 4, 5, 6 };
        int K = 2;

        findMinSum(A, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the minimum
# sum of two elements that
# are atleast K distance apart
def findMinSum(A, K):

    # Length of the array
    n = len(A);

    suffix_min = [0] * n;
    suffix_min[n - 1] = A[n - 1];

    # Find the suffix array
    for i in range(n - 2, -1, -1):
        suffix_min[i] = min(suffix_min[i + 1], A[i]);

    min_sum = sys.maxsize;

    # Iterate in the array
    for i in range(n):
        if (i + K < n):

            # Update minimum sum
            min_sum = min(min_sum, A[i] +
                          suffix_min[i + K]);

    # Print the answer
    print(min_sum);

# Driver Code
if __name__ == '__main__':

    A = [ 1, 2, 3, 4, 5, 6 ];
    K = 2;

    findMinSum(A, K);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the minimum
// sum of two elements that
// are atleast K distance apart
public static void findMinSum(int []A, int K)
{

    // Length of the array
    int n = A.Length;
    int []suffix_min = new int[n];

    suffix_min[n - 1] = A[n - 1];

    // Find the suffix array
    for(int i = n - 2; i >= 0; i--)
        suffix_min[i] = Math.Min(suffix_min[i + 1],
                                          A[i]);

    int min_sum = int.MaxValue;

    // Iterate in the array
    for(int i = 0; i < n; i++)
    {
        if (i + K < n)

            // Update minimum sum
            min_sum = Math.Min(min_sum, A[i] +
                               suffix_min[i + K]);
    }

    // Print the answer
    Console.WriteLine(min_sum);
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 1, 2, 3, 4, 5, 6 };
    int K = 2;

    findMinSum(A, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

    // Function to find the minimum
    // sum of two elements that
    // are atleast K distance apart
   function
    findMinSum(A, K)
    {

        // Length of the array
        let n = A.length;
        let suffix_min = Array.from({length: n}, (_, i) => 0);

        suffix_min[n - 1] = A[n - 1];

        // Find the suffix array
        for (let i = n - 2; i >= 0; i--)
            suffix_min[i]
                = Math.min(suffix_min[i + 1],
                           A[i]);

        let min_sum = Number.MAX_VALUE;

        // Iterate in the array
        for (let i = 0; i < n; i++) {

            if (i + K < n)

                // Update minimum sum
                min_sum = Math.min(
                    min_sum, A[i]
                                 + suffix_min[i + K]);
        }

        // Print the answer
        document.write(min_sum);
    }

// Driver Code

           let A = [ 1, 2, 3, 4, 5, 6 ];
        let K = 2;

        findMinSum(A, K);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*