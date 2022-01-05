# 使用最小给定操作数将数字 m 转换为 n

> 原文:[https://www . geesforgeks . org/convert-number-m-n-using-minimum-number-给定-operations/](https://www.geeksforgeeks.org/convert-number-m-n-using-minimum-number-given-operations/)

用最少的运算把 m 转换成 n。允许的操作有:

1.  乘以 2，即 do m = 2 * m
2.  减去 1，即做 m = m–1

如果无法转换，打印-1。
**例:**

```
Input : m = 3, n = 11
Output : 3
1st operation: *2 = 3*2 = 6
2nd operation: *2 = 6*2 = 12
3rd operation: -1 = 12-1 = 11

Input : m = 15, n = 20
Output : 6
1st operation: -1 '5' times = 15 + (-1*5) = 10
2nd operation: *2 = 10*2 = 20

Input : m = 0, n = 8
Output : -1
Using the given set of operations 'm' 
cannot be converted to 'n'

Input : m = 12, n = 8
Output : 4
```

这个想法基于以下事实。
1)如果 m 小于 0，n 大于 0，则不可能。
2)如果 m 大于 n，那么我们只需要减法就可以达到 n。
3)否则(m 小于 n)，我们必须做 m*2 运算。出现以下两种情况。
……a)如果 n 是奇数，我们必须做-1 运算才能到达。
……b)如果 n 是偶数，我们必须做*2 运算才能达到。
**算法:**

```
int convert(m,n)
    if (m == n) 
    return 0;

    // not possible
    if (m <= 0 && n > 0)  
    return -1;

    // m is greater than n
    if (m > n) 
        return m-n;

    // n is odd
    if (n % 2 == 1) 
    // perform '-1' 
    return 1 + convert(m, n+1);

    // n is even
    else 
    // perform '*2' 
    return 1 + convert(m, n/2);
```

**注意:**如此生成的操作列表应该以相反的顺序应用。
例如:

```
m = 3, n = 11
                convert(3,11)
                     |       --> n is odd:   operation '-1'
                convert(3,12) 
                     |       --> n is even:  operation '*2' 
                convert(3,6)
                     |       --> n is even:  operation '*2' 
                convert(3,3) 
                     |       --> m == n
                   return 
Therefore, the sequence of operations is '*2', '*2', '-1'.
```

## C++

```
// C++ implementation to convert
// a number m to n using minimum
// number of given operations
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum
// number of given operations
// to convert m to n
int convert(int m, int n)
{
    if (m == n)
        return 0;

    // only way is to do
    // -1 (m - n) times
    if (m > n)
        return m - n;

    // not possible
    if (m <= 0 && n > 0)
        return -1;

    // n is greater and n is odd
    if (n % 2 == 1)

        // perform '-1' on m
        // (or +1 on n)
        return 1 + convert(m, n + 1);

    // n is even
    else
        // perform '*2' on m
        // (or n/2 on n)
        return 1 + convert(m, n / 2);
}

// Driver code
int main()
{
    int m = 3, n = 11;
    cout << "Minimum number of operations : "
         << convert(m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to convert
// a number m to n using minimum
// number of given operations

class ConvertNum
{
    // function to find minimum
    // number of given operations
    // to convert m to n
    static int convert(int m, int n)
    {
        if (m == n)
            return 0;

        // only way is to do
        // -1 (m - n) times
        if (m > n)
            return m - n;

        // not possible
        if (m <= 0 && n > 0)
            return -1;

        // n is greater and n is odd
        if (n % 2 == 1)

            // perform '-1' on m
            // (or +1 on n)
            return 1 + convert(m, n + 1);

        // n is even
        else
            // perform '*2' on m
            // (or n / 2 on n)
            return 1 + convert(m, n / 2);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int m = 3, n = 11;
        System.out.println("Minimum number of " +
                                "operations : " +
                                  convert(m, n));
    }
}
```

## 蟒蛇 3

```
# Python implementation to convert
# a number m to n using minimum
# number of given operations

# Function to find minimum
# number of given operations
# to convert m to n
def conver(m, n):

    if(m == n):
        return 0

    # only way is to do
    # -1(m - n): times
    if(m > n):
        return m - n

    # not possible
    if(m <= 0 and n > 0):
        return -1

    # n is greater and n is odd
    if(n % 2 == 1):

        # perform '-1' on m
        #(or +1 on n):
        return 1 + conver(m, n + 1)

    # n is even
    else:

        # perform '*2' on m
        #(or n/2 on n):
        return 1 + conver(m, n / 2)

# Driver code
m = 3
n = 11
print("Minimum number of operations :",
                          conver(m, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation to convert
// a number m to n using minimum
// number of given operations
using System;

class GFG
{
    // function to find minimum
    // number of given operations
    // to convert m to n
    static int convert(int m, int n)
    {
        if (m == n)
            return 0;

        // only way is to do
        // -1 (m - n) times
        if (m > n)
            return m - n;

        // not possible
        if (m <= 0 && n > 0)
            return -1;

        // n is greater and n is odd
        if (n % 2 == 1)

            // perform '-1' on m
            // (or +1 on n)
            return 1 + convert(m, n + 1);

        // n is even
        else
            // perform '*2' on m
            // (or n / 2 on n)
            return 1 + convert(m, n / 2);
    }

    // Driver code
    public static void Main ()
    {
        int m = 3, n = 11;
        Console.Write("Minimum number of " +
                           "operations : " +
                             convert(m, n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to convert
// a number m to n using minimum
// number of given operations

// Function to find minimum
// number of given operations
// to convert m to n
function convert($m, $n)
{
    if ($m == $n)
        return 0;

    // only way is to do
    // -1 (m - n) times
    if ($m > $n)
        return $m - $n;

    // not possible
    if ($m <= 0 && $n > 0)
        return -1;

    // n is greater and n is odd
    if ($n % 2 == 1)

        // perform '-1' on m
        // (or +1 on n)
        return 1 + convert($m, $n + 1);

    // n is even
    else
        // perform '*2' on m
        // (or n/2 on n)
        return 1 + convert($m, $n / 2);
}

// Driver code
{
    $m = 3; $n = 11;
    echo "Minimum number of ".
              "operations : ",
              convert($m, $n);
    return 0;
}    

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript implementation to convert
// a number m to n using minimum
// number of given operations

// function to find minimum
// number of given operations
// to convert m to n
function convert(m , n)
{
    if (m == n)
        return 0;

    // only way is to do
    // -1 (m - n) times
    if (m > n)
        return m - n;

    // not possible
    if (m <= 0 && n > 0)
        return -1;

    // n is greater and n is odd
    if (n % 2 == 1)

        // perform '-1' on m
        // (or +1 on n)
        return 1 + convert(m, n + 1);

    // n is even
    else
        // perform '*2' on m
        // (or n / 2 on n)
        return 1 + convert(m, n / 2);
}

// Driver Code
var m = 3, n = 11;
document.write("Minimum number of " +
                        "operations : " +
                          convert(m, n));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
Minimum number of operations : 3
```

参考文献:
[http://tech . queryhome . com/112705/convert-number-with-minimum-operations-operations-allowed](http://tech.queryhome.com/112705/convert-number-with-minimum-operations-operations-allowed)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。