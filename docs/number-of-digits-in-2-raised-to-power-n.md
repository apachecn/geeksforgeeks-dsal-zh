# 2 的位数增加到 n 次方

> 原文:[https://www . geeksforgeeks . org/2 位数 n/升幂运算数/](https://www.geeksforgeeks.org/number-of-digits-in-2-raised-to-power-n/)

设 n 为升至 2 的任何功率，即 2 <sup>n</sup> 。我们被赋予数字 n，我们的任务是找出数字 2 <sup>n</sup> 中包含的位数。
**例:**

```
Input : n = 5
Output : 2
Explanation : 2n = 32, which has only
2 digits.

Input : n = 10
Output : 4
Explanation : 2n = 1024, which has only
4 digits.
```

我们可以用对数写出 2 <sup>n</sup> 如下:

2<sup>n</sup>= 10*<sup>nlog</sup><sub><sup>10</sup></sub><sup>2</sup>*

现在假设，x = nlog <sub>10</sub> 2、
因此，2 <sup>n</sup> = 10 <sup>x</sup>
同样，我们都知道数字 10 <sup>n</sup> 会有(n+1)个数字。因此，10 <sup>x</sup> 将有(x+1)个数字。
或者，我们可以说 2 <sup>n</sup> 会有(x+1)个数字作为 2 <sup>n</sup> = 10 <sup>x</sup> 。
因此，2 <sup>n</sup> 中的位数= (nlog <sub>10</sub> 2) + 1
以下是上述思路的实现:

## C++

```
// CPP program to find number of digits
// in 2^n
#include <bits/stdc++.h>
using namespace std;

// Function to find number of digits
// in 2^n
int countDigits(int n)
{
    return (n * log10(2) + 1);
}

// Driver code
int main()
{
    int n = 5;
    cout << countDigits(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of digits in 2^n
import java.util.*;

class Gfg
{
    // Function to find number of digits
    // in 2^n
    static int countDigits(int n)
    {
        return (int)(n * Math.log10(2) + 1);
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(countDigits(n));
    }
}

// This code is contributed by Niraj_Pandey.
```

## 蟒蛇 3

```
# Python3 program to find
# number of digits in 2^n
import math

# Function to find number
# of digits in 2^n
def countDigits(n):
    return int(n * math.log10(2) + 1);

# Driver code
n = 5;
print(countDigits(n));

# This code is contributed
# by mits
```

## C#

```
// C# program to find number
// of digits in 2^n
using System;

class GFG
{
    // Function to find
    // number of digits in 2^n
    static int countDigits(int n)
    {
        return (int)(n * Math.Log10(2) + 1);
    }

    // Driver code
    static void Main()
    {
        int n = 5;
        Console.Write(countDigits(n));
    }
}
// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// number of digits in 2^n

// Function to find number
// of digits in 2^n
function countDigits($n)
{
    return intval($n * log10(2) + 1);
}

// Driver code
$n = 5;
echo (countDigits($n));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program to find number
// of digits in 2^n

    // Function to find number of digits
    // in 2^n
    function countDigits(n)
    {
        return (n * Math.log10(2) + 1);
    }

// Driver code

        let n = 5;
        document.write(Math.floor(countDigits(n)));

             // This code is contributed by souravghosh0416.
</script>
```

**输出:**

```
2
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*