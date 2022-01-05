# 将给定数字四舍五入到 10 的最接近倍数| Set-2

> 原文:[https://www . geeksforgeeks . org/将给定数字四舍五入到最接近的 10 的倍数集-2/](https://www.geeksforgeeks.org/round-the-given-number-to-nearest-multiple-of-10-set-2/)

给定一个表示为字符串 **str** 的大正整数。任务是将这个数字四舍五入到 **10** 的最接近倍数。
**例:**

> **输入:**str = " 999999999999993 "
> T3】输出:99999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999

**方法:**同一问题的解决方案已经在[这篇](https://www.geeksforgeeks.org/round-the-given-number-to-nearest-multiple-of-10/)文章中讨论过了，它不适用于大数。当数字很大并表示为字符串时，我们可以一个数字一个数字地处理这个数字。主要观察的是，如果数字的最后一个数字是 **≤ 5** ，那么只有最后一个数字会受到影响，即被 **0** 代替。如果大于 **5** ，则该数字必须四舍五入到 **10** 的下一个更高倍数，即最后一个数字将被替换为 **0** 和 **1** 将被添加到该数字的其余部分，即由子串 **str[0…n-1]** 表示的数字，这可以通过存储每一步(数字)生成的进位来完成。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to round the given number
// to the nearest multiple of 10
void roundToNearest(string str, int n)
{

    // If string is empty
    if (str == "")
        return;

    // If the last digit is less then or equal to 5
    // then it can be rounded to the nearest
    // (previous) multiple of 10 by just replacing
    // the last digit with 0
    if (str[n - 1] - '0' <= 5) {

        // Set the last digit to 0
        str[n - 1] = '0';

        // Print the updated number
        cout << str.substr(0, n);
    }

    // The number hast to be rounded to
    // the next multiple of 10
    else {

        // To store the carry
        int carry = 0;

        // Replace the last digit with 0
        str[n - 1] = '0';

        // Starting from the second last digit, add 1
        // to digits while there is carry
        int i = n - 2;
        carry = 1;

        // While there are digits to consider
        // and there is carry to add
        while (i >= 0 && carry == 1) {

            // Get the current digit
            int currentDigit = str[i] - '0';

            // Add the carry
            currentDigit += carry;

            // If the digit exceeds 9 then
            // the carry will be generated
            if (currentDigit > 9) {
                carry = 1;
                currentDigit = 0;
            }

            // Else there will be no carry
            else
                carry = 0;

            // Update the current digit
            str[i] = (char)(currentDigit + '0');

            // Get to the previous digit
            i--;
        }

        // If the carry is still 1 then it must be
        // inserted at the beginning of the string
        if (carry == 1)
            cout << carry;

        // Print the rest of the number
        cout << str.substr(0, n);
    }
}

// Driver code
int main()
{
    string str = "99999999999999993";
    int n = str.length();

    roundToNearest(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to round the given number
// to the nearest multiple of 10
static void roundToNearest(StringBuilder str, int n)
{

    // If string is empty
    if (str.toString() == "")
        return;

    // If the last digit is less then or equal to 5
    // then it can be rounded to the nearest
    // (previous) multiple of 10 by just replacing
    // the last digit with 0
    if (str.charAt(n - 1) - '0' <= 5)
    {

        // Set the last digit to 0
        str.setCharAt(n - 1, '0');

        // Print the updated number
        System.out.print(str.substring(0, n));
    }

    // The number hast to be rounded to
    // the next multiple of 10
    else
    {

        // To store the carry
        int carry = 0;

        // Replace the last digit with 0
        str.setCharAt(n - 1, '0');

        // Starting from the second last digit,
        // add 1 to digits while there is carry
        int i = n - 2;
        carry = 1;

        // While there are digits to consider
        // and there is carry to add
        while (i >= 0 && carry == 1)
        {

            // Get the current digit
            int currentDigit = str.charAt(i) - '0';

            // Add the carry
            currentDigit += carry;

            // If the digit exceeds 9 then
            // the carry will be generated
            if (currentDigit > 9)
            {
                carry = 1;
                currentDigit = 0;
            }

            // Else there will be no carry
            else
                carry = 0;

            // Update the current digit
            str.setCharAt(i, (char)(currentDigit + '0'));

            // Get to the previous digit
            i--;
        }

        // If the carry is still 1 then it must be
        // inserted at the beginning of the string
        if (carry == 1)
            System.out.print(carry);

        // Print the rest of the number
        System.out.print(str.substring(0, n));
    }
}

// Driver code
public static void main(String[] args)
{
    StringBuilder str = new StringBuilder("99999999999999993");
    int n = str.length();
    roundToNearest(str, n);
}
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to round the given number
# to the nearest multiple of 10
def roundToNearest(str, n):

    # If string is empty
    if (str == ""):
        return

    # If the last digit is less then or equal to 5
    # then it can be rounded to the nearest
    # (previous) multiple of 10 by just replacing
    # the last digit with 0
    if (ord(str[n - 1]) - ord('0') <= 5):

        # Set the last digit to 0
        str = list(str)
        str[n - 1] = '0'
        str = ''.join(str)

        # Print the updated number
        print(str[0:n])

    # The number hast to be rounded to
    # the next multiple of 10
    else:

        # To store the carry
        carry = 0

        # Replace the last digit with 0
        str = list(str)
        str[n - 1] = '0'

        str = ''.join(str)

        # Starting from the second last digit,
        # add 1 to digits while there is carry
        i = n - 2
        carry = 1

        # While there are digits to consider
        # and there is carry to add
        while (i >= 0 and carry == 1):

            # Get the current digit
            currentDigit = ord(str[i]) - ord('0')

            # Add the carry
            currentDigit += carry

            # If the digit exceeds 9 then
            # the carry will be generated
            if (currentDigit > 9):
                carry = 1
                currentDigit = 0

            # Else there will be no carry
            else:
                carry = 0

            # Update the current digit
            str[i] = chr(currentDigit + '0')

            # Get to the previous digit
            i -= 1

        # If the carry is still 1 then it must be
        # inserted at the beginning of the string
        if (carry == 1):
            print(carry)

        # Print the rest of the number
        print(str[0:n])

# Driver code
if __name__ == '__main__':
    str = "99999999999999993"
    n = len(str)

    roundToNearest(str, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Text;

class GFG
{

// Function to round the given number
// to the nearest multiple of 10
static void roundToNearest(StringBuilder str, int n)
{

    // If string is empty
    if (str.ToString() == "")
        return;

    // If the last digit is less then or equal to 5
    // then it can be rounded to the nearest
    // (previous) multiple of 10 by just replacing
    // the last digit with 0
    if (str[n - 1] - '0' <= 5)
    {

        // Set the last digit to 0
        str[n - 1] = '0';

        // Print the updated number
        Console.Write(str.ToString().Substring(0, n));
    }

    // The number hast to be rounded to
    // the next multiple of 10
    else
    {

        // To store the carry
        int carry = 0;

        // Replace the last digit with 0
        str[n - 1] = '0';

        // Starting from the second last digit,
        // add 1 to digits while there is carry
        int i = n - 2;
        carry = 1;

        // While there are digits to consider
        // and there is carry to add
        while (i >= 0 && carry == 1)
        {

            // Get the current digit
            int currentDigit = str[i] - '0';

            // Add the carry
            currentDigit += carry;

            // If the digit exceeds 9 then
            // the carry will be generated
            if (currentDigit > 9)
            {
                carry = 1;
                currentDigit = 0;
            }

            // Else there will be no carry
            else
                carry = 0;

            // Update the current digit
            str[i] = (char)(currentDigit + '0');

            // Get to the previous digit
            i--;
        }

        // If the carry is still 1 then it must be
        // inserted at the beginning of the string
        if (carry == 1)
            Console.Write(carry);

        // Print the rest of the number
        Console.Write(str.ToString().Substring(0, n));
    }
}

// Driver code
public static void Main(String[] args)
{
    StringBuilder str = new StringBuilder("99999999999999993");
    int n = str.Length;
    roundToNearest(str, n);
}
}

// This code is contributed by
// Rajnis09
```

**Output:** 

```
99999999999999990
```