# 检查是否所有子串的元音数量至少与辅音数量相同

> 原文:[https://www . geesforgeks . org/check-all-the-substrings-with-number-of-元音-至少作为-of-辅音/](https://www.geeksforgeeks.org/check-whether-all-the-substrings-have-number-of-vowels-atleast-as-that-of-consonants/)

给定一个字符串 **str** ，任务是检查是否所有长度为 **≥ 2** 的子字符串的元音数至少与辅音数相同。
**例:**

> **输入:**str = " acaba "
> T3】输出: No
> 子串“cab”有 2 个辅音和一个单元音。
> **输入:** str = "aabaa"
> **输出:**是

**方法:**只有两种情况不满足给定条件:

1.  当有两个连续的辅音时，如在这种情况下，大小为 2 的子串可以有 2 个辅音，没有元音。
2.  当有一个元音被两个辅音包围时，在这种情况下，长度为 3 的子串可能有 2 个辅音和 1 个元音。

所有其他情况总是满足给定的条件。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if character ch is a vowel
bool isVowel(char ch)
{
    switch (ch) {
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        return true;
    }
    return false;
}

// Compares two integers according
// to their digit sum
bool isSatisfied(string str, int n)
{

    // Check if there are two
    // consecutive consonants
    for (int i = 1; i < n; i++) {
        if (!isVowel(str[i])
            && !isVowel(str[i - 1])) {
            return false;
        }
    }

    // Check if there is any vowel
    // surrounded by two consonants
    for (int i = 1; i < n - 1; i++) {
        if (isVowel(str[i])
            && !isVowel(str[i - 1])
            && !isVowel(str[i + 1])) {
            return false;
        }
    }

    return true;
}

// Driver code
int main()
{
    string str = "acaba";
    int n = str.length();

    if (isSatisfied(str, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true
// if character ch is a vowel
static boolean isVowel(char ch)
{
    switch (ch)
    {
        case 'a':
        case 'e':
        case 'i':
        case 'o':
        case 'u':
            return true;
    }
    return false;
}

// Compares two integers according
// to their digit sum
static boolean isSatisfied(char[] str, int n)
{

    // Check if there are two
    // consecutive consonants
    for (int i = 1; i < n; i++)
    {
        if (!isVowel(str[i]) &&
            !isVowel(str[i - 1]))
        {
            return false;
        }
    }

    // Check if there is any vowel
    // surrounded by two consonants
    for (int i = 1; i < n - 1; i++)
    {
        if (isVowel(str[i]) &&
            !isVowel(str[i - 1]) &&
            !isVowel(str[i + 1]))
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void main(String []args)
{
    String str = "acaba";
    int n = str.length();

    if (isSatisfied(str.toCharArray(), n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true
# if acter ch is a vowel
def isVowel(ch):
    if ch in ['i', 'a', 'e', 'o', 'u']:
        return True
    else:
        return False

# Compares two integers according
# to their digit sum
def isSatisfied(st, n):

    # Check if there are two
    # consecutive consonants
    for i in range(1, n):
        if (isVowel(st[i]) == False and
            isVowel(st[i - 1]) == False):
            return False

    # Check if there is any vowel
    # surrounded by two consonants
    for i in range(1, n - 1):
        if (isVowel(st[i]) and
            isVowel(st[i - 1]) == False and
            isVowel(st[i + 1]) == False ):
            return False
    return True

# Driver code
st = "acaba"
n = len(st)

if (isSatisfied(st, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true
// if character ch is a vowel
static bool isVowel(char ch)
{
    switch (ch)
    {
        case 'a':
        case 'e':
        case 'i':
        case 'o':
        case 'u':
            return true;
    }
    return false;
}

// Compares two integers according
// to their digit sum
static bool isSatisfied(char[] str, int n)
{

    // Check if there are two
    // consecutive consonants
    for (int i = 1; i < n; i++)
    {
        if (!isVowel(str[i]) &&
            !isVowel(str[i - 1]))
        {
            return false;
        }
    }

    // Check if there is any vowel
    // surrounded by two consonants
    for (int i = 1; i < n - 1; i++)
    {
        if (isVowel(str[i]) &&
            !isVowel(str[i - 1]) &&
            !isVowel(str[i + 1]))
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void Main(String []args)
{
    String str = "acaba";
    int n = str.Length;

    if (isSatisfied(str.ToCharArray(), n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function that returns true
      // if character ch is a vowel
      function isVowel(ch) {
        switch (ch) {
          case "a":
          case "e":
          case "i":
          case "o":
          case "u":
            return true;
        }
        return false;
      }

      // Compares two integers according
      // to their digit sum
      function isSatisfied(str, n) {
        // Check if there are two
        // consecutive consonants
        for (var i = 1; i < n; i++) {
          if (!isVowel(str[i]) && !isVowel(str[i - 1])) {
            return false;
          }
        }

        // Check if there is any vowel
        // surrounded by two consonants
        for (var i = 1; i < n - 1; i++) {
          if (isVowel(str[i]) && !isVowel(str[i - 1]) && !isVowel(str[i + 1])) {
            return false;
          }
        }
        return true;
      }

      // Driver code
      var str = "acaba";
      var n = str.length;

      if (isSatisfied(str.split(""), n)) document.write("Yes");
      else document.write("No");
    </script>
```

**Output:** 

```
No
```