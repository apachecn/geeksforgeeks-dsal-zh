# 由非重复字符组成的给定字符串的子序列

> 原文:[https://www . geeksforgeeks . org/由非重复字符组成的给定字符串的子序列/](https://www.geeksforgeeks.org/subsequences-of-given-string-consisting-of-non-repeating-characters/)

给定一个长度为 **N** 的字符串 **str** ，任务是打印字符串 **str** 的所有可能的不同[子序列，该字符串仅由非重复字符组成。](https://www.geeksforgeeks.org/print-subsequences-string/)

**示例:**

> **输入:** str = "abac"
> **输出:** a ab abc ac b ba bac bc c
> **解释:**
> 字符串的所有可能的不同子序列是{ a，aa，aac，ab，aba，abac，abc，ac，b，ba，bac，bc，c }
> 因此，仅由非重复字符组成的子序列是{ a，ab，abc，ac，b，ba，bac，bc，c }
> 
> **输入:**str = " AAA "
> T3】输出: a

**方法:**该问题可以使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)技术使用以下递归关系来解决:

> FindSub(str，res，i) = { FindSub(str，res，i + 1)，FindSub(str，res + str[i]，i + 1) }
> res =字符串的子序列
> i =字符串中某个字符的索引

按照以下步骤解决问题:

*   初始化一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如**子**，来存储所有可能的由非重复字符组成的子序列。
*   初始化另一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如 **ch** ，检查子序列中是否有字符。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并仅使用上述递归关系打印所有可能的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)，子序列由不重复的字符组成。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all the subsequences of
// the string with non-repeating characters
void FindSub(set<string>& sub, set<char>& ch, string str,
             string res, int i)
{

    // Base case
    if (i == str.length()) {

        // Insert current subsequence
        sub.insert(res);
        return;
    }

    // If str[i] is not present
    // in the current subsequence
    if (!ch.count(str[i])) {

        // Insert str[i] into the set
        ch.insert(str[i]);

        // Insert str[i] into the
        // current subsequence
        res.push_back(str[i]);
        FindSub(sub, ch, str, res, i + 1);

        // Remove str[i] from
        // current subsequence
        res.pop_back();

        // Remove str[i] from the set
        ch.erase(str[i]);
    }

    // Not including str[i] from
    // the current subsequence
    FindSub(sub, ch, str, res, i + 1);
}

// Utility function to print all subsequences
// of string with non-repeating characters
void printSubwithUniqueChar(string str, int N)
{

    // Stores all possible subsequences
    // with non-repeating characters
    set<string> sub;

    // Stores subsequence with
    // non-repeating characters
    set<char> ch;

    FindSub(sub, ch, str, "", 0);

    // Traverse all possible subsequences
    // containing non-repeating characters
    for (auto subString : sub) {

        // Print subsequence
        cout << subString << " ";
    }
}

