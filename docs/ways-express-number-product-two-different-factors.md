# 将一个数表示为两个不同因素的乘积的方法

> 原文:[https://www . geesforgeks . org/way-express-number-product-two-differential-factors/](https://www.geeksforgeeks.org/ways-express-number-product-two-different-factors/)

给定一个数 n，编写一个程序来计算数可以表示为两个不同因子的乘积的方式数。

**示例:**

```
Input : 12
Output : 3
12 can be expressed as 1 * 12, 2 * 6 and 3*4\. 

Input : 36
Output : 4
36 can be expressed as 1 * 36, 2 * 18, 3 * 12 and 4 * 9.
```

```
All factors of 12 are = 1, 2, 3, 4, 6, 12

We can observe that factors always exist in
pair which is equal to number.

Here (1, 12), (2, 6) and (3, 4) are such pairs.
```

由于一个数可以表示为两个因子的乘积，我们只需要求出数的因子数，直到数的平方根。我们只需要找到不同的对，所以在完美正方形的情况下，我们不包括这个因素。

## C++

```
// CPP program to find number of ways
// in which number expressed as
// product of two different factors
#include <bits/stdc++.h>
using namespace std;

// To count number of ways in which
// number expressed as product
// of two different numbers
int countWays(int n)
{
    // To store count of such pairs
    int count = 0;

    // Counting number of pairs
    // upto sqrt(n) - 1
    for (int i = 1; i * i < n; i++)
        if (n % i == 0)
            count++;

    // To return count of pairs
    return count;
}

// Driver program to test countWays()
int main()
{
    int n = 12;
    cout << countWays(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways
// in which number expressed as
// product of two different factors
public class Main {

    // To count number of ways in which
    // number expressed as product
    // of two different numbers
    static int countWays(int n)
    {
        // To store count of such pairs
        int count = 0;

        // Counting number of pairs
        // upto sqrt(n) - 1
        for (int i = 1; i * i < n; i++)
            if (n % i == 0)
                count++;

        // To return count of pairs
        return count;
    }

    // Driver program to test countWays()
    public static void main(String[] args)
    {
        int n = 12;
        System.out.println(countWays(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find number of ways
# in which number expressed as
# product of two different factors

# To count number of ways in which
# number expressed as product
# of two different numbers
def countWays(n):

    # To store count of such pairs
    count = 0
    i = 1

    # Counting number of pairs
    # upto sqrt(n) - 1
    while ((i * i)<n) :
        if(n % i == 0):
            count += 1   
        i += 1

    # To return count of pairs
    return count

# Driver program to test countWays()
n = 12
print (countWays(n))

# This code is contributed
# by Azkia Anam.
```

## C#

```
// C# program to find number of ways
// in which number expressed as
// product of two different factors
using System;

public class main {

    // To count number of ways in which
    // number expressed as product
    // of two different numbers
    static int countWays(int n)
    {

        // To store count of such pairs
        int count = 0;

        // Counting number of pairs
        // upto sqrt(n) - 1
        for (int i = 1; i * i < n; i++)
            if (n % i == 0)
                count++;

        // To return count of pairs
        return count;
    }

    // Driver program to test countWays()
    public static void Main()
    {
        int n = 12;

        Console.WriteLine(countWays(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of ways
// in which number expressed as
// product of two different factors

// To count number of ways in which
// number expressed as product
// of two different numbers
function countWays($n)
{
    // To store count of such pairs
    $count = 0;

    // Counting number of pairs
    // upto sqrt(n) - 1
    for ($i = 1; $i * $i < $n; $i++)
        if ($n % $i == 0)
            $count++;

    // To return count of pairs
    return $count;
}

// Driver Code
$n = 12;
echo countWays($n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to find number of ways
// in which number expressed as
// product of two different factors

    // To count number of ways in which
    // number expressed as product
    // of two different numbers
    function countWays(n)
    {
        // To store count of such pairs
        let count = 0;

        // Counting number of pairs
        // upto sqrt(n) - 1
        for (let i = 1; i * i < n; i++)
            if (n % i == 0)
                count++;

        // To return count of pairs
        return count;
    }

// Driver Code

    let n = 12;
    document.write(countWays(n));

</script>
```

**输出:**

```
3
```

本文由 [**核素**](https://auth.geeksforgeeks.org/profile.php?user=nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。