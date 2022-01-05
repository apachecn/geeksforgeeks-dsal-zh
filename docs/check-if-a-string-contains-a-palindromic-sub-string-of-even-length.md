# 检查字符串是否包含偶数长度的回文子串

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-a-回文-偶长度子串/](https://www.geeksforgeeks.org/check-if-a-string-contains-a-palindromic-sub-string-of-even-length/)

s 是只包含小写英文字母的字符串。我们需要找到是否至少存在一个长度为偶数的回文子串。

**示例:**

```
Input  : aassss
Output : YES

Input  : gfg
Output : NO
```

注意**甚至**长度的回文必须在中间包含两个相同的字母。所以我们只需要检查一下这种情况。如果我们在字符串中找到两个连续的相同字母，那么我们输出“是”，否则输出“否”。

下面是实现:

## C++

```
// C++ program to check if there is a substring
// palindrome of even length.
#include <bits/stdc++.h>
using namespace std;

// function to check if two consecutive same
// characters are present
bool check(string s)
{
    for (int i = 0; i < s.length() - 1; i++)
        if (s[i] == s[i + 1])
            return true;
    return false;
}

int main()
{
    string s = "xzyyz";
    if (check(s))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there is a substring
// palindrome of even length.

class GFG {

// function to check if two consecutive same
// characters are present
static boolean check(String s)
{
    for (int i = 0; i < s.length() - 1; i++)
        if (s.charAt(i) == s.charAt(i+1))
            return true;
    return false;
}

// Driver Code
    public static void main(String[] args) {

        String s = "xzyyz";
    if (check(s))
              System.out.println("YES");
    else
        System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check if there is
# a substring palindrome of even length.

# function to check if two consecutive
# same characters are present
def check(s):

    for i in range (0, len(s)):
        if (s[i] == s[i + 1]):
            return True

    return False

# Driver Code
s = "xzyyz"
if(check(s)):
    print("YES")
else:
    print("NO")

# This code is contributed
# by iAyushRAJ
```

## C#

```
// C# program to check if there is a substring
// palindrome of even length.
using System;
public class GFG {

// function to check if two consecutive same
// characters are present
static bool check(String s)
{
    for (int i = 0; i < s.Length - 1; i++)
        if (s[i] == s[i+1])
            return true;
    return false;
}

// Driver Code
    public static void Main() {

        String s = "xzyyz";
    if (check(s))
              Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if there is a
// substring palindrome of even length.

// function to check if two consecutive
// same characters are present
function check($s)
{
    for ($i = 0; $i < strlen($s) - 1; $i++)
        if ($s[$i] == $s[$i + 1])
            return true;
    return false;
}

// Driver Code
$s = "xzyyz";
if (check($s))
    echo "YES","\n";
else
    echo "NO" ,"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to check if there is
// a substring palindrome of even length.

// Function to check if two consecutive same
// characters are present
function check(s)
{
    for(let i = 0; i < s.length - 1; i++)
        if (s[i] == s[i + 1])
            return true;

    return false;
}

// Driver code
let s = "xzyyz";
if (check(s))
      document.write("YES");
else
    document.write("NO");

// This code is contributed by suresh07

</script>
```

**Output:** 

```
YES
```