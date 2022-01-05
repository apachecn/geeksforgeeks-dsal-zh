# 删除所有连续重复后检查字符串是否为回文

> 原文:[https://www . geesforgeks . org/check-if-string-is-回文-移除所有连续重复项后/](https://www.geeksforgeeks.org/check-if-string-is-palindrome-after-removing-all-consecutive-duplicates/)

给定一个字符串 **str** ，任务是从字符串 **str** 中移除所有连续的重复项，并检查最终的[字符串是否是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。如果是回文，打印**“是”**，否则打印**“否”**。
**举例:**

> **输入:**str = " abcbbbaaa "
> **输出:**是
> **解释:**
> 删除所有连续重复字符后，字符串变为“abcba”，即回文。
> **输入:**str = " aaabbaaccc "
> **输出:**否
> **说明:**
> 删除所有连续重复字符后，字符串变成“abac”，不是回文。

**方法:**想法是从给定的字符串创建一个新字符串，并检查新字符串是否是回文。以下是步骤:

*   初始化新字符串。
*   逐一遍历给定字符串的所有字符，如果当前字符与前一个字符不同，则将该字符追加到新字符串 **newStr** 中。
*   否则检查下一个字符。
*   检查最终形成的字符串是否为[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。打印**“是”**如果是回文其他打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is palindrome or not
bool isPalindrome(string str)
{
    // Length of the string
    int len = str.length();

    // Check if its a palindrome
    for (int i = 0; i < len; i++) {

        // If the palindromic
        // condition is not met
        if (str[i] != str[len - i - 1])
            return false;
    }

    // Return true as str is palindromic
    return true;
}

// Function to check if string str is
// palindromic after removing every
// consecutive characters from the str
bool isCompressablePalindrome(string str)
{
    // Length of the string str
    int len = str.length();

    // Create an empty
    // compressed string
    string compressed = "";

    // The first character will
    // always be included in
    // the final string
    compressed.push_back(str[0]);

    // Check all the characters
    // of the string
    for (int i = 1; i < len; i++) {

        // If the current character
        // is not same as its previous
        // one, then insert it in the
        // final string
        if (str[i] != str[i - 1])
            compressed.push_back(str[i]);
    }

    // Check if the compressed
    // string is a palindrome
    return isPalindrome(compressed);
}

// Driver Code
int main()
{

    // Given string
    string str = "abbcbbbaaa";

    // Function call
    if (isCompressablePalindrome(str))
        cout << "Yes\n";
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to check if a String
// is palindrome or not
static boolean isPalindrome(String str)
{
    // Length of the String
    int len = str.length();

    // Check if its a palindrome
    for (int i = 0; i < len; i++)
    {

        // If the palindromic
        // condition is not met
        if (str.charAt(i) != str.charAt(len - i - 1))
            return false;
    }

    // Return true as str is palindromic
    return true;
}

// Function to check if String str is
// palindromic after removing every
// consecutive characters from the str
static boolean isCompressablePalindrome(String str)
{
    // Length of the String str
    int len = str.length();

    // Create an empty
    // compressed String
    String compressed = "";

    // The first character will
    // always be included in
    // the final String
    compressed = String.valueOf(str.charAt(0));

    // Check all the characters
    // of the String
    for (int i = 1; i < len; i++)
    {

        // If the current character
        // is not same as its previous
        // one, then insert it in the
        // final String
        if (str.charAt(i) != str.charAt(i - 1))
            compressed += str.charAt(i);
    }

    // Check if the compressed
    // String is a palindrome
    return isPalindrome(compressed);
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String str = "abbcbbbaaa";

    // Function call
    if (isCompressablePalindrome(str))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a string
# is palindrome or not
def isPalindrome(Str):

    # Length of the string
    Len = len(Str)

    # Check if its a palindrome
    for i in range(Len):

        # If the palindromic
        # condition is not met
        if (Str[i] != Str[Len - i - 1]):
            return False

    # Return true as Str is palindromic
    return True

# Function to check if string str is
# palindromic after removing every
# consecutive characters from the str
def isCompressablePalindrome(Str):

    # Length of the string str
    Len = len(Str)

    # Create an empty compressed string
    compressed = ""

    # The first character will always
    # be included in final string
    compressed += Str[0]

    # Check all the characters
    # of the string
    for i in range(1, Len):

        # If the current character
        # is not same as its previous
        # one, then insert it in
        # the final string
        if (Str[i] != Str[i - 1]):
            compressed += Str[i]

    # Check if the compressed
    # string is a palindrome
    return isPalindrome(compressed)

# Driver Code
if __name__ == '__main__':

    # Given string
    Str = "abbcbbbaaa"

    # Function call
    if (isCompressablePalindrome(Str)):
        print("Yes")
    else:
        print("No")

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a String
// is palindrome or not
static bool isPalindrome(String str)
{

    // Length of the String
    int len = str.Length;

    // Check if its a palindrome
    for(int i = 0; i < len; i++)
    {

       // If the palindromic
       // condition is not met
       if (str[i] != str[len - i - 1])
           return false;
    }

    // Return true as str is palindromic
    return true;
}

// Function to check if String str is
// palindromic after removing every
// consecutive characters from the str
static bool isCompressablePalindrome(String str)
{

    // Length of the String str
    int len = str.Length;

    // Create an empty
    // compressed String
    String compressed = "";

    // The first character will
    // always be included in
    // the readonly String
    compressed = String.Join("", str[0]);

    // Check all the characters
    // of the String
    for(int i = 1; i < len; i++)
    {

       // If the current character
       // is not same as its previous
       // one, then insert it in the
       // readonly String
       if (str[i] != str[i - 1])
           compressed += str[i];
    }

    // Check if the compressed
    // String is a palindrome
    return isPalindrome(compressed);
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String str = "abbcbbbaaa";

    // Function call
    if (isCompressablePalindrome(str))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if a String
    // is palindrome or not
    function isPalindrome(str)
    {

        // Length of the String
        let len = str.length;

        // Check if its a palindrome
        for(let i = 0; i < len; i++)
        {

           // If the palindromic
           // condition is not met
           if (str[i] != str[len - i - 1])
               return false;
        }

        // Return true as str is palindromic
        return true;
    }

    // Function to check if String str is
    // palindromic after removing every
    // consecutive characters from the str
    function isCompressablePalindrome(str)
    {

        // Length of the String str
        let len = str.length;

        // Create an empty
        // compressed String
        let compressed = "";

        // The first character will
        // always be included in
        // the readonly String
        compressed = str[0];

        // Check all the characters
        // of the String
        for(let i = 1; i < len; i++)
        {

           // If the current character
           // is not same as its previous
           // one, then insert it in the
           // readonly String
           if (str[i] != str[i - 1])
               compressed += str[i];
        }

        // Check if the compressed
        // String is a palindrome
        return isPalindrome(compressed);
    }

    // Given String
    let str = "abbcbbbaaa";

    // Function call
    if (isCompressablePalindrome(str))
        document.write("Yes" + "</br>");
    else
        document.write("No");

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(N)* ，其中 N 为字符串长度。