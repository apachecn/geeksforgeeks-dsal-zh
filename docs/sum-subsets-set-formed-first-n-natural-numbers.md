# 由前 n 个自然数构成的集合的所有子集的和

> 原文:[https://www . geesforgeks . org/sum-subsets-set-formed-first-n-natural-numbers/](https://www.geeksforgeeks.org/sum-subsets-set-formed-first-n-natural-numbers/)

给定一个数 n，我们需要从由前 n 个自然数组成的集合的所有可能子集找到所有元素的和。
**例:**

```
Input :  n = 2
Output : 6
Possible subsets are {{1}, {2}, 
{1, 2}}. Sum of elements in subsets
is 1 + 2 + 1 + 2 = 6

Input :  n = 3
Output : 24
Possible subsets are {{1}, {2}, {3}, 
{1, 2}, {1, 3}, {2, 3}, {1, 2, 3}}
Sum of subsets is : 
1 + 2 + 3 + (1 + 2) + (1 + 3) + 
(2 + 3) + (1 + 2 + 3)
```

一个**简单的解决方案**是[生成所有子集](https://www.geeksforgeeks.org/power-set/)。对于每个子集，计算其总和，最后返回总和。
一个**高效的解决方案**是基于从 1 到 n 的每个数字恰好出现 2 次 <sup>(n-1)</sup> 的事实。所以我们需要的和是(1 + 2 + 3 +)..+ n) * 2 <sup>(n-1)</sup> 。总和可以写成(n *(n+1)/2)* 2<sup>(n-1)</sup>

## C++

```
// CPP program to find sum of all subsets
// of a set.
#include <bits/stdc++.h>
using namespace std;

unsigned long long findSumSubsets(int n)
{
    // sum of subsets is (n * (n + 1) / 2) *
    // pow(2, n-1)
    return (n * (n + 1) / 2) * (1 << (n - 1));
}

int main()
{
    int n = 3;
    cout << findSumSubsets(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all subsets
// of a set.

class GFG {
    static long findSumSubsets(int n)
    {
        // sum of subsets is (n * (n + 1) / 2) *
        // pow(2, n-1)
        return (n * (n + 1) / 2) * (1 << (n - 1));
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        System.out.print(findSumSubsets(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# sum of all subsets
# of a set.

def findSumSubsets( n):

    # sum of subsets
    # is (n * (n + 1) / 2) *
    # pow(2, n-1)
    return (n * (n + 1) / 2) * (1 << (n - 1))

# Driver code    
n = 3
print(findSumSubsets(n))

# This code is contributed
# by sunnysingh.
```

## C#

```
// C# program to find sum of all subsets
// of a set.
using System;

class GFG {

    static long findSumSubsets(int n)
    {

        // sum of subsets is (n * (n + 1) / 2) *
        // pow(2, n-1)
        return (n * (n + 1) / 2) * (1 << (n - 1));
    }

    // Driver code
    public static void Main()
    {
        int n = 3;

        Console.WriteLine(findSumSubsets(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of all subsets of a set

function findSumSubsets($n)
{
    // sum of subsets is (n *
    // (n + 1) / 2) * pow(2, n-1)
    return ($n * ($n + 1) / 2) *
                 (1 << ($n - 1));
}

// Driver Code
$n = 3;
echo findSumSubsets($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to find sum of all subsets
// of a set.

function findSumSubsets( n)
{
    // sum of subsets is (n * (n + 1) / 2) *
    // pow(2, n-1)
    return (n * (n + 1) / 2) * (1 << (n - 1));
}

// Driven Program

    let n = 3;
     document.write(findSumSubsets(n));

// This code contributed by aashish1995

</script>
```

**输出:**

```
24
```

本文由**拉杰·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。