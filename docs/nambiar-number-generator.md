# 南比亚尔数字发生器

> 原文:[https://www.geeksforgeeks.org/nambiar-number-generator/](https://www.geeksforgeeks.org/nambiar-number-generator/)

米（meter 的缩写））南比亚尔设计了一种机制来处理任何给定的数字，从而产生一个新的合成数字。他称这种机制为“南比亚尔数发生器”，由此产生的数被称为“南比亚尔数”。
**机制:**在给定的数字中，从第一个数字开始，继续加所有后续的数字，直到数字之和的状态(偶数或奇数)与第一个数字的状态(奇数或偶数)相反。从下一个数字开始，一直到数字的最后一个数字。将这些总和串联起来就产生了南比亚尔数。
**示例:**

> **输入:**N = 9880127431
> T3】输出: 26971
> 
> <figure class="table">
> 
> | 第一位数字 | 下一个有效的连续数字 | 结果数 |
> | --- | --- | --- |
> | **9** 880127431 | **98801** 27431 | Twenty-six |
> | 98801 **2** 7431 | 98801 **27** 431 | Two hundred and sixty-nine |
> | 9880127 **4** 31 | 9880127 **43** 1 | Two thousand six hundred and ninety-seven |
> | 988012743 **1** | 988012743 **1** | Twenty-six thousand nine hundred and seventy-one |
> 
> **输入:** N = 9866364552
> **输出:** 32157
> 
> </figure>

**方法:**对于左边第一个未使用的数字，检查它是偶数还是奇数。如果该数字为偶数，则从当前奇数数字开始计算连续数字的总和(如果第一个数字为奇数，则为偶数总和)。将此总和与结果数连接起来，并从左边第一个未使用的数字开始重复整个过程。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the Nambiar
// number of the given number
string numbiarNumber(string str, int i)
{
    // If there is no digit to choose
    if (i > str.length())
        return "";

    // Choose the first digit
    int firstDigit = str[i] - '0';

    // Chosen digit's parity
    int digitParity = firstDigit % 2;

    // To store the sum of the consecutive
    // digits starting from the chosen digit
    int sumDigits = 0;

    // While there are digits to choose
    while (i < str.length())
    {
        // Update the sum
        sumDigits += (str[i] - '0');
        int sumParity = sumDigits % 2;

        // If the parity differs
        if (digitParity != sumParity)
            break;
        i++;
    }

    // Return the current sum concatenated with the
    // Numbiar number for the rest of the string
    return (to_string(sumDigits) +
            numbiarNumber(str, i + 1));
}

// Driver code
int main()
{
    string str = "9880127431";
    cout << numbiarNumber(str, 0) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the Nambiar
    // number of the given number
    static String nambiarNumber(String str, int i)
    {

        // If there is no digit to choose
        if (i >= str.length())
            return "";

        // Choose the first digit
        int firstDigit = (str.charAt(i) - '0');

        // Chosen digit's parity
        int digitParity = firstDigit % 2;

        // To store the sum of the consecutive
        // digits starting from the chosen digit
        int sumDigits = 0;

        // While there are digits to choose
        while (i < str.length()) {

            // Update the sum
            sumDigits += (str.charAt(i) - '0');
            int sumParity = sumDigits % 2;

            // If the parity differs
            if (digitParity != sumParity) {
                break;
            }
            i++;
        }

        // Return the current sum concatenated with the
        // Numbiar number for the rest of the string
        return ("" + sumDigits + nambiarNumber(str, i + 1));
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "9880127431";
        System.out.println(nambiarNumber(str, 0));
    }
}
```

## 蟒蛇 3

```
# Java implementation of the approach

# Function to return the Nambiar
# number of the given number
def nambiarNumber(Str,i):

    # If there is no digit to choose
    if (i >= len(Str)):
        return ""

    # Choose the first digit
    firstDigit =ord(Str[i])-ord('0')

    # Chosen digit's parity
    digitParity = firstDigit % 2

    # To store the sum of the consecutive
    # digits starting from the chosen digit
    sumDigits = 0

    # While there are digits to choose
    while (i < len(Str)):

        # Update the sum
        sumDigits += (ord(Str[i]) - ord('0'))
        sumParity = sumDigits % 2

        # If the parity differs
        if (digitParity != sumParity):
            break
        i += 1

    # Return the current sum concatenated with the
    # Numbiar number for the rest of the String
    return ("" + str(sumDigits) +
                 nambiarNumber(Str, i + 1))

# Driver code
Str = "9880127431"
print(nambiarNumber(Str, 0))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach.
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the Nambiar
    // number of the given number
    static String nambiarNumber(String str, int i)
    {

        // If there is no digit to choose
        if (i >= str.Length)
            return "";

        // Choose the first digit
        int firstDigit = (str[i] - '0');

        // Chosen digit's parity
        int digitParity = firstDigit % 2;

        // To store the sum of the consecutive
        // digits starting from the chosen digit
        int sumDigits = 0;

        // While there are digits to choose
        while (i < str.Length)
        {

            // Update the sum
            sumDigits += (str[i] - '0');
            int sumParity = sumDigits % 2;

            // If the parity differs
            if (digitParity != sumParity)
            {
                break;
            }
            i++;
        }

        // Return the current sum concatenated with the
        // Numbiar number for the rest of the string
        return ("" + sumDigits + nambiarNumber(str, i + 1));
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "9880127431";
        Console.WriteLine(nambiarNumber(str, 0));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the Nambiar
    // number of the given number
function nambiarNumber(str,i)
{
    // If there is no digit to choose
        if (i >= str.length)
            return "";

        // Choose the first digit
        let firstDigit = (str[i].charCodeAt(0) - '0'.charCodeAt(0));

        // Chosen digit's parity
        let digitParity = firstDigit % 2;

        // To store the sum of the consecutive
        // digits starting from the chosen digit
        let sumDigits = 0;

        // While there are digits to choose
        while (i < str.length) {

            // Update the sum
            sumDigits += (str[i].charCodeAt(0) - '0'.charCodeAt(0));
            let sumParity = sumDigits % 2;

            // If the parity differs
            if (digitParity != sumParity) {
                break;
            }
            i++;
        }

        // Return the current sum concatenated with the
        // Numbiar number for the rest of the string
        return ("" + sumDigits + nambiarNumber(str, i + 1));
}

// Driver code
let str = "9880127431";
document.write(nambiarNumber(str, 0));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
26971
```