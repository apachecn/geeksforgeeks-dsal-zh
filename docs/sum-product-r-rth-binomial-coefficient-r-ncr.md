# r 与 rth 二项式系数(r * nCr)乘积之和

> 原文:[https://www . geesforgeks . org/sum-product-r-rth-二项式-系数-r-ncr/](https://www.geeksforgeeks.org/sum-product-r-rth-binomial-coefficient-r-ncr/)

给定正整数 **n** 。任务是求 r 和 r 的乘积之和 <sup>th</sup> 二项式系数。换句话说就是找:**σ(r *<sup>n</sup>C<sub>r</sub>)**，其中 0 < = r < = n.
**例:**

```
Input : n = 2
Output : 4
0.2C0 + 1.2C1 + 2.2C2
= 0*2 + 1*2 + 2*1
= 4

Input : n = 5
Output : 80
```

**方法 1(蛮力):**思路是从 0 到 n 迭代一个循环 I，求 i * <sup>n</sup> C <sub>i</sub> 加和变量。
以下是该方法的实现:

## C++

```
// CPP Program to find sum of product of r and
// rth Binomial Coefficient i.e summation r * nCr
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Return the first n term of binomial coefficient.
void binomialCoeff(int n, int C[])
{
    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++) {

        // Compute next row of pascal triangle
        // using the previous row
        for (int j = min(i, n); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
}

// Return summation of r * nCr
int summation(int n)
{
    int C[MAX];
    memset(C, 0, sizeof(C));

    // finding the first n term of binomial
    // coefficient
    binomialCoeff(n, C);

    // Iterate a loop to find the sum.
    int sum = 0;
    for (int i = 0; i <= n; i++)
        sum += (i * C[i]);   

    return sum;
}

// Driven Program
int main()
{
    int n = 2;
    cout << summation(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum
// of product of r and rth
// Binomial Coefficient i.e
// summation r * nCr
class GFG
{
static int MAX = 100;

// Return the first n term
// of binomial coefficient.
static void binomialCoeff(int n,
                          int C[])
{
    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++)
    {

        // Compute next row of
        // pascal triangle using
        // the previous row
        for (int j = Math.min(i, n); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
}

// Return summation
// of r * nCr
static int summation(int n)
{
    int C[] = new int[MAX];

    for(int i = 0; i < MAX; i++)
    C[i] = 0;

    // finding the first n term 
    // of binomial coefficient
    binomialCoeff(n, C);

    // Iterate a loop
    // to find the sum.
    int sum = 0;
    for (int i = 0; i <= n; i++)
        sum += (i * C[i]);

    return sum;
}

// Driver Code
public static void main(String args[])
{
    int n = 2;
    System.out.println( summation(n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 Program to find sum of product
# of r and rth Binomial Coefficient i.e
# summation r * nCr
MAX = 100

# Return the first n term of
# binomial coefficient.
def binomialCoeff(n, C):

    C[0] = 1 # nC0 is 1

    for i in range(1, n + 1):

        # Compute next row of pascal triangle
        # using the previous row
        for j in range(min(i, n), -1, -1):
            C[j] = C[j] + C[j - 1]

# Return summation of r * nCr
def summation( n):

    C = [0] * MAX

    # finding the first n term of
    # binomial coefficient
    binomialCoeff(n, C)

    # Iterate a loop to find the sum.
    sum = 0
    for i in range(n + 1):
        sum += (i * C[i])

    return sum

# Driver Code
if __name__ == "__main__":

    n = 2
    print(summation(n))

# This code is contributed by ita_c
```

## C#

```
// C# Program to find sum
// of product of r and rth
// Binomial Coefficient i.e
// summation r * nCr
using System;

class GFG
{
static int MAX = 100;

// Return the first n term
// of binomial coefficient.
static void binomialCoeff(int n,
                          int []C)
{
    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++)
    {

        // Compute next row of
        // pascal triangle using
        // the previous row
        for (int j = Math.Min(i, n);
                 j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
}

// Return summation
// of r * nCr
static int summation(int n)
{
    int []C = new int[MAX];

    for(int i = 0; i < MAX; i++)
    C[i] = 0;

    // finding the first n term
    // of binomial coefficient
    binomialCoeff(n, C);

    // Iterate a loop
    // to find the sum.
    int sum = 0;
    for (int i = 0; i <= n; i++)
        sum += (i * C[i]);

    return sum;
}

// Driver Code
public static void Main()
{
    int n = 2;
    Console.Write( summation(n));
}
}

// This code is contributed
// by shiv_bhakt
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of product
// of r and rth Binomial Coefficient
// i.e summation r * nCr
$MAX = 100;

// Return the first n term of
// binomial coefficient.
function binomialCoeff($n, &$C)
{
    $C[0] = 1; // nC0 is 1

    for ($i = 1; $i <= $n; $i++)
    {

        // Compute next row of pascal triangle
        // using the previous row
        for ($j = min($i, $n); $j > 0; $j--)
            $C[$j] = $C[$j] + $C[$j - 1];
    }
}

// Return summation of r * nCr
function summation($n)
{
    global $MAX;
    $C = array_fill(0, $MAX, 0);

    // finding the first n term of
    // binomial coefficient
    binomialCoeff($n, $C);

    // Iterate a loop to find the sum.
    $sum = 0;
    for ($i = 0; $i <= $n; $i++)
        $sum += ($i * $C[$i]);

    return $sum;
}

// Driver Code
$n = 2;
echo summation($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find sum of product of r and
    // rth Binomial Coefficient i.e summation r * nCr
    MAX = 100

    // Return the first n term of binomial coefficient.
    function binomialCoeff(n, C) {
      C[0] = 1; // nC0 is 1

      for (var i = 1; i <= n; i++) {

        // Compute next row of pascal triangle
        // using the previous row
        for (var j = Math.min(i, n); j > 0; j--)
          C[j] = C[j] + C[j - 1];
      }
    }

    // Return summation of r * nCr
    function summation(n) {
      C = Array(MAX).fill(0);

      // finding the first n term of binomial
      // coefficient
      binomialCoeff(n, C);

      // Iterate a loop to find the sum.
      var sum = 0;
      for (var i = 0; i <= n; i++)
        sum += (i * C[i]);

      return sum;
    }

    // Driven Program
    var n = 2;
    document.write(summation(n));

    // This code is contributed by noob2000.
  </script>
```

**Output:** 

```
4
```

**方法二(使用公式):**
数学上我们需要找到，
σ(I *<sup>n</sup>C<sub>I</sub>，其中 0<= I<= n
=σ(<sup>I</sup>C<sub>1</sub>*<sup>n</sup>C<sub>I</sub>)，(自<sup>n</sup>C<sub>1【t2t/(I–1)！* 1!)* (n！/(n–I)！*我！)
关于取消 I！从分子和分母
=σ(n！/(I–1)！*(n–I)！)
=σn *(n–1)！/(I–1)！*(n–I)！)
(使用 <sup>n</sup> C <sub>r</sub> 的反向= (n)！/ (r)！*(n–r)！)
= n *σ<sup>n–1</sup>C<sub>r–1</sub>
= n * 2<sup>n–1</sup>(自σ<sup>n</sup>C<sub>r</sub>= 2<sup>n</sup>)
以下为本办法执行情况:</sub> 

## C++

```
// CPP Program to find sum of product of r and
// rth Binomial Coefficient i.e summation r * nCr
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Return summation of r * nCr
int summation(int n)
{
    return n << (n - 1);
}

// Driven Program
int main()
{
    int n = 2;
    cout << summation(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of product of
// r and rth Binomial Coefficient i.e
// summation r * nCr
import java.io.*;

class GFG {

    static int MAX = 100;

    // Return summation of r * nCr
    static int summation(int n)
    {
        return n << (n - 1);
    }

    // Driven Program
    public static void main (String[] args)
    {
        int n = 2;
        System.out.println( summation(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to
# find sum of product
# of r and rth Binomial
# Coefficient i.e
# summation r * nCr

# Return summation
# of r * nCr
def summation( n):
    return n << (n - 1);

# Driver Code
n = 2;
print(summation(n));

# This code is contributed
# by mits
```

## C#

```
// C# Program to find sum of product of
// r and rth Binomial Coefficient i.e
// summation r * nCr
using System;

class GFG {

    //static int MAX = 100;

    // Return summation of r * nCr
    static int summation(int n)
    {
        return n << (n - 1);
    }

    // Driver Code
    public static void Main ()
    {
        int n = 2;
        Console.WriteLine( summation(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum
// of product of r and
// rth Binomial Coefficient
// i.e summation r * nCr

// Return summation of r * nCr
function summation( $n)
{
    return $n << ($n - 1);
}

// Driver Code
$n = 2;
echo summation($n) ;

// This code is contributed
// by shiv_bhakt
?>
```

## java 描述语言

```
<script>

// Javascript Program to find sum of product of r and
// rth Binomial Coefficient i.e summation r * nCr
var MAX=100

// Return summation of r * nCr
function summation(n)
{
    return n << (n - 1);
}

// Driven Program
var n = 2;
document.write(summation(n));

</script>
```

**Output:** 

```
4
```