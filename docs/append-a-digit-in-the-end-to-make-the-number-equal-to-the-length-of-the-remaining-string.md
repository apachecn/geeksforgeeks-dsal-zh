# 在末尾追加一个数字，使数字等于剩余字符串的长度

> 原文:[https://www . geeksforgeeks . org/追加一位数以使数字等于剩余字符串的长度/](https://www.geeksforgeeks.org/append-a-digit-in-the-end-to-make-the-number-equal-to-the-length-of-the-remaining-string/)

给定一个字符串**字符串**，其中一个整数被附加在末尾(有或没有前导零)。任务是从范围**【0，9】**中找到一个必须追加到整数末尾的数字，使该数字等于剩余字符串的长度。如果不可能，打印 **-1** 。
**举例:**

> **输入:**str = " geeksforgeks 1 "
> **输出:**3
> geeksforgeks 的长度为 13
> 所以，1 的末尾必须追加 3。
> **输入:** str = "abcd0"
> **输出:** 4

**方法:**找到字符串末尾附加的数字，说出 **num** 并在末尾附加一个 **0** ，这是可能的最少数字，即 **num = num * 10** 。现在找到剩余字符串的长度，忽略最后的数字，说 **len** 。现在必须追加的数字将是**数字= len–num**。如果**数字**在**【0，9】**范围内，则打印，否则打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required digit
int find_digit(string s, int n)
{

    // To store the position of the first
    // numeric digit in the string
    int first_digit = -1;
    for (int i = n - 1; i >= 0; i--) {
        if (s[i] < '0' || s[i] > '9') {
            first_digit = i;
            break;
        }
    }
    first_digit++;

    // To store the length of the
    // string without the numeric
    // digits in the end
    int s_len = first_digit;

    // pw stores the current power of 10
    // and num is to store the number
    // which is appended in the end
    int num = 0, pw = 1;
    int i = n - 1;
    while (i >= 0) {

        // If current character is
        // a numeric digit
        if (s[i] >= '0' && s[i] <= '9') {

            // Get the current digit
            int digit = s[i] - '0';

            // Build the number
            num = num + (pw * digit);

            // If number exceeds the length
            if (num >= s_len)
                return -1;

            // Next power of 10
            pw = pw * 10;
        }
        i--;
    }

    // Append 0 in the end
    num = num * 10;

    // Required number that must be added
    int req = s_len - num;

    // If number is not a single digit
    if (req > 9 || req < 0)
        return -1;
    return req;
}

// Driver code
int main()
{
    string s = "abcd0";
    int n = s.length();

    cout << find_digit(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the required digit
static int find_digit(String s, int n)
{

    // To store the position of the first
    // numeric digit in the string
    int first_digit = -1;
    for (int i = n - 1; i >= 0; i--)
    {
        if (s.charAt(i) < '0' ||
            s.charAt(i) > '9')
        {
            first_digit = i;
            break;
        }
    }
    first_digit++;

    // To store the length of the
    // string without the numeric
    // digits in the end
    int s_len = first_digit;

    // pw stores the current power of 10
    // and num is to store the number
    // which is appended in the end
    int num = 0, pw = 1;
    int i = n - 1;
    while (i >= 0)
    {

        // If current character is
        // a numeric digit
        if (s.charAt(i) >= '0' &&
            s.charAt(i) <= '9')
        {

            // Get the current digit
            int digit = s.charAt(i) - '0';

            // Build the number
            num = num + (pw * digit);

            // If number exceeds the length
            if (num >= s_len)
                return -1;

            // Next power of 10
            pw = pw * 10;
        }
        i--;
    }

    // Append 0 in the end
    num = num * 10;

    // Required number that must be added
    int req = s_len - num;

    // If number is not a single digit
    if (req > 9 || req < 0)
        return -1;
    return req;
}

// Driver code
public static void main (String[] args)
{
    String s = "abcd0";
    int n = s.length();

    System.out.print(find_digit(s, n));
}
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required digit
def find_digit(s, n):

    # To store the position of the first
    # numeric digit in the string
    first_digit = -1
    for i in range(n - 1, -1, -1):
        if s[i] < '0' or s[i] > '9':
            first_digit = i
            break

    first_digit += 1

    # To store the length of the
    # string without the numeric
    # digits in the end
    s_len = first_digit
    num = 0
    pw = 1
    i = n - 1
    while i >= 0:

        # If current character is
        # a numeric digit
        if s[i] >= '0' and s[i] <= '9':

            # Get the current digit
            digit = ord(s[i]) - ord('0')

            # Build the number
            num = num + (pw * digit)

            # If number exceeds the length
            if num >= s_len:
                return -1

            # Next power of 10
            pw = pw * 10

        i -= 1

    # Append 0 in the end
    num = num * 10

    # Required number that must be added
    req = s_len - num

    # If number is not a single digit
    if req > 9 or req < 0:
        return -1
    return req

# Driver code
if __name__ == "__main__":
    s = "abcd0"
    n = len(s)
    print(find_digit(s, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required digit
static int find_digit(String s, int n)
{

    // To store the position of the first
    // numeric digit in the string
    int first_digit = -1, i;
    for (i = n - 1; i >= 0; i--)
    {
        if (s[i] < '0' ||
            s[i] > '9')
        {
            first_digit = i;
            break;
        }
    }

    first_digit++;

    // To store the length of the
    // string without the numeric
    // digits in the end
    int s_len = first_digit;

    // pw stores the current power of 10
    // and num is to store the number
    // which is appended in the end
    int num = 0, pw = 1;
    i = n - 1;
    while (i >= 0)
    {

        // If current character is
        // a numeric digit
        if (s[i] >= '0' &&
            s[i] <= '9')
        {

            // Get the current digit
            int digit = s[i] - '0';

            // Build the number
            num = num + (pw * digit);

            // If number exceeds the length
            if (num >= s_len)
                return -1;

            // Next power of 10
            pw = pw * 10;
        }
        i--;
    }

    // Append 0 in the end
    num = num * 10;

    // Required number that must be added
    int req = s_len - num;

    // If number is not a single digit
    if (req > 9 || req < 0)
        return -1;
    return req;
}

// Driver code
public static void Main (String[] args)
{
    String s = "abcd0";
    int n = s.Length;

    Console.Write(find_digit(s, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required digit
function find_digit(s, n)
{

    // To store the position of the first
    // numeric digit in the string
    var first_digit = -1;
    for (var i = n - 1; i >= 0; i--) {
        if (s[i] < '0' || s[i] > '9') {
            first_digit = i;
            break;
        }
    }
    first_digit++;

    // To store the length of the
    // string without the numeric
    // digits in the end
    var s_len = first_digit;

    // pw stores the current power of 10
    // and num is to store the number
    // which is appended in the end
    var num = 0, pw = 1;
    var i = n - 1;
    while (i >= 0) {

        // If current character is
        // a numeric digit
        if (s[i] >= '0' && s[i] <= '9') {

            // Get the current digit
            var digit = s[i] - '0';

            // Build the number
            num = num + (pw * digit);

            // If number exceeds the length
            if (num >= s_len)
                return -1;

            // Next power of 10
            pw = pw * 10;
        }
        i--;
    }

    // Append 0 in the end
    num = num * 10;

    // Required number that must be added
    var req = s_len - num;

    // If number is not a single digit
    if (req > 9 || req < 0)
        return -1;
    return req;
}

// Driver code
var s = "abcd0";
var n = s.length;
document.write( find_digit(s, n));

</script>
```

**Output:** 

```
4
```