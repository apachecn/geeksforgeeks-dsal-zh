# 反转 N 的第 k 个最高有效位

> 原文:[https://www . geeksforgeeks . org/反转 n 的第 k 个最高有效位/](https://www.geeksforgeeks.org/invert-the-kth-most-significant-bit-of-n/)

给定两个非负整数 **N** 和 **K** ，任务是将 **N** 的 **K <sup>第</sup>T7】个最高有效位反相，并打印反相后得到的数字。
**举例:**** 

> **输入:** N = 10，K = 1
> **输出:**2
> **10**的二进制表示为 **1010** 。
> 第一位反相后变为 **0010**
> ，其十进制等价为 **2** 。
> **输入:** N = 56，K = 2
> **输出:** 40

**方法:**找出 **N** 中的位数，如果位数小于 **K** ，那么 **N** 本身就是需要的答案，否则翻转 **N** 的 **K <sup>th</sup>** 最高有效位，打印翻转后得到的数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal number n
// to its binary representation
// stored as an array arr[]
void decBinary(int arr[], int n)
{
    int k = log2(n);
    while (n > 0) {
        arr[k--] = n % 2;
        n /= 2;
    }
}

// Function to convert the number
// represented as a binary array
// arr[] into its decimal equivalent
int binaryDec(int arr[], int n)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += arr[i] << (n - i - 1);
    return ans;
}

// Function to return the updated integer
// after flipping the kth bit
int getNum(int n, int k)
{

    // Number of bits in n
    int l = log2(n) + 1;

    // Find the binary
    // representation of n
    int a[l] = { 0 };
    decBinary(a, n);

    // The number of bits in n
    // are less than k
    if (k > l)
        return n;

    // Flip the kth bit
    a[k - 1] = (a[k - 1] == 0) ? 1 : 0;

    // Return the decimal equivalent
    // of the number
    return binaryDec(a, l);
}

// Driver code
int main()
{
    int n = 56, k = 2;

    cout << getNum(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to convert decimal number n
    // to its binary representation
    // stored as an array arr[]
    static void decBinary(int arr[], int n)
    {
        int k = (int)(Math.log(n) /
                      Math.log(2));

        while (n > 0)
        {
            arr[k--] = n % 2;
            n /= 2;
        }
    }

    // Function to convert the number
    // represented as a binary array
    // arr[] into its decimal equivalent
    static int binaryDec(int arr[], int n)
    {
        int ans = 0;
        for (int i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to return the updated integer
    // after flipping the kth bit
    static int getNum(int n, int k)
    {

        // Number of bits in n
        int l = (int)(Math.log(n) /
                      Math.log(2)) + 1;

        // Find the binary
        // representation of n
        int a[] = new int[l];
        decBinary(a, n);

        // The number of bits in n
        // are less than k
        if (k > l)
            return n;

        // Flip the kth bit
        a[k - 1] = (a[k - 1] == 0) ? 1 : 0;

        // Return the decimal equivalent
        // of the number
        return binaryDec(a, l);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 56;
        int k = 2;

        System.out.println(getNum(n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python implementation of the approach
import math

# Function to convert decimal number n
# to its binary representation
# stored as an array arr[]
def decBinary(arr, n):
    k = int(math.log2(n))
    while (n > 0):
        arr[k] = n % 2
        k = k - 1
        n = n//2

# Function to convert the number
# represented as a binary array
# arr[] its decimal equivalent
def binaryDec(arr, n):
    ans = 0
    for i in range(0, n):
        ans = ans + (arr[i] << (n - i - 1))
    return ans

# Function to concatenate the binary
# numbers and return the decimal result
def getNum(n, k):

    # Number of bits in both the numbers
    l = int(math.log2(n)) + 1

    # Convert the bits in both the gers
    # to the arrays a[] and b[]
    a = [0 for i in range(0, l)]

    decBinary(a, n)
    # The number of bits in n
    # are less than k
    if(k > l):
        return n

    # Flip the kth bit
    if(a[k - 1] == 0):
        a[k - 1] = 1
    else:
        a[k - 1] = 0

    # Return the decimal equivalent
    # of the number
    return binaryDec(a, l)

# Driver code
n = 56
k = 2

print(getNum(n, k))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to convert decimal number n
    // to its binary representation
    // stored as an array []arr
    static void decBinary(int []arr, int n)
    {
        int k = (int)(Math.Log(n) /
                      Math.Log(2));

        while (n > 0)
        {
            arr[k--] = n % 2;
            n /= 2;
        }
    }

    // Function to convert the number
    // represented as a binary array
    // []arr into its decimal equivalent
    static int binaryDec(int []arr, int n)
    {
        int ans = 0;
        for (int i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to return the updated integer
    // after flipping the kth bit
    static int getNum(int n, int k)
    {

        // Number of bits in n
        int l = (int)(Math.Log(n) /
                      Math.Log(2)) + 1;

        // Find the binary
        // representation of n
        int []a = new int[l];
        decBinary(a, n);

        // The number of bits in n
        // are less than k
        if (k > l)
            return n;

        // Flip the kth bit
        a[k - 1] = (a[k - 1] == 0) ? 1 : 0;

        // Return the decimal equivalent
        // of the number
        return binaryDec(a, l);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 56;
        int k = 2;

        Console.WriteLine(getNum(n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // javascript implementation of the approach

    // Function to convert decimal number n
    // to its binary representation
    // stored as an array arr[]
    function decBinary(arr, n)
    {
      let k = parseInt(Math.log2(n), 10);
        while (n > 0)
        {
            arr[k--] = n % 2;
            n = parseInt(n/2,10);
        }
    }

    // Function to convert the number
    // represented as a binary array
    // arr[] into its decimal equivalent
    function binaryDec(arr, n)
    {
        let ans = 0;
        for (let i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to return the updated integer
    // after flipping the kth bit
    function getNum(n,k)
    {

        // Number of bits in n
        let l = parseInt(Math.log2(n),10) + 1;

        // Find the binary
        // representation of n
        let a =  new Array(l);
        a.fill(0);
        decBinary(a, n);

        // The number of bits in n
        // are less than k
        if (k > l)
            return n;

        // Flip the kth bit
        a[k - 1] = (a[k - 1] == 0) ? 1 : 0;

        // Return the decimal equivalent
        // of the number
        return binaryDec(a, l);
    }

    let n = 56, k = 2;
    document.write(getNum(n, k));

    // This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
40
```