# 给定范围内所有偶数的异或运算

> 原文:[https://www . geeksforgeeks . org/给定范围内所有偶数的异或/](https://www.geeksforgeeks.org/xor-of-all-even-numbers-from-a-given-range/)

给定两个整数 **L** 和 **R** ，任务是计算**【L，R】**范围内所有[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **例:**
> **输入:** L = 10，R = 20
> **输出:** 30
> **解释:**
> 按位异或= 10 ^ 12 ^ 14 ^ 16 ^ 18 ^ 20 = 30
> 因此，所需输出为 30。
> 
> **示例:**
> **输入:** L = 15，R = 23
> **输出:** 0
> **解释:**
> 按位异或= 16 ^ 18 ^ 20 ^ 22 = 0
> 因此，所需输出为 0。

**天真法:**解决问题最简单的方法是遍历**【L，R】**范围内的所有偶数，打印所有偶数的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

***时间复杂度:**O(R–L)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 如果 **N** 是偶数:
> 2 ^ 4 … ^ (N) = 2 * (1 ^ 2 ^ … ^ (N / 2))
> 
> 如果 **N** 是奇数:
> 2 ^ 4…^(n)= 2 *(1 ^ 2 ^…^((n–1)/2))

按照以下步骤解决问题:

*   [从范围[1，(R) / 2]](https://www.geeksforgeeks.org/calculate-xor-1-n/) 中找到所有数字的按位异或，并将其存储在一个变量中，比如 **xor_r** 。
*   [从范围【1，(L–1)/2】](https://www.geeksforgeeks.org/calculate-xor-1-n/)中找到所有数字的按位异或，并将其存储在一个变量中，比如 **xor_l.**
*   最后，打印 **xor_r ^ xor_l** 的值。

下面是上述方法的实现:

## C++

```
// C++ Implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate XOR of
// numbers in the range [1, n]
int bitwiseXorRange(int n)
{

    // If n is divisible by 4
    if (n % 4 == 0)
        return n;

    // If n mod 4 is equal to 1
    if (n % 4 == 1)
        return 1;

    // If n mod 4 is equal to 2
    if (n % 4 == 2)
        return n + 1;

    return 0;
}

// Function to find XOR of even
// numbers in the range [l, r]
int evenXorRange(int l, int r)
{

    // Stores XOR of even numbers
    // in the range [1, l - 1]
    int xor_l;

    // Stores XOR of even numbers
    // in the range [1, r]
    int xor_r;

    // Update xor_r
    xor_r
        = 2 * bitwiseXorRange(r / 2);

    // Update xor_l
    xor_l
        = 2 * bitwiseXorRange((l - 1) / 2);

    return xor_l ^ xor_r;
}

// Driver Code
int main()
{
    int l = 10;
    int r = 20;
    cout << evenXorRange(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the above approach
class GFG
{

  // Function to calculate XOR of
  // numbers in the range [1, n]
  static int bitwiseXorRange(int n)
  {

    // If n is divisible by 4
    if (n % 4 == 0)
      return n;

    // If n mod 4 is equal to 1
    if (n % 4 == 1)
      return 1;

    // If n mod 4 is equal to 2
    if (n % 4 == 2)
      return n + 1;

    return 0;
  }

  // Function to find XOR of even
  // numbers in the range [l, r]
  static int evenXorRange(int l, int r)
  {

    // Stores XOR of even numbers
    // in the range [1, l - 1]
    int xor_l;

    // Stores XOR of even numbers
    // in the range [1, r]
    int xor_r;

    // Update xor_r
    xor_r
      = 2 * bitwiseXorRange(r / 2);

    // Update xor_l
    xor_l
      = 2 * bitwiseXorRange((l - 1) / 2);

    return xor_l ^ xor_r;
  }

  // Driver Code
  public static void main (String[] args)
  {
    int l = 10;
    int r = 20;
    System.out.print(evenXorRange(l, r));   
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to calculate XOR of
# numbers in the range [1, n]
def bitwiseXorRange(n):

    # If n is divisible by 4
    if (n % 4 == 0):
        return n

    # If n mod 4 is equal to 1
    if (n % 4 == 1):
        return 1

    # If n mod 4 is equal to 2
    if (n % 4 == 2):
        return n + 1

    return 0

# Function to find XOR of even
# numbers in the range [l, r]
def evenXorRange(l, r):

    # Stores XOR of even numbers
    # in the range [1, l - 1]
    #xor_l

    # Stores XOR of even numbers
    # in the range [1, r]
    #xor_r

    # Update xor_r
    xor_r = 2 * bitwiseXorRange(r // 2)

    # Update xor_l
    xor_l = 2 * bitwiseXorRange((l - 1) // 2)

    return xor_l ^ xor_r

# Driver Code
if __name__ == '__main__':

    l = 10
    r = 20

    print(evenXorRange(l, r))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Implementation of the above approach
using System;
class GFG {

  // Function to calculate XOR of
  // numbers in the range [1, n]
  static int bitwiseXorRange(int n)
  {

    // If n is divisible by 4
    if (n % 4 == 0)
      return n;

    // If n mod 4 is equal to 1
    if (n % 4 == 1)
      return 1;

    // If n mod 4 is equal to 2
    if (n % 4 == 2)
      return n + 1;

    return 0;
  }

  // Function to find XOR of even
  // numbers in the range [l, r]
  static int evenXorRange(int l, int r)
  {

    // Stores XOR of even numbers
    // in the range [1, l - 1]
    int xor_l;

    // Stores XOR of even numbers
    // in the range [1, r]
    int xor_r;

    // Update xor_r
    xor_r
      = 2 * bitwiseXorRange(r / 2);

    // Update xor_l
    xor_l
      = 2 * bitwiseXorRange((l - 1) / 2);

    return xor_l ^ xor_r;
  }

  // Driver code
  static void Main()
  {
    int l = 10;
    int r = 20;
    Console.Write(evenXorRange(l, r));   
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// JavaScript Implementation of the above approach

// Function to calculate XOR of
// numbers in the range [1, n]
function bitwiseXorRange(n)
{

    // If n is divisible by 4
    if (n % 4 == 0)
        return n;

    // If n mod 4 is equal to 1
    if (n % 4 == 1)
        return 1;

    // If n mod 4 is equal to 2
    if (n % 4 == 2)
        return n + 1;
    return 0;
}

// Function to find XOR of even
// numbers in the range [l, r]
function evenXorRange(l, r)
{

    // Stores XOR of even numbers
    // in the range [1, l - 1]
    let xor_l;

    // Stores XOR of even numbers
    // in the range [1, r]
    let xor_r;

    // Update xor_r
    xor_r
        = 2 * bitwiseXorRange(Math.floor(r / 2));

    // Update xor_l
    xor_l
        = 2 * bitwiseXorRange(Math.floor((l - 1) / 2));

    return xor_l ^ xor_r;
}

// Driver Code

    let l = 10;
    let r = 20;
    document.write(evenXorRange(l, r));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
30
```

***时间复杂度:** O(1)。*
***辅助空间:** O(1)*