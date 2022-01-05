# N 以内所有与 N 同素的数的乘积

> 原文:[https://www . geesforgeks . org/所有数字的乘积-最多 n 个与-n 同素/](https://www.geeksforgeeks.org/product-of-all-numbers-up-to-n-that-are-co-prime-with-n/)

给定一个整数 **N** ，任务是找到从范围**【1，N】**[共质数](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)到给定数 **N** 的所有数的[乘积。](https://www.geeksforgeeks.org/program-for-product-of-array/)

**示例:**

> **输入:** N = 5
> **输出:** 24
> **说明:**
> 与 5 同素的数字为{1，2，3，4}。
> 因此，乘积由 1 * 2 * 3 * 4 = 24 给出。
> 
> **输入:** N = 6
> **输出:** 5
> **说明:**
> 与 6 同素的数字为{1，5}。
> 因此，要求的乘积等于 1 * 5 = 5

**方法:**思路是在**【1，N】**范围内迭代，对于每个数字，检查其带有 **N** 的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 是否等于 **1** 。如果发现任何一个数字都是真的，那么就把这个数字包含在结果中。
按照以下步骤解决问题:

1.  将**产品**初始化为 **1** 。
2.  迭代范围**【1，N】**，如果 **i** 和 **N** 的 **GCD** 为 **1** ，则将**乘积**乘以 **i** 。
3.  完成上述步骤后，打印**产品**的数值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    // Base Case
    if (a == 0)
        return b;

    // Recursive GCD
    return gcd(b % a, a);
}

// Function to find the product of
// all the numbers till N that are
// relatively prime to N
int findProduct(unsigned int N)
{
    // Stores the resultant product
    unsigned int result = 1;

    // Iterate over [2, N]
    for (int i = 2; i < N; i++) {

        // If gcd is 1, then find the
        // product with result
        if (gcd(i, N) == 1) {
            result *= i;
        }

    }
   // Return the final product
        return result;
}

// Driver Code
int main()
{
    int N = 5;

    cout << findProduct(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to return
// gcd of a and b
static int gcd(int a, int b)
{
  // Base Case
  if (a == 0)
    return b;

  // Recursive GCD
  return gcd(b % a, a);
}

// Function to find the
// product of all the
// numbers till N that are
// relatively prime to N
static int findProduct(int N)
{
  // Stores the resultant
  // product
  int result = 1;

  // Iterate over [2, N]
  for (int i = 2; i < N; i++)
  {
    // If gcd is 1, then
    // find the product
    // with result
    if (gcd(i, N) == 1)
    {
      result *= i;
    }
  }

  // Return the final
  // product
  return result;
}

// Driver Code
public static void main(String[] args)
{
  int N = 5;
  System.out.print(findProduct(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to return
# gcd of a and b
def gcd(a, b):

    # Base Case
    if (a == 0):
        return b;

    # Recursive GCD
    return gcd(b % a, a);

# Function to find the
# product of all the
# numbers till N that are
# relatively prime to N
def findProduct(N):

    # Stores the resultant
    # product
    result = 1;

    # Iterate over [2, N]
    for i in range(2, N):

        # If gcd is 1, then
        # find the product
        # with result
        if (gcd(i, N) == 1):
            result *= i;

    # Return the final
    # product
    return result;

# Driver Code
if __name__ == '__main__':

    N = 5;
    print(findProduct(N));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to return
// gcd of a and b
static int gcd(int a, int b)
{

  // Base Case
  if (a == 0)
    return b;

  // Recursive GCD
  return gcd(b % a, a);
}

// Function to find the
// product of all the
// numbers till N that are
// relatively prime to N
static int findProduct(int N)
{

  // Stores the resultant
  // product
  int result = 1;

  // Iterate over [2, N]
  for(int i = 2; i < N; i++)
  {

    // If gcd is 1, then
    // find the product
    // with result
    if (gcd(i, N) == 1)
    {
      result *= i;
    }
  }

  // Return the readonly
  // product
  return result;
}

// Driver Code
public static void Main(String[] args)
{
  int N = 5;

  Console.Write(findProduct(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return gcd of a and b
function gcd(a, b)
{
    // Base Case
    if (a == 0)
        return b;

    // Recursive GCD
    return gcd(b % a, a);
}

// Function to find the product of
// all the numbers till N that are
// relatively prime to N
function findProduct( N)
{
    // Stores the resultant product
    var result = 1;

    // Iterate over [2, N]
    for (var i = 2; i < N; i++) {

        // If gcd is 1, then find the
        // product with result
        if (gcd(i, N) == 1) {
            result *= i;
        }

    }
   // Return the final product
        return result;
}

// Driver Code
var N = 5;
document.write(findProduct(N))

</script>
```

**Output**

```
24
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(1)*