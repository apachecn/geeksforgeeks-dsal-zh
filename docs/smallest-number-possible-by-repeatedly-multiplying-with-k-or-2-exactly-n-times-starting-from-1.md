# 从 1

开始，重复乘以 K 或 2 正好 N 次可能的最小数

> 原文:[https://www . geeksforgeeks . org/最小可能数乘以-k 或-2-恰好 n 次-从-1 开始/](https://www.geeksforgeeks.org/smallest-number-possible-by-repeatedly-multiplying-with-k-or-2-exactly-n-times-starting-from-1/)

给定两个正整数 **N** 和 **K** ，以及一个整数 **X** ( *最初的 **1*** )，任务是找到 **X** 的最小值，该最小值可以在执行以下操作之一 **N** 次后获得:

*   将 **X** 的值增加 **K** 。
*   将 **X** 的电流值加倍。

**示例:**

> **输入:** N = 4，K = 3，X = 1
> **输出:** 10
> **说明:**
> 执行以下操作:
> **操作 1:** 将 X 的值从 1 增加一倍到 2。
> **操作 2:** 将 X 的值从 2 加倍为 4。
> **操作 3:** 将值 K(= 3)加到 X 会将值从 4 修改为 7。
> **操作 4:** 将值 K(= 3)加到 X 会将值从 7 修改为 10。
> 执行上述操作 N(= 4)次后，X 的值为 10，这是所有可能的操作组合中的最小值。
> 
> **输入:** N = 7，K = 4，X = 1
> T3】输出: 24

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是重复执行其中一个给定的操作，直到局部执行第二个操作使 **X** 的值最大化。按照以下步骤解决问题:

*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**并执行以下步骤:
    *   如果 **X** 的值小于 **K** ，则将 **X** 的值更新为 **X*2** 。
    *   否则，将 **X** 的值增加 **K** 。
*   完成上述步骤后，将 **X** 的值打印为 **X** 的最小可能值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum value
// of X after increment X by K or twice
// value of X in each of N operations
int minPossibleValue(int N, int K, int X)
{
    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // If the value of X is less
        // than equal to K
        if (X <= K) {
            X = X * 2;
        }

        // Otherwise
        else {
            X = X + K;
        }
    }

    // Return the minimum value of X
    return X;
}

// Driver Code
int main()
{
    int N = 7, K = 4, X = 1;
    cout << minPossibleValue(N, K, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum value
// of X after increment X by K or twice
// value of X in each of N operations
public static int minPossibleValue(int N, int K,
                                   int X)
{

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // If the value of X is less
        // than equal to K
        if (X <= K)
        {
            X = X * 2;
        }

        // Otherwise
        else
        {
            X = X + K;
        }
    }

    // Return the minimum value of X
    return X;
}

// Driver Code
public static void main(String[] args)
{
    int N = 7, K = 4, X = 1;

    System.out.println(minPossibleValue(N, K, X));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum value
# of X after increment X by K or twice
# value of X in each of N operations
def minPossibleValue(N, K, X):

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # If the value of X is less
        # than equal to K
        if (X <= K):
            X = X * 2;

        # Otherwise
        else :
            X = X + K;

    # Return the minimum value of X
    return X;

# Driver Code
N = 7;
K = 4;
X = 1;

print(minPossibleValue(N, K, X));

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the minimum value
    // of X after increment X by K or twice
    // value of X in each of N operations
    static int minPossibleValue(int N, int K, int X)
    {

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++) {

            // If the value of X is less
            // than equal to K
            if (X <= K) {
                X = X * 2;
            }

            // Otherwise
            else {
                X = X + K;
            }
        }

        // Return the minimum value of X
        return X;
    }

    // Driver Code
    public static void Main()
    {
        int N = 7, K = 4, X = 1;

        Console.WriteLine(minPossibleValue(N, K, X));
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum value
// of X after increment X by K or twice
// value of X in each of N operations
function minPossibleValue(N, K, X)
{

    // Iterate over the range [1, N]
    for(let i = 1; i <= N; i++)
    {
        // If the value of X is less
        // than equal to K
        if (X <= K)
        {
            X = X * 2;
        }

        // Otherwise
        else
        {
            X = X + K;
        }
    }

    // Return the minimum value of X
    return X;
}

// Driver Code
let N = 7, K = 4, X = 1;

document.write(minPossibleValue(N, K, X));

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
24
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)