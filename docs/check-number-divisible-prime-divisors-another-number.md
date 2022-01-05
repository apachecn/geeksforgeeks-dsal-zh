# 检查一个数是否能被另一个数的所有质因数整除

> 原文:[https://www . geesforgeks . org/check-number-除数-质因数-另一个数/](https://www.geeksforgeeks.org/check-number-divisible-prime-divisors-another-number/)

给定两个整数。我们需要找出第一个数 x 是否能被 y 的所有质因数整除。
**举例:**

```
Input  : x = 120, y = 75
Output : Yes
Explanation :
120 = (2^3)*3*5
75  = 3*(5^2)
120 is divisible by both 3 and 5 which 
are the prime divisors of 75\. Hence, 
answer is "Yes".

Input  :  x = 15, y = 6
Output : No
Explanation : 
15 = 3*5.
 6 = 2*3,
15 is not divisible by 2 which is a 
prime divisor of 6\. Hence, answer 
is "No".
```

一个**简单的解决方法**是[找到 y 的所有素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，对于每个素因子，检查它是否除了 x。
安**高效解决方案**基于以下事实。
1)如果 y == 1，那么它没有质因数。因此答案是“是”
2)我们找到 x 和 y 的 GCD。
a)如果 GCD == 1，那么显然不存在 x 和 y 的公约数，因此答案是“否”。
b)如果 GCD > 1，则 GCD 包含除以 x 的素数。现在，当且仅当 y/GCD 有这样唯一的素除数时，我们都有唯一的素除数。因此，我们必须使用递归来寻找对(x，y/GCD)的唯一性。

## C++

```
// CPP program to find if all prime factors
// of y divide x.
#include <bits/stdc++.h>
using namespace std;

// Returns true if all prime factors of y
// divide x.
bool isDivisible(int x, int y)
{
    if (y == 1)
        return true;

    if (__gcd(x, y) == 1)
        return false;
    return isDivisible(x, y / gcd);
}

// Driver Code
int main()
{
    int x = 18, y = 12;
    if (isDivisible(x, y))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if all
// prime factors of y divide x.
class Divisible
{
    public static int gcd(int a, int b) {
      return b == 0 ? a : gcd(b, a % b); }

    // Returns true if all prime factors
    // of y divide x.
    static boolean isDivisible(int x, int y)
    {
        if (y == 1)
            return true;

        int z = gcd(x, y);

        if (z == 1)
            return false;

        return isDivisible(x, y / z);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        int x = 18, y = 12;
        if (isDivisible(x, y))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# python program to find if all
# prime factors of y divide x.

def gcd(a, b):
    if(b == 0):
        return a
    else:
        return gcd(b, a % b)

# Returns true if all prime
# factors of y divide x.
def isDivisible(x,y):

    if (y == 1):
        return 1

    z = gcd(x, y);

    if (z == 1):
        return false;

    return isDivisible(x, y / z);

# Driver Code
x = 18
y = 12
if (isDivisible(x, y)):
    print("Yes")
else:
    print("No")

# This code is contributed by Sam007
```

## C#

```
// C# program to find if all
// prime factors of y divide x.
using System;

class GFG {

    public static int gcd(int a, int b)
    {
        return b == 0 ? a : gcd(b, a % b);
    }

    // Returns true if all prime factors
    // of y divide x.
    static bool isDivisible(int x, int y)
    {
        if (y == 1)
            return true;

        int z = gcd(x, y);

        if (z == 1)
            return false;

        return isDivisible(x, y / z);
    }

    // Driver program to test above functions
    public static void Main()
    {
        int x = 18, y = 12;

        if (isDivisible(x, y))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if all
// prime factors of y divide x.

function gcd ($a, $b)
{
    return $b == 0 ? $a :
        gcd($b, $a % $b);
}

// Returns true if all prime
// factors of y divide x.
function isDivisible($x, $y)
{
    if ($y == 1)
        return true;

    $z = gcd($x, $y);

    if ($z == 1)
        return false;

    return isDivisible($x, $y / $z);
}

// Driver Code
$x = 18;
$y = 12;
if (isDivisible($x, $y))
    echo "Yes";
else
    echo "No";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find if all
// prime factors of y divide x.

function gcd(a , b) {
  return b == 0 ? a : gcd(b, a % b); }

// Returns true if all prime factors
// of y divide x.
function isDivisible(x , y)
{
    if (y == 1)
        return true;

    var z = gcd(x, y);

    if (z == 1)
        return false;

    return isDivisible(x, y / z);
}

// Driver program to test above functions

var x = 18, y = 12;
if (isDivisible(x, y))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
Yes
```

**时间复杂度:**计算 GCD 的时间复杂度为 O(log min(x，y))，递归将在 log y 步后终止，因为我们正在将其减少一个大于 1 的因子。整体时间复杂度: **O(log <sup>2</sup> y)**
本文由 [**Harsha Mogali**](https://auth.geeksforgeeks.org/profile.php?user=Harsha Mogali 1) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。