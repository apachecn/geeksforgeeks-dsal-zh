# 求 K 次交替减 X 加 Y 等于 0 形成的数

> 原文:[https://www . geesforgeks . org/find-number-by-k-times-alternative-reducing-x-and-add-y-to-0/](https://www.geeksforgeeks.org/find-number-formed-by-k-times-alternatively-reducing-x-and-adding-y-to-0/)

给定三个正整数 **K** 、 **X** 、 **Y** ，任务是求 **X** 交替减去 **Y** 到 **0** 合计 **K** 次数形成的数。

**示例:**

> **输入:** X = 2，Y = 5，K = 3
> **输出:** 1
> **说明:**
> 以下是在 0 上执行 K(= 3)次的操作:
> **操作 1:** 将值 0 减少 X(= 2)将其修改为 0–2 = 2。
> **操作 2:** 将值-2 增加 Y(= 5)将其修改为-2 + 5 = 3。
> **操作 3:** 将值 3 减少 X(= 2)将其修改为 3–2 = 1。
> 修改值后得到的值为 1。
> 
> **输入:** X = 1，Y = 100，K = 4
> T3】输出: 198

**天真法:**给定的问题可以通过执行给定的操作 **K** 次数并打印得到的结果来解决。

***时间复杂度:** O(K)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过查找 **K** 移动次数中递减(使用 **X** 的值)和递增(使用 **Y** 的值)的总值，然后打印这些值的总和作为结果来优化。

必须添加到结果中的值计算如下:

> addY = Y*(K/2)
> 其中，K/2 执行加法运算的次数。

必须从结果中减去的值计算如下:

> addY = Y*(K/2 + K&1)
> 其中，K/2 执行减法运算的次数如果运算次数为奇数，则执行额外的减法运算。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value obtained
// after alternatively reducing X and
// adding Y to 0 total K number of times
int positionAfterKJumps(int X, int Y, int K)
{
    // Stores the final result after
    // adding only Y to 0
    int addY = Y * (K / 2);

    // Stores the final number after
    // reducing only X from 0
    int reduceX = -1 * X * (K / 2 + K % 2);

    // Return the result obtained
    return addY + reduceX;
}

// Driver Code
int main()
{
    int X = 2, Y = 5, K = 3;
    cout << positionAfterKJumps(X, Y, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the value obtained
    // after alternatively reducing X and
    // adding Y to 0 total K number of times
    static int positionAfterKJumps(int X, int Y, int K)
    {

        // Stores the final result after
        // adding only Y to 0
        int addY = Y * (K / 2);

        // Stores the final number after
        // reducing only X from 0
        int reduceX = -1 * X * (K / 2 + K % 2);

        // Return the result obtained
        return addY + reduceX;
    }

    // Driver Code
    public static void main(String[] args) {

        int X = 2, Y = 5, K = 3;
        System.out.print(positionAfterKJumps(X, Y, K));
    }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the value obtained
# after alternatively reducing X and
# adding Y to 0 total K number of times
def positionAfterKJumps(X, Y, K):

    # Stores the final result after
    # adding only Y to 0
    addY = Y * (K // 2)

    # Stores the final number after
    # reducing only X from 0
    reduceX = -1 * X * (K // 2 + K % 2)

   # Return the result obtained
    return addY + reduceX

# Driver Code
X = 2
Y = 5
K = 3
print(positionAfterKJumps(X, Y, K))

# This code is contributed by subhammahato348.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the value obtained
    // after alternatively reducing X and
    // adding Y to 0 total K number of times
    static int positionAfterKJumps(int X, int Y, int K)
    {

        // Stores the final result after
        // adding only Y to 0
        int addY = Y * (K / 2);

        // Stores the final number after
        // reducing only X from 0
        int reduceX = -1 * X * (K / 2 + K % 2);

        // Return the result obtained
        return addY + reduceX;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int X = 2, Y = 5, K = 3;
        Console.WriteLine(positionAfterKJumps(X, Y, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the value obtained
        // after alternatively reducing X and
        // adding Y to 0 total K number of times
        function positionAfterKJumps(X, Y, K) {
            // Stores the final result after
            // adding only Y to 0
            let addY = Y * Math.floor(K / 2);

            // Stores the final number after
            // reducing only X from 0
            let reduceX = -1 * X * (Math.floor(K / 2) + K % 2);

            // Return the result obtained
            return addY + reduceX;
        }

        // Driver Code

        let X = 2, Y = 5, K = 3;
        document.write(positionAfterKJumps(X, Y, K));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
1
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)