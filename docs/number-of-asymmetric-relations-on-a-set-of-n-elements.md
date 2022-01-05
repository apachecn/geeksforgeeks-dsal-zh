# 一组 N 个元素上的不对称关系数

> 原文:[https://www . geesforgeks . org/n 元素集合上的非对称关系数/](https://www.geeksforgeeks.org/number-of-asymmetric-relations-on-a-set-of-n-elements/)

给定一个正整数 **N** ，任务是在一组 **N** 元素中找到**[**关系**T7】的个数。由于关系数可以很大，打印出来](https://www.geeksforgeeks.org/relations-and-their-types/)[模 10 <sup>9</sup> +7](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。**

> **集合 **A** 上的关系 **R** 称为**非对称**当且仅当 **x R y** 存在时，则**y**T10**R**T13**x**为每一个 **(x，y) € A** 。
> **比如:**如果设置 **A** **= {a，b}，**那么 **R = {(a，b)}** 就是不对称关系。**

****示例:****

> ****输入:** N = 2
> **输出:** 3
> **说明:**考虑集合{1，2}，可能的不对称关系总数为{{}、{(1，2)}、{(2，1)}}。**
> 
>  ****输入:**N = 5
> T3】输出: 59049**

****方法:**给定的问题可以基于以下观察来解决:**

*   **集合 **A** 上的 A **关系** **R** 是集合的 [**笛卡尔乘积**的**子集**，即 **A * A** 与 **N <sup>2</sup>** 元素。](https://www.geeksforgeeks.org/cartesian-product-of-sets/)**
*   **笛卡尔乘积中存在总共 **N** 对类型 **(x，x)** ，其中任何 **(x，x)** 都不应包含在子集内。**
*   **现在，剩下一个是**笛卡儿积的**(N<sup>2</sup>–N)**元素。****
*   **为了满足非对称关系的性质，有**三种可能性**，要么只包括类型为 **(x，y)** 的，要么只包括类型为 **(y，x)** 的，要么不从单个组进入子集。**
*   **因此，可能的**不对称关系**的总数等于**3<sup>(N2–N)/2</sup>。****

**因此，想法是打印**3<sup>(N2–N)/2</sup>模 10 <sup>9</sup> + 7** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <iostream>
using namespace std;

const int mod = 1000000007;

// Function to calculate
// x^y modulo (10^9 + 7)
int power(long long x,
          unsigned int y)
{
    // Stores the result of x^y
    int res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0) {

        // If y is odd, then
        // multiply x with result
        if (y & 1)
            res = (res * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the final
    // value of x ^ y
    return res;
}

// Function to count the number of
// asymmetric relations in a set
// consisting of N elements
int asymmetricRelation(int N)
{
    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code
int main()
{
    int N = 2;
    cout << asymmetricRelation(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG{

final static int mod = 1000000007;

// Function to calculate
// x^y modulo (10^9 + 7)
public static int power(int x, int y)
{

    // Stores the result of x^y
    int res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd, then
        // multiply x with result
        if (y % 2 == 1)
            res = (res * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the final
    // value of x ^ y
    return res;
}

// Function to count the number of
// asymmetric relations in a set
// consisting of N elements
public static int asymmetricRelation(int N)
{

    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver code
public static void main (String[] args)
{
    int N = 2;

    System.out.print(asymmetricRelation(N));
}
}

// This code is contributed by user_qa7r
```

## **蟒蛇 3**

```
# Python3 program for the above approach
mod = 1000000007

# Function to calculate
# x^y modulo (10^9 + 7)
def power(x, y):

    # Stores the result of x^y
    res = 1

    # Update x if it exceeds mod
    x = x % mod

    # If x is divisible by mod
    if (x == 0):
        return 0

    while (y > 0):

        # If y is odd, then
        # multiply x with result
        if (y & 1):
            res = (res * x) % mod;

        # Divide y by 2
        y = y >> 1

        # Update the value of x
        x = (x * x) % mod

    # Return the final
    # value of x ^ y
    return res

# Function to count the number of
# asymmetric relations in a set
# consisting of N elements
def asymmetricRelation(N):

    # Return the resultant count
    return power(3, (N * N - N) // 2)

# Driver Code
if __name__ == '__main__':

    N = 2

    print(asymmetricRelation(N))

# This code is contributed by SURENDRA_GANGWAR
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

const int mod = 1000000007;

// Function to calculate
// x^y modulo (10^9 + 7)
static int power(int x, int y)
{

    // Stores the result of x^y
    int res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd, then
        // multiply x with result
        if ((y & 1) != 0)
            res = (res * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the final
    // value of x ^ y
    return res;
}

// Function to count the number of
// asymmetric relations in a set
// consisting of N elements
static int asymmetricRelation(int N)
{

    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 2;
    Console.WriteLine(asymmetricRelation(N));
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

var mod = 1000000007;

// Function to calculate
// x^y modulo (10^9 + 7)
function power(x, y)
{
    // Stores the result of x^y
    var res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0) {

        // If y is odd, then
        // multiply x with result
        if (y & 1)
            res = (res * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the final
    // value of x ^ y
    return res;
}

// Function to count the number of
// asymmetric relations in a set
// consisting of N elements
function asymmetricRelation( N)
{
    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code
var N = 2;
document.write( asymmetricRelation(N));

</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N*log N)*
***辅助空间:** O(1)***