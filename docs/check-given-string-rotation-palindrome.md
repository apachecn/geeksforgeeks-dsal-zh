# 检查给定的字符串是否是回文的旋转

> 原文:[https://www . geesforgeks . org/check-given-string-rotation-回文/](https://www.geeksforgeeks.org/check-given-string-rotation-palindrome/)

给定一个字符串，检查它是否是回文的旋转。例如，你的函数应该为“aab”返回 true，因为它是“aba”的旋转。
**例:**

```
Input:  str = "aaaad"
Output: 1  
// "aaaad" is a rotation of a palindrome "aadaa"

Input:  str = "abcd"
Output: 0
// "abcd" is not a rotation of any palindrome.
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/check-if-a-given-string-is-a-rotation-of-a-palindrome0317/1)

一个**简单的解决方法**是取输入字符串，尝试它的每一个可能的旋转，如果一个旋转是回文，返回 true。如果没有旋转是回文，那么返回 false。
以下是本办法的实施情况。

## C++

```
#include <iostream>
#include <string>
using namespace std;

// A utility function to check if a string str is palindrome
bool isPalindrome(string str)
{
    // Start from leftmost and rightmost corners of str
    int l = 0;
    int h = str.length() - 1;

    // Keep comparing characters while they are same
    while (h > l)
        if (str[l++] != str[h--])
            return false;

    // If we reach here, then all characters were matching
    return true;
}

// Function to check if a given string is a rotation of a
// palindrome.
bool isRotationOfPalindrome(string str)
{
    // If string iteself is palindrome
    if (isPalindrome(str))
        return true;

    // Now try all rotations one by one
    int n = str.length();
    for (int i = 0; i < n - 1; i++) {
        string str1 = str.substr(i + 1, n - i - 1);
        string str2 = str.substr(0, i + 1);

        // Check if this rotation is palindrome
        if (isPalindrome(str1.append(str2)))
            return true;
    }
    return false;
}

// Driver program to test above function
int main()
{
    cout << isRotationOfPalindrome("aab") << endl;
    cout << isRotationOfPalindrome("abcde") << endl;
    cout << isRotationOfPalindrome("aaaad") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given string
// is a rotation of a palindrome
import java.io.*;

class Palindrome {
    // A utility function to check if a string str is palindrome
    static boolean isPalindrome(String str)
    {
        // Start from leftmost and rightmost corners of str
        int l = 0;
        int h = str.length() - 1;

        // Keep comparing characters while they are same
        while (h > l)
            if (str.charAt(l++) != str.charAt(h--))
                return false;

        // If we reach here, then all characters were matching
        return true;
    }

    // Function to check if a given string is a rotation of a
    // palindrome
    static boolean isRotationOfPalindrome(String str)
    {
        // If string iteself is palindrome
        if (isPalindrome(str))
            return true;

        // Now try all rotations one by one
        int n = str.length();
        for (int i = 0; i < n - 1; i++) {
            String str1 = str.substring(i + 1);
            String str2 = str.substring(0, i + 1);

            // Check if this rotation is palindrome
            if (isPalindrome(str1 + str2))
                return true;
        }
        return false;
    }

    // driver program
    public static void main(String[] args)
    {
        System.out.println((isRotationOfPalindrome("aab")) ? 1 : 0);
        System.out.println((isRotationOfPalindrome("abcde")) ? 1 : 0);
        System.out.println((isRotationOfPalindrome("aaaad")) ? 1 : 0);
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program to check if a given string is a rotation
# of a palindrome

# A utility function to check if a string str is palindrome
def isPalindrome(string):

    # Start from leftmost and rightmost corners of str
    l = 0
    h = len(string) - 1

    # Keep comparing characters while they are same
    while h > l:
        l+= 1
        h-= 1
        if string[l-1] != string[h + 1]:
            return False

    # If we reach here, then all characters were matching   
    return True

# Function to check if a given string is a rotation of a
# palindrome.
def isRotationOfPalindrome(string):

    # If string itself is palindrome
    if isPalindrome(string):
        return True

    # Now try all rotations one by one
    n = len(string)
    for i in xrange(n-1):
        string1 = string[i + 1:n]
        string2 = string[0:i + 1]

        # Check if this rotation is palindrome
        string1+=(string2)
        if isPalindrome(string1):
            return True

    return False

# Driver program
print "1" if isRotationOfPalindrome("aab") == True else "0"
print "1" if isRotationOfPalindrome("abcde") == True else "0"
print "1" if isRotationOfPalindrome("aaaad") == True else "0"

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to check if a given string
// is a rotation of a palindrome
using System;

class GFG {
    // A utility function to check if
    // a string str is palindrome
    public static bool isPalindrome(string str)
    {
        // Start from leftmost and
        // rightmost corners of str
        int l = 0;
        int h = str.Length - 1;

        // Keep comparing characters
        // while they are same
        while (h > l) {
            if (str[l++] != str[h--]) {
                return false;
            }
        }

        // If we reach here, then all
        // characters were matching
        return true;
    }

    // Function to check if a given string
    // is a rotation of a palindrome
    public static bool isRotationOfPalindrome(string str)
    {
        // If string iteself is palindrome
        if (isPalindrome(str)) {
            return true;
        }

        // Now try all rotations one by one
        int n = str.Length;
        for (int i = 0; i < n - 1; i++) {
            string str1 = str.Substring(i + 1);
            string str2 = str.Substring(0, i + 1);

            // Check if this rotation is palindrome
            if (isPalindrome(str1 + str2)) {
                return true;
            }
        }
        return false;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        Console.WriteLine((isRotationOfPalindrome("aab")) ? 1 : 0);
        Console.WriteLine((isRotationOfPalindrome("abcde")) ? 1 : 0);
        Console.WriteLine((isRotationOfPalindrome("aaaad")) ? 1 : 0);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// javascript program to check if a given string
// is a rotation of a palindrome

    // A utility function to check if
    // a string str is palindrome
    function  isPalindrome( str)
    {

        // Start from leftmost and
        // rightmost corners of str
        var l = 0;
        var h = str.length - 1;

        // Keep comparing characters
        // while they are same
        while (h > l) {
            if (str[l++] != str[h--]) {
                return false;
            }
        }

        // If we reach here, then all
        // characters were matching
        return true;
    }

    // Function to check if a given string
    // is a rotation of a palindrome
    function isRotationOfPalindrome( str)
    {
        // If string iteself is palindrome
        if (isPalindrome(str)) {
            return true;
        }

        // Now try all rotations one by one
        var n = str.length;
        for (var i = 0; i < n - 1; i++) {
            var str1 = str.substring(i + 1);
            var str2 = str.substring(0, i + 1);

            // Check if this rotation is palindrome
            if (isPalindrome(str1 + str2)) {
                return true;
            }
        }
        return false;
    }

    // Driver Code
        document.write((isRotationOfPalindrome("aab")) ? 1 : 0 );
        document.write("<br>");
        document.write((isRotationOfPalindrome("abcde")) ? 1 : 0 );
        document.write("<br>");
        document.write((isRotationOfPalindrome("aaaad")) ? 1 : 0);

// This code is contributed by bunnyram19.
</script>
```

**输出:**

```
1
0
1
```

**时间复杂度:**O(n)<sup>2</sup>)
辅助空间:O(n)用于存储旋转。
注意，上面的算法可以优化为在 O(1)个额外空间中工作，因为我们可以[在 O(n)个时间和 O(1)个额外空间](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)中旋转一个字符串。
一个**优化方案**可以在 O(n)时间内工作。这里的思路是用 Manacher 的算法来解决上述问题。

*   让给定的字符串为“s”，字符串长度为“n”。
*   预处理/准备使用 Manachers 算法的字符串，以帮助找到偶数长度的回文，为此，我们将给定的字符串与其本身连接起来(以发现旋转是否会给出回文)，并添加“{ content }”；开头的符号和字母之间的“#”字符。我们用“@”结束字符串。因此，对于“aaad”输入，重组后的字符串将是–“$ # a # a # a # a # d # a # a # a # a # a # a # d # @”
*   现在问题简化为在字符串中使用长度为 n 或更大的 Manacher 算法找到[最长回文子串。](https://www.geeksforgeeks.org/manachers-algorithm-linear-time-longest-palindromic-substring-part-1/)
*   如果有长度为 n 的回文子串，则返回 true，否则返回 false。如果我们找到一个更长的回文，那么我们检查输入的大小是偶数还是奇数，相应地，我们找到的回文长度也应该是偶数还是奇数。

例如，如果我们的输入大小是 3，在执行 Manacher 的算法时，我们得到的回文大小为 5，显然它会包含大小为 3 的子串，这是一个回文，但长度为 4 的回文就不能这样说了。因此，我们检查在任何情况下输入的大小和回文的大小是偶数还是奇数。
边界情况将是具有相同字母的单词，这将违反上述属性，但是对于这种情况，我们的算法将发现偶数长度和奇数长度回文，其中一个是子串，因此不会有问题。
以下是上述算法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if we have found
// a palindrome of same length as the input
// which is a rotation of the input string
bool checkPal(int x, int len)
{
    if (x == len)
        return true;
    else if (x > len) {
        if ((x % 2 == 0 && len % 2 == 0)
            || (x % 2 != 0 && len % 2 != 0))
            return true;
    }
    return false;
}

// Function to preprocess the string
// for Manacher's Algorithm
string reform(string s)
{
    string s1 = "$#";

    // Adding # between the characters
    for (int i = 0; i < s.size(); i++) {
        s1 += s[i];
        s1 += '#';
    }

    s1 += '@';
    return s1;
}

// Function to find the longest palindromic
// substring using Manacher's Algorithm
bool longestPal(string s, int len)
{

    // Current Left Position
    int mirror = 0;

    // Center Right Position
    int R = 0;

    // Center Position
    int C = 0;

    // LPS Length Array
    int P[s.size()] = { 0 };
    int x = 0;

    // Get currentLeftPosition Mirror
    // for currentRightPosition i
    for (int i = 1; i < s.size() - 1; i++) {
        mirror = 2 * C - i;

        // If currentRightPosition i is
        // within centerRightPosition R
        if (i < R)
            P[i] = min((R - i), P[mirror]);

        // Attempt to expand palindrome centered
        // at currentRightPosition i
        while (s[i + (1 + P[i])] == s[i - (1 + P[i])]) {
            P[i]++;
        }

        // Check for palindrome
        bool ans = checkPal(P[i], len);
        if (ans)
            return true;

        // If palindrome centered at currentRightPosition i
        // expand beyond centerRightPosition R,
        // adjust centerPosition C based on expanded palindrome
        if (i + P[i] > R) {
            C = i;
            R = i + P[i];
        }
    }

    return false;
}

// Driver code
int main()
{
    string s = "aaaad";
    int len = s.size();
    s += s;
    s = reform(s);
    cout << longestPal(s, len);

    return 0;
}

// This code is contributed by Vindusha Pankajakshan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to check if we have found
// a palindrome of same length as the input
// which is a rotation of the input string
static boolean checkPal(int x, int len)
{
    if (x == len)
    {
        return true;
    }
    else if (x > len)
    {
        if ((x % 2 == 0 && len % 2 == 0) ||
            (x % 2 != 0 && len % 2 != 0))
        {
            return true;
        }
    }
    return false;
}

// Function to preprocess the string
// for Manacher's Algorithm
static String reform(String s)
{
    String s1 = "$#";

    // Adding # between the characters
    for (int i = 0; i < s.length(); i++)
    {
        s1 += s.charAt(i);
        s1 += '#';
    }

    s1 += '@';
    return s1;
}

// Function to find the longest palindromic
// substring using Manacher's Algorithm
static boolean longestPal(String s, int len)
{

    // Current Left Position
    int mirror = 0;

    // Center Right Position
    int R = 0;

    // Center Position
    int C = 0;

    // LPS Length Array
    int[] P = new int[s.length()];
    int x = 0;

    // Get currentLeftPosition Mirror
    // for currentRightPosition i
    for (int i = 1; i < s.length() - 1; i++)
    {
        mirror = 2 * C - i;

        // If currentRightPosition i is
        // within centerRightPosition R
        if (i < R)
        {
            P[i] = Math.min((R - i), P[mirror]);
        }

        // Attempt to expand palindrome centered
        // at currentRightPosition i
        while (s.charAt(i + (1 + P[i])) ==
               s.charAt(i - (1 + P[i])))
        {
            P[i]++;
        }

        // Check for palindrome
        boolean ans = checkPal(P[i], len);
        if (ans)
        {
            return true;
        }

        // If palindrome centered at currentRightPosition i
        // expand beyond centerRightPosition R,
        // adjust centerPosition C based on expanded palindrome
        if (i + P[i] > R)
        {
            C = i;
            R = i + P[i];
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    String s = "aaaad";
    int len = s.length();
    s += s;
    s = reform(s);
    System.out.println(longestPal(s, len) ? 1 : 0);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to check if we have found
# a palindrome of same length as the input
# which is a rotation of the input string
def checkPal (x, Len):

    if (x == Len):
        return True
    elif (x > Len):
        if ((x % 2 == 0 and Len % 2 == 0) or (x % 2 != 0 and Len % 2 != 0)):
            return True

    return False

# Function to preprocess the string
# for Manacher's Algorithm
def reform (s):

    s1 = "$#"

    # Adding '#' between the characters
    for i in range(len(s)):
        s1 += s[i]
        s1 += "#"

    s1 += "@"
    return s1

# Function to find the longest palindromic
# substring using Manacher's Algorithm
def longestPal (s, Len):

    # Current Left Position
    mirror = 0

    # Center Right Position
    R = 0

    # Center Position
    C = 0

    # LPS Length Array
    P = [0] * len(s)
    x = 0

    # Get currentLeftPosition Mirror
    # for currentRightPosition i
    for i in range(1, len(s) - 1):
        mirror = 2 * C - i

        # If currentRightPosition i is
        # within centerRightPosition R
        if (i < R):
            P[i] = min((R-i), P[mirror])

        # Attempt to expand palindrome centered
        # at currentRightPosition i
        while (s[i + (1 + P[i])] == s[i - (1 + P[i])]):
            P[i] += 1

        # Check for palindrome
        ans = checkPal(P[i], Len)
        if (ans):
            return True

        # If palindrome centered at current
        # RightPosition i expand beyond
        # centerRightPosition R, adjust centerPosition
        # C based on expanded palindrome
        if (i + P[i] > R):
            C = i
            R = i + P[i]

    return False

# Driver Code
if __name__ == '__main__':

    s = "aaaad"
    Len = len(s)
    s += s
    s = reform(s)
    print(longestPal(s, Len))

# This code is contributed by himanshu77
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if we have found
// a palindrome of same length as the input
// which is a rotation of the input string
static bool checkPal(int x, int len)
{
    if (x == len)
    {
        return true;
    }
    else if (x > len)
    {
        if ((x % 2 == 0 && len % 2 == 0) ||
            (x % 2 != 0 && len % 2 != 0))
        {
            return true;
        }
    }
    return false;
}

// Function to preprocess the string
// for Manacher's Algorithm
static String reform(String s)
{
    String s1 = "$#";

    // Adding # between the characters
    for (int i = 0; i < s.Length; i++)
    {
        s1 += s[i];
        s1 += '#';
    }

    s1 += '@';
    return s1;
}

// Function to find the longest palindromic
// substring using Manacher's Algorithm
static bool longestPal(String s, int len)
{

    // Current Left Position
    int mirror = 0;

    // Center Right Position
    int R = 0;

    // Center Position
    int C = 0;

    // LPS Length Array
    int[] P = new int[s.Length];
    int x = 0;

    // Get currentLeftPosition Mirror
    // for currentRightPosition i
    for (int i = 1; i < s.Length - 1; i++)
    {
        mirror = 2 * C - i;

        // If currentRightPosition i is
        // within centerRightPosition R
        if (i < R)
        {
            P[i] = Math.Min((R - i), P[mirror]);
        }

        // Attempt to expand palindrome centered
        // at currentRightPosition i
        while (s[i + (1 + P[i])] == s[i - (1 + P[i])])
        {
            P[i]++;
        }

        // Check for palindrome
        bool ans = checkPal(P[i], len);
        if (ans)
        {
            return true;
        }

        // If palindrome centered at currentRightPosition i
        // expand beyond centerRightPosition R,
        // adjust centerPosition C based on expanded palindrome
        if (i + P[i] > R)
        {
            C = i;
            R = i + P[i];
        }
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    String s = "aaaad";
    int len = s.Length;
    s += s;
    s = reform(s);
    Console.WriteLine(longestPal(s, len) ? 1 : 0);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to check if we have found
    // a palindrome of same length as the input
    // which is a rotation of the input string
    function checkPal(x , len) {
        if (x == len) {
            return true;
        } else if (x > len) {
            if ((x % 2 == 0 && len % 2 == 0) ||
            (x % 2 != 0 && len % 2 != 0))
            {
                return true;
            }
        }
        return false;
    }

    // Function to preprocess the string
    // for Manacher's Algorithm
     function reform( s) {
        var s1 = "$#";

        // Adding # between the characters
        for (i = 0; i < s.length; i++) {
            s1 += s.charAt(i);
            s1 += '#';
        }

        s1 += '@';
        return s1;
    }

    // Function to find the longest palindromic
    // substring using Manacher's Algorithm
    function longestPal( s , len) {

        // Current Left Position
        var mirror = 0;

        // Center Right Position
        var R = 0;

        // Center Position
        var C = 0;

        // LPS Length Array
        var P = Array(s.length).fill(0);
        var x = 0;

        // Get currentLeftPosition Mirror
        // for currentRightPosition i
        for (i = 1; i < s.length - 1; i++) {
            mirror = 2 * C - i;

            // If currentRightPosition i is
            // within centerRightPosition R
            if (i < R) {
                P[i] = Math.min((R - i), P[mirror]);
            }

            // Attempt to expand palindrome centered
            // at currentRightPosition i
            while (s.charAt(i + (1 + P[i])) == s.charAt(i - (1 + P[i]))) {
                P[i]++;
            }

            // Check for palindrome
            var ans = checkPal(P[i], len);
            if (ans) {
                return true;
            }

            // If palindrome centered at currentRightPosition i
            // expand beyond centerRightPosition R,
            // adjust centerPosition C based on expanded palindrome
            if (i + P[i] > R) {
                C = i;
                R = i + P[i];
            }
        }
        return false;
    }

    // Driver code
        var s = "aaaad";
        var len = s.length;
        s += s;
        s = reform(s);
        document.write(longestPal(s, len) ? 1 : 0);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
1
```

本文由 **Abhay Rathi** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息