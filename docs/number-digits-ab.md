# a^b 的位数

> 原文:[https://www.geeksforgeeks.org/number-digits-ab/](https://www.geeksforgeeks.org/number-digits-ab/)

给定两个正整数 a 和 b，任务是找出 a^b 的位数(a 的 b 次方)。
示例:

```
Input: a = 2  b = 5
Output: no. of digits = 2
Explanation:
2^5 = 32 
Hence, no. of digits = 2

Input: a = 2  b = 100
Output: no. of digits = 31
Explanation:
2^100 = 1.2676506e+30
Hence, no. of digits = 31
```

**方法:**
a^b 的位数可以用公式计算:

```
Number of Digits = 1 + b * (log<sub>10a)</sub>
```

当一个数除以 10 时，它会减少 1 位数。
例:

```
554 / 10 = 55, 55 / 10 = 5
```

请注意，554 最初有 3 位数字，但除法后有 2 位数字 55，进一步除法后只有 1 位数字 5。所以可以得出结论，要数位数，需要计算一个数除以 10 达到 1 的次数。
**对数基数 10** 的一个数是一个数需要除以 10 才能达到 1 的次数，但由于 1 本身不包含在对数基数 10 中，所以 1 被加起来就得到位数。
**注: **b *(原木 <sub>10</sub> a)** 楼层值取。
以下是计算 a^b.位数的实现方式** 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP Program to calculate
// no. of digits in a^b
#include<iostream>
#include<math.h>
using namespace std;

// function to calculate number
// of digits in a^b
int no_of_digit(int a, int b)
{
    return ((int)(b * log10(a)) + 1);
}

// driver program
int main()
{
    int a = 2, b = 100;
    cout <<"no. of digits = "<<
                  no_of_digit(a, b);
}

// This code is contributed by Smitha
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to calculate
// no. of digits in a^b
class GFG {

    // function to calculate number
    // of digits in a^b
    static int no_of_digit(int a, int b)
    {
        return ((int)(b * Math.log10(a)) + 1);
    }

    // driver program
    public static void main(String[] args)
    {
        int a = 2, b = 100;
        System.out.print("no. of digits = " +
                          no_of_digit(a, b));
    }
}
```

## 蟒蛇 3

```
# Python Program to calculate
# no. of digits in a^b
import math

# function to calculate number
# of digits in a^b
def no_of_digit(a, b):
    return ((int)(b * math.log10(a)) + 1)

# Driver Program
a = 2
b = 100
print("no of digits = ", no_of_digit(a, b))

# This code is contributed by Shrikant13
```

## C#

```
// C# Program to calculate
// no. of digits in a^b
using System;

class GFG {

    // function to calculate number
    // of digits in a^b
    static int no_of_digit(int a, int b)
    {
        return ((int)(b * Math.Log10(a)) + 1);
    }

    // driver program
    public static void Main()
    {
        int a = 2, b = 100;
        Console.Write("no. of digits = " +
                        no_of_digit(a, b));
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to calculate
// no. of digits in a^b

// function to calculate number
// of digits in a^b
function no_of_digit($a, $b)
{
    return ((int)($b * log10($a)) + 1);
}

// Driver Code
$a = 2; $b = 100;
echo("no. of digits = " .no_of_digit($a, $b));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to calculate
// no. of digits in a^b

// function to calculate number
    // of digits in a^b
    function no_of_digit(a, b)
    {
        return (Math.round((b * Math.log10(a)) + 1));
    }

// Driver program

        let a = 2, b = 100;
        document.write("no. of digits = " +
                          no_of_digit(a, b));

        // This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
no.of digits = 31
```