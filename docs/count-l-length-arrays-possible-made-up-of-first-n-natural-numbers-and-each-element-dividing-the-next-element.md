# 计算可能由前 N 个自然数和每个元素分割下一个元素构成的 L 长度数组

> 原文:[https://www . geesforgeks . org/count-l-length-arrays-可能-由第一个 n 个自然数和每个元素组成-分割下一个元素/](https://www.geeksforgeeks.org/count-l-length-arrays-possible-made-up-of-first-n-natural-numbers-and-each-element-dividing-the-next-element/)

给定两个正整数 **N** 和 **L** ，任务是找出由第一个**N**T10】个自然数组成的**L**-长度[个数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的个数，这样数组中的每个元素都会划分下一个元素。

**示例:**

> **输入:** N = 3，L = 3
> **输出:** 7
> **解释:**
> 以下数组具有范围[1，3]中的元素，每个数组元素划分其下一个元素:
> 
> 1.  {1, 1, 1}
> 2.  {1, 1, 2}
> 3.  {1, 2, 2}
> 4.  {1, 1, 3}
> 5.  {1, 3, 3}
> 6.  {2, 2, 2}
> 7.  {3, 3, 3}
> 
> 因此，数组的数量是 7。
> 
> **输入:** N = 2，L = 4
> T3】输出: 5

**方法:**给定的问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和厄拉多塞的[筛的思想来解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   初始化一个 2D [数组](https://www.geeksforgeeks.org/array-data-structure/) **dp[][]** ，其中 **dp[i][j]** 表示以 **j** 结束的长度为 **i** 的序列数，并将 **dp[0][1]** 初始化为 **1** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，L–1】**，使用变量 **j** 嵌套范围[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**:
    *   由于构造数组的下一个元素应该是当前元素的倍数，因此以增量 **j** 迭代范围**【j，N】**，并将 **dp[i + 1][k]** 的值更新为值 **dp[i][j] + dp[i + 1][k]** 。
*   初始化一个变量，说**回答**为 **0** ，存储数组的结果数。
*   迭代范围**【1，N】**并将**DP【L】【I】**的值添加到变量 **ans** 中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// arrays of length L such that each
// element divides the next element
int numberOfArrays(int n, int l)
{

    // Stores the number of sequences
    // of length i that ends with j
    int dp[l + 1][n + 1];

    // Initialize 2D array dp[][] as 0
    memset(dp, 0, sizeof dp);

    // Base Case
    dp[0][1] = 1;

    // Iterate over the range [0, l]
    for (int i = 0; i < l; i++) {
        for (int j = 1; j <= n; j++) {

            // Iterate for all multiples
            // of j
            for (int k = j; k <= n; k += j) {

                // Incrementing dp[i+1][k]
                // by dp[i][j] as the next
                // element is multiple of j
                dp[i + 1][k] += dp[i][j];
            }
        }
    }

    // Stores the number of arrays
    int ans = 0;

    for (int i = 1; i <= n; i++) {

        // Add all array of length
        // L that ends with i
        ans += dp[l][i];
    }

    // Return the resultant count
    return ans;
}

// Driver Code
int main()
{
    int N = 2, L = 4;
    cout << numberOfArrays(N, L);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    static int numberOfArrays(int n, int l)
    {
        // Stores the number of sequences
    // of length i that ends with j
    int[][] dp=new int[l + 1][n + 1];

    // Base Case
    dp[0][1] = 1;

    // Iterate over the range [0, l]
    for (int i = 0; i < l; i++) {
        for (int j = 1; j <= n; j++) {

            // Iterate for all multiples
            // of j
            for (int k = j; k <= n; k += j) {

                // Incrementing dp[i+1][k]
                // by dp[i][j] as the next
                // element is multiple of j
                dp[i + 1][k] += dp[i][j];
            }
        }
    }

    // Stores the number of arrays
    int ans = 0;

    for (int i = 1; i <= n; i++) {

        // Add all array of length
        // L that ends with i
        ans += dp[l][i];
    }

    // Return the resultant count
    return ans;
    }

    // Driver Code
    public static void main (String[] args) {

        int N = 2, L = 4;
        System.out.println(numberOfArrays(N, L));
    }
}

// This code is contributed by unknown2108
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of
# arrays of length L such that each
# element divides the next element
def numberOfArrays(n, l):

    # Stores the number of sequences
    # of length i that ends with j
    dp = [[0 for i in range(n + 1)]
             for i in range(l + 1)]

    # Initialize 2D array dp[][] as 0a
    # memset(dp, 0, sizeof dp)

    # Base Case
    dp[0][1] = 1

    # Iterate over the range [0, l]
    for i in range(l):
        for j in range(1, n + 1):

            # Iterate for all multiples
            # of j
            for k in range(j, n + 1, j):

                # Incrementing dp[i+1][k]
                # by dp[i][j] as the next
                # element is multiple of j
                dp[i + 1][k] += dp[i][j]

    # Stores the number of arrays
    ans = 0

    for i in range(1, n + 1):

        # Add all array of length
        # L that ends with i
        ans += dp[l][i]

    # Return the resultant count
    return ans

# Driver Code
if __name__ == '__main__':

    N, L = 2, 4

    print(numberOfArrays(N, L))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Fumction to find the number of
// arrays of length L such that each
// element divides the next element
static int numberOfArrays(int n, int l)
{

    // Stores the number of sequences
    // of length i that ends with j
    int [,]dp = new int[l + 1,n + 1];

    // Initialize 2D array dp[][] as 0
    for(int i = 0; i < l + 1; i++){
      for(int j = 0; j < n + 1; j++)
        dp[i, j] = 0;
    }

    // Base Case
    dp[0, 1] = 1;

    // Iterate over the range [0, l]
    for (int i = 0; i < l; i++) {
        for (int j = 1; j <= n; j++) {

            // Iterate for all multiples
            // of j
            for (int k = j; k <= n; k += j) {

                // Incrementing dp[i+1][k]
                // by dp[i][j] as the next
                // element is multiple of j
                dp[i + 1,k] += dp[i,j];
            }
        }
    }

    // Stores the number of arrays
    int ans = 0;

    for (int i = 1; i <= n; i++) {

        // Add all array of length
        // L that ends with i
        ans += dp[l,i];
    }

    // Return the resultant count
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 2, L = 4;
    Console.Write(numberOfArrays(N, L));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Fumction to find the number of
// arrays of length L such that each
// element divides the next element
function numberOfArrays(n, l)
{

    // Stores the number of sequences
    // of length i that ends with j

    let dp= Array(l+1).fill().map(() =>
    Array(n+1).fill(0));

    // Initialize 2D array dp[][] as 0

    // Base Case
    dp[0][1] = 1;

    // Iterate over the range [0, l]
    for (let i = 0; i < l; i++) {
        for (let j = 1; j <= n; j++) {

            // Iterate for all multiples
            // of j
            for (let k = j; k <= n; k += j) {

                // Incrementing dp[i+1][k]
                // by dp[i][j] as the next
                // element is multiple of j
                dp[i + 1][k] += dp[i][j];
            }
        }
    }

    // Stores the number of arrays
    let ans = 0;

    for (let i = 1; i <= n; i++) {

        // Add all array of length
        // L that ends with i
        ans += dp[l][i];
    }

    // Return the resultant count
    return ans;
}

// Driver Code

    let N = 2, L = 4;
    document.write( numberOfArrays(N, L));

// This code is contributed by
// Potta Lokesh

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N * L * log N)*
T5**辅助空间:** O(N*L)