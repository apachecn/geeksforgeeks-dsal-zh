# 不包含 9 的 n 位数的个数

> 原文:[https://www . geesforgeks . org/numbers-n-digital-numbers-not-contain-9/](https://www.geeksforgeeks.org/numbers-n-digit-numbers-not-contain-9/)

给定一个数字 n，找出可以形成多少个不包含 9 的 n 位数。
示例:

```
Input : 1
Output : 8
Explanation :
Except 9, all numbers are possible

Input : 2
Output : 72
Explanation :
Except numbers from 90 - 99 and all
two digit numbers that does not end
with 9 are possible.
```

可以形成的 n 位数字的总数将是 9*10^(n-1)，因为除了第一个位置之外，所有数字都可以用 10 个数字(0-9)填充。如果从列表中删除数字 9，那么 n 个数字的总数将是 8*9^(n-1).
以下是上述思路的实现:

## C++

```
// CPP program to find number of n
// digit numbers that do not
// contain 9 as it's digit
#include <bits/stdc++.h>
using namespace std;

// function to find number of
// n digit numbers possible
int totalNumber(int n)
{
    return 8*pow(9, n - 1);
}

// driver function
int main()
{
    int n = 3;
    cout << totalNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of 
// n digit numbers that do not
// contain 9 as it's digit
import java.io.*;

public class GFG
{

// function to find number of
// n digit numbers possible
static int totalNumber(int n)
{
    return 8 * (int)Math.pow(9, n - 1);
}

    // Driver Code
    static public void main (String[] args)
    {
        int n = 3;
        System.out.println(totalNumber(n));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# python program to find number of n
# digit numbers that do not
# contain 9 as it's digit

# function to find number of
# n digit numbers possible
def totalNumber(n):

    return 8 * pow(9, n - 1);

# driver function
n = 3
print(totalNumber(n))

# This code is contributed by Sam007
```

## C#

```
// C# program to find number of 
// n digit numbers that do not
// contain 9 as it's digit
using System;

public class GFG
{

// function to find number of
// n digit numbers possible
static int totalNumber(int n)
{
    return 8 * (int)Math.Pow(9, n - 1);
}

    // Driver Code
    static public void Main ()
    {
        int n = 3;
        Console.WriteLine(totalNumber(n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find number of n
// digit numbers that do not
// contain 9 as it's digit

// function to find number of
// n digit numbers possible
function totalNumber($n)
{
    return 8 * pow(9, $n - 1);
}

// driver function
$n = 3;
print(totalNumber($n))

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of 
// n digit numbers that do not
// contain 9 as it's digit

// function to find number of
// n digit numbers possible
function totalNumber(n)
{
    return 8 * Math.pow(9, n - 1);
}

// Driver code
        let n = 3;
        document.write(totalNumber(n));

   // This code is contributed by code_hunt.
</script>
```

输出:

```
648
```

本文由 [**迪本杜·罗伊·乔杜里**](https://auth.geeksforgeeks.org/profile.php?user=Dibyendu Roy Chaudhuri) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。