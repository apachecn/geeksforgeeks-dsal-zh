# 检查兑换是否可能

> 原文:[https://www . geeksforgeeks . org/check-交换是否可能/](https://www.geeksforgeeks.org/check-whether-the-exchange-is-possible-or-not/)

给定一个国家的货币面额类型作为一个数组 **arr[]** 。一个人和店主可以多次选择每种面额的纸币。任务是检查当该人想从商店购买价值 **P** 的产品时，交换是否可能。
**举例:**

> **输入:** arr[] = {6，9}，P = 3
> **输出:**是
> 此人可以支付 9，得到 6 作为回报。
> **输入:** arr[] = {6，9}，P = 4
> **输出:**否

**方法:**为了使兑换成为可能， **P** 必须能被所有面额的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 整除。所以，求数组元素的 gcd，检查 **P** 是否能被它整除。
以下是实施办法:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// the exchange is possible
bool isPossible(int arr[], int n, int p)
{

    // Find the GCD of the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // If the exchange is possible
    if (p % gcd == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 6, 9 };
    int n = sizeof(arr) / sizeof(int);
    int p = 3;

    if (isPossible(arr, n, p))
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

    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function that returns true if
    // the exchange is possible
    static boolean isPossible(int []arr,
                              int n, int p)
    {

        // Find the GCD of the array elements
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = __gcd(gcd, arr[i]);

        // If the exchange is possible
        if (p % gcd == 0)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 6, 9 };
        int n = arr.length;
        int p = 3;

        if (isPossible(arr, n, p))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

# Function that returns true if
# the exchange is possible
def isPossible(arr, n, p) :

    # Find the GCD of the array elements
    gcd = 0;
    for i in range(n) :
        gcd = __gcd(gcd, arr[i]);

    # If the exchange is possible
    if (p % gcd == 0) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    arr = [ 6, 9 ];
    n = len(arr);
    p = 3;

    if (isPossible(arr, n, p)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function that returns true if
    // the exchange is possible
    static bool isPossible(int []arr,
                           int n, int p)
    {

        // Find the GCD of the array elements
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = __gcd(gcd, arr[i]);

        // If the exchange is possible
        if (p % gcd == 0)
            return true;

        return false;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 6, 9 };
        int n = arr.Length;
        int p = 3;

        if (isPossible(arr, n, p))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Recursive function to
    // return gcd of a and b
    function __gcd(a, b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function that returns true if
    // the exchange is possible
    function isPossible(arr, n, p)
    {

        // Find the GCD of the array elements
        let gcd = 0;
        for (let i = 0; i < n; i++)
            gcd = __gcd(gcd, arr[i]);

        // If the exchange is possible
        if (p % gcd == 0)
            return true;

        return false;
    }

    let arr = [ 6, 9 ];
    let n = arr.length;
    let p = 3;

    if (isPossible(arr, n, p))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output:** 

```
Yes
```