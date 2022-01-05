# 求第一个 N 居中七边数的和

> 原文:[https://www . geesforgeks . org/find-第一个以 n 为中心的七边形数的和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-n-centered-heptagonal-number/)

给定一个数字 **N** ，任务是找出前 N 个[居中七边形数字](https://www.geeksforgeeks.org/centered-heptagonal-number/)的和。

> 前几个居中的七边形数字是 **1、8、22、43、71、106、148、……**

**例:**

> **输入:** N = 3
> **输出:** 31
> **说明:**
> 1、8、22 是前三个居中的七边数。
> **输入:** N = 5
> **输出:** 145

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算以 T2 为中心的第 N 个七边形数。
2.  现在，运行一个从 1 到 N 的循环，找到第 I<sup>[个居中的七边数](https://www.geeksforgeeks.org/centered-heptagonal-number/)。</sup>
3.  将上面计算的所有居中的七边形数相加。
4.  最后，显示前 N 个居中七边数的和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N centered heptagonal numbers
#include<bits/stdc++.h>
using namespace std;

// Function to find the N-th centered
// heptagonal number
int center_heptagonal_num(int n)
{

    // Formula to calculate
    // nth centered heptagonal
    // number
    return (7 * n * n - 7 * n + 2) / 2;
}

// Function to find the sum of the first
// N centered heptagonal numbers
int sum_center_heptagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
       summ += center_heptagonal_num(i);
    }
    return summ;
}

// Driver Code
int main()
{
    int n = 5;

    cout << (sum_center_heptagonal_num(n));
    return 0;
}

// This code is contributed by PratikBasu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N centered heptagonal numbers
class GFG{

// Function to find the N-th centered
// heptagonal number
public static int center_heptagonal_num(int n)
{

    // Formula to calculate
    // nth centered heptagonal
    // number
    return (7 * n * n - 7 * n + 2) / 2;
}

// Function to find the sum of the first
// N centered heptagonal numbers
public static int sum_center_heptagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
        summ += center_heptagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void main(String args[])
{
    int n = 5;

    System.out.print(sum_center_heptagonal_num(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of the first N centered
# heptagonal numbers

# Function to find N-th
# centered heptagonal
# number
def center_heptagonal_num(n):

    # Formula to calculate 
    # nth centered heptagonal
    # number
    return (7 * n * n - 7 * n + 2) // 2

# Function to find the
# sum of the first N
# centered heptagonal
# numbers
def sum_center_heptagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Iterate through the range
    # 1 to N
    for i in range(1, n + 1):
        summ += center_heptagonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 5

    print(sum_center_heptagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centered heptagonal numbers
using System;

class GFG{

// Function to find the N-th centered
// heptagonal number
public static int center_heptagonal_num(int n)
{

    // Formula to calculate
    // nth centered heptagonal
    // number
    return (7 * n * n - 7 * n + 2) / 2;
}

// Function to find the sum of the first
// N centered heptagonal numbers
public static int sum_center_heptagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
       summ += center_heptagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void Main()
{
    int n = 5;

    Console.Write(sum_center_heptagonal_num(n));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of the 
    // first N centered heptagonal numbers

    // Function to find the N-th centered
    // heptagonal number 
    function center_heptagonal_num(n)
    {

        // Formula to calculate
        // nth centered heptagonal 
        // number
        return (7 * n * n - 7 * n + 2) / 2;
    }

    // Function to find the sum of the first
    // N centered heptagonal numbers
    function sum_center_heptagonal_num(n)
    {

        // Variable to store
        // the sum
        let summ = 0;

        // Iterating through the range
        // 1 to N
        for(let i = 1; i < n + 1; i++)
        {
           summ += center_heptagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    document.write(sum_center_heptagonal_num(n));

</script>

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
145
```

**时间复杂度:** O(N)。