# 从总共 M 男 W 女中选择 X 男 Y 女的总方式

> 原文:[https://www . geesforgeks . org/total-way-choice-x-men-y-women-from-total-m-men-w-women/](https://www.geeksforgeeks.org/total-ways-of-choosing-x-men-and-y-women-from-a-total-of-m-men-and-w-women/)

给定四个整数 **X** 、 **Y** 、 **M** 和 **W** 。任务是从总的 **M** 男性和 **W** 女性中找出选择 **X** 男性和 **Y** 女性的途径数。

**示例:**

> **输入:** X = 1，Y = 2，M = 1，W = 3
> **输出:** 3
> 方式 1:选择唯一男性和 1 <sup>st</sup> 和 2 <sup>nd</sup> 女性。
> 方式二:选择唯一的男性和 2 <sup>nd</sup> 和 3 <sup>rd</sup> 女性。
> 方式三:选择唯一的男性和 1 <sup>st</sup> 和 3 <sup>rd</sup> 女性。
> 
> **输入:** X = 4，Y = 3，M = 6，W = 5
> T3】输出: 150

**途径:**从共计 **M** 男性中选择 **X** 男性的途径总数为**<sup>M</sup>C<sub>X</sub>T11】而从 **W** 女性中选择 **Y** 女性的途径总数为**T17】WC<sub>Y</sub>T21】。因此，组合方式的总数将为**<sup>M</sup>C<sub>X</sub>*<sup>W</sup>C<sub>Y</sub>**。****

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// value of ncr effectively
int ncr(int n, int r)
{

    // Initialize the answer
    int ans = 1;

    for (int i = 1; i <= r; i += 1) {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans /= i;
    }
    return ans;
}

// Function to return the count of required ways
int totalWays(int X, int Y, int M, int W)
{
    return (ncr(M, X) * ncr(W, Y));
}

int main()
{
    int X = 4, Y = 3, M = 6, W = 5;

    cout << totalWays(X, Y, M, W);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of the approach
import java.io.*;

class GFG
{

    // Function to return the
    // value of ncr effectively
    static int ncr(int n, int r)
    {

        // Initialize the answer
        int ans = 1;

        for (int i = 1; i <= r; i += 1)
        {

            // Divide simultaneously by
            // i to avoid overflow
            ans *= (n - r + i);
            ans /= i;
        }
        return ans;
    }

    // Function to return the count of required ways
    static int totalWays(int X, int Y, int M, int W)
    {
        return (ncr(M, X) * ncr(W, Y));
    }

    // Driver code
    public static void main (String[] args)
    {
        int X = 4, Y = 3, M = 6, W = 5;

        System.out.println(totalWays(X, Y, M, W));
    }
}

// This code is contributed by ajit_23
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# value of ncr effectively
def ncr(n, r):
    # Initialize the answer
    ans = 1

    for i in range(1,r+1):

        # Divide simultaneously by
        # i to avoid overflow
        ans *= (n - r + i)
        ans //= i
    return ans

# Function to return the count of required ways
def totalWays(X, Y, M, W):

    return (ncr(M, X) * ncr(W, Y))

X = 4
Y = 3
M = 6
W = 5

print(totalWays(X, Y, M, W))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // value of ncr effectively
    static int ncr(int n, int r)
    {

        // Initialize the answer
        int ans = 1;

        for (int i = 1; i <= r; i += 1)
        {

            // Divide simultaneously by
            // i to avoid overflow
            ans *= (n - r + i);
            ans /= i;
        }
        return ans;
    }

    // Function to return the count of required ways
    static int totalWays(int X, int Y, int M, int W)
    {
        return (ncr(M, X) * ncr(W, Y));
    }

    // Driver code
    static public void Main ()
    {
        int X = 4, Y = 3, M = 6, W = 5;

        Console.WriteLine(totalWays(X, Y, M, W));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the
// value of ncr effectively
function ncr(n, r)
{

    // Initialize the answer
    let ans = 1;

    for (let i = 1; i <= r; i += 1) {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans = parseInt(ans / i);
    }
    return ans;
}

// Function to return the count of required ways
function totalWays(X, Y, M, W)
{
    return (ncr(M, X) * ncr(W, Y));
}

// Driver Code
    let X = 4, Y = 3, M = 6, W = 5;

    document.write(totalWays(X, Y, M, W));

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
150
```