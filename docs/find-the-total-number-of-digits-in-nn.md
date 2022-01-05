# 求(N！)N

> 原文:[https://www . geesforgeks . org/find-总位数-in-nn/](https://www.geeksforgeeks.org/find-the-total-number-of-digits-in-nn/)

给定一个数字 n，任务是找出![(N!)^{N}  ](img/11a7d942cbf3aeab4a0f1b85ba99e7f1.png "Rendered by QuickLaTeX.com")中的总位数。
**示例** :

```
Input: N = 3
Output: 3
If N=3, (3!)3=216, 
So the count of digits is 3

Input: N = 4
Output: 6
```

**进场:**

```
As we know,
log(a*b) = log(a) + log(b)

Consider,
X = log(N!) = log(1*2*3....... * N) 
            = log(1)+log(2)+........ +log(N)
```

现在，我们知道任何数字的对数基数 10 的底值增加 1，给出该数字中存在的位数。也就是说，数字 N 中的位数将是**楼(原木 <sub>10</sub> N) + 1** 。
因此![(N!)^{N}  ](img/11a7d942cbf3aeab4a0f1b85ba99e7f1.png "Rendered by QuickLaTeX.com")中的位数为:

```
floor(log())+1
= floor(N*log10(N!)) + 1
= floor(N*X) + 1.
```

以下是上述方法的实现:

## C++

```
// C++ program to find the total
// Number of Digits in (N!)^N

#include <bits/stdc++.h>
using namespace std;

// Function to find the total
// Number of Digits in (N!)^N
int CountDigits(int n)
{
    if (n == 1)
        return 1;

    double sum = 0;

    // Finding X
    for (int i = 2; i <= n; ++i) {
        sum += (double)log(i) / (double)log(10);
    }

    // Calculating N*X
    sum *= (double)n;

    // Floor(N*X) + 1
    return ceil(sum); // equivalent to floor(sum) + 1
}

// Driver code
int main()
{
    int N = 5;

    cout << CountDigits(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the total
// Number of Digits in (N!)^N
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
// Function to find the total
// Number of Digits in (N!)^N
public double CountDigits(int n)
{
    if (n == 1)
        return 1;

    double sum = 0;

    // Finding X
    for (int i = 2; i <= n; ++i)
    {
        sum += ((double)Math.log(i) /
                (double)Math.log(10));
    }

    // Calculating N*X
    sum *= n;

    // Floor(N*X) + 1
    // equivalent to floor(sum) + 1
    return Math.ceil(sum);
}

// Driver code
public static void main(String args[])
{
    GFG g = new GFG();
    int N = 5;
    System.out.println(g.CountDigits(N));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to find the total
# Number of Digits in (N!)^N

import math as ma
def CountDigits(n):

    if(n==1):
        return 1
    sum=0

    # Finding X
    for i in range(2,n+1):
        sum+=ma.log(i,10)

    # Calculating N*X
    sum*=n

    # Floor(N*X)+1
    #equivalent to floor(sum) + 1
    return ma.ceil(sum)

# Driver code
if __name__=='__main__':
    N=5
    print(CountDigits(N))

# This code is contributed by
# Indrajit Sinha.
```

## C#

```
// C# program to find the total
// Number of Digits in (N!)^N
using System;

class GFG
{
// Function to find the total
// Number of Digits in (N!)^N
public double CountDigits(int n)
{
    if (n == 1)
        return 1;

    double sum = 0;

    // Finding X
    for (int i = 2; i <= n; ++i)
    {
        sum += ((double)Math.Log(i) /
                (double)Math.Log(10));
    }

    // Calculating N*X
    sum *= n;

    // Floor(N*X) + 1
    // equivalent to floor(sum) + 1
    return Math.Ceiling(sum);
}

// Driver code
public static void Main()
{
    GFG g = new GFG();
    int N = 5;
    Console.WriteLine(g.CountDigits(N));
}
}

// This code is contributed
// by SoumikMondal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the total
// Number of Digits in (N!)^N

// Function to find the total
// Number of Digits in (N!)^N
function CountDigits($n)
{
    if ($n == 1)
        return 1;

    $sum = 0;

    // Finding X
    for ($i = 2; $i <= $n; ++$i)
    {
        $sum += log($i) / log(10);
    }

    // Calculating N*X
    $sum *= $n;

    // Floor(N*X) + 1
    return ceil($sum); // equivalent to floor(sum) + 1
}

// Driver code
$N = 5;
echo CountDigits($N);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to find the total
// Number of Digits in (N!)^N    
// Function to find the total
    // Number of Digits in (N!)^N
    function CountDigits(n) {
        if (n == 1)
            return 1;

        var sum = 0;

        // Finding X
        for (i = 2; i <= n; ++i) {
            sum += (Math.log(i) /  Math.log(10));
        }

        // Calculating N*X
        sum *= n;

        // Floor(N*X) + 1
        // equivalent to floor(sum) + 1
        return Math.ceil(sum);
    }

    // Driver code

        var N = 5;
        document.write(CountDigits(N));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
11
```