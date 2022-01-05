# 检查给定的数字是否为正|有效方法

> 原文:[https://www . geeksforgeeks . org/check-given-number-pronic-efficient-approach/](https://www.geeksforgeeks.org/check-given-number-pronic-efficient-approach/)

一个复数是这样一个数，它可以表示为两个连续正整数的乘积。通过将这两个连续的正整数相乘，可以形成一个用乘积或复数表示的矩形。所以也被称为[矩形数](https://www.geeksforgeeks.org/rectangular-numbers/)。
前几个 Pronic 号码是:
0、2、6、12、20、30、42、56、72、90、110、132、156、182、210、240、272、306、342、380、420、462。。。。。。
复数是两个连续整数的乘积，即 n 是 x 和(x+1)的乘积。任务是检查给定的数字是否发音。

数学表示:

```
If x is a pronic number, then x=n(n+1) ∀ n∈N0
Where, N0={0, 1, 2, 3, 4, ....}, (A set of Natural Numbers)
```

示例:

```
Input : 56
Output : YES
Explanation: 56 = 7 * 8 i.e 56 is a product 
of two consecutive integers 7 and 8.

Input : 65
Output : NO
Explanation: 65 cannot be represented as a
product of any two consecutive integers.
```

我们之前讨论过一种方法，在本文中使用循环来检查一个数字是否发音。以前算法的时间复杂度比较高，按照大 O 渐近表示法，是 O(√n)。
在本文中，我们将解释一种时间复杂度为 O(log(log n)的有效方法。其思想是观察到，如果一个数可以表示为两个连续整数的乘积，那么这两个整数将接近该数的平方根。更恰当的观察将导致这样一个事实，即只有当 floor(sqrt(N))和 floor(sqrt(N))+1 的乘积等于 N 时，一个数 N 才能表示为两个连续整数的乘积。

下面是上述方法的逐步算法:

```
Step 1: Evaluate the square root value of the given number.
Step 2: Calculate the floor value of that square root.
Step 3: Calculate the product of value calculated in step-2
    and its next consecutive number.
Step 4: Check the product value in step-3 with the given number.
    Step 4.1: If the condition satisfies,
          then the number is a pronic number.
    Step 4.2: Otherwise the number is not a pronic number.
```

下面是上述算法的实现:

## C++

```
// C/C++ program to check if a number is pronic or not

#include<bits/stdc++.h>
using namespace std;

// function to check Pronic Number
bool pronic_check(int n)
{
    int x = (int)(sqrt(n));

    // Checking Pronic Number by
    // multiplying consecutive numbers
    if (x*(x+1)==n)
        return true;
    else
        return false;
}

// Driver Code
int main(void)
{
    int n = 56;   
    pronic_check(n) == true? cout << "YES" :
                             cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is pronic or not

import java.io.*;
import java.util.*;
import java.math.*;

class GFG
{

    // Function to check Pronic Number
    static boolean pronic_check(int n)
    {
        int x = (int)(Math.sqrt(n));

        // Checking Pronic Number by
        // multiplying consecutive numbers
        if (x * (x + 1) == n)
            return true;
        else
            return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 56;       
        if (pronic_check(n)==true)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python program to check if a number is pronic or not

import math

# function to check Pronic Number
def pronic_check(n) :
    x = (int)(math.sqrt(n))

    # Checking Pronic Number by multiplying
    # consecutive numbers
    if (x*(x + 1)== n):
        return True
    else:
        return False

# Driver Code
n = 56

if (pronic_check(n)==True):
    print("YES")
else:
    print("NO")
```

## C#

```
// C# program to check if a number is
// pronic or not
using System;

class GFG
{

    // Function to check Pronic Number
    static bool pronic_check(int n)
    {
        int x = (int)(Math.Sqrt(n));

        // Checking Pronic Number by
        // multiplying consecutive numbers
        if (x * (x + 1) == n)
            return true;
        else
            return false;
    }

    // Driver Code
    public static void Main()
    {
        int n = 56;

        if (pronic_check(n)==true)
            Console.Write("YES");
        else
            Console.Write("NO");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// number is pronic or not

// function to check Pronic Number
function pronic_check($n)
{
    $x = floor(sqrt($n));

    // Checking Pronic Number by
    // multiplying consecutive numbers
    if ($x * ($x + 1) == $n)
        return true;
    else
        return false;
}

    // Driver Code
    $n = 56;
    if (pronic_check($n) == true)
        echo "YES" ;
    else
        echo "NO";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number is pronic or not

// function to check Pronic Number
function pronic_check(n)
{
    var x = parseInt(Math.sqrt(n));

    // Checking Pronic Number by
    // multiplying consecutive numbers
    if (x * (x + 1) == n)
        return true;
    else
        return false;
}

// Driver Code
var n = 56;    
pronic_check(n) == true? document.write("YES") :
document.write("NO");

// This code is contributed by noob2000.
</script>
```

输出:

```
YES
```