# 给定字符串的置换，最大化回文子字符串的计数

> 原文:[https://www . geeksforgeeks . org/最大化回文子串计数的给定字符串排列/](https://www.geeksforgeeks.org/permutation-of-given-string-that-maximizes-count-of-palindromic-substrings/)

给定一个字符串 **S** ，任务是找到该字符串的排列，使得该字符串中的回文子字符串最大。
**注:**每个字符串可以有多个答案。
**例:**

> **输入:** S = "abcb"
> **输出:**【abbc】
> **说明:**
> 【abbc】是回文子串数量最多的字符串。
> 回文子串为–{“a”、“b”、“b”、“c”、“abbc”}
> **输入:** S = "oolol"
> **输出:**【奥洛洛】

**方法:**想法是[对字符串](https://www.geeksforgeeks.org/sort-string-characters/)的字符进行排序，使得单独和一起形成一个回文子串，这将最大化字符串排列的总[回文子串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// permutation of the given string
// such that palindromic substrings
// is maximum in the string

#include <bits/stdc++.h>
using namespace std;

// Function to find the permutation
// of the string such that the
// palindromic substrings are maximum
string maxPalindromicSubstring(string s){

    // Sorting the characters of  the
    // given string
    sort(s.begin(), s.end());

    cout << s;

    return s;
}

// Driver Code
int main()
{
    // String s
    string s = "abcb";

    // Function Call
    maxPalindromicSubstring(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// permutation of the given string
// such that palindromic substrings
// is maximum in the string
import java.io.*;
import java.util.*;

class GFG {

// Function to find the permutation
// of the string such that the
// palindromic substrings are maximum
static String maxPalindromicSubstring(String s)
{

    // Convert input string to char array
    char tempArray[] = s.toCharArray();

    // Sorting the characters of the
    // given string
    Arrays.sort(tempArray);

    System.out.println(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver code
public static void main(String[] args)
{

    // String s
    String s = "abcb";

    // Function Call
    maxPalindromicSubstring(s);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 implementation to find the
# permutation of the given string
# such that palindromic substrings
# is maximum in the string

# Function to find the permutation
# of the string such that the
# palindromic substrings are maximum
def maxPalindromicSubstring(s):

    # Sorting the characters of the
    # given string
    res = ''.join(sorted(s))
    s = str(res)

    print(s)

# Driver Code
if __name__ == '__main__':

    # String s
    s = "abcb"

    # Function Call
    maxPalindromicSubstring(s)

# This code is contributed by BhupendraSingh
```

## C#

```
// C# implementation to find the
// permutation of the given string
// such that palindromic substrings
// is maximum in the string
using System;
class GFG{

// Function to find the permutation
// of the string such that the
// palindromic substrings are maximum
static String maxPalindromicSubstring(String s)
{

    // Convert input string to char array
    char []tempArray = s.ToCharArray();

    // Sorting the characters of the
    // given string
    Array.Sort(tempArray);

    Console.WriteLine(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver code
public static void Main()
{

    // String s
    String s = "abcb";

    // Function Call
    maxPalindromicSubstring(s);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// permutation of the given string
// such that palindromic substrings
// is maximum in the string

// Function to find the permutation
// of the string such that the
// palindromic substrings are maximum
function maxPalindromicSubstring(s){

    // Sorting the characters of  the
    // given string
    s.sort();

    document.write(s.join(""))

    return s;
}

// Driver Code
// String s
var s = "abcb".split('');

// Function Call
maxPalindromicSubstring(s);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
abbc
```