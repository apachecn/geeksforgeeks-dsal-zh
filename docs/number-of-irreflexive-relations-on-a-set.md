# 集合上不可逆关系的个数

> 原文:[https://www . geeksforgeeks . org/非灵活关系集数/](https://www.geeksforgeeks.org/number-of-irreflexive-relations-on-a-set/)

给定一个正整数 **N** ，任务是找出在给定的元素集合上可以形成的不灵活的 [**关系**](https://www.geeksforgeeks.org/relations-and-their-types/) 的数量。由于计数可以很大，打印到 [**模 10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

> 集合 **A** 上的关系 **R** 如果没有 **(a，a)** € **R** 适用于每个元素 **a € A** 。
> 例如:如果集合 A = {a，b}，那么 R = {(a，b)，(b，a)}就是不可逆关系。

**示例:**

> **输入:** N = 2
> **输出:** 4
> **解释:**
> 考虑集合{1，2}，总的可能不灵活关系为:
> 
> *   {}
> *   {(1, 2)}
> *   {(2, 1)}
> *   {(1, 2), (2, 1)}
> 
> **输入:**N = 5
> T3】输出: 1048576

**方法:**按照以下步骤解决问题:

*   集合**上的 A [**关系**](https://www.geeksforgeeks.org/relations-and-their-types/)**R**A**是集合的 [**笛卡尔乘积**的**子集，即 **A * A** 与 **N <sup>2</sup>** 元素。**](https://www.geeksforgeeks.org/cartesian-product-two-sets/)
*   **非弹性关系:**集合 **A** 上的关系 **R** 称为非弹性当且仅当**x**T8**R**T12】x[(x，x)不属于 R] 对于 **A** 中的每个元素 **x** 。
*   笛卡尔乘积中存在总共 **N 对 **(x，x)** 的**，它们不应该包含在非弹性关系中。因此，对于剩余的**(N<sup>2</sup>–N)**元素，每个元素都有两个选择，即在子集中包含或排除它。
*   因此，可能的**非弹性关系**的总数由**2<sup>(N2–N)</sup>**给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

const int mod = 1000000007;

// Function to calculate x^y
// modulo 1000000007 in O(log y)
int power(long long x, unsigned int y)
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

    // Return the resultant value of x^y
    return res;
}

// Function to count the number of
// irreflixive relations in a set
// consisting of N elements
int irreflexiveRelation(int N)
{

    // Return the resultant count
    return power(2, N * N - N);
}

// Driver Code
int main()
{
    int N = 2;
    cout << irreflexiveRelation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

static int mod = 1000000007;

// Function to calculate x^y
// modulo 1000000007 in O(log y)
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

    // Return the resultant value of x^y
    return res;
}

// Function to count the number of
// irreflixive relations in a set
// consisting of N elements
static int irreflexiveRelation(int N)
{

    // Return the resultant count
    return power(2, N * N - N);
}

// Driver Code
public static void main(String[] args)
{
    int N = 2;
    System.out.println(irreflexiveRelation(N));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach
mod = 1000000007

# Function to calculate x^y
# modulo 1000000007 in O(log y)
def power(x, y):
    global mod

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
            res = (res * x) % mod

        # Divide y by 2
        y = y >> 1

        # Update the value of x
        x = (x * x) % mod

    # Return the resultant value of x^y
    return res

# Function to count the number of
# irreflixive relations in a set
# consisting of N elements
def irreflexiveRelation(N):

    # Return the resultant count
    return power(2, N * N - N)

# Driver Code
if __name__ == '__main__':
    N = 2
    print(irreflexiveRelation(N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

  static int mod = 1000000007;

  // Function to calculate x^y
  // modulo 1000000007 in O(log y)
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

    // Return the resultant value of x^y
    return res;
  }

  // Function to count the number of
  // irreflixive relations in a set
  // consisting of N elements
  static int irreflexiveRelation(int N)
  {

    // Return the resultant count
    return power(2, N * N - N);
  }

  // Driver code
  public static void Main(String[] args)
  {
    int N = 2;
    Console.WriteLine(irreflexiveRelation(N));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let mod = 1000000007;

// Function to calculate x^y
// modulo 1000000007 in O(log y)
function power(x, y)
{

    // Stores the result of x^y
    let res = 1;

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

    // Return the resultant value of x^y
    return res;
}

// Function to count the number of
// irreflixive relations in a set
// consisting of N elements
function irreflexiveRelation(N)
{

    // Return the resultant count
    return power(2, N * N - N);
}

// Driver code

    let N = 2;
    document.write(irreflexiveRelation(N));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(log N)
T3】辅助空间: O(1)