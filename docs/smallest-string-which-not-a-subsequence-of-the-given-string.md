# 不是给定字符串子序列的最小字符串

> 原文:[https://www . geeksforgeeks . org/最小字符串不是给定字符串的子序列/](https://www.geeksforgeeks.org/smallest-string-which-not-a-subsequence-of-the-given-string/)

给定一个由小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是找到不是给定字符串的[子序列](https://www.geeksforgeeks.org/tag/subsequence/)的最短字符串。如果存在多个字符串，则打印其中任何一个。

**示例:**

> **输入:** str = "abaabcc"
> **输出:** d
> **解释:**
> 不是给定字符串的子序列的一个可能的最短字符串是“d”。因此，所需的输出为“d”。
> 
> **输入:**str = " abcdefghijklmnopqrstuvwxyzaabccdd "
> T3】输出: ze

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个[字符串](https://www.geeksforgeeks.org/stdstring-class-in-c/)，比如说**短字符串**，来存储不是给定字符串的子序列的最短字符串。
*   初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如说**段**，来存储每个子段所有可能的字符。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)和[将字符串的字符插入分段](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)并检查**分段**是否包含所有小写字母。如果发现为真，则[将当前字符追加到**短字符串**](https://www.geeksforgeeks.org/stdstringpush_back-in-cpp/) 中，并删除**段**中的所有元素。
*   遍历范围**【a–z】**中所有可能的小写字母，并检查当前字符是否出现在该段中。如果发现为真，则[将当前字符插入短字符串](https://www.geeksforgeeks.org/stdstringpush_back-in-cpp/)。
*   最后，打印 **shortestString** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find shortest string which
// not a subsequence of the given string
string ShortestSubsequenceNotPresent(string str)
{

    // Stores the shortest string which is
    // not a subsequence of the given string
    string shortestString;

    // Stores length of string
    int N = str.length();

    // Stores distinct character of subsegments
    unordered_set<char> subsegments;

    // Traverse the given string
    for (int i = 0; i < N; i++) {

        // Insert current character
        // into subsegments
        subsegments.insert(str[i]);

        // If all lowercase alphabets
        // present in the subsegment
        if (subsegments.size() == 26) {

            // Insert the last character of
            // subsegment into shortestString
            shortestString.push_back(str[i]);

            // Remove all elements from
            // the current subsegment
            subsegments.clear();
        }
    }

    // Traverse all lowercase alphabets
    for (char ch = 'a'; ch <= 'z'; ch++) {

        // If current character is not
        // present in the subsegment
        if (subsegments.count(ch) == 0) {
            shortestString.push_back(ch);

            // Return shortestString
            return shortestString;
        }
    }
    return shortestString;
}

// Driver Code
int main()
{

    // Given String
    string str
        = "abcdefghijklmnopqrstuvwxyzaabbccdd";

    cout << ShortestSubsequenceNotPresent(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {
    public static String
    ShortestSubsequenceNotPresent(String str)
    {
        // Stores the shortest string which is
        // not a subsequence of the given string
        String shortestString = "";

        // Stores length of string
        int N = str.length();

        // Stores distinct character of subsegments
        HashSet<Character> subsegments = new HashSet<>();

        // Traverse the given string
        for (int i = 0; i < N; i++) {

            // Insert current character
            // into subsegments
            subsegments.add(str.charAt(i));

            // If all lowercase alphabets
            // present in the subsegment
            if (subsegments.size() == 26) {

                // Insert the last character of
                // subsegment into shortestString
                shortestString
                    = shortestString + str.charAt(i);

                // Remove all elements from
                // the current subsegment
                subsegments.clear();
            }
        }

        // Traverse all lowercase alphabets
        for (char ch = 'a'; ch <= 'z'; ch++) {

            // If current character is not
            // present in the subsegment
            if (!subsegments.contains(ch)) {
                shortestString = shortestString + ch;

                // Return shortestString
                return shortestString;
            }
        }
        return shortestString;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "abcdefghijklmnopqrstuvwxyzaabbccdd";

        System.out.print(
            ShortestSubsequenceNotPresent(str));
    }
}
// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find shortest string which
# not a subsequence of the given string
def ShortestSubsequenceNotPresent(Str):

    # Stores the shortest string which is
    # not a subsequence of the given string
    shortestString = ""

    # Stores length of string
    N = len(Str)

    # Stores distinct character of subsegments
    subsegments = set()

    # Traverse the given string
    for i in range(N):

        # Insert current character
        # into subsegments
        subsegments.add(Str[i])

        # If all lowercase alphabets
        # present in the subsegment
        if (len(subsegments) == 26) :

            # Insert the last character of
            # subsegment into shortestString
            shortestString += Str[i]

            # Remove all elements from
            # the current subsegment
            subsegments.clear()

    # Traverse all lowercase alphabets
    for ch in range(int(26)):

        # If current character is not
        # present in the subsegment
        if (chr(ch + 97) not in subsegments) :

            shortestString += chr(ch + 97)

            # Return shortestString
            return shortestString

    return shortestString

# Driver code
# Given String
Str = "abcdefghijklmnopqrstuvwxyzaabbccdd"

print(ShortestSubsequenceNotPresent(Str))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

public static String ShortestSubsequenceNotPresent(
    String str)
{

    // Stores the shortest string which is
    // not a subsequence of the given string
    String shortestString = "";

    // Stores length of string
    int N = str.Length;

    // Stores distinct character of subsegments
    HashSet<char> subsegments = new HashSet<char>();

    // Traverse the given string
    for(int i = 0; i < N; i++)
    {

        // Insert current character
        // into subsegments
        subsegments.Add(str[i]);

        // If all lowercase alphabets
        // present in the subsegment
        if (subsegments.Count == 26)
        {

            // Insert the last character of
            // subsegment into shortestString
            shortestString = shortestString + str[i];

            // Remove all elements from
            // the current subsegment
            subsegments.Clear();
        }
    }

    // Traverse all lowercase alphabets
    for(char ch = 'a'; ch <= 'z'; ch++)
    {

        // If current character is not
        // present in the subsegment
        if (!subsegments.Contains(ch))
        {
            shortestString = shortestString + ch;

            // Return shortestString
            return shortestString;
        }
    }
    return shortestString;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "abcdefghijklmnopqrstuvwxyzaabbccdd";

    Console.Write(
        ShortestSubsequenceNotPresent(str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find shortest string which
// not a subsequence of the given string
function ShortestSubsequenceNotPresent(str)
{

    // Stores the shortest string which is
    // not a subsequence of the given string
    var shortestString = [];

    // Stores length of string
    var N = str.length;

    // Stores distinct character of subsegments
    var subsegments = new Set();

    // Traverse the given string
    for (var i = 0; i < N; i++) {

        // Insert current character
        // into subsegments
        subsegments.add(str[i].charCodeAt(0));

        // If all lowercase alphabets
        // present in the subsegment
        if (subsegments.size == 26) {

            // Insert the last character of
            // subsegment into shortestString
            shortestString.push(str[i]);

            // Remove all elements from
            // the current subsegment
            subsegments = new Set();
        }
    }

    // Traverse all lowercase alphabets
    for (var ch = 'a'.charCodeAt(0);
    ch <= 'z'.charCodeAt(0); ch++) {

        // If current character is not
        // present in the subsegment
        if (!subsegments.has(ch)) {
            shortestString.push(String.fromCharCode(ch));

            // Return shortestString
            return shortestString.join("");
        }
    }
    return shortestString.join("");
}

// Driver Code

// Given String
var str = "abcdefghijklmnopqrstuvwxyzaabbccdd";

document.write( ShortestSubsequenceNotPresent(str));

</script>
```

**Output**

```
ze
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)