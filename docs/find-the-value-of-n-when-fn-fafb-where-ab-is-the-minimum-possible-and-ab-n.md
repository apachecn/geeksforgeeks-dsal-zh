# 当 F(N) = f(a)+f(b)时求 N 的值，其中 a+b 是最小可能值，a*b = N

> 原文:[https://www . geesforgeks . org/find-the-value-of-n-when-fn-fafb-where-ab-是最小可能和-ab-n/](https://www.geeksforgeeks.org/find-the-value-of-n-when-fn-fafb-where-ab-is-the-minimum-possible-and-ab-n/)

给定一个整数 **N** ，任务是找到 **F(N)** 的值，如果:

1.  F(1) = 0
2.  F(2) = 2
3.  F(N) = 0，如果 N 是奇素数。
4.  F(N) = F(a) + F(b)，其中 a 和 b 是 N 的因子，而(a + b)是所有因子中的最小值。同样，a * b = N

**示例:**

> **输入:**N = 5
> T3】输出: 0
> 因为 5 是奇素数。
> **输入:** N = 4
> **输出:** 4
> 4 可写成 2 * 2，故 f(2) + f(2) = 4
> **输入:** N = 20
> **输出:** 4
> 20 可写成 f(4) + f(5)，f(4)可写成 f(2) + f(2)，即为 4。

**接近**:可以按照以下步骤解决问题:

*   如果 N 是 1 或 2，答案分别是 0 或 2。
*   在打破递推 f(n) = f(a) + f(b)时，我们得到它是一个数被 2 整除的次数。
*   f(n)的答案是 **2 *(一个数被 2 整除的次数)**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the value of F(N)
int getValueOfF(int n)
{

    // Base cases
    if (n == 1)
        return 0;
    if (n == 2)
        return 1;

    int cnt = 0;

    // Count the number of times a number
    // if divisible by 2
    while (n % 2 == 0) {
        cnt += 1;
        n /= 2;
    }

    // Return the summation
    return 2 * cnt;
}

// Driver code
int main()
{
    int n = 20;
    cout << getValueOfF(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the value of F(N)
static int getValueOfF(int n)
{

    // Base cases
    if (n == 1)
        return 0;
    if (n == 2)
        return 1;

    int cnt = 0;

    // Count the number of times a number
    // if divisible by 2
    while (n % 2 == 0)
    {
        cnt += 1;
        n /= 2;
    }

    // Return the summation
    return 2 * cnt;
}

// Driver code
public static void main (String[] args)
{
    int n = 20;
    System.out.println (getValueOfF(n));
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the value of F(N)
def getValueOfF(n):

    # Base cases
    if (n == 1):
        return 0
    if (n == 2):
        return 1

    cnt = 0

    # Count the number of times a number
    # if divisible by 2
    while (n % 2 == 0):
        cnt += 1
        n /= 2

    # Return the summation
    return 2 * cnt

# Driver code
n = 20
print(getValueOfF(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the value of F(N)
static int getValueOfF(int n)
{

    // Base cases
    if (n == 1)
        return 0;
    if (n == 2)
        return 1;

    int cnt = 0;

    // Count the number of times a number
    // if divisible by 2
    while (n % 2 == 0)
    {
        cnt += 1;
        n /= 2;
    }

    // Return the summation
    return 2 * cnt;
}

// Driver code
static public void Main ()
{
    int n = 20;
    Console.WriteLine(getValueOfF(n));
}
}

// This code is contributed by akt_mit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach
// Function to return the value of F(N)

function getValueOfF($n)
{

    // Base cases
    if ($n == 1)
        return 0;
    if ($n == 2)
        return 1;

    $cnt = 0;

    // Count the number of times a number
    // if divisible by 2
    while ($n % 2 == 0)
    {
        $cnt += 1;
        $n /= 2;
    }

    // Return the summation
    return 2 * $cnt;
}

    // Driver code
    $n = 20;
    echo getValueOfF($n);

// This code is contributed by Tushil..
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the value of F(N)
    function getValueOfF(n)
    {

        // Base cases
        if (n == 1)
            return 0;
        if (n == 2)
            return 1;

        let cnt = 0;

        // Count the number of times a number
        // if divisible by 2
        while (n % 2 == 0)
        {
            cnt += 1;
            n = parseInt(n / 2, 10);
        }

        // Return the summation
        return 2 * cnt;
    }

    let n = 20;
    document.write(getValueOfF(n));

</script>
```

**Output:** 

```
4
```