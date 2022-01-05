# 检查矩阵和是否为素数

> 原文:[https://www . geesforgeks . org/check-if-matrix-sum-is-prime-or-not/](https://www.geeksforgeeks.org/check-if-matrix-sum-is-prime-or-not/)

给定一个矩阵 **mat[][]** ，任务是检查矩阵元素的和是否为素数。
**例:**

> **输入:** mat[][] = {{1，2}，{2，1}}
> **输出:** NO
> **说明:**
> 矩阵之和= 1 + 2 + 2 + 1 = 6
> 因为 6 不是素数。因此，输出为 NO
> **输入:** mat[][] = {{1，2}，{2，2}}
> **输出:** YES
> **说明:**
> 矩阵之和= 1 + 2 + 2 + 2 = 7
> 因为 7 是素数。因此，输出为是

**方法:**思路是利用两个嵌套循环求矩阵的和，然后最后检查矩阵的和是否为素数。如果是，则输出为是，否则输出为否
以下是上述方法的实现:

## C++

```
// C++ implementation to check
// if the sum of matrix
// is prime or not

#include <bits/stdc++.h>
using namespace std;

const int N = 4, M = 5;

// Function to check
// whether a number
// is prime or not
bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for (int i = 2; i <= sqrt(n); i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function for to find the sum
// of the given matrix
int takeSum(int a[N][M])
{
    int s = 0;
    for (int i = 0; i < N; i++)
        for (int j = 0; j < M; j++)
            s += a[i][j];

    return s;
}

// Driver Code
int main()
{

    int a[N][M] = { { 1, 2, 3, 4, 2 },
                    { 0, 1, 2, 3, 34 },
                    { 0, 34, 21, 12, 12 },
                    { 1, 2, 3, 6, 6 } };
    int sum = takeSum(a);

    if (isPrime(sum))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// the sum of matrix is prime or not
class GFG{

static int N = 4, M = 5;

// Function to check whether
// a number is prime or not
static boolean isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for(int i = 2; i <= Math.sqrt(n); i++)
       if (n % i == 0)
           return false;

    return true;
}

// Function for to find the sum
// of the given matrix
static int takeSum(int a[][])
{
    int s = 0;

    for(int i = 0; i < N; i++)
       for(int j = 0; j < M; j++)
          s += a[i][j];

    return s;
}

// Driver Code
public static void main(String[] args)
{
    int a[][] = { { 1, 2, 3, 4, 2 },
                  { 0, 1, 2, 3, 34 },
                  { 0, 34, 21, 12, 12 },
                  { 1, 2, 3, 6, 6 } };

    int sum = takeSum(a);

    if (isPrime(sum))
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to check if
# the sum of matrix is prime or not
import math

# Function to check whether a number
# is prime or not
def isPrime(n):

    # Corner case
    if (n <= 1):
        return False;

    # Check from 2 to n-1
    for i in range(2, (int)(math.sqrt(n)) + 1):
        if (n % i == 0):
            return False;

    return True;

# Function for to find the sum
# of the given matrix
def takeSum(a):

    s = 0
    for i in range(0, 4):
        for j in range(0, 5):
            s += a[i][j]

    return s;

# Driver Code
a = [ [ 1, 2, 3, 4, 2 ],
      [ 0, 1, 2, 3, 34 ],
      [ 0, 34, 21, 12, 12 ],
      [ 1, 2, 3, 6, 6 ] ];
sum = takeSum(a);

if (isPrime(sum)):
    print("YES")
else:
    print("NO")

# This code is contributed by grand_master
```

## C#

```
// C# implementation to check if
// the sum of matrix is prime or not
using System;
class GFG{

static int N = 4, M = 5;

// Function to check whether
// a number is prime or not
static Boolean isPrime(int n)
{

    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for(int i = 2; i <= Math.Sqrt(n); i++)
    if (n % i == 0)
        return false;

    return true;
}

// Function for to find the sum
// of the given matrix
static int takeSum(int [][]a)
{
    int s = 0;

    for(int i = 0; i < N; i++)
    for(int j = 0; j < M; j++)
        s += a[i][j];

    return s;
}

// Driver Code
public static void Main(String[] args)
{
    int [][]a = new int[][]
                {
                    new int[] { 1, 2, 3, 4, 2 },
                    new int[] { 0, 1, 2, 3, 34 },
                    new int[] { 0, 34, 21, 12, 12 },
                    new int[] { 1, 2, 3, 6, 6 }
                };

    int sum = takeSum(a);

    if (isPrime(sum))
        Console.Write("YES" + "\n");
    else
        Console.Write("NO" + "\n");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Javascript implementation to check
    // if the sum of matrix
    // is prime or not

    let N = 4, M = 5;

    // Function to check
    // whether a number
    // is prime or not
    function isPrime(n)
    {
        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to n-1
        for (let i = 2; i <= Math.sqrt(n); i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function for to find the sum
    // of the given matrix
    function takeSum(a)
    {
        let s = 0;
        for (let i = 0; i < N; i++)
            for (let j = 0; j < M; j++)
                s += a[i][j];

        return s;
    }

    let a = [ [ 1, 2, 3, 4, 2 ],
             [ 0, 1, 2, 3, 34 ],
             [ 0, 34, 21, 12, 12 ],
             [ 1, 2, 3, 6, 6 ] ];
    let sum = takeSum(a);

    if (isPrime(sum))
        document.write("YES");
    else
        document.write("NO");

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(N*M)*