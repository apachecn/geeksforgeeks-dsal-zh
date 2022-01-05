# 骆驼香蕉拼图| DP

> 原文:[https://www.geeksforgeeks.org/camel-and-banana-puzzle-dp/](https://www.geeksforgeeks.org/camel-and-banana-puzzle-dp/)

一个人想把香蕉转移到一个目的地**一个**公里外。他最初有 T2 香蕉和一头骆驼。骆驼一次不能携带超过 T4 的香蕉，每走一公里就要吃一根香蕉。给定三个整数 **A** 、 **B** 和 **C** ，任务是找到此人可以使用骆驼转移到目的地的最大香蕉数量。

**注:**给定的问题是著名的[骆驼-香蕉难题](https://www.geeksforgeeks.org/puzzle-15-camel-and-banana-puzzle/)的一般化版本。

**示例:**

> **输入:** A = 10，B = 30，C = 10
> T3】输出: 5
> 
> **输入:** A = 1000，B = 3000，C = 1000
> T3】输出: 533

**方法:**利用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)借助[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决给定问题，使用以下要点:

*   可以观察到，最有效的转移香蕉的方法是将有 **A** km 的路径 **(u，v)** 分割成一些更小的部分。假设 **x** 是路径 **(u，v)** 中的断点。最佳选择是将所有香蕉从 **u** 转移到 **x** ，再从 **x** 转移到 **v** 。
*   路径 **(u，v)** 中可以有任意数量的断点，这样断点的计数< **A** 。
*   如果 **C** 是 **X** (即 **X % C = 0** )的因子，则骆驼一次可以携带 **C** 香蕉以便将 **X** 香蕉运送任意距离的总行程数可以通过公式**2 * X/C–1**来计算，否则 **2 * X / C +1** 。

利用上述观察，可以通过以下步骤解决给定的问题:

*   考虑一个 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)T2【DP】[]，其中一个状态**DP【A】【B】**代表一只骆驼在最初拥有 **B** 香蕉的 **A** 公里的距离上可以转移的最大香蕉数量。用 **-1** 初始化 **dp[][]** 数组。
*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)来迭代 **A** km 的给定路径，并在每个有效索引处创建一个断点，然后递归调用剩余路径的函数。
*   记住每个状态下香蕉的最大数量，如果已经计算出当前状态，则返回记忆值。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the overlapping state
int dp[1001][3001];

// Recursive function to find the maximum
// number of bananas that can be transferred
// to A distance using memoization
int recBananaCnt(int A, int B, int C)
{
    // Base Case where count of bananas
    // is less that the given distance
    if (B <= A) {
        return 0;
    }

    // Base Case where count of bananas
    // is less that camel's capacity
    if (B <= C) {
        return B - A;
    }

    // Base Case where distance = 0
    if (A == 0) {
        return B;
    }

    // If the current state is already
    // calculated
    if (dp[A][B] != -1) {
        return dp[A][B];
    }

    // Stores the maximum count of bananas
    int maxCount = INT_MIN;

    // Stores the number of trips to transfer
    // B bananas using a camel of capacity C
    int tripCount = B % C == 0 ? ((2 * B) / C) - 1
                               : ((2 * B) / C) + 1;

    // Loop to iterate over all the
    // breakpoints in range [1, A]
    for (int i = 1; i <= A; i++) {

        // Recursive call over the
        // remaining path
        int curCount
            = recBananaCnt(A - i,
                           B - tripCount * i, C);

        // Update the maxCount
        if (curCount > maxCount) {
            maxCount = curCount;

            // Memoize the current value
            dp[A][B] = maxCount;
        }
    }

    // Return answer
    return maxCount;
}

// Function to find the maximum number of
// bananas that can be transferred
int maxBananaCnt(int A, int B, int C)
{
    // Initialize dp array with -1
    memset(dp, -1, sizeof(dp));

    // Function Call
    return recBananaCnt(A, B, C);
}

