# 使用两个梯子找到最大不可到达高度

> 原文:[https://www . geeksforgeeks . org/find-最大-无法到达-高度-使用两个梯子/](https://www.geeksforgeeks.org/find-maximum-unreachable-height-using-two-ladders/)

给定两个高度为 **h1** 和 **h2** 的梯子。任务是找到两个梯子的任何可能组合都无法达到的最大高度。如果可以到达所有高度，则打印 **0** 。
**举例:**

> **输入:** H1 = 2，H2 = 11
> **输出:** 9
> 我们无法到达高度 1、3、5、7 和 9。
> 所以，最大可能高度是 9。
> **输入:** H1 = 7，H2 = 5
> **输出:** 23

**方法:**对于给定的编号 **a** 和 **b** ，最大编号 **c** 使得 **ax + by = c** 在 **x ≥ 0** 和 **y ≥ 0** 是等于**(a * b)–a–b**的[弗洛贝纽斯编号](https://en.wikipedia.org/wiki/Coin_problem)的情况下是不可能的。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum height
// which can't be reached
int maxHeight(int h1, int h2)
{
    return ((h1 * h2) - h1 - h2);
}

// Driver code
int main()
{
    int h1 = 7, h2 = 5;

    cout << max(0, maxHeight(h1, h2));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximum height
    // which can't be reached
    static int maxHeight(int h1, int h2)
    {
        return ((h1 * h2) - h1 - h2);
    }

    // Driver code
    public static void main(String args[])
    {
        int h1 = 7, h2 = 5;

        System.out.println(Math.max(0, maxHeight(h1, h2)));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the maximum height
# which can't be reached
def maxHeight(h1, h2):
    return ((h1 * h2) - h1 - h2)

# Driver code
h1 = 7
h2 = 5

print(max(0, maxHeight(h1, h2)))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum height
    // which can't be reached
    static int maxHeight(int h1, int h2)
    {
        return ((h1 * h2) - h1 - h2);
    }

    // Driver code
    public static void Main()
    {
        int h1 = 7, h2 = 5;

        Console.WriteLine(Math.Max(0, maxHeight(h1, h2)));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximum height
// which can't be reached
function maxHeight( h1,  h2)
{
    return ((h1 * h2) - h1 - h2);
}

    var h1 = 7, h2 = 5;

    document.write(Math.max(0, maxHeight(h1, h2)));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
23
```

**时间复杂度:** O(1)