# 用字符串表示的大数平方

> 原文:[https://www . geeksforgeeks . org/大数平方表示为字符串/](https://www.geeksforgeeks.org/square-of-large-number-represented-as-string/)

给定一个非常大的数字，任务是编写一个程序来计算它的平方。

**示例:**

> **输入:**9999
> T3】输出:99980001
> 9999 * 9999 = 99980001
> 
> **输入:**45454545
> T3】输出:2066115661157025
> 45454545 * 45454545 45 = 2066115661157025

**天真的方法**:天真的方法是计算数字与自身相乘的平方。但是在 C++中，如果输入的是一个大数，那么得到的平方就会溢出。

**高效方法**:一种高效的方法是将数字存储为字符串，并对两个大数进行[乘法运算。](https://www.geeksforgeeks.org/multiply-large-numbers-represented-as-strings/)

下面是上述方法的实现:

## C++

```
// C++ program to multiply two numbers
// represented as strings.
#include <bits/stdc++.h>
using namespace std;

// Multiplies str1 and str2, and prints result.
string multiply(string num1, string num2)
{
    int n1 = num1.size();
    int n2 = num2.size();
    if (n1 == 0 || n2 == 0)
        return "0";

    // will keep the result number in vector
    // in reverse order
    vector<int> result(n1 + n2, 0);

    // Below two indexes are used to find positions
    // in result.
    int i_n1 = 0;
    int i_n2 = 0;

    // Go from right to left in num1
    for (int i = n1 - 1; i >= 0; i--) {
        int carry = 0;
        int n1 = num1[i] - '0';

        // To shift position to left after every
        // multiplication of a digit in num2
        i_n2 = 0;

        // Go from right to left in num2
        for (int j = n2 - 1; j >= 0; j--) {
            // Take current digit of second number
            int n2 = num2[j] - '0';

            // Multiply with current digit of first number
            // and add result to previously stored result
            // at current position.
            int sum = n1 * n2 + result[i_n1 + i_n2] + carry;

            // Carry for next iteration
            carry = sum / 10;

            // Store result
            result[i_n1 + i_n2] = sum % 10;

            i_n2++;
        }

        // store carry in next cell
        if (carry > 0)
            result[i_n1 + i_n2] += carry;

        // To shift position to left after every
        // multiplication of a digit in num1.
        i_n1++;
    }

    // ignore '0's from the right
    int i = result.size() - 1;
    while (i >= 0 && result[i] == 0)
        i--;

    // If all were '0's - means either both or
    // one of num1 or num2 were '0'
    if (i == -1)
        return "0";

    // generate the result string
    string s = "";

    while (i >= 0)
        s += std::to_string(result[i--]);

    return s;
}

// Driver code
int main()
{
    string str1 = "454545454545454545";

    cout << multiply(str1, str1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply two numbers
// represented as strings.

class GFG
{

    // Multiplies str1 and str2, and prints result.
    public static String multiply(String num1, String num2)
    {
        int n1 = num1.length();
        int n2 = num2.length();
        if (n1 == 0 || n2 == 0)
            return "0";

        // will keep the result number in vector
        // in reverse order
        int[] result = new int[n1 + n2];

        // Below two indexes are used to find positions
        // in result.
        int i_n1 = 0;
        int i_n2 = 0;

        // Go from right to left in num1
        for (int i = n1 - 1; i >= 0; i--)
        {
            int carry = 0;
            int n_1 = num1.charAt(i) - '0';

            // To shift position to left after every
            // multiplication of a digit in num2
            i_n2 = 0;

            // Go from right to left in num2
            for (int j = n2 - 1; j >= 0; j--)
            {

                // Take current digit of second number
                int n_2 = num2.charAt(j) - '0';

                // Multiply with current digit of first number
                // and add result to previously stored result
                // at current position.
                int sum = n_1 * n_2 + result[i_n1 + i_n2] + carry;

                // Carry for next iteration
                carry = sum / 10;

                // Store result
                result[i_n1 + i_n2] = sum % 10;

                i_n2++;
            }

            // store carry in next cell
            if (carry > 0)
                result[i_n1 + i_n2] += carry;

            // To shift position to left after every
            // multiplication of a digit in num1.
            i_n1++;
        }

        // ignore '0's from the right
        int i = result.length - 1;
        while (i >= 0 && result[i] == 0)
            i--;

        // If all were '0's - means either both or
        // one of num1 or num2 were '0'
        if (i == -1)
            return "0";

        // generate the result string
        String s = "";
        while (i >= 0)
            s += Integer.toString(result[i--]);

        return s;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str1 = "454545454545454545";
        System.out.println(multiply(str1, str1));

    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to multiply two numbers
# represented as strings.

# Multiplies str1 and str2, and prints result.
def multiply(num1, num2):

    n1 = len(num1)
    n2 = len(num2)

    if (n1 == 0 or n2 == 0):
        return "0"

    # Will keep the result number in vector
    # in reverse order
    result = [0] * (n1 + n2)

    # Below two indexes are used to
    # find positions in result.
    i_n1 = 0
    i_n2 = 0

    # Go from right to left in num1
    for i in range(n1 - 1, -1, -1):
        carry = 0
        n_1 = ord(num1[i]) - ord('0')

        # To shift position to left after every
        # multiplication of a digit in num2
        i_n2 = 0

        # Go from right to left in num2
        for j in range(n2 - 1, -1, -1):

            # Take current digit of second number
            n_2 = ord(num2[j]) - ord('0')

            # Multiply with current digit of first number
            # and add result to previously stored result
            # at current position.
            sum = n_1 * n_2 + result[i_n1 + i_n2] + carry

            # Carry for next iteration
            carry = sum // 10

            # Store result
            result[i_n1 + i_n2] = sum % 10

            i_n2 += 1

        # Store carry in next cell
        if (carry > 0):
            result[i_n1 + i_n2] += carry

        # To shift position to left after every
        # multiplication of a digit in num1.
        i_n1 += 1

    # Ignore '0's from the right
    i = len(result) - 1

    while (i >= 0 and result[i] == 0):
        i -= 1

    # If all were '0's - means either both or
    # one of num1 or num2 were '0'
    if (i == -1):
        return "0"

    # Generate the result string
    s = ""

    while (i >= 0):
        s += str(result[i])
        i -= 1

    return s

# Driver code
if __name__ == "__main__":

    str1 = "454545454545454545"

    print(multiply(str1, str1))

# This code is contributed by chitranayal
```

## C#

```
// C# program to multiply two numbers
// represented as strings.
using System;
using System.Collections.Generic;

class GFG
{

    // Multiplies str1 and str2,
    // and prints result.
    public static String multiply(String num1,
                                  String num2)
    {
        int n1 = num1.Length;
        int n2 = num2.Length;
        if (n1 == 0 || n2 == 0)
            return "0";

        // will keep the result number in vector
        // in reverse order
        int[] result = new int[n1 + n2];

        // Below two indexes are used to
        // find positions in result.
        int i_n1 = 0;
        int i_n2 = 0;
        int i = 0;

        // Go from right to left in num1
        for (i = n1 - 1; i >= 0; i--)
        {
            int carry = 0;
            int n_1 = num1[i] - '0';

            // To shift position to left after every
            // multiplication of a digit in num2
            i_n2 = 0;

            // Go from right to left in num2
            for (int j = n2 - 1; j >= 0; j--)
            {

                // Take current digit of second number
                int n_2 = num2[j] - '0';

                // Multiply with current digit of first number
                // and add result to previously stored result
                // at current position.
                int sum = n_1 * n_2 +
                          result[i_n1 + i_n2] + carry;

                // Carry for next iteration
                carry = sum / 10;

                // Store result
                result[i_n1 + i_n2] = sum % 10;

                i_n2++;
            }

            // store carry in next cell
            if (carry > 0)
                result[i_n1 + i_n2] += carry;

            // To shift position to left after every
            // multiplication of a digit in num1.
            i_n1++;
        }

        // ignore '0's from the right
        i = result.Length - 1;
        while (i >= 0 && result[i] == 0)
            i--;

        // If all were '0's - means either both or
        // one of num1 or num2 were '0'
        if (i == -1)
            return "0";

        // generate the result string
        String s = "";
        while (i >= 0)
            s += (result[i--]).ToString();

        return s;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str1 = "454545454545454545";
        Console.WriteLine(multiply(str1, str1));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to multiply two numbers
// represented as strings.

    // Multiplies str1 and str2, and prints result.
    function multiply(num1,num2)
    {
        let n1 = num1.length;
        let n2 = num2.length;
        if (n1 == 0 || n2 == 0)
            return "0";

        // will keep the result number in vector
        // in reverse order
        let result = new Array(n1 + n2);
         for(let i=0;i<result.length;i++)
        {
            result[i]=0;
        }
        // Below two indexes are used to find positions
        // in result.
        let i_n1 = 0;
        let i_n2 = 0;

        // Go from right to left in num1
        for (let i = n1 - 1; i >= 0; i--)
        {
            let carry = 0;
            let n_1 = num1[i].charCodeAt(0) - '0'.charCodeAt(0);

            // To shift position to left after every
            // multiplication of a digit in num2
            i_n2 = 0;

            // Go from right to left in num2
            for (let j = n2 - 1; j >= 0; j--)
            {

                // Take current digit of second number
                let n_2 = num2[j].charCodeAt(0) - '0'.charCodeAt(0);

                // Multiply with current digit of first number
                // and add result to previously stored result
                // at current position.
                let sum = n_1 * n_2 + result[i_n1 + i_n2] + carry;

                // Carry for next iteration
                carry = Math.floor(sum / 10);

                // Store result
                result[i_n1 + i_n2] = sum % 10;

                i_n2++;
            }

            // store carry in next cell
            if (carry > 0)
                result[i_n1 + i_n2] += carry;

            // To shift position to left after every
            // multiplication of a digit in num1.
            i_n1++;
        }

        // ignore '0's from the right
        let i = result.length - 1;
        while (i >= 0 && result[i] == 0)
            i--;

        // If all were '0's - means either both or
        // one of num1 or num2 were '0'
        if (i == -1)
            return "0";

        // generate the result string
        let s = "";
        while (i >= 0)
            s += (result[i--]).toString();

        return s;
    }

    // Driver code
    let str1 = "454545454545454545";
    document.write(multiply(str1, str1));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
206611570247933883884297520661157025
```