# 检查字符串的后缀和前缀是否是回文

> 原文:[https://www . geesforgeks . org/check-if-后缀和前缀的字符串都是回文/](https://www.geeksforgeeks.org/check-if-suffix-and-prefix-of-a-string-are-palindromes/)

给定一个字符串，任务是检查该字符串是否有长度大于 1 的前缀和后缀子串，这些子串是回文。
如果满足上述条件，则打印“是”，否则打印“否”。
**例:**

```
Input : s = abartbb
Output : YES
Explanation : The string has prefix substring 'aba' 
and suffix substring 'bb' which are both palindromes, so the output is 'YES'.

Input : s = abcc
Output : NO
Explanation : The string has no prefix substring which is palindrome, 
it only has a suffix substring 'cc' which is a palindrome. 
So the output is 'NO'.
```

**进场:**

*   首先，检查所有长度大于 1 的前缀子串，看看是否有回文。
*   检查所有后缀子字符串。
*   如果两个条件都为真，则输出为“是”。
*   否则，输出为“否”。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// the string is a palindrome
bool isPalindrome(string r)
{
    string p = r;

    // reverse the string to
    // compare with the
    // original string
    reverse(p.begin(), p.end());

    // check if both are same
    return (r == p);
}

// Function to check whether the string
// has prefix and suffix substrings
// of length greater than 1
// which are palindromes.
bool CheckStr(string s)
{
    int l = s.length();

    // check all prefix substrings
    int i;
    for (i = 2; i <= l; i++) {

        // check if the prefix substring
        // is a palindrome
        if (isPalindrome(s.substr(0, i)))
           break;
    }

    // If we did not find any palindrome prefix
    // of length greater than 1.
    if (i == (l+1))
      return false;

    // check all suffix substrings,
    // as the string is reversed now
    i = 2;
    for (i = 2; i <= l; i++) {

        // check if the suffix substring
        // is a palindrome
        if (isPalindrome(s.substr(l-i, i)))
            return true;
    }

    // If we did not find a suffix
    return false;   
}

// Driver code
int main()
{
    string s = "abccbarfgdbd";
    if (CheckStr(s))
        cout << "YES\n";
    else
        cout << "NO\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static String reverse(String input)
    {
        char[] a = input.toCharArray();
        int l, r = 0;
        r = a.length - 1;
        for (l = 0; l < r; l++, r--)
        {
            // Swap values of l and r
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.valueOf(a);
    }

    // Function to check whether
    // the string is a palindrome
    static boolean isPalindrome(String r)
    {
        String p = r;

        // reverse the string to
        // compare with the
        // original string
        p = reverse(p);

        // check if both are same
        return (r.equals(p));
    }

    // Function to check whether the string
    // has prefix and suffix substrings
    // of length greater than 1
    // which are palindromes.
    static boolean CheckStr(String s)
    {
        int l = s.length();

        // check all prefix substrings
        int i;
        for (i = 2; i <= l; i++)
        {

            // check if the prefix substring
            // is a palindrome
            if (isPalindrome(s.substring(0, i)))
            {
                break;
            }
        }

        // If we did not find any palindrome prefix
        // of length greater than 1.
        if (i == (l + 1))
        {
            return false;
        }

        // check all suffix substrings,
        // as the string is reversed now
        i = 2;
        for (i = 2; i <=l; i++)
        {

            // check if the suffix substring
            // is a palindrome
            if (isPalindrome(s.substring(l-i,l)))
            {
                return true;
            }
        }

        // If we did not find a suffix
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "abccbarfgdbd";
        if (CheckStr(s))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check whether
# the string is a palindrome
def isPalindrome(r):

    # Reverse the string and assign
    # it to new variable for comparison
    p = r[::-1]

    # check if both are same
    return r == p

# Function to check whether the string
# has prefix and suffix substrings
# of length greater than 1
# which are palindromes.
def CheckStr(s):

    l = len(s)

    # check all prefix substrings
    i = 0
    for i in range(2, l + 1):

        # check if the prefix substring
        # is a palindrome
        if isPalindrome(s[0:i]) == True:
            break

    # If we did not find any palindrome
    # prefix of length greater than 1.
    if i == (l + 1):
        return False

    # check all suffix substrings,
    # as the string is reversed now
    for i in range(2, l + 1):

        # check if the suffix substring
        # is a palindrome
        if isPalindrome(s[l - i : l]) == True:
            return True

    # If we did not find a suffix
    return False   

# Driver code
if __name__ == "__main__":

    s = "abccbarfgdbd"

    if CheckStr(s) == True:
        print("YES")
    else:
        print("NO")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static String reverse(String input)
    {
        char[] a = input.ToCharArray();
        int l, r = 0;
        r = a.Length - 1;
        for (l = 0; l < r; l++, r--)
        {
            // Swap values of l and r
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.Join("",a);
    }

    // Function to check whether
    // the string is a palindrome
    static Boolean isPalindrome(String r)
    {
        String p = r;

        // reverse the string to
        // compare with the
        // original string
        p = reverse(p);

        // check if both are same
        return (r.Equals(p));
    }

    // Function to check whether the string
    // has prefix and suffix substrings
    // of length greater than 1
    // which are palindromes.
    static Boolean CheckStr(String s)
    {
        int l = s.Length;

        // check all prefix substrings
        int i;
        for (i = 2; i <= l; i++)
        {

            // check if the prefix substring
            // is a palindrome
            if (isPalindrome(s.Substring(0, i)))
            {
                break;
            }
        }

        // If we did not find any palindrome prefix
        // of length greater than 1.
        if (i == (l + 1))
        {
            return false;
        }

        // check all suffix substrings,
        // as the string is reversed now
        i = 2;
        for (i = 2; i <=l; i++)
        {

            // check if the suffix substring
            // is a palindrome
            if (isPalindrome(s.Substring(l-i,i)))
            {
                return true;
            }
        }

        // If we did not find a suffix
        return false;
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "abccbarfgdbd";
        if (CheckStr(s))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to check whether
// the string is a palindrome
function isPalindrome($r)
{
    $p = $r;

    // reverse the string to
    // compare with the
    // original string
    strrev($p);

    // check if both are same
    return ($r == $p);
}

// Function to check whether the
// string has prefix and suffix
// substrings of length greater
// than 1 which are palindromes.
function CheckStr($s)
{
    $l = strlen($s);

    // check all prefix substrings
    for ($i = 2; $i <= $l; $i++)
    {

        // check if the prefix substring
        // is a palindrome
        if (isPalindrome(substr($s, 0, $i)))
        break;
    }

    // If we did not find any palindrome
    // prefix of length greater than 1.
    if ($i == ($l + 1))
    return false;

    // check all suffix substrings,
    // as the string is reversed now
    $i = 2;
    for ($i = 2; $i <= $l; $i++)
    {

        // check if the suffix substring
        // is a palindrome
        if (isPalindrome(substr($s, $l -
                                $i, $i)))
            return true;
    }

    // If we did not find a suffix
    return false;
}

// Driver code
$s = "abccbarfgdbd";
if (CheckStr($s))
    echo ("YES\n");
else
    echo ("NO\n");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to check whether
// the string is a palindrome
function isPalindrome(r)
{
    var p = r;

    // reverse the string to
    // compare with the
    // original string
    p.split('').reverse().join('');

    // check if both are same
    return (r == p);
}

// Function to check whether the string
// has prefix and suffix substrings
// of length greater than 1
// which are palindromes.
function CheckStr( s)
{
    var l = s.length;

    // check all prefix substrings
    var i;
    for (i = 2; i <= l; i++) {

        // check if the prefix substring
        // is a palindrome
        if (isPalindrome(s.substring(0, i)))
           break;
    }

    // If we did not find any palindrome prefix
    // of length greater than 1.
    if (i == (l+1))
      return false;

    // check all suffix substrings,
    // as the string is reversed now
    i = 2;
    for (i = 2; i <= l; i++) {

        // check if the suffix substring
        // is a palindrome
        if (isPalindrome(s.substring(l-i, l)))
            return true;
    }

    // If we did not find a suffix
    return false;   
}

// Driver code
var s = "abccbarfgdbd";
if (CheckStr(s))
    document.write( "YES");
else
    document.write( "NO");

</script>
```

**Output:** 

```
YES
```

**复杂度:O(n^2)**