# 找到一个数字 x，使得 x 和它的数字之和等于给定的 n。

> 原文:[https://www . geesforgeks . org/find-number-x-sum-x-digits-equal-given-n/](https://www.geeksforgeeks.org/find-number-x-sum-x-digits-equal-given-n/)

给定一个正数 n .我们需要找到一个数 x，使得 x 对其本身的位数之和等于 n.
如果没有这样的 x 是可能的，打印-1。
**例:**

```
Input : n = 21
Output : x = 15
Explanation : x + its digit sum = 15 + 1 + 5 = 21 

Input : n = 5
Output : -1
```

我们从 1 迭代到 n，对于每个中间数，x 找到它的数字和，然后加到 x 上，如果等于 n，那么 x 就是我们需要的答案。

```
    // iterate from 1 to n. For every no.
    // check if its digit sum with it is
    // equal to n.
    for (int i = 0; i <= n; i++)
        if (i + digSum(i)  == n)
            return i;

    return -1;
```

## C++

```
// CPP program to find x such that x +
// digSum(x) is equal to n.
#include <bits/stdc++.h>
using namespace std;

// utility function for digit sum
int digSum(int n)
{
    int sum = 0, rem = 0;
    while (n) {
        rem = n % 10;
        sum += rem;
        n /= 10;
    }
    return sum;
}

// function for finding x
int findX(int n)
{
    // iterate from 1 to n. For every no.
    // check if its digit sum with it is
    // equal to n.
    for (int i = 0; i <= n; i++)
        if (i + digSum(i) == n)
            return i;

    // if no such i found return -1
    return -1;
}

// driver function
int main()
{
    int n = 43;
    cout << "x = " << findX(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find x such that x +
// digSum(x) is equal to n.
class GFG
{

    // utility function for digit sum
    static int digSum(int n)
    {
        int sum = 0, rem = 0;

        while (n>0) {
            rem = n % 10;
            sum += rem;
            n /= 10;
        }

        return sum;
    }

    // function for finding x
    static int findX(int n)
    {

        // iterate from 1 to n. For every no.
        // check if its digit sum with it is
        // equal to n.
        for (int i = 0; i <= n; i++)
            if (i + digSum(i) == n)
                return i;

        // if no such i found return -1
        return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 43;

        System.out.println("x = "+findX(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# x such that dx + igSum(x)
# is equal to n.

# utility function
# for digit sum
def digSum(n):
    sum = 0;
    rem = 0;
    while(n):
        rem = n % 10;
        sum = sum + rem;
        n = int(n / 10);
    return sum;

# function for finding x
def findX(n):

    # iterate from 1 to n.
    # For every no.
    # check if its digit
    # sum with it is# equal to n.
    for i in range(n + 1):
        if (i + digSum(i) == n):
            return i;

    # if no such i
    # found return -1
    return -1;

# Driver Code
n = 43;
print("x = ", findX(n));

# This code is contributed by mits
```

## C#

```
// C# program to find x such that
// x + digSum(x) is equal to n.
using System;

class GFG {

    // utility function for digit sum
    static int digSum(int n)
    {
        int sum = 0, rem = 0;

        while (n > 0)
        {
            rem = n % 10;
            sum += rem;
            n /= 10;
        }

        return sum;
    }

    // function for finding x
    static int findX(int n)
    {

        // iterate from 1 to n. For every no.
        // check if its digit sum with it is
        // equal to n.
        for (int i = 0; i <= n; i++)
            if (i + digSum(i) == n)
                return i;

        // if no such i found return -1
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int n = 43;

        Console.Write("x = " + findX(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find x such that
// dx + igSum(x) is equal to n.

// utility function
// for digit sum
function digSum($n)
{
    $sum = 0; $rem = 0;
    while ($n)
    {
        $rem = $n % 10;
        $sum += $rem;
        $n /= 10;
    }
    return $sum;
}

// function for finding x
function findX($n)
{

    // iterate from 1 to n.
    // For every no.
    // check if its digit
    // sum with it is
    // equal to n.
    for ($i = 0; $i <= $n; $i++)
        if ($i + digSum($i) == $n)
            return $i;

    // if no such i
    // found return -1
    return -1;
}

    // Driver Code
    $n = 43;
    echo "x = " , findX($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program to find x such that x +
// digSum(x) is equal to n.

    // utility function for digit sum
    function digSum(n)
    {
        let sum = 0, rem = 0;

        while (n>0) {
            rem = n % 10;
            sum += rem;
            n = Math.floor(n / 10);
        }

        return sum;
    }

    // function for finding x
    function findX(n)
    {

        // iterate from 1 to n. For every no.
        // check if its digit sum with it is
        // equal to n.
        for (let i = 0; i <= n; i++)
            if (i + digSum(i) == n)
                return i;

        // if no such i found return -1
        return -1;
    }

// driver program

    let n = 43;

    document.write("x = "+findX(n));

</script>
```

**输出:**

```
x = 35
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://auth.geeksforgeeks.org/profile.php?user=ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。