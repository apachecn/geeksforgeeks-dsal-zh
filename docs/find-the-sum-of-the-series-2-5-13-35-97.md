# 求数列 2、5、13、35、97 的和……

> 原文:[https://www . geesforgeks . org/find-the-sum-the-series-2-5-13-35-97/](https://www.geeksforgeeks.org/find-the-sum-of-the-series-2-5-13-35-97/)

给定一个数列和一个数 n，任务是求其前 n 项的和。下面是系列:

> 2, 5, 13, 35, 97, …

**例:**

```
Input: N = 2
Output: 7
The sum of first 2 terms of Series is
2 + 5 = 7

Input: N = 4
Output: 55
The sum of first 4 terms of Series is
2 + 5 + 13 + 35 = 55
```

**方法:**从这个给定的数列中，我们发现它是两个具有共同比率 2，3 的 **GP** 数列的和。

> sn = 2+5+13+35+97……+第 n 项
> sn =(2^0+3^ 0)+(2^1+3^1)+(2^2+3^2)+(2^3+3^3)+(+3 4)……+第 n 项
> sn =(2 0+2 1+2 2+2 3+2 4……+第 n 项)+(3 0+3 1+3 2+3……+第 n 项)

因为，我们知道 **GP** 的 n 项之和由以下公式给出:

![$ S_n=\frac{a(r^n-1)}{(r-1)} $   ](img/fbcda96639c851f33cf2f396cb2ac607.png "Rendered by QuickLaTeX.com")

**以下是上述方法的实施:**

## C++

```
// C++ program for finding the sum
// of first N terms of the series.
#include <bits/stdc++.h>
using namespace std;

// CalculateSum function returns the final sum
int calculateSum(int n)
{
    // r1 and r2 are common ratios
    // of 1st and 2nd series
    int r1 = 2, r2 = 3;

    // a1 and a2 are common first terms
    // of 1st and 2nd series
    int a1 = 1, a2 = 1;

    return a1 * (pow(r1, n) - 1) / (r1 - 1)
           + a2 * (pow(r2, n) - 1) / (r2 - 1);
}

// Driver code
int main()
{
    int n = 4;

    // function calling for 4 terms
    cout << "Sum = " << calculateSum(n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program for finding the sum
//of first N terms of the series.

public class GFG {

    //CalculateSum function returns the final sum
    static int calculateSum(int n)
    {
     // r1 and r2 are common ratios
     // of 1st and 2nd series
     int r1 = 2, r2 = 3;

     // a1 and a2 are common first terms
     // of 1st and 2nd series
     int a1 = 1, a2 = 1;

     return (int)(a1 * (Math.pow(r1, n) - 1) / (r1 - 1)
            + a2 * (Math.pow(r2, n) - 1) / (r2 - 1));
    }

    //Driver code
    public static void main(String[] args) {

        int n = 4;

         // function calling for 4 terms
         System.out.println("Sum = " +calculateSum(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program for finding the sum
# of first N terms of the series.

# from math import everything
from math import *

# CalculateSum function returns the final sum
def calculateSum(n) :

    # r1 and r2 are common ratios
    # of 1st and 2nd series
    r1, r2 = 2, 3

    # a1 and a2 are common first terms
    # of 1st and 2nd series
    a1, a2 = 1, 1

    return (a1 * (pow(r1, n) - 1) // (r1 - 1)
           + a2 * (pow(r2, n) - 1) // (r2 - 1))

# Driver Code
if __name__ == "__main__" :

    n = 4

    # function calling for 4 terms
    print("SUM = ",calculateSum(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program for finding the sum
// of first N terms of the series.
using System;

class GFG
{

// CalculateSum function
// returns the final sum
static int calculateSum(int n)
{
// r1 and r2 are common ratios
// of 1st and 2nd series
int r1 = 2, r2 = 3;

// a1 and a2 are common first
// terms of 1st and 2nd series
int a1 = 1, a2 = 1;

return (int)(a1 * (Math.Pow(r1, n) - 1) / (r1 - 1) +
             a2 * (Math.Pow(r2, n) - 1) / (r2 - 1));
}

// Driver code
static public void Main ()
{
    int n = 4;

    // function calling for 4 terms
    Console.Write("Sum = " +
                   calculateSum(n));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding the sum
// of first N terms of the series.

// CalculateSum function returns
// the final sum
function calculateSum($n)
{
    // r1 and r2 are common ratios
    // of 1st and 2nd series
    $r1 = 2;
    $r2 = 3;

    // a1 and a2 are common first 
    // terms of 1st and 2nd series
    $a1 = 1;
    $a2 = 1;

    return $a1 * (pow($r1, $n) - 1) /
                     ($r1 - 1) + $a2 *
                 (pow($r2, $n) - 1) /
                     ($r2 - 1);
}

// Driver code
$n = 4;

// function calling for 4 terms
echo "Sum = ", calculateSum($n);

// This code is contributed by ash264
?>
```

## java 描述语言

```
<script>

//javascript program for finding the sum
//of first N terms of the series.
//CalculateSum function returns the final sum
function calculateSum(n)
{
 // r1 and r2 are common ratios
 // of 1st and 2nd series
 var r1 = 2, r2 = 3;

 // a1 and a2 are common first terms
 // of 1st and 2nd series
 var a1 = 1, a2 = 1;

 return parseInt((a1 * (Math.pow(r1, n) - 1) / (r1 - 1)
        + a2 * (Math.pow(r2, n) - 1) / (r2 - 1)));
}

    //Driver code

var n = 4;

 // function calling for 4 terms
 document.write("Sum = " +calculateSum(n));

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
Sum = 55
```