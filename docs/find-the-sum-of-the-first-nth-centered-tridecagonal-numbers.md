# 求第 n 个居中的三叉数的和

> 原文:[https://www . geesforgeks . org/find-第 n 个以第一个为中心的三叉戟数字之和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-centered-tridecagonal-numbers/)

给定一个数 **N** ，任务是求第一个 N [中心三叉数](https://www.geeksforgeeks.org/centered-tridecagonal-number/)的和。

> 居中的三叉数字表示连续三叉(13 边多边形)图层中位于中心的点和围绕中心点的其他点。前几个居中的三叉戟数字是 1，14，40，79 …

**例:**

> **输入:** N = 3
> **输出:** 55
> **说明:**
> 1、14、40 为前三个 Centered 三叉戟数字。
> 1 + 14 + 40 = 55。
> **输入:** N = 5
> **输出:** 265

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N 个<sup>[中心三叉数](https://www.geeksforgeeks.org/centered-tridecagonal-number/)。</sup>
2.  现在，运行一个从 1 到 N 的循环，在这个范围内找到居中的三叉数。
3.  将以上计算的所有居中三叉数相加。
4.  最后，显示前 N 个以 N 为中心的三叉戟数字的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of
// the first Nth centered
// tridecagonal number
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the
// N-th centered tridecagonal
// number
int Centered_tridecagonal_num(int n)
{
    // Formula to calculate
    // Nth centered tridecagonal
    // number & return it
    return (13 * n * (n - 1) + 2) / 2;
}

// Function to find the sum
// of the first N centered
// tridecagonal numbers
int sum_Centered_tridecagonal_num(int n)
{
    // Variable to store
    // the sum
    int summ = 0;

    // Loop to iterate and find the
    // sum of first N centered
    // tridecagonal numbers
    for(int i = 1; i <= n; i++)
    {
        summ += Centered_tridecagonal_num(i);
    }
    return summ ;
}

// Driver code
int main()
{
    int n = 5;

    cout << sum_Centered_tridecagonal_num(n)
         << endl;
    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// the first Nth centered
// tridecagonal number
class GFG{

// Function to calculate the
// N-th centered tridecagonal
// number
public static int Centered_tridecagonal_num(int n)
{

    // Formula to calculate
    // Nth centered tridecagonal
    // number & return it
    return (13 * n * (n - 1) + 2) / 2;
}

// Function to find the sum
// of the first N centered
// tridecagonal numbers
public static int sum_Centered_tridecagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Loop to iterate and find the
    // sum of first N centered
    // tridecagonal numbers
    for(int i = 1; i <= n; i++)
    {
       summ += Centered_tridecagonal_num(i);
    }
    return summ ;
}

// Driver code   
public static void main(String[] args)
{
    int n = 5;

    System.out.println(sum_Centered_tridecagonal_num(n));
}
}

// This code is contributed by divyeshrabadiya07   
```

## 蟒蛇 3

```
# Program to find the sum of
# the first Nth 
# Centered_tridecagonal number

# Function to calculate the
# N-th Centered tridecagonal
# number
def Centered_tridecagonal_num(n):

    # Formula to calculate 
    # Nth Centered tridecagonal
    # number & return it
    return (13 * n *
           (n - 1) + 2) // 2

# Function to find the sum
# of the first N
# Centered tridecagonal
# numbers
def sum_Centered_tridecagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Loop to iterate and find the
    # sum of first N Centered
    # tridecagonal numbers
    for i in range(1, n + 1):

        summ += Centered_tridecagonal_num(i)

    return summ

# Driver Code
if __name__ == '__main__' :

    n = 5

    print(sum_Centered_tridecagonal_num(n))
```

## C#

```
// C# program to find the sum of
// the first Nth centered
// tridecagonal number
using System;

class GFG{

// Function to calculate the
// N-th centered tridecagonal
// number
public static int Centered_tridecagonal_num(int n)
{

    // Formula to calculate
    // Nth centered tridecagonal
    // number & return it
    return (13 * n * (n - 1) + 2) / 2;
}

// Function to find the sum
// of the first N centered
// tridecagonal numbers
public static int sum_Centered_tridecagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Loop to iterate and find the
    // sum of first N centered
    // tridecagonal numbers
    for(int i = 1; i <= n; i++)
    {
       summ += Centered_tridecagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main()
{
    int n = 5;

    Console.WriteLine(sum_Centered_tridecagonal_num(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of 
    // the first Nth centered
    // tridecagonal number   

    // Function to calculate the 
    // N-th centered tridecagonal 
    // number 
    function Centered_tridecagonal_num(n)
    {

        // Formula to calculate 
        // Nth centered tridecagonal 
        // number & return it 
        return (13 * n * (n - 1) + 2) / 2;
    }

    // Function to find the sum 
    // of the first N centered
    // tridecagonal numbers 
    function sum_Centered_tridecagonal_num(n)
    {

        // Variable to store 
        // the sum 
        let summ = 0;

        // Loop to iterate and find the 
        // sum of first N centered 
        // tridecagonal numbers 
        for(let i = 1; i <= n; i++)
        {
            summ += Centered_tridecagonal_num(i); 
        }
        return summ ;
    }

    let n = 5;       
    document.write(sum_Centered_tridecagonal_num(n));

 // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
265
```

**时间复杂度:** O(N)。