# 求 M 和 N 的二进制表示串联后得到的数

> 原文:[https://www . geeksforgeeks . org/find-m 和 n 的二进制表示串联后获得的数字/](https://www.geeksforgeeks.org/find-the-number-obtained-after-concatenation-of-binary-representation-of-m-and-n/)

给定两个整数 **M** 和 **N** ，任务是找到通过连接 **M** 和 **N** 的二进制等价物形成的数，即 **M + N** 。

**示例:**

> **输入:** M = 4，N = 5
> **输出:**37
> 4 的二进制等效值为 100，5 的二进制等效值为 101
> 串接后，形成的结果二进制数
> 为 100101，其十进制等效值为 37。
> 
> **输入:** M = 3，N = 4
> T3】输出: 28

**方法:**将数字 **M** 和 **N** 转换为二进制等价数，然后将这些数字连接为 **M + N** ，并打印连接后形成的二进制数的十进制等价数。

下面是上述方法的实现:

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

// Funtion to convert the number
// represented as a binary array
// arr[] into its decimal equivalent
int binaryDec(int arr[], int n)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += arr[i] << (n - i - 1);
    return ans;
}

// Function to concatenate the binary
// numbers and return the decimal result
int concat(int m, int n)
{

    // Number of bits in both the numbers
    int k = log2(m) + 1;
    int l = log2(n) + 1;

    // Convert the bits in both the integers
    // to the arrays a[] and b[]
    int a[k] = { 0 }, b[l] = { 0 };

    // c[] will be the binary array
    // for the result
    int c[k + l] = { 0 };
    decBinary(a, m);
    decBinary(b, n);

    // Update the c[] array
    int in = 0;
    for (int i = 0; i < k; i++)
        c[in++] = a[i];
    for (int i = 0; i < l; i++)
        c[in++] = b[i];

    // Return the decimal equivalent
    // of the result
    return (binaryDec(c, k + l));
}

