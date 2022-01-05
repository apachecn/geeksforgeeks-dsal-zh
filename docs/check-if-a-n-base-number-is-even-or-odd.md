# 检查一个 N 基数是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-if-a-n-base-number-是偶数还是奇数/](https://www.geeksforgeeks.org/check-if-a-n-base-number-is-even-or-odd/)

给定基数 **N** 中的数字 **num** ，检查是偶数还是奇数。
**例:**

```
Input: num = 10, N = 8
Output: Even
Explanation:
108 = 810, which is even

Input: num = 122, N = 5 
Output: Odd
Explanation:
1225 = 3710, which is odd
```

**进场:**

*   将数字编号[从基数 N 转换为十进制基数](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)。
*   [检查数字是奇数还是偶数。](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)用 2 除，检查余数，很容易检查出来。

下面是上述方法的实现。

## C++

```
// C++ code to check if a Octal
// number is Even or Odd
#include <iostream>
using namespace std;

    // To return value of a char.
    int val(char c)
    {
        if (c >= '0' && c <= '9')
            return (int)c - '0';
        else
            return (int)c - 'A' + 10;
    }

    // Function to convert a
    // number from N base to decimal
    int toDeci(string str,
                      int base)
    {
        int len = str.length();

        // power of base
        int power = 1;

        int num = 0;
        int i;

        // Decimal equivalent is
        // str[len-1]*1 + str[len-1] *
        // base + str[len-1]*(base^2) + ...
        for (i = len - 1; i >= 0; i--) {

            // A digit in input number
            // must be less than
            // number's base
            if (val(str[i]) >= base) {

                cout << "Invalid Number";
                return -1;
            }

            num += val(str[i])* power;
            power = power * base;
        }

        return num;
    }

    // Returns true if n is even, else odd
     bool isEven(string num, int N)
    {

        int deci = toDeci(num, N);

        return (deci % 2 == 0);
    }

int main()
{
        string num = "11A";
        int N = 16;

        if (isEven(num, N)) {
            cout << "Even";
        }
        else {
            cout << "Odd";
        }
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a Octal
// number is Even or Odd

import java.io.*;

class Main {

    // To return value of a char.
    static int val(char c)
    {
        if (c >= '0' && c <= '9')
            return (int)c - '0';
        else
            return (int)c - 'A' + 10;
    }

    // Function to convert a
    // number from N base to decimal
    static int toDeci(String str,
                      int base)
    {
        int len = str.length();

        // power of base
        int power = 1;

        int num = 0;
        int i;

        // Decimal equivalent is
        // str[len-1]*1 + str[len-1] *
        // base + str[len-1]*(base^2) + ...
        for (i = len - 1; i >= 0; i--) {

            // A digit in input number
            // must be less than
            // number's base
            if (val(str.charAt(i)) >= base) {

                System.out.println("Invalid Number");
                return -1;
            }

            num += val(str.charAt(i))
                   * power;
            power = power * base;
        }

        return num;
    }

    // Returns true if n is even, else odd
    public static boolean isEven(
        String num, int N)
    {

        int deci = toDeci(num, N);

        return (deci % 2 == 0);
    }

    // Driver code
    public static void main(String[] args)
    {
        String num = "11A";
        int N = 16;

        if (isEven(num, N)) {
            System.out.println("Even");
        }
        else {
            System.out.println("Odd");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 code to check if a Octal
# number is Even or Odd

# To return value of a char.
def val(c):
    if (ord(c) >= ord('0') and ord(c) <= ord('9')):
        return ord(c) - ord('0')
    else:
        return ord(c) - ord('A') + 10

# Function to convert a
# number from N base to decimal
def toDeci(str, base):
    Len = len(str)

    # power of base
    power = 1

    num = 0

    # Decimal equivaLent is
    # str[Len-1]*1 + str[Len-1] *
    # base + str[Len-1]*(base^2) + ...
    for i in range(Len-1, -1, -1):

        # A digit in input number
        # must be less than
        # number's base
        if (val(str[i]) >= base):

            print("Invalid Number")
            return -1

        num += val(str[i])*power
        power = power * base

    return num

# Returns true if n is even, else odd
def isEven(num, N):

    deci = toDeci(num, N)

    return (deci % 2 == 0)

# Driver code
if __name__ == '__main__':
    num = "11A"
    N = 16

    if (isEven(num, N)):
        print("Even")
    else:
        print("Odd")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code to check if a Octal
// number is Even or Odd
using System;

class Gfg{

    // To return value of a char.
    static int val(char c)
    {
        if (c >= '0' && c <= '9')
            return (int)c - '0';
        else
            return (int)c - 'A' + 10;
    }

    // Function to convert a
    // number from N base to decimal
    static int toDeci(string str,int base_var)
    {
        int len = str.Length;

        // power of base
        int power = 1;

        int num = 0;
        int i;

        // Decimal equivalent is
        // str[len-1]*1 + str[len-1] *
        // base + str[len-1]*(base^2) + ...
        for (i = len - 1; i >= 0; i--) {

            // A digit in input number
            // must be less than
            // number's base
            if (val(str[i]) >= base_var) {

                Console.WriteLine("Invalid Number");
                return -1;
            }

            num += val(str[i])
                   * power;
            power = power * base_var;
        }

        return num;
    }

    // Returns true if n is even, else odd
    public static bool isEven(
        string num, int N)
    {

        int deci = toDeci(num, N);

        return (deci % 2 == 0);
    }

    // Driver code
    public static void Main(string[] args)
    {
        string num = "11A";
        int N = 16;

        if (isEven(num, N)) {
            Console.WriteLine("Even");
        }
        else {
            Console.WriteLine("Odd");
        }
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript code to check if a Octal
// number is Even or Odd

   // To return value of a char.
    function val(c)
    {
        if (c >= '0' && c <= '9')
            return c.charCodeAt() - '0'.charCodeAt();
        else
            return c.charCodeAt() - 'A'.charCodeAt() + 10;
    }

    // Function to convert a
    // number from N base to decimal
    function toDeci(str, base)
    {
        let len = str.length;

        // power of base
        let power = 1;

        let num = 0;
        let i;

        // Decimal equivalent is
        // str[len-1]*1 + str[len-1] *
        // base + str[len-1]*(base^2) + ...
        for (i = len - 1; i >= 0; i--) {

            // A digit in input number
            // must be less than
            // number's base
            if (val(str[i]) >= base) {

                 document.write("Invalid Number");
                return -1;
            }

            num += val(str[i])
                   * power;
            power = power * base;
        }

        return num;
    }

    // Returns true if n is even, else odd
    function isEven(num, N)
    {

        let deci = toDeci(num, N);

        return (deci % 2 == 0);
    }

// Driver Code

    let num = "11A";
        let N = 16;

        if (isEven(num, N)) {
            document.write("Even");
        }
        else {
            document.write("Odd");
        }

</script>
```

**Output:** 

```
Even
```

时间复杂度:0

辅助空间:0(1)