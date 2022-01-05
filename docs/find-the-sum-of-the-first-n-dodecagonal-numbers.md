# 求前 N 个十二边形数的和

> 原文:[https://www . geeksforgeeks . org/find-the-sum-first-n-十二边形数字/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-n-dodecagonal-numbers/)

给定一个数字 **N** ，任务是找出第一个 N [十二边形数字](https://www.geeksforgeeks.org/dodecagonal-number/)的和。

> 前几个十二边形数字是 **1、12、33、64、105、156、217……**

**例:**

> **输入:** N = 3
> **输出:** 46
> **说明:**
> 1、12、33 是前三个十二边形数字
> **输入:** N = 5
> **输出:** 215

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个十二边形数](https://www.geeksforgeeks.org/dodecagonal-number/)。</sup>
2.  运行一个从 1 到 N 的循环，找到一个十二边形数。
3.  将上面计算的所有十二边形数相加。
4.  最后，显示前 N 个十二边形数字的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of
// the first N dodecagonal numbers
#include <bits/stdc++.h>
using namespace std;

// Function to find the N-th
// dodecagonal number
int Dodecagonal_num(int n)
{

    // Formula to calculate N-th
    // dodecagonal number
    return (5 * n * n - 4 * n);
}

// Function to find the sum of
// the first N dodecagonal numbers
int sum_Dodecagonal_num(int n)
{

    // Variable to get the sum
    int summ = 0;

    // Iterating through the
    // first N numbers
    for(int i = 1; i < n + 1; i++)
    {

        // Compute the sum
        summ += Dodecagonal_num(i);
    }
    return summ;
}

// Driver Code
int main()
{
    int n = 5;

    // Display first Nth
    // centered_decagonal number
    cout << (sum_Dodecagonal_num(n));
    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// the first N dodecagonal numbers
class GFG {

// Function to find the N-th
// dodecagonal number
static int Dodecagonal_num(int n)
{

    // Formula to calculate N-th
    // dodecagonal number
    return (5 * n * n - 4 * n);
}

// Function to find the sum of
// the first N dodecagonal numbers
static int sum_Dodecagonal_num(int n)
{

    // Variable to get the sum
    int summ = 0;

    // Iterating through the
    // first N numbers
    for(int i = 1; i < n + 1; i++)
    {

       // Compute the sum
       summ += Dodecagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    // Display first Nth
    // centered_decagonal number
    System.out.println(sum_Dodecagonal_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the
# sum of the first N
# Dodecagonal numbers

# Function to find the N-th
# Dodecagonal number
def Dodecagonal_num(n):

    # Formula to calculate 
    # N-th Dodecagonal
    # number 
    return (5 * n * n - 4 * n)

# Function to find the
# sum of the first N
# Dodecagonal numbers
def sum_Dodecagonal_num(n) :

    # Variable to get the sum
    summ = 0

    # Iterating through the
    # first N numbers
    for i in range(1, n + 1):

        # Compute the sum
        summ += Dodecagonal_num(i)

    return summ

# Driver Code
if __name__ == '__main__' :

    n = 5

    print(sum_Dodecagonal_num(n))
```

## C#

```
// C# program to find the sum of
// the first N dodecagonal numbers
using System;

class GFG {

// Function to find the N-th
// dodecagonal number
static int Dodecagonal_num(int n)
{

    // Formula to calculate N-th
    // dodecagonal number
    return (5 * n * n - 4 * n);
}

// Function to find the sum of
// the first N dodecagonal numbers
static int sum_Dodecagonal_num(int n)
{

    // Variable to get the sum
    int summ = 0;

    // Iterating through the
    // first N numbers
    for(int i = 1; i < n + 1; i++)
    {

        // Compute the sum
        summ += Dodecagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;

    // Display first Nth
    // centered_decagonal number
    Console.WriteLine(sum_Dodecagonal_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of
    // the first N dodecagonal numbers

    // Function to find the N-th
    // dodecagonal number
    function Dodecagonal_num(n)
    {

        // Formula to calculate N-th
        // dodecagonal number
        return (5 * n * n - 4 * n);
    }

    // Function to find the sum of 
    // the first N dodecagonal numbers
    function sum_Dodecagonal_num(n)
    {

        // Variable to get the sum
        let summ = 0;

        // Iterating through the
        // first N numbers
        for(let i = 1; i < n + 1; i++)
        {

            // Compute the sum
            summ += Dodecagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    // Display first Nth
    // centered_decagonal number
    document.write(sum_Dodecagonal_num(n));

</script>
```

**Output:** 

```
215
```

**时间复杂度:** O(N)。