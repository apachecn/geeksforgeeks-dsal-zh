# 求第 n 个居中的五边形数的和

> 原文:[https://www . geesforgeks . org/find-第 n 个中心五边形数的和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-centered-pentadecagonal-number/)

给定一个数字 **N** ，任务是找出第一个 N [中心五边形数字](https://www.geeksforgeeks.org/centered-pentadecagonal-number/)的和。

> 前几个居中的五边形数字是 **1、16、46、91、151、226、316……**

**例:**

> **输入:** N = 3
> **输出:** 63
> **说明:**
> 1、16、46 是前三个居中的五边形数。
> **输入:** N = 5
> **输出:** 305

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个以五边形为中心的数。](https://www.geeksforgeeks.org/centered-pentadecagonal-number/)</sup> 
2.  现在，运行一个从 1 到 N 的循环，找到第 I<sup>个居中的五边形数。</sup>
3.  将上面计算的所有居中的五边形数相加。
4.  最后，显示第一个以 N 为中心的五边形数的和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N centered pentadecagonal number
#include<bits/stdc++.h>
using namespace std;

// Function to find the centered
// pentadecagonal number
int Centered_Pentadecagonal_num(int n)
{

    // Formula to calculate
    // N-th centered pentadecagonal
    // number
    return (15 * n * n - 15 * n + 2) / 2;
}

// Function to find the sum of
// the first N centered
// pentadecagonal numbers
int sum_Centered_Pentadecagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    for(int i = 1; i < n + 1; i++)
    {
       summ += Centered_Pentadecagonal_num(i);
    }
    return summ;
}

// Driver Code
int main()
{
    int n = 5;

    cout << sum_Centered_Pentadecagonal_num(n);
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N centered pentadecagonal number
class GFG {

// Function to find the centered
// pentadecagonal number
static int Centered_Pentadecagonal_num(int n)
{

    // Formula to calculate
    // N-th centered pentadecagonal
    // number
    return (15 * n * n - 15 * n + 2) / 2;
}

// Function to find the sum of
// the first N centered
// pentadecagonal numbers
static int sum_Centered_Pentadecagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    for(int i = 1; i < n + 1; i++)
    {
       summ += Centered_Pentadecagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    System.out.println(sum_Centered_Pentadecagonal_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of the first N centered 
# Pentadecagonal number

# Function to find the
# Centered_Pentadecagonal
# number
def Centered_Pentadecagonal_num(n):

    # Formula to calculate 
    # N-th Centered_Pentadecagonal
    # number
    return (15 * n * n -
            15 * n + 2) // 2

# Function to find the
# sum of the first N
# Centered_Pentadecagonal
# numbers
def sum_Centered_Pentadecagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    for i in range(1, n + 1):

        summ += Centered_Pentadecagonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 5

    print(sum_Centered_Pentadecagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centered pentadecagonal number
using System;

class GFG
{

// Function to find the centered
// pentadecagonal number
static int Centered_Pentadecagonal_num(int n)
{

    // Formula to calculate
    // N-th centered pentadecagonal
    // number
    return (15 * n * n - 15 * n + 2) / 2;
}

// Function to find the sum of
// the first N centered
// pentadecagonal numbers
static int sum_Centered_Pentadecagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    for(int i = 1; i < n + 1; i++)
    {
        summ += Centered_Pentadecagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;

    Console.WriteLine(sum_Centered_Pentadecagonal_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of the
    // first N centered pentadecagonal number

    // Function to find the centered
    // pentadecagonal number
    function Centered_Pentadecagonal_num(n)
    {

        // Formula to calculate
        // N-th centered pentadecagonal
        // number
        return (15 * n * n - 15 * n + 2) / 2;
    }

    // Function to find the sum of 
    // the first N centered 
    // pentadecagonal numbers
    function sum_Centered_Pentadecagonal_num(n)
    {

        // Variable to store
        // the sum
        let summ = 0;

        for(let i = 1; i < n + 1; i++)
        {
           summ += Centered_Pentadecagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    document.write(sum_Centered_Pentadecagonal_num(n));

</script>
```

**Output:** 

```
305
```

**时间复杂度:** O(N)