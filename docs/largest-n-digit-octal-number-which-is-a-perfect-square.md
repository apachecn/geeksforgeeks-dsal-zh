# 最大的 N 位八进制数，它是一个完美的正方形

> 原文:[https://www . geesforgeks . org/最大 n 位八进制数-哪是完美的正方形/](https://www.geeksforgeeks.org/largest-n-digit-octal-number-which-is-a-perfect-square/)

给定一个自然数 **N** ，任务是找到最大的 N 位八进制数，它是一个完美的正方形。
**例:**

> **输入:** N = 1
> **输出:** 4
> **说明:**
> 4 是最大的 1 位数八进制数，也是完美的平方
> **输入:** N = 2
> **输出:** 61
> **说明:**
> 49 是最大的数，是 2 位数八进制数，也是完美的平方。
> 因此八进制 49 = 61

**逼近:**
可以观察到，八进制中也是正方的最大数级数是:

> 4, 61, 744, 7601, 77771, 776001 …..

正如我们所知，当一个数大于 8 <sup>k</sup> 时，八进制中的位数增加，其中 k 表示数中的位数。所以对于八进制数字系统中的任何 N 位数，都必须小于 8 <sup>N+1</sup> 的值。因此，利用这一观察可以得出的一般术语是–

> N 位八进制数=八进制(幂(ceil(sqrt(幂(8，N))) -1，2))

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to find the maximum
// N-digit octal number which is perfect square

#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal number
// to a octal number
void decToOctal(int n)
{

    // Array to store octal number
    int octalNum[100];

    // Counter for octal number array
    int i = 0;
    while (n != 0) {

        // Store remainder in
        // octal array
        octalNum[i] = n % 8;
        n = n / 8;
        i++;
    }

    // Print octal number array
    // in reverse order
    for (int j = i - 1; j >= 0; j--)
        cout << octalNum[j];
    cout << "\n";
}

void nDigitPerfectSquares(int n)
{
    // Largest n-digit perfect square
    int decimal = pow(
        ceil(sqrt(pow(8, n))) - 1, 2
        );
    decToOctal(decimal);
}

// Driver Code
int main()
{
    int n = 2;
    nDigitPerfectSquares(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the maximum
// N-digit octal number which is perfect square
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

    // Function to convert decimal number
    // to a octal number
    static void decToOctal(int n)
    {

        // Array to store octal number
        int octalNum[] = new int[100];

        // Counter for octal number array
        int i = 0;
        while (n != 0)
        {

            // Store remainder in
            // octal array
            octalNum[i] = n % 8;
            n = n / 8;
            i++;
        }

        // Print octal number array
        // in reverse order
        for (int j = i - 1; j >= 0; j--)
            System.out.print(octalNum[j]);
        System.out.println("\n");
    }

    static void nDigitPerfectSquares(int n)
    {
        // Largest n-digit perfect square
        int decimal = (int) Math.pow(Math.ceil(Math.sqrt(Math.pow(8, n))) - 1, 2);
        decToOctal(decimal);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2;
        nDigitPerfectSquares(n);
    }
}

// This code is contributed by nidhiva
```

## 蟒蛇 3

```
# Python3 implementation to find the maximum
# N-digit octal number which is perfect square
from math import sqrt,ceil

# Function to convert decimal number
# to a octal number
def decToOctal(n) :

    # Array to store octal number
    octalNum = [0]*100;

    # Counter for octal number array
    i = 0;
    while (n != 0) :

        # Store remainder in
        # octal array
        octalNum[i] = n % 8;
        n = n // 8;
        i += 1;

    # Print octal number array
    # in reverse order
    for j in range(i - 1, -1, -1) :
        print(octalNum[j], end= "");
    print();

def nDigitPerfectSquares(n) :

    # Largest n-digit perfect square
    decimal = pow(ceil(sqrt(pow(8, n))) - 1, 2);
    decToOctal(decimal);

# Driver Code
if __name__ == "__main__" :

    n = 2;
    nDigitPerfectSquares(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the maximum
// N-digit octal number which is perfect square
using System;

class GFG
{

    // Function to convert decimal number
    // to a octal number
    static void decToOctal(int n)
    {

        // Array to store octal number
        int []octalNum = new int[100];

        // Counter for octal number array
        int i = 0;
        while (n != 0)
        {

            // Store remainder in
            // octal array
            octalNum[i] = n % 8;
            n = n / 8;
            i++;
        }

        // Print octal number array
        // in reverse order
        for (int j = i - 1; j >= 0; j--)
            Console.Write(octalNum[j]);
    Console.WriteLine();
    }

    static void nDigitPerfectSquares(int n)
    {
        // Largest n-digit perfect square
        int _decimal = (int) Math.Pow(Math.Ceiling(Math.Sqrt(Math.Pow(8, n))) - 1, 2);
        decToOctal(_decimal);
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        nDigitPerfectSquares(n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation to find the maximum
// N-digit octal number which is perfect square

// Function to convert decimal number
// to a octal number
function decToOctal(n)
{

    // Array to store octal number
    var octalNum = Array(100).fill(0);

    // Counter for octal number array
    var i = 0;
    while (n != 0) {

        // Store remainder in
        // octal array
        octalNum[i] = n % 8;
        n = parseInt(n / 8);
        i++;
    }

    // Print octal number array
    // in reverse order
    for (var j = i - 1; j >= 0; j--)
        document.write(octalNum[j]);
    document.write("<br>");
}

function nDigitPerfectSquares(n)
{
    // Largest n-digit perfect square
    var decimal = Math.pow(
        Math.ceil(Math.sqrt(Math.pow(8, n))) - 1, 2
        );
    decToOctal(decimal);
}

// Driver Code
var n = 2;
nDigitPerfectSquares(n);

</script>
```

**Output:** 

```
61
```