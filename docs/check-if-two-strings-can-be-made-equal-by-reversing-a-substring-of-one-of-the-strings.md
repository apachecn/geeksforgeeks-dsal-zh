# 通过反转其中一个字符串的子字符串来检查两个字符串是否可以相等

> 原文:[https://www . geesforgeks . org/check-if-two-strings-通过反转字符串中的一个子字符串可以使其相等/](https://www.geeksforgeeks.org/check-if-two-strings-can-be-made-equal-by-reversing-a-substring-of-one-of-the-strings/)

给定两个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **X** 和 **Y** ，任务是通过将 **X** 的任何子字符串恰好反转一次来检查这两个字符串是否可以相等。如果可能，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**X =“adcbef”，Y =“abcdef”
> **输出:**是
> **说明:**通过反转字符串 X 的子字符串“dcb”可以使字符串相等
> 
> **输入:**X =“126543”，Y =“123456”
> **输出:**是
> **说明:**通过反转字符串 X 的子串“6543”可以使字符串相等

**天真方法:**解决问题最简单的方法是反转字符串 **X** 的每个可能的子串，对于每个反转，检查两个字符串是否相等。如果反转后发现是真的，则打印**“是”**。否则，打印“否”。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，请按照以下步骤解决问题:

*   初始化一个变量，比如说 **L** 为 **-1** ，以存储左边第一个在两个字符串中有不相等字符的索引。
*   [使用变量 **i** 在范围**【0，N–1】**上遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **X** ，如果对于任何索引，如果发现两个字符串中的字符不相等，则设置 **L = i** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   初始化一个变量，比如说 **R** 为 **-1** ，从右边开始存储两个字符串中不相等字符的第一个索引。
*   [使用变量 **i** 在范围**【N–1，0】**内遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **X** ，如果对于任何索引，如果发现两个字符串中的字符不相等，则设置 **R = i** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   [在索引**【L，R】**](https://www.geeksforgeeks.org/reverse-the-given-string-in-the-range-l-r/)上反转字符串 **X** 的字符。
*   完成上述步骤后，[检查两个字符串是否相等](https://www.geeksforgeeks.org/program-to-check-if-two-strings-are-same-or-not/)。如果发现相等，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the strings
// can be made equal or not by
// reversing a substring of X
bool checkString(string X, string Y)
{
    // Store the first index from
    // the left which contains unequal
    // characters in both the strings
    int L = -1;

    // Store the first element from
    // the right which contains unequal
    // characters in both the strings
    int R = -1;

    // Checks for the first index from
    // left in which characters in both
    // the strings are unequal
    for (int i = 0; i < X.length(); ++i) {

        if (X[i] != Y[i]) {

            // Store the current index
            L = i;

            // Break out of the loop
            break;
        }
    }

    // Checks for the first index from
    // right in which characters in both
    // the strings are unequal
    for (int i = X.length() - 1; i > 0; --i) {
        if (X[i] != Y[i]) {

            // Store the current index
            R = i;

            // Break out of the loop
            break;
        }
    }

    // Reverse the substring X[L, R]
    reverse(X.begin() + L,
            X.begin() + R + 1);

    // If X and Y are equal
    if (X == Y) {
        cout << "Yes";
    }

    // Otherwise
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    string X = "adcbef", Y = "abcdef";

    // Function Call
    checkString(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the Strings
// can be made equal or not by
// reversing a subString of X
static void checkString(String X, String Y)
{
    // Store the first index from
    // the left which contains unequal
    // characters in both the Strings
    int L = -1;

    // Store the first element from
    // the right which contains unequal
    // characters in both the Strings
    int R = -1;

    // Checks for the first index from
    // left in which characters in both
    // the Strings are unequal
    for (int i = 0; i < X.length(); ++i) {

        if (X.charAt(i) != Y.charAt(i)) {

            // Store the current index
            L = i;

            // Break out of the loop
            break;
        }
    }

    // Checks for the first index from
    // right in which characters in both
    // the Strings are unequal
    for (int i = X.length() - 1; i > 0; --i) {
        if (X.charAt(i) != Y.charAt(i)) {

            // Store the current index
            R = i;

            // Break out of the loop
            break;
        }
    }

    // Reverse the subString X[L, R]
    X = X.substring(0, L) +
      reverse(X.substring(L, R + 1)) +
      X.substring(R + 1);

    // If X and Y are equal
    if (X.equals(Y)) {
        System.out.print("Yes");
    }

    // Otherwise
    else {
        System.out.print("No");
    }
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{
    String X = "adcbef", Y = "abcdef";

    // Function Call
    checkString(X, Y);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the strings
# can be made equal or not by
# reversing a substring of X
def checkString(X, Y):

    # Store the first index from
    # the left which contains unequal
    # characters in both the strings
    L = -1

    # Store the first element from
    # the right which contains unequal
    # characters in both the strings
    R = -1

    # Checks for the first index from
    # left in which characters in both
    # the strings are unequal
    for i in range(len(X)):
        if (X[i] != Y[i]):

            # Store the current index
            L = i

            # Break out of the loop
            break

    # Checks for the first index from
    # right in which characters in both
    # the strings are unequal
    for i in range(len(X) - 1, 0, -1):
        if (X[i] != Y[i]):

            # Store the current index
            R = i

            # Break out of the loop
            break

    X = list(X)

    X = X[:L] + X[R  : L - 1 : -1 ] + X[R + 1:]

    # If X and Y are equal
    if (X == list(Y)):
        print("Yes")

    # Otherwise
    else:
        print("No")

# Driver Code
if __name__ == "__main__" :

    X = "adcbef"
    Y = "abcdef"

    # Function Call
    checkString(X, Y)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the Strings
// can be made equal or not by
// reversing a subString of X
static void checkString(String X, String Y)
{

    // Store the first index from
    // the left which contains unequal
    // characters in both the Strings
    int L = -1;

    // Store the first element from
    // the right which contains unequal
    // characters in both the Strings
    int R = -1;

    // Checks for the first index from
    // left in which characters in both
    // the Strings are unequal
    for(int i = 0; i < X.Length; ++i)
    {
        if (X[i] != Y[i])
        {

            // Store the current index
            L = i;

            // Break out of the loop
            break;
        }
    }

    // Checks for the first index from
    // right in which characters in both
    // the Strings are unequal
    for(int i = X.Length - 1; i > 0; --i)
    {
        if (X[i] != Y[i])
        {

            // Store the current index
            R = i;

            // Break out of the loop
            break;
        }
    }

    // Reverse the subString X[L, R]
    X = X.Substring(0, L) +
        reverse(X.Substring(L, R + 1 - L)) +
        X.Substring(R + 1);

    // If X and Y are equal
    if (X.Equals(Y))
    {
        Console.Write("Yes");
    }

    // Otherwise
    else
    {
        Console.Write("No");
    }
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{
    String X = "adcbef", Y = "abcdef";

    // Function Call
    checkString(X, Y);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to check if the Strings
      // can be made equal or not by
      // reversing a subString of X
      function checkString(X, Y) {
        // Store the first index from
        // the left which contains unequal
        // characters in both the Strings
        var L = -1;

        // Store the first element from
        // the right which contains unequal
        // characters in both the Strings
        var R = -1;

        // Checks for the first index from
        // left in which characters in both
        // the Strings are unequal
        for (var i = 0; i < X.length; ++i) {
          if (X[i] !== Y[i]) {
            // Store the current index
            L = i;

            // Break out of the loop
            break;
          }
        }

        // Checks for the first index from
        // right in which characters in both
        // the Strings are unequal
        for (var i = X.length - 1; i > 0; --i) {
          if (X[i] !== Y[i]) {
            // Store the current index
            R = i;

            // Break out of the loop
            break;
          }
        }

        // Reverse the subString X[L, R]
        X =
          X.substring(0, L) +
          reverse(X.substring(L, R + 1)) +
          X.substring(R + 1);

        // If X and Y are equal
        if (X === Y) {
          document.write("Yes");
        }

        // Otherwise
        else {
          document.write("No");
        }
      }

      function reverse(input) {
        var a = input.split("");
        var l,
          r = a.length - 1;

        for (l = 0; l < r; l++, r--) {
          var temp = a[l];
          a[l] = a[r];
          a[r] = temp;
        }
        return a.join("");
      }

      // Driver Code
      var X = "adcbef",
        Y = "abcdef";

      // Function Call
      checkString(X, Y);

 </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)