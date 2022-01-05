# 检查两个给定字符串的分裂子串的连接是否形成回文

> 原文:[https://www . geesforgeks . org/check-if-concation-of-splited-substrings-of-two-给定字符串-forms-a-回文-or-not/](https://www.geeksforgeeks.org/check-if-concatenation-of-splitted-substrings-of-two-given-strings-forms-a-palindrome-or-not/)

给定两个长度相同的字符串 **a** 和 **b** ，任务是检查是否将两个字符串拆分并连接它们相反的子字符串，即把 **a** 的左子字符串与 **b** 的右子字符串连接起来，或者把 **b** 的左子字符串与 **a** 、[的右子字符串连接起来是否形成回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。如果发现是真的打印**“是”**。否则，打印**“否”**。

***注意:**其中一个拆分的子串可以为空。*

**示例:**

> **输入:** a = "x "，b = "y"
> **输出:**是
> **解释:**
> 在索引 0 处拆分两个字符串。
> a 的左子串(aLeft) =“”，a 的右子串(aRight)=“x”
> b 的左子串(bLeft) =“”，b 的右子串(bRight)=“y”
> 既然 aLeft+bRight =“+”y”=“y”，这是回文以及 bLeft+aRight =“+”x”=“x”也是回文，打印 Yes。
> 
> **输入:**a =“ula CFD”，b =“jizalu”
> **输出:**真
> **解释:**
> 在索引 3 处拆分两个字符串:
> a(aLeft)=“ula”的左子字符串，a(aRight)=“CFD”
> 的右子字符串，b(bLeft)=“jiz”的左子字符串，b(bRight)=“alu”
> 因为 aLeft+bRight =“ula”+“alu”

**方法:**思路是用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决这个问题。按照以下步骤解决问题:

1.  将指针 **i** 放在 **0 <sup>第</sup>T5**a**的索引处，将**j**放在 **b** 的最后一个索引处。**
2.  [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，检查 **a[i] == b[j]** ，然后递增 **i** 并递减 **j** 。
3.  否则，只要打破循环，因为它不是回文型序列。
4.  在一个字符串变量 **xa** 中连接 **aLeft** 和 **bRight** ，在另一个字符串变量 **xb** 中连接**right**和 **bLeft** 。
5.  检查两个字符串中是否有一个是回文。如果发现是真的，打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if concatenating
// opposite substrings after splitting
// two given strings forms a palindrome
// or not
bool checkSplitting(string a, string b)
{

    // Length of the string
    int len = a.length();
    int i = 0, j = len - 1;

    // Iterate through the strings
    while (i < len)
    {

        // If not a palindrome sequence
        if (a[i] != b[j])
        {
            break;
        }
        i += 1;
        j -= 1;

        // Concatenate left substring of a
        // and right substring of b in xa
        // Concatenate right substring of a
        // and left substring of b in xb
        string xa = a.substr(i, j + 1);
        string xb = b.substr(i, j + 1);

        // Check if either of the two concatenated
        // strings is a palindrom or not
        if (xa == string(xa.rbegin(), xa.rend()) ||
            xb == string(xb.rbegin(), xb.rend()))
            return true;
    }
}

// Function to check if concatenation of splitted
// substrings of two given strings forms a palindrome
void isSplitPossible(string a, string b)
{
    if (checkSplitting(a, b) == true)
    {
        cout << "Yes";
    }
    else if (checkSplitting(b, a) == true)
    {
        cout << "Yes";
    }
    else
    {
        cout << "No";
    }
}

// Driver Code
int main()
{
    string a = "ulacfd", b = "jizalu";

    // Function Call
    isSplitPossible(a, b);

    return 0;
}

// This code is contributed by pushpendrayadav1057
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if concatenating
// opposite subStrings after splitting
// two given Strings forms a palindrome
// or not
static boolean checkSplitting(String a, String b)
{

    // Length of the String
    int len = a.length();
    int i = 0, j = len - 1;

    // Iterate through the Strings
    while (i < len)
    {

        // If not a palindrome sequence
        if (a.charAt(i) != b.charAt(j))
        {
            break;
        }
        i += 1;
        j -= 1;

        // Concatenate left subString of a
        // and right subString of b in xa
        // Concatenate right subString of a
        // and left subString of b in xb
        String xa = a.substring(i, j + 1);
        String xb = b.substring(i, j + 1);

        // Check if either of the two concatenated
        // Strings is a palindrom or not
        if (xa.equals(reverse(xa))||xb.equals(reverse(xb)))
            return true;
    }
    return false;
}

// Function to check if concatenation of splitted
// subStrings of two given Strings forms a palindrome
static void isSplitPossible(String a, String b)
{
    if (checkSplitting(a, b) == true)
    {
        System.out.print("Yes");
    }
    else if (checkSplitting(b, a) == true)
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{
    String a = "ulacfd", b = "jizalu";

    // Function Call
    isSplitPossible(a, b);   
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if concatenating
# opposite substrings after splitting
# two given strings forms a palindrome or not
def checkSplitting(a, b, n):
    i, j = 0, n - 1

    # Iterate through the strings
    while(i < n):

        # If not a palindrome sequence
        if(a[i] != b[j]):
            break
        i += 1
        j -= 1

        # Concatenate left substring of a
        # and right substring of b in xa
        # Concatenate right substring of a
        # and left substring of b in xb
        xa = a[i:j + 1]
        xb = b[i:j + 1]

        # Check if either of the two concatenated
        # strings is a palindrom or not
        if(xa == xa[::-1] or xb == xb[::-1]):
            return True

# Function to check if concatenation of splitted
# substrings of two given strings forms a palindrome
def isSplitPossible(a, b):
    if checkSplitting(a, b, len(a)) == True:
        print("Yes")

    elif checkSplitting(b, a, len(a)) == True:
        print("Yes")

    else:
        print("No")

# Given string a and b
a = "ulacfd"
b = "jizalu"

# Function Call
isSplitPossible(a, b)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if concatenating
// opposite subStrings after splitting
// two given Strings forms a palindrome
// or not
static bool checkSplitting(String a, String b)
{

    // Length of the String
    int len = a.Length;
    int i = 0, j = len - 1;

    // Iterate through the Strings
    while (i < len)
    {

        // If not a palindrome sequence
        if (a[i] != b[j])
        {
            break;
        }
        i += 1;
        j -= 1;

        // Concatenate left subString of a
        // and right subString of b in xa
        // Concatenate right subString of a
        // and left subString of b in xb
        String xa = a.Substring(i, j + 1 - i);
        String xb = b.Substring(i, j + 1 - i);

        // Check if either of the two concatenated
        // Strings is a palindrom or not
        if (xa.Equals(reverse(xa)) ||
            xb.Equals(reverse(xb)))
            return true;
    }
    return false;
}

// Function to check if concatenation of splitted
// subStrings of two given Strings forms a palindrome
static void isSplitPossible(String a, String b)
{
    if (checkSplitting(a, b) == true)
    {
        Console.Write("Yes");
    }
    else if (checkSplitting(b, a) == true)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{
    String a = "ulacfd", b = "jizalu";

    // Function Call
    isSplitPossible(a, b);   
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if the string is palindrome or not

function checkPalindrome(str) {

    // find the length of a string
    var len = str.length;

    // loop through half of the string
    for (var i = 0; i < parseInt(len / 2); i++) {

        // check if first and last string are same
        if (str[i] !== str[len - 1 - i]) {
            return false;
        }
    }
    return true;
}

// Function to check if concatenating
// opposite substrings after splitting
// two given strings forms a palindrome
// or not
function checkSplitting(a, b)
{

    // Length of the string
    var len = a.length;
    var i = 0, j = len - 1;

    // Iterate through the strings
    while (i < len)
    {

        // If not a palindrome sequence
        if (a[i] != b[j])
        {
            break;
        }
        i += 1;
        j -= 1;

        // Concatenate left substring of a
        // and right substring of b in xa
        // Concatenate right substring of a
        // and left substring of b in xb
        var xa = a.substring(i, j + 1);
        var xb = b.substring(i, j + 1);

        // Check if either of the two concatenated
        // strings is a palindrom or not
        if (checkPalindrome(xa)==true || checkPalindrome(xb)==true)
            return true;
    }
}

// Function to check if concatenation of splitted
// substrings of two given strings forms a palindrome
function isSplitPossible(a, b)
{
    if (checkSplitting(a, b) == true)
    {
       document.write( "Yes");
    }
    else if (checkSplitting(b, a) == true)
    {
        document.write("Yes");
    }
    else
    {
        document.write( "No");
    }
}

var a = "ulacfd", b = "jizalu";

    // Function Call
    isSplitPossible(a, b);

// This code is contributed by SoumikMondal

</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)