# 检查给定的字符串是否是奇怪的回文

> 原文:[https://www . geesforgeks . org/check-given-string-is-奇怪的是-回文-or-not/](https://www.geeksforgeeks.org/check-given-string-is-oddly-palindrome-or-not/)

给定字符串 **str** ，任务是检查 **str** 奇数索引处的字符是否构成回文字符串。如果不是，则打印**“否”**否则打印**“是”**。
**举例:**

> **输入:** str = "osafdfgsg "，N = 9
> **输出:**是
> **说明:**
> 奇数索引字符为= { s，f，f，s }
> 所以会做成回文串，“sffs”。
> **输入:** str = "addwfefwkll "，N = 11
> **输出:** No
> **说明:**
> 奇数索引字符为= {d，w，e，w，l}
> 所以不会做成回文串，【dwewl】

**天真方法:**天真方法是通过附加给定字符串的奇数索引字符来创建新字符串。然后，简单地检查形成的字符串是否是回文。如果字符串是回文，则打印**“是”**否则打印**“否”**。
以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the string str
// is palindromic or not
bool isPalindrome(string str)
{

    // Iterate the string str from left
    // and right pointers
    int l = 0;
    int h = str.size() - 1;

    // Keep comparing characters
    // while they are same
    while (h > l) {

        // If they are not same
        // then return false
        if (str[l++] != str[h--]) {
            return false;
        }
    }

    // Return true if the string is
    // palindromic
    return true;
}

// Function to make string using odd
// indices of string str
string makeOddString(string str)
{
    string odd = "";
    for (int i = 1; i < str.size();
         i += 2) {
        odd += str[i];
    }

    return odd;
}

// Functions checks if characters at
// odd index of the string forms
// palindrome or not
void checkOddlyPalindrome(string str)
{

    // Make odd indexed string
    string odd = makeOddString(str);

    // Check for Palindrome
    if (isPalindrome(odd))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    // Given string
    string str = "ddwfefwde";

    // Function Call
    checkOddlyPalindrome(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the String str
// is palindromic or not
public static boolean isPalindrome(String str)
{

    // Iterate the String str from left
    // and right pointers
    int l = 0;
    int h = str.length() - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
    {

        // If they are not same
        // then return false
        if (str.charAt(l) != str.charAt(h))
        {
            return false;
        }

        l++;
        h--;
    }

    // Return true if the String is
    // palindromic
    return true;
}

// Function to make String using odd
// indices of String str
public static String makeOddString(String str)
{
    String odd = "";

    for(int i = 1; i < str.length(); i += 2)
    {
       odd += str.charAt(i);
    }
    return odd;
}

// Functions checks if characters at
// odd index of the String forms
// palindrome or not
public static void checkOddlyPalindrome(String str)
{

    // Make odd indexed String
    String odd = makeOddString(str);

    // Check for Palindrome
    if (isPalindrome(odd))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String []args)
{

    // Given String
    String str = "ddwfefwde";

    // Function Call
    checkOddlyPalindrome(str);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the string 
# str is palindromic or not
def isPalindrome(str):

    # Iterate the string str from
    # left and right pointers
    l = 0;
    h = len(str) - 1;

    # Keep comparing characters
    # while they are same
    while (h > l):

        # If they are not same
        # then return false
        if (str[l] != str[h]):
            return False;

        l += 1
        h -= 1

    # Return true if the string is
    # palindromic
    return True;

# Function to make string using odd
# indices of string str
def makeOddString(str):

    odd = "";
    for i in range(1, len(str), 2):
        odd += str[i];

    return odd;

# Functions checks if characters at
# odd index of the string forms
# palindrome or not
def checkOddlyPalindrome(str):

    # Make odd indexed string
    odd = makeOddString(str);

    # Check for Palindrome
    if (isPalindrome(odd)):
        print("Yes")
    else:
        print("No")

# Driver code

# Given string
str = "ddwfefwde";

# Function call
checkOddlyPalindrome(str);

# This code is contributed by grand_master
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the String str
// is palindromic or not
static bool isPalindrome(string str)
{

    // Iterate the String str from left
    // and right pointers
    int l = 0;
    int h = str.Length - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
    {

        // If they are not same
        // then return false
        if (str[l] != str[h])
        {
            return false;
        }

        l++;
        h--;
    }

    // Return true if the String is
    // palindromic
    return true;
}

// Function to make String using odd
// indices of String str
static string makeOddString(string str)
{
    string odd = "";

    for(int i = 1; i < str.Length; i += 2)
    {
        odd += str[i];
    }
    return odd;
}

// Functions checks if characters at
// odd index of the String forms
// palindrome or not
static void checkOddlyPalindrome(string str)
{

    // Make odd indexed String
    string odd = makeOddString(str);

    // Check for Palindrome
    if (isPalindrome(odd))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
static void Main()
{

    // Given String
    string str = "ddwfefwde";

    // Function Call
    checkOddlyPalindrome(str);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the string str
// is palindromic or not
function isPalindrome(str)
{

    // Iterate the string str from left
    // and right pointers
    var l = 0;
    var h = str.length - 1;

    // Keep comparing characters
    // while they are same
    while (h > l) {

        // If they are not same
        // then return false
        if (str[l++] != str[h--]) {
            return false;
        }
    }

    // Return true if the string is
    // palindromic
    return true;
}

// Function to make string using odd
// indices of string str
function makeOddString(str)
{
    var odd = "";
    for (var i = 1; i < str.length;
         i += 2) {
        odd += str[i];
    }

    return odd;
}

// Functions checks if characters at
// odd index of the string forms
// palindrome or not
function checkOddlyPalindrome(str)
{

    // Make odd indexed string
    var odd = makeOddString(str);

    // Check for Palindrome
    if (isPalindrome(odd))
        document.write( "Yes" );
    else
        document.write( "No" );
}

// Driver Code

// Given string
var str = "ddwfefwde";

// Function Call
checkOddlyPalindrome(str);

// This code is contributed by itsok.
</script>
```

**Output:**

```
Yes
```

**时间复杂度:** *O(N)* ，N 是字符串的长度。
**辅助空间:** *O(N/2)*