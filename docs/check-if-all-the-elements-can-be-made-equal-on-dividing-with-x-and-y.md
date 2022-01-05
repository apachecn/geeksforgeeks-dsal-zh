# 检查用 X 和 Y 除是否可以使所有元素相等

> 原文:[https://www . geeksforgeeks . org/check-if-all-elements-on-division-with-x-and-y/](https://www.geeksforgeeks.org/check-if-all-the-elements-can-be-made-equal-on-dividing-with-x-and-y/)

给定一个数组 **arr[]** 和两个整数 **X** 和 **Y** 。任务是检查是否可以用 **X** 和 **Y** 对所有元素进行任意次包括 0 的除法运算，使所有元素相等。

**示例:**

> **输入:** arr[] = {2，4，6，8}，X = 2，Y = 3
> **输出:**Yes
> 2->2
> 4->(4/X)=(4/2)= 2
> 6->(6/Y)=(6/3)= 2
> 8->(8/X)=(8/2)= 4 和 4->(4/X)=(2)
> 
> **输入:** arr[] = {2，4，10}，X = 11，Y = 12
> T3】输出:否

**方法:**从给定的数组中找到所有元素的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，因为这个 gcd 是我们可以通过用一些任意常数(比如 **gcd = arr[0] / k1 或 arr[1] / k2 或…或 arr[n-1] / kn** )除所有元素而得到的值。现在的任务是找出这些常数 **k1，k2，k3，…，kn** 是否为**X * X * X *……* Y Y *……。**。如果是，那么有可能使所有元素与给定的操作相等，否则就不相等。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if num
// is of the form x*x*x*...*y*y*...
bool isDivisible(int num, int x, int y)
{

    // While num divisible is divible
    // by either x or y, keep dividing
    while (num % x == 0 || num % y == 0) {
        if (num % x == 0)
            num /= x;
        if (num % y == 0)
            num /= y;
    }

    // If num > 1, it means it cannot be
    // further divided by either x or y
    if (num > 1)
        return false;

    return true;
}

// Function that returns true if all
// the array elements can be made
// equal with the given operation
bool isPossible(int arr[], int n, int x, int y)
{

    // To store the gcd of the array elements
    int gcd = arr[0];
    for (int i = 1; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // Check if k is of the form x*x*..*y*y*...
        // where (gcd * k = arr[i])
        if (!isDivisible(arr[i] / gcd, x, y))
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 2, y = 3;

    if (isPossible(arr, n, x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function that returns true if num
    // is of the form x*x*x*...*y*y*...
    public static boolean isDivisible(int num, int x, int y)
    {

        // While num divisible is divible
        // by either x or y, keep dividing
        while (num % x == 0 || num % y == 0)
        {
            if (num % x == 0)
                num /= x;
            if (num % y == 0)
                num /= y;
        }

        // If num > 1, it means it cannot be
        // further divided by either x or y
        if (num > 1)
            return false;

        return true;
    }

    // Function to calculate gcd of two numbers
    // using Euclid's algorithm
    public static int _gcd(int a, int b)
    {
        while (a != b)
        {
            if (a > b)
                a = a - b;
            else
                b = b - a;
        }

        return a;
    }

    // Function that returns true if all
    // the array elements can be made
    // equal with the given operation
    public static boolean isPossible(int[] arr, int n,
                                        int x, int y)
    {

        // To store the gcd of the array elements
        int gcd = arr[0];
        for (int i = 1; i < n; i++)
            gcd = _gcd(gcd, arr[i]);

        // For every element of the array
        for (int i = 0; i < n; i++)
        {

            // Check if k is of the form x*x*..*y*y*...
            // where (gcd * k = arr[i])
            if (!isDivisible(arr[i] / gcd, x, y))
                return false;
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 2, 4, 6, 8 };
        int n = arr.length;
        int x = 2, y = 3;
        if (isPossible(arr, n, x, y))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

# Function that returns True if num
# is of the form x*x*x*...*y*y*...
def isDivisible(num, x, y):

    # While num divisible is divible
    # by either x or y, keep dividing
    while (num % x == 0 or num % y == 0):
        if (num % x == 0):
            num //= x
        if (num % y == 0):
            num //= y

    # If num > 1, it means it cannot be
    # further divided by either x or y
    if (num > 1):
        return False

    return True

# Function that returns True if all
# the array elements can be made
# equal with the given operation
def isPossible(arr, n, x, y):

    # To store the gcd of the array elements
    gcd = arr[0]
    for i in range(1,n):
        gcd = __gcd(gcd, arr[i])

    # For every element of the array
    for i in range(n):

        # Check if k is of the form x*x*..*y*y*...
        # where (gcd * k = arr[i])
        if (isDivisible(arr[i] // gcd, x, y) == False):
            return False
    return True

# Driver code

arr = [2, 4, 6, 8]
n = len(arr)
x = 2
y = 3

if (isPossible(arr, n, x, y) == True):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if num
    // is of the form x*x*x*...*y*y*...
    public static bool isDivisible(int num, int x, int y)
    {

        // While num divisible is divible
        // by either x or y, keep dividing
        while (num % x == 0 || num % y == 0)
        {
            if (num % x == 0)
                num /= x;
            if (num % y == 0)
                num /= y;
        }

        // If num > 1, it means it cannot be
        // further divided by either x or y
        if (num > 1)
            return false;

        return true;
    }

    // Function to calculate gcd of two numbers
    // using Euclid's algorithm
    public static int _gcd(int a, int b)
    {
        while (a != b)
        {
            if (a > b)
                a = a - b;
            else
                b = b - a;
        }

        return a;
    }

    // Function that returns true if all
    // the array elements can be made
    // equal with the given operation
    public static bool isPossible(int[] arr, int n,
                                        int x, int y)
    {

        // To store the gcd of the array elements
        int gcd = arr[0];
        for (int i = 1; i < n; i++)
            gcd = _gcd(gcd, arr[i]);

        // For every element of the array
        for (int i = 0; i < n; i++)
        {

            // Check if k is of the form x*x*..*y*y*...
            // where (gcd * k = arr[i])
            if (!isDivisible(arr[i] / gcd, x, y))
                return false;
        }
        return true;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 4, 6, 8 };
        int n = arr.Length;
        int x = 2, y = 3;
        if (isPossible(arr, n, x, y))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by
// anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if num
// is of the form x*x*x*...*y*y*...
function isDivisible(num, x, y)
{

    // While num divisible is divible
    // by either x or y, keep dividing
    while (num % x == 0 || num % y == 0) {
        if (num % x == 0)
            num /= x;
        if (num % y == 0)
            num /= y;
    }

    // If num > 1, it means it cannot be
    // further divided by either x or y
    if (num > 1)
        return false;

    return true;
}

 // Function to calculate gcd of two numbers
// using Euclid's algorithm
function __gcd(a, b)
{
    while (a != b)
    {
        if (a > b)
            a = a - b;
        else
            b = b - a;
    }
    return a;
}

// Function that returns true if all
// the array elements can be made
// equal with the given operation
function isPossible(arr, n, x, y)
{

    // To store the gcd of the array elements
    var gcd = arr[0];
    for (var i = 1; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // For every element of the array
    for (var i = 0; i < n; i++) {

        // Check if k is of the form x*x*..*y*y*...
        // where (gcd * k = arr[i])
        if (!isDivisible(arr[i] / gcd, x, y))
            return false;
    }
    return true;
}

// Driver code
var arr = [ 2, 4, 6, 8 ];
var n = arr.length;
var x = 2, y = 3;
if (isPossible(arr, n, x, y))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```