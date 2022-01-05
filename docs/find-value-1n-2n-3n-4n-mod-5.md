# 找到(1^n + 2^n + 3^n + 4^n ) mod 5

的值

> 原文:[https://www.geeksforgeeks.org/find-value-1n-2n-3n-4n-mod-5/](https://www.geeksforgeeks.org/find-value-1n-2n-3n-4n-mod-5/)

给你一个正整数 n，你要求(1<sup>n</sup>+2<sup>n</sup>+3<sup>n</sup>+4<sup>n</sup>)mod 5 的值。
**注:**n 的值可能非常大，数量级为 10 <sup>15</sup> 。
示例:

```
Input : n = 4
Output : 4
Explanation : (14 + 24 + 34 + 44)mod 5 = (1+16+81+256)mod 5 = 354 mod 5 = 4

Input : n = 2
Output : 0
Explanation : (12 + 22 + 32 + 42)mod 5 = (1+4+9+16)mod 5 = 30 mod 5 = 0
```

**基本方法:**如果你用一个非常基本的方法来解决这个问题，即求(1<sup>n</sup>+2<sup>n</sup>+3<sup>n</sup>+4<sup>n</sup>)的值，然后求其模值为 5，你肯定会得到你的答案，但是对于较大的 n 值，我们肯定得到了错误的答案，因为你将无法存储(1<sup>n</sup>+2<sup>n</sup>+3 <sup>**更好更恰当的方法:**在进行求解之前，让我们先看一下 2，3 的幂的一些周期性性质& 4。</sup> 

*   f(n) = 2 <sup>n</sup> 是 n = 4 的周期，以最后一位数字表示。即 2 <sup>n</sup> 的最后一个数字，总是重复 n 的下一个第四个值(例如:2，4，8，16，32，64…)
*   f(n) = 3 <sup>n</sup> 是 n = 4 的周期，以最后一位数字表示。即 3 <sup>n</sup> 的最后一个数字，总是重复 n 的下一个第四个值(例如:3，9，27，81，243，729…)
*   f(n) = 4 <sup>n</sup> 是 n = 2 的周期，以最后一位数字表示。即 4 <sup>n</sup> 的最后一个数字，总是重复 n 的下一个第二个值(例如:4，16，64，256..)
*   1 <sup>n</sup> 永远是 1，独立于 n。

所以，如果我们仔细寻找 f(n)=(1<sup>n</sup>+2<sup>n</sup>+3<sup>n</sup>+4<sup>n</sup>)的周期性，我们会发现它的周期性也是 4，它的最后一位出现为:

*   对于 n = 1，f(n) = 10
*   对于 n = 2，f(n) = 30
*   对于 n = 3，f(n) = 100
*   对于 n = 4，f(n) = 354
*   对于 n = 5，f(n) = 1300

观察上述周期性，我们可以看到，如果 f(n)%5 的(n%4==0)结果将是 4，其他方面的结果=0。因此，我们不是计算 f(n)的实际值，然后用 mod 5 获得它的值，而是只检查 n 的值

## C++

```
// Program to find value of f(n)%5
#include <bits/stdc++.h>
using namespace std;

// function for obtaining remainder
int fnMod(int n)
{
    // calculate res based on value of n
    return (n % 4) ? 0 : 4;
}

// driver program
int main()
{
    int n = 43;
    cout << fnMod(n) << endl;
    n = 44;
    cout << fnMod(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find value of f(n)% 5

class GFG
{
    // function for obtaining remainder
    static int fnMod(int n)
    {
        // calculate res based on value of n
        return (n % 4 != 0) ? 0 : 4;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 43;
        System.out.println(fnMod(n));
        n = 44;
        System.out.print(fnMod(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# program to find f(n) mod 5
def fnMod (n):
    res = 4 if (n % 4 == 0) else 0
    return res

# driver section
n = 43
print (fnMod(n))
n = 44
print (fnMod(n))
```

## C#

```
// C# Program to find value of f(n) % 5
using System;

class GFG {

    // function for obtaining remainder
    static int fnMod(int n)
    {
        // calculate res based on value of n
        return (n % 4 != 0) ? 0 : 4;
    }

    // Driver code
    public static void Main ()
    {
        int n = 43;
        Console.WriteLine(fnMod(n));
        n = 44;
        Console.Write(fnMod(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find value of f(n)%5

// function for obtaining remainder
function fnMod($n)
{

    // calculate res based
    // on value of n
    return ($n % 4) ? 0 : 4;
}

// Driver Code
{
    $n = 43;
    echo fnMod($n),"\n" ;
    $n = 44;
    echo fnMod($n);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find value of f(n)% 5

// function for obtaining remainder
    function fnMod(n)
    {
        // calculate res based on value of n
        return (n % 4 != 0) ? 0 : 4;
    }

// Driver Code

        let n = 43;
        document.write(fnMod(n) + "<br/>");
        n = 44;
        document.write(fnMod(n)  + "<br/>");

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
0
4
```