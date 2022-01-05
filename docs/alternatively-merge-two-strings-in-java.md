# 在 Java 中交替合并两个字符串

> 原文:[https://www . geesforgeks . org/alternative-merge-two-string-in-Java/](https://www.geeksforgeeks.org/alternatively-merge-two-strings-in-java/)

给定 2 个字符串，以另一种方式合并它们，即最终字符串的第一个字符是第一个字符串的第一个字符，最终字符串的第二个字符是第二个字符串的第一个字符，以此类推。如果一旦到达一个字符串的末尾，而另一个字符串仍然存在，则将该字符串的剩余部分追加到最终字符串中

**示例:**

```
Input : string 1 :"geeks"
        string 2 :"forgeeks"
Output: "gfeoerkgseeks"
Explanation : The answer contains characters from alternate strings, and once 
the first string ends the remaining of the second string is added to the final string

Input :string 1 :"hello"
        string 2 :"geeks"
Output : hgeelelkos
```

想法很简单，我们创建一个结果字符串。我们以交替的方式一个接一个地附加两个给定字符串的字符。

## C++

```
// C++ code to alternatively merge two strings
#include <bits/stdc++.h>
using namespace std;

// Function for alternatively merging two strings
string merge(string s1, string s2)
{
    // To store the final string
    string result = "";

    // For every index in the strings
    for (int i = 0; i < s1.length() ||
                    i < s2.length(); i++)
    {

        // First choose the ith character of the
        // first string if it exists
        if (i < s1.length())
            result += s1[i];

        // Then choose the ith character of the
        // second string if it exists
        if (i < s2.length())
            result += s2[i];
    }
    return result;
}

// Driver code
int main()
{
    string s1 = "geeks";
    string s2 = "forgeeks";
    cout << merge(s1, s2);

    return 0;
}

// This code is contributed by gp6
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to alternatively merge two strings
public class mergeString {

    // Function for alternatively merging two strings
    public static String merge(String s1, String s2)
    {
        // To store the final string
        StringBuilder result = new StringBuilder();

        // For every index in the strings
        for (int i = 0; i < s1.length() || i < s2.length(); i++) {

            // First choose the ith character of the
            // first string if it exists
            if (i < s1.length())
                result.append(s1.charAt(i));

            // Then choose the ith character of the
            // second string if it exists
            if (i < s2.length())
                result.append(s2.charAt(i));
        }

        return result.toString();
    }

    // Driver code
    public static void main(String[] args)
    {
        String s1 = "geeks";
        String s2 = "forgeeks";
        System.out.println(merge(s1, s2));
    }
}
```

## 蟒蛇 3

```
# Python3 code to alternatively merge two strings

# Function for alternatively merging two strings
def merge(s1, s2):

    # To store the final string
    result = ""

    # For every index in the strings
    i = 0
    while (i < len(s1)) or (i < len(s2)):

        # First choose the ith character of the
        # first string if it exists
        if (i < len(s1)):
            result += s1[i]

        # Then choose the ith character of the
        # second string if it exists
        if (i < len(s2)):
            result += s2[i]

        i += 1

    return result

# Driver Code
s1 = "geeks"
s2 = "forgeeks"

print(merge(s1, s2))

# This code is contributed by divyesh072019
```

## C#

```
// C# code to alternatively merge two strings
using System;
class GFG {

    // Function for alternatively merging two strings
    static string merge(string s1, string s2)
    {
        // To store the final string
        string result = "";

        // For every index in the strings
        for (int i = 0; i < s1.Length || i < s2.Length; i++)
        {

            // First choose the ith character of the
            // first string if it exists
            if (i < s1.Length)
                result += s1[i];

            // Then choose the ith character of the
            // second string if it exists
            if (i < s2.Length)
                result += s2[i];
        }
        return result;
    } 

  static void Main() {
        string s1 = "geeks";
        string s2 = "forgeeks";
        Console.WriteLine(merge(s1, s2));
  }
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
gfeoerkgseeks
```