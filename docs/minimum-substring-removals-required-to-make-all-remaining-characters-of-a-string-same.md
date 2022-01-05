# 使一个字符串的所有剩余字符相同所需的最小子字符串删除量

> 原文:[https://www . geesforgeks . org/minimum-substring-removes-required-to-make-所有剩余字符的字符串-相同/](https://www.geeksforgeeks.org/minimum-substring-removals-required-to-make-all-remaining-characters-of-a-string-same/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是找到需要移除的最小子字符串数，以使该字符串的所有剩余字符相同。

***注意:***[*要删除的子串*](https://www.geeksforgeeks.org/program-print-substrings-given-string/) *不能包含字符串中最后一个剩余字符。*

**示例:**

> **输入:** str = "ACBDAB"
> **输出:** 2
> **解释:**
> 删除子串{ str[1]，…，str[3] }将 str 修改为“AAB”
> 删除子串{str[2] }将 str 修改为“AA”
> 由于 str 的所有字符都是相等的，因此所需的输出为 2。
> 
> **输入:** str = "ZBCDEFZ"
> **输出:** 1
> **解释:**
> 删除子串{ str[1]，…，str[5] }将 str 修改为“ZZ”
> 由于 str 的所有字符都是相等的，所以需要的输出为 1。

**方法:**思路是先[去掉字符串](https://www.geeksforgeeks.org/remove-consecutive-duplicates-string/)的所有连续重复字符，统计字符串每个不同字符的[频率。最后，删除字符串中除最小频率字符以外的所有字符。按照以下步骤解决问题:](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的所有字符，[删除字符串](https://www.geeksforgeeks.org/remove-consecutive-duplicates-string/)的所有连续重复字符。
*   [统计字符串中每个不同字符的出现频率](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)并将字符串的第一个和最后一个字符的出现频率递减 **1** 。
*   最后，打印获得的最小频率。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum operations
// required to make all characters equal
// by repeatedly removing substring
void minOperationNeeded(string str)
{
    // Remove consecutive duplicate
    // characters from str
    str = string(str.begin(),
                 unique(str.begin(), str.end()));

    // Stores length of the string
    int N = str.length();

    // Stores frequency of each distinct
    // characters of the string str
    int res[256] = { 0 };

    // Iterate over all the characters
    // of the string str
    for (int i = 0; i < N; ++i) {

        // Update frequency of str[i]
        res[str[i]] += 1;
    }

    // Decrementing the frequency
    // of the string str[0]
    res[str[0]] -= 1;

    // Decrementing the frequency
    // of the string str[N - 1]
    res[str[N - 1]] -= 1;

    // Stores the required count
    int ans = INT_MAX;

    // Iterate over all characters
    // of the string str
    for (int i = 0; i < N; ++i) {

        // Update ans
        ans = min(ans, res[str[i]]);
    }

    cout << (ans + 1) << endl;
}

// Driver Code
int main()
{
    // Given string
    string str = "ABCDABCDABCDA";

    minOperationNeeded(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to count minimum operations
    // required to make all characters equal
    // by repeatedly removing subString
    static void minOperationNeeded(char[] str)
    {

        // Remove consecutive duplicate
        // characters from str
        str = modstring(str);

        // Stores length of the String
        int N = str.length;

        // Stores frequency of each distinct
        // characters of the String str
        int res[] = new int[256];

        // Iterate over all the characters
        // of the String str
        for (int i = 0; i < N; ++i) {

            // Update frequency of str[i]
            res[str[i]] += 1;
        }

        // Decrementing the frequency
        // of the String str[0]
        res[str[0]] -= 1;

        // Decrementing the frequency
        // of the String str[N - 1]
        res[str[N - 1]] -= 1;

        // Stores the required count
        int ans = Integer.MAX_VALUE;

        // Iterate over all characters
        // of the String str
        for (int i = 0; i < N; ++i) {

            // Update ans
            ans = Math.min(ans, res[str[i]]);
        }

        System.out.print((ans + 1) + "\n");
    }

    private static char[] modstring(char[] str) {
        String s = "";
        boolean b = true;
        for (int i = 1; i < str.length; ++i) {
            if (str[i - 1] != str[i])
                b = true;
            if (b) {
                s += str[i-1];
                b = false;
            }

        }
        return s.toCharArray();
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given String
        String str = "ABCDABCDABCDA";

        minOperationNeeded(str.toCharArray());
    }
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import re, sys

# Function to count minimum operations
# required to make all characters equal
# by repeatedly removing substring
def minOperationNeeded(s):

    # Remove consecutive duplicate
    # characters from str
    d = {}

    str = re.sub(r"(.)\1 + ",'', s)

    # Stores length of the string
    N = len(str)

    # Stores frequency of each distinct
    # characters of the string str
    res = [0 for i in range(256)]

    # Iterate over all the characters
    # of the string str
    for i in range(N):

        # Update frequency of str[i]
        res[ord(str[i])] += 1

    # Decrementing the frequency
    # of the string str[0]
    res[ord(str[0])] -= 1

    # Decrementing the frequency
    # of the ord(string ord(str[N - 1]
    res[ord(str[N - 1])] -= 1

    # Stores the required count
    ans = sys.maxsize

    # Iterate over all characters
    # of the string str
    for i in range(N):

        # Update ans
        ans = min(ans, res[ord(str[i])])

    print ((ans + 1))

# Driver Code
if __name__ == '__main__':

    # Given string
    str = "ABCDABCDABCDA"

    minOperationNeeded(str)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

    // Function to count minimum operations
    // required to make all characters equal
    // by repeatedly removing subString
    static void minOperationNeeded(char[] str)
    {

        // Remove consecutive duplicate
        // characters from str
        str = modstring(str);

        // Stores length of the String
        int N = str.Length;

        // Stores frequency of each distinct
        // characters of the String str
        int[] res = new int[256];

        // Iterate over all the characters
        // of the String str
        for (int i = 0; i < N; ++i)
        {

            // Update frequency of str[i]
            res[str[i]] += 1;
        }

        // Decrementing the frequency
        // of the String str[0]
        res[str[0]] -= 1;

        // Decrementing the frequency
        // of the String str[N - 1]
        res[str[N - 1]] -= 1;

        // Stores the required count
        int ans = Int32.MaxValue;

        // Iterate over all characters
        // of the String str
        for (int i = 0; i < N; ++i)
        {

            // Update ans
            ans = Math.Min(ans, res[str[i]]);
        }

         Console.WriteLine((ans + 1) + "\n");
    }

    private static char[] modstring(char[] str)
    {
        string s = "";
        bool b = true;
        for (int i = 1; i < str.Length; ++i)
        {
            if (str[i - 1] != str[i])
                b = true;
            if (b)
            {
                s += str[i - 1];
                b = false;
            }

        }
        return s.ToCharArray();
    }

    // Driver Code
    public static void Main()
    {

        // Given String
        string str = "ABCDABCDABCDA";
        minOperationNeeded(str.ToCharArray());
    }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count minimum operations
      // required to make all characters equal
      // by repeatedly removing subString
      function minOperationNeeded(str) {
        // Remove consecutive duplicate
        // characters from str
        str = modstring(str);

        // Stores length of the String
        var N = str.length;

        // Stores frequency of each distinct
        // characters of the String str
        var res = new Array(256).fill(0);

        // Iterate over all the characters
        // of the String str
        for (var i = 0; i < N; ++i) {
          // Update frequency of str[i]
          res[str[i].charCodeAt(0)] += 1;
        }

        // Decrementing the frequency
        // of the String str[0]
        res[str[0].charCodeAt(0)] -= 1;

        // Decrementing the frequency
        // of the String str[N - 1]
        res[str[N - 1].charCodeAt(0)] -= 1;

        // Stores the required count(Max Integer value)
        var ans = 2147483647;

        // Iterate over all characters
        // of the String str
        for (var i = 0; i < N; ++i) {
          // Update ans
          ans = Math.min(ans, res[str[i].charCodeAt(0)]);
        }

        document.write(ans + 1 + "<br>");
      }

      function modstring(str) {
        var s = "";
        var b = true;
        for (var i = 1; i < str.length; ++i) {
          if (str[i - 1] !== str[i]) b = true;
          if (b) {
            s += str[i - 1];
            b = false;
          }
        }
        return s.split("");
      }

      // Driver Code
      // Given String
      var str = "ABCDABCDABCDA";
      minOperationNeeded(str.split(""));
    </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(256)