# 寻找简单兴趣的程序

> 原文:[https://www.geeksforgeeks.org/program-find-simple-interest/](https://www.geeksforgeeks.org/program-find-simple-interest/)

**什么是“单利”？**
简单利息是一种快速计算贷款利息的方法。单利是通过每日利率乘以本金再乘以两次付款之间的天数来确定的。
**单利公式:**

> 单利公式为:
> 单利=(P×T×R)/100
> 其中，
> P 为本金金额
> T 为时间，
> R 为利率

**例:**

```
EXAMPLE1:
Input : P = 10000
        R = 5
        T = 5
Output :2500
We need to find simple interest on 
Rs. 10,000 at the rate of 5% for 5 
units of time.

EXAMPLE2:
Input : P = 3000
        R = 7
        T = 1
Output :210
```

计算单利的公式为:单利= (P * T * R) / 100 其中 P 为本金，T 为时间& R 为利率。

## C++

```
// CPP program to find simple interest for
// given principal amount, time and rate of
// interest.
#include<iostream>
using namespace std;
int main()
{
    // We can change values here for
    // different inputs
    float P = 1, R = 1, T = 1;

    /* Calculate simple interest */
    float SI = (P * T * R) / 100;

    /* Print the resultant value of SI */
    cout << "Simple Interest = " << SI;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple JAVA program to compute
// simple interest for given principal
// amount, time and rate of interest.
import java.io.*;

class GFG
{
    public static void main(String args[])
    {  
        // We can change values here for
        // different inputs
        float P = 1, R = 1, T = 1;

        /* Calculate simple interest */
        float SI = (P * T * R) / 100;
        System.out.println("Simple interest = "+ SI);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find simple interest
# for given principal amount, time and
# rate of interest.

# We can change values here for
# different inputs
P = 1
R = 1
T = 1

# Calculates simple interest
SI = (P * R * T) / 100

# Print the resultant value of SI
print("simple interest is", SI)

# This code is contributed by Azkia Anam.
```

## C#

```
// A Simple C# program to compute
// simple interest for given principal
// amount, time and rate of interest.
using System;

class GFG {

    // Driver Code
    public static void Main()
    {

        // We can change values here for
        // different inputs
        float P = 1, R = 1, T = 1;

        // Calculate simple interest
        float SI = (P * T * R) / 100;
        Console.Write("Simple interest = "+ SI);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find simple interest
// for given principal amount, time
// and rate of interest.

// We can change values here for
// different inputs
$P = 1;
$R = 1;
$T = 1;

/* Calculate simple interest */
$SI = ($P * $T * $R) / 100;

/* Print the resultant value of SI */
echo "Simple Interest = ". $SI;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript program to find simple interest for
// given principal amount, time and rate of
// interest.

    // We can change values here for
    // different inputs
    let P = 1, R = 1, T = 1;

    /* Calculate simple interest */
    let SI = (P * T * R) / 100;

    /* Print the resultant value of SI */
    document.write("Simple Interest = " + SI);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
Simple Interest : 0.01
```

本文由 **Anurag Rawat** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。