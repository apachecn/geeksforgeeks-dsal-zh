# 求最接近或等于^ b 的 x 的倍数(a 升到 b 的幂)

> 原文:[https://www.geeksforgeeks.org/find-multiple-x-closest-ab/](https://www.geeksforgeeks.org/find-multiple-x-closest-ab/)

给我们 3 个数字 a、b 和 x，我们需要输出最接近 a^b.的 x 的倍数
**注:** b 可以是负数
**例:**

```
Input : x = 2, a = 4, b = -2
Output : 0
Explanation : a^b = 1/16\. 
Closest multiple of 2 to 1/16 is 0.

Input : x = 4, a = 349, b = 1
Output : 348
Explanation :a^b = 349
The closest multiple of 4 to 349 is 348.
```

**观察:**

```
1\. When b is negative and a is 1, then a ^ b turns out 
to be 1 and hence, closest multiple of x becomes either
 x * 0 or x * 1.

2\. When b is negative and a is more than 1, then a ^ b
turns out to be less than 1 and hence closest multiple
of x becomes 0.

3\. When b is positive, calculate a ^ b, then let 
mul = Integer (a^b / x), then closest multiple of x is 
mul * x or (mul + 1) * x.
```

## C++

```
// C++ Program to find closest
// multiple of x to a^b
#include <bits/stdc++.h>
using namespace std;

// function to find closest multiple 
// of x to a^b
void multiple(int a, int b, int x)
{   
    if (b < 0) {
        if (a == 1 && x == 1)
            cout << "1";

        else
            cout << "0";
    }

    // calculate a ^ b / x
    int mul = pow(a, b);

    int ans = mul / x;

    // Answer is either (ans * x) or
    // (ans + 1) * x
    int ans1 = x * ans;
    int ans2 = x * (ans + 1);

    // Printing nearest answer
    cout << (((mul - ans1) <= (ans2 - mul)) ?
                                ans1 : ans2);
}

// Driver Program
int main()
{
    int a = 349, b = 1, x = 4;

    multiple(a, b, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java Program to find closest
// multiple of x to a^b
import java.io.*;

public class GFG {

    // function to find closest
    // multiple of x to a^b
    static void multiple(int a, int b, int x)
    {
        if (b < 0)
        {
            if (a == 1 && x == 1)
                System.out.println("1");
            else
                System.out.println("0");
        }

        // calculate a ^ b / x
        int mul = (int)Math.pow(a, b);

        int ans = mul / x;

        // Answer is either (ans * x) or
        // (ans + 1) * x
        int ans1 = x * ans;
        int ans2 = x * (ans + 1);

        // Printing nearest answer
        System.out.println(((mul - ans1)
                        <= (ans2 - mul))
                         ? ans1 : ans2);
    }

    // Driver Program
    static public void main (String[] args)
    {
        int a = 349, b = 1, x = 4;

        multiple(a, b, x);
    }
}

// This code is contributed by vt_m.
```

## C#

```
// C# Program to find closest
// multiple of x to a^b
using System;

public class GFG {

    // function to find closest multiple
    // of x to a^b
    static void multiple(int a, int b, int x)
    {
        if (b < 0) {
            if (a == 1 && x == 1)
                Console.WriteLine("1");

            else
                Console.WriteLine("0");
        }

        // calculate a ^ b / x
        int mul = (int)Math.Pow(a, b);

        int ans = mul / x;

        // Answer is either (ans * x) or
        // (ans + 1) * x
        int ans1 = x * ans;
        int ans2 = x * (ans + 1);

        // Printing nearest answer
        Console.WriteLine(((mul - ans1)
                       <= (ans2 - mul))
                         ? ans1 : ans2);
    }

    // Driver Program
    static public void Main ()
    {
        int a = 349, b = 1, x = 4;

        multiple(a, b, x);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find closest
// multiple of x to a^b

// function to find
// closest multiple
// of x to a^b
function multiple($a, $b, $x)
{
    if ($b < 0)
    {
        if ($a == 1 && $x == 1)
            echo "1";

        else
            echo "0";
    }

    // calculate a ^ b / x
    $mul = pow($a, $b);

    $ans = $mul / $x;

    // Answer is either
    // (ans * x) or
    // (ans + 1) * x
    $ans1 = $x * $ans;
    $ans2 = $x * ($ans + 1);

        $k = ((($mul - $ans1) <= ($ans2 - $mul))
                               ? $ans1 : $ans2);
        echo($k);
}

    // Driver Code
    $a = 348;
    $b = 1;
    $x = 4;

    multiple($a, $b, $x);

// This code is contributed by ajit
?>
```

## 蟒蛇 3

```
# Python3 Program to
# find closest multiple
# of x to a^b
import math

# function to find closest
# multiple of x to a^b
def multiple(a, b, x):
    if (b < 0):
        if (a == 1 and x == 1):
            print("1");
        else:
            print("0");

    # calculate a ^ b / x
    mul = int(pow(a, b));

    ans = int(mul / x);

    # Answer is either (ans * x)
    # or (ans + 1) * x
    ans1 = x * ans;
    ans2 = x * (ans + 1);

    # Printing nearest answer
    if ((mul - ans1) <= (ans2 - mul)):
        print(ans1);
    else:
        print(ans2);

# Driver Code
a = 349;
b = 1;
x = 4;
multiple(a, b, x);

# This code is contributed
# by mits
```

## java 描述语言

```
<script>
// javascript Program to find closest
// multiple of x to a^bpublic

    // function to find closest
    // multiple of x to a^b
    function multiple(a , b , x) {
        if (b < 0) {
            if (a == 1 && x == 1)
                document.write("1");
            else
                document.write("0");
        }

        // calculate a ^ b / x
        var mul = parseInt( Math.pow(a, b));

        var ans = mul / x;

        // Answer is either (ans * x) or
        // (ans + 1) * x
        var ans1 = x * ans;
        var ans2 = x * (ans + 1);

        // Printing nearest answer
        document.write(((mul - ans1) <= (ans2 - mul)) ? ans1 : ans2);
    }

    // Driver Program
        var a = 349, b = 1, x = 4;

        multiple(a, b, x);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
348
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。