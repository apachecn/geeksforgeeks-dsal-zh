# 计算(a*b)%c，使得(a%c) * (b%c)可以超出范围

> 原文:[https://www . geesforgeks . org/compute-ABC-so-AC-BC-can-beyond-beyond/](https://www.geeksforgeeks.org/compute-abc-such-that-ac-bc-can-be-beyond-range/)

给定三个数字 a、b 和 c，使得 a、b 和 c 最多为 10 <sup>16</sup> 。任务是计算(a*b)%c
一个简单的做((a % c) * (b % c) ) % c 的解决方案在这里行不通。这里的问题是 a 和 b 可能很大，所以当我们计算(a % c) * (b % c)时，它超出了 long long int 可以容纳的范围，因此会发生溢出。例如，如果 a = (10 <sup>12</sup> +7)，b = (10 <sup>13</sup> +5)，c = (10 <sup>15</sup> +3)。
现在 long long int 最多可以容纳 4 x 10 <sup>18</sup> (大约)，a*b 比这个大很多。

我们可以不用直接乘法，而用加法找到 a + a + ……。(b 乘以)并在每次加 a 时用 c 取模，这样溢出就不会发生。但是这将是低效的，我们必须以优化的方式计算(∑ a) % c。
我们可以用分治来计算。主要思路是:

1.  如果 b 是偶数，那么 a*b = (2*a) * (b/2)
2.  如果 b 是奇数，那么 a*b = a + (2*a)*((b-1)/2)

下面是算法的实现:

## C++

```
// C++ program to Compute (a*b)%c
// such that (a%c) * (b%c) can be
// beyond range
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

// returns (a*b)%c
ll mulmod(ll a,ll b,ll c)
{
    // base case if b==0, return 0
    if (b==0)
        return 0;

    // Divide the problem into 2 parts
    ll s = mulmod(a, b/2, c);

    // If b is odd, return
    // (a+(2*a)*((b-1)/2))%c
    if (b%2==1)
        return (a%c+2*(s%c)) % c;

    // If b is odd, return
    // ((2*a)*(b/2))%c
    else
        return (2*(s%c)) % c;
}

// Driver code
int main()
{
    ll a = 1000000000007, b = 10000000000005;
    ll c = 1000000000000003;
    printf("%lldn", mulmod(a, b, c));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Compute (a*b)%c
// such that (a%c) * (b%c) can be
// beyond range
// returns (a*b)%c
class GFG {

    static long mulmod(long a, long b, long c) {
        // base case if b==0, return 0
        if (b == 0) {
            return 0;
        }

        // Divide the problem into 2 parts
        long s = mulmod(a, b / 2, c);

        // If b is odd, return
        // (a+(2*a)*((b-1)/2))%c
        if (b % 2 == 1) {
            return (a % c + 2 * (s % c)) % c;
        } // If b is odd, return
        // ((2*a)*(b/2))%c
        else {
            return (2 * (s % c)) % c;
        }
    }

// Driver code
    public static void main(String[] args) {
        long a = 1000000000007L, b = 10000000000005L;
        long c = 1000000000000003L;
        System.out.println((mulmod(a, b, c)));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program of above approach

# returns (a*b)%c
def mulmod(a, b, c):

    # base case if b==0, return 0
    if(b == 0):
        return 0

    # Divide the problem into 2 parts
    s = mulmod(a, b // 2, c)

    # If b is odd, return
    # (a+(2*a)*((b-1)/2))%c
    if(b % 2 == 1):
        return (a % c + 2 * (s % c)) % c

    # If b is odd, return
    # ((2*a)*(b/2))%c
    else:
        return (2 * (s % c)) % c

# Driver code
if __name__=='__main__':
    a = 1000000000007
    b = 10000000000005
    c = 1000000000000003
    print(mulmod(a, b, c))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to Compute (a*b)%c
// such that (a%c) * (b%c) can be
// beyond range
using System;

// returns (a*b)%c
class GFG
{
static long mulmod(long a, long b, long c)
{
    // base case if b==0, return 0
    if (b == 0)
        return 0;

    // Divide the problem into 2 parts
    long s = mulmod(a, b / 2, c);

    // If b is odd, return
    // (a+(2*a)*((b-1)/2))%c
    if (b % 2 == 1)
        return (a % c + 2 * (s % c)) % c;

    // If b is odd, return
    // ((2*a)*(b/2))%c
    else
        return (2 * (s % c)) % c;
}

// Driver code
public static void Main()
{
    long a = 1000000000007, b = 10000000000005;
    long c = 1000000000000003;
    Console.WriteLine(mulmod(a, b, c));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Compute (a*b)%c
// such that (a%c) * (b%c) can be
// beyond range

// returns (a*b)%c
function mulmod($a, $b, $c)
{

    // base case if b==0, return 0
    if ($b==0)
        return 0;

    // Divide the problem into 2 parts
    $s = mulmod($a, $b/2, $c);

    // If b is odd, return
    // (a+(2*a)*((b-1)/2))%c
    if ($b % 2 == 1)
        return ($a % $c + 2 *
           ($s % $c))  %  $c;

    // If b is odd, return
    // ((2*a)*(b/2))%c
    else
        return (2 * ($s % $c)) % $c;
}

    // Driver Code
    $a = 1000000000007;
    $b = 10000000000005;
    $c = 1000000000000003;
    echo mulmod($a, $b, $c);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// javascript program to Compute (a*b)%c
// such that (a%c) * (b%c) can be
// beyond range
// returns (a*b)%c  
function mulmod(a , b , c) {

        // base case if b==0, return 0
        if (b == 0) {
            return 0;
        }

        // Divide the problem into 2 parts
        var s = mulmod(a, parseInt(b / 2), c);

        // If b is odd, return
        // (a+(2*a)*((b-1)/2))%c
        if (b % 2 == 1) {
            return (a % c + 2 * (s % c)) % c;
        }
        // If b is odd, return
        // ((2*a)*(b/2))%c
        else {
            return (2 * (s % c)) % c;
        }
    }

// Driver code
var a = 1000000000007, b = 10000000000005;
var c = 1000000000000003;
document.write((mulmod(a, b, c)));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
74970000000035
```

样品运行见[本](https://ide.geeksforgeeks.org/if7DC4)。
**时间复杂度:** O(log b)
本文由 **Madhur Modi** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息