# 计算折扣百分比的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-difference-percent/](https://www.geeksforgeeks.org/program-to-find-the-discount-percentage/)

给定产品的标价![M  ](img/20aead0a95215a9a83fdd34d16c40b4d.png "Rendered by QuickLaTeX.com")和售价![S  ](img/286065faa2e31cda66548efbe78a36d1.png "Rendered by QuickLaTeX.com")。任务是计算应用于该产品的折扣百分比。

**示例**:

```
Input: M = 120, S = 100
Output: 16.66%

Input: M = 1000, S = 500
Output: 50% 
```

计算产品折扣百分比的数学公式为:

```
Discount = Marked Price - Selling price

Therefore,
Discount Percentage = (Discount / Marked Price) * 100
```

以下是查找产品折扣百分比的程序:

## C++

```
// CPP Program to find the Discount Percentage

#include <bits/stdc++.h>
using namespace std;

// Function to find the Discount Percentage
float discountPercentage(float S, float M)
{
    // Calculating discount
    float discount = M - S;

    // Calculating discount percentage
    float disPercent = (discount / M) * 100;

    return disPercent;
}

// Driver code
int main()
{
    int M, S;
    M = 120;
    S = 100;

    // Setting the precision to 2 decimals
    cout << std::fixed << std::setprecision(2)
        << discountPercentage(S, M) << "%" << endl;

    M = 1000;
    S = 500;

    // Setting the precision to 2 decimals
    cout << std::fixed << std::setprecision(2)
        << discountPercentage(S, M) << "%" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the Discount Percentage

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find the Discount Percentage
static float discountPercentage(float S, float M)
{
    // Calculating discount
    float discount = M - S;

    // Calculating discount percentage
    float disPercent = (discount / M) * 100;

    return disPercent;
}

// Driver code
public static void main(String args[])
{
    int M, S;
    M = 120;
    S = 100;

    System.out.printf("%.2f",discountPercentage(S,M));
    System.out.println("%");

    M = 1000;
    S = 500;

   System.out.printf("%.2f",discountPercentage(S,M));
    System.out.println("%");
}
}
```

## 蟒蛇 3

```
# Python3 Program to find the 
# Discount Percentage

# Function to find the 
# Discount Percentage
def discountPercentage(S, M):

    # Calculating discount
    discount = M - S

    # Calculating discount percentage
    disPercent = (discount /M) * 100

    return disPercent

# Driver code
if __name__=='__main__':
    M = 120
    S = 100

    print(discountPercentage(S, M), "%")

    M = 1000
    S = 500

    print(discountPercentage(S, M), "%")

# This code is contribute 
# by ihritik
```

## C#

```
// C# Program to find the 
// Discount Percentage
using System;

class GFG
{

// Function to find the
// Discount Percentage
static float discountPercentage(float S, 
                                float M)
{
    // Calculating discount
    float discount = M - S;

    // Calculating discount percentage
    float disPercent = (discount / M) * 100;

    return disPercent;
}

// Driver code
static public void Main ()
{
    int M, S;
    M = 120;
    S = 100;

    Console.Write(discountPercentage(S, M));
    Console.WriteLine("%");

    M = 1000;
    S = 500;

    Console.Write(discountPercentage(S, M));
    Console.Write("%");
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the 
// Discount Percentage

// Function to find the 
// Discount Percentage
function discountPercentage($S, $M)
{
    // Calculating discount
    $discount = $M - $S;

    // Calculating discount percentage
    $disPercent = ($discount /$M) * 100;

    return $disPercent;
}

// Driver code
$M; $S;
$M = 120;
$S = 100;

echo discountPercentage($S, $M), "%", "\n";

$M = 1000;
$S = 500;

echo discountPercentage($S, $M), "%", "\n";

// This code is contribute 
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Java Script Program to find the Discount Percentage

// Function to find the Discount Percentage
function discountPercentage( S,  M)
{
    // Calculating discount
    let discount = M - S;

    // Calculating discount percentage
    let disPercent = (discount / M) * 100;

    return disPercent;
}

// Driver code
 let M, S;
    M = 120;
    S = 100;

    document.write(discountPercentage(S,M).toFixed(2));
    document.write("%");
    document.write("<br>");

    M = 1000;
    S = 500;

    document.write(discountPercentage(S,M).toFixed(2));
    document.write("%");

// Contributed by sravan kumar 
</script>
```

**Output:** 

```
16.67%
50.00%
```