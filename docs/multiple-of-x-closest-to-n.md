# 最接近 n 的 x 的倍数

> 原文:[https://www.geeksforgeeks.org/multiple-of-x-closest-to-n/](https://www.geeksforgeeks.org/multiple-of-x-closest-to-n/)

给定两个数字 n 和 x，我们需要计算最接近给定数字 n 的 x 的最小值
**例:**

```
Input : n = 9, x = 4
Output : 8

Input  : n = 2855, x = 13
Output : 2860

Input  :  n = 46426171, x = 43
Output :  46426154

Input  :  n = 1, x = 3
Output :  3
```

我们需要找到一个 k，使得 x*k 最接近 n，如果我们做 k = n/x，我们得到的 k 值可能不会导致最大值。我们可以通过比较 floor(n/x) * x 和 ceil(n/x) * x 的值来得到最接近的值。
下面是一个有趣的解决方案，不需要计算 floor(n/x)和 ceil(n/x)。想法是做以下两步。

```
    n = n + x/2;
    n = n - (n%x);
    result = n
```

让我们考虑下面的例子

```
  n = 2855 
  x = 13

  n = 2855 + 13/2
    = 2861
  n = 2861 - (2861 % 13)
    = 2861 - 1
    = 2860 
```

以下是上述步骤的实现。

## C++

```
// CPP program to calculate the smallest multiple
// of x closest to a given number
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the smallest multiple
int closestMultiple(int n, int x)
{  
    if(x>n)
       return x;

    n = n + x/2;
    n = n - (n%x);
    return n;
}

// driver program
int main()
{
    int n = 9, x = 4;
    printf("%d", closestMultiple(n, x));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the smallest
// multiple of x closest to a given number
import java.io.*;
class Solution
{
    // Function to calculate the smallest multiple
    static int closestMultiple(int n, int x)
    {  
        if(x>n)
           return x;
        n = n + x/2;
        n = n - (n%x);
        return n;
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 56287, x = 27;
        System.out.println(closestMultiple(n, x));
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate
# the smallest multiple of x
# closest to a given number

# Function to calculate
# the smallest multiple
def closestMultiple(n, x):
    if x > n:
        return x;
    z = (int)(x / 2);
    n = n + z;
    n = n - (n % x);
    return n;

# Driver Code
n = 56287;
x = 27;
print(closestMultiple(n, x));

# This code is contributed
# by mits
```

## C#

```
// C# program to calculate smallest
// multiple of x closest to a
// given number
using System;

class Solution {
    // Function to calculate the
    // smallest multiple
    static int closestMultiple(int n, int x)
    {

        if (x > n)
            return x;
        n = n + x / 2;
        n = n - (n % x);
        return n;
    }

    // Driver program
    public static void Main()
    {
        int n = 56287, x = 27;
        Console.WriteLine(closestMultiple(n, x));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// the smallest multiple
// of x closest to a
// given number

// Function to calculate
// the smallest multiple
function closestMultiple($n, $x)
{
    if($x > $n)
    return $x;

    $n = $n + $x / 2;
    $n = $n - ($n % $x);
    return $n;
}

    // Driver Code
    $n = 9;
    $x = 4;
    echo closestMultiple($n, $x);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to calculate smallest
    // multiple of x closest to a
    // given number

    // Function to calculate the
    // smallest multiple
    function closestMultiple(n, x)
    {

        if (x > n)
            return x;
        n = n + parseInt(x / 2, 10);
        n = n - (n % x);
        return n;
    }

    let n = 56287, x = 27;
      document.write(closestMultiple(n, x));

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
 56295
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。