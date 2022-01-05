# 在循环游中返回起点的最少步数

> 原文:[https://www . geeksforgeeks . org/最少返回原地的步骤循环游/](https://www.geeksforgeeks.org/minimum-steps-to-come-back-to-origin-in-a-circular-tour/)

考虑有 n 个标记为 1，2，…n 的点的圆形轨迹。一个人最初被放置在点 k 上。这个人移动 m > 0，在每一步向前(以圆形方式)开槽。找到所需的最小步数，使人到达起始点 k.
**示例:**

```
Input : n = 9, k = 2, m = 6 
Output : 3
Explanation : Sequence of moves is
 2 => 8 => 5 => 2

Input : n = 6, k = 3, m = 2 
Output : 3
```

**天真方法:**用“k”和“count”= 0 初始化计数器“I”。此外，对于每次迭代增量“计数”，将“m”添加到“I”。取其模数 n，即 **i=((i+m)%n)** ，如果 i > n，如果 I 等于 k，那么计数就是我们的答案。
**时间复杂度:** O(n)。
**有效途径:**我们找到 GCD(n，m)，然后用 GCD(n，m)除 n。这将是我们的答案。这可以解释为:
现在按照问题来思考 n 和 m，因为我们知道 gcd(n，m)必须除 n，商告诉我们 m 个数从起始位置(比如 0)连续跳跃(相加)多少次后，我们再次到达起始位置。
**注:**在圆形排列的 n 个数字中，第 n 个和第 0 个位置相同。

## C++

```
// C++ program to find minimum steps to reach
// starting position in a circular tour.
#include<bits / stdc++.h>
using namespace std;

// function for finding minimum steps
int minStroke(int n, int m)
{
    // return value n / gcd(n, m)
    return (n/__gcd(n, m));
}

// Driver function
int main()
{
    int n = 12, k = 5, m = 8;
    cout << minStroke(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum steps to reach
// starting position in a circular tour.

class Test
{
    // method for finding minimum steps
    static int minStroke(int n, int m)
    {
        // return value n / gcd(n, m)
        return (n/gcd(n, m));
    }

    // method for gcd
    static int gcd(int n, int m) {

        if (n == 0 || m == 0)
           return 0;

        if (n == m)
            return n;

        if (n > m)
            return gcd(n-m, m);
        return gcd(n, m-n);
    }

    // Driver method
    public static void main(String args[])
    {
        int n = 12, k = 5, m = 8;
        System.out.println(minStroke(n, m));
    }
}
```

## 蟒蛇 3

```
# Python program to find minimum
# steps to reach starting position
# in a circular tour.

# function for finding minimum steps
def minStroke(n, m):

    # return value n / gcd(n, m)
    return (n / __gcd(n, m))

# method for gcd
def __gcd(n, m):

    if(n == 0 or m == 0):
        return 0

    if (n == m):
        return n

    if (n > m):
        return __gcd(n-m, m)

    return __gcd(n, m-n)

# Driver code
n = 12
k = 5
m = 8

print(minStroke(n, m))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find minimum steps to reach
// starting position in a circular tour.
using System;
using System.Collections;

class GFG
{
    // method for finding minimum steps
    static int minStroke(int n, int m)
    {
        // return value n / gcd(n, m)
        return (n/gcd(n, m));
    }

    // method for gcd
    static int gcd(int n, int m) {

        if (n == 0 || m == 0)
        return 0;

        if (n == m)
            return n;

        if (n > m)
            return gcd(n-m, m);

        return gcd(n, m-n);
    }

    // Driver method
    public static void Main()
    {
        int n = 12, m = 8;
        Console.WriteLine(minStroke(n, m));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// steps to reach starting
// position in a circular tour.

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{
    // Everything divides 0
    if($a == 0 || $b == 0)
        return 0 ;

    // base case
    if($a == $b)
        return $a ;

    // a is greater
    if($a > $b)
        return __gcd($a - $b , $b);

    return __gcd($a , $b - $a);
}

// function for
// finding minimum steps
function minStroke($n, $m)
{
    // return value n / gcd(n, m)
    return ($n / __gcd($n, $m));
}

// Driver Code
$n = 12; $k = 5; $m = 8;
echo minStroke($n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum steps to reach
// starting position in a circular tour.

// function for finding minimum steps
function minStroke(n, m)
{
    // return value n / gcd(n, m)
    return (n/gcd(n, m));
}

// method for gcd
function gcd(n, m) {

        if (n == 0 || m == 0)
           return 0;

        if (n == m)
            return n;

        if (n > m)
            return gcd(n-m, m);
        return gcd(n, m-n);
}
// Driver function

    let n = 12, k = 5, m = 8;
    document.write(minStroke(n, m));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(log(n))
本文由[Shivam Pradhan(anuj _ charm)](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。