# 求第一个 N 中心八角数的和

> 原文:[https://www . geeksforgeeks . org/find-第一个以 n 为中心的八边形数字的总和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-n-centered-octagonal-number/)

给定一个数 N，任务是求前 N 个[居中的八边形数](https://www.geeksforgeeks.org/centered-octagonal-number/)的和。

> 前几个居中的八边形数字是 **1、9、25、49、81、121、169、225、289、361……**

**例:**

> **输入:** N = 3
> **输出:** 35
> **说明:**
> 1、9、25 是前三个居中的八角形数字。
> **输入:** N = 5
> **输出:** 165

**进场:**

1.  首先，我们需要创建一个函数来帮助我们计算第 N<sup>[个以八角形为中心的数字](https://www.geeksforgeeks.org/centered-octagonal-number/)。</sup>
2.  现在，运行一个从 1 到 N 的循环，找到第 I<sup>[个居中的八边形数字](https://www.geeksforgeeks.org/centered-octagonal-number/)。</sup>
3.  将上面计算的所有居中的八边形数字相加。
4.  最后，显示前 N 个居中的八边形数字的总和。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// first N centered octagonal number
#include<bits/stdc++.h>
using namespace std;

// Function to find the N-th centered
// octagonal number
int center_Octagonal_num(int n)
{

    // Formula to calculate
    // nth centered octagonal
    // number
    return (4 * n * n - 4 * n + 1);
}

// Function to find the sum of the first
// N centered octagonal numbers
int sum_center_Octagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the range
    // 1 to N
    for(int i = 1; i < n + 1; i++)
    {
       summ += center_Octagonal_num(i);
    }
    return summ;
}

// Driver Code
int main()
{
    int n = 5;

    cout << (sum_center_Octagonal_num(n));
    return 0;
}

// This code is contributed by PratikBasu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// first N centered octagonal number
class GFG {

// Function to find N-th centered
// octagonal number
static int center_Octagonal_num(int n)
{

    // Formula to calculate
    // nth centered octagonal
    // number
    return (4 * n * n - 4 * n + 1);
}

// Function to find the
// sum of the first N
// centered octagonal
// numbers
static int sum_center_Octagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the first N
    // numbers
    for(int i = 1; i < n + 1; i++)
    {
       summ += center_Octagonal_num(i);
    }
    return summ;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    System.out.println(sum_center_Octagonal_num(n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the
# sum of the first N
# Centered Octagonal number

# Function to find N-th
# Centered Octagonal
# number
def center_Octagonal_num(n):

    # Formula to calculate 
    # nth centered Octagonal
    # number
    return (4 * n * n - 4 * n + 1)

# Function to find the
# sum of the first N
# Centered Octagonal
# numbers
def sum_center_Octagonal_num(n) :

    # Variable to store
    # the sum
    summ = 0

    # Iterating through the first N
    # numbers
    for i in range(1, n + 1):

        summ += center_Octagonal_num(i)

    return summ

# Driver code
if __name__ == '__main__' :

    n = 5

    print(sum_center_Octagonal_num(n))
```

## C#

```
// C# program to find the sum of the
// first N centered octagonal number
using System;

class GFG{

// Function to find N-th centered
// octagonal number
static int center_Octagonal_num(int n)
{

    // Formula to calculate
    // nth centered octagonal
    // number
    return (4 * n * n - 4 * n + 1);
}

// Function to find the sum of
// the first N centered octagonal
// numbers
static int sum_center_Octagonal_num(int n)
{

    // Variable to store
    // the sum
    int summ = 0;

    // Iterating through the first N
    // numbers
    for(int i = 1; i < n + 1; i++)
    {
       summ += center_Octagonal_num(i);
    }
    return summ;
}

// Driver code
public static void Main()
{
    int n = 5;

    Console.WriteLine(sum_center_Octagonal_num(n));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

    // Javascript program to find the sum of the 
    // first N centered octagonal number

    // Function to find the N-th centered
    // octagonal number 
    function center_Octagonal_num(n)
    {

        // Formula to calculate
        // nth centered octagonal 
        // number
        return (4 * n * n - 4 * n + 1);
    }

    // Function to find the sum of the first
    // N centered octagonal numbers
    function sum_center_Octagonal_num(n)
    {

        // Variable to store
        // the sum
        let summ = 0;

        // Iterating through the range
        // 1 to N
        for(let i = 1; i < n + 1; i++)
        {
           summ += center_Octagonal_num(i);
        }
        return summ;
    }

    let n = 5;

    document.write(sum_center_Octagonal_num(n));

</script>

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
165
```

**时间复杂度:** O(N)。