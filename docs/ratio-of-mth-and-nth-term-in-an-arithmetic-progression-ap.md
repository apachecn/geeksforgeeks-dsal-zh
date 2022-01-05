# 等差数列中第 n 项和第 m 项的比值

> 原文:[https://www . geesforgeks . org/mth 和第 n 项算术级数比-ap/](https://www.geeksforgeeks.org/ratio-of-mth-and-nth-term-in-an-arithmetic-progression-ap/)

给定两个值“m”和“n ”,算术级数的第五项为零。任务是找出这个 AP 的 mth 和第 n 项的比值。
**例:**

```
Input: m = 10, n = 20
Output: 1/3

Input: m = 10, n = 15
Output: 1/2
```

**接近:** Acc。对于该语句，第五项为零。现在用一个例子来理解这个概念。As A5=a+4*d=0。
现在，我们要求 m =第 10 项和 n =第 20 项的比值。

> A[10]
> = A+9 * d
> = A5+5 * d
> = 0+5 * d
> =**5 * d**
> 同样，A[20]
> = A+19 * d
> = A5+15 * d
> = 0+15 * d
> =**15 * d**
> 现在，我们要找到比例，所以 **Ans= A[10] /**

**下面是需要的实现:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find the ratio
void findRatio(ll m, ll n)
{

    ll Am = m - 5, An = n - 5;

    // divide numerator by gcd to get
    // smallest fractional value
    ll numerator = Am / (__gcd(Am, An));

    // divide denominator by gcd to get
    // smallest fractional value
    ll denominator = An / (__gcd(Am, An));

    cout << numerator << "/" << denominator << endl;
}

// Driver code
int main()
{

    // let d=1 as d doesn't affect ratio
    ll m = 10, n = 20;

    findRatio(m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation of above approach

public class GFG {

    // Function to calculate the GCD
    static int GCD(int a, int b) {
           if (b==0) return a;
           return GCD(b,a%b);
        }

    // Function to find the ratio
    static void findRatio(int m,int  n)
    {
        int Am = m - 5, An = n - 5 ;

        // divide numerator by GCD to get
        // smallest fractional value
        int numerator = Am / GCD(Am, An) ;

        // divide denominator by GCD to get
        // smallest fractional value
        int denominator = An / GCD(Am, An) ;

        System.out.println(numerator + "/" + denominator);
    }
    // Driver code
    public static void main (String args[]){

        // let d=1 as d doesn't affect ratio 
        int m = 10, n = 20;

            findRatio(m, n);

    }

// This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach
# Function to find the ratio

from fractions import gcd
def findRatio(m,n):
    Am = m - 5
    An = n - 5

    # divide numerator by gcd to get
    # smallest fractional value
    numerator=Am//(gcd(Am,An))

    # divide denominator by gcd to get
    #smallest fractional value
    denominator = An // (gcd(Am, An))
    print(numerator,'/',denominator)

# Driver code
# let d=1 as d doesn't affect ratio
if __name__=='__main__':
    m = 10
    n = 20
    findRatio(m, n)

# this code is contributed by sahilshelangia
```

## C#

```
// C# implementation of above approach

using System;
public class GFG {

    // Function to calculate the GCD
    static int GCD(int a, int b) {
           if (b==0) return a;
           return GCD(b,a%b);
        }

    // Function to find the ratio
    static void findRatio(int m,int  n)
    {
        int Am = m - 5, An = n - 5 ;

        // divide numerator by GCD to get
        // smallest fractional value
        int numerator = Am / GCD(Am, An) ;

        // divide denominator by GCD to get
        // smallest fractional value
        int denominator = An / GCD(Am, An) ;

        Console.Write(numerator + "/" + denominator);
    }
    // Driver code
    public static void Main (){

        // let d=1 as d doesn't affect ratio 
        int m = 10, n = 20;

            findRatio(m, n);

    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

function __gcd($a, $b)
{
    if ($b == 0) return $a;
    return __gcd($b, $a % $b);
}

// Function to find the ratio
function findRatio($m, $n)
{
    $Am = $m - 5; $An = $n - 5;

    // divide numerator by gcd to get
    // smallest fractional value
    $numerator = $Am / (__gcd($Am, $An));

    // divide denominator by gcd to
    // get smallest fractional value
    $denominator = $An / (__gcd($Am, $An));

    echo $numerator , "/" ,
         $denominator;
}

// Driver code

// let d=1 as d doesn't affect ratio
$m = 10; $n = 20;

findRatio($m, $n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to calculate the GCD
function GCD(a, b) {
    if (b==0) return a;
    return GCD(b,a%b);
    }

// Function to find the ratio
function findRatio(m,n)
{
    var Am = m - 5, An = n - 5 ;

    // divide numerator by GCD to get
    // smallest fractional value
    var numerator = parseInt(Am / GCD(Am, An)) ;

    // divide denominator by GCD to get
    // smallest fractional value
    var denominator = parseInt(An / GCD(Am, An));

    document.write(numerator + "/" + denominator);
}
// Driver code
// let d=1 as d doesn't affect ratio
var m = 10, n = 20;

findRatio(m, n);

</script>
```

**Output:** 

```
1/3
```