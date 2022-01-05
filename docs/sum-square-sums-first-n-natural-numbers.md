# 前 n 个自然数平方和之和

> 原文:[https://www . geesforgeks . org/sum-square-sums-first-n-natural-numbers/](https://www.geeksforgeeks.org/sum-square-sums-first-n-natural-numbers/)

给定正整数 **n** 。任务是求前 n 个自然数平方和的和。
**例:**

```
Input : n = 3
Output : 20
Sum of square of first natural number = 1
Sum of square of first two natural number = 1^2 + 2^2 = 5
Sum of square of first three natural number = 1^2 + 2^2 + 3^2 = 14
Sum of sum of square of first three natural number = 1 + 5 + 14 = 20

Input : n = 2
Output : 6
```

**方法 1: O(n)** 思路是求第一个 I 自然数的平方和，其中 1 < = i < = n，然后将它们全部相加。
我们可以通过公式求出前 n 个自然数的平方和:n * (n + 1)* (2*n + 1)/6
下面是这个方法的实现:

## C++

```
// CPP Program to find the sum of sum of
// squares of first n natural number
#include <bits/stdc++.h>
using namespace std;

// Function to find sum of sum of square of
// first n natural number
int findSum(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += ((i * (i + 1) * (2 * i + 1)) / 6);
    return sum;
}

// Driven Program
int main()
{
    int n = 3;
    cout << findSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the sum of
// sum of squares of first n natural
// number

class GFG {

    // Function to find sum of sum of
    // square of first n natural number
    static int findSum(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += ((i * (i + 1)
               * (2 * i + 1)) / 6);
        return sum;
    }

    // Driver Program
    public static void main(String[] args)
    {
        int n = 3;

        System.out.println( findSum(n));
    }
}

// This code is contributed by
// Arnab Kundu
```

## 蟒蛇 3

```
# Python3 Program to find the sum
# of sum of squares of first n
# natural number

# Function to find sum of sum of
# square of first n natural number
def findSum(n):
    summ = 0
    for i in range(1, n+1):
        summ = (summ + ((i * (i + 1)
                * (2 * i + 1)) / 6))
    return summ

# Driven Program
n = 3
print(int(findSum(n)))

# This code is contributed by
# Prasad Kshirsagar
```

## C#

```
// C# Program to find the sum of sum of
// squares of first n natural number
using System;

public class GFG {

    // Function to find sum of sum of
    // square of first n natural number
    static int findSum(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += ((i * (i + 1) *
                  (2 * i + 1)) / 6);
        return sum;
    }

    // Driver Program
    static public void Main()
    {
        int n = 3;

        Console.WriteLine(findSum(n));
    }
}

// This code is contributed by
// Arnab Kundu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the sum of
// squares of first n natural number

// Function to find sum of sum of
// square of first n natural number
function findSum( $n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += (($i * ($i + 1) *
                 (2 * $i + 1)) / 6);
    return $sum;
}

// Driver Code
$n = 3;
echo findSum($n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the sum of sum of
// squares of first n natural number

// Function to find sum of sum of square
// of first n natural number
function findSum(n)
{
    return (n * (n + 1) * (n + 1) * (n + 2)) / 12;
}

// Driven Program

    let n = 3;
    document.write(findSum(n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output :** 

```
20
```