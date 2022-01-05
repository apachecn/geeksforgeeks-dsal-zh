# 用给定的操作生成数字，检查是否是回文

> 原文:[https://www . geesforgeks . org/生成带有给定操作的数字并检查它是否是回文/](https://www.geeksforgeeks.org/generate-number-with-given-operation-and-check-if-it-is-palindrome/)

给定一个整数 **N** ，任务是通过重复该数字来创建一个字符串，使得结果字符串的长度等于原始数字中数字的总和。
例如:如果数字是 **61** ，数字之和是 **6 + 1 = 7** ，那么重复 **61** 后生成的字符串将是 **7** 长度，即 **6161616** 。
**举例:**

> **输入:** N = 10101
> **输出:**是
> 字符串的长度由数字的总和给出，即 1 + 0 + 1 + 0 + 1 = 3。
> 所以结果串是“101”，是回文。
> **输入:** N = 123
> **输出:**否
> 字符串的长度将为 1+2 ^ 3 = 6。
> 所以结果串是“123123”，不是回文。

**进场:**

*   求 **N** 的数字之和，重复这个数字，直到字符串的长度等于这个和。
*   现在检查结果字符串是否是回文。
*   如果是回文，则打印**是**。
*   否则打印**否**。

以下是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // Function that returns true if str is a palindrome
    bool isPalindrome(string str)
    {
        int len = str.length();
        for (int i = 0; i < len / 2; i++)
        {
            if (str[i] != str[len - 1 - i])
                return false;
        }

        return true;
    }

    // Function that returns true if the
    // generated string is a palindrome
    bool createStringAndCheckPalindrome(int N)
    {

        // sub contains N as a string
        ostringstream out;
        out << N;
        string result = out.str();

        string sub = "" + result, res_str = "";

        int sum = 0;

        // Calculate the sum of the digits
        while (N > 0)
        {
            int digit = N % 10;
            sum += digit;
            N = N / 10;
        }

        // Repeat the substring until the length
        // of the resultant string < sum
        while (res_str.length() < sum)
            res_str += sub;

        // If length of the resultant string exceeded sum
        // then take substring from 0 to sum - 1
        if (res_str.length() > sum)
            res_str = res_str.substr(0, sum);

        // If the generated string is a palindrome
        if (isPalindrome(res_str))
            return true;

        return false;
    }

    // Driver code
    int main()
    {
        int N = 10101;
        if (createStringAndCheckPalindrome(N))
            cout << ("Yes");
        else
            cout << ("No");
    }

// This code is contributed by
// Shashank_Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if str is a palindrome
    static boolean isPalindrome(String str)
    {
        int len = str.length();
        for (int i = 0; i < len / 2; i++) {
            if (str.charAt(i) != str.charAt(len - 1 - i))
                return false;
        }

        return true;
    }

    // Function that returns true if the
    // generated string is a palindrome
    static boolean createStringAndCheckPalindrome(int N)
    {

        // sub contains N as a string
        String sub = "" + N, res_str = "";

        int sum = 0;

        // Calculate the sum of the digits
        while (N > 0) {
            int digit = N % 10;
            sum += digit;
            N = N / 10;
        }

        // Repeat the substring until the length
        // of the resultant string < sum
        while (res_str.length() < sum)
            res_str += sub;

        // If length of the resultant string exceeded sum
        // then take substring from 0 to sum - 1
        if (res_str.length() > sum)
            res_str = res_str.substring(0, sum);

        // If the generated string is a palindrome
        if (isPalindrome(res_str))
            return true;

        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 10101;
        if (createStringAndCheckPalindrome(N))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if
# str is a palindrome
def isPalindrome(s):

    l = len(s)
    for i in range(l // 2):
        if (s[i] != s[l - 1 - i]):
            return False
    return True

# Function that returns true if the
# generated string is a palindrome
def createStringAndCheckPalindrome(N):

    # sub contains N as a string
    sub = "" + chr(N)
    res_str = ""

    sum = 0

    # Calculate the sum of the digits
    while (N > 0) :
        digit = N % 10
        sum += digit
        N = N // 10

    # Repeat the substring until the length
    # of the resultant string < sum
    while (len(res_str) < sum):
        res_str += sub

    # If length of the resultant string exceeded
    # sum then take substring from 0 to sum - 1
    if (len(res_str) > sum):
        res_str = res_str[0: sum]

    # If the generated string is a palindrome
    if (isPalindrome(res_str)):
        return True

    return False

# Driver code
if __name__ == "__main__":

    N = 10101
    if (createStringAndCheckPalindrome(N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach

using System ;

class GFG {

    // Function that returns true if str is a palindrome
    static bool isPalindrome(string str)
    {
        int len = str.Length;
        for (int i = 0; i < len / 2; i++) {
            if (str[i] != str[len - 1 - i])
                return false;
        }

        return true;
    }

    // Function that returns true if the
    // generated string is a palindrome
    static bool createStringAndCheckPalindrome(int N)
    {

        // sub contains N as a string
        string sub = "" + N, res_str = "";

        int sum = 0;

        // Calculate the sum of the digits
        while (N > 0) {
            int digit = N % 10;
            sum += digit;
            N = N / 10;
        }

        // Repeat the substring until the length
        // of the resultant string < sum
        while (res_str.Length< sum)
            res_str += sub;

        // If length of the resultant string exceeded sum
        // then take substring from 0 to sum - 1
        if (res_str.Length > sum)
            res_str = res_str.Substring(0, sum);

        // If the generated string is a palindrome
        if (isPalindrome(res_str))
            return true;

        return false;
    }

    // Driver code
    public static void Main()
    {
        int N = 10101;
        if (createStringAndCheckPalindrome(N))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
    // This code is contributed by Ryuga
}
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

     // Function that returns true
     // if str is a palindrome
    function isPalindrome(str)
    {
        let len = str.length;
        for (let i = 0; i < len / 2; i++) {
            if (str[i] != str[len - 1 - i])
                return false;
        }

        return true;
    }

     // Function that returns true if the
    // generated string is a palindrome
    function createStringAndCheckPalindrome(N)
    {
        // sub contains N as a string
        let sub = "" + N, res_str = "";

        let sum = 0;

        // Calculate the sum of the digits
        while (N > 0) {
            let digit = N % 10;
            sum += digit;
            N = N / 10;
        }

        // Repeat the substring until the length
        // of the resultant string < sum
        while (res_str.length < sum)
            res_str += sub;

        // If length of the resultant string exceeded sum
        // then take substring from 0 to sum - 1
        if (res_str.length > sum)
            res_str = res_str.substring(0, sum);

        // If the generated string is a palindrome
        if (isPalindrome(res_str))
            return true;

        return false;
    }

    // Driver code
    let N = 10101;
        if (createStringAndCheckPalindrome(N))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Yes
```