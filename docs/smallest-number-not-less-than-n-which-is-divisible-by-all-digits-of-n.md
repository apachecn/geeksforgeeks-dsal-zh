# 不小于 N 的最小数，可被 N 的所有数字整除

> 原文:[https://www . geeksforgeeks . org/最小数字不小于 n，可被 n 的所有数字整除/](https://www.geeksforgeeks.org/smallest-number-not-less-than-n-which-is-divisible-by-all-digits-of-n/)

给定一个正整数 **N** ，任务是找到大于或等于 **X** 的最小整数，使其所有数字都可以被 **N** 的非零数字整除。

**示例:**

> **输入:** N = 280
> **输出:** 280
> **说明:**
> 280 是最小的，可以被数字 8 和 2 整除。
> 
> **输入:** N = 32
> **输出:** 36
> **说明:**
> 36 是能被数字 2 和 3 整除的最小数。

**方法:**思路是找到 **X** 所有非零数字的 [LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) ，然后只找到该 LCM 值的下一个大于 **N** 的倍数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to calculate the LCM
int LCM(int A, int B)
{
    return (A * B / __gcd(A, B));
}

// Function to find the smallest number
// satisfying given constraints
int findSmallestNumber(int X)
{
    // LCM value is 1 initially
    int lcm = 1;
    int temp = X;

    // Finding the LCM of all
    // non zero digits
    while (temp) {

        int last = temp % 10;
        temp /= 10;

        if (!last)
            continue;

        // Update the value lcm
        lcm = LCM(lcm, last);
    }

    // Stores ceil value
    int answer = ((X + lcm - 1) / lcm)
                 * lcm;

    // Print the answer
    cout << answer;
}

// Driver Code
int main()
{
    int X = 280;

    // Function Call
    findSmallestNumber(X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

  // Function to calculate the LCM
  static int LCM(int A, int B)
  {
    return (A * B / __gcd(A, B));
  }

  // Function to find the smallest number
  // satisfying given constraints
  static void findSmallestNumber(int X)
  {

    // LCM value is 1 initially
    int lcm = 1;
    int temp = X;

    // Finding the LCM of all
    // non zero digits
    while (temp > 0)
    {
      int last = temp % 10;
      temp /= 10;

      if (last == 0)
        continue;

      // Update the value lcm
      lcm = LCM(lcm, last);
    }

    // Stores ceil value
    int answer = ((X + lcm - 1) / lcm)
      * lcm;

    // Print the answer
    System.out.print(answer);

  }
  static int __gcd(int a, int b) 
  { 
    return b == 0 ? a:__gcd(b, a % b);    
  }

  // Driver Code
  public static void main(String[] args)
  {
    int X = 280;

    // Function Call
    findSmallestNumber(X);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to calculate the LCM
def LCM(A, B):

    return (A * B // math.gcd(A, B))

# Function to find the smallest number
# satisfying given constraints
def findSmallestNumber(X):

    # LCM value is 1 initially
    lcm = 1
    temp = X

    # Finding the LCM of all
    # non zero digits
    while (temp):
        last = temp % 10
        temp //= 10

        if (not last):
            continue

        # Update the value lcm
        lcm = LCM(lcm, last)

    # Stores ceil value
    answer = ((X + lcm - 1) // lcm) * lcm

    # Print the answer
    print(answer)

# Driver Code
if __name__ == "__main__":

    X = 280

    # Function Call
    findSmallestNumber(X)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  // Function to calculate the LCM
  static int LCM(int A, int B)
  {
    return (A * B / __gcd(A, B));
  }

  // Function to find the smallest number
  // satisfying given constraints
  static void findSmallestNumber(int X)
  {

    // LCM value is 1 initially
    int lcm = 1;
    int temp = X;

    // Finding the LCM of all
    // non zero digits
    while (temp > 0)
    {
      int last = temp % 10;
      temp /= 10;

      if (last == 0)
        continue;

      // Update the value lcm
      lcm = LCM(lcm, last);
    }

    // Stores ceil value
    int answer = ((X + lcm - 1) / lcm)
      * lcm;

    // Print the answer
    Console.Write(answer);

  }
  static int __gcd(int a, int b) 
  { 
    return b == 0 ? a:__gcd(b, a % b);    
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int X = 280;

    // Function Call
    findSmallestNumber(X);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the LCM
function LCM(A,B)
{
    return (A * B / __gcd(A, B));
}

// Function to find the smallest number
  // satisfying given constraints
function findSmallestNumber(X)
{
    // LCM value is 1 initially
    let lcm = 1;
    let temp = X;

    // Finding the LCM of all
    // non zero digits
    while (temp > 0)
    {
      let last = temp % 10;
      temp = Math.floor(temp/10);

      if (last == 0)
        continue;

      // Update the value lcm
      lcm = LCM(lcm, last);
    }

    // Stores ceil value
    let answer = Math.floor((X + lcm - 1) / lcm)
      * lcm;

    // Print the answer
    document.write(answer);
}

function __gcd(a,b)
{
    return b == 0 ? a:__gcd(b, a % b);
}

 // Driver Code
let X = 280;

// Function Call
findSmallestNumber(X);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
280
```

***时间复杂度:**O(N * log<sub>10</sub>N)*
***辅助空间:** O(1)*