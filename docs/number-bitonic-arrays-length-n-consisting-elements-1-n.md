# 长度为 n 且由 1 至 n 个元素组成的双离子阵列的数量

> 原文:[https://www . geesforgeks . org/number-bitonic-arrays-length-n-composited-elements-1-n/](https://www.geeksforgeeks.org/number-bitonic-arrays-length-n-consisting-elements-1-n/)

对于一个给定的数 n (n > 1)，我们需要找到你可以做出长度为 n 的双调和数组的方法数，由从 1 到 n 的所有元素组成。
注:[1，2，…n]和[n，n–1…2，1]不被认为是双调和数组。

**示例:**

```
Input : n = 3
Output : 2

Explanation : [1, 3, 2] & [2, 3, 1] 
are only two ways of bitonic array 
formation for n = 3.

Input : n = 4
Output : 6
```

为了创建一个双音素数组，假设我们有一个长度为 n 的空数组，我们想把这个数组中从 1 到 n 的数字用双音素的形式表示出来，现在假设我们想把数字 1 相加，我们只有两种可能的方法来表示数字 1，两者都是结束位置，因为如果我们应该把 1 放在端点以外的任何地方，那么 1 两边的数字都大于 1。之后我们可以想象，我们有一个长度为 n-1 的数组，现在我们想把数字 2，同样的原因，我们有两种方式，以此类推，直到我们想把数字 n，我们将只有 1 种方式，而不是 2，所以我们有 n-1 个数字，有 2 种方式，所以根据组合学的乘法规则，答案是 2^n-1，最后我们应该从答案中减去 2，因为排列 1 2 3 4。n 和 n-1 … 3 2 1 不应该计算在内。

## C++

```
// C++ program for finding
// total bitonic array
#include<bits/stdc++.h>
using namespace std;

// Function to calculate no. of ways
long long int maxWays( int n)
{
    // return (2^(n - 1)) -2
    return (pow(2, n - 1) - 2);
}

// Driver Code
int main()
{
    int n = 6;
    cout << maxWays(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding
// total bitonic array
class GFG
{

    // Function to calculate no. of ways
    static int maxWays( int n)
    {

        // return (2 ^ (n - 1)) -2
        return (int)(Math.pow(2, n - 1) - 2);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 6;

        System.out.print(maxWays(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python program for finding
# total bitonic array

# Function to calculate no. of ways
def maxWays(n):

    # return (2^(n - 1)) -2
    return (pow(2, n - 1) - 2);

# Driver Code
n = 6;
print(maxWays(n))

# This code is contributed by Sam007
```

## C#

```
// C# program for finding
// total bitonic array
using System;

class GFG
{

    // Function to calculate no. of ways
    static int maxWays( int n)
    {

        // return (2 ^ (n - 1)) -2
        return (int)(Math.Pow(2, n - 1) - 2);
    }

    // Driver Code
    public static void Main ()
    {
        int n = 6;

        Console.Write(maxWays(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding
// total bitonic array

// Function to calculate
// no. of ways
function maxWays( $n)
{

    // return (2^(n - 1)) -2
    return (pow(2, $n - 1) - 2);
}

// Driver Code
$n = 6;
echo maxWays($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program for finding
// total bitonic array

// Function to calculate no. of ways
function maxWays( n)
{
    // return (2^(n - 1)) -2
    return (Math.pow(2, n - 1) - 2);
}

// Driver Code
var n = 6;
document.write( maxWays(n));

</script>
```

**输出:**

```
30
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。