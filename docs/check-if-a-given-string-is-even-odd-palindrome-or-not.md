# 检查给定字符串是否为奇偶回文

> 原文:[https://www . geesforgeks . org/check-if-a-给定字符串是否为奇偶回文/](https://www.geeksforgeeks.org/check-if-a-given-string-is-even-odd-palindrome-or-not/)

给定一个字符串**字符串**，任务是检查给定的字符串是否为**奇偶回文**。

> 一个**偶奇回文**串被定义为一个串，其偶索引处的字符形成一个回文，而奇索引处的字符也分别形成一个回文。

**例:**

> **输入:** str="abzzab"
> **输出:** YES
> **解释:**
> 奇数索引字符组成的字符串: **bzb** ，是回文。
> 由偶数索引的字符组成的字符串: **aza** ，是回文。
> 因此，给定的字符串是奇偶回文。
> **输入:** str="daccad"
> **输出:**否

**方法:**要解决这个问题，通过添加给定字符串的 ***【奇数索引字符】*** 来创建一个新字符串，并检查所形成的字符串是否回文。同样，检查 ***偶数索引字符*** 。如果两个字符串都是回文，则打印**“是”**。否则，打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the string
// str is palindromic or not
bool isPalindrome(string str)
{

    // Pointers to iterate the
    // string from both ends
    int l = 0;
    int h = str.size() - 1;

    while (h > l) {

        // If characters are found
        // to be distinct
        if (str[l++] != str[h--]) {
            return false;
        }
    }

    // Return true if the
    // string is palindromic
    return true;
}

// Function to generate string
// from characters at odd indices
string makeOddString(string str)
{
    string odd = "";
    for (int i = 1; i < str.size();
         i += 2) {
        odd += str[i];
    }

    return odd;
}

// Function to generate string
// from characters at even indices
string makeevenString(string str)
{
    string even = "";
    for (int i = 0; i < str.size();
         i += 2) {
        even += str[i];
    }

    return even;
}

// Functions to checks if string
// is Even-Odd Palindrome or not
void checkevenOddPalindrome(string str)
{

    // Generate odd indexed string
    string odd = makeOddString(str);

    // Generate even indexed string
    string even = makeevenString(str);

    // Check for Palindrome
    if (isPalindrome(odd)
        && isPalindrome(even))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    string str = "abzzab";

    checkevenOddPalindrome(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program implementation
// of the approach
import java.util.*;
import java.io.*;

class GFG{

// Function to check if the string
// str is palindromic or not
static boolean isPalindrome(String str)
{

    // Pointers to iterate the
    // string from both ends
    int l = 0;
    int h = str.length() - 1;

    while (h > l)
    {

        // If characters are found
        // to be distinct
        if (str.charAt(l++) !=
            str.charAt(h--))
            return false;
    }

    // Return true if the
    // string is palindromic
    return true;
}

// Function to generate string
// from characters at odd indices
static String makeOddString(String str)
{
    String odd = "";

    for(int i = 1; i < str.length(); i += 2)
    {
        odd += str.charAt(i);
    }

    return odd;
}

// Function to generate string
// from characters at even indices
static String makeevenString(String str)
{
    String even = "";

    for(int i = 0; i < str.length(); i += 2)
    {
        even += str.charAt(i);
    }

    return even;
}

// Functions to checks if string
// is Even-Odd Palindrome or not
static void checkevenOddPalindrome(String str)
{

    // Generate odd indexed string
    String odd = makeOddString(str);

    // Generate even indexed string
    String even = makeevenString(str);

    // Check for Palindrome
    if (isPalindrome(odd) && isPalindrome(even))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    String str = "abzzab";

    checkevenOddPalindrome(str);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if the string
# str is palindromic or not
def isPalindrome(Str):

    # Pointers to iterate the
    # string from both ends
    l = 0
    h = len(Str) - 1

    while (h > l):

        # If characters are found
        # to be distinct
        if (Str[l] != Str[h]):
            return False

        l += 1
        h -= 1

    # Return true if the
    # string is palindromic
    return True

# Function to generate string
# from characters at odd indices
def makeOddString(Str):

    odd = ""
    for i in range(1, len(Str), 2):
        odd += Str[i]

    return odd

# Function to generate string
# from characters at even indices
def makeevenString(Str):

    even = ""
    for i in range(0, len(Str), 2):
        even += Str[i]

    return even

# Functions to checks if string
# is Even-Odd Palindrome or not
def checkevenOddPalindrome(Str):

    # Generate odd indexed string
    odd = makeOddString(Str)

    # Generate even indexed string
    even = makeevenString(Str)

    # Check for Palindrome
    if (isPalindrome(odd) and
        isPalindrome(even)):
        print("Yes")
    else:
        print("No")

# Driver code
Str = "abzzab"

checkevenOddPalindrome(Str)

# This code is contributed by himanshu77
```

## C#

```
// C# program implementation
// of the approach
using System;

class GFG{

// Function to check if the string
// str is palindromic or not
static bool isPalindrome(string str)
{

    // Pointers to iterate the
    // string from both ends
    int l = 0;
    int h = str.Length - 1;

    while (h > l)
    {
        // If characters are found
        // to be distinct
        if (str[l++] != str[h--])
            return false;
    }

    // Return true if the
    // string is palindromic
    return true;
}

// Function to generate string
// from characters at odd indices
static string makeOddString(string str)
{
    string odd = "";

    for(int i = 1; i < str.Length; i += 2)
    {
        odd += str[i];
    }

    return odd;
}

// Function to generate string
// from characters at even indices
static string makeevenString(string str)
{
    string even = "";

    for(int i = 0; i < str.Length; i += 2)
    {
        even += str[i];
    }

    return even;
}

// Functions to checks if string
// is Even-Odd Palindrome or not
static void checkevenOddPalindrome(string str)
{

    // Generate odd indexed string
    string odd = makeOddString(str);

    // Generate even indexed string
    string even = makeevenString(str);

    // Check for Palindrome
    if (isPalindrome(odd) && isPalindrome(even))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
public static void Main()
{
    string str = "abzzab";

    checkevenOddPalindrome(str);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to check if the string
// str is palindromic or not
function isPalindrome(str)
{

    // Pointers to iterate the
    // string from both ends
    var l = 0;
    var h = str.length - 1;

    while (h > l)
    {

        // If characters are found
        // to be distinct
        if (str.charAt(l++) !=
            str.charAt(h--))
            return false;
    }

    // Return true if the
    // string is palindromic
    return true;
}

// Function to generate string
// from characters at odd indices
function makeOddString(str)
{
    var odd = "";

    for(var i = 1; i < str.length; i += 2)
    {
        odd += str.charAt(i);
    }
    return odd;
}

// Function to generate string
// from characters at even indices
function makeevenString(str)
{
    var even = "";

    for(var i = 0; i < str.length; i += 2)
    {
        even += str.charAt(i);
    }

    return even;
}

// Functions to checks if string
// is Even-Odd Palindrome or not
function checkevenOddPalindrome(str)
{

    // Generate odd indexed string
    var odd = makeOddString(str);

    // Generate even indexed string
    var even = makeevenString(str);

    // Check for Palindrome
    if (isPalindrome(odd) && isPalindrome(even))
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
var str = "abzzab";

checkevenOddPalindrome(str);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Yes
```