# 通过替换元音和辅音检查一个字符串是否可以转换成另一个字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-transformed-to-other-string-by-replacement-元音-辅音/](https://www.geeksforgeeks.org/check-if-a-string-can-be-converted-to-another-string-by-replacing-vowels-and-consonants/)

给定两个字符串 S1 和 S2，如果一个字符是元音或辅音，你只允许在任何位置把它变成任何元音。任务是检查字符串 S1 是否可以更改为 S2，或者 S2 是否可以更改为 S1。
**例:**

> **输入:**S1 =“abccgle”，S2 =“ezg gli”
> **输出:**是
> 将‘a’改为‘e’、‘b’改为‘z’、‘c’改为‘g’、‘e’改为‘I’。
> **输入:**S1 =“ABC”，S2 =“cgth”
> **输出:**否

**途径:**解决上述问题应遵循以下条件:

*   两个字符串的长度应该相等。
*   在每个索引中，S1 和 S2 的字符都应该是元音或辅音。

以下是上述方法的实现:

## C++

```
// C++ program to check if a string can be converted
// to other string by replacing vowels and consonants
#include <bits/stdc++.h>
using namespace std;

// Function to check if the character
// is vowel or not
bool isVowel(char c)
{
    if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u')
        return true;

    return false;
}

// Function that checks if a string can be
// converted to another string
bool checkPossibility(string s1, string s2)
{
    // Find length of string
    int l1 = s1.length();
    int l2 = s2.length();

    // If length is not same
    if (l1 != l2)
        return false;

    // Iterate for every character
    for (int i = 0; i < l1; i++) {
        // If both vowel
        if (isVowel(s1[i]) && isVowel(s2[i]))
            continue;

        // Both are consonants
        else if (!(isVowel(s1[i])) && !(isVowel(s2[i])))
            continue;
        else
            return false;
    }
    return true;
}

// Driver Code
int main()
{

    string S1 = "abcgle", S2 = "ezggli";
    if (checkPossibility(S1, S2))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string
// can be converted to other string
// by replacing vowels and consonants
class GfG
{

// Function to check if the character
// is vowel or not
static boolean isVowel(char c)
{
    if (c == 'a' || c == 'e' || c == 'i' ||
                    c == 'o' || c == 'u')
        return true;

    return false;
}

// Function that checks if a string can be
// converted to another string
static boolean checkPossibility(String s1, String s2)
{
    // Find length of string
    int l1 = s1.length();
    int l2 = s2.length();

    // If length is not same
    if (l1 != l2)
        return false;

    // Iterate for every character
    for (int i = 0; i < l1; i++)
    {
        // If both vowel
        if (isVowel(s1.charAt(i)) &&
            isVowel(s2.charAt(i)))
            continue;

        // Both are consonants
        else if (!(isVowel(s1.charAt(i))) &&
                    !(isVowel(s2.charAt(i))))
            continue;
        else
            return false;
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{

    String S1 = "abcgle";
    String S2 = "ezggli";
    if (checkPossibility(S1, S2) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Prerna saini.
```

## 蟒蛇 3

```
# Python3 program to check if a string can
# be converted to other string by replacing
# vowels and consonants

# Function to check if the character
# is vowel or not
def isVowel(c):

    if (c == 'a' or c == 'e' or
        c == 'i' or c == 'o' or c == 'u'):
        return True

    return False

# Function that checks if a string can
# be converted to another string
def checkPossibility(s1, s2):

    # Find length of string
    l1 = len(s1)
    l2 = len(s2)

    # If length is not same
    if (l1 != l2):
        return False

    # Iterate for every character
    for i in range(l1):

        # If both vowel
        if (isVowel(s1[i]) and isVowel(s2[i])):
            continue

        # Both are consonants
        elif ((isVowel(s1[i])) == False and
              (isVowel(s2[i]) == False)):
            continue
        else:
            return False

    return True

# Driver Code
S1, S2 = "abcgle", "ezggli"
if (checkPossibility(S1, S2)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to check if a string
// can be converted to other string
// by replacing vowels and consonants
using System;

class GfG
{

    // Function to check if the character
    // is vowel or not
    static bool isVowel(char c)
    {
        if (c == 'a' || c == 'e' || c == 'i' ||
                        c == 'o' || c == 'u')
            return true;

        return false;
    }

    // Function that checks if a string can be
    // converted to another string
    static bool checkPossibility(string s1, string s2)
    {
        // Find length of string
        int l1 = s1.Length ;
        int l2 = s2.Length ;

        // If length is not same
        if (l1 != l2)
            return false;

        // Iterate for every character
        for (int i = 0; i < l1; i++)
        {
            // If both vowel
            if (isVowel(s1[i]) &&
                isVowel(s2[i]))
                continue;

            // Both are consonants
            else if (!(isVowel(s1[i])) &&
                        !(isVowel(s2[i])))
                continue;
            else
                return false;
        }
        return true;
    }

    // Driver Code
    public static void Main()
    {

        string S1 = "abcgle";
        string S2 = "ezggli";
        if (checkPossibility(S1, S2) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Ryuga.
```

## java 描述语言

```
<script>
      // JavaScript program to check if a string can be converted
      // to other string by replacing vowels and consonants

      // Function to check if the character
      // is vowel or not
      function isVowel(c) {
        if (c === "a" || c === "e" || c === "i" || c === "o" || c === "u")
          return true;

        return false;
      }

      // Function that checks if a string can be
      // converted to another string
      function checkPossibility(s1, s2)
      {

        // Find length of string
        var l1 = s1.length;
        var l2 = s2.length;

        // If length is not same
        if (l1 !== l2) return false;

        // Iterate for every character
        for (var i = 0; i < l1; i++)
        {

          // If both vowel
          if (isVowel(s1[i]) && isVowel(s2[i])) continue;

          // Both are consonants
          else if (!isVowel(s1[i]) && !isVowel(s2[i])) continue;
          else return false;
        }
        return true;
      }

      // Driver Code
      var S1 = "abcgle",
        S2 = "ezggli";
      if (checkPossibility(S1, S2)) document.write("Yes");
      else document.write("No");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
Yes
```