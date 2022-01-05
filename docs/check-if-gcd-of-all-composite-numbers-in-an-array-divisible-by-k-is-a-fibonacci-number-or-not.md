# 检查被 K 整除的数组中所有复合数的 GCD 是否为斐波那契数

> 原文:[https://www . geesforgeks . org/check-if-gcd-of-all-composite-numbers-in-a-Fibonacci-or-not/](https://www.geeksforgeeks.org/check-if-gcd-of-all-composite-numbers-in-an-array-divisible-by-k-is-a-fibonacci-number-or-not/)

给定由 **N** 个非负整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是检查数组中所有可被 **K** 整除的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 是否为[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。如果发现是真的，打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = *{13* ，55，1331，7，13，11，44，77，144，89}，K = 11
> **输出:**否
> **说明:**数组中可被 11 整除的复合数为{55，1331，11，44，77}。这些元素的 GCD 等于 11，不是斐波那契数。
> 
> **输入:** arr[] = {34，2，4，8，5，7，11}，K = 2
> **输出:**是
> **说明:**数组中可被 2 整除的复合数为{34，2，4，8}。这些元素的 GCD 等于 2，不是斐波那契数。

**方法:**按照以下步骤解决问题:

1.  创建一个函数 **isComposite()** 到[检查一个数字是否是复合数字](https://www.geeksforgeeks.org/composite-number/)。
2.  创建另一个函数**是斐波那契()**来[检查一个数字是否是斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。
3.  初始化一个整数[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**组合**，和另一个整数变量 **gcd** 来存储数组中可被 **K** 整除的**组合数**的 gcd。
4.  [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。
5.  对于每一个元素**arr【I】**，检查它是否是复合的，是否能被 **K** 整除。如果发现是真的，[将其插入向量](https://www.geeksforgeeks.org/vector-insert-function-in-c-stl/) **组合**
6.  [计算矢量中所有元素的 GCD**组合**](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 并存储在变量 **gcd** 中。
7.  [检查 **gcd** 是否为斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
8.  如果发现为真，则打印**“是”**。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is composite or not
bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return false;

    // Check if the number is
    // divisible by 2 or 3 or not
    if (n % 2 == 0 || n % 3 == 0)

        return true;

    // Check if n is a multiple of
    // any other prime number
    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)

            return true;

    return false;
}

// Function to check if a number
// is a Perfect Square or not
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Function to check if a number
// is a Fibonacci number or not
bool isFibonacci(int n)
{
    // If 5*n^2 + 4 or 5*n^2 - 4 or
    // both are perfect square
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to check if GCD of composite
// numbers from the array a[] which are
// divisible by k is a Fibonacci number or not
void ifgcdFibonacci(int a[], int n, int k)
{
    vector<int> compositeset;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If array element is composite
        // and divisible by k
        if (isComposite(a[i]) && a[i] % k == 0) {
            compositeset.push_back(a[i]);
        }
    }
    int gcd = compositeset[0];

    // Calculate GCD of all elements in compositeset
    for (int i = 1; i < compositeset.size(); i++) {
        gcd = __gcd(gcd, compositeset[i]);
        if (gcd == 1) {
            break;
        }
    }

    // If GCD is Fibonacci
    if (isFibonacci(gcd)) {
        cout << "Yes";
        return;
    }
    cout << "No";
    return;
}

// Driver Code
int main()
{

    int arr[] = { 34, 2, 4, 8, 5, 7, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    ifgcdFibonacci(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GFG{

// Function to check if a
// number is composite or not
static boolean isComposite(int n)
{

    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return false;

    // Check if the number is
    // divisible by 2 or 3 or not
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check if n is a multiple of
    // any other prime number
    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to check if a number
// is a Perfect Square or not
static boolean isPerfectSquare(int x)
{
    int s = (int)Math.sqrt(x);
    return (s * s == x);
}

// Function to check if a number
// is a Fibonacci number or not
static boolean isFibonacci(int n)
{

    // If 5*n^2 + 4 or 5*n^2 - 4 or
    // both are perfect square
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to check if GCD of composite
// numbers from the array a[] which are
// divisible by k is a Fibonacci number or not
static void ifgcdFibonacci(int a[], int n, int k)
{
    Vector<Integer> compositeset = new Vector<>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If array element is composite
        // and divisible by k
        if (isComposite(a[i]) && a[i] % k == 0)
        {
            compositeset.add(a[i]);
        }
    }
    int gcd = compositeset.get(0);

    // Calculate GCD of all elements in compositeset
    for(int i = 1; i < compositeset.size(); i++)
    {
        gcd = __gcd(gcd, compositeset.get(i));

        if (gcd == 1)
        {
            break;
        }
    }

    // If GCD is Fibonacci
    if (isFibonacci(gcd))
    {
        System.out.print("Yes");
        return;
    }
    System.out.print("No");
    return;
}

// Recursive function to return gcd of a and b 
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 34, 2, 4, 8, 5, 7, 11 };
    int n = arr.length;
    int k = 2;

    ifgcdFibonacci(arr, n, k);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if a
# number is composite or not
def isComposite(n):

    # Corner cases
    if n <= 1:
        return False

    if n <= 3:
        return False

    # Check if the number is
    # divisible by 2 or 3 or not
    if n % 2 == 0 or n % 3 == 0:
        return True

    # Check if n is a multiple of
    # any other prime number
    i = 5
    while i * i <= n:
        if ((n % i == 0 ) or
            (n % (i + 2) == 0)):
            return True

        i += 6   

    return False

# Function to check if a number
# is a Perfect Square or not
def isPerfectSquare(x):

    s = int(math.sqrt(x))
    return (s * s == x)

# Function to check if a number
# is a Fibonacci number or not
def isFibonacci(n):

    # If 5*n^2 + 4 or 5*n^2 - 4 or
    # both are perfect square
    return (isPerfectSquare(5 * n * n + 4) or
            isPerfectSquare(5 * n * n - 4))

# Function to check if GCD of composite
# numbers from the array a[] which are
# divisible by k is a Fibonacci number or not
def ifgcdFibonacci(a,  n,  k):

    compositeset = []

    # Traverse the array
    for i in range(n):

        # If array element is composite
        # and divisible by k
        if (isComposite(a[i]) and a[i] % k == 0):
            compositeset.append(a[i])

    gcd = compositeset[0]

    # Calculate GCD of all elements in compositeset
    for i in range(1, len(compositeset), 1):
        gcd = math.gcd(gcd, compositeset[i])

        if gcd == 1:
            break

    # If GCD is Fibonacci
    if (isFibonacci(gcd)):
        print("Yes")
        return

    print("No")
    return

# Driver Code
if __name__ == "__main__" :

    arr = [ 34, 2, 4, 8, 5, 7, 11 ]
    n = len(arr)
    k = 2

    ifgcdFibonacci(arr, n, k)

# This code is contributed by jana_sayantan
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if a
// number is composite or not
static bool isComposite(int n)
{

    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return false;

    // Check if the number is
    // divisible by 2 or 3 or not
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    // Check if n is a multiple of
    // any other prime number
    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to check if a number
// is a Perfect Square or not
static bool isPerfectSquare(int x)
{
    int s = (int)Math.Sqrt(x);
    return (s * s == x);
}

// Function to check if a number
// is a Fibonacci number or not
static bool isFibonacci(int n)
{

    // If 5*n^2 + 4 or 5*n^2 - 4 or
    // both are perfect square
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to check if GCD of composite
// numbers from the array []a which are
// divisible by k is a Fibonacci number or not
static void ifgcdFibonacci(int []a, int n, int k)
{
    List<int> compositeset = new List<int>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If array element is composite
        // and divisible by k
        if (isComposite(a[i]) && a[i] % k == 0)
        {
            compositeset.Add(a[i]);
        }
    }
    int gcd = compositeset[0];

    // Calculate GCD of all elements in compositeset
    for(int i = 1; i < compositeset.Count; i++)
    {
        gcd = __gcd(gcd, compositeset[i]);

        if (gcd == 1)
        {
            break;
        }
    }

    // If GCD is Fibonacci
    if (isFibonacci(gcd))
    {
        Console.Write("Yes");
        return;
    }
    Console.Write("No");
    return;
}

// Recursive function to return gcd of a and b 
static int __gcd(int a, int b) 
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 34, 2, 4, 8, 5, 7, 11 };
    int n = arr.Length;
    int k = 2;

    ifgcdFibonacci(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

function __gcd(a, b) {
  if (!b) {
    return a;
  }

  return __gcd(b, a % b);
}

// Function to check if a
// number is composite or not
function isComposite(n)
{
    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return false;

    // Check if the number is
    // divisible by 2 or 3 or not
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    var i;
    // Check if n is a multiple of
    // any other prime number
    for(i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to check if a number
// is a Perfect Square or not
function isPerfectSquare(x)
{
    var s = Math.sqrt(x);
    return (s * s == x);
}

// Function to check if a number
// is a Fibonacci number or not
function isFibonacci(n)
{
    // If 5*n^2 + 4 or 5*n^2 - 4 or
    // both are perfect square
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to check if GCD of composite
// numbers from the array a[] which are
// divisible by k is a Fibonacci number or not
function ifgcdFibonacci(a, n, k)
{
    var compositeset = [];

    var i;
    // Traverse the array
    for (i = 0; i < n; i++) {

        // If array element is composite
        // and divisible by k
        if (isComposite(a[i]) && a[i] % k == 0) {
            compositeset.push(a[i]);
        }
    }
    var gcd = compositeset[0];

    // Calculate GCD of all elements in compositeset
    for (i = 1; i < compositeset.length; i++) {
        gcd = __gcd(gcd, compositeset[i]);
        if (gcd == 1) {
            break;
        }
    }

    // If GCD is Fibonacci
    if (isFibonacci(gcd)) {
        document.write("Yes");
        return;
    }
    document.write("No");
    return;
}

// Driver Code
    var arr = [34, 2, 4, 8, 5, 7, 11];
    var n = arr.length;
    var k = 2;

    ifgcdFibonacci(arr, n, k);

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N*log(N))，其中 N 是数组的大小
T3】辅助空间: O(N)