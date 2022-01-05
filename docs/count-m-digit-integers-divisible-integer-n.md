# 可被整数 n 整除的 m 位整数的计数

> 原文:[https://www . geesforgeks . org/count-m-digits-integers-整除-integer-n/](https://www.geeksforgeeks.org/count-m-digit-integers-divisible-integer-n/)

给定两个数字 m 和 n，计算可被 n 整除的 m 位数的个数
示例:

```
Input : m = 2 
        n = 6
Output : 15
Two digit numbers that are divisible by 6
are 12, 18, 24, 30, 36, ....., 96.

Input : m = 3 
        n = 5
Output :180
```

一个**简单的解决方法**就是两次尝试所有 m 位数。对于每个数字，检查它是否可以被 n 整除。如果可以，我们增加计数。
一个**高效的解决方案**包括以下步骤。
这个想法是基于这样一个事实:从第一个可除数开始，每第 n 个数都可以被 n 整除。

1.  找到最大的 m 位数。
2.  找到最大的 m-1 位数。
3.  将两个数除以 n，然后从前面减去。

下面是以上步骤的实现。

## C++

```
// C++ program to count m digit numbers having
// n as divisor.
#include<bits/stdc++.h>
using namespace std;

// Returns count of m digit numbers having n
// as divisor
int findCount(int m, int n)
{   
    // generating largest number of m digit
    int num1 = 0;
    for (int i = 0; i < m; i++)
        num1 = (num1 * 10) + 9;

    // generating largest number of m-1 digit
    int num2 = 0;
    for (int i = 0; i < (m - 1); i++)
        num2 = (num2 * 10) + 9;

    // returning number of dividend
    return ((num1 / n) - (num2 / n));
}

// Driver code
int main()
{
    int m = 2, n = 6;
    printf("%d\n", findCount(m, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count m digit numbers having
// n as divisor.

class Main
{
    // Returns count of m digit numbers having n
    // as divisor
    static int findCount(int m, int n)
    {   
        // generating largest number of m digit
        int num1 = 0;
        for (int i = 0; i < m; i++)
            num1 = (num1 * 10) + 9;

        // generating largest number of m-1 digit
        int num2 = 0;
        for (int i = 0; i < (m - 1); i++)
            num2 = (num2 * 10) + 9;

        // returning number of dividend
        return ((num1 / n) - (num2 / n));
    }

    // main function
    public static void main (String[] args)
    {
        int m = 2, n = 6;
        System.out.println(findCount(m, n));
    }
}

/* This code is contributed by Harsh Agarwal */
```

## 蟒蛇 3

```
# Python3 program to count m digit
# numbers having n as divisor.

# Returns count of m digit
# numbers having n as divisor
def findCount(m, n):

    # Generating largest number of m digit
    num1 = 0

    for i in range(0, m):
        num1 = (num1 * 10) + 9

    # Generating largest number of m-1 digit
    num2 = 0

    for i in range(0, (m - 1)):
        num2 = (num2 * 10) + 9

    # returning number of dividend
    return int((num1 / n) - (num2 / n))

# Driver code
m = 2; n = 6
print(findCount(m, n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to count m digit numbers
// having n as divisor.
using System;

class GfG {

    // Returns count of m digit numbers
    // having n as divisor
    static int findCount(int m, int n)
    {

        // generating largest number
        // of m digit
        int num1 = 0;
        for (int i = 0; i < m; i++)
            num1 = (num1 * 10) + 9;

        // generating largest number
        // of m-1 digit
        int num2 = 0;
        for (int i = 0; i < (m - 1); i++)
            num2 = (num2 * 10) + 9;

        // returning number of dividend
        return ((num1 / n) - (num2 / n));
    }

    // main function
    public static void Main ()
    {
        int m = 2, n = 6;

        Console.Write(findCount(m, n));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count m digit
// numbers having n as divisor.

// Returns count of m digit numbers
// having n as divisor
function findCount($m, $n)
{
    // generating largest number
    // of m digit
    $num1 = 0;
    for ($i = 0; $i < $m; $i++)
        $num1 = ($num1 * 10) + 9;

    // generating largest number
    // of m-1 digit
    $num2 = 0;
    for ($i = 0; $i < ($m - 1); $i++)
        $num2 = ($num2 * 10) + 9;

    // returning number of dividend
    return (($num1 / $n) - ($num2 / $n));
}

// Driver code
$m = 2; $n = 6;
echo findCount($m, $n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to count m digit
// numbers having n as divisor.

// Returns count of m digit numbers
// having n as divisor
function findCount(m, n)
{

    // generating largest number
    // of m digit
    let num1 = 0;
    for (let i = 0; i < m; i++)
        num1 = (num1 * 10) + 9;

    // generating largest number
    // of m-1 digit
    let num2 = 0;
    for (let i = 0; i < (m - 1); i++)
        num2 = (num2 * 10) + 9;

    // returning number of dividend
    return ((num1 / n) - (num2 / n));
}

// Driver code
let m = 2; n = 6;
document.write(findCount(m, n) + "<br>");

// This code is contributed by gfgking
</script>
```

输出:

```

15
```

时间复杂度:O(m)
本文由[阿迪亚库马尔](https://www.linkedin.com/in/aditya-kumar-837315100/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。