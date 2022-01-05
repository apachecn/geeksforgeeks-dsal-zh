# 通过关联操作将 n 个元素相乘的方法

> 原文:[https://www . geesforgeks . org/way-multiple-n-elements-associated-operation/](https://www.geeksforgeeks.org/ways-multiply-n-elements-associative-operation/)

给定一个数字 n，找出用关联运算相乘 n 个元素的方法。
**例:**

```
Input : 2
Output : 2
For a and b there are two ways to multiply them.
1\. (a * b)        
2\. (b * a)

Input : 3
Output : 12
```

**说明(例 2) :**

```
For a, b and c there are 12 ways to multiply them.
1\.  ((a * b) * c)     2\.  (a * (b * c))
3\.  ((a * c) * b)     4\.  (a * (c * b))
5\.  ((b * a) * c)     6\.  (b * (a * c))
7\.  ((b * c) * a)     8\.  (b * (c * a))
9\.  ((c * a) * b)     10\.  (c * (a * b))
11\.  ((c * b) * a)    12\.  (c * (b * a))
```

**方法:**首先，我们尝试找出递归关系。从上面的例子中，我们可以看到 h(1) = 1，h(2) = 2，h(3) = 12。现在，对于 n 个元素，将有 n–1 次乘法和 n–1 个括号。并且，(a1，a2，…，an)可以从(a1，a2，…，a(n-1))以两种方式之一获得:

1.  取一个乘法(a1，a2，…，a(n–1))(它有 n–2 个乘法和 n–2 个括号)，在 n–2 个乘法中的一个中，在任一因子的任一侧插入第 n 个元素“an”。因此，对于 n–1 个数字的每个方案，以这种方式给出 n 个数字的 2 * 2 *(n–2)= 4 *(n–2)个方案。
2.  对(a1，a2，..，a(n-1))并在左边或右边乘以(' an ')。因此，对于 n–1 个数字的每个方案，以这种方式给出 n 个数字的两个方案。

所以把上面两个相加，我们得到，h(n)=(4 * n–8+2)* h(n–1)，h(n)=(4 * n–6)* h(n–1)。这个初始值相同的递推关系由伪加泰罗尼亚数满足。因此，h(n)=(2 * n–2)！/(n–1)！

## C++

```
// C++ code to find number of ways to multiply n
// elements with an associative operation
# include <bits/stdc++.h>
using namespace std;

// Function to find the required factorial
int fact(int n)
{
    if (n == 0 || n == 1)   
        return 1 ;

    int ans = 1;  
    for (int i = 1 ; i <= n; i++)   
        ans = ans * i ;

    return ans ;
}

// Function to find nCr
int nCr(int n, int r)
{
    int Nr = n , Dr = 1 , ans = 1;
    for (int i = 1 ; i <= r ; i++ ) {
        ans = ( ans * Nr ) / ( Dr ) ;
        Nr-- ;
        Dr++ ;
    }
    return ans ;
}

// function to find the number of ways
int solve ( int n )
{
    int N = 2*n - 2 ;
    int R = n - 1 ;   
    return nCr (N, R) * fact(n - 1) ;
}

// Driver code
int main()
{
    int n = 6 ;
    cout << solve (n) ;   
    return 0 ;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find number of
// ways to multiply n elements
// with an associative operation
import java.io.*;

class GFG
{
// Function to find the
// required factorial
static int fact(int n)
{
    if (n == 0 || n == 1)
        return 1 ;

    int ans = 1;
    for (int i = 1 ; i <= n; i++)
        ans = ans * i ;

    return ans ;
}

// Function to find nCr
static int nCr(int n, int r)
{
    int Nr = n , Dr = 1 , ans = 1;
    for (int i = 1 ; i <= r ; i++ )
    {
        ans = ( ans * Nr ) / ( Dr ) ;
        Nr-- ;
        Dr++ ;
    }
    return ans ;
}

// function to find
// the number of ways
static int solve ( int n )
{
    int N = 2 * n - 2 ;
    int R = n - 1 ;
    return nCr (N, R) * fact(n - 1) ;
}

// Driver Code
public static void main (String[] args)
{
int n = 6 ;
System.out.println( solve (n)) ;
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 code to find number
# of ways to multiply n
# elements with an
# associative operation

# Function to find the
# required factorial
def fact(n):
    if (n == 0 or n == 1):
        return 1;

    ans = 1;
    for i in range(1, n + 1):
        ans = ans * i;

    return ans;

# Function to find nCr
def nCr(n, r):
    Nr = n ; Dr = 1 ; ans = 1;
    for i in range(1, r + 1):
        ans = int((ans * Nr) / (Dr));
        Nr = Nr - 1;
        Dr = Dr + 1;
    return ans;

# function to find
# the number of ways
def solve ( n ):
    N = 2* n - 2;
    R = n - 1 ;
    return (nCr (N, R) *
            fact(n - 1));

# Driver code
n = 6 ;
print(solve (n) );

# This code is contributed
# by mits
```

## C#

```
// C# code to find number of
// ways to multiply n elements
// with an associative operation
using System;

class GFG {

    // Function to find the
    // required factorial
    static int fact(int n)
    {
        if (n == 0 || n == 1)
            return 1 ;

        int ans = 1;
        for (int i = 1 ; i <= n; i++)
            ans = ans * i ;

        return ans ;
    }

    // Function to find nCr
    static int nCr(int n, int r)
    {
        int Nr = n , Dr = 1 , ans = 1;
        for (int i = 1 ; i <= r ; i++ )
        {
            ans = ( ans * Nr ) / ( Dr ) ;
            Nr-- ;
            Dr++ ;
        }
        return ans ;
    }

    // function to find
    // the number of ways
    static int solve ( int n )
    {
        int N = 2 * n - 2 ;
        int R = n - 1 ;
        return nCr (N, R) * fact(n - 1) ;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 6 ;
        Console.WriteLine( solve (n)) ;
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find number
// of ways to multiply n
// elements with an
// associative operation

// Function to find the
// required factorial
function fact($n)
{
    if ($n == 0 || $n == 1)
        return 1;

    $ans = 1;
    for ($i = 1 ; $i <= $n; $i++)
        $ans = $ans * $i;

    return $ans;
}

// Function to find nCr
function nCr($n, $r)
{
    $Nr = $n ; $Dr = 1 ; $ans = 1;
    for ($i = 1 ; $i <= $r ; $i++ )
    {
        $ans = ($ans * $Nr) /
                      ($Dr);
        $Nr--;
        $Dr++;
    }
    return $ans ;
}

// function to find
// the number of ways
function solve ( $n )
{
    $N = 2* $n - 2 ;
    $R = $n - 1 ;
    return nCr ($N, $R) *
           fact($n - 1) ;
}

// Driver code
$n = 6 ;
echo solve ($n) ;

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// Javascript code to find number of
// ways to multiply n elements
// with an associative operation

// Function to find the
// required factorial
function fact(n)
{
    if (n == 0 || n == 1)
        return 1;

    let ans = 1;
    for(let i = 1 ; i <= n; i++)
        ans = ans * i;

    return ans;
}

// Function to find nCr
function nCr(n, r)
{
    let Nr = n , Dr = 1 , ans = 1;
    for(let i = 1 ; i <= r ; i++)
    {
        ans = parseInt((ans * Nr) / (Dr), 10);
        Nr--;
        Dr++;
    }
    return ans;
}

// Function to find
// the number of ways
function solve(n)
{
    let N = 2 * n - 2;
    let R = n - 1;
    return nCr (N, R) * fact(n - 1);
}

// Driver code
let n = 6;
document.write(solve(n));

// This code is contributed by decode2207

</script>
```

**Output :** 

```
30240
```