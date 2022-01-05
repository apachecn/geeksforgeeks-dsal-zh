# 将六进制数转换为其等效 BCD 的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-hexa-decimal-number-to-it-等价物-bcd/](https://www.geeksforgeeks.org/program-to-convert-hexa-decimal-number-to-its-equivalent-bcd/)

给定一个[十六进制数](https://www.geeksforgeeks.org/check-if-a-hexadecimal-number-is-even-or-odd/) **N** ，任务是将该数转换为其等价的[二进制编码十进制](https://www.geeksforgeeks.org/bcd-to-7-segment-decoder/)。
**举例:**

> **输入:** 11F
> **输出:** 0001 0001 1111
> **解释:**
> 1–0001 的二进制数
> F–1111 的二进制数
> 因此，等效 BCD 为 0001 0001 1111
> **输入:** A D
> **输出:** 1010 1101 【T17

**方法:**想法是迭代给定的六进制数的每个数字，并找到该数字的四位[二进制等价物](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)。最后，逐一打印所有转换后的数字。
以下是上述方法的实施:

## C++

```
// C++ implementation  to convert the given
// HexaDecimal number to its equivalent BCD.

#include <bits/stdc++.h>
using namespace std;

// Function to convert
// HexaDecimal to its BCD
void HexaDecimaltoBCD(string s)
{
    int len = s.length(), check = 0;
    int num = 0, sum = 0, mul = 1;

    // Iterating through the digits
    for (int i = 0; i <= len - 1; i++) {

        // check whether s[i] is a character
        // or a integer between 0 to 9
        // and compute its equivalent BCD
        if (s[i] >= 47 && s[i] <= 52)
            cout << bitset<4>(s[i])
                 << " ";
        else
            cout << bitset<4>(s[i] - 55)
                 << " ";
    }
}

// Driver Code
int main()
{
    string s = "11F";

    // Function Call
    HexaDecimaltoBCD(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation  to convert the given
// HexaDecimal number to its equivalent BCD.
public class Main
{
    // Function to convert
    // HexaDecimal to its BCD
    public static void HexaDecimaltoBCD(String s)
    {
        int len = s.length(), check = 0;
        int num = 0, sum = 0, mul = 1;

        // Iterating through the digits
        for (int i = 0; i <= len - 1; i++) {

            // check whether s[i] is a character
            // or a integer between 0 to 9
            // and compute its equivalent BCD
            if (s.charAt(i) >= 47 && s.charAt(i) <= 52)
            {
                String result = Integer.toBinaryString((int)s.charAt(i));
                System.out.print(result.substring(result.length() - 4) + " ");
            }
            else
            {
                String result = Integer.toBinaryString((int)s.charAt(i) - 55);
                System.out.print(result.substring(result.length() - 4) + " ");
            }
        }
    }

    public static void main(String[] args) {
        String s = "11F";

        // Function Call
        HexaDecimaltoBCD(s);
    }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program to convert the given
# HexaDecimal number to its equivalent BCD

# Function to convert
# Haxadecimal to BCD
def HexaDecimaltoBCD(str):

    # Iterating through the digits
    for i in range(len(str)):

        # Conversion into equivalent BCD
        print("{0:04b}".format(
              int(str[i], 16)), end = " ")

# Driver code
str = "11F"

# Function call
HexaDecimaltoBCD(str)

# This code is contributed by himanshu77
```

## C#

```
// C# implementation  to convert the given
// HexaDecimal number to its equivalent BCD.
using System;
class GFG {

    // Function to convert
    // HexaDecimal to its BCD
    static void HexaDecimaltoBCD(string s)
    {
        int len = s.Length;

        // Iterating through the digits
        for (int i = 0; i <= len - 1; i++) {

            // check whether s[i] is a character
            // or a integer between 0 to 9
            // and compute its equivalent BCD
            if (s[i] >= 47 && s[i] <= 52)
            {
                string result = Convert.ToString((int)s[i], 2);
                Console.Write(result.Substring(result.Length - 4) + " ");
            }
            else
            {
                string result = Convert.ToString((int)s[i] - 55, 2);
                Console.Write(result.Substring(result.Length - 4) + " ");
            }
        }
    }

  static void Main() {
        string s = "11F";

        // Function Call
        HexaDecimaltoBCD(s);
  }
}

// This code is contributed by diyeshrabadiya07
```

**Output:** 

```
0001 0001 1111
```