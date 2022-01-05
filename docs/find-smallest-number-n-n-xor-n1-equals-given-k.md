# 求最小数 n，使 n 异或 n+1 等于给定 k

> 原文:[https://www . geesforgeks . org/find-minist-number-n-xor-n1-equals-given-k/](https://www.geeksforgeeks.org/find-smallest-number-n-n-xor-n1-equals-given-k/)

给你一个正数 k，我们需要找到一个正整数 n，这样 n 和 n+1 的异或等于 k，如果不存在这样的 n，那么打印-1。
示例:

```
Input : 3
Output : 1

Input : 7
Output : 3

Input : 6
Output : -1
```

下面是我们对一个数 n 做 n 异或(n+1)的两种情况
T1】情况 1 : n 为偶数。n 的最后一位是 0，(n+1)的最后一位是 1。其余位在两者中都是相同的。所以如果 n 是偶数，异或总是 1。
**案例:n 为奇数**n 的最后一位为 1。在 n+1 中，最后一位是 0。但是在这种情况下，可能会有更多的位因进位而不同。进位继续向左传播，直到我们找到第一个 0 位。所以 n XOR n+1 将得到 2^i-1，其中 I 是从左数 n 中第一个 0 位的位置。所以，我们可以说，如果 k 是 2^i-1 的形式，那么我们的答案就是 k/2。
最后我们的步骤是:

```
If we have k=1, answer = 2 [We need smallest positive n]
Else If k is of form 2^i-1, answer = k/2,
else, answer = -1
```

## C++

```
// CPP to find n such that XOR of n and n+1
// is equals to given n
#include <bits/stdc++.h>
using namespace std;

// function to return the required n
int xorCalc(int k)
{
    if (k == 1)
        return 2;

    // if k is of form 2^i-1
    if (((k + 1) & k) == 0)
        return k / 2;

    return -1;
}

// driver program
int main()
{
    int k = 31;
    cout << xorCalc(k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to find n such that XOR of n and n+1
// is equals to given n
class GFG
{

    // function to return the required n
    static int xorCalc(int k)
    {
        if (k == 1)
            return 2;

        // if k is of form 2^i-1
        if (((k + 1) & k) == 0)
            return k / 2;

        return 1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int k = 31;

        System.out.println(xorCalc(k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python to find n such that
# XOR of n and n+1 is equals
# to given n

# function to return the
# required n
def xorCalc(k):
    if (k == 1):
        return 2

    # if k is of form 2^i-1
    if (((k + 1) & k) == 0):
        return k / 2

    return 1;

# driver program
k = 31
print(int(xorCalc(k)))

# This code is contributed
# by Sam007
```

## C#

```
// C# to find n such that XOR
// of n and n+1 is equals to
// given n
using System;

class GFG
{

    // function to return the required
    // n
    static int xorCalc(int k)
    {
        if (k == 1)
            return 2;

        // if k is of form 2^i-1
        if (((k + 1) & k) == 0)
            return k / 2;

        return 1;
    }

    // Driver code
    public static void Main ()
    {
        int k = 31;

        Console.WriteLine(xorCalc(k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find n such
// that XOR of n and n+1
// is equals to given n

// function to return
// the required n
function xorCalc($k)
{
    if ($k == 1)
        return 2;

    // if k is of form 2^i-1
    if ((($k + 1) & $k) == 0)
        return floor($k / 2);

    return 1;
}

// Driver Code
$k = 31;
echo xorCalc($k);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript to find n such that XOR of n and n+1
// is equals to given n

// function to return the required n
function xorCalc(k)
{
    if (k == 1)
        return 2;

    // if k is of form 2^i-1
    if (((k + 1) & k) == 0)
        return parseInt(k / 2);

    return 1;
}

// driver program
var k = 31;
document.write( xorCalc(k));

// This code is contributed by itsok.
</script>
```

输出:

```
15
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。