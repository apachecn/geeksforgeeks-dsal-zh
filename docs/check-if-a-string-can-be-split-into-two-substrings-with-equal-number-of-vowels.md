# 检查一个字符串是否可以拆分成两个元音数量相等的子字符串

> 原文:[https://www . geeksforgeeks . org/check-if-a-string-can-split-in-two-substrings-具有相等数量的元音/](https://www.geeksforgeeks.org/check-if-a-string-can-be-split-into-two-substrings-with-equal-number-of-vowels/)

给定一个[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，任务是检查该字符串是否可以分成两个[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，使得两者中的元音数量相等。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** S =【极客】
> **输出:**是
> **解释:**将字符串拆分为子串“ge”(*元音计数= 1* )和“eks”(*元音计数= 1* )满足条件。
> 
> **输入:** S =【教科书】
> T3】输出:否

**天真方法:**解决这个问题最简单的方法是[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并在每个可能的索引处将该字符串划分为两个子字符串。对于每个这样的分割，检查两个子串中是否存在相同数量的元音。如果发现属实，则打印**“是”**否则打印**“否”**。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**可以通过预先计算字符串中元音的总数来优化上述方法。按照以下步骤解决问题:

*   初始化两个变量，比如**total 元音**和**vowelstilnow**，分别存储元音总数和当前元音计数。
*   现在[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 并统计所有的元音并将其存储在**total 元音**中。
*   现在，再次[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 并将**总计元音**减少 **1** 并将**vowelstillow**增加 **1** ，如果出现元音。检查**总元音**是否在任意点变得等于**vowelstilnow**。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if any
// character is a vowel or not
bool isVowel(char ch)
{

    // Lowercase vowels
    if (ch == 'a' || ch == 'e' || ch == 'i'
        || ch == 'o' || ch == 'u')
        return true;

    // Uppercase vowels
    if (ch == 'A' || ch == 'E' || ch == 'I'
        || ch == 'O' || ch == 'U')
        return true;

    // Otherwise
    return false;
}

// Function to check if string S
// can be split into two substrings
// with equal number of vowels
string containsEqualStrings(string S)
{

    // Stores the count of vowels
    // in the string S
    int totalVowels = 0;

    // Traverse over the string
    for (int i = 0;
         i < S.size(); i++)
    {

        // If S[i] is vowel
        if (isVowel(S[i]))
            totalVowels++;
    }

    // Stores the count of vowels
    // upto the current index
    int vowelsTillNow = 0;

    // Traverse over the string
    for (int i = 0;
         i < S.size(); i++)
    {

        // If S[i] is vowel
        if (isVowel(S[i]))
        {
            vowelsTillNow++;
            totalVowels--;

            // If vowelsTillNow and
            // totalVowels are equal
            if (vowelsTillNow
                == totalVowels)
            {

                return "Yes";
            }
        }
    }

    // Otherwise
    return "No";
}

// Driver Code
int main()
{
    string S = "geeks";
    cout<<(containsEqualStrings(S));
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to check if any
    // character is a vowel or not
    public static boolean isVowel(char ch)
    {
        // Lowercase vowels
        if (ch == 'a' || ch == 'e' || ch == 'i'
            || ch == 'o' || ch == 'u')
            return true;

        // Uppercase vowels
        if (ch == 'A' || ch == 'E' || ch == 'I'
            || ch == 'O' || ch == 'U')
            return true;

        // Otherwise
        return false;
    }

    // Function to check if string S
    // can be split into two substrings
    // with equal number of vowels
    public static String
    containsEqualStrings(String S)
    {

        // Stores the count of vowels
        // in the string S
        int totalVowels = 0;

        // Traverse over the string
        for (int i = 0;
             i < S.length(); i++) {

            // If S[i] is vowel
            if (isVowel(S.charAt(i)))
                totalVowels++;
        }

        // Stores the count of vowels
        // upto the current index
        int vowelsTillNow = 0;

        // Traverse over the string
        for (int i = 0;
             i < S.length(); i++) {

            // If S[i] is vowel
            if (isVowel(S.charAt(i))) {
                vowelsTillNow++;
                totalVowels--;

                // If vowelsTillNow and
                // totalVowels are equal
                if (vowelsTillNow
                    == totalVowels) {

                    return "Yes";
                }
            }
        }

        // Otherwise
        return "No";
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "geeks";
        System.out.println(
            containsEqualStrings(S));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if any
# character is a vowel or not
def isVowel(ch):

    # Lowercase vowels
    if (ch == 'a' or ch == 'e' or
        ch == 'i' or ch == 'o' or
        ch == 'u'):
        return True

    # Uppercase vowels
    if (ch == 'A' or ch == 'E' or
        ch == 'I' or ch == 'O' or
        ch == 'U'):
        return True

    # Otherwise
    return False

# Function to check if string S
# can be split into two substrings
# with equal number of vowels
def containsEqualStrings(S):

    # Stores the count of vowels
    # in the string S
    totalVowels = 0

    # Traverse over the string
    for i in range(len(S)):

        # If S[i] is vowel
        if (isVowel(S[i])):
            totalVowels += 1

    # Stores the count of vowels
    # upto the current index
    vowelsTillNow = 0

    # Traverse over the string
    for i in range(len(S)):

        # If S[i] is vowel
        if (isVowel(S[i])):
            vowelsTillNow += 1
            totalVowels -= 1

            # If vowelsTillNow and
            # totalVowels are equal
            if (vowelsTillNow == totalVowels):
                return "Yes"

    # Otherwise
    return "No"

# Driver Code
if __name__ == "__main__":

    S = "geeks"
    print(containsEqualStrings(S))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to check if any
    // character is a vowel or not
    public static bool isVowel(char ch)
    {

        // Lowercase vowels
        if (ch == 'a' || ch == 'e' || ch == 'i'
            || ch == 'o' || ch == 'u')
            return true;

        // Uppercase vowels
        if (ch == 'A' || ch == 'E' || ch == 'I'
            || ch == 'O' || ch == 'U')
            return true;

        // Otherwise
        return false;
    }

    // Function to check if string S
    // can be split into two substrings
    // with equal number of vowels
    public static String
    containsEqualStrings(string S)
    {

        // Stores the count of vowels
        // in the string S
        int totalVowels = 0;

        // Traverse over the string
        for (int i = 0;
             i < S.Length; i++)
        {

            // If S[i] is vowel
            if (isVowel(S[i]))
                totalVowels++;
        }

        // Stores the count of vowels
        // upto the current index
        int vowelsTillNow = 0;

        // Traverse over the string
        for (int i = 0;
             i < S.Length; i++) {

            // If S[i] is vowel
            if (isVowel(S[i])) {
                vowelsTillNow++;
                totalVowels--;

                // If vowelsTillNow and
                // totalVowels are equal
                if (vowelsTillNow
                    == totalVowels) {

                    return "Yes";
                }
            }
        }

        // Otherwise
        return "No";
    }

// Driver Code
static public void Main()
{
    string S = "geeks";
    Console.WriteLine(
        containsEqualStrings(S));
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to check if any
      // character is a vowel or not
      function isVowel(ch) {
        // Lowercase vowels
        if (ch === "a" || ch === "e" || ch === "i" || ch === "o" || ch === "u")
          return true;

        // Uppercase vowels
        if (ch === "A" || ch === "E" || ch === "I" || ch === "O" || ch === "U")
          return true;

        // Otherwise
        return false;
      }

      // Function to check if string S
      // can be split into two substrings
      // with equal number of vowels
      function containsEqualStrings(S) {
        // Stores the count of vowels
        // in the string S
        var totalVowels = 0;

        // Traverse over the string
        for (var i = 0; i < S.length; i++) {
          // If S[i] is vowel
          if (isVowel(S[i])) totalVowels++;
        }

        // Stores the count of vowels
        // upto the current index
        var vowelsTillNow = 0;

        // Traverse over the string
        for (var i = 0; i < S.length; i++) {
          // If S[i] is vowel
          if (isVowel(S[i])) {
            vowelsTillNow++;
            totalVowels--;

            // If vowelsTillNow and
            // totalVowels are equal
            if (vowelsTillNow === totalVowels) {
              return "Yes";
            }
          }
        }

        // Otherwise
        return "No";
      }

      // Driver Code
      var S = "geeks";
      document.write(containsEqualStrings(S));
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)