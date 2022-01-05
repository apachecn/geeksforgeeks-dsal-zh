# 求第一个 N 中心十二边形数的和

> 原文:[https://www . geesforgeks . org/find-第一个以 n 为中心的十二边形数的和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-n-centered-dodecagonal-number/)

给定一个数 N，任务是求第一个 N 的和[中心十二边形数](https://www.geeksforgeeks.org/centered-dodecagonal-number/)。

> 前几个居中的十二边形数字是 **1、13、37、73、121、181……**

**例:**

> **输入:** N = 3
> **输出:** 51
> **说明:**
> 1、13、37 是前三个居中的十二边形数。
> **输入:** N = 5
> **输出:** 245

**进场:**

1.  首先，创建一个函数来帮助我们计算第 N 个<sup>[中心十二边形数](https://www.geeksforgeeks.org/centered-dodecagonal-number/)。</sup>
2.  运行一个从 1 到 N 的循环，找到第 I 个居中的十二边形数。
3.  将上面计算的所有居中十二边形数相加。
4.  最后，显示前 N 个居中十二边形数字的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum
// of the first N Centred
// Dodecagonal number
#include <bits/stdc++.h>
using namespace std;

// Function to find the N-th 
// Centered Dodecagonal number
int Centered_Dodecagonal_num(int n)
{

    // Formula to calculate nth 
    // Centered_Dodecagonal number
    return 6 * n * (n - 1) + 1;
}

// Function to find the sum of the first
// N Centered_Dodecagonal number
int sum_Centered_Dodecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating from 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Centered_Dodecagonal_num(i);
    }
    return summ;
}

// Driver code
int main()
{
    int n = 5;

    cout << sum_Centered_Dodecagonal_num(n);
}

// This code is contributed by coder001
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the 
// first N centred dodecagonal number
class GFG {

// Function to find the N-th
// centered dodecagonal number
static int Centered_Dodecagonal_num(int n)
{

    // Formula to calculate nth
    // Centered_Dodecagonal number
    return 6 * n * (n - 1) + 1;
}

// Function to find the sum of the first
// N Centered_Dodecagonal number
static int sum_Centered_Dodecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating from 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Centered_Dodecagonal_num(i);
    }
    return summ;
}

// Driver code
public static void main (String[] args)
{
    int n = 5;

    System.out.print(sum_Centered_Dodecagonal_num(n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of the first N centred
# Dodecagonal number

# Function to find the
# N-th Centered Dodecagonal
# number
def Centered_Dodecagonal_num(n):

    # Formula to calculate 
    # nth Centered_Dodecagonal
    # number
    return 6 * n * (n - 1) + 1

# Function to find the
# sum of the first N
# Centered_Dodecagonal
# number
def sum_Centered_Dodecagonal_num(n) :

    # Variable to store the
    # sum
    summ = 0

    # Iterating from 1 to N
    for i in range(1, n + 1):

        # Finding the sum
        summ += Centered_Dodecagonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 5

    print(sum_Centered_Dodecagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centred dodecagonal number
using System;

class GFG{

// Function to find the N-th
// centered dodecagonal number
static int Centered_Dodecagonal_num(int n)
{

    // Formula to calculate nth
    // Centered_Dodecagonal number
    return 6 * n * (n - 1) + 1;
}

// Function to find the sum of the first
// N Centered_Dodecagonal number
static int sum_Centered_Dodecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating from 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Centered_Dodecagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main()
{
    int n = 5;

    Console.Write(sum_Centered_Dodecagonal_num(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find the sum 
    // of the first N Centred
    // Dodecagonal number

    // Function to find the N-th  
    // Centered Dodecagonal number 
    function Centered_Dodecagonal_num(n) 
    {

        // Formula to calculate nth  
        // Centered_Dodecagonal number
        return 6 * n * (n - 1) + 1;
    }

    // Function to find the sum of the first 
    // N Centered_Dodecagonal number
    function sum_Centered_Dodecagonal_num(n)
    {

        // Variable to store the sum
        let summ = 0;

        // Iterating from 1 to N
        for(let i = 1; i < n + 1; i++)
        {

           // Finding the sum
           summ += Centered_Dodecagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    document.write(sum_Centered_Dodecagonal_num(n));

</script>
```

**Output:** 

```
245
```

**时间复杂度:** O(N)。