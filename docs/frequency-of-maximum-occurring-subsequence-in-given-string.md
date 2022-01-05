# 给定字符串中最大出现子序列的频率

> 原文:[https://www . geesforgeks . org/给定字符串中最大出现子序列的频率/](https://www.geeksforgeeks.org/frequency-of-maximum-occurring-subsequence-in-given-string/)

给定一个由小写英文字母组成的字符串 **str** ，我们的任务是找到出现次数最多的字符串的子序列的[出现频率。](https://www.geeksforgeeks.org/find-number-times-string-occurs-given-string/)

**示例:**

> **输入:** s = "aba"
> **输出:** 2
> **解释:**
> 对于“aba”，子序列“ab”在子序列‘ab’和‘ABA’中出现次数最多。
> 
> **输入:** s = "acbab"
> **输出:** 3
> **说明:**
> 对于“acbab”，“ab”出现 3 次，为最大值。

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。为了解决上述问题，关键的观察是，结果子序列将具有长度 **1 或 2** ，因为长度**长度> 2** 的任何子序列的频率将低于长度 **1 或 2** 的子序列，因为它们也存在于更长的子序列中。所以我们只需要检查长度为 1 或 2 的子序列。以下是步骤:

*   对于长度 1，计算字符串中每个字母的频率。
*   对于长度 2，形成一个 2D 数组 **dp[26][26]** ，其中 dp[i][j]表示**字符(' a' + i) +字符(' a' + j)** 的字符串频率。
*   步骤 2 中使用的递归关系由下式给出:

> dp[i][j] = dp[i][j] + freq[i]
> 其中，
> freq[i] =字符 char 的频率(' a '+I)
> DP[I][j]= current _ char+char(' a '+I)形成的字符串的频率。

*   频率数组和数组**的最大值 dp[][]** 给出给定字符串中任何子序列的最大计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to find the frequency
ll findCount(string s)
{
    // freq stores frequency of each
    // english lowercase character
    ll freq[26];

    // dp[i][j] stores the count of
    // subsequence with 'a' + i
    // and 'a' + j character
    ll dp[26][26];

    memset(freq, 0, sizeof freq);

    // Initialize dp to 0
    memset(dp, 0, sizeof dp);

    for (int i = 0; i < s.size(); ++i) {

        for (int j = 0; j < 26; j++) {

            // Increment the count of
            // subsequence j and s[i]
            dp[j][s[i] - 'a'] += freq[j];
        }

        // Update the frequency array
        freq[s[i] - 'a']++;
    }

    ll ans = 0;

    // For 1 length subsequence
    for (int i = 0; i < 26; i++)
        ans = max(freq[i], ans);

    // For 2 length subsequence
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < 26; j++) {

            ans = max(dp[i][j], ans);
        }
    }

    // Return the final result
    return ans;
}

// Driver Code
int main()
{
    // Given string str
    string str = "acbab";

    // Function Call
    cout << findCount(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the frequency
static int findCount(String s)
{

    // freq stores frequency of each
    // english lowercase character
    int []freq = new int[26];

    // dp[i][j] stores the count of
    // subsequence with 'a' + i
    // and 'a' + j character
    int [][]dp = new int[26][26];

    for(int i = 0; i < s.length(); ++i)
    {
        for(int j = 0; j < 26; j++)
        {

            // Increment the count of
            // subsequence j and s[i]
            dp[j][s.charAt(i) - 'a'] += freq[j];
        }

        // Update the frequency array
        freq[s.charAt(i) - 'a']++;
    }

    int ans = 0;

    // For 1 length subsequence
    for(int i = 0; i < 26; i++)
        ans = Math.max(freq[i], ans);

    // For 2 length subsequence
    for(int i = 0; i < 26; i++)
    {
        for(int j = 0; j < 26; j++)
        {
            ans = Math.max(dp[i][j], ans);
        }
    }

    // Return the final result
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String str = "acbab";

    // Function call
    System.out.print(findCount(str));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import numpy

# Function to find the frequency
def findCount(s):

    # freq stores frequency of each
    # english lowercase character
    freq = [0] * 26

    # dp[i][j] stores the count of
    # subsequence with 'a' + i
    # and 'a' + j character
    dp = [[0] * 26] * 26

    freq = numpy.zeros(26)
    dp = numpy.zeros([26, 26])

    for i in range(0, len(s)):
        for j in range(26):

            # Increment the count of
            # subsequence j and s[i]
            dp[j][ord(s[i]) - ord('a')] += freq[j]

        # Update the frequency array
        freq[ord(s[i]) - ord('a')] += 1

    ans = 0

    # For 1 length subsequence
    for i in range(26):
        ans = max(freq[i], ans)

    # For 2 length subsequence
    for i in range(0, 26):
        for j in range(0, 26):
            ans = max(dp[i][j], ans)

    # Return the final result
    return int(ans)

# Driver Code

# Given string str
str = "acbab"

# Function call
print(findCount(str))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the frequency
static int findCount(String s)
{

    // freq stores frequency of each
    // english lowercase character
    int []freq = new int[26];

    // dp[i,j] stores the count of
    // subsequence with 'a' + i
    // and 'a' + j character
    int [,]dp = new int[26, 26];

    for(int i = 0; i < s.Length; ++i)
    {
        for(int j = 0; j < 26; j++)
        {

            // Increment the count of
            // subsequence j and s[i]
            dp[j, s[i] - 'a'] += freq[j];
        }

        // Update the frequency array
        freq[s[i] - 'a']++;
    }

    int ans = 0;

    // For 1 length subsequence
    for(int i = 0; i < 26; i++)
        ans = Math.Max(freq[i], ans);

    // For 2 length subsequence
    for(int i = 0; i < 26; i++)
    {
        for(int j = 0; j < 26; j++)
        {
            ans = Math.Max(dp[i, j], ans);
        }
    }

    // Return the readonly result
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "acbab";

    // Function call
    Console.Write(findCount(str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the frequency
function findCount(s)
{
    // freq stores frequency of each
    // english lowercase character
    var freq = Array(26).fill(0);

    // dp[i][j] stores the count of
    // subsequence with 'a' + i
    // and 'a' + j character
    var dp = Array.from(Array(26), ()=>Array(26).fill(0));

    for (var i = 0; i < s.length; ++i) {

        for (var j = 0; j < 26; j++) {

            // Increment the count of
            // subsequence j and s[i]
            dp[j][s[i].charCodeAt(0) -
            'a'.charCodeAt(0)] += freq[j];
        }

        // Update the frequency array
        freq[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    var ans = 0;

    // For 1 length subsequence
    for (var i = 0; i < 26; i++)
        ans = Math.max(freq[i], ans);

    // For 2 length subsequence
    for (var i = 0; i < 26; i++) {
        for (var j = 0; j < 26; j++) {

            ans = Math.max(dp[i][j], ans);
        }
    }

    // Return the final result
    return ans;
}

// Driver Code

// Given string str
var str = "acbab";

// Function Call
document.write( findCount(str));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(26*N)* ，其中 N 为给定字符串的长度。