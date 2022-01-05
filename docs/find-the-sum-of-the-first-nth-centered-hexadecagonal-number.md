# 求第一个第 n 个居中的六边形数的和

> 原文:[https://www . geesforgeks . org/find-第 n 个中心十六边形数的和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-centered-hexadecagonal-number/)

给定一个数 N，任务是求第一个 N 的和[居中的六边形数](https://www.geeksforgeeks.org/centered-hexadecagonal-number/)。

> 前几个居中的十六边形数字是 1、17、49、97、161、241……

**示例:**

> **输入:** N = 3
> **输出:** 67
> **说明:**
> 1、17、49 是前三个居中的十六进制数。
> **输入:** N = 5
> **输出:** 325

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个居中的六边形数](https://www.geeksforgeeks.org/centered-hexadecagonal-number/)。</sup>
2.  现在，我们运行一个从 1 到 N 的循环，找到一个以十六边形为中心的数。
3.  将上面计算的所有居中十六边形数相加。
4.  最后，显示第一个以 N 为中心的十六边形数的和。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of the first
// N centered hexadecagonal numbers
#include <bits/stdc++.h>
using namespace std;

// Centered_Hexadecagonal
// number function
int Centered_Hexadecagonal_num(int n)
{

    // Formula to calculate nth
    // Centered_Hexadecagonal
    // number & return it into
    // main function.
    return (8 * n * n - 8 * n + 1);
}

// Function to find the sum of the first
// N centered hexadecagonal number
int sum_Centered_Hexadecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Loop to iterate through the
    // first N numbers
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Centered_Hexadecagonal_num(i);
    }
    return summ;
}

// Driver code
int main()
{
    int n = 5;

    // Display first Nth
    // Centered_Hexadecagonal number
    cout << sum_Centered_Hexadecagonal_num(n);
}

// This code is contributed by coder001
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the first
// N centered hexadecagonal numbers

class GFG{

// Centered_Hexadecagonal
// number function
public static int Centered_Hexadecagonal_num(int n)
{

    // Formula to calculate nth
    // Centered_Hexadecagonal
    // number & return it into
    // main function.
    return (8 * n * n - 8 * n + 1);
}

// Function to find the sum of the first
// N centered hexadecagonal number
public static int sum_Centered_Hexadecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Loop to iterate through the
    // first N numbers
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Centered_Hexadecagonal_num(i);
    }
    return summ;
}

// Driver Code   
public static void main(String[] args)
{
    int n = 5;

    // Display first Nth
    // Centered_Hexadecagonal number
    System.out.println(sum_Centered_Hexadecagonal_num(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# the first N centered
# hexadecagonal numbers

# Centered_Hexadecagonal
# number function
def Centered_Hexadecagonal_num(n):
    # Formula to calculate 
    # nth Centered_Hexadecagonal
    # number & return it
    # into main function.
    return (8 * n * n -
            8 * n + 1)

# Function to find the
# sum of the first N
# Centered Hexadecagonal
# number
def sum_Centered_Hexadecagonal_num(n) :

    # Variable to store the
    # sum
    summ = 0

    # Loop to iterate through the
    # first N numbers
    for i in range(1, n + 1):

        # Find the sum
        summ += Centered_Hexadecagonal_num(i)

    return summ

# Driver Code
if __name__ == '__main__' :

    n = 5

    # display first Nth
    # Centered_Hexadecagonal number
    print(sum_Centered_Hexadecagonal_num(n))
```

## C#

```
// C# program to find the sum of the first
// N centered hexadecagonal numbers
using System;

class GFG{

// Centered_Hexadecagonal
// number function
public static int Centered_Hexadecagonal_num(int n)
{

    // Formula to calculate nth
    // Centered_Hexadecagonal
    // number & return it into
    // main function.
    return (8 * n * n - 8 * n + 1);
}

// Function to find the sum of the first
// N centered hexadecagonal number
public static int sum_Centered_Hexadecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Loop to iterate through the
    // first N numbers
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += Centered_Hexadecagonal_num(i);
    }
    return summ;
}

// Driver Code
public static void Main()
{
    int n = 5;

    // Display first Nth
    // Centered_Hexadecagonal number
    Console.Write(sum_Centered_Hexadecagonal_num(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
  // Javascript program to find the sum of the first 
  // N centered hexadecagonal numbers

  // Centered_Hexadecagonal 
  // number function
  function Centered_Hexadecagonal_num(n) 
  {

      // Formula to calculate nth 
      // Centered_Hexadecagonal 
      // number & return it into
      // main function. 
      return (8 * n * n - 8 * n + 1);
  }

  // Function to find the sum of the first
  // N centered hexadecagonal number
  function sum_Centered_Hexadecagonal_num(n)
  {

      // Variable to store the sum
      let summ = 0;

      // Loop to iterate through the
      // first N numbers
      for(let i = 1; i < n + 1; i++)
      {

         // Finding the sum
         summ += Centered_Hexadecagonal_num(i);
      }
      return summ;
  }

  let n = 5;

  // Display first Nth 
  // Centered_Hexadecagonal number
  document.write(sum_Centered_Hexadecagonal_num(n));

  // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
325
```

**时间复杂度:** O(N)