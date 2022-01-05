# 检查字符串中大写字符使用是否正确

> 原文:[https://www . geesforgeks . org/check-如果字符串中的大写字符使用正确与否/](https://www.geeksforgeeks.org/check-if-uppercase-characters-in-a-string-are-used-correctly-or-not/)

给定一个由大小写字母组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是检查给定字符串中大写字符是否使用正确。大写字符的正确用法如下:

*   字符串中的所有字符都是大写的。比如**【极客】**。
*   所有字符都不是大写的。比如**“极客”**。
*   只有第一个字符是大写的。比如**“极客”**。

**示例:**

> **输入:** S = "Geeks"
> **输出:**是
> **说明:**只有字符串的第一个字符是大写的，其余所有字符都是小写的。
> 
> **输入:**S = " geeks forgeeks "
> T3】输出:否

**方法:**按照以下步骤解决问题:

*   [检查字符串的第一个字符是否大写](https://www.geeksforgeeks.org/check-whether-the-given-character-is-in-upper-case-lower-case-or-non-alphabetic-character/)。如果发现为真，则迭代剩余的字符。
*   如果剩余字符全部大写，则打印**“是”**。否则，如果剩余字符中有大写的，则打印**“否”**。
*   如果第一个字符不是大写的，则检查其余所有字符是否都是小写的。如果发现为真，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// character c is in lowercase or not
bool isLower(char c)
{

    return c >= 'a' and c <= 'z';
}

// Function to check if the
// character c is in uppercase or not
bool isUpper(char c)
{

    return c >= 'A' and c <= 'Z';
}

// Utility function to check if uppercase
// characters are used correctly or not
bool detectUppercaseUseUtil(string S)
{

    // Length of string
    int N = S.size();
    int i;

    // If the first character is in lowercase
    if (isLower(S[0]))
    {
        i = 1;
        while (S[i] && isLower(S[i]))
            ++i;
        return i == N ? true : false;
    }

    // Otherwise
    else {
        i = 1;

        // Check if all characters
        // are in uppercase or not
        while (S[i] && isUpper(S[i]))
            ++i;

        // If all characters are
        // in uppercase
        if (i == N)
            return true;
        else if (i > 1)
            return false;

        // Check if all characters except
        // the first are in lowercase
        while (S[i] && isLower(S[i]))
            ++i;
        return i == N ? true : false;
    }
}

// Function to check if uppercase
// characters are used correctly or not
void detectUppercaseUse(string S)
{

    // Stores whether the use of uppercase
    // characters are correct or not
    bool check = detectUppercaseUseUtil(S);

    // If correct
    if (check)
        cout << "Yes";

    // Otherwise
    else
        cout << "No";
}

// Driver Code
int main()
{

    // Given string
    string S = "GeeKs";

    // Function call to check if use of
    // uppercase characters is correct or not
    detectUppercaseUse(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {

  // Function to check if the
  // character c is in lowercase or not
  static boolean isLower(char c)
  {

    return c >= 'a' && c <= 'z';
  }

  // Function to check if the
  // character c is in uppercase or not
  static boolean isUpper(char c)
  {

    return c >= 'A' && c <= 'Z';
  }

  // Utility function to check if uppercase
  // characters are used correctly or not
  static boolean detectUppercaseUseUtil(String S)
  {
    // Length of string
    int N = S.length();

    int i;

    // If the first character is in lowercase
    if (isLower(S.charAt(0))) {
      i = 1;
      while (i<N && isLower(S.charAt(i)))
        ++i;
      return i == N ? true : false;
    }

    // Otherwise
    else {
      i = 1;

      // Check if all characters
      // are in uppercase or not
      while (i<N && isUpper(S.charAt(i)))
        ++i;

      // If all characters are
      // in uppercase
      if (i == N)
        return true;
      else if (i > 1)
        return false;

      // Check if all characters except
      // the first are in lowercase
      while (i<N && isLower(S.charAt(i)))
        ++i;
      return i == N ? true : false;
    }
  }

  // Function to check if uppercase
  // characters are used correctly or not
  static void detectUppercaseUse(String S)
  {

    // Stores whether the use of uppercase
    // characters are correct or not
    boolean check = detectUppercaseUseUtil(S);

    // If correct
    if (check)
      System.out.println("Yes");

    // Otherwise
    else
      System.out.println("No");
  }

  // Driver Code
  public static void main (String[] args)
  {
    // Given string
    String S = "GeeKs";

    // Function call to check if use of
    // uppercase characters is correct or not
    detectUppercaseUse(S);
  }
}

// This code is contributed by subhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the
# character c is in lowercase or not
def isLower(c):
    return ord(c) >= ord('a') and ord(c) <= ord('z')

# Function to check if the
# character c is in uppercase or not
def isUpper(c):
    return ord(c) >= ord('A') and ord(c) <= ord('Z')

# Utility function to check if uppercase
# characters are used correctly or not
def detectUppercaseUseUtil(S):

    # Length of string
    N = len(S)
    i = 0

    # If the first character is in lowercase
    if (isLower(S[0])):
        i = 1
        while (S[i] and isLower(S[i])):
            i += 1
        return True if (i == N) else False

    # Otherwise
    else:
        i = 1

        # Check if all characters
        # are in uppercase or not
        while (S[i] and isUpper(S[i])):
            i += 1

        # If all characters are
        # in uppercase
        if (i == N):
            return True
        elif (i > 1):
            return False

        # Check if all characters except
        # the first are in lowercase
        while (S[i] and isLower(S[i])):
            i += 1
        return True if (i == N) else False

# Function to check if uppercase
# characters are used correctly or not
def detectUppercaseUse(S):

    # Stores whether the use of uppercase
    # characters are correct or not
    check = detectUppercaseUseUtil(S)

    # If correct
    if (check):
        print("Yes")
    # Otherwise
    else:
        print ("No")

# Driver Code
if __name__ == '__main__':

    # Given string
    S = "GeeKs"

    # Function call to check if use of
    # uppercase characters is correct or not
    detectUppercaseUse(S)

# This code is contributed by mohit kumar 29.
```

## C#

```
using System;
public class GFG
{

  // Function to check if the
  // character c is in lowercase or not
  static bool isLower(char c)
  {

    return c >= 'a' && c <= 'z';
  }

  // Function to check if the
  // character c is in uppercase or not
  static bool isUpper(char c)
  {

    return c >= 'A' && c <= 'Z';
  }

  // Utility function to check if uppercase
  // characters are used correctly or not
  static bool detectUppercaseUseUtil(string S)
  {

    // Length of string
    int N = S.Length;

    int i;

    // If the first character is in lowercase
    if (isLower(S[0]))
    {
      i = 1;
      while (i < N && isLower(S[i]))
        ++i;
      return i == N ? true : false;
    }

    // Otherwise
    else {
      i = 1;

      // Check if all characters
      // are in uppercase or not
      while (i < N && isUpper(S[i]))
        ++i;

      // If all characters are
      // in uppercase
      if (i == N)
        return true;
      else if (i > 1)
        return false;

      // Check if all characters except
      // the first are in lowercase
      while (i < N && isLower(S[i]))
        ++i;
      return i == N ? true : false;
    }
  }

  // Function to check if uppercase
  // characters are used correctly or not
  static void detectUppercaseUse(string S)
  {

    // Stores whether the use of uppercase
    // characters are correct or not
    bool check = detectUppercaseUseUtil(S);

    // If correct
    if (check)
      Console.WriteLine("Yes");

    // Otherwise
    else
      Console.WriteLine("No");
  }

  // Driver Code
  static public void Main ()
  {

    // Given string
    string S = "GeeKs";

    // Function call to check if use of
    // uppercase characters is correct or not
    detectUppercaseUse(S);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to check if the
      // character c is in lowercase or not
      function isLower(str) {
        return str === str.toLowerCase();
      }

      // Function to check if the
      // character c is in uppercase or not
      function isUpper(str) {
        return str === str.toUpperCase();
      }

      // Utility function to check if uppercase
      // characters are used correctly or not
      function detectUppercaseUseUtil(S) {
        // Length of string
        var N = S.length;
        var i;

        // If the first character is in lowercase
        if (isLower(S[0])) {
          i = 1;
          while (S[i] && isLower(S[i])) ++i;
          return i === N ? true : false;
        }

        // Otherwise
        else {
          i = 1;

          // Check if all characters
          // are in uppercase or not
          while (S[i] && isUpper(S[i])) ++i;

          // If all characters are
          // in uppercase
          if (i === N) return true;
          else if (i > 1) return false;

          // Check if all characters except
          // the first are in lowercase
          while (S[i] && isLower(S[i])) ++i;
          return i === N ? true : false;
        }
      }

      // Function to check if uppercase
      // characters are used correctly or not
      function detectUppercaseUse(S) {
        // Stores whether the use of uppercase
        // characters are correct or not
        var check = detectUppercaseUseUtil(S);

        // If correct
        if (check) document.write("Yes");
        // Otherwise
        else document.write("No");
      }

      // Driver Code
      // Given string
      var S = "GeeKs";
      // Function call to check if use of
      // uppercase characters is correct or not
      detectUppercaseUse(S);
    </script>
```

**Output:** 

```
No
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)