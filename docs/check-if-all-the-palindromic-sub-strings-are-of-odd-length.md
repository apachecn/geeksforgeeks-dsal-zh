# 检查是否所有回文子串都是奇数长度

> 原文:[https://www . geeksforgeeks . org/check-如果所有回文子串都是奇数长度/](https://www.geeksforgeeks.org/check-if-all-the-palindromic-sub-strings-are-of-odd-length/)

给定一个字符串，检查它的所有回文子字符串是否都是奇数长度。如果是，则打印“是”或“否”。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:** NO
> 因为，“ee”是一个偶数长度的回文子串。
> **输入:**str = " madamimum "
> **输出:**是

**蛮力进场:**

简单地说，遍历每个“s”的子串，检查它是否是回文。如果它是回文，那么它的长度一定是奇数。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits//stdc++.h>
using namespace std;

// Function to check if
// the string is palindrome
bool checkPalindrome(string s)
{
    for (int i = 0; i < s.length(); i++)
    {
        if(s[i] != s[s.length() - i - 1])
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
bool CheckOdd(string s)
{
int n = s.length();
for (int i = 0; i < n; i++)
{

    // Creating each substring
    string x = "";
    for (int j = i; j < n; j++)
    {
        x += s[j];

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.length() % 2 == 0 &&
        checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    if(CheckOdd(s))
        cout<<("YES");
    else
        cout<<("NO");
}
// This code is contributed by
// Sahil_shelangia
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to check if
// the string is palindrome
static boolean checkPalindrome(String s)
{
    for (int i = 0; i < s.length(); i++)
    {
        if(s.charAt(i) != s.charAt(s.length() - i - 1))
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
static boolean CheckOdd(String s)
{
int n = s.length();
for (int i = 0; i < n; i++)
{

    // Creating each substring
    String x = "";
    for (int j = i; j < n; j++)
    {
        x += s.charAt(j);

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.length() % 2 == 0 &&
        checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
public static void main(String args[])
{
    String s = "geeksforgeeks";
    if(CheckOdd(s))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed
// by Arnab Kundu
```

## 计算机编程语言

```
# Python implementation of the approach

# Function to check if
# the string is palindrome

def checkPalindrome(s):
    for i in range(len(s)):
        if(s[i] != s[len(s)-i-1]):
            return False
    return True

# Function that checks whether
# all the palindromic
# sub-strings are of odd length.

def CheckOdd(s):
    n = len(s)
    for i in range(n):

        # Creating each substring
        x = ""
        for j in range(i, n):
            x += s[j]
            # If the sub-string is
            # of even length and
            # is a palindrome then,
            # we return False
            if(len(x) % 2 == 0
                    and checkPalindrome(x) == True):
                return False
    return True

# Driver code
s = "geeksforgeeks"
if(CheckOdd(s)):
    print("YES")
else:
    print("NO")
```

## C#

```
// C# implementation of the approach
using System;

public class GFG {

// Function to check if
// the string is palindrome
static bool checkPalindrome(String s)
{
    for (int i = 0; i < s.Length; i++)
    {
        if(s[i] != s[(s.Length - i - 1)])
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
static bool CheckOdd(String s)
{
int n = s.Length;
for (int i = 0; i < n; i++)
{

    // Creating each substring
    String x = "";
    for (int j = i; j < n; j++)
    {
        x += s[j];

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.Length % 2 == 0 &&
        checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
public static void Main()
{
    String s = "geeksforgeeks";
    if(CheckOdd(s))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

/* This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to check if the string
// is palindrome
function checkPalindrome($s)
{
    for ($i = 0; $i < strlen($s); $i++)
    {
        if($s[$i] != $s[strlen($s) - $i - 1])
            return false;
    }
    return true;
}

// Function that checks whether all the
// palindromic sub-strings are of odd length.
function CheckOdd($s)
{
    $n = strlen($s);
    for ($i = 0; $i < $n; $i++)
    {

        // Creating each substring
        $x = "";
        for ($j = $i; $j < $n; $j++)
        {
            $x = $x.$s[$i];

            // If the sub-string is
            // of even length and
            // is a palindrome then,
            // we return False
            if(strlen($x) % 2 == 0 &&
            checkPalindrome($x) == true)
                return false;
        }
    }

    return true;
}

// Driver code
$s = "geeksforgeeks";
if(CheckOdd($s))
    echo "YES";
else
    echo "NO";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to check if
// the string is palindrome
function checkPalindrome(s)
{
    for (let i = 0; i < s.length; i++)
    {
        if(s[i] != s[s.length - i - 1])
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
function CheckOdd(s)
{
    let n = s.length;
for (let i = 0; i < n; i++)
{

    // Creating each substring
    let x = "";
    for (let j = i; j < n; j++)
    {
        x += s[j];

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.length % 2 == 0 &&
        checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
let s = "geeksforgeeks";
if(CheckOdd(s))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
NO
```

**高效方法:**为了检查 s 的所有回文子串是否都具有奇数长度，我们可以搜索它的偶数长度回文子串。我们知道每个偶数长度回文至少有两个相同的连续字符(例如 cxxa，ee)。因此，我们可以一次检查两个连续的字符，看看它们是否相同。如果是，那么 s 有一个偶数长度的回文子串，因此输出将是 NO，如果我们没有找到偶数长度的子串，答案将是 YES。

我们可以在一次字符串遍历后完成这个检查。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits//stdc++.h>
using namespace std;

// Function that checks whether s
// contains a even length palindromic
// sub-strings or not.
bool CheckEven(string s)
{
  for (int i = 1; i < s.size(); ++i) {
        if (s[i] == s[i - 1]) {
            return true;
        }
    }
    return false;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    if(CheckEven(s)==false)
        cout<<("YES");
    else
        cout<<("NO");
}
// This code is contributed by
// Aditya Jaiswal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to check if
// the string is palindrome
static boolean checkPalindrome(String s)
{
    for (int i = 0; i < s.length(); i++)
    {
        if(s.charAt(i) != s.charAt(s.length() - i - 1))
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
static boolean CheckOdd(String s)
{
int n = s.length();
for (int i = 0; i < n; i++)
{

    // Creating each substring
    String x = "";
    for (int j = i; j < n; j++)
    {
        x += s.charAt(j);

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.length() % 2 == 0 &&
           checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
public static void main(String args[])
{
    String s = "geeksforgeeks";
    if(CheckOdd(s))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to check if
# the string is palindrome
def checkPalindrome(s):
    for i in range(len(s)):
        if(s[i] != s[len(s)-i-1]):
            return False
    return True

# Function that checks whether
# all the palindromic
# sub-strings are of odd length.
def CheckOdd(s):
    n = len(s)
    for i in range(n):

        # Creating each substring
        x = ""
        for j in range(i, n):
            x += s[j]
            # If the sub-string is
            # of even length and
            # is a palindrome then,
            # we return False
            if(len(x)% 2 == 0
                  and checkPalindrome(x) == True):
                return False
    return True

# Driver code
s = "geeksforgeeks"
if(CheckOdd(s)):
    print("YES")
else:
    print("NO")
```

## C#

```
// C# implementation of the approach
using System;

public class GFG {

// Function to check if
// the string is palindrome
static bool checkPalindrome(String s)
{
    for (int i = 0; i < s.Length; i++)
    {
        if(s[i] != s[(s.Length - i - 1)])
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
static bool CheckOdd(String s)
{
int n = s.Length;
for (int i = 0; i < n; i++)
{

    // Creating each substring
    String x = "";
    for (int j = i; j < n; j++)
    {
        x += s[j];

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.Length % 2 == 0 &&
           checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
public static void Main()
{
    String s = "geeksforgeeks";
    if(CheckOdd(s))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

/* This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to check if the string
// is palindrome
function checkPalindrome($s)
{
    for ($i = 0; $i < strlen($s); $i++)
    {
        if($s[$i] != $s[strlen($s) - $i - 1])
            return false;
    }
    return true;
}

// Function that checks whether all the
// palindromic sub-strings are of odd length.
function CheckOdd($s)
{
    $n = strlen($s);
    for ($i = 0; $i < $n; $i++)
    {

        // Creating each substring
        $x = "";
        for ($j = $i; $j < $n; $j++)
        {
            $x = $x.$s[$i];

            // If the sub-string is
            // of even length and
            // is a palindrome then,
            // we return False
            if(strlen($x) % 2 == 0 &&
            checkPalindrome($x) == true)
                return false;
        }
    }

    return true;
}

// Driver code
$s = "geeksforgeeks";
if(CheckOdd($s))
    echo "YES";
else
    echo "NO";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to check if
// the string is palindrome
function  checkPalindrome(s)
{
    for (let i = 0; i < s.length; i++)
    {
        if(s[i] != s[(s.length - i - 1)])
            return false;
    }
    return true;
}

// Function that checks whether
// all the palindromic
// sub-strings are of odd length.
function CheckOdd(s)
{
    let n = s.length;
for (let i = 0; i < n; i++)
{

    // Creating each substring
    let x = "";
    for (let j = i; j < n; j++)
    {
        x += s[j];

        // If the sub-string is
        // of even length and
        // is a palindrome then,
        // we return False
        if(x.length % 2 == 0 &&
           checkPalindrome(x) == true)
            return false;
        }
    }

    return true;
}

// Driver code
let s = "geeksforgeeks";
if(CheckOdd(s))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
NO
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)