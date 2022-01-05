# 集合上不可逆和反对称的关系数

> 原文:[https://www . geeksforgeeks . org/关系数集上的非弹性和反对称/](https://www.geeksforgeeks.org/number-of-relations-that-are-both-irreflexive-and-antisymmetric-on-a-set/)

给定一个正整数 **N** ，任务是找出在给定元素集合上可以形成的[非弹性反对称关系](https://www.geeksforgeeks.org/relations-and-their-types/)的关系数。由于计数可能非常大，将其打印到模 **10 <sup>9</sup> + 7** 。

> 集合 **A** 上的关系 **R** 如果没有 **(a，a)** € **R** 适用于每个元素 **a € A** 。
> 例如:如果集合 A = {a，b}，那么 R = {(a，b)，(b，a)}就是不可逆关系。
> 
> 集合 **A** 上的关系 **R** 称为**反对称**当且仅当 **(a，b) € R** 和 **(b，a) € R** ，则 **a = b** 称为反对称，即关系 **R = {(a，b)→ R | a ≤ b** 为反对称，因为**A≤b**

**示例:**

> **输入:** N = 2
> **输出:** 3
> **解释:**
> 考虑集合{a，b}，所有可能的既非灵活又反对称的关系是:
> 
> 1.  {}
> 2.  {{a，b}}
> 3.  {{b，a}}
> 
> **输入:**N = 5
> T3】输出: 59049

**方法:**给定的问题可以基于以下观察来解决:

*   集合 **A** 上的关系 **R** 是集合的 [**笛卡儿积**](https://www.geeksforgeeks.org/sql-join-cartesian-join-self-join/) 的子集，即 A * A 带有 **N <sup>2</sup> 元素**。
*   不应该将 **(x，x)** 对包含在子集内，以确保关系为**非弹性**。
*   剩下的**(N<sup>2</sup>–N)**对，分成**(N<sup>2</sup>–N)/2 组**，每组由一对 **(x，y)** 及其对称对 **(y，x)** 组成。
*   现在，有**三个选择**，要么包含一个有序对，要么两个都不来自一个组。
*   因此，非弹性和反对称的可能关系的总数由**3<sup>(N2–N)/2</sup>**给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

const int mod = 1000000007;

// Function to calculate
// x ^ y % mod in O(log y)
int power(long long x,
unsigned int y)
{
    // Stores the result of x^y
    int res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    while (y > 0) {

        // If y is odd, then multiply
        // x with result
        if (y & 1)
            res = (res * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the value of x^y
    return res;
}

// Function to count relations that
// are  irreflexive and antisymmetric
// in a set consisting of N elements
int numberOfRelations(int N)
{
    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code
int main()
{
    int N = 2;
    cout << numberOfRelations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int mod = 1000000007;

// Function to calculate
// x ^ y % mod in O(log y)
static int power(long x, int y)
{

    // Stores the result of x^y
    int res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    while (y > 0)
    {

        // If y is odd, then multiply
        // x with result
        if (y % 2 == 1)
            res = (int)(res  * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the value of x^y
    return res;
}

// Function to count relations that
// are  irreflexive and antisymmetric
// in a set consisting of N elements
static int numberOfRelations(int N)
{

    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code
public static void main(String[] args)
{
    int N = 2;
    System.out.print(numberOfRelations(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
mod = 1000000007

# Function to calculate
# x ^ y % mod in O(log y)
def power(x,  y):

    # Stores the result of x^y
    res = 1

    # Update x if it exceeds mod
    x = x % mod

    while (y > 0):

        # If y is odd, then multiply
        # x with result
        if (y & 1):
            res = (res * x) % mod

        # Divide y by 2
        y = y >> 1

        # Update the value of x
        x = (x * x) % mod

    # Return the value of x^y
    return res

# Function to count relations that
# are  irreflexive and antisymmetric
# in a set consisting of N elements
def numberOfRelations(N):

    # Return the resultant count
    return power(3, (N * N - N) // 2)

# Driver Code
if __name__ == "__main__":

    N = 2
    print(numberOfRelations(N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int mod = 1000000007;

// Function to calculate
// x ^ y % mod in O(log y)
static int power(long x, int y)
{

    // Stores the result of x^y
    int res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    while (y > 0)
    {

        // If y is odd, then multiply
        // x with result
        if (y % 2 == 1)
            res = (int)(res  * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the value of x^y
    return res;
}

// Function to count relations that
// are  irreflexive and antisymmetric
// in a set consisting of N elements
static int numberOfRelations(int N)
{

    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2;
    Console.Write(numberOfRelations(N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let mod = 1000000007;

// Function to calculate
// x ^ y % mod in O(log y)
function power(x, y)
{
    // Stores the result of x^y
    let res = 1;

    // Update x if it exceeds mod
    x = x % mod;

    while (y > 0) {

        // If y is odd, then multiply
        // x with result
        if (y & 1)
            res = (res * x) % mod;

        // Divide y by 2
        y = y >> 1;

        // Update the value of x
        x = (x * x) % mod;
    }

    // Return the value of x^y
    return res;
}

// Function to count relations that
// are  irreflexive and antisymmetric
// in a set consisting of N elements
function numberOfRelations(N)
{
    // Return the resultant count
    return power(3, (N * N - N) / 2);
}

// Driver Code

     let N = 2;
    document.write(numberOfRelations(N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*