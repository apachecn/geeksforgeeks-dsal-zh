# 将给定的十进制数转换为其 BCD 表示

> 原文:[https://www . geesforgeks . org/convert-a-给定-十进制-number-it-BCD-presentation/](https://www.geeksforgeeks.org/convert-a-given-decimal-number-to-its-bcd-representation/)

给定一个十进制数 **N** ，任务是将 N 转换成它的[二进制编码十进制(BCD)](https://www.geeksforgeeks.org/code-converters-bcd8421-to-from-excess-3/) 形式。
**例:**

> **输入:** N = 12
> **输出:** 0001 0000
> **解释:**
> 考虑 4 位概念:
> 二进制 1 为 **0001** ，二进制 2 为 **0010** 。
> 所以它的等价 BCD 是 0001 0010。
> **输入:** N = 10
> **输出:** 0001 0000
> **解释:**
> 考虑 4 位概念:二进制中的
> 1 为 **0001** ，二进制中的 0 为 **0000** 。
> 所以相当于 BCD 是 0001 0000。

**进场:**

1.  使用本文中讨论的方法反转给定号码 **N** 的数字，并将该号码存储在 **Rev** 中。
2.  提取 **Rev** 的数字，并使用[位组](https://www.geeksforgeeks.org/c-bitset-and-its-application/)打印该数字的二进制形式。
3.  对 **Rev** 中的每个数字重复上述步骤。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert Decimal to BCD
void BCDConversion(int n)
{
    // Base Case
    if (n == 0) {
        cout << "0000";
        return;
    }

    // To store the reverse of n
    int rev = 0;

    // Reversing the digits
    while (n > 0) {
        rev = rev * 10 + (n % 10);
        n /= 10;
    }

    // Iterate through all digits in rev
    while (rev > 0) {

        // Find Binary for each digit
        // using bitset
        bitset<4> b(rev % 10);

        // Print the Binary conversion
        // for current digit
        cout << b << ' ';

        // Divide rev by 10 for next digit
        rev /= 10;
    }
}

// Driver Code
int main()
{
    // Given Number
    int N = 12;

    // Function Call
    BCDConversion(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class Gfg
{

    // Function to convert Decimal to BCD
    public static void BCDConversion(int n)
    {

        // Base Case
        if(n == 0)
        {
            System.out.print("0000");
        }

        // To store the reverse of n
        int rev = 0;

        // Reversing the digits
        while (n > 0)
        {
            rev = rev * 10 + (n % 10);
            n /= 10;
        }

        // Iterate through all digits in rev
        while(rev > 0)
        {

            // Find Binary for each digit
            // using bitset
            String b = Integer.toBinaryString(rev % 10);

            b = String.format("%04d", Integer.parseInt(b));

              // Print the Binary conversion
            // for current digit
            System.out.print(b + " ");

            // Divide rev by 10 for next digit
            rev /= 10;
        }
    }

  // Driver code
  public static void main(String []args)
  {

    // Given Number
    int N = 12;

    // Function Call
    BCDConversion(N);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to convert Decimal to BCD
def BCDConversion(n) :

    # Base Case
    if (n == 0) :
        print("0000")
        return

    # To store the reverse of n
    rev = 0

    # Reversing the digits
    while (n > 0) :
        rev = rev * 10 + (n % 10)
        n = n // 10

    # Iterate through all digits in rev
    while (rev > 0) :

        # Find Binary for each digit
        # using bitset
        b = str(rev % 10)

        # Print the Binary conversion
        # for current digit
        print("{0:04b}".format(int(b, 16)), end = " ")

        # Divide rev by 10 for next digit
        rev = rev // 10

# Given Number
N = 12

# Function Call
BCDConversion(N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to convert Decimal to BCD
    static void BCDConversion(int n)
    {
        // Base Case
        if (n == 0) {
            Console.Write("0000");
            return;
        }

        // To store the reverse of n
        int rev = 0;

        // Reversing the digits
        while (n > 0) {
            rev = rev * 10 + (n % 10);
            n /= 10;
        }

        // Iterate through all digits in rev
        while (rev > 0) {

            // Find Binary for each digit
            // using bitset
            string b = Convert.ToString(rev % 10, 2).PadLeft(4, '0');

            // Print the Binary conversion
            // for current digit
            Console.Write(b + " ");

            // Divide rev by 10 for next digit
            rev /= 10;
        }
    }

  static void Main() {

    // Given Number
    int N = 12;

    // Function Call
    BCDConversion(N);
  }
}

// This code is contributed divyesh072019
```

## java 描述语言

```
<script>

    //JavaScript for the above approach

    // Function to convert Decimal to BCD
    function BCDConversion(n)
    {
        // Base Case
        if (n == 0) {
            document.write("0000");
            return;
        }

        // To store the reverse of n
        let rev = 0;

        // Reversing the digits
        while (n > 0) {
            rev = rev * 10 + (n % 10);
            n = parseInt(n / 10, 10);
        }

        // Iterate through all digits in rev
        while (rev > 0) {

            // Find Binary for each digit
            // using bitset
            let b = (rev % 10).toString(2);
            while(b.length != 4)
            {
                b = "0" + b;
            }

            // Print the Binary conversion
            // for current digit
            document.write(b + " ");

            // Divide rev by 10 for next digit
            rev = parseInt(rev / 10, 10);
        }
    }

    // Driver Code
    // Given Number
    let N = 12;

    // Function Call
    BCDConversion(N);

</script>
```

**Output:** 

```
0001 0010
```

**时间复杂度:** *O(log <sub>10</sub> N)* ，其中 N 为给定数字。