// Driver Code
int main()
{
    int A = 1000;
    int B = 3000;
    int C = 1000;
    cout << maxBananaCnt(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
public class GFG {

    // Stores the overlapping state
    final static int dp[][] = new int[1001][3001];

    // Recursive function to find the maximum
    // number of bananas that can be transferred
    // to A distance using memoization
    static int recBananaCnt(int A, int B, int C)
    {

        // Base Case where count of bananas
        // is less that the given distance
        if (B <= A) {
            return 0;
        }

        // Base Case where count of bananas
        // is less that camel's capacity
        if (B <= C) {
            return B - A;
        }

        // Base Case where distance = 0
        if (A == 0) {
            return B;
        }

        // If the current state is already
        // calculated
        if (dp[A][B] != -1) {
            return dp[A][B];
        }

        // Stores the maximum count of bananas
        int maxCount = Integer.MIN_VALUE;

        // Stores the number of trips to transfer
        // B bananas using a camel of capacity C
        int tripCount = B % C == 0 ? ((2 * B) / C) - 1 : ((2 * B) / C) + 1;

        // Loop to iterate over all the
        // breakpoints in range [1, A]
        for (int i = 1; i <= A; i++) {

            // Recursive call over the
            // remaining path
            int curCount
                = recBananaCnt(A - i,
                               B - tripCount * i, C);

            // Update the maxCount
            if (curCount > maxCount) {
                maxCount = curCount;

                // Memoize the current value
                dp[A][B] = maxCount;
            }
        }

        // Return answer
        return maxCount;
    }

    // Function to find the maximum number of
    // bananas that can be transferred
    static int maxBananaCnt(int A, int B, int C)
    {
        // Initialize dp array with -1
        for(int i = 0; i < 1001; i++)
            for (int j = 0; j < 3001; j++)
                dp[i][j] = -1;

        // Function Call
        return recBananaCnt(A, B, C);
    }

    // Driver Code
    public static void main (String[] args) {

            int A = 1000;
            int B = 3000;
            int C = 1000;
            System.out.println(maxBananaCnt(A, B, C));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python program of the above approach
# Stores the overlapping state
dp = [[-1 for i in range(3001)] for j in range(1001)]

# Recursive function to find the maximum
# number of bananas that can be transferred
# to A distance using memoization
def recBananaCnt(A, B, C):

    # Base Case where count of bananas
    # is less that the given distance
    if (B <= A):
        return 0

    # Base Case where count of bananas
    # is less that camel's capacity
    if (B <= C):
        return B - A

    # Base Case where distance = 0
    if (A == 0):
        return B

    # If the current state is already
    # calculated
    if (dp[A][B] != -1):
        return dp[A][B]

    # Stores the maximum count of bananas
    maxCount = -2**32

    # Stores the number of trips to transfer
    # B bananas using a camel of capacity C
    tripCount = ((2 * B) // C) - 1 if(B % C == 0 ) else ((2 * B) // C) + 1

    # Loop to iterate over all the
    # breakpoints in range [1, A]
    for i in range(1,A+1):

        # Recursive call over the
        # remaining path
        curCount = recBananaCnt(A - i, B - tripCount * i, C)

        # Update the maxCount
        if (curCount > maxCount):
            maxCount = curCount

            # Memoize the current value
            dp[A][B] = maxCount

    # Return answer
    return maxCount

# Function to find the maximum number of
# bananas that can be transferred
def maxBananaCnt(A, B, C):

    # Function Call
    return recBananaCnt(A, B, C)

# Driver Code
A = 1000
B = 3000
C = 1000
print(maxBananaCnt(A, B, C))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program of the above approach
using System;

public class GFG {

    // Stores the overlapping state
    static int[, ] dp = new int[1001, 3001];

    // Recursive function to find the maximum
    // number of bananas that can be transferred
    // to A distance using memoization
    static int recBananaCnt(int A, int B, int C)
    {

        // Base Case where count of bananas
        // is less that the given distance
        if (B <= A) {
            return 0;
        }

        // Base Case where count of bananas
        // is less that camel's capacity
        if (B <= C) {
            return B - A;
        }

        // Base Case where distance = 0
        if (A == 0) {
            return B;
        }

        // If the current state is already
        // calculated
        if (dp[A, B] != -1) {
            return dp[A, B];
        }

        // Stores the maximum count of bananas
        int maxCount = Int32.MinValue;

        // Stores the number of trips to transfer
        // B bananas using a camel of capacity C
        int tripCount = B % C == 0 ? ((2 * B) / C) - 1
                                   : ((2 * B) / C) + 1;

        // Loop to iterate over all the
        // breakpoints in range [1, A]
        for (int i = 1; i <= A; i++) {

            // Recursive call over the
            // remaining path
            int curCount
                = recBananaCnt(A - i, B - tripCount * i, C);

            // Update the maxCount
            if (curCount > maxCount) {
                maxCount = curCount;

                // Memoize the current value
                dp[A, B] = maxCount;
            }
        }

        // Return answer
        return maxCount;
    }

    // Function to find the maximum number of
    // bananas that can be transferred
    static int maxBananaCnt(int A, int B, int C)
    {

        // Initialize dp array with -1
        for (int i = 0; i < 1001; i++)
            for (int j = 0; j < 3001; j++)
                dp[i, j] = -1;

        // Function Call
        return recBananaCnt(A, B, C);
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int A = 1000;
        int B = 3000;
        int C = 1000;
        Console.WriteLine(maxBananaCnt(A, B, C));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Stores the overlapping state
       // Initialize dp array with -1
       let dp = new Array(1001);
       for (let i = 0; i < dp.length; i++)
       {
           dp[i] = (new Array(3001).fill(-1))
       }

       // Recursive function to find the maximum
       // number of bananas that can be transferred
       // to A distance using memoization
       function recBananaCnt(A, B, C)
       {

           // Base Case where count of bananas
           // is less that the given distance
           if (B <= A) {
               return 0;
           }

           // Base Case where count of bananas
           // is less that camel's capacity
           if (B <= C) {
               return B - A;
           }

           // Base Case where distance = 0
           if (A == 0) {
               return B;
           }

           // If the current state is already
           // calculated
           if (dp[A][B] != -1) {
               return dp[A][B];
           }

           // Stores the maximum count of bananas
           let maxCount = Number.MIN_VALUE;

           // Stores the number of trips to transfer
           // B bananas using a camel of capacity C
           let tripCount = B % C == 0 ? Math.floor((2 * B) / C) - 1
               : Math.floor((2 * B) / C) + 1;

           // Loop to iterate over all the
           // breakpoints in range [1, A]
           for (let i = 1; i <= A; i++) {

               // Recursive call over the
               // remaining path
               let curCount
                   = recBananaCnt(A - i,
                       B - tripCount * i, C);

               // Update the maxCount
               if (curCount > maxCount) {
                   maxCount = curCount;

                   // Memoize the current value
                   dp[A][B] = maxCount;
               }
           }

           // Return answer
           return maxCount;
       }

       // Function to find the maximum number of
       // bananas that can be transferred
       function maxBananaCnt(A, B, C) {
           // Function Call
           return recBananaCnt(A, B, C);
       }

       // Driver Code
       let A = 1000;
       let B = 3000;
       let C = 1000;
       document.write(maxBananaCnt(A, B, C));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
533
```

***时间复杂度:**O(A * A * B)*
T5**辅助空间:** O(A*B)