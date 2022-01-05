# 一个数的阶乘中的第一个数字

> 原文:[https://www.geeksforgeeks.org/first-digit-factorial-number/](https://www.geeksforgeeks.org/first-digit-factorial-number/)

给定一个正整数 n，求其阶乘的第一个数字。

**示例:**

```
Input  : n = 5
Output : 1
Factorial of 5 is 120 and first
digit is 1.

Input  : 1000
Output : 4
```

一个**简单的解决方案**是计算数的阶乘，然后找到其中的第一个数字。
以上解决方案导致**很快溢出**。更好的解决方案是利用[阶乘包含尾随 0](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)的事实，移除尾随 0 不会改变第一个数字。例如，对于 x > 0 和 y > 0，x * y 的第一位数字与 x * y * 100 相同。

## C++

```
// A C++ program for finding the First digit
// of the large factorial number
#include <bits/stdc++.h>
using namespace std;

int firstDigit(int n)
{
    long long int fact = 1;

    for (int i = 2; i <= n; i++) {
        fact = fact * i;

        // Removing trailing 0s as this
        // does not change first digit.
        while (fact % 10 == 0)
            fact = fact / 10;       
    }

    // loop for divide the fact until it
    // become the single digit and return
    // the fact
    while (fact >= 10)
        fact = fact / 10;

    return fact;
}

// derive main
int main()
{
    int n = 5;
    cout << firstDigit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program for finding the First digit
// of the large factorial number
class GFG{
static int firstDigit(int n)
{
    int fact = 1;

    for (int i = 2; i <= n; i++) {
        fact = fact * i;

        // Removing trailing 0s as this
        // does not change first digit.
        while (fact % 10 == 0)
            fact = fact / 10;    
    }

    // loop for divide the fact until it
    // become the single digit and return
    // the fact
    while (fact >= 10)
        fact = fact / 10;

    return fact;
}

// derive main
public static void main(String[] args)
{
    int n = 5;
    System.out.println(firstDigit(n));
}
}
//This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program for finding
# the First digit of the
# large factorial number
import math
def firstDigit(n) :
    fact = 1

    for i in range(2, n + 1) :
        fact = fact * i

        # Removing trailing 0s
        # as this does not
        # change first digit.
        while (fact % 10 == 0) :
            fact = int(fact / 10)

    # loop for divide the fact
    # until it become the single
    # digit and return the fact

    while (fact >= 10) :
        fact = int(fact / 10)

    return math.floor(fact)

# Driver Code
n = 5
print (firstDigit(n))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// A C# program for finding the First digit
// of the large factorial number
using System;

class GFG {

    static int firstDigit(int n)
    {
        int fact = 1;

        for (int i = 2; i <= n; i++)
        {
            fact = fact * i;

            // Removing trailing 0s as this
            // does not change first digit.
            while (fact % 10 == 0)
                fact = fact / 10;    
        }

        // loop for divide the fact until
        // it become the single digit and
        // return the fact
        while (fact >= 10)
            fact = fact / 10;

        return fact;
    }

    // driver function
    public static void Main()
    {
        int n = 5;

        Console.Write(firstDigit(n));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding
// the First digit of the
// large factorial number

function firstDigit($n)
{
    $fact = 1;

    for ($i = 2; $i <= $n; $i++)
    {
        $fact = $fact * $i;

        // Removing trailing 0s as this
        // does not change first digit.
        while ($fact % 10 == 0)
            $fact = $fact / 10;
    }

    // loop for divide the fact
    // until it become the single
    // digit and return    the fact

    while ($fact >= 10)
        $fact = $fact / 10;

    return floor($fact);
}

// Driver Code
$n = 5;
echo firstDigit($n);

// This code is contributed by aj_36.
?>
```

## java 描述语言

```
<script>

// JavaScript program for finding the
// First digit of the large factorial number
function firstDigit(n)
{
    let fact = 1;

    for(let i = 2; i <= n; i++)
    {
        fact = fact * i;

        // Removing trailing 0s as this
        // does not change first digit.
        while (fact % 10 == 0)
            fact = fact / 10;    
    }

    // Loop for divide the fact until it
    // become the single digit and return
    // the fact
    while (fact >= 10)
        fact = fact / 10;

    return (Math.round(fact));
}

// Driver code
let n = 5;

document.write(firstDigit(n));

// This code is contributed by splevel62

</script>
```

**Output :** 

```
1
```

对于稍高的值，上述代码也失败。最好的办法似乎是[求大数](https://www.geeksforgeeks.org/factorial-large-number/)的阶乘，然后求第一位数字。