// Driver Code
int main()
{

    string str = "abac";

    int N = str.length();

    printSubwithUniqueChar(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Javs program to implement
// the above approach

import java.util.*;

class GFG {

    // Function to find all the subsequences of
    // the string with non-repeating characters
    public static void FindSub(HashSet<String> sub,
                               HashSet<Character> ch,
                               String str, String res,
                               int i)
    {

        // Base case
        if (i == str.length()) {

            // Insert current subsequence
            sub.add(res);
            return;
        }

        // If str[i] is not present
        // in the current subsequence
        if (!ch.contains(str.charAt(i))) {

            // Insert str[i] into the set
            ch.add(str.charAt(i));

            // Insert str[i] into the
            // current subsequence
            FindSub(sub, ch, str, res + str.charAt(i),
                    i + 1);

            // Remove str[i] from the set
            ch.remove(str.charAt(i));
        }
        // Not including str[i] from
        // the current subsequence
        FindSub(sub, ch, str, res, i + 1);
    }

    // Utility function to print all subsequences
    // of string with non-repeating characters
    public static void printSubwithUniqueChar(String str,
                                              int N)
    {

        // Stores all possible subsequences
        // with non-repeating characters
        HashSet<String> sub = new HashSet<>();

        // Stores subsequence with
        // non-repeating characters
        HashSet<Character> ch = new HashSet<>();

        FindSub(sub, ch, str, "", 0);

        // Traverse all possible subsequences
        // containing non-repeating characters
        for (String subString : sub) {

            // Print subsequence
            System.out.print(subString + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {

        String str = "abac";

        int N = str.length();

        printSubwithUniqueChar(str, N);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach1

# Function to find all the subsequences of
# the str1ing with non-repeating ch1aracters
def FindSub(sub, ch1, str1, res, i):

    # Base case
    if (i == len(str1)):

        # Insert current subsequence
        sub.add(res)
        return

    # If str1[i] is not present
    # in the current subsequence
    if (str1[i] not in ch1):

        # Insert str1[i] into the set
        ch1.add(str1[i])

        # Insert str1[i] into the
        # current subsequence
        FindSub(sub, ch1, str1, res+str1[i], i + 1)
        res += str1[i]

        # Remove str1[i] from
        # current subsequence
        res = res[0:len(res) - 1]

        # Remove str1[i] from the set
        ch1.remove(str1[i])

    # Not including str1[i] from
    # the current subsequence
    FindSub(sub, ch1, str1, res, i + 1)

# Utility function to print all subsequences
# of str1ing with non-repeating ch1aracters
def printSubwithUniquech1ar(str1, N):

    # Stores all possible subsequences
    # with non-repeating ch1aracters
    sub = set()

    # Stores subsequence with
    # non-repeating ch1aracters
    ch1 = set()
    FindSub(sub, ch1, str1, "", 0)

    # Traverse all possible subsequences
    # containing non-repeating ch1aracters
    temp = []
    for substr1ing in sub:
      temp.append(substr1ing)
    temp.sort(reverse = False)
    for x in temp:

      # Print subsequence
      print(x, end = " ")

# Driver Code
if __name__ == '__main__':
    str2 = "abac"
    N = len(str2)
    printSubwithUniquech1ar(str2, N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    // Function to find all the subsequences of
    // the string with non-repeating characters
    public static void FindSub(HashSet<String> sub,
                               HashSet<char> ch,
                               String str, String res,
                               int i)
    {

        // Base case
        if (i == str.Length)
        {

            // Insert current subsequence
            sub.Add(res);
            return;
        }

        // If str[i] is not present
        // in the current subsequence
        if (!ch.Contains(str[i]))
        {

            // Insert str[i] into the set
            ch.Add(str[i]);

            // Insert str[i] into the
            // current subsequence
            FindSub(sub, ch, str, res + str[i],
                    i + 1);

            // Remove str[i] from the set
            ch.Remove(str[i]);
        }

        // Not including str[i] from
        // the current subsequence
        FindSub(sub, ch, str, res, i + 1);
    }

    // Utility function to print all subsequences
    // of string with non-repeating characters
    public static void printSubwithUniqueChar(String str,
                                              int N)
    {

        // Stores all possible subsequences
        // with non-repeating characters
        HashSet<String> sub = new HashSet<String>();

        // Stores subsequence with
        // non-repeating characters
        HashSet<char> ch = new HashSet<char>();
        FindSub(sub, ch, str, "", 0);

        // Traverse all possible subsequences
        // containing non-repeating characters
        foreach (String subString in sub)
        {

            // Print subsequence
            Console.Write(subString + " ");
        }
    }

    // Driver Code
    public static void Main(String []args)
    {
        String str = "abac";
        int N = str.Length;
        printSubwithUniqueChar(str, N);
    }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Stores all possible subsequences
// with non-repeating characters
var sub = new Set();

// Stores subsequence with
// non-repeating characters
var ch = new Set();

// Function to find all the subsequences of
// the string with non-repeating characters
function FindSub(str, res, i)
{

    // Base case
    if (i == str.length) {

        // Insert current subsequence
        sub.add(res.join(""));
        return;
    }

    // If str[i] is not present
    // in the current subsequence
    if (!ch.has(str[i])) {

        // Insert str[i] into the set
        ch.add(str[i]);

        // Insert str[i] into the
        // current subsequence
        res.push(str[i]);
        FindSub(str, res, i + 1);
        res.pop()

        // Remove str[i] from the set
        ch.delete(str[i]);
    }

    // Not including str[i] from
    // the current subsequence
    FindSub(str, res, i + 1);
}

// Utility function to print all subsequences
// of string with non-repeating characters
function printSubwithUniqueChar(str, N)
{

    FindSub(str, [], 0);

    var tmp = [...sub].sort();

    // Traverse all possible subsequences
    // containing non-repeating characters
    tmp.forEach(subString => {
        // Print subsequence
        document.write( subString + " ");
    });
}

// Driver Code
var str = "abac";
var N = str.length;
printSubwithUniqueChar(str, N);

</script>
```

**Output:** 

```
a ab abc ac b ba bac bc c
```

**时间复杂度**:O(N * log(N)* 2<sup>N</sup>)
T5】辅助空间 O(N * 2 <sup>N</sup>