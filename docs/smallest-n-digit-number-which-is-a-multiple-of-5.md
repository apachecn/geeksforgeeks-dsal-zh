# 最小的 N 位数，是 5 的倍数

> 原文:[https://www . geeksforgeeks . org/最小 n 位数 5 的倍数/](https://www.geeksforgeeks.org/smallest-n-digit-number-which-is-a-multiple-of-5/)

给定一个整数 **N ≥ 1** ，任务是找到最小的 **N** 位数，它是 **5** 的倍数。
**举例:**

> **输入:** N = 1
> **输出:** 5
> **输入:** N = 2
> **输出:** 10
> **输入:** N = 3
> **输出:** 100

**进场:**

*   如果 **N = 1** ，则答案为 **5** 。
*   **如果 N > 1** 那么答案将是**(10<sup>(N–1)</sup>)**因为 **5** 的最小倍数系列将像 **10、100、1000、10000、100000、…** 一样继续下去

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest n digit
// number which is a multiple of 5
int smallestMultiple(int n)
{
    if (n == 1)
        return 5;
    return pow(10, n - 1);
}

// Driver code
int main()
{
    int n = 4;
    cout << smallestMultiple(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the smallest n digit
    // number which is a multiple of 5
    static int smallestMultiple(int n)
    {
        if (n == 1)
            return 5;
        return (int)(Math.pow(10, n - 1));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        System.out.println(smallestMultiple(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the smallest n digit
# number which is a multiple of 5
def smallestMultiple(n):

    if (n == 1):
        return 5
    return pow(10, n - 1)

# Driver code
n = 4
print(smallestMultiple(n))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the smallest n digit
    // number which is a multiple of 5
    static int smallestMultiple(int n)
    {
        if (n == 1)
            return 5;
        return (int)(Math.Pow(10, n - 1));
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.Write(smallestMultiple(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the smallest n digit
// number which is a multiple of 5
function smallestMultiple($n)
{
    if ($n == 1)
        return 5;
    return pow(10, $n - 1);
}

// Driver code
$n = 4;
echo smallestMultiple($n);
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the smallest n digit
// number which is a multiple of 5
function smallestMultiple(n)
{
    if (n == 1)
        return 5;
    return Math.pow(10, n - 1);
}

// Driver code
var n = 4;
document.write(smallestMultiple(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1000
```

**时间复杂度:** O(1)