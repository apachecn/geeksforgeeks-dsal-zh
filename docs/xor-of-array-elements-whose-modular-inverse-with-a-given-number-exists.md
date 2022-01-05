# 给定个数的模逆存在的数组元素的异或

> 原文:[https://www . geeksforgeeks . org/数组元素的异或运算-给定数字的模逆运算-存在/](https://www.geeksforgeeks.org/xor-of-array-elements-whose-modular-inverse-with-a-given-number-exists/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个正整数 **M** ，任务是找到其[模逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)与 **M** 存在的所有数组元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = {1，2，3}，M = 4
> **输出:** 2
> **解释:**
> 初始化与 0 异或的值:
> 对于索引为 0 即 1 的元素，其与 4 的 mod 逆为 1，因为(1 * 1) % 4 = 1 即它存在。因此，xor = (xor ^ 1) = 1。
> 对于索引为 1 即 2 的元素，其 mod 逆不存在。
> 对于索引为 2 即 3 的元素，它与 4 的 mod 逆为 3，因为(3 * 3) % 4 = 1 即它存在。因此，xor = (xor ^ 3) = 2。
> 因此，异或为 2。
> 
> **输入:** arr[] = {3，6，4，5，8}，M = 9
> **输出:** 9
> **解释:**
> 初始化与 0 异或的值:
> 对于索引为 0 即 3 的元素，其 mod 逆不存在。
> 对于索引为 1 即 6 的元素，其 mod 逆不存在。
> 对于索引为 2 即 4 的元素，它与 9 的 mod 倒数是 7，因为(4 * 7) % 9 = 1 即它存在。因此，xor = (xor ^ 4) = 4。
> 对于索引为 3 即 5 的元素，它与 9 的 mod 倒数是 2，因为(5 * 2) % 9 = 1 即它存在。因此，xor = (xor ^ 5) = 1。
> 对于索引为 4 即 8 的元素，它与 9 的 mod 倒数是 8，因为(8 * 8) % 9 = 1 即它存在。因此，xor = (xor ^ 8) = 9。
> 因此，异或是 9。

**<u>天真方法</u> :** 最简单的方法是打印数组中存在任何 **j** 的所有元素的[异或，其中 **(1 < = j < M)** 使得 **(arr[i] * j) % M = 1** 其中 **0 ≤ i < N** 。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)

***时间复杂度:** O(N * M)*
***辅助空间:** O(N)*

**高效法:**优化上述方法，思路是利用 mod **M** 下任意数 **X** 的[模逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)存在的性质，当且仅当 M 和 X 的 [GCD 为 1](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) ，即 **gcd(M，X)** 为 **1** 。按照以下步骤解决问题:

1.  初始化一个变量**将**与 **0** 异或，以存储所有在 **M** 下存在模逆的元素的异或。
2.  [在**【0，N–1】**范围内遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)。
3.  如果[**gcd(M，arr[i])**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 为 **1** 则更新 **xor** 为**xor =(xor^arr[i)**。
4.  遍历后，将值**异或**打印为所需结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the gcd of a & b
int gcd(int a, int b)
{
    // Base Case
    if (a == 0)
        return b;

     // Recursively calculate GCD
    return gcd(b % a, a);
}

// Function to print the Bitwise XOR of
// elements of arr[] if gcd(arr[i], M) is 1
void countInverse(int arr[], int N, int M)
{
    // Initialize xor
    int XOR = 0;

    // Traversing the array
    for (int i = 0; i < N; i++) {

        // GCD of M and arr[i]
        int gcdOfMandelement
          = gcd(M, arr[i]);

        // If GCD is 1, update xor
        if (gcdOfMandelement == 1) {

            XOR ^= arr[i];
        }
    }

    // Print xor
    cout << XOR << ' ';
}

// Drive Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3 };

    // Given number M
    int M = 4;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countInverse(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to return the gcd of a & b
static int gcd(int a, int b)
{

    // Base Case
    if (a == 0)
        return b;

    // Recursively calculate GCD
    return gcd(b % a, a);
}

// Function to print the Bitwise XOR of
// elements of arr[] if gcd(arr[i], M) is 1
static void countInverse(int[] arr, int N, int M)
{

    // Initialize xor
    int XOR = 0;

    // Traversing the array
    for(int i = 0; i < N; i++)
    {

        // GCD of M and arr[i]
        int gcdOfMandelement = gcd(M, arr[i]);

        // If GCD is 1, update xor
        if (gcdOfMandelement == 1)
        {
            XOR ^= arr[i];
        }
    }

    // Print xor
    System.out.println(XOR);
}

// Drive Code
public static void main(String[] args)
{

    // Given array arr[]
    int[] arr = { 1, 2, 3 };

    // Given number M
    int M = 4;

    // Size of the array
    int N = arr.length;

    // Function Call
    countInverse(arr, N, M);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the gcd of a & b
def gcd(a, b):

    # Base Case
    if (a == 0):
        return b

    # Recursively calculate GCD
    return gcd(b % a, a)

# Function to print the Bitwise XOR of
# elements of arr[] if gcd(arr[i], M) is 1
def countInverse(arr, N, M):

    # Initialize xor
    XOR = 0

    # Traversing the array
    for i in range(0, N):

        # GCD of M and arr[i]
        gcdOfMandelement = gcd(M, arr[i])

        # If GCD is 1, update xor
        if (gcdOfMandelement == 1):
            XOR = XOR ^ arr[i]

    # Print xor
    print(XOR)

# Drive Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3 ]

    # Given number M
    M = 4

    # Size of the array
    N = len(arr)

    # Function Call
    countInverse(arr, N, M)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the gcd of a & b
static int gcd(int a, int b)
{

    // Base Case
    if (a == 0)
        return b;

    // Recursively calculate GCD
    return gcd(b % a, a);
}

// Function to print the Bitwise XOR of
// elements of arr[] if gcd(arr[i], M) is 1
static void countInverse(int[] arr, int N, int M)
{

    // Initialize xor
    int XOR = 0;

    // Traversing the array
    for(int i = 0; i < N; i++)
    {

        // GCD of M and arr[i]
        int gcdOfMandelement = gcd(M, arr[i]);

        // If GCD is 1, update xor
        if (gcdOfMandelement == 1)
        {

            XOR ^= arr[i];
        }
    }

    // Print xor
    Console.WriteLine(XOR);
}

// Drive Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 1, 2, 3 };

    // Given number M
    int M = 4;

    // Size of the array
    int N = arr.Length;

    // Function Call
    countInverse(arr, N, M);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the gcd of a & b
function gcd(a, b)
{

    // Base Case
    if (a == 0)
        return b;

    // Recursively calculate GCD
    return gcd(b % a, a);
}

// Function to print the Bitwise XOR of
// elements of arr[] if gcd(arr[i], M) is 1
function countInverse(arr, N, M)
{

    // Initialize xor
    var XOR = 0;

    // Traversing the array
    for(var i = 0; i < N; i++)
    {

        // GCD of M and arr[i]
        var gcdOfMandelement = gcd(M, arr[i]);

        // If GCD is 1, update xor
        if (gcdOfMandelement == 1)
        {
            XOR ^= arr[i];
        }
    }

    // Print xor
    document.write(XOR);
}

// Driver Code

// Given array arr[]
var arr = [ 1, 2, 3 ];

// Given number M
var M = 4;

// Size of the array
var N = arr.length;

// Function Call
countInverse(arr, N, M);

// This code is contributed by Kirti

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log M)*
***辅助空间:** O(N)*