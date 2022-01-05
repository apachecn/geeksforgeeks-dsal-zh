# 求第一个 N 中心五边形数的和

> 原文:[https://www . geesforgeks . org/find-第 n 个以第一个为中心的五边形数字的总和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-centered-pentagonal-number/)

给定一个数字 **N** ，任务是找到第一个**N**T4】中心五边形数字的和。

> 前几个居中的五边形数字是 *1，6，16，31，51，76，106 …*

**例:**

> **输入:** N = 3
> **输出:** 23
> **说明:**
> 1、6、16 是前三个
> 居中的五边形数。
> **输入:** N = 5
> **输出:** 105

**方法:**想法是首先创建一个函数，它将帮助我们在恒定时间内找到中心五边形数。这个功能的实现已经在[这篇文章](https://www.geeksforgeeks.org/centered-pentagonal-number/)中讨论过了。创建此功能后，遵循以下步骤:

1.  运行[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)从 1 开始到 **N、**找到**I<sup>th</sup>**T8】中心五边形号。
2.  将上面计算的所有*中心五边形*数相加。
3.  然后，显示 **N** *中心五边形*数字之和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N centered pentagonal numbers
#include<bits/stdc++.h>
using namespace std;

// Function to find the
// Centered_Pentagonal number
int Centered_Pentagonal_num(int n)
{

    // Formula to calculate
    // nth Centered_Pentagonal
    // number & return it
    // into main function.
    return (5 * n * n - 5 * n + 2) / 2;
}

// Function to find the sum of the first
// N Centered_Pentagonal numbers
int sum_Centered_Pentagonal_num(int n)
{

    // To get the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
       summ += Centered_Pentagonal_num(i);
    }
    return summ;
}

// Driver Code
int main()
{
    int n = 5;

    // Display first Nth
    // Centered_Pentagonal number
    cout << (sum_Centered_Pentagonal_num(n));
    return 0;
}

// This code is contributed by PratikBasu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N centered pentagonal numbers
class GFG{

// Function to find the
// Centered_Pentagonal number
static int Centered_Pentagonal_num(int n)
{

    // Formula to calculate
    // nth Centered_Pentagonal
    // number & return it
    // into main function.
    return (5 * n * n - 5 * n + 2) / 2;
}

// Function to find the sum of the first
// N Centered_Pentagonal numbers
static int sum_Centered_Pentagonal_num(int n)
{

    // To get the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
        summ += Centered_Pentagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    // Display first Nth
    // Centered_Pentagonal number
    System.out.print((sum_Centered_Pentagonal_num(n)));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# the first N Centered
# Pentagonal number

# Function to find the
# Centered_Pentagonal number
def Centered_Pentagonal_num(n):

    # Formula to calculate 
    # nth Centered_Pentagonal
    # number & return it
    # into main function.
    return (5 * n * n -
            5 * n + 2) // 2

# Function to find the
# sum of the first N
# Centered_Pentagonal
# numbers
def sum_Centered_Pentagonal_num(n) :

    # To get the sum
    summ = 0

    for i in range(1, n + 1):

        # Function to get the
        # Centered_Pentagonal_num
        summ += Centered_Pentagonal_num(i)

    return summ

# Driver Code
if __name__ == '__main__' :

    n = 5

    # display first Nth
    # Centered_Pentagonal number
    print(sum_Centered_Pentagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centered pentagonal numbers
using System;

class GFG{

// Function to find the
// Centered_Pentagonal number
static int Centered_Pentagonal_num(int n)
{

    // Formula to calculate
    // nth Centered_Pentagonal
    // number & return it
    // into main function.
    return (5 * n * n - 5 * n + 2) / 2;
}

// Function to find the sum of the first
// N Centered_Pentagonal numbers
static int sum_Centered_Pentagonal_num(int n)
{

    // To get the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
       summ += Centered_Pentagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;

    // Display first Nth
    // Centered_Pentagonal number
    Console.Write((sum_Centered_Pentagonal_num(n)));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of the 
    // first N centered pentagonal numbers

    // Function to find the 
    // Centered_Pentagonal number 
    function Centered_Pentagonal_num(n)
    {

        // Formula to calculate 
        // nth Centered_Pentagonal 
        // number & return it 
        // into main function. 
        return (5 * n * n - 5 * n + 2) / 2;
    }

    // Function to find the sum of the first
    // N Centered_Pentagonal numbers 
    function sum_Centered_Pentagonal_num(n)
    {

        // To get the sum
        let summ = 0;

        // Iterating through the range
        // 1 to N
        for(let i = 1; i < n + 1; i++)
        {
           summ += Centered_Pentagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    // Display first Nth 
    // Centered_Pentagonal number
    document.write(sum_Centered_Pentagonal_num(n));

</script>
```

**Output:** 

```
105
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)