# 给定范围内奇数因子的元素数量

> 原文:[https://www . geesforgeks . org/number-elements-奇数-factors-给定-range/](https://www.geeksforgeeks.org/number-elements-odd-factors-given-range/)

给定一个范围【 ***n*** 、 ***m*** 】,求给定范围内因子个数为奇数的元素个数( ***n*** 和 ***m*** )。
**举例:**

```
Input  : n = 5, m = 100
Output : 8
The numbers with odd factors are 9, 16, 25, 
36, 49, 64, 81 and 100

Input  : n = 8, m = 65
Output : 6

Input  : n = 10, m = 23500
Output : 150
```

一个**简单的解决方案**是从 ***n*** 开始循环所有的数字。对于每个数字，检查它是否有偶数个因子。如果它有偶数个因子，那么增加这些数字的计数，最后打印这些元素的数量。要高效地找到自然数的所有除数，请参考[自然数的所有除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)
**高效的解决方案**是观察模式。只有那些 [**完美正方形**](https://en.wikipedia.org/wiki/Square_number) 的数字有奇数个因子。让我们通过一个例子来分析这个模式。
比如 9 有奇数个因子，1，3，9。16 也有奇数个因子，1，2，4，8，16。这样做的原因是，对于完美平方以外的数字，所有因子都是成对的形式，但是对于完美平方，一个因子是单个的，使得总数为奇数。
**如何找到一个范围内的完美方块数？**
答案是 **m** 和 **n-1** ( **不是 n** )
的平方根差，有一点告诫。由于 **n** 和 **m** 都是包含的，如果 **n** 是一个完美的正方形，我们会得到一个比实际答案少一个的答案。要理解这一点，考虑范围[4，36]。答案是 5，即数字 4、9、16、25 和 36。
但是如果我们做(36 * * 0.5)–(4 * * 0.5)我们得到 4。所以为了避免这个语义错误，我们取 **n-1** 。

## C++

```
// C++ program to count number of odd squares
// in given range [n, m]
#include <bits/stdc++.h>
using namespace std;

int countOddSquares(int n, int m)
{
   return (int)pow(m,0.5) - (int)pow(n-1,0.5);
}

// Driver code
int main()
{
    int n = 5, m = 100;
    cout << "Count is " << countOddSquares(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of odd squares
// in given range [n, m]

import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
    public static int countOddSquares(int n, int m)
    {
        return (int)Math.pow((double)m,0.5) - (int)Math.pow((double)n-1,0.5);
    }
    // Driver code for above functions
    public static void main (String[] args)
    {
        int n = 5, m = 100;
        System.out.print("Count is " + countOddSquares(n, m));
    }
}
// Mohit Gupta_OMG <(o_0)>
```

## 蟒蛇 3

```
# Python program to count number of odd squares
# in given range [n, m]

def countOddSquares(n, m):
    return int(m**0.5) - int((n-1)**0.5)

# Driver code
n = 5
m = 100
print("Count is", countOddSquares(n, m))

# Mohit Gupta_OMG <0_o>
```

## C#

```
// C# program to count number of odd
// squares in given range [n, m]
using System;

class GFG {

    // Function to count odd squares
    public static int countOddSquares(int n, int m)
    {
        return (int)Math.Pow((double)m, 0.5) -
               (int)Math.Pow((double)n - 1, 0.5);
    }

    // Driver code
    public static void Main ()
    {
        int n = 5, m = 100;
        Console.Write("Count is " + countOddSquares(n, m));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of odd squares
// in given range [n, m]

function countOddSquares($n, $m)
{
return pow($m, 0.5) -
       pow($n - 1, 0.5);
}

// Driver code
$n = 5; $m = 100;
echo "Count is " ,
      countOddSquares($n, $m);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count number of odd squares
// in given range [n, m]

function countOddSquares(n, m)
    {
        return Math.pow(m,0.5) - Math.pow(n-1,0.5);
    }

// Driver Code

        let n = 5, m = 100;
        document.write("Count is " + countOddSquares(n, m));

</script>
```

**输出:**

```
Count is 8
```

**时间复杂度:** O(1)
本文由 [**迪维言舒班萨尔**](https://www.hackerearth.com/@divyanshu12) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。