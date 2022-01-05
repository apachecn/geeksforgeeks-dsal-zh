# 前 n 个奇数自然数的四次幂之和

> 原文:[https://www . geesforgeks . org/sum-四次幂-一次-n-奇数-自然数/](https://www.geeksforgeeks.org/sum-fourth-power-first-n-odd-natural-numbers/)

写一个程序求前 n 个奇数自然数的四次幂之和。
1<sup>4</sup>+3<sup>4</sup>+5<sup>4</sup>+7<sup>4</sup>+9<sup>4</sup>+11<sup>4</sup>……。+(2n-1) <sup>4</sup> 。
示例:

```
Input  :   3
Output :   707
14 +34 +54 =  707
Input  :   6
Output :   24310
14 + 34 + 54 + 74 + 94 + 114 
```

天真的方法:-在这个简单的寻找前 n 个奇数自然数的四次方是迭代一个从 1 到 n 次的循环，结果存储在变量 sum 中。
Ex。-n=3 那么，(1 * 1 * 1 * 1)+(3 * 3 * 3 * 3)+(5 * 5 * 5 * 5)= 707

## C++

```
// CPP Program to find the sum of fourth powers
// of first n odd natural numbers
#include <bits/stdc++.h>
using namespace std;

// calculate the sum of fourth power of first
// n odd natural numbers
long long int oddNumSum(int n)
{
    int j = 0;
    long long int sum = 0;
    for (int i = 1; i <= n; i++) {
        j = (2 * i - 1);
        sum = sum + (j * j * j * j);
    }
    return sum;
}

// Driven Program
int main()
{
    int n = 6;
    cout << oddNumSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// sum of fourth powers of
// first n odd natural numbers
import java.io.*;

class GFG {

    // calculate the sum of
    // fourth power of first
    // n odd natural numbers
    static long oddNumSum(int n)
    {
        int j = 0;
        long sum = 0;
        for (int i = 1; i <= n; i++) {
            j = (2 * i - 1);
            sum = sum + (j * j * j * j);
        }
        return sum;
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 6;
        System.out.println(oddNumSum(n));
    }
}

// This code is contributed
// by Nikita tiwari.
```

## 蟒蛇 3

```
# Python 3 Program to find the
# sum of fourth powers of
# first n odd natural numbers

# calculate the sum of
# fourth power of first 
# n odd natural numbers
def oddNumSum(n) :
    j = 0
    sm = 0
    for i in range(1, n + 1) :
        j = (2 * i - 1)
        sm = sm + (j * j * j * j)

    return sm

# Driven Program
n = 6;
print(oddNumSum(n))

# This code is contributed
# by Nikita tiwari.
```

## C#

```
// C# Program to find the
// sum of fourth powers of
// first n odd natural numbers
using System;

class GFG {

    // calculate the sum of
    // fourth power of first
    // n odd natural numbers
    static long oddNumSum(int n)
    {
        int j = 0;
        long sum = 0;
        for (int i = 1; i <= n; i++) {
            j = (2 * i - 1);
            sum = sum + (j * j * j * j);
        }
        return sum;
    }

    // Driven Program
    public static void Main()
    {
        int n = 6;
        Console.Write(oddNumSum(n));
    }
}

// This code is contributed by
// vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// sum of fourth powers
// of first n odd natural
// numbers

// calculate the sum of
// fourth power of first
// n odd natural numbers
function oddNumSum($n)
{
    $j = 0;
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
    {
        $j = (2 * $i - 1);
        $sum = $sum + ($j * $j * $j * $j);
    }
    return $sum;
}

// Driver Code
$n = 6;
echo(oddNumSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript Program to find the sum of fourth powers
// of first n odd natural numbers

// calculate the sum of fourth power of first
// n odd natural numbers
function oddNumSum( n)
{
    let j = 0;
    let sum = 0;
    for (let i = 1; i <= n; i++) {
        j = (2 * i - 1);
        sum = sum + (j * j * j * j);
    }
    return sum;
}

// Driven Program

    let n = 6;
     document.write(oddNumSum(n));

// This code contributed by aashish1995

</script>
```

**输出:**

```
24310
```

**时间复杂度:O(N)**
**有效方法:-** 一个有效的解决方案是使用直接的数学公式，即:

> [四次方自然数](https://www.geeksforgeeks.org/sum-fourth-powers-first-n-natural-numbers/)=(1<sup>4</sup>+2<sup>4</sup>+3<sup>4</sup>+…………+n<sup>4</sup>)
> =(n(n+1)(2n+1)(3n<sup>2</sup>+3n-1))/30
> [四次方偶数自然数](https://www.geeksforgeeks.org/sum-of-fourth-power-of-first-n-even-natural-numbers/)=(2<sup>4</sup>+4<sup>4【T14
> 我们需要奇数，所以我们减去
> (四次幂奇数自然数)=(四次幂前 n 自然数)–(四次幂偶数自然数)
> =(1<sup>4</sup>+2<sup>4</sup>+3<sup>4</sup>+……+n<sup>4</sup>–(2<sup>4</sup>+4<sup>4</sup>+6<sup>4</sup>
> =(1<sup>4</sup>+3<sup>4</sup>+5<sup>4</sup>+…………+(2n-1)<sup>4</sup>)
> 驱动公式
> =(2n(2n+1)(4n+1)(12n<sup>2</sup>+6n-1))/30 –( 8(n(n+1)(2n+1)(3n<sup>2</sup> –(24n<sup>3</sup>+24n<sup>2</sup>–8n+24n<sup>2</sup>+24n-8】】
> = n(2n+1)/15【24n<sup>3</sup>–12n<sup>2</sup>–14n+7】</sup> 
> 
> ```
>     Sum of fourth power of first n odd numbers =  n(2n+1)/15[24n3 - 12n2 - 14n + 7]
> ```

## C++

```
// CPP Program to find the sum of fourth powers
// of first n odd natural numbers
#include <bits/stdc++.h>
using namespace std;

// calculate the sum of fourth power of first
// n odd natural numbers
long long int oddNumSum(int n)
{
    return (n * (2 * n + 1) *
    (24 * n * n * n - 12 * n
    * n - 14 * n + 7)) / 15;
}

// Driven Program
int main()
{
    int n = 4;
    cout << oddNumSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the sum of
// fourth powers of first n odd
// natural numbers
class GFG {

    // calculate the sum of fourth
    // power of first n odd natural
    // numbers
    static long oddNumSum(int n)
    {
        return (n * (2 * n + 1) *
         (24 * n * n * n - 12 * n
          * n - 14 * n + 7)) / 15;
    }

    // Driven Program
    public static void main(String[] args)
    {
        int n = 4;

        System.out.println(oddNumSum(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python 3 Program to find the
# sum of fourth powers of first
# n odd natural numbers

# calculate the sum of fourth
# power of first n odd natural
#numbers
def oddNumSum(n):

    return (n * (2 * n + 1) *
      (24 * n * n * n - 12 * n
      * n - 14 * n + 7)) / 15

# Driven Program
n = 4
print(int(oddNumSum(n)))

# This code is contributed by
# Smitha Dinesh Semwal.
```

## C#

```
// C# Program to find the sum of
// fourth powers of first n
// odd natural numbers
using System;

class GFG {

    // calculate the sum of fourth
    // power of first n odd
    // natural numbers
    static long oddNumSum(int n)
    {
        return (n * (2 * n + 1) *
        (24 * n * n * n - 12 * n
        * n - 14 * n + 7)) / 15;
    }

    // Driven Program
    public static void Main()
    {
        int n = 4;
        Console.Write(oddNumSum(n));
    }
}

// This code is contributed by
// vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// sum of fourth powers
// of first n odd natural
// numbers

// calculate the sum of
// fourth power of first
// n odd natural numbers
function oddNumSum($n)
{
    return ($n * (2 * $n + 1) *
           (24 * $n * $n * $n -
            12 * $n * $n - 14 *
            $n + 7)) / 15;
}

// Driver Code
$n = 4;
echo(oddNumSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript Program to find the sum of
// fourth powers of first n odd
// natural numbers

// calculate the sum of fourth
// power of first n odd natural
// numbers
function oddNumSum(n)
{
    return (n * (2 * n + 1) *
     (24 * n * n * n - 12 * n
      * n - 14 * n + 7)) / 15;
}

// Driven Program
var n = 4;

document.write(oddNumSum(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
  3108
```

**时间复杂度:O(1)**