# 打印给定字符串的最长前缀，也是同一字符串的后缀

> 原文:[https://www . geesforgeks . org/print-给定字符串中最长的前缀，也是相同字符串的后缀/](https://www.geeksforgeeks.org/print-the-longest-prefix-of-the-given-string-which-is-also-the-suffix-of-the-same-string/)

给定一个字符串 **str** ，任务是找到最长的前缀，也是给定字符串的后缀。前缀和后缀不应重叠。如果没有这样的前缀，则打印 **-1** 。

**示例:**

> **输入:** str = "aabcdaabc"
> **输出:** aabc
> 字符串“aabc”是最长的
> 前缀，也是后缀。
> 
> **输入:**str = " AAAA "
> T3】输出: aa

**做法:**思路是采用 [KMP](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/) 搜索的预处理算法。在该算法中，我们构建 **lps** 数组，该数组存储以下值:

> **lps[i]** =最长的**前缀 pat[0..i]**
> 也是**pat【0】的后缀..i]** 。

我们用上面的方法得到长度，然后从前面打印相同数量的字符，这就是我们的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Returns length of the longest prefix
// which is also suffix and the two do
// not overlap. This function mainly is
// copy of computeLPSArray() in KMP Algorithm
int LengthlongestPrefixSuffix(string s)
{
    int n = s.length();

    int lps[n];

    // lps[0] is always 0
    lps[0] = 0;

    // Length of the previous
    // longest prefix suffix
    int len = 0;

    // Loop to calculate lps[i]
    // for i = 1 to n - 1
    int i = 1;
    while (i < n) {
        if (s[i] == s[len]) {
            len++;
            lps[i] = len;
            i++;
        }
        else {

            // This is tricky. Consider
            // the example. AAACAAAA
            // and i = 7\. The idea is
            // similar to search step.
            if (len != 0) {
                len = lps[len - 1];

                // Also, note that we do
                // not increment i here
            }

            // If len = 0
            else {
                lps[i] = 0;
                i++;
            }
        }
    }

    int res = lps[n - 1];

    // Since we are looking for
    // non overlapping parts
    return (res > n / 2) ? n / 2 : res;
}

// Function that returns the prefix
string longestPrefixSuffix(string s)
{
    // Get the length of the longest prefix
    int len = LengthlongestPrefixSuffix(s);

    // Stores the prefix
    string prefix = "";

    // Traverse and add characters
    for (int i = 0; i < len; i++)
        prefix += s[i];

    // Returns the prefix
    return prefix;
}

