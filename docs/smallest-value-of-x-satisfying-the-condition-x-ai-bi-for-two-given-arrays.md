# 满足两个给定数组条件 X % A[i] = B[i]的 X 的最小值

> 原文:[https://www . geesforgeks . org/x 的最小值-满足条件-x-ai-bi-for-two-给定-数组/](https://www.geeksforgeeks.org/smallest-value-of-x-satisfying-the-condition-x-ai-bi-for-two-given-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，两者都由 **N** 正整数组成，一个整数 **P** 和数组**A【】**的元素成对[共素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)，任务是找出最小的整数 **X** ，至少是**P**和 **X % A[i]**

**示例:**

> **输入:** A[] = {3，4，5}，B[] = {2，3，1}，P = 72
> **输出:** 131
> **说明:**
> 将 X 的值考虑如下运算为 131。
> 
> *   X % A[0] = 131 % 3 = 2 (= B[0])
> *   X % A[1] = 131 % 4 = 3 (= B[1])
> *   X % A[2] = 131 % 5 = 1 (= B[2])
> 
> 因此，131 是最小的整数，至少是 P( = 72)。
> 
> **输入:** A[] = {5，7}，B[] = {1，3}，P = 0
> T3】输出: 31

**方法:**解决给定问题的思路是使用[中国剩余定理](https://www.geeksforgeeks.org/chinese-remainder-theorem-set-1-introduction/)。按照以下步骤解决给定的问题:

*   计算数组 **A[]** 的 [LCM，等于数组 **A[]** 中存在的所有元素](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)的乘积[，说 **M** ，因为所有的](https://www.geeksforgeeks.org/program-for-product-of-array/)[元素都是同素的](https://www.geeksforgeeks.org/check-if-all-array-elements-are-pairwise-co-prime-or-not/)。
*   利用[中国剩余定理](https://www.geeksforgeeks.org/chinese-remainder-theorem-set-2-implementation/)，求所需的最小正整数 **Y** 。因此， **X** 的值由 **(Y + K * M)** 给出，对于某个整数 **K** ，在指标**【0，N–1】**的范围内，满足**X % A[I]= B[I]****I**。
*   **K** 的值可以从方程 **Y + K * M > = P** 中找到，相当于**K>=(P–Y)/M**。
*   因此，所需的最小可能整数 **X** 为 **(Y + K * M)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate modulo
// inverse of a w.r.t m using
// Extended Euclid Algorithm
int inv(int a, int m)
{
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;

    // Base Case
    if (m == 1)
        return 0;

    // Perform extended
    // euclid algorithm
    while (a > 1)
    {
        // q is quotient
        q = a / m;

        t = m;

        // m is remainder now,
        // process same as
        // euclid's algorithm
        m = a % m;
        a = t;

        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    // If x1 is negative
    if (x1 < 0)

        // Make x1 positive
        x1 += m0;

    return x1;
}

// Function to implement Chinese
// Remainder Theorem to find X
int findMinX(int A[], int B[], int N)
{

    // Stores the product
    // of array elements
    int prod = 1;

    // Traverse the array
    for(int i = 0; i < N; i++)

        // Update product
        prod *= A[i];

    // Initialize the result
    int result = 0;

    // Apply the above formula
    for(int i = 0; i < N; i++)
    {
        int pp = prod / A[i];
        result += B[i] * inv(pp, A[i]) * pp;
    }
    return result % prod;
}

// Function to calculate the product
// of all elements of the array a[]
int product(int a[], int n)
{

    // Stores product of
    // all array elements
    int ans = 1;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        ans *= a[i];
    }

    // Return the product
    return ans;
}

// Function to find the value of X
// that satisfies the given condition
void findSmallestInteger(int A[], int B[],
                         int P, int n)
{

    // Stores the required smallest value
    // using Chinese Remainder Theorem
    int Y = findMinX(A, B, n);

    // Stores the product
    // of all array elements
    int M = product(A,n);

    // The equation is Y + K*M >= P
    // Therefore, calculate K = ceil((P-Y)/M)
    int K = ceil(((double)P - (double)Y) /
                  (double)M);

    // So, X = Y + K*M
    int X = Y + K * M;

    // Print the resultant value of X
    cout << X;
}

// Driver Code
int main()
{
    int A[] = { 3, 4, 5 };
    int B[] = { 2, 3, 1 };
    int n = sizeof(A) / sizeof(A[0]);
    int P = 72;

    findSmallestInteger(A, B, P,n);
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.lang.*;
import java.util.*;
public class Main {

    // Function to calculate modulo
    // inverse of a w.r.t m using
    // Extended Euclid Algorithm
    static int inv(int a, int m)
    {
        int m0 = m, t, q;
        int x0 = 0, x1 = 1;

        // Base Case
        if (m == 1)
            return 0;

        // Perform extended
        // euclid algorithm
        while (a > 1) {

            // q is quotient
            q = a / m;

            t = m;

            // m is remainder now,
            // process same as
            // euclid's algorithm
            m = a % m;
            a = t;

            t = x0;

            x0 = x1 - q * x0;

            x1 = t;
        }

        // If x1 is negative
        if (x1 < 0)

            // Make x1 positive
            x1 += m0;

        return x1;
    }

    // Function to implement Chinese
    // Remainder Theorem to find X
    static int findMinX(int A[], int B[], int N)
    {
        // Stores the product
        // of array elements
        int prod = 1;

        // Traverse the array
        for (int i = 0; i < N; i++)

            // Update product
            prod *= A[i];

        // Initialize the result
        int result = 0;

        // Apply the above formula
        for (int i = 0; i < N; i++) {
            int pp = prod / A[i];
            result += B[i] * inv(pp, A[i]) * pp;
        }

        return result % prod;
    }

    // Function to calculate the product
    // of all elements of the array a[]
    static int product(int a[])
    {
        // Stores product of
        // all array elements
        int ans = 1;

        // Traverse the array
        for (int i = 0; i < a.length; i++) {
            ans *= a[i];
        }

        // Return the product
        return ans;
    }

    // Function to find the value of X
    // that satisfies the given condition
    public static void findSmallestInteger(int A[], int B[],
                                           int P)
    {
        // Stores the required smallest value
        // using Chinese Remainder Theorem
        int Y = findMinX(A, B, A.length);

        // Stores the product
        // of all array elements
        int M = product(A);

        // The equation is Y + K*M >= P
        // Therefore, calculate K = ceil((P-Y)/M)
        int K = (int)Math.ceil(((double)P - (double)Y)
                               / (double)M);

        // So, X = Y + K*M
        int X = Y + K * M;

        // Print the resultant value of X
        System.out.println(X);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 3, 4, 5 };
        int B[] = { 2, 3, 1 };

        int P = 72;

        findSmallestInteger(A, B, P);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to calculate modulo
# inverse of a w.r.t m using
# Extended Euclid Algorithm
def inv(a, m):

    m0 = m
    x0 = 0
    x1 = 1

    # Base Case
    if (m == 1):
        return 0

    # Perform extended
    # euclid algorithm
    while (a > 1):

        # q is quotient
        q = a // m

        t = m

        # m is remainder now,
        # process same as
        # euclid's algorithm
        m = a % m
        a = t

        t = x0
        x0 = x1 - q * x0
        x1 = t

    # If x1 is negative
    if (x1 < 0):

        # Make x1 positive
        x1 += m0

    return x1

# Function to implement Chinese
# Remainder Theorem to find X
def findMinX(A, B, N):

    # Stores the product
    # of array elements
    prod = 1

    # Traverse the array
    for i in range(N):

        # Update product
        prod *= A[i]

    # Initialize the result
    result = 0

    # Apply the above formula
    for i in range(N):
        pp = prod // A[i]
        result += B[i] * inv(pp, A[i]) * pp

    return result % prod

# Function to calculate the product
# of all elements of the array a[]
def product(a, n):

    # Stores product of
    # all array elements
    ans = 1

    # Traverse the array
    for i in range(n):
        ans *= a[i]

    # Return the product
    return ans

# Function to find the value of X
# that satisfies the given condition
def findSmallestInteger(A, B, P, n):

    # Stores the required smallest value
    # using Chinese Remainder Theorem
    Y = findMinX(A, B, n)

    # Stores the product
    # of all array elements
    M = product(A, n)

    # The equation is Y + K*M >= P
    # Therefore, calculate K = ceil((P-Y)/M)
    K = math.ceil((P - Y) / M)

    # So, X = Y + K*M
    X = Y + K * M

    # Print the resultant value of X
    print(X)

# Driver Code
if __name__ == "__main__" :

    A = [ 3, 4, 5 ]
    B = [ 2, 3, 1 ]
    n = len(A)
    P = 72

    findSmallestInteger(A, B, P, n)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to calculate modulo
  // inverse of a w.r.t m using
  // Extended Euclid Algorithm
  static int inv(int a, int m)
  {
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;

    // Base Case
    if (m == 1)
      return 0;

    // Perform extended
    // euclid algorithm
    while (a > 1) {

      // q is quotient
      q = a / m;

      t = m;

      // m is remainder now,
      // process same as
      // euclid's algorithm
      m = a % m;
      a = t;

      t = x0;

      x0 = x1 - q * x0;

      x1 = t;
    }

    // If x1 is negative
    if (x1 < 0)

      // Make x1 positive
      x1 += m0;

    return x1;
  }

  // Function to implement Chinese
  // Remainder Theorem to find X
  static int findMinX(int[] A, int[] B, int N)
  {
    // Stores the product
    // of array elements
    int prod = 1;

    // Traverse the array
    for (int i = 0; i < N; i++)

      // Update product
      prod *= A[i];

    // Initialize the result
    int result = 0;

    // Apply the above formula
    for (int i = 0; i < N; i++) {
      int pp = prod / A[i];
      result += B[i] * inv(pp, A[i]) * pp;
    }

    return result % prod;
  }

  // Function to calculate the product
  // of all elements of the array a[]
  static int product(int[] a)
  {
    // Stores product of
    // all array elements
    int ans = 1;

    // Traverse the array
    for (int i = 0; i < a.Length; i++) {
      ans *= a[i];
    }

    // Return the product
    return ans;
  }

  // Function to find the value of X
  // that satisfies the given condition
  public static void findSmallestInteger(int[] A, int[] B,
                                         int P)
  {
    // Stores the required smallest value
    // using Chinese Remainder Theorem
    int Y = findMinX(A, B, A.Length);

    // Stores the product
    // of all array elements
    int M = product(A);

    // The equation is Y + K*M >= P
    // Therefore, calculate K = ceil((P-Y)/M)
    int K = (int)Math.Ceiling(((double)P - (double)Y)
                              / (double)M);

    // So, X = Y + K*M
    int X = Y + K * M;

    // Print the resultant value of X
    Console.WriteLine(X);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] A = { 3, 4, 5 };
    int[] B = { 2, 3, 1 };

    int P = 72;

    findSmallestInteger(A, B, P);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate modulo
// inverse of a w.r.t m using
// Extended Euclid Algorithm
function inv(a, m)
{
    var m0 = m, t, q;
    var x0 = 0, x1 = 1;

    // Base Case
    if (m == 1)
        return 0;

    // Perform extended
    // euclid algorithm
    while (a > 1)
    {
        // q is quotient
        q = parseInt(a / m);

        t = m;

        // m is remainder now,
        // process same as
        // euclid's algorithm
        m = a % m;
        a = t;

        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    // If x1 is negative
    if (x1 < 0)

        // Make x1 positive
        x1 += m0;

    return x1;
}

// Function to implement Chinese
// Remainder Theorem to find X
function findMinX(A, B, N)
{

    // Stores the product
    // of array elements
    var prod = 1;

    // Traverse the array
    for(var i = 0; i < N; i++)

        // Update product
        prod *= A[i];

    // Initialize the result
    var result = 0;

    // Apply the above formula
    for(var i = 0; i < N; i++)
    {
        var pp = parseInt(prod / A[i]);
        result += B[i] * inv(pp, A[i]) * pp;
    }
    return result % prod;
}

// Function to calculate the product
// of all elements of the array a[]
function product(a, n)
{

    // Stores product of
    // all array elements
    var ans = 1;

    // Traverse the array
    for(var i = 0; i < n; i++)
    {
        ans *= a[i];
    }

    // Return the product
    return ans;
}

// Function to find the value of X
// that satisfies the given condition
function findSmallestInteger(A, B, P, n)
{

    // Stores the required smallest value
    // using Chinese Remainder Theorem
    var Y = findMinX(A, B, n);

    // Stores the product
    // of all array elements
    var M = product(A,n);

    // The equation is Y + K*M >= P
    // Therefore, calculate K = ceil((P-Y)/M)
    var K = Math.ceil((P - Y) / M);

    // So, X = Y + K*M
    var X = Y + K * M;

    // Print the resultant value of X
    document.write( X);
}

// Driver Code
var A = [ 3, 4, 5 ];
var B = [ 2, 3, 1 ];
var n = A.length;
var P = 72;
findSmallestInteger(A, B, P,n);

</script>
```

**Output:** 

```
131
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*