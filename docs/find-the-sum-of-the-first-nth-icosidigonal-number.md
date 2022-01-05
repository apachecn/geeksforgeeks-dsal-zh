# 求第 n 个整数的和

> 原文:[https://www . geesforgeks . org/find-the-sum-the-first-n-icosidigional-number/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-icosidigonal-number/)

给定一个数字 **N** ，任务是找出前 N 个[icosidigional 数字](https://www.geeksforgeeks.org/icosidigonal-number/)的和。

> 前几个数字是 **1、22、63、124、205、306……**

**例:**

> **输入:** N = 3
> **输出:** 86
> **说明:**
> 1、22、63 是前三个 Icosidigonal 数。
> **输入:** N = 6
> **输出:** 721

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个整数](https://www.geeksforgeeks.org/icosidigonal-number/)。</sup>
2.  现在，运行一个从 1 到 N 的循环，找到 I<sup>th</sup>[icosidigional numbers](https://www.geeksforgeeks.org/icosidigonal-number/)。
3.  将上面计算的所有 icosidigonal 数相加。
4.  最后，显示前 N 个 Icosidigonal 数的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N icosidigonal numbers
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// N-th icosidigonal number
int Icosidigonal_num(int n)
{

    // Formula to calculate
    // nth icosidigonal number
    return (20 * n * n - 18 * n) / 2;
}

// Function to find the sum of the
// first N icosidigonal number
int sum_Icosidigonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating in the range 1 to N
    for(int i = 1; i < n + 1; i++)
    {

        // Finding the sum
        summ += Icosidigonal_num(i);
    }
    return summ;
}

// Driver code
int main()
{
    int n = 6;

    // Display first Nth
    // icosidigonal numbers
    cout << sum_Icosidigonal_num(n);
}

// This code is contributed by coder001
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N icosidigonal numbers
class GFG{

// Function to find the
// N-th icosidigonal number
public static int Icosidigonal_num(int n)
{

    // Formula to calculate
    // nth icosidigonal number
    return (20 * n * n - 18 * n) / 2;
}

// Function to find the sum of the
// first N icosidigonal number
public static int sum_Icosidigonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating in the range 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Icosidigonal_num(i);
    }
    return summ;
}

// Driver code   
public static void main(String[] args)
{
    int n = 6;

    // Display first Nth
    // icosidigonal numbers
    System.out.println(sum_Icosidigonal_num(n));
}
}

// This code is contributed by divyeshrabadiya07   
```

## 蟒蛇 3

```
# Python3 program to find the
# sum of the first N 
# Icosidigonal numbers

# Function to find the
# N-th Icosidigonal
# number
def Icosidigonal_num(n):

    # Formula to calculate 
    # nth Icosidigonal
    # number
    return (20 * n * n -
            18 * n) // 2

# Function to find the
# sum of the first N
# Icosidigonal number
def sum_Icosidigonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Iterating in the range
    # 1 to N
    for i in range(1, n + 1):

        summ += Icosidigonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 6

    print(sum_Icosidigonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N icosidigonal numbers
using System;

class GFG{

// Function to find the
// N-th icosidigonal number
static int Icosidigonal_num(int n)
{

    // Formula to calculate
    // nth icosidigonal number
    return (20 * n * n - 18 * n) / 2;
}

// Function to find the sum of the
// first N icosidigonal number
static int sum_Icosidigonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating in the range 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Icosidigonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main(string[] args)
{
    int n = 6;

    // Display first Nth
    // icosidigonal numbers
    Console.WriteLine(sum_Icosidigonal_num(n));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to find the sum of the
    // first N icosidigonal numbers

    // Function to find the 
    // N-th icosidigonal number 
    function Icosidigonal_num(n) 
    {

        // Formula to calculate 
        // nth icosidigonal number
        return (20 * n * n - 18 * n) / 2;
    }

    // Function to find the sum of the
    // first N icosidigonal number 
    function sum_Icosidigonal_num(n)
    {

        // Variable to store the sum
        let summ = 0;

        // Iterating in the range 1 to N
        for(let i = 1; i < n + 1; i++)
        {

            // Finding the sum
            summ += Icosidigonal_num(i);
        }
        return summ;
    }

    let n = 6;

    // Display first Nth 
    // icosidigonal numbers
    document.write(sum_Icosidigonal_num(n));

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
721
```

**时间复杂度:** O(N)。