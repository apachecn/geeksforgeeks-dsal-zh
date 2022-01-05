# 对给定范围的索引中给定字符的频率进行计数的查询

> 原文:[https://www . geeksforgeeks . org/给定范围索引中给定字符的查询计数频率/](https://www.geeksforgeeks.org/queries-to-count-frequencies-of-a-given-character-in-a-given-range-of-indices/)

给定长度为 **N** 的字符串 **S** 和形式为 **{l，r，y}** 的查询数组 **Q[][]** 。对于每个查询，任务是打印范围**【l，r】**中存在的字符数 **y** 。

**示例:**

> **输入:** S = "aabv "，Q[][] = {{0，3，' a'}，{1，2，' b ' }
> **输出:**2 1
> T6】解释:
> 查询 1:出现在[0，3]范围内的字符‘a’个数为 2。
> 查询 2:范围[1，2]中出现的字符“b”的数量为 1。
> 
> **输入:** S = "abcd "，Q[][] = {{1，3，' c'}，{1，1，' b ' }
> T3】输出:1 1
> T6】解释:
> 查询 1:范围[1，3]内存在的字符' c '个数为 1。
> 查询 2:范围[1，1]中出现的字符“b”的数量为 1。

**简单方法:**最简单的方法是[在范围**【l，r】**内遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，如果索引 **i** 处的字符对于每个查询 **{l，r，y}** 等于 **y** ，则将计数器增加 **1** 。遍历后，打印每个查询的计数器。

***时间复杂度:** O(N*Q)*
***辅助空间:** O(N)*

**有效方法:**想法是使用[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术，为从 **'a'** 到 **'z'** 的每个字符预先计算存在于范围 **1 到 i** 中的字符数，其中 **1 ≤ i ≤ N** 。按照以下步骤解决问题:

1.  初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **dp[N+1][26]** ，其中 **dp[i][j]** 存储范围**【0，I】**中存在的字符数 **(i+'a')** 。
2.  现在，通过将 **dp[i][j]** 增加**DP[I–1][j]**其中 **0 ≤ j < 26** 并将**DP[I][S[j]–‘a’】**增加 **1** 来预先计算 **[1，i]** 中 **1 ≤ i ≤ N** 的每个字符的数量。
3.  对于每个查询 **{l，r，y}** ，打印**DP[r][y –' a '】–DP[l–1][y –' a '】**的值，作为范围 **[l，r]** 中存在的字符数 **y** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print count of char
// y present in the range [l, r]
void noOfChars(string s, char queries[][3], int q)
{

    // Length of the string
    int n = s.length();

    // Stores the precomputed results
    int dp[n + 1][26];
    memset(dp, 0, sizeof(dp));

    // Iterate the given string
    for(int i = 0; i < n; i++)
    {

         // Increment dp[i][y-'a'] by 1
        dp[i + 1][s[i]-'a']++;

        // Pre-compute
        for(int j = 0; j < 26; j++)
        {
            dp[i + 1][j] += dp[i][j];
        }

    }

    // Traverse each query
    for(int i = 0; i < q; i++)
    {
        int l = (int)queries[i][0];
        int r = (int)queries[i][1];
        int c = queries[i][2] - 'a';

        // Print the result for
        // each query
        cout << dp[r] - dp[l - 1] << " ";
    }
}

// Driver Code
int main()
{

    // Given string
    string S = "aabv";

    // Given Queries
    char queries[2][3] = {{ 1, 2, 'a' },{ 2, 3, 'b' }};

    // Function Call
    noOfChars(S, queries, 2);
    return 0;
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to print count of char
    // y present in the range [l, r]
    static void noOfChars(String s,
                          char[][] queries)
    {

        // Length of the string
        int n = s.length();

        // Stores the precomputed results
        int dp[][] = new int[n + 1][26];

        // Iterate the given string
        for (int i = 0; i < n; i++) {

            // Increment dp[i][y-'a'] by 1
            dp[i + 1][s.charAt(i) - 'a']++;

            // Pre-compute
            for (int j = 0; j < 26; j++) {
                dp[i + 1][j] += dp[i][j];
            }
        }

        // Number of queries
        int q = queries.length;

        // Traverse each query
        for (int i = 0; i < q; i++) {

            int l = (int)queries[i][0];
            int r = (int)queries[i][1];
            int c = queries[i][2] - 'a';

            // Print the result for
            // each query
            System.out.print(
                dp[r] - dp[l - 1]
                + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string
        String S = "aabv";

        // Given Queries
        char queries[][]
            = new char[][] { { 1, 2, 'a' },
                             { 2, 3, 'b' } };

        // Function Call
        noOfChars(S, queries);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to prcount of char
# y present in the range [l, r]
def noOfChars(s, queries):

    # Length of the string
    n = len(s)

    # Stores the precomputed results
    dp = [[0 for i in range(26)]
             for i in range(n + 1)]

    # Iterate the given string
    for i in range(n):

        # Increment dp[i][y-'a'] by 1
        dp[i + 1][ord(s[i]) - ord('a')] += 1

        # Pre-compute
        for j in range(26):
            dp[i + 1][j] += dp[i][j]

    # Number of queries
    q = len(queries)

    # Traverse each query
    for i in range(q):
        l = queries[i][0]
        r = queries[i][1]
        c = ord(queries[i][2]) - ord('a')

        # Print the result for
        # each query
        print(dp[r] - dp[l - 1], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given string
    S = "aabv"

    # Given Queries
    queries = [ [ 1, 2, 'a' ],
                [ 2, 3, 'b' ] ]

    # Function Call
    noOfChars(S, queries)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to print count of char
    // y present in the range [l, r]
    static void noOfChars(String s,
                          char[,] queries)
    {

        // Length of the string
        int n = s.Length;

        // Stores the precomputed results
        int [,]dp = new int[n + 1, 26];

        // Iterate the given string
        for (int i = 0; i < n; i++) {

            // Increment dp[i,y-'a'] by 1
            dp[i + 1, s[i] - 'a']++;

            // Pre-compute
            for (int j = 0; j < 26; j++) {
                dp[i + 1, j] += dp[i, j];
            }
        }

        // Number of queries
        int q = queries.GetLength(0);

        // Traverse each query
        for (int i = 0; i < q; i++) {

            int l = (int)queries[i, 0];
            int r = (int)queries[i, 1];
            int c = queries[i, 2] - 'a';

            // Print the result for
            // each query
            Console.Write(
                dp[r, c] - dp[l - 1, c]
                + " ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given string
        String S = "aabv";

        // Given Queries
        char [,]queries
            = new char[,] { { (char)1, (char)2, 'a' },
                             { (char)2, (char)3, 'b' } };

        // Function Call
        noOfChars(S, queries);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach  

// Function to print count of char
// y present in the range [l, r]
function noOfChars(s,queries)
{

    // Length of the string
    var n = s.length;

    // Stores the precomputed results
    var dp =
    Array(n+1).fill(0).map(x => Array(26).fill(0));

    // Iterate the given string
    for (var i = 0; i < n; i++) {

        // Increment dp[i][y-'a'] by 1
        dp[i + 1][s.charAt(i).charCodeAt(0) -
        'a'.charCodeAt(0)]++;

        // Pre-compute
        for (var j = 0; j < 26; j++) {
            dp[i + 1][j] += dp[i][j];
        }
    }

    // Number of queries
    var q = queries.length;

    // Traverse each query
    for (var i = 0; i < q; i++) {

        var l =
        String.fromCharCode(queries[i][0]).charCodeAt(0);

        var r =
        String.fromCharCode(queries[i][1]).charCodeAt(0);

        var c =
        queries[i][2].charCodeAt(0) - 'a'.charCodeAt(0);

        // Print the result for
        // each query
        document.write(
            dp[r] - dp[l - 1]
            + " ");
    }
}

// Driver Code
 // Given string
var S = "aabv";

// Given Queries
var queries
    = [ [ 1, 2, 'a' ],
                     [ 2, 3, 'b' ] ];

// Function Call
noOfChars(S, queries);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
2 1
```

***时间复杂度:**O(Q+N * 26)*
T5**辅助空间:** O(N)