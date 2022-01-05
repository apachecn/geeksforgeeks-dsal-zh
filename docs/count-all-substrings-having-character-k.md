# 统计所有字符为 K 的子串

> 原文:[https://www . geesforgeks . org/count-all-substrings-having-character-k/](https://www.geeksforgeeks.org/count-all-substrings-having-character-k/)

给定一个字符串 **str** 和一个字符 **K** ，任务是找到包含字符 **K** 的 **str** 的所有子字符串的计数。
**示例:**

> **输入:** str = "geeks "，K = 'g'
> **输出:**5
> “g”、“ge”、“gee”、“geek”和“geeks”为有效子串。
> **输入:** str = "geeksforgeeks "，K = 'k'
> **输出:** 56

**天真的方法**一个简单的方法是找到给定字符串中具有字符 K 的所有子字符串，并返回计数；
**有效方法:**对于字符串中的每个索引 **i** ，找到第一个索引 **j** ，使得 **i ≤ j** 和 **str[j] = K** 。现在，子字符串 **str[i…j]，str[i…j + 1]，str[i…j + 2]，…，str[I…n–1]**都将包含字符 **K** 至少一次。开始看起来是 O(n <sup>2</sup> )的方法，但是对于每一个指标 **i** ， **j** 将不再计算指标 **j** ，对于所有小于 **j** 的 **i** 的值来说，该指标将是一个有效的指标。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the index of the
// next occurrence of character ch in str
// starting from the given index
int nextOccurrence(string str, int n,
                   int start, char ch)
{
    for (int i = start; i < n; i++) {

        // Return the index of the first
        // occurrence of ch
        if (str[i] == ch)
            return i;
    }

    // No occurrence found
    return -1;
}

// Function to return the count of all
// the substrings of str which contain
// the character ch at least one
int countSubStr(string str, int n, char ch)
{

    // To store the count of valid substrings
    int cnt = 0;

    // Index of the first occurrence of ch in str
    int j = nextOccurrence(str, n, 0, ch);
    for (int i = 0; i < n; i++) {
        while (j != -1 && j < i) {
            j = nextOccurrence(str, n, j + 1, ch);
        }

        // No occurrence of ch after index i in str
        if (j == -1)
            break;

        // Substrings starting at index i
        // and ending at indices j, j+1, ..., n-1
        // are all valid substring
        cnt += (n - j);
    }

    return cnt;
}

// Driver code
int main()
{

    string str = "geeksforgeeks";
    int n = str.length();
    char ch = 'k';

    cout << countSubStr(str, n, ch);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the index of the
    // next occurrence of character ch in str
    // starting from the given index
    static int nextOccurrence(String str, int n,
                              int start, char ch)
    {
        for (int i = start; i < n; i++)
        {

            // Return the index of the first
            // occurrence of ch
            if (str.charAt(i) == ch)
                return i;
        }

        // No occurrence found
        return -1;
    }

    // Function to return the count of all
    // the substrings of str which contain
    // the character ch at least one
    static int countSubStr(String str,
                           int n, char ch)
    {

        // To store the count of valid substrings
        int cnt = 0;

        // Index of the first occurrence of ch in str
        int j = nextOccurrence(str, n, 0, ch);
        for (int i = 0; i < n; i++)
        {
            while (j != -1 && j < i)
            {
                j = nextOccurrence(str, n, j + 1, ch);
            }

            // No occurrence of ch after index i in str
            if (j == -1)
                break;

            // Substrings starting at index i
            // and ending at indices j, j+1, ..., n-1
            // are all valid substring
            cnt += (n - j);
        }
        return cnt;
    }

    // Driver code
    static public void main ( String []arg)
    {
        String str = "geeksforgeeks";
        int n = str.length();
        char ch = 'k';

        System.out.println(countSubStr(str, n, ch));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the index of the
# next occurrence of character ch in strr
# starting from the given index
def nextOccurrence(strr, n, start, ch):
    for i in range(start, n):

        # Return the index of the first
        # occurrence of ch
        if (strr[i] == ch):
            return i

    # No occurrence found
    return -1

# Function to return the count of all
# the substrings of strr which contain
# the character ch at least one
def countSubStr(strr, n, ch):

    # To store the count of valid substrings
    cnt = 0

    # Index of the first occurrence of ch in strr
    j = nextOccurrence(strr, n, 0, ch)

    for i in range(n):
        while (j != -1 and j < i):
            j = nextOccurrence(strr, n, j + 1, ch)

        # No occurrence of ch after index i in strr
        if (j == -1):
            break

        # Substrings starting at index i
        # and ending at indices j, j+1, ..., n-1
        # are all valid substring
        cnt += (n - j)

    return cnt

# Driver code
strr = "geeksforgeeks"
n = len(strr)
ch = 'k'

print(countSubStr(strr, n, ch))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the index of the
    // next occurrence of character ch in str
    // starting from the given index
    static int nextOccurrence(String str, int n,
                               int start, char ch)
    {
        for (int i = start; i < n; i++)
        {

            // Return the index of the first
            // occurrence of ch
            if (str[i] == ch)
                return i;
        }

        // No occurrence found
        return -1;
    }

    // Function to return the count of all
    // the substrings of str which contain
    // the character ch at least one
    static int countSubStr(String str,
                           int n, char ch)
    {

        // To store the count of valid substrings
        int cnt = 0;

        // Index of the first occurrence of ch in str
        int j = nextOccurrence(str, n, 0, ch);
        for (int i = 0; i < n; i++)
        {
            while (j != -1 && j < i)
            {
                j = nextOccurrence(str, n, j + 1, ch);
            }

            // No occurrence of ch after index i in str
            if (j == -1)
                break;

            // Substrings starting at index i
            // and ending at indices j, j+1, ..., n-1
            // are all valid substring
            cnt += (n - j);
        }
        return cnt;
    }

    // Driver code
    static public void Main ()
    {
        String str = "geeksforgeeks";
        int n = str.Length;
        char ch = 'k';

        Console.WriteLine(countSubStr(str, n, ch));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the index of the
      // next occurrence of character ch in str
      // starting from the given index
      function nextOccurrence(str, n, start, ch) {
        for (var i = start; i < n; i++) {
          // Return the index of the first
          // occurrence of ch
          if (str[i] === ch) return i;
        }

        // No occurrence found
        return -1;
      }

      // Function to return the count of all
      // the substrings of str which contain
      // the character ch at least one
      function countSubStr(str, n, ch) {
        // To store the count of valid substrings
        var cnt = 0;

        // Index of the first occurrence of ch in str
        var j = nextOccurrence(str, n, 0, ch);
        for (var i = 0; i < n; i++) {
          while (j !== -1 && j < i) {
            j = nextOccurrence(str, n, j + 1, ch);
          }

          // No occurrence of ch after index i in str
          if (j === -1) break;

          // Substrings starting at index i
          // and ending at indices j, j+1, ..., n-1
          // are all valid substring
          cnt += n - j;
        }
        return cnt;
      }

      // Driver code
      var str = "geeksforgeeks";
      var n = str.length;
      var ch = "k";

      document.write(countSubStr(str, n, ch));
    </script>
```

**Output:** 

```
56
```