# 求第 n 个二进制数的和

> 原文:[https://www . geeksforgeeks . org/find-第 n 个数字的总和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-icosagonal-numbers/)

给定一个数字 **N** ，任务是找到第一个**N**T4】二叉数的和。

> 前几个 Icosagonal 数字是 **1，20，57，112，185，276…**

**例:**

> **输入:** N = 3
> **输出:** 78
> **说明:**
> 1、20、57 是前三个
> Icosagonal 数。
> **输入:** N = 5
> **输出:** 375

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N 个 [Icosagonal 数](https://www.geeksforgeeks.org/icosagonal-number/)。
2.  现在，运行一个从 1 到 **N，**的循环，以找到所有 Icosagonal 数的和。
3.  现在，将上面计算的所有 Icosagonal 数相加。
4.  最后，显示第 1**N**个二进制数之和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of
// the first N icosagonal number
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the
// N-th icosagonal number
int Icosagonal_num(int n)
{
    // Formula to calculate
    // nth icosagonal number
    // & return it
    return (18 * n * n - 16 * n) / 2;
}

// Function to find the
// sum of the first N
// icosagonal numbers
int sum_Icosagonal_num(int n)
{
    // Variable to store
    // the sum
    int summ = 0;

    // Loop to iterate through
    // the first N values and
    // find the sum of first N
    // icosagonal numbers
    for(int i = 1; i <= n; i++)
    {

        // Function to get the
        // Icosagonal_num
        summ += Icosagonal_num(i);
    }
    return summ;
}

// Driver code
int main()
{
    int n = 5;

    // Display the sum of
    // first N icosagonal number
    cout << sum_Icosagonal_num(n) << endl;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// the first N icosagonal number
class GFG{

// Function to calculate the
// N-th icosagonal number
public static int Icosagonal_num(int n)
{

    // Formula to calculate
    // nth icosagonal number
    // & return it
    return (18 * n * n - 16 * n) / 2;
}

// Function to find the
// sum of the first N
// icosagonal numbers
public static int sum_Icosagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Loop to iterate through
    // the first N values and
    // find the sum of first N
    // icosagonal numbers
    for(int i = 1; i <= n; i++)
    {

       // Function to get the
       // Icosagonal_num
       summ += Icosagonal_num(i);
    }
    return summ;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    // Display the sum of
    // first N icosagonal number
    System.out.println(sum_Icosagonal_num(n));
}
}

// This code is contributed by divyeshrabadiya07       
```

## 蟒蛇 3

```
# Python program to find the
# sum of the first N 
# Icosagonal number

# Function to calculate the
# N-th Icosagonal number
def Icosagonal_num(n):

    # Formula to calculate 
    # nth Icosagonal
    # number & return it 
    return (18 * n * n -
            16 * n) // 2

# Function to find the
# sum of the first N
# Icosagonal numbers
def sum_Icosagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Loop to iterate through
    # the first N values and
    # find the sum of first N
    # Icosagonal numbers
    for i in range(1, n + 1):

        # function to get the
        # Icosagonal_num
        summ += Icosagonal_num(i)

    return summ

# Driver Code
if __name__ == '__main__' :

    n = 5

    # Display the sum of
    # first N Icosagonal number
    print(sum_Icosagonal_num(n))
```

## C#

```
// C# program to find the sum of
// the first N icosagonal number
using System;

class GFG{

// Function to calculate the
// N-th icosagonal number
public static int Icosagonal_num(int n)
{

    // Formula to calculate
    // nth icosagonal number
    // & return it
    return (18 * n * n - 16 * n) / 2;
}

// Function to find the
// sum of the first N
// icosagonal numbers
public static int sum_Icosagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Loop to iterate through
    // the first N values and
    // find the sum of first N
    // icosagonal numbers
    for(int i = 1; i <= n; i++)
    {

       // Function to get the
       // Icosagonal_num
       summ += Icosagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main()
{
    int n = 5;

    // Display the sum of
    // first N icosagonal number
    Console.WriteLine(sum_Icosagonal_num(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of
      // the first N icosagonal number

    // Function to calculate the 
    // N-th icosagonal number 
    function Icosagonal_num(n)
    {
        // Formula to calculate 
        // nth icosagonal number 
        // & return it 
        return (18 * n * n - 16 * n) / 2;
    }

    // Function to find the 
    // sum of the first N 
    // icosagonal numbers 
    function sum_Icosagonal_num(n)
    {
        // Variable to store 
        // the sum 
        let summ = 0;

        // Loop to iterate through 
        // the first N values and 
        // find the sum of first N 
        // icosagonal numbers 
        for(let i = 1; i <= n; i++)
        {

            // Function to get the 
            // Icosagonal_num 
            summ += Icosagonal_num(i); 
        }
        return summ;
    }

      let n = 5; 

    // Display the sum of 
    // first N icosagonal number
    document.write(sum_Icosagonal_num(n));

</script>
```

**Output:** 

```
375
```

**时间复杂度:** O(N)