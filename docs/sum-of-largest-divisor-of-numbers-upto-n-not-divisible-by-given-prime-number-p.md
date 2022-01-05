# 不可被给定素数 P 整除的数的最大除数之和

> 原文:[https://www . geeksforgeeks . org/数的最大除数之和-up-n-不可被给定素数除尽-p/](https://www.geeksforgeeks.org/sum-of-largest-divisor-of-numbers-upto-n-not-divisible-by-given-prime-number-p/)

给定一个数 **N** 和一个[质数](https://www.geeksforgeeks.org/prime-numbers/) **P** ，任务是求**【1，N】**范围内每个数的最大除数之和，这个数不能被 **P** 整除。

**示例:**

> **输入:** N = 8，P = 2
> **输出:** 22
> **说明:**数字在[1，8]范围内。
> **不能被 P 整除的数最大除数= 2**
> 1 1
> 2 1
> 3 3
> 4 1
> 5 5
> 6 3
> 7
> 8**1
> 给定约束的所有除数之和= 22。**
> 
> ****输入:** N = 10，P = 5
> **输出:** 43
> **说明:**数字在[1，8]范围内。
> **不能被 P 整除的最大除数= 5**
> 1 1
> 2 2
> 3 3
> 4
> 5 1
> 6
> 7
> 8
> 9
> 10 2
> 给定约束条件下所有除数之和= 43**

****天真的做法:**天真的想法是[找到范围**【1，N】**中每个数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)的除数，找到最大的不能被 **P** 和那些数整除的除数。打印所有最大除数的总和。
***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(1)*
**高效方法:**其思想是观察一个数的最大除数 **N** 不能被 **P** 整除，如果 **N** 则为 **N** 本身否则所需除数将与**不适用**相同。以下是步骤:**

1.  **如果 N 不能被 P 整除，那么最大的除数就是 **N** ，把这个加到最后的和上。**
2.  **如果 N 能被 P 整除，所需除数将与 **N/P** 相同。**
3.  **所以，求所有不能被 **P** 整除的数的和，分别加上那些能被 P 整除的数的除数。**
4.  **总和将为 **N*(N + 1)/2** 。减去那些可被 **P** 整除的和，通过递归调用函数相加它们相应的值，找到 **N/P** 的和。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of largest
// divisors of numbers in range 1 to N
// not divisible by prime number P
int func(int N, int P)
{
    // Total sum upto N
    int sumUptoN = (N * (N + 1) / 2);
    int sumOfMultiplesOfP;

    // If no multiple of P exist up to N
    if (N < P) {
        return sumUptoN;
    }

    // If only P itself is in the range
    // from 1 to N
    else if ((N / P) == 1) {
        return sumUptoN - P + 1;
    }

    // Sum of those that are divisible by P
    sumOfMultiplesOfP
        = ((N / P) * (2 * P + (N / P - 1) * P)) / 2;

    // Recursively function call to
    // find the sum for N/P
    return (sumUptoN
            + func(N / P, P)
            - sumOfMultiplesOfP);
}

// Driver Code
int main()
{
    // Given N and P
    int N = 10, P = 5;

    // Function Call
    cout << func(N, P) << "\n";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
class GFG{

// Function to find the sum of largest
// divisors of numbers in range 1 to N
// not divisible by prime number P
static int func(int N, int P)
{

    // Total sum upto N
    int sumUptoN = (N * (N + 1) / 2);
    int sumOfMultiplesOfP;

    // If no multiple of P exist up to N
    if (N < P)
    {
        return sumUptoN;
    }

    // If only P itself is in the range
    // from 1 to N
    else if ((N / P) == 1)
    {
        return sumUptoN - P + 1;
    }

    // Sum of those that are divisible by P
    sumOfMultiplesOfP = ((N / P) * (2 * P +
                         (N / P - 1) * P)) / 2;

    // Recursively function call to
    // find the sum for N/P
    return (sumUptoN + func(N / P, P) -
            sumOfMultiplesOfP);
}

// Driver Code
public static void main(String[] args)
{

    // Given N and P
    int N = 10, P = 5;

    // Function call
    System.out.println(func(N, P));
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program for the
# above approach

# Function to find the sum
# of largest divisors of
# numbers in range 1 to N
# not divisible by prime number P
def func(N, P):

    # Total sum upto N
    sumUptoN = (N * (N + 1) / 2);
    sumOfMultiplesOfP = 0;

    # If no multiple of P exist
    # up to N
    if (N < P):
        return sumUptoN;

    # If only P itself is
    # in the range from 1
    # to N
    elif ((N / P) == 1):
        return sumUptoN - P + 1;

    # Sum of those that are
    # divisible by P
    sumOfMultiplesOfP = (((N / P) *
                         (2 * P +
                         (N / P - 1) *
                          P)) / 2);

    # Recursively function call to
    # find the sum for N/P
    return (sumUptoN +
            func(N / P, P) -
            sumOfMultiplesOfP);

# Driver Code
if __name__ == '__main__':

    # Given N and P
    N = 10;
    P = 5;

    # Function call
    print(func(N, P));

# This code is contributed by Rajput-Ji
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to find the sum of largest
// divisors of numbers in range 1 to N
// not divisible by prime number P
static int func(int N, int P)
{

    // Total sum upto N
    int sumUptoN = (N * (N + 1) / 2);
    int sumOfMultiplesOfP;

    // If no multiple of P exist up to N
    if (N < P)
    {
        return sumUptoN;
    }

    // If only P itself is in the range
    // from 1 to N
    else if ((N / P) == 1)
    {
        return sumUptoN - P + 1;
    }

    // Sum of those that are divisible by P
    sumOfMultiplesOfP = ((N / P) * (2 * P +
                         (N / P - 1) * P)) / 2;

    // Recursively function call to
    // find the sum for N/P
    return (sumUptoN + func(N / P, P) -
            sumOfMultiplesOfP);
}

// Driver Code
public static void Main(String[] args)
{

    // Given N and P
    int N = 10, P = 5;

    // Function call
    Console.WriteLine(func(N, P));
}
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
<script>
// JavaScript program for the above approach

// Function to find the sum of largest
// divisors of numbers in range 1 to N
// not divisible by prime number P
function func(N, P)
{

    // Total sum upto N
    let sumUptoN = (N * (N + 1) / 2);
    let sumOfMultiplesOfP;

    // If no multiple of P exist up to N
    if (N < P)
    {
        return sumUptoN;
    }

    // If only P itself is in the range
    // from 1 to N
    else if ((N / P) == 1)
    {
        return sumUptoN - P + 1;
    }

    // Sum of those that are divisible by P
    sumOfMultiplesOfP = ((N / P) * (2 * P +
                         (N / P - 1) * P)) / 2;

    // Recursively function call to
    // find the sum for N/P
    return (sumUptoN + func(N / P, P) -
            sumOfMultiplesOfP);
}

// Driver Code

    // Given N and P
    let N = 10, P = 5;

    // Function call
    document.write(func(N, P));

</script>
```

****Output:** 

```
43
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**