# 方程 x1 + x2 +的积分解的个数。+ xN = k

> 原文:[https://www . geesforgeks . org/方程式积分解的数量-x1-x2-xn-k/](https://www.geeksforgeeks.org/number-of-integral-solutions-of-the-equation-x1-x2-xn-k/)

给定 N 和 k，任务是计算一个具有 N 个变量的线性方程的积分解的个数，如下所示:

> x1+x2+x3 .+xn-1++xn = k

**示例** :

```
Input: N = 3, K = 3
Output: 10

Input: N = 2, K = 2
Output: 3
```

**方法:**这个问题可以用排列组合的概念来解决。下面是分别求非负积分解和正积分解的直接公式。

> 方程 x1 + x2 + …… + xn = k 的非负积分解个数由 **(n+k-1)给出！/ (n-1)！*k！。**
> 方程 x1 + x2 +的正整数解的个数…..+ xn = k 由 **(k-1)给出！/ (n-1)！* (k-n)！。**

以下是上述方法的实现:

## c++

```
// C++ program for above implementation
#include<iostream>

using namespace std ;

int nCr(int n, int r)
{
    int fac[100] = {1} ;

    for (int i = 1 ; i < n + 1 ; i++)
    {
        fac[i] = fac[i - 1] * i ;
    }

    int ans = fac[n] / (fac[n - r] *
                        fac[r]) ;
    return ans ;
}

// Driver Code
int main()
{
    int n = 3 ;
    int k = 3 ;

    int ans = nCr(n + k - 1 , k) +
              nCr(k - 1, n - 1);

    cout << ans ;

    return 0 ;
}

// This code is contributed
// by ANKITRAI1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation
import java.io.*;

class GFG
{
static int nCr(int n, int r)
{
    int fac[] = new int[100] ;
    for(int i = 0; i < n; i++)
    fac[i] = 1;

    for (int i = 1 ; i < n + 1 ; i++)
    {
        fac[i] = fac[i - 1] * i ;
    }

    int ans = fac[n] / (fac[n - r] *
                        fac[r]);
    return ans ;
}

// Driver Code
public static void main (String[] args)
{
    int n = 3 ;
    int k = 3 ;

    int ans = nCr(n + k - 1 , k) +
              nCr(k - 1, n - 1);

    System.out.println(ans) ;
}
}

// This code is contributed
// by anuj_67
```

## 蟒蛇 3

```
# Python implementation of
# above approach

# Calculate nCr i.e binomial
# cofficent nCr = n !/(r !*(n-r)!)
def nCr(n, r):

    # first find factorial
    # upto n
    fac = list()
    fac.append(1)
    for i in range(1, n + 1):
        fac.append(fac[i - 1] * i)

    # use nCr formula
    ans = fac[n] / (fac[n - r] * fac[r])
    return ans

# n = number of variables
n = 3

# sum of n variables = k
k = 3

# find number of solutions
ans = nCr(n + k - 1, k) + nCr(k - 1, n - 1)

print(ans)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program for above implementation
using System;

class GFG
{
static int nCr(int n, int r)
{
    int[] fac = new int[100] ;
    for(int i = 0; i < n; i++)
    fac[i] = 1;

    for (int i = 1 ; i < n + 1 ; i++)
    {
        fac[i] = fac[i - 1] * i ;
    }

    int ans = fac[n] / (fac[n - r] *
                        fac[r]);
    return ans ;
}

// Driver Code
public static void Main ()
{
    int n = 3 ;
    int k = 3 ;

    int ans = nCr(n + k - 1 , k) +
              nCr(k - 1, n - 1);

    Console.Write(ans) ;
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Calculate nCr i.e binomial
// cofficent nCr = n !/(r !*(n-r)!)
function nCr($n, $r)
{
    // first find factorial
    // upto n
    $fac = array();
    array_push($fac, 1);
    for($i = 1; $i < $n + 1; $i++)
        array_push($fac, $fac[$i - 1] * $i);

    // use nCr formula
    $ans = $fac[$n] / ($fac[$n - $r] *
                       $fac[$r]);
    return $ans;
}

// Driver Code

// n = number of variables
$n = 3;

// sum of n variables = k
$k = 3;

// find number of solutions
$ans = nCr($n + $k - 1, $k) +
       nCr($k - 1, $n - 1);

print($ans);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for above implementation
function nCr(n, r)
{
    var fac = Array(100).fill(1);

    for (var i = 1 ; i < n + 1 ; i++)
    {
        fac[i] = fac[i - 1] * i ;
    }

    var ans = fac[n] / (fac[n - r] *
                        fac[r]) ;
    return ans ;
}

// Driver Code
var n = 3 ;
var k = 3 ;

var ans = nCr(n + k - 1 , k) +
        nCr(k - 1, n - 1);

document.write(ans );

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
11.0
```

**上述概念的应用:**

1.  方程 x1 + x2 +…+ xn = k 的非负积分解的个数等于 k 个相同球可以分布成 N 个唯一盒子的方式个数。
2.  方程 x1 + x2 + … + xn = k 的正整数解的个数等于 k 个相同的球可以被分配到 N 个唯一的盒子中的方式的个数，使得每个盒子必须包含至少-1 个球。