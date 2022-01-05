# 将 BCD 数转换为十进制数的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-BCD-number-to-decimal-number/](https://www.geeksforgeeks.org/program-to-convert-bcd-number-into-decimal-number/)

给定一个 [BCD](https://en.wikipedia.org/wiki/Binary-coded_decimal) (二进制编码十进制)数，任务是将 BCD 数转换成其等价的**十进制数**。

**示例:**

> **输入:** BCD = 100000101000
> **输出:** 828
> **解释:**
> 将数字分成 4 的组块，就变成了**10000001000**。
> 此处 **1000** 相当于**8**
> **0010**相当于 **2** 。
> 于是，这个数字变成了 **828** 。
> 
> **输入:** BCD = 1001000
> **输出:** 48
> **解释:**
> 将数字分成 4 的组块，就变成了 **0100 1000** 。
> 这里 **0100** 相当于**4**
> **1000**相当于 **8** 。
> 于是，这个数字变成了 **48** 。

**进场:**

1.  迭代给定 BCD 号中的所有位。
2.  将给定的 BCD 数分成 4 块，开始计算其等价的**十进制数**。
3.  将这个数字存储在名为 **sum** 的变量中。
4.  从变量 **num** 中存储在总和中的数字开始构建一个数字。
5.  反转到目前为止形成的数字并返回该数字。

下面是上述方法的实现。

## C++

```
// C++ code to convert BCD to its
// decimal number(base 10).

// Including Header Files
#include <bits/stdc++.h>
using namespace std;

// Function to convert BCD to Decimal
int bcdToDecimal(string s)
{
    int len = s.length(),
        check = 0, check0 = 0;
    int num = 0, sum = 0,
        mul = 1, rev = 0;

    // Iterating through the bits backwards
    for (int i = len - 1; i >= 0; i--) {

        // Forming the equivalent
        // digit(0 to 9)
        // from the group of 4.
        sum += (s[i] - '0') * mul;
        mul *= 2;
        check++;

        // Reinitialize all variables
        // and compute the number.
        if (check == 4 || i == 0) {
            if (sum == 0 && check0 == 0) {
                num = 1;
                check0 = 1;
            }
            else {
                // update the answer
                num = num * 10 + sum;
            }

            check = 0;
            sum = 0;
            mul = 1;
        }
    }

    // Reverse the number formed.
    while (num > 0) {
        rev = rev * 10 + (num % 10);
        num /= 10;
    }

    if (check0 == 1)
        return rev - 1;

    return rev;
}

// Driver Code
int main()
{
    string s = "100000101000";

    // Function Call
    cout << bcdToDecimal(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert BCD to its
// decimal number(base 10).
// Including Header Files
import java.io.*;
import java.util.*;

class GFG {

// Function to convert BCD to Decimal
public static int bcdToDecimal(String s)
{
    int len = s.length();
    int check = 0, check0 = 0;
    int num = 0, sum = 0;
    int mul = 1, rev = 0;

    // Iterating through the bits backwards
    for(int i = len - 1; i >= 0; i--)
    {

       // Forming the equivalent
       // digit(0 to 9)
       // from the group of 4.
       sum += (s.charAt(i) - '0') * mul;
       mul *= 2;
       check++;

       // Reinitialize all variables
       // and compute the number.
       if (check == 4 || i == 0)
       {
           if (sum == 0 && check0 == 0)
           {
               num = 1;
               check0 = 1;
           }
           else
           {

               // Update the answer
               num = num * 10 + sum;
           }

           check = 0;
           sum = 0;
           mul = 1;
       }
    }

    // Reverse the number formed.
    while (num > 0)
    {
        rev = rev * 10 + (num % 10);
        num /= 10;
    }

    if (check0 == 1)
        return rev - 1;

    return rev;
}

// Driver code
public static void main(String[] args)
{
    String s = "100000101000";

    // Function Call
    System.out.println(bcdToDecimal(s));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 code to convert BCD to its
# decimal number(base 10).

# Function to convert BCD to Decimal
def bcdToDecimal(s):

    length = len(s);
    check = 0;
    check0 = 0;
    num = 0;
    sum = 0;
    mul = 1;
    rev = 0;

    # Iterating through the bits backwards
    for i in range(length - 1, -1, -1):

        # Forming the equivalent
        # digit(0 to 9)
        # from the group of 4.
        sum += (ord(s[i]) - ord('0')) * mul;
        mul *= 2;
        check += 1;

        # Reinitialize all variables
        # and compute the number
        if (check == 4 or i == 0):
            if (sum == 0 and check0 == 0):
                num = 1;
                check0 = 1;

            else:

                # Update the answer
                num = num * 10 + sum;

            check = 0;
            sum = 0;
            mul = 1;

    # Reverse the number formed.
    while (num > 0):
        rev = rev * 10 + (num % 10);
        num //= 10;

    if (check0 == 1):
        return rev - 1;

    return rev;

# Driver Code
if __name__ == "__main__":

    s = "100000101000";

    # Function Call
    print(bcdToDecimal(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# code to convert BCD to its
// decimal number(base 10).
// Including Header Files
using System;

class GFG
{

// Function to convert BCD to Decimal
public static int bcdToDecimal(String s)
{
    int len = s.Length;
    int check = 0, check0 = 0;
    int num = 0, sum = 0;
    int mul = 1, rev = 0;

    // Iterating through the bits backwards
    for(int i = len - 1; i >= 0; i--)
    {

        // Forming the equivalent
        // digit(0 to 9)
        // from the group of 4.
        sum += (s[i] - '0') * mul;
        mul *= 2;
        check++;

        // Reinitialize all variables
        // and compute the number.
        if (check == 4 || i == 0)
        {
            if (sum == 0 && check0 == 0)
            {
                num = 1;
                check0 = 1;
            }
            else
            {

                // Update the answer
                num = num * 10 + sum;
            }

            check = 0;
            sum = 0;
            mul = 1;
        }
    }

    // Reverse the number formed.
    while (num > 0)
    {
        rev = rev * 10 + (num % 10);
        num /= 10;
    }

    if (check0 == 1)
        return rev - 1;

    return rev;
}

// Driver code
public static void Main(String[] args)
{
    String s = "100000101000";

    // Function Call
    Console.WriteLine(bcdToDecimal(s));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript code to convert BCD to its
// decimal number(base 10).
// Including Header Files

// Function to convert BCD to Decimal
function bcdToDecimal(s)
{
    let len = s.length;
    let check = 0, check0 = 0;
    let num = 0, sum = 0;
    let mul = 1, rev = 0;

    // Iterating through the bits backwards
    for(let i = len - 1; i >= 0; i--)
    {

       // Forming the equivalent
       // digit(0 to 9)
       // from the group of 4.
       sum += (s[i] - '0') * mul;
       mul *= 2;
       check++;

       // Reinitialize all variables
       // and compute the number.
       if (check == 4 || i == 0)
       {
           if (sum == 0 && check0 == 0)
           {
               num = 1;
               check0 = 1;
           }
           else
           {

               // Update the answer
               num = num * 10 + sum;
           }

           check = 0;
           sum = 0;
           mul = 1;
       }
    }

    // Reverse the number formed.
    while (num > 0)
    {
        rev = rev * 10 + (num % 10);
        num = Math.floor(num / 10);
    }

    if (check0 == 1)
        return rev - 1;

    return rev;
}

// Driver Code

    let s = "100000101000";

    // Function Call
    document.write(bcdToDecimal(s.split('')));

</script>
```

**Output:** 

```
828
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(1)*