// Driver code
int main()
{
    string s = "abcab";
    string ans = longestPrefixSuffix(s);
    if (ans == "")
        cout << "-1";
    else
        cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Returns length of the longest prefix
// which is also suffix and the two do
// not overlap. This function mainly is
// copy of computeLPSArray() in KMP Algorithm
static int LengthlongestPrefixSuffix(String s)
{
    int n = s.length();

    int lps[] = new int[n];

    // lps[0] is always 0
    lps[0] = 0;

    // Length of the previous
    // longest prefix suffix
    int len = 0;

    // Loop to calculate lps[i]
    // for i = 1 to n - 1
    int i = 1;
    while (i < n)
    {
        if (s.charAt(i) == s.charAt(len))
        {
            len++;
            lps[i] = len;
            i++;
        }
        else
        {

            // This is tricky. Consider
            // the example. AAACAAAA
            // and i = 7\. The idea is
            // similar to search step.
            if (len != 0)
            {
                len = lps[len - 1];

                // Also, note that we do
                // not increment i here
            }

            // If len = 0
            else
            {
                lps[i] = 0;
                i++;
            }
        }
    }

    int res = lps[n - 1];

    // Since we are looking for
    // non overlapping parts
    return (res > n / 2) ? n / 2 : res;
}

// Function that returns the prefix
static String longestPrefixSuffix(String s)
{
    // Get the length of the longest prefix
    int len = LengthlongestPrefixSuffix(s);

    // Stores the prefix
    String prefix = "";

    // Traverse and add characters
    for (int i = 0; i < len; i++)
        prefix += s.charAt(i);

    // Returns the prefix
    return prefix;
}

// Driver code
public static void main(String[] args)
{
    String s = "abcab";
    String ans = longestPrefixSuffix(s);
    if (ans == "")
        System.out.println("-1");
    else
        System.out.println(ans);
}
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Returns length of the longest prefix
# which is also suffix and the two do
# not overlap. This function mainly is
# copy of computeLPSArray() in KMP Algorithm
def LengthlongestPrefixSuffix(s):
    n = len(s)

    lps = [0 for i in range(n)]

    # Length of the previous
    # longest prefix suffix
    len1 = 0

    # Loop to calculate lps[i]
    # for i = 1 to n - 1
    i = 1
    while (i < n):
        if (s[i] == s[len1]):
            len1 += 1
            lps[i] = len1
            i += 1

        else:

            # This is tricky. Consider
            # the example. AAACAAAA
            # and i = 7\. The idea is
            # similar to search step.
            if (len1 != 0):
                len1 = lps[len1 - 1]

                # Also, note that we do
                # not increment i here

            # If len = 0
            else:
                lps[i] = 0
                i += 1

    res = lps[n - 1]

    # Since we are looking for
    # non overlapping parts
    if (res > int(n / 2)):
        return int(n / 2)
    else:
        return res

# Function that returns the prefix
def longestPrefixSuffix(s):

    # Get the length of the longest prefix
    len1 = LengthlongestPrefixSuffix(s)

    # Stores the prefix
    prefix = ""

    # Traverse and add characters
    for i in range(len1):
        prefix += s[i]

    # Returns the prefix
    return prefix

# Driver code
if __name__ == '__main__':
    s = "abcab"
    ans = longestPrefixSuffix(s)
    if (ans == ""):
        print("-1")
    else:
        print(ans)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Returns length of the longest prefix
    // which is also suffix and the two do
    // not overlap. This function mainly is
    // copy of computeLPSArray() in KMP Algorithm
    static int LengthlongestPrefixSuffix(string s)
    {
        int n = s.Length;

        int []lps = new int[n];

        // lps[0] is always 0
        lps[0] = 0;

        // Length of the previous
        // longest prefix suffix
        int len = 0;

        // Loop to calculate lps[i]
        // for i = 1 to n - 1
        int i = 1;
        while (i < n)
        {
            if (s[i] == s[len])
            {
                len++;
                lps[i] = len;
                i++;
            }
            else
            {

                // This is tricky. Consider
                // the example. AAACAAAA
                // and i = 7\. The idea is
                // similar to search step.
                if (len != 0)
                {
                    len = lps[len - 1];

                    // Also, note that we do
                    // not increment i here
                }

                // If len = 0
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        int res = lps[n - 1];

        // Since we are looking for
        // non overlapping parts
        return (res > n / 2) ? n / 2 : res;
    }

    // Function that returns the prefix
    static String longestPrefixSuffix(string s)
    {
        // Get the length of the longest prefix
        int len = LengthlongestPrefixSuffix(s);

        // Stores the prefix
        string prefix = "";

        // Traverse and add characters
        for (int i = 0; i < len; i++)
            prefix += s[i];

        // Returns the prefix
        return prefix;
    }

    // Driver code
    public static void Main()
    {
        string s = "abcab";
        string ans = longestPrefixSuffix(s);
        if (ans == "")
            Console.WriteLine("-1");
        else
            Console.WriteLine(ans);
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Returns length of the longest prefix
// which is also suffix and the two do
// not overlap. This function mainly is
// copy of computeLPSArray() in KMP Algorithm
function LengthlongestPrefixSuffix(s)
{
    var n = s.length;

    var lps = Array.from({length: n}, (_, i) => 0);

    // lps[0] is always 0
    lps[0] = 0;

    // Length of the previous
    // longest prefix suffix
    var len = 0;

    // Loop to calculate lps[i]
    // for i = 1 to n - 1
    var i = 1;
    while (i < n)
    {
        if (s.charAt(i) == s.charAt(len))
        {
            len++;
            lps[i] = len;
            i++;
        }
        else
        {

            // This is tricky. Consider
            // the example. AAACAAAA
            // and i = 7\. The idea is
            // similar to search step.
            if (len != 0)
            {
                len = lps[len - 1];

                // Also, note that we do
                // not increment i here
            }

            // If len = 0
            else
            {
                lps[i] = 0;
                i++;
            }
        }
    }

    var res = lps[n - 1];

    // Since we are looking for
    // non overlapping parts
    return (res > n / 2) ? n / 2 : res;
}

// Function that returns the prefix
function longestPrefixSuffix(s)
{
    // Get the length of the longest prefix
    var len = LengthlongestPrefixSuffix(s);

    // Stores the prefix
    var prefix = "";

    // Traverse and add characters
    for (var i = 0; i < len; i++)
        prefix += s.charAt(i);

    // Returns the prefix
    return prefix;
}

// Driver code
var s = "abcab";
var ans = longestPrefixSuffix(s);
if (ans == "")
    document.write("-1");
else
    document.write(ans);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
ab
```