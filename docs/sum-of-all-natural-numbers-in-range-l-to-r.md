# L 到 R 范围内所有自然数之和

> 原文:[https://www . geesforgeks . org/所有自然数之和-范围-l 到-r/](https://www.geeksforgeeks.org/sum-of-all-natural-numbers-in-range-l-to-r/)

给定范围 L 和 R，任务是找出范围 L 到 R 内所有自然数的和
**例** :

```
Input: L = 2, R = 5
Output: 14
2 + 3 + 4 + 5 = 14

Input: L = 10, R = 20
Output: 165
```

一种**天真的方法**是从 L 遍历到 R，将所有元素一个一个相加得到总和。
一种**有效的方法**是使用前 N 个自然数之和的公式。包含-排除原则的思想有助于解决上述问题。求自然数的和直到 **R** 和 **L-1** 再减去 ***和(R)-和(l-1)*** **。**
以下是上述方法的实施:

## C++

```
// C++ program to print the sum
// of all numbers in range L and R
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of
// all natural numbers
int sumNatural(int n)
{
    int sum = (n * (n + 1)) / 2;
    return sum;
}

// Function to return the sum
// of all numbers in range L and R
int suminRange(int l, int r)
{
    return sumNatural(r) - sumNatural(l - 1);
}

// Driver Code
int main()
{
    int l = 2, r = 5;
    cout << "Sum of Natural numbers from L to R is "
         << suminRange(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the sum
// of all numbers in range L and R

class GFG{
// Function to return the sum of
// all natural numbers
static int sumNatural(int n)
{
    int sum = (n * (n + 1)) / 2;
    return sum;
}

// Function to return the sum
// of all numbers in range L and R
static int suminRange(int l, int r)
{
    return sumNatural(r) - sumNatural(l - 1);
}

// Driver Code
public static void main(String[] args)
{
    int l = 2, r = 5;
    System.out.println("Sum of Natural numbers from L to R is "+suminRange(l, r));

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to print the sum  of
# all numbers in range L and R

# Function to return the sum of all natural numbers
def sumNatural(n):

    sum = (n*(n+1))//2

    return sum

# Function to return the sum
# of all numbers in range L and R
def suminRange(l, r):
    return sumNatural(r) - sumNatural(l-1)

#  Driver Code
l =2; r= 5
print("Sum of Natural numbers from L to R is ",suminRange(l, r))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to print the sum
// of all numbers in range L and R
using System;

class GFG
{
// Function to return the sum
// of all natural numbers
static int sumNatural(int n)
{
    int sum = (n * (n + 1)) / 2;
    return sum;
}

// Function to return the sum
// of all numbers in range L and R
static int suminRange(int l, int r)
{
    return sumNatural(r) -
           sumNatural(l - 1);
}

// Driver Code
static public void Main ()
{
    int l = 2, r = 5;
    Console.WriteLine("Sum of Natural numbers " +
                              "from L to R is " +
                               suminRange(l, r));
}
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the sum
// of all numbers in range L and R

// Function to return the sum of
// all natural numbers
function sumNatural($n)
{
    $sum = ($n * ($n + 1)) / 2;
    return $sum;
}

// Function to return the sum
// of all numbers in range L and R
function suminRange($l, $r)
{
    return sumNatural($r) -
           sumNatural($l - 1);
}

// Driver Code
$l = 2;
$r = 5;
echo "Sum of Natural numbers " .
              "from L to R is ",
             suminRange($l, $r);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to print the sum
// of all numbers in range L and R

// Function to return the sum of
// all natural numbers
function sumNatural(n)
{
    sum = (n * (n + 1)) / 2;
    return sum;
}

// Function to return the sum
// of all numbers in range L and R
function suminRange(l, r)
{
    return sumNatural(r) -
           sumNatural(l - 1);
}

// Driver Code
let l = 2;
let r = 5;
document.write("Sum of Natural numbers from L to R is "+
             suminRange(l, r));

// This code is contributed by sravan kumar gottumukkalan

</script>
```

**Output:** 

```
Sum of Natural numbers from L to R is 14
```