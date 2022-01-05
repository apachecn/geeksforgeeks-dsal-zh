# 给定基数的两个整数相加的程序

> 原文:[https://www . geeksforgeeks . org/给定基数的程序加二整数/](https://www.geeksforgeeks.org/program-to-add-two-integers-of-given-base/)

给定三个整数 **X** 、 **Y** 和 **B** ，其中 X 和 Y 是 Base-B 整数。任务是求整数 **X** 和 **Y** 的和。

**例:**

```
Input: X = 123, Y = 234, B = 6
Output: 401
Explanation:
Sum of two integers in base 6 - 
     1 1   
     1 2 3
+    2 3 4
-------------
     4 0 1

Input: X = 546, Y = 248 B = 9
Output: 805
Explanation:
Sum of two integers in base 9 - 
     1 1
     5 4 6
+    2 4 8
-------------
     8 0 5   
```

**方法:**其思想是利用这样一个事实，即每当数字的两位数相加时，位置值将是数字总和除以基数的模，而进位将是数字总和除以基数的整数除法。即

```
Let two digits of the number be D1 and D2 -
Place Value = (D1 + D2) % B

Carry = (D1 + D2) / B
```

同样，将最后一个数字的每一个数字相加，得到想要的结果。

下面是上述方法的实现:

## c++

```
// C++ implementation to find the
// sum of two integers of base B

#include <bits/stdc++.h>

using namespace std;

// Function to find the sum of
// two integers of base B
string sumBaseB(string a,
      string b, int base)
{
    int len_a, len_b;

    len_a = a.size();
    len_b = b.size();

    string sum, s;
    s = "";
    sum = "";

    int diff;
    diff = abs(len_a - len_b);

    // Padding 0 in front of the
    // number to make both numbers equal
    for (int i = 1; i <= diff; i++)
        s += "0";

    // Condition to check if the strings
    // have lengths mis-match
    if (len_a < len_b)
        a = s + a;
    else
        b = s + b;

    int curr, carry = 0;

    // Loop to find the find the sum
    // of two integers of base B
    for (int i = max(len_a, len_b) - 1;
                           i > -1; i--) {

        // Current Place value for
        // the resultant sum
        curr = carry + (a[i] - '0') +
                       (b[i] - '0');

        // Update carry
        carry = curr / base;

        // Find current digit
        curr = curr % base;

        // Update sum result
        sum = (char)(curr + '0') + sum;
    }
    if (carry > 0)
        sum = (char)(carry + '0') + sum;
    return sum;
}

// Driver Code
int main()
{
    string a, b, sum;
    int base;
    a = "123";
    b = "234";
    base = 6;

    // Function Call
    sum = sumBaseB(a, b, base);
    cout << sum << endl;
    return 0;
}
```

## Java

```
// Java implementation to find the
// sum of two integers of base B
class GFG {

    // Function to find the sum of
    // two integers of base B
    static String sumBaseB(String a, String b, int base)
    {
        int len_a, len_b;

        len_a = a.length();
        len_b = b.length();

        String sum, s;
        s = "";
        sum = "";

        int diff;
        diff = Math.abs(len_a - len_b);

        // Padding 0 in front of the
        // number to make both numbers equal
        for (int i = 1; i <= diff; i++)
            s += "0";

        // Condition to check if the strings
        // have lengths mis-match
        if (len_a < len_b)
            a = s + a;
        else
            b = s + b;

        int curr, carry = 0;

        // Loop to find the find the sum
        // of two integers of base B
        for (int i = Math.max(len_a, len_b) - 1;
                            i > -1; i--) {

            // Current Place value for
            // the resultant sum
            curr = carry + (a.charAt(i) - '0') +
                        (b.charAt(i) - '0');

            // Update carry
            carry = curr / base;

            // Find current digit
            curr = curr % base;

            // Update sum result
            sum = (char)(curr + '0') + sum;
        }
        if (carry > 0)
            sum = (char)(carry + '0') + sum;
        return sum;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String a, b, sum;
        int base;
        a = "123";
        b = "234";
        base = 6;

        // Function Call
        sum = sumBaseB(a, b, base);
        System.out.println(sum);
    }
}

// This code is contributed by AnkitRai01
```

## python 3

```
# Python 3 implementation to find the
# sum of two integers of base B

# Function to find the sum of
# two integers of base B
def sumBaseB(a,b,base):

    len_a = len(a)
    len_b = len(b)

    s = "";
    sum = "";

    diff = abs(len_a - len_b);

    # Padding 0 in front of the
    # number to make both numbers equal
    for i in range(1,diff+1):
        s += "0"

    # Condition to check if the strings
    # have lengths mis-match
    if (len_a < len_b):
        a = s + a
    else:
        b = s + b;

    carry = 0;

    # Loop to find the find the sum
    # of two integers of base B
    for i in range(max(len_a, len_b) - 1,-1,-1):

        # Current Place value for
        # the resultant sum
        curr = carry + (ord(a[i]) -ord('0')) +( ord(b[i]) - ord('0'));

        # Update carry
        carry = curr // base

        # Find current digit
        curr = curr % base;

        # Update sum result
        sum = chr(curr + ord('0')) + sum

    if (carry > 0):
        sum = chr(carry + ord('0')) + sum;
    return sum

# Driver Code

a = "123"
b = "234"
base = 6

# Function Call
sum = sumBaseB(a, b, base);
print(sum)

# This code is contributed by atul_kumar_shrivastava
```

## c#

```
// C# implementation to find the
// sum of two integers of base B
using System;

class GFG {

    // Function to find the sum of
    // two integers of base B
    static string sumBaseB(string a, string b, int base_var)
    {
        int len_a, len_b;

        len_a = a.Length;
        len_b = b.Length;

        string sum, s;
        s = "";
        sum = "";

        int diff;
        diff = Math.Abs(len_a - len_b);

        // Padding 0 in front of the
        // number to make both numbers equal
        for (int i = 1; i <= diff; i++)
            s += "0";

        // Condition to check if the strings
        // have lengths mis-match
        if (len_a < len_b)
            a = s + a;
        else
            b = s + b;

        int curr, carry = 0;

        // Loop to find the find the sum
        // of two integers of base B
        for (int i = Math.Max(len_a, len_b) - 1;
                            i > -1; i--) {

            // Current Place value for
            // the resultant sum
            curr = carry + (a[i] - '0') +
                        (b[i] - '0');

            // Update carry
            carry = curr / base_var;

            // Find current digit
            curr = curr % base_var;

            // Update sum result
            sum = (char)(curr + '0') + sum;
        }
        if (carry > 0)
            sum = (char)(carry + '0') + sum;
        return sum;
    }

    // Driver Code
    public static void Main (string[] args)
    {
        string a, b, sum;
        int base_var;
        a = "123";
        b = "234";
        base_var = 6;

        // Function Call
        sum = sumBaseB(a, b, base_var);
        Console.WriteLine(sum);
    }
}

// This code is contributed by AnkitRai01
```

## Javascript

```
<script>

// Javascript implementation to find the
// sum of two integers of base B

// Function to find the sum of
// two integers of base B
function sumBaseB(a, b, base_var)
{
    let len_a, len_b;

    len_a = a.length;
    len_b = b.length;

    let sum, s;
    s = "";
    sum = "";

    let diff;
    diff = Math.abs(len_a - len_b);

    // Padding 0 in front of the
    // number to make both numbers equal
    for(let i = 1; i <= diff; i++)
        s += "0";

    // Condition to check if the strings
    // have lengths mis-match
    if (len_a < len_b)
        a = s + a;
    else
        b = s + b;

    let curr, carry = 0;

    // Loop to find the find the sum
    // of two integers of base B
    for(let i = Math.max(len_a, len_b) - 1;
            i > -1; i--)
    {

        // Current Place value for
        // the resultant sum
        curr = carry + (a[i].charCodeAt() -
                         '0'.charCodeAt()) +
                       (b[i].charCodeAt() -
                         '0'.charCodeAt());

        // Update carry
        carry = parseInt(curr / base_var, 10);

        // Find current digit
        curr = curr % base_var;

        // Update sum result
        sum = String.fromCharCode(
            curr + '0'.charCodeAt()) + sum;
    }
    if (carry > 0)
        sum = String.fromCharCode(
            carry + '0'.charCodeAt()) + sum;

    return sum;
}

// Driver code
let a, b, sum;
let base_var;
a = "123";
b = "234";
base_var = 6;

// Function Call
sum = sumBaseB(a, b, base_var);
document.write(sum + "</br>");

// This code is contributed by divyesh072019  

</script>
```

**输出:**

```
401
```

时间复杂度:0(透镜 _ a–透镜 _b)

辅助空间:0(1)