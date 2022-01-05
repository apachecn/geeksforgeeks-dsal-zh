# 求前 N 个居中的十八边形数的和

> 原文:[https://www . geesforgeks . org/find-第一个以 n 为中心的十八进制数字的总和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-n-centered-octadecagonal-numbers/)

给定一个数字 **N** ，任务是找到前 N 个[中心十八边形数字](https://www.geeksforgeeks.org/centered-octadecagonal-number/)的和。
**例:**

> **输入:** N = 3
> **输出:** 75
> **说明:**
> 1、19、55 是前三个居中的十八进制数。
> **输入:** N = 10
> **输出:** 298

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个以十八边形为中心的数](https://www.geeksforgeeks.org/centered-octadecagonal-number/)。</sup>
2.  现在，运行一个从 1 到 N 的循环，找到以十八进制数字为中心的 i <sup>th</sup> [。](https://www.geeksforgeeks.org/centered-octadecagonal-number/)
3.  将上面计算的所有居中的十八进制数相加。
4.  最后，显示前 N 个居中的十八进制数的和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N centered octadecagonal numbers
#include<bits/stdc++.h>
using namespace std;

// Function to find the N-th centered
// octadecagonal number
int center_octadecagon_num(int n)
{

    // Formula to calculate
    // nth centered octadecagonal
    // number
    return (9 * n * n - 9 * n + 1);
}

// Function to find the sum of the first
// N centered octadecagonal numbers
int sum_center_octadecagon_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
        summ += center_octadecagon_num(i);
    }
    return summ;
}

// Driver Code
int main()
{
    int n = 3;

    cout << (sum_center_octadecagon_num(n));
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the 
// first N centered octadecagonal numbers
class GFG {

// Function to find the N-th centered
// octadecagonal number
static int center_octadecagon_num(int n)
{

    // Formula to calculate
    // nth centered octadecagonal
    // number
    return (9 * n * n - 9 * n + 1);
}

// Function to find the sum of the first
// N centered octadecagonal numbers
static int sum_center_octadecagon_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
       summ += center_octadecagon_num(i);
    }
    return summ;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;

    System.out.println(sum_center_octadecagon_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# the first N Centered Octadecagonal
# numbers

# Function to find the N-th
# Centered octadecagonal
# number
def center_octadecagon_num(n):

    # Formula to calculate 
    # nth centered octadecagonal
    # number
    return (9 * n * n - 9 * n + 1)

# Function to find the sum of
# the first N Centered
# octadecagonal numbers
def sum_center_octadecagon_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Iterating through the range
    # 1 to N
    for i in range(1, n + 1):

        summ += center_octadecagon_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 3

    print(sum_center_octadecagon_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centered octadecagonal numbers
using System;

class GFG {

// Function to find the N-th centered
// octadecagonal number
static int center_octadecagon_num(int n)
{

    // Formula to calculate
    // nth centered octadecagonal
    // number
    return (9 * n * n - 9 * n + 1);
}

// Function to find the sum of the first
// N centered octadecagonal numbers
static int sum_center_octadecagon_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
        summ += center_octadecagon_num(i);
    }
    return summ;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine(sum_center_octadecagon_num(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
    // Javascript program to find the sum of the 
    // first N centered octadecagonal numbers

    // Function to find the N-th centered
    // octadecagonal number
    function center_octadecagon_num(n)
    {

        // Formula to calculate
        // nth centered octadecagonal
        // number
        return (9 * n * n - 9 * n + 1);
    }

    // Function to find the sum of the first
    // N centered octadecagonal numbers
    function sum_center_octadecagon_num(n)
    {

        // Variable to store
        // the sum
        let summ = 0;

        // Iterating through the range
        // 1 to N
        for(let i = 1; i < n + 1; i++)
        {
            summ += center_octadecagon_num(i);
        }
        return summ;
    }

    let n = 3;
    document.write(sum_center_octadecagon_num(n));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
75
```

**时间复杂度:** O(N)。