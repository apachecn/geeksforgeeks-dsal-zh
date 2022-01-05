# 生成 n 位格雷码|设置 2

> 原文:[https://www . geesforgeks . org/generate-n-bit-gray-codes-set-2/](https://www.geeksforgeeks.org/generate-n-bit-gray-codes-set-2/)

给定数字 n，生成从 0 到 2^n-1 的位模式，使得连续的模式相差一位。

**示例:**

> **输入:** n=2
> **输出:** 00 01 11 10
> **解释:**
> 格雷码的每个相邻元素只相差一位。所以 n 位格雷码是:00 01 11 10
> 
> **输入:** n=3
> **输出:**000 001 011 010 110 111 101 100
> **解释:**
> 格雷码的每个相邻元素只相差一位。所以 n 位格雷码是:000 001 011 010 110 111 101 100

[生成 n 位格雷码](https://www.geeksforgeeks.org/given-a-number-n-generate-bit-patterns-from-0-to-2n-1-so-that-successive-patterns-differ-by-one-bit/)的另一种方法已经讨论过了。

**<u>进场:</u>**
*思路是利用异或和右移运算得到二进制数的格雷码。*

1.  格雷码的第一位(MSB)与二进制数的第一位(MSB)相同。
2.  格雷码的第二位(从左侧开始)等于二进制数的第一位(MSB)和第二位(第二 MSB)的异或。
3.  格雷码的第三位(从左侧开始)等于第二位(第二 MSB)和第三位(第三 MSB)的异或，依此类推..

通过这种方式，可以为相应的二进制数计算格雷码。因此，可以观察到，第 I 个元素可以通过 I 和 floor(i/2)的按位异或形成，等于 I 和(i >> 1)的按位异或，即，I 右移 1。通过执行此操作，二进制数的 MSB 保持不变，所有其他位与其相邻的高位执行按位异或运算。

## C++

```
// C++ program to generate n-bit
// gray codes
#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal to binary
void decimalToBinaryNumber(int x, int n)
{
    int* binaryNumber = new int(x);
    int i = 0;
    while (x > 0) {
        binaryNumber[i] = x % 2;
        x = x / 2;
        i++;
    }

    // leftmost digits are filled with 0
    for (int j = 0; j < n - i; j++)
        cout << '0';

    for (int j = i - 1; j >= 0; j--)
        cout << binaryNumber[j];
}

// Function to generate gray code
void generateGrayarr(int n)
{
    int N = 1 << n;
    for (int i = 0; i < N; i++) {

        // generate gray code of corresponding
        // binary number of integer i.
        int x = i ^ (i >> 1);

        // printing gray code
        decimalToBinaryNumber(x, n);

        cout << endl;
    }
}

// Drivers code
int main()
{
    int n = 3;
    generateGrayarr(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate
// n-bit gray codes
import java.io.*;

class GFG {

    // Function to convert
    // decimal to binary
    static void decimalToBinaryNumber(int x,
                                      int n)
    {
        int[] binaryNumber = new int[x];
        int i = 0;
        while (x > 0) {
            binaryNumber[i] = x % 2;
            x = x / 2;
            i++;
        }

        // leftmost digits are
        // filled with 0
        for (int j = 0; j < n - i; j++)
            System.out.print('0');

        for (int j = i - 1;
             j >= 0; j--)
            System.out.print(binaryNumber[j]);
    }

    // Function to generate
    // gray code
    static void generateGrayarr(int n)
    {
        int N = 1 << n;
        for (int i = 0; i < N; i++) {

            // generate gray code of
            // corresponding binary
            // number of integer i.
            int x = i ^ (i >> 1);

            // printing gray code
            decimalToBinaryNumber(x, n);

            System.out.println();
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        generateGrayarr(n);
    }
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python program to generate
# n-bit gray codes

# Function to convert
# decimal to binary
def decimalToBinaryNumber(x, n):
    binaryNumber = [0]*x;
    i = 0;
    while (x > 0):
        binaryNumber[i] = x % 2;
        x = x // 2;
        i += 1;

    # leftmost digits are
    # filled with 0
    for j in range(0, n - i):
        print('0', end ="");

    for j in range(i - 1, -1, -1):
        print(binaryNumber[j], end ="");

# Function to generate
# gray code
def generateGrayarr(n):
    N = 1 << n;
    for i in range(N):

        # generate gray code of
        # corresponding binary
        # number of integer i.
        x = i ^ (i >> 1);

        # printing gray code
        decimalToBinaryNumber(x, n);

        print();

# Driver code
if __name__ == '__main__':
    n = 3;
    generateGrayarr(n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to generate
// n-bit gray codes
using System;

class GFG {

    // Function to convert
    // decimal to binary
    static void decimalToBinaryNumber(int x,
                                      int n)
    {
        int[] binaryNumber = new int[x];
        int i = 0;
        while (x > 0) {
            binaryNumber[i] = x % 2;
            x = x / 2;
            i++;
        }

        // leftmost digits are
        // filled with 0
        for (int j = 0; j < n - i; j++)
            Console.Write('0');

        for (int j = i - 1;
             j >= 0; j--)
            Console.Write(binaryNumber[j]);
    }

    // Function to generate
    // gray code
    static void generateGrayarr(int n)
    {
        int N = 1 << n;
        for (int i = 0; i < N; i++) {

            // Generate gray code of
            // corresponding binary
            // number of integer i.
            int x = i ^ (i >> 1);

            // printing gray code
            decimalToBinaryNumber(x, n);

            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        generateGrayarr(n);
    }
}

// This code is contributed
// by anuj_67.
```

## java 描述语言

```
<script>

// JavaScript program to generate n-bit
// gray codes

// Function to convert decimal to binary
function decimalToBinaryNumber(x, n)
{
    var binaryNumber = Array(x);
    var i = 0;
    while (x > 0) {
        binaryNumber[i] = x % 2;
        x = parseInt(x / 2);
        i++;
    }

    // leftmost digits are filled with 0
    for (var j = 0; j < n - i; j++)
        document.write('0');

    for (var j = i - 1; j >= 0; j--)
        document.write( binaryNumber[j]);
}

// Function to generate gray code
function generateGrayarr(n)
{
    var N = 1 << n;
    for (var i = 0; i < N; i++) {

        // generate gray code of corresponding
        // binary number of integer i.
        var x = i ^ (i >> 1);

        // printing gray code
        decimalToBinaryNumber(x, n);

        document.write("<br>");
    }
}

// Drivers code
var n = 3;
generateGrayarr(n);

</script>
```

**Output**

```
000
001
011
010
110
111
101
100
```

**复杂度分析:**

*   **时间复杂度:** O(2 <sup>n</sup> )。
    只需要一次从 0 到(2 <sup>n</sup> 的遍历。
*   **辅助空间:** O(log x)。
    对于(x)
    的二进制表示，需要(log x)的空间