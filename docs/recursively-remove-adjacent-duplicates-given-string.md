# 递归删除所有相邻副本

> 原文:[https://www . geeksforgeeks . org/递归-移除-相邻-重复-给定-字符串/](https://www.geeksforgeeks.org/recursively-remove-adjacent-duplicates-given-string/)

给定一个字符串，递归地从该字符串中移除相邻的重复字符。输出字符串不应有任何相邻的重复项。请参见以下示例。

**示例**:

> **输入**:azxzy
> 输出 : ay
> 第一个“azxzy”降为“azzy”。
> 字符串“azzy”包含重复项，
> 因此进一步简化为“ay”。
> 
> **输入**:极客 First
> 输出 : gksfor
> 第一个“极客 foreg”降为
> “gksforgg”。字符串“gksforgg”
> 包含重复项，因此进一步
> 简化为“gksfor”。
> 
> **输入** : caaabbbaacdddd
> **输出**:空字符串
> 
> **输入**:acaaabbbacdddd
> T3】输出 : acac

在 **O(N)** 时间内，可遵循以下**方法**删除重复项:

*   从最左边的字符开始，删除左上角的重复字符(如果有)。
*   第一个字符现在必须与其相邻字符不同。长度为 n-1 的字符串(没有第一个字符的字符串)重复出现。
*   让长度为 n-1 的右子串缩减后得到的字符串为 *rem_str* 。有三种可能的情况
    1.  如果 *rem_str* 的第一个字符与原始字符串的第一个字符匹配，则从 *rem_str* 中删除第一个字符。
    2.  如果剩余字符串为空，并且最后删除的字符与原始字符串的第一个字符相同。返回空字符串。
    3.  否则，在 *rem_str* 的开头追加原始字符串的第一个字符。
*   返回 *rem_str* 。

下图是上述方法的模拟运行:

![](img/15282eefe069a5fe20433f116e14e9a7.png)

下面是上述方法的实现:

## C++

```
// C/C++ program to remove all
// adjacent duplicates from a string
#include <iostream>
#include <string.h>

using namespace std;

// Recursively removes adjacent
// duplicates from str and returns
// new string. las_removed is a
// pointer to last_removed character
char* removeUtil(char *str, char *last_removed)
{

    // If length of string is 1 or 0
    if (str[0] == '\0' || str[1] == '\0')
        return str;

    // Remove leftmost same characters
    // and recur for remaining
    // string
    if (str[0] == str[1])
    {
        *last_removed = str[0];
        while (str[1] && str[0] == str[1])
            str++;
        str++;
        return removeUtil(str, last_removed);
    }

    // At this point, the first character
    // is definiotely different
    // from its adjacent. Ignore first
    // character and recursively
    // remove characters from remaining string
    char* rem_str = removeUtil(str+1,
                               last_removed);

    // Check if the first character
    // of the rem_string matches with
    // the first character of the
    // original string
    if (rem_str[0] && rem_str[0] == str[0])
    {
        *last_removed = str[0];

        // Remove first character
        return (rem_str+1);
    }

    // If remaining string becomes
    // empty and last removed character
    // is same as first character of
    // original string. This is needed
    // for a string like "acbbcddc"
    if (rem_str[0] == '\0' &&
                 *last_removed == str[0])
        return rem_str;

    // If the two first characters
    // of str and rem_str don't match,
    // append first character of str
    // before the first character of
    // rem_str.
    rem_str--;
    rem_str[0] = str[0];
    return rem_str;
}

// Function to remove
char *remove(char *str)
{
    char last_removed = '\0';
    return removeUtil(str, &last_removed);
}

// Driver program to test
// above functions
int main()
{
    char str1[] = "geeksforgeeg";
    cout << remove(str1) << endl;

    char str2[] = "azxxxzy";
    cout << remove(str2) << endl;

    char str3[] = "caaabbbaac";
    cout << remove(str3) << endl;

    char str4[] = "gghhg";
    cout << remove(str4) << endl;

    char str5[] = "aaaacddddcappp";
    cout << remove(str5) << endl;

    char str6[] = "aaaaaaaaaa";
    cout << remove(str6) << endl;

    char str7[] = "qpaaaaadaaaaadprq";
    cout << remove(str7) << endl;

    char str8[] = "acaaabbbacdddd";
    cout << remove(str8) << endl;

    char str9[] = "acbbcddc";
    cout << remove(str9) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove
// all adjacent duplicates
// from a string
import java.io.*;
import java.util.*;

class GFG
{

  // Recursively removes adjacent
  //  duplicates from str and returns
  // new string. las_removed is a
  // pointer to last_removed character
  static String removeUtil(String str,
                            char last_removed)
  {

    // If length of string is 1 or 0
    if (str.length() == 0 || str.length() == 1)
      return str;

    // Remove leftmost same characters
    // and recur for remaining 
    // string
    if (str.charAt(0) == str.charAt(1))
    {
      last_removed = str.charAt(0);
      while (str.length() > 1 && str.charAt(0) ==
                                   str.charAt(1))
        str = str.substring(1, str.length());
      str = str.substring(1, str.length());
      return removeUtil(str, last_removed);
    }

    // At this point, the first
    // character is definiotely different 
    // from its adjacent. Ignore first
    // character and recursively 
    // remove characters from remaining string
    String rem_str = removeUtil(str.substring(
                  1,str.length()), last_removed);

    // Check if the first character of
    // the rem_string matches with 
    // the first character of the original string
    if (rem_str.length() != 0 &&
             rem_str.charAt(0) == str.charAt(0))
    {
      last_removed = str.charAt(0);

      // Remove first character
      return rem_str.substring(1,rem_str.length());
    }

    // If remaining string becomes
    // empty and last removed character
    // is same as first character of
    // original string. This is needed
    // for a string like "acbbcddc"
    if (rem_str.length() == 0 && last_removed ==
                                      str.charAt(0))
      return rem_str;

    // If the two first characters
    // of str and rem_str don't match, 
    // append first character of str
    // before the first character of
    // rem_str
    return (str.charAt(0) + rem_str);
  }

  static String remove(String str) 
  {
    char last_removed = '\0';
    return removeUtil(str, last_removed);      
  }

  // Driver code
  public static void main(String args[])
  {
    String str1 = "geeksforgeeg";
    System.out.println(remove(str1));

    String str2 = "azxxxzy";
    System.out.println(remove(str2));

    String str3 = "caaabbbaac";
    System.out.println(remove(str3));

    String str4 = "gghhg";
    System.out.println(remove(str4));

    String str5 = "aaaacddddcappp";
    System.out.println(remove(str5));

    String str6 = "aaaaaaaaaa";
    System.out.println(remove(str6));

    String str7 = "qpaaaaadaaaaadprq";
    System.out.println(remove(str7));

    String str8 = "acaaabbbacdddd";
    System.out.println(remove(str8));
  }
}

// This code is contributed by rachana soma
```

## 计算机编程语言

```
# Python program to remove
# all adjacent duplicates from a string

# Recursively removes adjacent
# duplicates from str and returns
# new string. las_removed is a
# pointer to last_removed character
def removeUtil(string, last_removed):

    # If length of string is 1 or 0
    if len(string) == 0 or len(string) == 1:
        return string

    # Remove leftmost same characters
    # and recur for remaining
    # string
    if string[0] == string[1]:
        last_removed = ord(string[0])
        while len(string) > 1 and string[0] ==
                                    string[1]:
            string = string[1:]
        string = string[1:]

        return removeUtil(string, last_removed)

    # At this point, the first
    # character is definiotely different
    # from its adjacent. Ignore first
    # character and recursively
    # remove characters from remaining string
    rem_str = removeUtil(string[1:], last_removed)

    # Check if the first character
    # of the rem_string matches
    # with the first character of
    # the original string
    if len(rem_str) != 0 and rem_str[0] ==
                                         string[0]:
        last_removed = ord(string[0])
        return (rem_str[1:])

    # If remaining string becomes
    # empty and last removed character
    # is same as first character of
    # original string. This is needed
    # for a string like "acbbcddc"
    if len(rem_str) == 0 and last_removed ==
                                   ord(string[0]):
        return rem_str

    # If the two first characters of
    # str and rem_str don't match,
    # append first character of str
    # before the first character of
    # rem_str.
    return ([string[0]] + rem_str)

def remove(string):
    last_removed = 0
    return toString(removeUtil(toList(string),
                                    last_removed))

# Utility functions
def toList(string):
    x = []
    for i in string:
        x.append(i)
    return x

def toString(x):
    return ''.join(x)

# Driver program
string1 = "geeksforgeeg"
print remove(string1)

string2 = "azxxxzy"
print remove(string2)

string3 = "caaabbbaac"
print remove(string3)

string4 = "gghhg"
print remove(string4)

string5 = "aaaacddddcappp"
print remove(string5)

string6 = "aaaaaaaaaa"
print remove(string6)

string7 = "qpaaaaadaaaaadprq"
print remove(string7)

string8 = "acaaabbbacdddd"
print remove(string8)

string9 = "acbbcddc"
print remove(string9)

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to remove
// all adjacent duplicates
// from a string
using System;

class GFG
{

  // Recursively removes adjacent
  //  duplicates from str and returns
  // new string. las_removed is a
  // pointer to last_removed character
  static string removeUtil(string str,
                           char last_removed)
  {

    // If length of string is 1 or 0
    if (str.Length == 0 || str.Length == 1)
      return str;

    // Remove leftmost same characters
    // and recur for remaining 
    // string
    if (str[0] == str[1])
    {
      last_removed = str[0];
      while (str.Length > 1 && str[0] ==
             str[1]) {
        str = str.Substring(1, str.Length - 1);
      }
      str = str.Substring(1, str.Length - 1);
      return removeUtil(str, last_removed);
    }

    // At this point, the first
    // character is definiotely different 
    // from its adjacent. Ignore first
    // character and recursively 
    // remove characters from remaining string
    string rem_str = removeUtil(str.Substring(
      1,str.Length - 1), last_removed);

    // Check if the first character of
    // the rem_string matches with 
    // the first character of the original string
    if (rem_str.Length != 0 &&
        rem_str[0] == str[0])
    {
      last_removed = str[0];

      // Remove first character
      return rem_str.Substring(1,rem_str.Length - 1);
    }

    // If remaining string becomes
    // empty and last removed character
    // is same as first character of
    // original string. This is needed
    // for a string like "acbbcddc"
    if (rem_str.Length == 0 && last_removed ==
        str[0])
      return rem_str;

    // If the two first characters
    // of str and rem_str don't match, 
    // append first character of str
    // before the first character of
    // rem_str
    return (str[0] + rem_str);
  }

  static string remove(string str) 
  {
    char last_removed = '\0';
    return removeUtil(str, last_removed);      
  }

  // Driver code
  public static void Main()
  {

    string str1 = "geeksforgeeg";
    Console.Write(remove(str1) + "\n");

    string str2 = "azxxxzy";
    Console.Write(remove(str2)  + "\n");

    string str3 = "caaabbbaac";
    Console.Write(remove(str3)  + "\n");

    string str4 = "gghhg";
    Console.Write(remove(str4)  + "\n");

    string str5 = "aaaacddddcappp";
    Console.Write(remove(str5)  + "\n");

    string str6 = "aaaaaaaaaa";
    Console.Write(remove(str6)  + "\n");

    string str7 = "qpaaaaadaaaaadprq";
    Console.Write(remove(str7)  + "\n");

    string str8 = "acaaabbbacdddd";
    Console.Write(remove(str8)  + "\n");

    string str9 = "acbbcdd";
    Console.Write(remove(str9)  + "\n");

  }
}

// This code is contributed by Samim Hossain Mondal.
```

**输出:**

```
gksfor
ay

g
a

qrq
acac
a
```

**时间复杂度:**解的时间复杂度可以写成 T(n) = T(n-k) + O(k)，其中 n 是输入字符串的长度，k 是相同的第一个字符的个数。递归的解是 O(n)

感谢 **Prachi Bodke** 提出这个问题和初步解决方案。

**另一种方法:**
这里的想法是检查字符串 remStr 是否具有与父字符串的最后一个字符匹配的重复字符。如果发生这种情况，那么我们必须在连接字符串 s 和字符串 remStr 之前继续删除该字符。

下面是上述方法的实现:

## C++

```
// C++ Program for above approach

#include <bits/stdc++.h>
using namespace std;

// Recursively removes adjacent
// duplicates from str and
// returns new string. las_removed
// is a pointer to
// last_removed character
string removeDuplicates(string s, char ch)
{

    // If length of string is 1 or 0
    if (s.length() <= 1) {
        return s;
    }

    int i = 0;
    while (i < s.length()) {
        if (i + 1 < s.length() && s[i] == s[i + 1]) {
            int j = i;
            while (j + 1 < s.length() && s[j] == s[j + 1]) {
                j++;
            }
            char lastChar = i > 0 ? s[i - 1] : ch;

            string remStr = removeDuplicates(
                s.substr(j + 1, s.length()), lastChar);

            s = s.substr(0, i);
            int k = s.length(), l = 0;

            // Recursively remove all the adjacent
            // characters formed by removing the
            // adjacent characters
            while (remStr.length() > 0 && s.length() > 0
                   && remStr[0] == s[s.length() - 1]) {

                // Have to check whether this is the
                // repeated character that matches the
                // last char of the parent String
                while (remStr.length() > 0
                       && remStr[0] != ch
                       && remStr[0] == s[s.length() - 1]) {
                    remStr
                        = remStr.substr(1, remStr.length());
                }
                s = s.substr(0, s.length() - 1);
            }
            s = s + remStr;
            i = j;
        }
        else {
            i++;
        }
    }
    return s;
}

// Driver Code
int main()
{

    string str1 = "mississipie";
    cout << removeDuplicates(str1, ' ') << endl;

    string str2 = "ocvvcolop";
    cout << removeDuplicates(str2, ' ') << endl;
}

// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

  // Recursively removes adjacent
  // duplicates from str and
  // returns new string. las_removed
  // is a pointer to
  // last_removed character
  private static String removeDuplicates(
    String s, char ch)
  {

    // If length of string is 1 or 0
    if (s == null || s.length() <= 1)
    {
      return s;
    }

    int i = 0;
    while (i < s.length())
    {
      if (i + 1 < s.length()
          && s.charAt(i) == s.charAt(i + 1))
      {
        int j = i;
        while (j + 1 < s.length()
               && s.charAt(j) ==
               s.charAt(j + 1))
        {
          j++;
        }
        char lastChar
          = i > 0 ? s.charAt(i - 1) : ch;

        String remStr = removeDuplicates(
          s.substring(j + 1, s.length()),
          lastChar);

        s = s.substring(0, i);
        int k = s.length(), l = 0;

        // Recursively remove all the adjacent
        // characters formed by removing the
        // adjacent characters
        while (remStr.length() > 0 &&
               s.length() > 0 &&
               remStr.charAt(0) ==
               s.charAt(s.length() - 1))
        {

          // Have to check whether this is the
          // repeated character that matches the
          // last char of the parent String
          while (remStr.length() > 0
                 && remStr.charAt(0) != ch
                 && remStr.charAt(0)
                 == s.charAt(s.length()
                             - 1))
          {
            remStr = remStr.substring(
              1, remStr.length());
          }
          s = s.substring(0, s.length() - 1);
        }
        s = s + remStr;
        i = j;
      }
      else
      {
        i++;
      }
    }
    return s;
  }

  // Driver Code
  public static void main(String[] args)
  {

    String str1 = "mississipie";
    System.out.println(removeDuplicates(
      str1, ' '));
    String str2 = "ocvvcolop";
    System.out.println(removeDuplicates(
      str2, ' '));
  }
}

// This code is contributed by Niharika Sahai
```

**输出:**

```
mpie
lop
```

**时间复杂度:** O(n)

感谢 **Niharika Sahai** 提出这个问题和初步解决方案。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论