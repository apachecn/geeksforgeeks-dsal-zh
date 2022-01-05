# 求前 N 个居中十边形数的和

> 原文:[https://www . geesforgeks . org/find-第一个以 n 为中心的十边形数字的总和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-n-centered-decagonal-numbers/)

给定一个数字 N，任务是找出前 N 个[居中十边形数字](https://www.geeksforgeeks.org/centered-decagonal-number/)的和。

> 前几个居中的十边形数字是 **1、11、31、61、101、151……**

**示例:**

> **输入:** N = 3
> **输出:** 43
> **说明:**
> 1、11、31 是前三个居中的十边形数字。
> **输入:** N = 5
> **输出:** 205

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个居中的十边形数](https://www.geeksforgeeks.org/centered-decagonal-number/)。</sup>
2.  现在，运行一个从 1 到 N 的循环，找到第 i <sup>个</sup>个居中的十边形数。
3.  将以上计算的所有居中十边形数字相加。
4.  最后，显示第一个以 N 为中心的十边形数字的总和。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N centered decagonal number
#include <bits/stdc++.h>
using namespace std;

// Function to find the N-th
// centered decagonal number
int Centered_decagonal_num(int n)
{

    // Formula to calculate nth
    // centered_decagonal number
    // & return it into main function.
    return (5 * n * n - 5 * n + 1);
}

// Function to find the sum of
// the first N centered decagonal
// numbers
int sum_Centered_decagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    for(int i = 1; i < n + 1; i++)
    {
       summ += Centered_decagonal_num(i);
    }
    return summ;
}

// Driver code
int main()
{
    int n = 5;

    // Display first Nth
    // centered_decagonal number
    cout << (sum_Centered_decagonal_num(n));

    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N centered decagonal number
class GFG {

// Function to find the N-th
// centered decagonal number
static int Centered_decagonal_num(int n)
{

    // Formula to calculate nth
    // centered_decagonal number
    // & return it into main function.
    return (5 * n * n - 5 * n + 1);
}

// Function to find the sum of
// the first N centered decagonal
// numbers
static int sum_Centered_decagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    for(int i = 1; i < n + 1; i++)
    {
       summ += Centered_decagonal_num(i);
    }
    return summ;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    // Display first Nth
    // centered_decagonal number
    System.out.println(sum_Centered_decagonal_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# the first N centered
# decagonal number

# Function to find the N-th
# centered decagonal number
def Centered_decagonal_num(n):

    # Formula to calculate 
    # nth Centered_decagonal
    # number & return it
    # into main function.
    return (5 * n * n -
            5 * n + 1)

# Function to find the
# sum of the first N
# Centered decagonal
# numbers
def sum_Centered_decagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Iterating through the range
    for i in range(1, n + 1):

        summ += Centered_decagonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 5

    # display first Nth
    # Centered_decagonal number
    print(sum_Centered_decagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centered decagonal number
using System;

class GFG {

// Function to find the N-th
// centered decagonal number
static int Centered_decagonal_num(int n)
{

    // Formula to calculate nth
    // centered_decagonal number
    // & return it into main function.
    return (5 * n * n - 5 * n + 1);
}

// Function to find the sum of
// the first N centered decagonal
// numbers
static int sum_Centered_decagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    for(int i = 1; i < n + 1; i++)
    {
        summ += Centered_decagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;

    // Display first Nth
    // centered_decagonal number
    Console.WriteLine(sum_Centered_decagonal_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of the 
    // first N centered decagonal number

    // Function to find the N-th
    // centered decagonal number
    function Centered_decagonal_num(n) 
    {

        // Formula to calculate nth
        // centered_decagonal number
        // & return it into main function.
        return (5 * n * n - 5 * n + 1);
    }

    // Function to find the sum of
    // the first N centered decagonal
    // numbers
    function sum_Centered_decagonal_num(n)
    {

        // Variable to store
        // the sum
        let summ = 0;

        // Iterating through the range
        for(let i = 1; i < n + 1; i++)
        {
           summ += Centered_decagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    // Display first Nth 
    // centered_decagonal number
    document.write(sum_Centered_decagonal_num(n));

</script>
```

**Output:** 

```
205
```

**时间复杂度:** O(N)。