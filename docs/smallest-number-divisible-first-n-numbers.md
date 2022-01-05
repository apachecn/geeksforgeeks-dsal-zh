# 可被前 n 个数字整除的最小数字

> 原文:[https://www . geeksforgeeks . org/最小可除数第一 n 位数字/](https://www.geeksforgeeks.org/smallest-number-divisible-first-n-numbers/)

给定一个数 **n** 找到能被 1 到 n 整除的最小数
**举例:**

```
Input : n = 4
Output : 12
Explanation : 12 is the smallest numbers divisible
              by all numbers from 1 to 4

Input : n = 10
Output : 2520

Input :  n = 20
Output : 232792560
```

如果你仔细观察**和**一定是数字 1 到 n 的 **LCM。
寻找从 1 到 n 的数的 LCM–** 

1.  初始化 ans = 1。

2.  迭代从 i = 1 到 i = n 的所有数字。在第 I 次迭代中 **ans = LCM(1，2，…..，我)**。这可以通过 **LCM(1，2，…)轻松完成。，i) = LCM(ans，i)** 。
    因此在第一次迭代中，我们只需要做–

```
ans = LCM(ans, i) 
         = ans * i / gcd(ans, i) [Using the below property,
                                 a*b = gcd(a,b) * lcm(a,b)]
```

**注意:**在 C++代码中，答案很快就超过了整数限制，甚至是超长限制。
下面是逻辑的实现。

## C++

```
// C++ program to find smallest number evenly divisible by
// all numbers 1 to n
#include<bits/stdc++.h>
using namespace std;

// Function returns the lcm of first n numbers
long long lcm(long long n)
{
    long long ans = 1;   
    for (long long i = 1; i <= n; i++)
        ans = (ans * i)/(__gcd(ans, i));
    return ans;
}

// Driver program to test the above function
int main()
{
    long long n = 20;
    cout << lcm(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest number evenly divisible by
// all numbers 1 to n

 class GFG{

static long gcd(long a, long b)
{
   if(a%b != 0)
      return gcd(b,a%b);
   else
      return b;
}

// Function returns the lcm of first n numbers
static long lcm(long n)
{
    long ans = 1;   
    for (long i = 1; i <= n; i++)
        ans = (ans * i)/(gcd(ans, i));
    return ans;
}

// Driver program to test the above function
public static void main(String []args)
{
    long n = 20;
    System.out.println(lcm(n));

}
}
```

## C#

```
// C#  program to find smallest number
// evenly divisible by
// all numbers 1 to n
using System;

public class GFG{
    static long gcd(long a, long b)
{
if(a%b != 0)
    return gcd(b,a%b);
else
    return b;
}

// Function returns the lcm of first n numbers
static long lcm(long n)
{
    long ans = 1;    
    for (long i = 1; i <= n; i++)
        ans = (ans * i)/(gcd(ans, i));
    return ans;
}

// Driver program to test the above function
    static public void Main (){
        long n = 20;
        Console.WriteLine(lcm(n));
    }
//This code is contributed by akt_mit   
}
```

## 蟒蛇 3

```
# Python program to find the smallest number evenly 
# divisible by all number 1 to n
import math

# Returns the lcm of first n numbers
def lcm(n):
    ans = 1
    for i in range(1, n + 1):
        ans = int((ans * i)/math.gcd(ans, i))        
    return ans

# main
n = 20
print (lcm(n))
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Note: This code is not working on GFG-IDE
// because gmp libraries are not supported

// PHP program to find smallest number
// evenly divisible by all numbers 1 to n

// Function returns the lcm
// of first n numbers
function lcm($n)
{
    $ans = 1;
    for ($i = 1; $i <= $n; $i++)
        $ans = ($ans * $i) / (gmp_gcd(strval(ans),
                                      strval(i)));
    return $ans;
}

// Driver Code
$n = 20;
echo lcm($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the smallest number evenly divisible by
// all numbers 1 to n

function gcd(a, b)
{
   if(a%b != 0)
      return gcd(b,a%b);
   else
      return b;
}

// Function returns the lcm of first n numbers
function lcm(n)
{
    let ans = 1;   
    for (let i = 1; i <= n; i++)
        ans = (ans * i)/(gcd(ans, i));
    return ans;
}

// function call

    let n = 20;
    document.write(lcm(n));

</script>
```

**输出:**

```
232792560
```

上述解决方案适用于单个输入。但是如果我们有多个输入，使用厄拉多塞筛来存储所有质因数是一个好主意。请参考以下文章了解基于筛子的方法。
[前 n 个自然数的 LCM](https://www.geeksforgeeks.org/lcm-first-n-natural-numbers/)
本文由 [**阿尤什·坎德里**](https://in.linkedin.com/in/ayush-khanduri-b4ab87106) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。