# 求给定数列第 n 行所有项的和

> 原文:[https://www . geesforgeks . org/find-sum-terms-n-th-row-given-series/](https://www.geeksforgeeks.org/find-sum-terms-n-th-row-given-series/)

求下面给出的数列的第**n**行中所有项的和。

```
               1  2
            3  4  5  6
         7  8  9 10 11 12
     13 14 15 16 17 18 19 20
    ..........................
   ............................
             (so on)
```

**例:**

```
Input : n = 2
Output : 18
terms in 2nd row and their sum
sum = (3 + 4 + 5 + 6) = 18

Input : n = 4
Output : 132
```

**天真方法:**使用两个循环。外环执行 **i = 1 到 n** 次。内部循环执行 **j = 1 到 2 * i** 次。计数器变量 **k** 以跟踪系列中的当前术语。当 **i = n** 时， **k** 的值相加。
时间复杂度:O(k)，其中 k 是从第 n 行开始到结束的总项数。
**有效方法:**第**n 行**中所有项的和可以通过公式:
得到

```
 Sum(n) = n * (2 * n<sup>2 + 1)</sup>
```

公式证明如下:
**前提:**

1.  以 **a** 为第一项，以 **d** 为公共差的等差数列的 **n** 项之和给出为:

```
   Sum = (n * [2*a + (n-1)*d]) / 2
```

2.  第 1 个 **n 个**自然数之和为:

```
   Sum = (n * (n + 1)) / 2
```

**证明:**

```
Let the number of terms from the beginning 
till the end of the nth row be p.
Here p = 2 + 4 + 6 + .....n terms
For the given AP series, a = 2, d = 2.
Using the above formula for the sum of
n terms of the AP series, we get,

     p = n * (n + 1)

Similarly, let the number of terms from the 
beginning till the end of the (n-1)th row be q.
Here q = 2 + 4 + 6 + .....n-1 terms
For the given AP series, a = 2, d = 2.
Using the above formula for the sum of
n-1 terms of the AP series, we get,

     q = n * (n - 1)

Now,
Sum of all the terms in the nth row 
           = sum of 1st p natural numbers - 
             sum of 1st q natural numbers

           = (p * (p + 1)) / 2 - (q * (q + 1)) / 2

Substituting the values of p and q and then solving
the equation, we will get,

Sum of all the terms in the nth row = n * (2 * n<sup>2 + 1)</sup>
```

## C++

```
// C++ implementation to find the sum of all the
// terms in the nth row of the given series
#include <bits/stdc++.h>

using namespace std;

// function to find the required sum
int sumOfTermsInNthRow(int n)
{
    // sum = n * (2 * n^2 + 1)
    int sum = n * (2 * pow(n, 2) + 1);
    return sum;
}

// Driver program to test above
int main()
{
    int n = 4;
    cout << "Sum of all the terms in nth row = "
         << sumOfTermsInNthRow(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum of all the
// terms in the nth row of the given series

import static java.lang.Math.pow;

class Test {
    // method to find the required sum
    static int sumOfTermsInNthRow(int n)
    {
        // sum = n * (2 * n^2 + 1)
        int sum = (int)(n * (2 * pow(n, 2) + 1));
        return sum;
    }

    // Driver method
    public static void main(String args[])
    {
        int n = 4;
        System.out.println("Sum of all the terms in nth row = "
                           + sumOfTermsInNthRow(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to find
# the sum of all the terms in the
# nth row of the given series
from math import pow

# function to find the required sum
def sumOfTermsInNthRow(n):

    # sum = n * (2 * n^2 + 1)
    sum = n * (2 * pow(n, 2) + 1)
    return sum

# Driver Code
if __name__ == '__main__':
    n = 4
    print("Sum of all the terms in nth row =",
                   int(sumOfTermsInNthRow(n)))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# implementation to find the sum of all the
// terms in the nth row of the given series
using System;

class Test {
    // method to find the required sum
    static int sumOfTermsInNthRow(int n)
    {
        // sum = n * (2 * n^2 + 1)
        int sum = (int)(n * (2 * Math.Pow(n, 2) + 1));
        return sum;
    }

    // Driver method
    public static void Main()
    {
        int n = 4;
        Console.Write("Sum of all the terms in nth row = "
                      + sumOfTermsInNthRow(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the sum of all the terms in
// the nth row of the given series

// function to find the required sum
function sumOfTermsInNthRow($n)
{

    // sum = n * (2 * n^2 + 1)
    $sum = $n * (2 * pow($n, 2) + 1);
    return $sum;
}

    // Driver Code
    $n = 4;
    echo "Sum of all the terms in nth row = ",
                        sumOfTermsInNthRow($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript implementation to find the sum of all the
// terms in the nth row of the given series

// function to find the required sum
function sumOfTermsInNthRow( n)
{

    // sum = n * (2 * n^2 + 1)
    let sum = n * (2 * Math.pow(n, 2) + 1);
    return sum;
}

// Driver program to test above

    let n = 4;
    document.write( "Sum of all the terms in nth row = "
         + sumOfTermsInNthRow(n));

// This code is contributed by aashish1995

</script>
```

输出:

```
Sum of all the terms in nth row = 132
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。