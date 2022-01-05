# 给定 n 的 5^N 第三个最后一位数字

> 原文:[https://www . geeksforgeeks . org/给定 n 的 5n 位中的最后三位数字/](https://www.geeksforgeeks.org/third-last-digit-in-5n-for-given-n/)

给定一个正整数 N，任务是从 5 <sup>N</sup> 的最后一位(最右边)找到 3 <sup>第三位</sup>数字的值。

**示例:**

```
Input : N = 6
Output : 6
Explanation : Value of 56 = 15625.

Input : N = 3
Output : 1
Explanation : Value of 53 = 125\. 
```

**方法:**在进入实际方法之前，关于数论的一些事实如下:

*   5 <sup>3</sup> 是最小的 3 位数，是 5 的幂。
*   由于 125 * 5 = 625，这就得出结论，从结果的最后三位数开始，5 的倍数(以 125 结尾)总是构成 625。
*   同样，625 * 5 = 3125，这就得出结论，多个数字(以 625 结尾)加上 5 总是会构造 125 作为结果的最后三位数字。

因此，最终的一般解决方案是:

> 案例一:如果 **n < 3** ，答案= 0。
> 案例二:如果 **n > = 3 且为偶数，**答案= 6。
> 情况 3:如果 **n > = 3 且为奇数，**答案= 1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the element
int findThirdDigit(int n)
{
    // if n < 3
    if (n < 3)
        return 0;

    // If n is even return 6
    // If n is odd return 1
    return n & 1 ? 1 : 6;
}

// Driver code
int main()
{
    int n = 7;

    cout << findThirdDigit(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG
{

// Function to find the element
static int findThirdDigit(int n)
{
    // if n < 3
    if (n < 3)
        return 0;

    // If n is even return 6
    // If n is odd return 1
    return (n & 1) > 0 ? 1 : 6;
}

// Driver code
public static void main(String args[])
{
    int n = 7;

    System.out.println(findThirdDigit(n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the element
def findThirdDigit(n):

    # if n < 3
    if n < 3:
        return 0

    # If n is even return 6
    # If n is odd return 1
    return 1 if n and 1 else 6

# Driver code
n = 7
print(findThirdDigit(n))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to find the element
static int findThirdDigit(int n)
{
    // if n < 3
    if (n < 3)
        return 0;

    // If n is even return 6
    // If n is odd return 1
    return (n & 1)>0 ? 1 : 6;
}

// Driver code
static void Main()
{
    int n = 7;

    Console.WriteLine(findThirdDigit(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the element
function findThirdDigit($n)
{
    // if n < 3
    if ($n < 3)
        return 0;

    // If n is even return 6
    // If n is odd return 1
    return $n & 1 ? 1 : 6;
}

// Driver code
$n = 7;
echo findThirdDigit($n);

// This code contributed by
// PrinciRaj1992
?>
```

## java 描述语言

```
<script>

 // Javascript implementation of the above approach

// Function to find the element
function findThirdDigit(n)
{
    // if n < 3
    if (n < 3)
        return 0;

    // If n is even return 6
    // If n is odd return 1
    return n & 1 ? 1 : 6;
}

// Driver code
var n = 7;
document.write( findThirdDigit(n));

</script>
```

**Output:** 

```
1
```