// Driver code
int main()
{
    int m = 4, n = 5;

    cout << concat(m, n);

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

    // Funtion to convert the number
    // represented as a binary array
    // arr[] into its decimal equivalent
    static int binaryDec(int arr[], int n)
    {
        int ans = 0;
        for (int i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to concatenate the binary
    // numbers and return the decimal result
    static int concat(int m, int n)
    {

        // Number of bits in both the numbers
        int k = (int)(Math.log(m) /
                      Math.log(2)) + 1;
        int l = (int)(Math.log(n) /
                      Math.log(2)) + 1;

        // Convert the bits in both the integers
        // to the arrays a[] and b[]
        int a[] = new int[k];
        int b[] = new int[l];

        // c[] will be the binary array
        // for the result
        int c[] = new int[k + l];
        decBinary(a, m);
        decBinary(b, n);

        // Update the c[] array
        int in = 0;
        for (int i = 0; i < k; i++)
            c[in++] = a[i];
        for (int i = 0; i < l; i++)
            c[in++] = b[i];

        // Return the decimal equivalent
        // of the result
        return (binaryDec(c, k + l));
    }

    // Driver code
    public static void main (String[] args)
    {
        int m = 4, n = 5;

        System.out.println(concat(m, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
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

# Funtion to convert the number
# represented as a binary array
# arr[] its decimal equivalent
def binaryDec(arr, n):
    ans = 0
    for i in range(0, n):
        ans = ans + (arr[i] << (n - i - 1))
    return ans

# Function to concatenate the binary
# numbers and return the decimal result
def concat(m, n):

    # Number of bits in both the numbers
    k = int(math.log2(m)) + 1
    l = int(math.log2(n)) + 1

    # Convert the bits in both the gers
    # to the arrays a[] and b[]
    a = [0 for i in range(0, k)]
    b = [0 for i in range(0, l)]

    # c[] will be the binary array
    # for the result
    c = [0 for i in range(0, k + l)]
    decBinary(a, m);
    decBinary(b, n);

    # Update the c[] array
    iin = 0
    for i in range(0, k):
        c[iin] = a[i]
        iin = iin + 1
    for i in range(0, l):
        c[iin] = b[i]
        iin = iin + 1

    # Return the decimal equivalent
    # of the result
    return (binaryDec(c, k + l))

# Driver code
m = 4
n = 5

print(concat(m, n))

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

    // Funtion to convert the number
    // represented as a binary array
    // []arr into its decimal equivalent
    static int binaryDec(int []arr, int n)
    {
        int ans = 0;
        for (int i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to concatenate the binary
    // numbers and return the decimal result
    static int concat(int m, int n)
    {

        // Number of bits in both the numbers
        int k = (int)(Math.Log(m) /
                      Math.Log(2)) + 1;
        int l = (int)(Math.Log(n) /
                      Math.Log(2)) + 1;

        // Convert the bits in both the integers
        // to the arrays []a and []b
        int []a = new int[k];
        int []b = new int[l];

        // c[] will be the binary array
        // for the result
        int []c = new int[k + l];
        decBinary(a, m);
        decBinary(b, n);

        // Update the c[] array
        int iN = 0;
        for (int i = 0; i < k; i++)
            c[iN++] = a[i];
        for (int i = 0; i < l; i++)
            c[iN++] = b[i];

        // Return the decimal equivalent
        // of the result
        return (binaryDec(c, k + l));
    }

    // Driver code
    public static void Main(String[] args)
    {
        int m = 4, n = 5;

        Console.WriteLine(concat(m, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to convert decimal number n
    // to its binary representation
    // stored as an array []arr
    function decBinary(arr, n)
    {
        let k = parseInt(Math.log(n) / Math.log(2), 10);

        while (n > 0)
        {
            arr[k--] = n % 2;
            n = parseInt(n / 2, 10);
        }
    }

    // Funtion to convert the number
    // represented as a binary array
    // []arr into its decimal equivalent
    function binaryDec(arr, n)
    {
        let ans = 0;
        for (let i = 0; i < n; i++)
            ans += arr[i] << (n - i - 1);
        return ans;
    }

    // Function to concatenate the binary
    // numbers and return the decimal result
    function concat(m, n)
    {

        // Number of bits in both the numbers
        let k = parseInt(Math.log(m) / Math.log(2), 10) + 1;
        let l = parseInt(Math.log(n) / Math.log(2), 10) + 1;

        // Convert the bits in both the integers
        // to the arrays []a and []b
        let a = new Array(k);
        let b = new Array(l);

        // c[] will be the binary array
        // for the result
        let c = new Array(k + l);
        decBinary(a, m);
        decBinary(b, n);

        // Update the c[] array
        let iN = 0;
        for (let i = 0; i < k; i++)
            c[iN++] = a[i];
        for (let i = 0; i < l; i++)
            c[iN++] = b[i];

        // Return the decimal equivalent
        // of the result
        return (binaryDec(c, k + l));
    }

    let m = 4, n = 5;

    document.write(concat(m, n));

    // This code is contributed by rameshtravel07.
</script>
```

**Output**

```
37
```

上述解的时间复杂度为 **O(log(m) + log(n))** 。

我们可以通过使用**二进制移位算子**将上述问题的时间复杂度提高到 **O(log(n))** 。

**更好的接近**:

我们将把数字 M 向左二进制移位 n 中的位数。

例如:

> M=4，N=5
> 
> bin(N) = 101，具有二进制表示三。
> 
> 我们将二进制 M 左移 3，然后加上 n。
> 
> M<<3 + N = 37。

由于二进制移位运算符采用**恒定时间**，因此第二步在恒定时间内完成，整体时间复杂度为 **O(log(N))** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to calculate binary
// length of a number.
int getBinaryLength(int n)
{
    int length = 0;
    while (n > 0) {
        length += 1;
        n /= 2;
    }
    return length;
}

// Function to concatenate the binary
// numbers and return the decimal result
int concat(int m, int n)
{
    // find binary length of n
    int length = getBinaryLength(n);

    // left binary shift m and then add n
    return (m << length) + n;
}

// Driver code
int main()
{
    int m = 4, n = 5;

    cout << concat(m, n);

    return 0;
}

// This code is contributed by Vivek Moar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Utility function to calculate binary
// length of a number.
public static int getBinaryLength(int n)
{
    int length = 0;
    while (n > 0)
    {
        length += 1;
        n /= 2;
    }
    return length;
}

// Function to concatenate the binary
// numbers and return the decimal result
public static int concat(int m, int n)
{

    // Find binary length of n
    int length = getBinaryLength(n);

    // left binary shift m and then add n
    return (m << length) + n;
}

// Driver code
public static void main(String[] args) throws Exception
{
    int m = 4, n = 5;

    System.out.println(concat(m, n));
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to calculate binary
# length of a number.

def getBinaryLength(n):
    length = 0
    while(n > 0):
        length += 1
        n //= 2
    return length

# Function to concatenate the binary
# numbers and return the decimal result

def concat(m, n):
    # find binary length of n
    length = getBinaryLength(n)

    # left binary shift m and then add n
    return (m << length) + n

# Driver code

m, n = 4, 5

print(concat(m, n))

# This code is contributed by Vivek Moar
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Utility function to calculate binary
// length of a number.
static int getBinaryLength(int n)
{
    int length = 0;

    while (n > 0)
    {
        length += 1;
        n /= 2;
    }
    return length;
}

// Function to concatenate the binary
// numbers and return the decimal result
static int concat(int m, int n)
{

    // Find binary length of n
    int length = getBinaryLength(n);

    // left binary shift m and then add n
    return (m << length) + n;
}

// Driver code
static void Main()
{
    int m = 4, n = 5;

    Console.WriteLine(concat(m, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Utility function to calculate binary
    // length of a number.
    function getBinaryLength(n)
    {
        let length = 0;

        while (n > 0)
        {
            length += 1;
            n = parseInt(n / 2, 10);
        }
        return length;
    }

    // Function to concatenate the binary
    // numbers and return the decimal result
    function concat(m, n)
    {

        // Find binary length of n
        let length = getBinaryLength(n);

        // left binary shift m and then add n
        return (m << length) + n;
    }

    let m = 4, n = 5;

    document.write(concat(m, n));

</script>
```

**Output**

```
37
```

时间复杂度: **O(log(n))** 。