# 求第 n 个七进制数的和

> 原文:[https://www . geeksforgeeks . org/find-第一个-第 n 个-第七个-十进制数之和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-nth-heptadecagonal-number/)

给定一个数 N，任务是求前 N 个[七个数](https://www.geeksforgeeks.org/heptadecagonal-number/)的和。

> 前几个七位数字是 **1、17、48、94、155、231……**

**例:**

> **输入:** N = 3
> **输出:** 66
> **说明:**
> 1、17、48 是前三个七进制数。
> **输入:** N = 6
> **输出:** 546

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N <sup>个</sup> [个十七进制数](https://www.geeksforgeeks.org/heptadecagonal-number/)。
2.  现在，运行一个从 1 到 N 的循环，找到第 I<sup>[个七进制数。](https://www.geeksforgeeks.org/heptadecagonal-number/)</sup>
3.  把上面计算的所有七进制数相加。
4.  最后，显示前 N 个七进制数的和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N heptadecagonal numbers
#include <bits/stdc++.h>
using namespace std;

// Function to find the N-th
// heptadecagonal number
int heptadecagonal_num(int n)
{

    // Formula to calculate nth
    // heptadecagonal number
    return ((15 * n * n) - 13 * n) / 2;
}

// Function to find the sum of the
// first N heptadecagonal numbers
int sum_heptadecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating from 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += heptadecagonal_num(i);
    }
    return summ;
}

// Driver code
int main()
{
    int n = 5;

    cout << sum_heptadecagonal_num(n);
}

// This code is contributed by coder001
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N heptadecagonal numbers
class GFG{

// Function to find the N-th
// heptadecagonal number
public static int heptadecagonal_num(int n)
{

    // Formula to calculate nth
    // heptadecagonal number
    return ((15 * n * n) - 13 * n) / 2;
}

// Function to find the sum of the
// first N heptadecagonal numbers
public static int sum_heptadecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating from 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += heptadecagonal_num(i);
    }
    return summ;
}

// Driver code    
public static void main(String[] args)
{
    int n = 5;

    System.out.println(sum_heptadecagonal_num(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of the first N 
# heptadecagonal numbers

# Function to find the
# N-th heptadecagonal
# number
def heptadecagonal_num(n):

    # Formula to calculate 
    # nth heptadecagonal
    # number
    return ((15 * n * n) - 13 * n) // 2

# Function to find the
# sum of the first N
# heptadecagonal numbers
def sum_heptadecagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Iterate from 1 to N
    for i in range(1, n + 1):

        summ += heptadecagonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 5

    print(sum_heptadecagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N heptadecagonal numbers
using System;

class GFG{

// Function to find the N-th
// heptadecagonal number
public static int heptadecagonal_num(int n)
{

    // Formula to calculate nth
    // heptadecagonal number
    return ((15 * n * n) - 13 * n) / 2;
}

// Function to find the sum of the
// first N heptadecagonal numbers
public static int sum_heptadecagonal_num(int n)
{

    // Variable to store the sum
    int summ = 0;

    // Iterating from 1 to N
    for(int i = 1; i < n + 1; i++)
    {

       // Finding the sum
       summ += heptadecagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main()
{
    int n = 5;

    Console.WriteLine(sum_heptadecagonal_num(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of the
    // first N heptadecagonal numbers

    // Function to find the N-th
    // heptadecagonal number 
    function heptadecagonal_num(n) 
    {

        // Formula to calculate nth
        // heptadecagonal number 
        return ((15 * n * n) - 13 * n) / 2;
    }

    // Function to find the sum of the
    // first N heptadecagonal numbers 
    function sum_heptadecagonal_num(n)
    {

        // Variable to store the sum
        let summ = 0;

        // Iterating from 1 to N
        for(let i = 1; i < n + 1; i++)
        {

           // Finding the sum
           summ += heptadecagonal_num(i);
        }
        return summ;
    }

    let n = 5;
    document.write(sum_heptadecagonal_num(n));

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
315
```

**时间复杂度:** O(N)。