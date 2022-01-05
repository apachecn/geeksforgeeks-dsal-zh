# 1^2+3^2+5^2+系列之和。。。+(2 * n–1)^2

> 原文:[https://www.geeksforgeeks.org/sum-series-12-32-52-2n-12/](https://www.geeksforgeeks.org/sum-series-12-32-52-2n-12/)

给定系列 1<sup>2</sup>+3<sup>2</sup>+5<sup>2</sup>+7<sup>2</sup>+。。。+(2 * n–1)<sup>2</sup>，求级数之和。
示例:

```
Input : n = 4
Output : 84
Explanation : 
sum = 12 + 32 + 52 + 72
    = 1 + 9 + 25 + 49
    = 84

Input : n = 10 
Output : 1330
Explanation :
sum = 12 + 32 + 52 + 72 + 92 + 112 + 132 + 152 + 172 + 192
    = 1 + 9 + 24 + 49 + . . . + 361
    = 1330
```

## C++

```
// Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.
#include <bits/stdc++.h>
using namespace std;

// Function to find sum of series.
int sumOfSeries(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum = sum + (2 * i - 1) * (2 * i - 1);
    return sum;
}

// Driver code
int main()
{
    int n = 10;

    cout << sumOfSeries(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

import java.io.*;

class GFG {

// Function to find sum of series.
 static int sumOfSeries(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
       sum = sum + (2 * i - 1) * (2 * i - 1);
    return sum;
}

// Driver code
  public static void  main(String[] args)
{
    int n = 10;
    System.out.println( sumOfSeries(n));   
}

}
```

## 蟒蛇 3

```
# Python Program to find sum of series
# 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

import math

# Function to find sum of series.
def sumOfSeries(n):

    sum = 0
    for i in range(1,n+1):
        sum = sum + (2 * i - 1) * (2 * i - 1)
    return sum

# driver code
n= 10
print(sumOfSeries(n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.
using System;

class GFG {

// Function to find sum of series.
static int sumOfSeries(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum = sum + (2 * i - 1) * (2 * i - 1);

    return sum;
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.Write( sumOfSeries(n));
}
}

/* This code is contributed by vt_m*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

// Function to find sum of series.
function sumOfSeries($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum = $sum + (2 * $i - 1) *
                      (2 * $i - 1);
    return $sum;
}

// Driver code
$n = 10;
echo(sumOfSeries($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

// Function to find sum of series.
function sumOfSeries(n)
{
    let sum = 0;
    for(let i = 1; i <= n; i++)
       sum = sum + (2 * i - 1) *
                   (2 * i - 1);

    return sum;
}

// Driver Code
let n = 10;

document.write(sumOfSeries(n)); 

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
1330
```

**时间复杂度:** O(n)

**另一种方法:**用公式求级数和:

```
    12 + 32 + 52 + 
     72 + . . . + (2*n - 1)2 
      = (n * (2 * n - 1) * (2 * n + 1)) / 3.

Please refer sum of squares of even and odd numbers for proof.
```

## C++

```
// Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.
#include <bits/stdc++.h>
using namespace std;

// Function that find sum of series.
int sumOfSeries(int n)
{
    // Formula to find sum of series.
    return (n * (2 * n - 1) * (2 * n + 1)) / 3;
}

// Driver code
int main()
{
    int n = 10;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

import java.io.*;
import java.util.*;

class GFG {

// Function to find sum of series.
static int sumOfSeries(int n)
{
   // Formula to find sum of series.
    return (n * (2 * n - 1) * (2 * n + 1)) / 3;

}

// Driver function
   public static void main (String[] args) {
   int n=10;
    System.out.println(sumOfSeries(n));

}

}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python Program to find sum of series
# 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

import math

# Function to find sum of series.
def sumOfSeries(n):

   # Formula to find sum of series.
    return int((n * (2 * n - 1) * (2 * n + 1)) / 3)

# driver code
n=10
print(sumOfSeries(n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.
using System;

class GFG {

// Function to find sum of series.
static int sumOfSeries(int n)
{
    // Formula to find sum of series.
    return (n * (2 * n - 1) * (2 * n + 1)) / 3;
}

// Driver function
public static void Main ()
{
    int n = 10;
    Console.Write(sumOfSeries(n));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

// Function that find sum of series.
function sumOfSeries($n)
{
    // Formula to find sum of series.
    return ($n * (2 * $n - 1) *
                 (2 * $n + 1)) / 3;
}

// Driver code
$n = 10;
echo(sumOfSeries($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript Program to find sum of series
// 1^2 + 3^2 + 5^2 + . . . + (2*n - 1)^2.

// Function that find sum of series.
function sumOfSeries(n)
{
    // Formula to find sum of series.
    return (n * (2 * n - 1) *
                 (2 * n + 1)) / 3;
}

// Driver code
let n = 10;
document.write(sumOfSeries(n));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**Output:** 

```
1330
```

**时间复杂度:** O(1)