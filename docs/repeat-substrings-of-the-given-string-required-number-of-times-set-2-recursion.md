# 重复给定字符串的子字符串所需的次数|集合 2(递归)

> 原文:[https://www . geesforgeks . org/repeat-给定字符串的子字符串-所需次数-set-2-递归/](https://www.geeksforgeeks.org/repeat-substrings-of-the-given-string-required-number-of-times-set-2-recursion/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)字符串，任务是重复字符串 **X** 的每个[子字符串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的次数，其中 **X** 是由原始字符串中子字符串后面的连续数字组成的数字。例如，如果**字符串**=“g1e2k S1”，那么结果字符串将是“极客”。

**示例:**

> **输入:** str = "2a10bd3"
> **输出:**aaaaaaaaaaabdbd
> **说明:**第一位数字“2”是不必要的，因为它前面没有有效的子串。字符“a”将重复 10 次，然后“bd”将重复 3 次。
> 
> **输入:**str = " g1e 2k S1 for 1g 2e 2k S1 "
> **输出:**geeks forges

这个问题的迭代方法已经在这里讨论过了。本文重点介绍一种解决给定问题的[递归方法](https://www.geeksforgeeks.org/recursion/)。

**方法:** [递归地逐字符遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。遍历时，将字符保存在单独的字符串中，并将代表重复次数的数字保存在一个整数中。对于找到的每一组数字，根据找到的整数将存储的字符串的出现追加到最终的结果字符串中，并且[递归调用剩余字符串的](https://www.geeksforgeeks.org/recursive-functions/)。

下面是上述方法的实现:

## C++

```
// C++ program of the above appraoch
#include <bits/stdc++.h>
using namespace std;

// Stores the final string
string res = "";

// Recursive function to generate
// the required string
void decode(string s, int i, string t, int x)
{
    // If complete string has
    // been traversed
    if (i == s.length()) {

        // Append string t, s times
        for (int i = 0; i < x; i++)
            res = res + t;
        return;
    }

    // If current character
    // is an integer
    if (isdigit(s[i]) && !t.empty()) {
        x = x * 10 + (s[i] - '0');
    }

    // If current character
    // in an alphabet
    if (!isdigit(s[i])) {
        if (!t.empty() && x > 0) {

            // Append t, x times
            for (int i = 0; i < x; i++)
                res = res + t;

            // Update the value
            // of t and x
            t = "";
            x = 0;
        }
        t = t + s[i];
    }

    // Recursive call for the
    // remaining string
    decode(s, i + 1, t, x);
}

// Function to convert the given
// string into desired form
string decodeString(string s)
{
    // Recursive Call
    decode(s, 0, "", 0);

    // Return Answer
    return res;
}

// Driven Program
int main()
{
    string str = "g1e2k1s1for1g1e2ks1";
    cout << decodeString(str);
    return 0;
}
```

**Output**

```
geeksforgeeks
```

***时间复杂度:** O(M)，其中 M 是给定字符串中存在的所有整数之和*
***辅助空间:** O(N)*