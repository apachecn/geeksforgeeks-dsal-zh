# 检查所有数组元素是否成对同素

> 原文:[https://www . geesforgeks . org/check-if-all-array-elements-is-pair-co-prime-or-not/](https://www.geeksforgeeks.org/check-if-all-array-elements-are-pairwise-co-prime-or-not/)

给定一个由 **N** 正整数组成的数组**A【】**，任务是检查所有数组元素是否成对[共素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)，即所有对(A <sub>i</sub> ，A <sub>j</sub> ，这样 1 < =i < j < =N， **GCD(A <sub>i</sub> ，A <sub>j</sub> ) = 1**

**示例:**

> **输入:** A[] = {2，3，5}
> **输出:**是
> **说明:**所有的对，(2，3)，(3，5)，(2，5)都是成对的同素。
> 
> **输入:** A[] = {5，10}
> **输出:**否
> **说明:** GCD(5，10)=5 所以它们不是同素的。

**天真方法:**解决这个问题最简单的方法是从给定的数组中生成所有可能的对，对于每个对，检查它是否是互质。如果发现任何一对非互质，打印“**否**”。否则，打印“**是**”。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 如果任何两个数字都有一个[公共质因数](https://www.geeksforgeeks.org/common-prime-factors-of-two-numbers/)，那么它们的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 永远不可能是 1。

这也可以解释为:

> 数组的 [LCM 必须等于数组中元素的乘积。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)

因此，解决方案归结为计算给定数组的 LCM，并检查它是否等于所有数组元素的乘积。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to calculate GCD
ll GCD(ll a, ll b)
{
    if (a == 0)
        return b;
    return GCD(b % a, a);
}

// Function to calculate LCM
ll LCM(ll a, ll b)
{
    return (a * b)
        / GCD(a, b);
}

// Function to check if all elements
// in the array are pairwise coprime
void checkPairwiseCoPrime(int A[], int n)
{
    // Initialize variables
    ll prod = 1;
    ll lcm = 1;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        // Calculate product of
        // array elements
        prod *= A[i];

        // Calculate LCM of
        // array elements
        lcm = LCM(A[i], lcm);
    }

    // If the product of array elements
    // is equal to LCM of the array
    if (prod == lcm)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
// Driver Code
int main()
{
    int A[] = { 2, 3, 5 };
    int n = sizeof(A) / sizeof(A[0]);

    // Function call
    checkPairwiseCoPrime(A, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to calculate GCD
static long GCD(long a, long b)
{
    if (a == 0)
        return b;

    return GCD(b % a, a);
}

// Function to calculate LCM
static long LCM(long a, long b)
{
    return (a * b) / GCD(a, b);
}

// Function to check if all elements
// in the array are pairwise coprime
static void checkPairwiseCoPrime(int A[], int n)
{

    // Initialize variables
    long prod = 1;
    long lcm = 1;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {

        // Calculate product of
        // array elements
        prod *= A[i];

        // Calculate LCM of
        // array elements
        lcm = LCM(A[i], lcm);
    }

    // If the product of array elements
    // is equal to LCM of the array
    if (prod == lcm)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 2, 3, 5 };
    int n = A.length;

    // Function call
    checkPairwiseCoPrime(A, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate GCD
def GCD(a, b):

    if (a == 0):
        return b

    return GCD(b % a, a)

# Function to calculate LCM
def LCM(a, b):

    return (a * b) // GCD(a, b)

# Function to check if aelements
# in the array are pairwise coprime
def checkPairwiseCoPrime(A, n):

    # Initialize variables
    prod = 1
    lcm = 1

    # Iterate over the array
    for i in range(n):

        # Calculate product of
        # array elements
        prod *= A[i]

        # Calculate LCM of
        # array elements
        lcm = LCM(A[i], lcm)

    # If the product of array elements
    # is equal to LCM of the array
    if (prod == lcm):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    A = [ 2, 3, 5 ]
    n = len(A)

    # Function call
    checkPairwiseCoPrime(A, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to calculate GCD
static long GCD(long a,
                long b)
{
  if (a == 0)
    return b;
  return GCD(b % a, a);
}

// Function to calculate LCM
static long LCM(long a,
                long b)
{
  return (a * b) / GCD(a, b);
}

// Function to check if all elements
// in the array are pairwise coprime
static void checkPairwiseCoPrime(int []A,
                                 int n)
{    
  // Initialize variables
  long prod = 1;
  long lcm = 1;

  // Iterate over the array
  for(int i = 0; i < n; i++)
  {
    // Calculate product of
    // array elements
    prod *= A[i];

    // Calculate LCM of
    // array elements
    lcm = LCM(A[i], lcm);
  }

  // If the product of array elements
  // is equal to LCM of the array
  if (prod == lcm)
    Console.WriteLine("Yes");
  else
    Console.WriteLine("No");
}

// Driver Code
public static void Main(String[] args)
{
  int []A = {2, 3, 5};
  int n = A.Length;

  // Function call
  checkPairwiseCoPrime(A, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to calculate GCD
    function GCD(a , b) {
        if (a == 0)
            return b;

        return GCD(b % a, a);
    }

    // Function to calculate LCM
    function LCM(a , b) {
        return (a * b) / GCD(a, b);
    }

    // Function to check if all elements
    // in the array are pairwise coprime
    function checkPairwiseCoPrime(A , n) {

        // Initialize variables
        var prod = 1;
        var lcm = 1;

        // Iterate over the array
        for (i = 0; i < n; i++) {

            // Calculate product of
            // array elements
            prod *= A[i];

            // Calculate LCM of
            // array elements
            lcm = LCM(A[i], lcm);
        }

        // If the product of array elements
        // is equal to LCM of the array
        if (prod == lcm)
            document.write("Yes");
        else
            document.write("No");
    }

    // Driver Code

        var A = [ 2, 3, 5 ];
        var n = A.length;

        // Function call
        checkPairwiseCoPrime(A, n);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N log(min(A[I])】*
***辅助空间:** O(1)*