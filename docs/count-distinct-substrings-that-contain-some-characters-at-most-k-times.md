# 统计最多 k 次包含某些字符的不同子串

> 原文:[https://www . geeksforgeeks . org/count-distinct-substrings-最多包含一些字符-k 次/](https://www.geeksforgeeks.org/count-distinct-substrings-that-contain-some-characters-at-most-k-times/)

给定一个整数 **k** 和一个刺痛**字符串**，任务是计算**不同的**子字符串的数量，使得每个子字符串包含的特定字符不超过 **k** 次。特定字符作为另一个字符串给出。
**举例:**

> **输入:** str = "ababab "，otherStr = "bcd "，k = 1
> **输出:** 5
> 所有有效子串为“a”、“b”、“ab”、“ba”和“ABA”
> **输入:** str = "acbacbacaa "，otherStr = "ycb "，k = 2
> **输出:** 8

**进场:**

*   将另一个字符串的字符存储在大小为 256 的布尔数组中，以便快速查找
*   遍历给定字符串的所有子字符串。对于每个子字符串，保留**另一个字符串**中**非法**字符的数量。
*   如果这些字符的**计数**超过了 **k** 的值，则脱离内环。
*   否则，将这个子字符串存储在哈希表中，以保留不同的子字符串。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 256;

// Function to return the count of valid sub-strings
int countSubStrings(string s, string anotherStr, int k)
{
    // Store all characters of anotherStr in a
    // direct index table for quick lookup.
    bool illegal[MAX_CHAR] = { false };
    for (int i = 0; i < anotherStr.size(); i++)
        illegal[anotherStr[i]] = true;

    // To store distinct output substrings
    unordered_set<string> us;

    // Traverse through the given string and
    // one by one generate substrings beginning
    // from s[i].
    for (int i = 0; i < s.size(); ++i) {

        // One by one generate substrings ending
        // with s[j]
        string ss = "";
        int count = 0;
        for (int j = i; j < s.size(); ++j) {

            // If character is illegal
            if (illegal[s[j]])
                ++count;
            ss = ss + s[j];

            // If current substring is valid
            if (count <= k) {
                us.insert(ss);
            }

            // If current substring is invalid,
            // adding more characters would not
            // help.
            else
                break;
        }
    }

    // Return the count of distinct sub-strings
    return us.size();
}

// Driver code
int main()
{
    string str = "acbacbacaa";
    string anotherStr = "abcdefghijklmnopqrstuvwxyz";
    int k = 2;
    cout << countSubStrings(str, anotherStr, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    static int MAX_CHAR = 256;

    // Function to return the count of valid sub-strings
    static int countSubStrings(String s, String anotherStr, int k)
    {
        // Store all characters of anotherStr in a
        // direct index table for quick lookup.
        boolean illegal[] = new boolean[MAX_CHAR];
        for (int i = 0; i < anotherStr.length(); i++)
        {
            illegal[anotherStr.charAt(i)] = true;
        }

        // To store distinct output substrings
        HashSet<String> us = new HashSet<String>();

        // Traverse through the given string and
        // one by one generate substrings beginning
        // from s[i].
        for (int i = 0; i < s.length(); ++i)
        {

            // One by one generate substrings ending
            // with s[j]
            String ss = "";
            int count = 0;
            for (int j = i; j < s.length(); ++j)
            {

                // If character is illegal
                if (illegal[s.charAt(j)])
                {
                    ++count;
                }
                ss = ss + s.charAt(j);

                // If current substring is valid
                if (count <= k)
                {
                    us.add(ss);
                }

                // If current substring is invalid,
                // adding more characters would not
                // help.
                else
                {
                    break;
                }
            }
        }

        // Return the count of distinct sub-strings
        return us.size();
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "acbacbacaa";
        String anotherStr = "abcdefghijklmnopqrstuvwxyz";
        int k = 2;
        System.out.println(countSubStrings(str, anotherStr, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX_CHAR = 256

# Function to return the count
# of valid sub-strings
def countSubStrings(s, anotherStr, k) :

    # Store all characters of anotherStr in
    # a direct index table for quick lookup.
    illegal = [False] * MAX_CHAR

    for i in range(len(anotherStr)) :
        illegal[ord(anotherStr[i])] = True

    # To store distinct output substrings
    us = set()

    # Traverse through the given string
    # and one by one generate substrings
    # beginning from s[i].
    for i in range(len(s)) :

        # One by one generate substrings
        # ending with s[j]
        ss = ""

        count = 0
        for j in range(i, len(s)) :

            # If character is illegal
            if (illegal[ord(s[j])]) :
                count += 1
            ss = ss + s[j]

            # If current substring is valid
            if (count <= k) :
                us.add(ss)

            # If current substring is invalid,
            # adding more characters would not
            # help.
            else :
                break

    # Return the count of distinct
    # sub-strings
    return len(us)

# Driver code
if __name__ == "__main__" :

    string = "acbacbacaa"
    anotherStr = "abcdefghijklmnopqrstuvwxyz"
    k = 2
    print(countSubStrings(string,
                          anotherStr, k))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int MAX_CHAR = 256;

    // Function to return the count
    // of valid sub-strings
    static int countSubStrings(String s,
                        String anotherStr, int k)
    {

        // Store all characters of anotherStr in a
        // direct index table for quick lookup.
        bool []illegal = new bool[MAX_CHAR];
        for (int i = 0; i < anotherStr.Length; i++)
        {
            illegal[anotherStr[i]] = true;
        }

        // To store distinct output substrings
        HashSet<String> us = new HashSet<String>();

        // Traverse through the given
        // string and one by one generate
        // substrings beginning from s[i].
        for (int i = 0; i < s.Length; ++i)
        {

            // One by one generate substrings
            // ending with s[j]
            String ss = "";
            int count = 0;
            for (int j = i; j < s.Length; ++j)
            {

                // If character is illegal
                if (illegal[s[j]])
                {
                    ++count;
                }
                ss = ss + s[j];

                // If current substring is valid
                if (count <= k)
                {
                    us.Add(ss);
                }

                // If current substring is invalid,
                // adding more characters would not
                // help.
                else
                {
                    break;
                }
            }
        }

        // Return the count of distinct sub-strings
        return us.Count;
    }

    // Driver code
    public static void Main()
    {
        String str = "acbacbacaa";
        String anotherStr = "abcdefghijklmnopqrstuvwxyz";
        int k = 2;
        Console.WriteLine(countSubStrings(str, anotherStr, k));
    }
}

//This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// js implementation of the approach

let MAX_CHAR = 256;

// Function to return the count of valid sub-strings
function countSubStrings( s, anotherStr, k)
{
    // Store all characters of anotherStr in a
    // direct index table for quick lookup.
    let illegal = [];
    for(let i = 0;i<256;i++)
         illegal.push(false);
    for (let i = 0; i < anotherStr.length; i++)
        illegal[anotherStr[i]] = true;

    // To store distinct output substrings
    let us = new Set();

    // Traverse through the given string and
    // one by one generate substrings beginning
    // from s[i].
    for (let i = 0; i < s.length; ++i) {

        // One by one generate substrings ending
        // with s[j]
        let ss = "";
        let count = 0;
        for (let j = i; j < s.length; ++j) {

            // If character is illegal
            if (illegal[s[j]])
                ++count;
            ss = ss + s[j];

            // If current substring is valid
            if (count <= k) {
                us.add(ss);
            }

            // If current substring is invalid,
            // adding more characters would not
            // help.
            else
                break;
        }
    }

    // Return the count of distinct sub-strings
    return us.size;
}

// Driver code
let str = "acbacbacaa";
let anotherStr = "abcdefghijklmnopqrstuvwxyz";
let k = 2;
document.write(countSubStrings(str, anotherStr, k));

</script>
```

**Output:** 

```
8
```