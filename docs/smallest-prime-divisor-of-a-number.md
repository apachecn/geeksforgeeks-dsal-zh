# 一个数的最小质数

> 原文:[https://www . geesforgeks . org/最小素数除数/](https://www.geeksforgeeks.org/smallest-prime-divisor-of-a-number/)

给定一个数 N，求 N 的最小素除数。

**示例:**

> **输入:**25
> T3】输出: 5
> 
> **输入:**31
> T3】输出: 31

**进场:**

*   检查这个数是否能被 2 整除。
*   从 i = 3 迭代到 *sqrt(N)* ，跳 2。
*   如果任何一个数除以 N，那么它就是最小的素除数。
*   如果它们都不分裂，那么 N 就是答案。

下面是上述算法的实现:

## C++

```
// C++ program to count the number of
// subarrays that having 1
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest divisor
int smallestDivisor(int n)
{
    // if divisible by 2
    if (n % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for (int i = 3; i * i <= n; i += 2) {
        if (n % i == 0)
            return i;
    }

    return n;
}

// Driver Code
int main()
{
    int n = 31;
    cout << smallestDivisor(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to count the number of
// subarrays that having 1

import java.io.*;

class GFG {
// Function to find the smallest divisor
static int smallestDivisor(int n)
{
    // if divisible by 2
    if (n % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for (int i = 3; i * i <= n; i += 2) {
        if (n % i == 0)
            return i;
    }

    return n;
}

// Driver Code

    public static void main (String[] args) {

        int n = 31;
        System.out.println (smallestDivisor(n));

    }
}
```

## 蟒蛇 3

```
# Python3 program to count the number
# of subarrays that having 1

# Function to find the smallest divisor
def smallestDivisor(n):

    # if divisible by 2
    if (n % 2 == 0):
        return 2;

    # iterate from 3 to sqrt(n)
    i = 3;
    while(i * i <= n):
        if (n % i == 0):
            return i;
        i += 2;

    return n;

# Driver Code
n = 31;
print(smallestDivisor(n));

# This code is contributed by mits
```

## C#

```
// C# program to count the number
// of subarrays that having 1
using System;

class GFG
{

// Function to find the
// smallest divisor
static int smallestDivisor(int n)
{
    // if divisible by 2
    if (n % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for (int i = 3;
             i * i <= n; i += 2)
    {
        if (n % i == 0)
            return i;
    }

    return n;
}

// Driver Code
static public void Main ()
{
    int n = 31;
    Console.WriteLine(smallestDivisor(n));
}
}

// This code is contributed
// by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the number
// of subarrays that having 1

// Function to find the smallest divisor
function smallestDivisor($n)
{
    // if divisible by 2
    if ($n % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for ($i = 3; $i * $i <= $n; $i += 2)
    {
        if ($n % $i == 0)
            return $i;
    }

    return $n;
}

// Driver Code
$n = 31;
echo smallestDivisor($n);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>
// javascript  program to count the number of
// subarrays that having 1

    // Function to find the smallest divisor
    function smallestDivisor(n) {
        // if divisible by 2
        if (n % 2 == 0)
            return 2;

        // iterate from 3 to sqrt(n)
        for (var i = 3; i * i <= n; i += 2) {
            if (n % i == 0)
                return i;
        }

        return n;
    }

    // Driver Code

        var n = 31;
        document.write(smallestDivisor(n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
31
```

**如何高效地找到直到 n 的所有数的素因子？**
请参考[数字的最小质因数直到 n](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)