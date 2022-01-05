# 计算可被给定数字除尽的 n 位数

> 原文:[https://www . geesforgeks . org/count-n 位数-可被给定数字除尽/](https://www.geeksforgeeks.org/count-n-digit-numbers-divisible-by-given-number/)

给定 n 位数和一个数，任务是计算所有能被该数整除的 n 位数。
**例:**

```
Input : n = 2, number = 7
Output : 9
There are nine n digit numbers that
are divisible by 7\. Numbers are 14, 
21, 28, 35, 42, 49, .... 70.

Input : n = 3, number = 7
Output : 128

Input : n = 4, number = 4
Output : 2250
```

**原生方式:**遍历所有 n 位数。对于每个数字，检查可除性，

## C++

```
// Simple CPP program to count n digit
// divisible numbers.
#include <cmath>
#include <iostream>
using namespace std;

// Returns count of n digit numbers
// divisible by 'number'
int numberofterm(int n, int number)
{
    // compute the first and last term
    int firstnum = pow(10, n - 1);
    int lastnum = pow(10, n);

    // count total number of which having
    // n digit and divisible by number
    int count = 0;
    for (int i = firstnum; i < lastnum; i++)
        if (i % number == 0)
            count++;
    return count;
}

// Driver code
int main()
{
    int n = 3, num = 7;
    cout << numberofterm(n, num) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to count n digit
// divisible numbers.
import java.io.*;

class GFG {

    // Returns count of n digit numbers
    // divisible by 'number'
    static int numberofterm(int n, int number)
    {
        // compute the first and last term
        int firstnum = (int)Math.pow(10, n - 1);
        int lastnum = (int)Math.pow(10, n);

        // count total number of which having
        // n digit and divisible by number
        int count = 0;
        for (int i = firstnum; i < lastnum; i++)
            if (i % number == 0)
                count++;
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3, num = 7;
        System.out.println(numberofterm(n, num));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Simple Python 3 program to count n digit
# divisible numbers

import math

# Returns count of n digit
# numbers divisible by number
def numberofterm(n, number):

    # compute the first and last term
    firstnum = math.pow(10, n - 1)
    lastnum = math.pow(10, n)

    # count total number of which having
    # n digit and divisible by number
    count = 0
    for i in range(int(firstnum), int(lastnum)):
        if (i % number == 0):
            count += 1
    return count

# Driver code
n = 3
num = 7
print(numberofterm(n, num))

# This article is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// Simple C# program to count n digit
// divisible numbers.
using System;

class GFG
{

    // Returns count of n digit numbers
    // divisible by 'number'
    static int numberofterm(int n, int number)
    {
        // compute the first and last term
        int firstnum = (int)Math.Pow(10, n - 1);
        int lastnum = (int)Math.Pow(10, n);

        // count total number of which having
        // n digit and divisible by number
        int count = 0;
        for (int i = firstnum; i < lastnum; i++)
            if (i % number == 0)
                count++;
        return count;
    }

    // Driver code
    public static void Main ()
    {
        int n = 3, num = 7;
        Console.Write(numberofterm(n, num));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple php program to count n digit
// divisible numbers.

// Returns count of n digit numbers
// divisible by 'number'
function numberofterm($n, $number)
{

    // compute the first and last term
    $firstnum = pow(10, $n - 1);
    $lastnum = pow(10, $n);

    // count total number of which having
    // n digit and divisible by number
    $count = 0;
    for ($i = $firstnum; $i < $lastnum; $i++)
        if ($i % $number == 0)
            $count++;
    return $count;
}

    // Driver code
    $n = 3;
    $num = 7;
    echo numberofterm($n, $num);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// JavaScript program to count n digit
// divisible numbers.

// Returns count of n digit numbers
    // divisible by 'number'
    function numberofterm(n, number)
    {
        // compute the first and last term
        let firstnum = Math.pow(10, n - 1);
        let lastnum = Math.pow(10, n);

        // count total number of which having
        // n digit and divisible by number
        let count = 0;
        for (let i = firstnum; i < lastnum; i++)
            if (i % number == 0)
                count++;
        return count;
    }

// Driver Code

        let n = 3, num = 7;
        document.write(numberofterm(n, num));

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
128
```