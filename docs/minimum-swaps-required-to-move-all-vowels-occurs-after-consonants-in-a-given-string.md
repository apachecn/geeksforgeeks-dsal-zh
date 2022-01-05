# 移动所有元音所需的最小互换发生在给定字符串中的辅音之后

> 原文:[https://www . geesforgeks . org/minimum-swaps-需要移动所有元音-在给定字符串中出现在辅音之后/](https://www.geeksforgeeks.org/minimum-swaps-required-to-move-all-vowels-occurs-after-consonants-in-a-given-string/)

给定一个字符串 **S** ，任务是计算元音必须移动的位置数，这样所有的辅音都放在前面，所有的元音都放在最后。新字符串中辅音和元音的顺序必须相同。

**示例:**

> **输入:** S = "abcdefghi"
> **输出:** 9
> **解释:**
> 字符串中出现的辅音是 b、c、d、f、g 和 h，元音是 a、e 和 I，重排时最后的字符串变成“bcdfghaei”，辅音和元音的顺序不变。
> 最初‘a’位于指数 0，最后移到指数 6。移动的位置数= 6–0 = 6。
> 最初‘e’位于指数 4，最后移至指数 7。移动的位置数= 7–4 = 3。
> 最初‘I’位于指数 8，它没有改变位置。所以移动次数= 0。
> 移动的位置总数= 6 + 3 + 0 = 9。
> **输入:** S = "iijedf"
> **输出:** 8
> **解释:**
> 字符串中出现的辅音是 j、d 和 f，元音是 I、I 和 e，重新排列后，最终的字符串变成了“jdfiie”，辅音和元音的顺序没有改变。
> 索引 0 处的“I”移动到索引 3。移动的位置数= 3–0 = 3。
> 索引 1 处的“I”移动到索引 4。移动的位置数= 4–1 = 3。
> 索引 3 处的“e”移动到索引 5。移动的位置数= 5–3 = 2。
> 移动的位置总数= 3 + 3 + 2 = 8。

**进场:**

1.  创建空字符串**元音**和**辅音**来存储给定字符串的元音和辅音。
2.  遍历给定的字符串 **S** ，如果当前字符是元音，则将它附加到字符串**元音**字符串，否则附加到字符串**辅音**字符串。
3.  将字符串**辅音**和**元音**的连接存储在 **ans** 字符串中。
4.  初始化两个指针 **p1** 和 **p2** ，这样 p1 指向 S 的第一个索引，p2 指向第一个元音出现在 **ans** 字符串中的索引。
5.  将计数器变量 **cnt** 初始化为 0。
6.  每次索引 p1 的字符与索引 p2 的字符匹配时，将**p2–p1**的值加到 **cnt** 上，并将 P1 和 p2 的值加 1。
7.  对每个索引重复步骤 6，直到达到最后一个索引**和**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a character
// is vowel or not
bool isvowel(char x)
{
    if (x == 'a' || x == 'e' || x == 'i'
        || x == 'o' || x == 'u' || x == 'A'
        || x == 'E' || x == 'I' || x == 'O'
        || x == 'U')
        return true;
    else
        return false;
}

// Function that creates a new string
// such that all consonants are at
// the front of the string
void movetofront(string s)
{
    // To store the vowels and
    // consonants in the same order
    string vowels, consonants;

    // To store the resultant string
    string ans;

    vowels = consonants = ans = "";

    for (int i = 0; s[i]; i++) {

        // Check if s[i] is vowel
        if (isvowel(s[i])) {
            vowels += s[i];
        }

        // Else s[i] is consonant
        else {
            consonants += s[i];
        }
    }

    // concatenate the strings formed
    ans = consonants + vowels;

    // Pointer variables
    int p1 = 0;
    int p2 = consonants.size();

    // Counter variable
    int cnt = 0;

    // Condition to check if the
    // given string has only
    // consonants
    if (p2 == ans.size()) {
        cout << 0 << endl;
        return;
    }

    // Condition to check if the
    // string has only vowels
    if (ans.size() == vowels.size()) {
        cout << 0 << endl;
        return;
    }

    // Loop to find the count of
    // number of positions moved
    while (p2 < ans.size()) {
        if (ans[p2] == s[p1]) {
            cnt += p2 - p1;
            p1++;
            p2++;
        }
        else {
            p1++;
        }
    }
    cout << cnt << endl;
    return;
}

// Driver Code
int main()
{
    // Given string
    string s = "abcdefghi";

    // Function Call
    movetofront(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to check whether a character
// is vowel or not
static boolean isvowel(char x)
{
    if (x == 'a' || x == 'e' || x == 'i' ||
        x == 'o' || x == 'u' || x == 'A' ||
        x == 'E' || x == 'I' || x == 'O' ||
        x == 'U')
        return true;
    else
        return false;
}

// Function that creates a new String
// such that all consonants are at
// the front of the String
static void movetofront(String s)
{
    // To store the vowels and
    // consonants in the same order
    String vowels, consonants;

    // To store the resultant String
    String ans;

    vowels = consonants = ans = "";

    for (int i = 0; i < s.length(); i++)
    {

        // Check if s.charAt(i) is vowel
        if (isvowel(s.charAt(i)))
        {
            vowels += s.charAt(i);
        }

        // Else s.charAt(i) is consonant
        else
        {
            consonants += s.charAt(i);
        }
    }

    // concatenate the Strings formed
    ans = consonants + vowels;

    // Pointer variables
    int p1 = 0;
    int p2 = consonants.length();

    // Counter variable
    int cnt = 0;

    // Condition to check if the
    // given String has only
    // consonants
    if (p2 == ans.length())
    {
        System.out.print(0 + "\n");
        return;
    }

    // Condition to check if the
    // String has only vowels
    if (ans.length() == vowels.length())
    {
        System.out.print(0 + "\n");
        return;
    }

    // Loop to find the count of
    // number of positions moved
    while (p2 < ans.length())
    {
        if (ans.charAt(p2) == s.charAt(p1))
        {
            cnt += p2 - p1;
            p1++;
            p2++;
        }
        else
        {
            p1++;
        }
    }
    System.out.print(cnt + "\n");
    return;
}

// Driver Code
public static void main(String[] args)
{
    // Given String
    String s = "abcdefghi";

    // Function Call
    movetofront(s);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether a character
# is vowel or not
def isvowel(x):

    if (x == 'a' or x == 'e' or
        x == 'i' or x == 'o' or
        x == 'u' or x == 'A' or
        x == 'E' or x == 'I' or
        x == 'O' or x == 'U'):
        return bool(True)
    else:
        return bool(False)

# Function that creates a new string
# such that all consonants are at
# the front of the string
def movetofront(s):

    # To store the vowels and
    # consonants in the same order
    vowels = consonants = ans = ""

    for i in range(len(s)):

        # Check if s[i] is vowel
        if (isvowel(s[i])):
            vowels += s[i]

        # Else s[i] is consonant
        else:
            consonants += s[i]

    # concatenate the strings formed
    ans = consonants + vowels

    # Pointer variables
    p1 = 0
    p2 = len(consonants)

    # Counter variable
    cnt = 0

    # Condition to check if the
    # given string has only
    # consonants
    if (p2 == len(ans)):
        print(0)
        return

    # Condition to check if the
    # string has only vowels
    if (len(ans) == len(vowels)):
        print(0)
        return

    # Loop to find the count of
    # number of positions moved
    while (p2 < len(ans)):
        if (ans[p2] == s[p1]):
            cnt += p2 - p1
            p1 += 1
            p2 += 1
        else:
            p1 += 1

    print(cnt)
    return

# Driver code

# Given string
s = "abcdefghi"

# Function call
movetofront(s)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check whether a character
// is vowel or not
static bool isvowel(char x)
{
    if (x == 'a' || x == 'e' || x == 'i' ||
        x == 'o' || x == 'u' || x == 'A' ||
        x == 'E' || x == 'I' || x == 'O' ||
        x == 'U')
        return true;
    else
        return false;
}

// Function that creates a new String
// such that all consonants are at
// the front of the String
static void movetofront(String s)
{
    // To store the vowels and
    // consonants in the same order
    String vowels, consonants;

    // To store the resultant String
    String ans;

    vowels = consonants = ans = "";

    for (int i = 0; i < s.Length; i++)
    {

        // Check if s[i] is vowel
        if (isvowel(s[i]))
        {
            vowels += s[i];
        }

        // Else s[i] is consonant
        else
        {
            consonants += s[i];
        }
    }

    // concatenate the Strings formed
    ans = consonants + vowels;

    // Pointer variables
    int p1 = 0;
    int p2 = consonants.Length;

    // Counter variable
    int cnt = 0;

    // Condition to check if the
    // given String has only
    // consonants
    if (p2 == ans.Length)
    {
        Console.Write(0 + "\n");
        return;
    }

    // Condition to check if the
    // String has only vowels
    if (ans.Length == vowels.Length)
    {
        Console.Write(0 + "\n");
        return;
    }

    // Loop to find the count of
    // number of positions moved
    while (p2 < ans.Length)
    {
        if (ans[p2] == s[p1])
        {
            cnt += p2 - p1;
            p1++;
            p2++;
        }
        else
        {
            p1++;
        }
    }
    Console.Write(cnt + "\n");
    return;
}

// Driver Code
public static void Main(String[] args)
{
    // Given String
    String s = "abcdefghi";

    // Function Call
    movetofront(s);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to check whether a character
      // is vowel or not
      function isvowel(x) {
        if (
          x === "a" ||
          x === "e" ||
          x === "i" ||
          x === "o" ||
          x === "u" ||
          x === "A" ||
          x === "E" ||
          x === "I" ||
          x === "O" ||
          x === "U"
        )
          return true;
        else return false;
      }

      // Function that creates a new String
      // such that all consonants are at
      // the front of the String
      function movetofront(s) {
        // To store the vowels and
        // consonants in the same order
        var vowels, consonants;

        // To store the resultant String
        var ans;

        vowels = consonants = ans = "";

        for (var i = 0; i < s.length; i++) {
          // Check if s[i] is vowel
          if (isvowel(s[i])) {
            vowels += s[i];
          }

          // Else s[i] is consonant
          else {
            consonants += s[i];
          }
        }

        // concatenate the Strings formed
        ans = consonants + vowels;

        // Pointer variables
        var p1 = 0;
        var p2 = consonants.length;

        // Counter variable
        var cnt = 0;

        // Condition to check if the
        // given String has only
        // consonants
        if (p2 === ans.length) {
          document.write(0 + "<br>");
          return;
        }

        // Condition to check if the
        // String has only vowels
        if (ans.length === vowels.length) {
          document.write(0 + "<br>");
          return;
        }

        // Loop to find the count of
        // number of positions moved
        while (p2 < ans.length) {
          if (ans[p2] === s[p1]) {
            cnt += p2 - p1;
            p1++;
            p2++;
          } else {
            p1++;
          }
        }
        document.write(cnt + "<br>");
        return;
      }

      // Driver Code
      // Given String
      var s = "abcdefghi";
      // Function Call
      movetofront(s);
    </script>
```

**Output:** 

```
9
```

**时间复杂度:** *O(N)，其中 N 是字符串的长度。*
**辅助空间:***O(N)*其中 N 为弦的长度。