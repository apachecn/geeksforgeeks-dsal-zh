# 将二进制分数转换为十进制

> 原文:[https://www . geesforgeks . org/convert-binary-fraction-decimal/](https://www.geeksforgeeks.org/convert-binary-fraction-decimal/)

给定一串二进制数 **n** 。将二进制小数 **n** 转换成它的十进制等价物。

**示例:**

```
Input: n = 110.101
Output: 6.625

Input: n = 101.1101
Output: 5.8125
```

We strongly recommend that you click here and practice it, before moving on to the solution.

以下是将二进制小数转换为十进制的步骤。

**A)将二进制的整数部分转换成等价的十进制**

1.  从基点左侧开始，将每个数字分别乘以 2 <sup>0</sup> 、2 <sup>1</sup> 、2 <sup>2</sup> 、…直到第一个数字。
2.  添加来自步骤 1 的所有结果。
3.  等效整数十进制数将是步骤 2 中获得的结果。

**B)将二进制的小数部分转换成等价的十进制**

1.  将每个数字从基点右侧一直到末端分别除以 2 <sup>1</sup> 、2 <sup>2</sup> 、2 <sup>3</sup> 、…。
2.  添加来自步骤 1 的所有结果。
3.  等效分数十进制数将是步骤 2 中获得的结果。

**C)将小数的整数部分和小数部分相加。**
**插图**

```
Let's take an example for n = 110.101

Step 1: Conversion of 110 to decimal
=> 1102 = (1*22) + (1*21) + (0*20)
=> 1102 = 4 + 2 + 0
=> 1102 = 6
*So equivalent decimal of binary integral is 6.*

Step 2: Conversion of .101 to decimal
=> 0.1012 = (1*1/2) + (0*1/22) + (1*1/23)
=> 0.1012 = 1*0.5 + 0*0.25 + 1*0.125
=> 0.1012 = 0.625
*So equivalent decimal of binary fractional is 0.625*

Step 3: Add result of step 1 and 2.
=> 6 + 0.625 = 6.625
```

## C++

```
// C++ program to demonstrate above steps of
// binary fractional to decimal conversion
#include<bits/stdc++.h>
using namespace std;

// Function to convert binary fractional to
// decimal
double binaryToDecimal(string binary, int len)
{
    // Fetch the radix point
    size_t point = binary.find('.');

    // Update point if not found
    if (point == string::npos)
        point = len;

    double intDecimal = 0, fracDecimal = 0, twos = 1;

    // Convert integral part of binary to decimal
    // equivalent
    for (int i = point-1; i>=0; --i)
    {
        // Subtract '0' to convert character
        // into integer
        intDecimal += (binary[i] - '0') * twos;
        twos *= 2;
    }

    // Convert fractional part of binary to
    // decimal equivalent
    twos = 2;
    for (int i = point+1; i < len; ++i)
    {
        fracDecimal += (binary[i] - '0') / twos;
        twos *= 2.0;
    }

    // Add both integral and fractional part
    return intDecimal + fracDecimal;
}

// Driver code
int main()
{
    string n = "110.101";
    cout << binaryToDecimal(n, n.length()) << "\n";

    n = "101.1101";
    cout << binaryToDecimal(n, n.length());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate above steps of
// binary fractional to decimal conversion
import java.io.*;

class GFG{

// Function to convert binary fractional to
// decimal
static double binaryToDecimal(String binary,
                              int len)
{

    // Fetch the radix point
    int point = binary.indexOf('.');

    // Update point if not found
    if (point == -1)
        point = len;

    double intDecimal = 0,
           fracDecimal = 0,
           twos = 1;

    // Convert integral part of binary to decimal
    // equivalent
    for(int i = point - 1; i >= 0; i--)
    {
        intDecimal += (binary.charAt(i) - '0') * twos;
        twos *= 2;
    }

    // Convert fractional part of binary to
    // decimal equivalent
    twos = 2;
    for(int i = point + 1; i < len; i++)
    {
        fracDecimal += (binary.charAt(i) - '0') / twos;
        twos *= 2.0;
    }

    // Add both integral and fractional part
    return intDecimal + fracDecimal;
}

// Driver Code
public static void main(String[] args)
{
    String n = "110.101";
    System.out.println(
        binaryToDecimal(n, n.length()));

    n = "101.1101";
    System.out.println(
        binaryToDecimal(n, n.length()));
}
}

// This code is contributed by dheeraj_2801
```

