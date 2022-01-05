# 给定数字的位数 LCM

> 原文:[https://www.geeksforgeeks.org/lcm-digits-given-number/](https://www.geeksforgeeks.org/lcm-digits-given-number/)

给定一个数字 n，求其数字的 LCM。
**例:**

```
Input : 397
Output : 63
LCM of 3, 9 and 7 is 63.

Input : 244
Output : 4
LCM of 2, 4 and 4 is 4.
```

我们在循环
数字= n mod 10 下一个一个遍历数字的数字；
n = n/10；
在遍历数字时，我们跟踪当前的 LCM，并通过用当前的 LCM 查找当前数字的 LCM 来更新 LCM。

## C++

```
// CPP program to find LCM of digits of a number
#include<iostream>
#include<boost/math/common_factor.hpp>
using namespace std;

int digitLCM(int n)
{
    int lcm = 1;
    while (n > 0)
    {
        lcm = boost::math::lcm(n%10, lcm);

        // If at any point LCM become 0.
        // return it
        if (lcm == 0)
            return 0;

        n = n/10;
    }
    return lcm;
}

// driver code
int main()
{
    long n = 397;
    cout << digitLCM(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCM of digits of a number

class GFG
{
// define lcm function
static int lcm_fun(int a, int b)
{
    if (b == 0)
        return a;
    return lcm_fun(b, a % b);
}

static int digitLCM(int n)
{
    int lcm = 1;
    while (n > 0)
    {
        lcm = (n % 10 * lcm) / lcm_fun(n % 10, lcm);

        // If at any point LCM become 0.
        // return it
        if (lcm == 0)
            return 0;

        n = n/10;
    }
    return lcm;
}

// driver code
public static void main(String[] args)
{
    int n = 397;
    System.out.println(digitLCM(n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find
# LCM of digits of a number

# define lcm function
def lcm_fun(a, b):

    if (b == 0):
        return a;
    return lcm_fun(b, a % b);

def digitLCM(n):

    lcm = 1;
    while (n > 0):
        lcm = int((n % 10 * lcm) /
              lcm_fun(n % 10, lcm));

        # If at any point LCM
        # become 0\. return it
        if (lcm == 0):
            return 0;

        n = int(n / 10);

    return lcm;

# Driver code
n = 397;
print(digitLCM(n));

# This code is contributed by mits
```

## C#

```
// C# program to find LCM of digits
// of a number
class GFG
{

// define lcm function
static int lcm_fun(int a, int b)
{
    if (b == 0)
        return a;
    return lcm_fun(b, a % b);
}

static int digitLCM(int n)
{
    int lcm = 1;
    while (n > 0)
    {
        lcm = (n % 10 * lcm) / lcm_fun(n % 10, lcm);

        // If at any point LCM become 0.
        // return it
        if (lcm == 0)
            return 0;

        n = n/10;
    }
    return lcm;
}

// Driver Code
public static void Main()
{
    int n = 397;
    System.Console.WriteLine(digitLCM(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// LCM of digits of a number

// define lcm function
function lcm_fun($a, $b)
{
    if ($b == 0)
        return $a;
    return lcm_fun($b, $a % $b);
}

function digitLCM($n)
{
    $lcm = 1;
    while ($n > 0)
    {
        $lcm = (int)(($n % 10 * $lcm) /
              lcm_fun($n % 10, $lcm));

        // If at any point LCM
        // become 0\. return it
        if ($lcm == 0)
            return 0;

        $n = (int)($n / 10);
    }
    return $lcm;
}

// Driver code
$n = 397;
echo digitLCM($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find LCM of digits of a number

    // define lcm function
    function lcm_fun( a, b)
    {
        if (b == 0)
            return a;
        return lcm_fun(b, a % b);
    }

    function digitLCM( n)
    {
        let lcm = 1;
        while (n > 0)
        {
            lcm = (n % 10 * lcm) / lcm_fun(n % 10, lcm);

            // If at any point LCM become 0.
            // return it
            if (lcm == 0)
                return 0;

            n = parseInt(n / 10);
        }
        return lcm;
    }

    // Driver code    
        let n = 397;
        document.write(digitLCM(n));

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
63
```

本文由[**nikun Ji _ Agarwal**](https://auth.geeksforgeeks.org/profile.php?user=nikunj_agarwal)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。