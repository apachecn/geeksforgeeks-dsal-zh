# 检查字符串中是否存在非回文的子序列

> 原文:[https://www . geesforgeks . org/check-if-exist-any-sub-sequence-in-a-string-is-not-回文/](https://www.geeksforgeeks.org/check-if-there-exists-any-sub-sequence-in-a-string-which-is-not-palindrome/)

给定一串小写英文字母。任务是检查字符串中是否存在非回文的子序列。如果至少有一个子序列不是回文，则打印“是”，否则打印“否”
**示例** :

```
Input : str = "abaab"
Output : YES
Subsequences "ab" or "abaa" or "aab", are not palindrome.

Input : str = "zzzz"
Output : NO
All possible subsequences are palindrome.
```

主要的观察是，如果字符串包含至少两个不同的字符，那么总会有一个长度至少为 2 的子序列，它不是回文。只有当字符串的所有字符都相同时，才不会有任何子序列不是回文。因为以最佳方式，我们可以从一个字符串中选择任意两个不同的字符，并将它们以相同的顺序一个接一个地放置，以形成一个非回文字符串。
以下是上述方法的实施:

## C++

```
// C++ program to check if there exists
// at least 1 sub-sequence in a string
// which is not palindrome

#include <bits/stdc++.h>
using namespace std;

// Function to check if there exists
// at least 1 sub-sequence in a string
// which is not palindrome
bool isAnyNotPalindrome(string s)
{
    // use set to count number of
    // distinct characters
    set<char> unique;

    // insert each character in set
    for (int i = 0; i < s.length(); i++)
        unique.insert(s[i]);

    // If there is more than 1 unique
    // characters, return true
    if (unique.size() > 1)
        return true;
    // Else, return false
    else
        return false;
}

// Driver code
int main()
{
    string s = "aaaaab";

    if (isAnyNotPalindrome(s))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there exists
// at least 1 sub-sequence in a string
// which is not palindrome

import java.util.*;
class GFG
{

    // Function to check if there exists
    // at least 1 sub-sequence in a string
    // which is not palindrome
    static boolean isAnyNotPalindrome(String s)
    {
        // use set to count number of
        // distinct characters
        Set<Character> unique=new HashSet<Character>();

        // insert each character in set
        for (int i = 0; i < s.length(); i++)
            unique.add(s.charAt(i));

        // If there is more than 1 unique
        // characters, return true
        if (unique.size() > 1)
            return true;
        // Else, return false
        else
            return false;
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "aaaaab";

        if (isAnyNotPalindrome(s))
            System.out.println("YES");
        else
            System.out.println("NO");

    }
}
```

## 蟒蛇 3

```
# Python3 program to check if there exists
# at least 1 sub-sequence in a string
# which is not palindrome

# Function to check if there exists
# at least 1 sub-sequence in a string
# which is not palindrome
def isAnyNotPalindrome(s):

    # use set to count number of
    # distinct characters
    unique=set()

    # insert each character in set
    for i in range(0,len(s)):
        unique.add(s[i])

    # If there is more than 1 unique
    # characters, return true
    if (len(unique) > 1):
        return True

    # Else, return false
    else:
        return False

# Driver code
if __name__=='__main__':
    s = "aaaaab"

    if (isAnyNotPalindrome(s)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# ihritik
```

## C#

```
// C# program to check if there exists
// at least 1 sub-sequence in a string
// which is not palindrome
using System;
using System.Collections.Generic;

class GFG
{

    // Function to check if there exists
    // at least 1 sub-sequence in a string
    // which is not palindrome
    static bool isAnyNotPalindrome(String s)
    {
        // use set to count number of
        // distinct characters
        HashSet<char> unique=new HashSet<char>();

        // insert each character in set
        for (int i = 0; i < s.Length; i++)
            unique.Add(s[i]);

        // If there is more than 1 unique
        // characters, return true
        if (unique.Count > 1)
            return true;
        // Else, return false
        else
            return false;
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "aaaaab";

        if (isAnyNotPalindrome(s))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to check if there exists
// at least 1 sub-sequence in a string
// which is not palindrome

// Function to check if there exists
// at least 1 sub-sequence in a string
// which is not palindrome
function isAnyNotPalindrome(s)
{
    // use set to count number of
    // distinct characters
    var unique = new Set();

    // insert each character in set
    for (var i = 0; i < s.length; i++)
        unique.add(s[i]);

    // If there is more than 1 unique
    // characters, return true
    if (unique.size > 1)
        return true;
    // Else, return false
    else
        return false;
}

// Driver code
var s = "aaaaab";
if (isAnyNotPalindrome(s))
    document.write( "YES");
else
    document.write( "NO");

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N * logN)，其中 N 为字符串长度。
***辅助空间:*** O(N)