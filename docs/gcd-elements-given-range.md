# 给定范围内元素的 GCD

> 原文:[https://www.geeksforgeeks.org/gcd-elements-given-range/](https://www.geeksforgeeks.org/gcd-elements-given-range/)

给定两个数字 n 和 m，求最大整数 a(gcd)，这样所有整数 n，n + 1，n + 2，…，m 都可以被 a 整除。
示例:

```
Input : n = 1, m = 2
Output: 1
Explanation:
Here, series become 1, 2\. So, the 
greatest no which divides both of 
them is 1.

Input : n = 475, m = 475
Output : 475
Explanation:
Here, series has only one term 475.
So, greatest no which divides 475 is 475.
```

这里，我们只需要检查两种情况:

1.  如果 a = b:线段由一个数字组成，那么答案就是 a。
2.  如果 a < b:我们有 gcd(n，n + 1，n？+ 2，…，m) = gcd(gcd(n，n + 1)，n + 2，…，m) = gcd(1，n + 2，…，n) = 1。

## C++

```
// GCD of given range
#include <bits/stdc++.h>
using namespace std;

int rangeGCD(int n, int m)
{
    return (n == m)? n : 1;
}

int main()
{
    int n = 475;
    int m = 475;
    cout << rangeGCD(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// GCD of given range

import java.io.*;

class GFG {

    static int rangeGCD(int n, int m)
    {
        return (n == m) ? n : 1;
    }

    public static void main(String[] args)
    {
        int n = 475;
        int m = 475;

        System.out.println(rangeGCD(n, m));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# GCD of given range

def rangeGCD(n, m):
    return n if(n == m) else 1

# Driver code
n, m = 475, 475
print(rangeGCD(n, m))

# This code is contributed by Anant Agarwal.
```

## C#

```
// GCD of given range
using System;

class GFG {

    static int rangeGCD(int n, int m)
    {
        return (n == m) ? n : 1;
    }

    public static void Main()
    {
        int n = 475;
        int m = 475;

        Console.WriteLine(rangeGCD(n, m));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for
// GCD of given range

// function returns the GCD
function rangeGCD($n, $m)
{
    return ($n == $m)? $n : 1;
}

    // Driver Code
    $n = 475;
    $m = 475;
    echo rangeGCD($n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// GCD of given range

    function rangeGCD( n,  m)
    {
        return (n == m) ? n : 1;
    }

        var n = 475;
        var m = 475;

        document.write(rangeGCD(n, m));

</script>
```

**输出:**

```
475
```