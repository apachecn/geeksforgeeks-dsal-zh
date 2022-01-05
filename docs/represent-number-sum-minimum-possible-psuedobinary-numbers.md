# 将一个数表示为最小可能伪二进制数的和

> 原文:[https://www . geesforgeks . org/represent-number-sum-minimum-psuedobinary-numbers/](https://www.geeksforgeeks.org/represent-number-sum-minimum-possible-psuedobinary-numbers/)

给定一个数，你必须将这个数表示为可能的最小数量*伪二进制*数之和。如果一个数的十进制数只由两位数(0 和 1)组成，则称其为*伪二进制*数。例如:11，10，101 都是伪二进制数。
**例:-**

```
Input : 44
Output : 11 11 11 11

Explanation : 44 can be represented as sum of 
minimum 4 psuedobinary numbers as 11+11+11+11  

Input : 31
Output : 11 10 10

Explanation : 31 can be represented as sum of
minimum 3 psuedobinary numbers as 11+10+10  
```

这样做的想法是首先仔细观察我们需要计算可能的伪二进制数的最小数量。为此，我们找到一个新的数字 m，这样，如果给定数字 n 中的某个位置的数字不为零，那么 m 中该位置的数字为 1，否则为零。例如，如果 n = 5102，那么 m 将是 1101。然后我们将打印这个数字 m，并从 n 中减去 m。我们将继续重复这些步骤，直到 n 大于零。

## C++

```
// C++ program to represent a given
// number as sum of minimum possible
// psuedobinary numbers
#include<iostream>
using namespace std;

// function to represent a given
// number as sum of minimum possible
// psuedobinary numbers
void psuedoBinary(int n)
{
    // Repeat below steps until n > 0
    while (n > 0)
    {                
        // calculate m (A number that has same
        // number of digits as n, but has 1 in
        // place of non-zero digits 0 in place
        // of 0 digits)
        int temp = n, m = 0, p = 1;
        while (temp)
        {
            int rem = temp % 10;
            temp = temp / 10;

            if (rem != 0)
                m += p;

            p *= 10;
        }

        cout << m << " ";

        // subtract m from n
        n = n - m;
    }
}

// Driver code
int main()
{
    int n = 31;

    psuedoBinary(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to represent a given
// number as sum of minimum possible
// psuedobinary numbers

import java.util.*;
import java.lang.*;

class GFG
{
    public static void psuedoBinary(int n)
    {
        // Repeat below steps until n > 0
        while (n != 0)
        {
            // calculate m (A number that has same
            // number of digits as n, but has 1 in
            // place of non-zero digits 0 in place
            // of 0 digits)
            int temp = n, m = 0, p = 1;
            while(temp != 0)
            {
                int rem = temp % 10;
                temp = temp / 10;

                if (rem != 0)
                    m += p;

                p *= 10;
            }

            System.out.print(m + " ");

            // subtract m from n
            n = n - m;
        }
        System.out.println(" ");
    }

// Driver code
public static void main(String[] args)
    {
        int n = 31;
        psuedoBinary(n);
    }
}

// This code is contributed by Mohit Gupta_OMG
```

## 蟒蛇 3

```
# Python3 program to represent
# a given number as sum of
# minimum possible psuedobinary
# numbers

# function to represent a
# given number as sum of
# minimum possible
# psuedobinary numbers
def psuedoBinary(n):

    # Repeat below steps
    # until n > 0
    while (n > 0):

        # calculate m (A number
        # that has same number
        # of digits as n, but
        # has 1 in place of non-zero
        # digits 0 in place of 0 digits)
        temp = n;
        m = 0;
        p = 1;
        while (temp):
            rem = temp % 10;
            temp = int(temp / 10);

            if (rem != 0):
                m += p;
            p *= 10;

        print(m,end=" ");

        # subtract m from n
        n = n - m;

# Driver code
n = 31;
psuedoBinary(n);

# This code is contributed
# by mits.
```

## C#

```
// C# program to represent a given
// number as sum of minimum possible
// psuedobinary numbers

using System;

class GFG
{
    public static void psuedoBinary(int n)
    {
        // Repeat below steps until n > 0
        while (n != 0)
        {
            // calculate m (A number that has same
            // number of digits as n, but has 1 in
            // place of non-zero digits 0 in place
            // of 0 digits)
            int temp = n, m = 0, p = 1;
            while(temp != 0)
            {
                int rem = temp % 10;
                temp = temp / 10;

                if (rem != 0)
                    m += p;

                p *= 10;
            }

            Console.Write(m + " ");

            // subtract m from n
            n = n - m;
        }
        Console.Write(" ");
    }

// Driver code
public static void Main()
    {
        int n = 31;
        psuedoBinary(n);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to represent a
// given number as sum of minimum
// possible psuedobinary numbers

// Function to represent a
// given number as sum of minimum
// possible psuedobinary numbers
function psuedoBinary($n)
{
    // Repeat below steps until n > 0
    while ($n > 0)
    {                
        // calculate m (A number
        // that has same number of
        // digits as n, but has 1
        // in place of non-zero
        // digits 0 in place of 0
        // digits)
        $temp = $n; $m = 0; $p = 1;
        while ($temp)
        {
            $rem = $temp % 10;
            $temp = $temp / 10;

            if ($rem != 0)
                $m += $p;

            $p *= 10;
        }

        echo $m , " ";

        // subtract m from n
        $n = $n - $m;
    }
}

// Driver code
$n = 31;
psuedoBinary($n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to represent a given
// number as sum of minimum possible
// psuedobinary numbers   

function psuedoBinary( n)
{
        // Repeat below steps until n > 0
        while (n != 0)
        {
            // calculate m (A number that has same
            // number of digits as n, but has 1 in
            // place of non-zero digits 0 in place
            // of 0 digits)
            var temp = n, m = 0, p = 1;
            while (temp != 0) {
                var rem = temp % 10;
                temp = parseInt(temp / 10);

                if (rem != 0)
                    m += p;

                p *= 10;
            }

            document.write(m + " ");

            // subtract m from n
            n = n - m;
        }
        document.write(" ");
    }

    // Driver code

        var n = 31;
        psuedoBinary(n);

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
11 10 10
```

**时间复杂度** : O( log n )
**辅助空间** : O(1)
本文由 **Harsh Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。