## 蟒蛇 3

```
# Python3 program to demonstrate above steps
# of binary fractional to decimal conversion

# Function to convert binary fractional 
# to decimal
def binaryToDecimal(binary, length) :

    # Fetch the radix point
    point = binary.find('.')

    # Update point if not found
    if (point == -1) :
        point = length

    intDecimal = 0
    fracDecimal = 0
    twos = 1

    # Convert integral part of binary
    # to decimal equivalent
    for i in range(point-1, -1, -1) :

        # Subtract '0' to convert
        # character into integer
        intDecimal += ((ord(binary[i]) -
                        ord('0')) * twos)
        twos *= 2

    # Convert fractional part of binary
    # to decimal equivalent
    twos = 2

    for i in range(point + 1, length):

        fracDecimal += ((ord(binary[i]) -
                         ord('0')) / twos);
        twos *= 2.0

    # Add both integral and fractional part
    ans = intDecimal + fracDecimal

    return ans

# Driver code :
if __name__ == "__main__" :
    n = "110.101"
    print(binaryToDecimal(n, len(n)))

    n = "101.1101"
    print(binaryToDecimal(n, len(n)))

# This code is contributed
# by aishwarya.27
```

## C#

```
// C# program to demonstrate above steps of
// binary fractional to decimal conversion
using System;

class GFG{

// Function to convert binary fractional to
// decimal
static double binaryToDecimal(string binary,
                              int len)
{

    // Fetch the radix point
    int point = binary.IndexOf('.');

    // Update point if not found
    if (point == -1)
        point = len;

    double intDecimal = 0, 
           fracDecimal = 0,
           twos = 1;

    // Convert integral part of binary to decimal
    // equivalent
    for(int i = point - 1; i >= 0; i--)
    {
        intDecimal += (binary[i] - '0') * twos;
        twos *= 2;
    }

    // Convert fractional part of binary to
    // decimal equivalent
    twos = 2;
    for(int i = point + 1; i < len; i++)
    {
        fracDecimal += (binary[i] - '0') / twos;
        twos *= 2.0;
    }

    // Add both integral and fractional part
    return intDecimal + fracDecimal;
}

// Driver Code
public static void Main(string[] args)
{
    string n = "110.101";
    Console.Write(
        binaryToDecimal(n, n.Length) + "\n");

    n = "101.1101";
    Console.Write(
        binaryToDecimal(n, n.Length));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
      // JavaScript program to demonstrate above steps of
      // binary fractional to decimal conversion
      // Function to convert binary fractional to
      // decimal
      function binaryToDecimal(binary, len) {
        // Fetch the radix point
        var point = binary.indexOf(".");

        // Update point if not found
        if (point === -1) point = len;

        var intDecimal = 0,
          fracDecimal = 0,
          twos = 1;

        // Convert integral part of binary to decimal
        // equivalent
        for (var i = point - 1; i >= 0; i--) {
          intDecimal += (binary[i] - "0") * twos;
          twos *= 2;
        }

        // Convert fractional part of binary to
        // decimal equivalent
        twos = 2;
        for (var i = point + 1; i < len; i++) {
          fracDecimal += (binary[i] - "0") / twos;
          twos *= 2.0;
        }

        // Add both integral and fractional part
        return intDecimal + fracDecimal;
      }

      // Driver Code
      var n = "110.101";
      document.write(binaryToDecimal(n, n.length) + "<br>");

      n = "101.1101";
      document.write(binaryToDecimal(n, n.length));
    </script>
```

**输出:**

```
6.625
5.8125
```

**时间复杂度:**O(len(n))
T3】辅助空间: O(len(n))

其中 len 是包含在 n 的二进制数中的总位数。

**见此:** [将十进制小数转换为二进制数。](https://www.geeksforgeeks.org/convert-decimal-fraction-binary-number/)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。