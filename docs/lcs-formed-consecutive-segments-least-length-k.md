# 由至少长度为 K 的连续片段形成的 LCS

> 原文:[https://www . geesforgeks . org/LCS-formed-continuous-segments-最小长度-k/](https://www.geeksforgeeks.org/lcs-formed-consecutive-segments-least-length-k/)

给定两个字符串 s1、s2 和 K，找出由至少长度为 K 的连续片段形成的最长子序列的长度。
示例:

```
Input : s1 = aggayxysdfa
        s2 = aggajxaaasdfa 
         k = 4
Output : 8 
Explanation: aggasdfa is the longest
subsequence that can be formed by taking
consecutive segments, minimum of length 4.
Here segments are "agga" and "sdfa" which 
are of length 4 which is included in making 
the longest subsequence. 

Input : s1 = aggasdfa 
        s2 = aggajasdfaxy
         k = 5
Output : 5 

Input: s1 = "aabcaaaa" 
       s2 = "baaabcd"  
        k = 3
Output: 4 
Explanation: "aabc" is the longest subsequence that 
is formed by taking segment of minimum length 3\. 
The segment is of length 4\. 
```

**先决条件** : [最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence/)
创建 LCS[][]数组，其中 LCS <sub>i，j</sub> 表示由长度至少为 k 的连续段的 s1 到 I 和 s2 到 j 的字符形成的最长公共子序列的长度。 **cnt <sub>i，j</sub> = cnt <sub>i-1，j-1</sub> +1** 当 s1[i-1]==s2[j-1]时。如果字符不相等，则段不相等，因此将 cnt <sub>i，j</sub> 标记为 0。
当 **cnt <sub>i，j</sub> > =k** 时，则通过将 lcs <sub>i-a，j-a</sub> 的值相加来更新 lcs 值，其中 a 为线段的长度 **a < =cnt <sub>i，j</sub>** 。长度至少为 k 的连续片段的最长子序列的答案将存储在 **lcs[n][m]** 中，其中 n 和 m 是 string1 和 string2 的长度。

## C++

```
// CPP program to find the Length of Longest
// subsequence formed by consecutive segments
// of at least length K
#include <bits/stdc++.h>
using namespace std;

// Returns the length of the longest common subsequence
// with a minimum of length of K consecutive segments
int longestSubsequenceCommonSegment(int k, string s1,
                                           string s2)
{
    // length of strings
    int n = s1.length();
    int m = s2.length();

    // declare the lcs and cnt array
    int lcs[n + 1][m + 1];
    int cnt[n + 1][m + 1];

    // initialize the lcs and cnt array to 0
    memset(lcs, 0, sizeof(lcs));
    memset(cnt, 0, sizeof(cnt));

    // iterate from i=1 to n and j=1 to j=m
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {

            // stores the maximum of lcs[i-1][j] and lcs[i][j-1]
            lcs[i][j] = max(lcs[i - 1][j], lcs[i][j - 1]);

            // when both the characters are equal
            // of s1 and s2
            if (s1[i - 1] == s2[j - 1])
                cnt[i][j] = cnt[i - 1][j - 1] + 1;

            // when length of common segment is
            // more than k, then update lcs answer
            // by adding that segment to the answer
            if (cnt[i][j] >= k) {

                // formulate for all length of segments
                // to get the longest subsequence with
                // consecutive Common Segment of length
                // of min k length
                for (int a = k; a <= cnt[i][j]; a++)

                    // update lcs value by adding segment length
                    lcs[i][j] = max(lcs[i][j],
                                    lcs[i - a][j - a] + a);

            }
        }
    }

    return lcs[n][m];
}

// driver code to check the above function
int main()
{
    int k = 4;
    string s1 = "aggasdfa";
    string s2 = "aggajasdfa";
    cout << longestSubsequenceCommonSegment(k, s1, s2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Length of Longest
// subsequence formed by consecutive segments
// of at least length K

class GFG {

    // Returns the length of the longest common subsequence
    // with a minimum of length of K consecutive segments
    static int longestSubsequenceCommonSegment(int k, String s1,
                                               String s2)
    {
        // length of strings
        int n = s1.length();
        int m = s2.length();

        // declare the lcs and cnt array
        int lcs[][] = new int[n + 1][m + 1];
        int cnt[][] = new int[n + 1][m + 1];

        // iterate from i=1 to n and j=1 to j=m
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {

                // stores the maximum of lcs[i-1][j] and lcs[i][j-1]
                lcs[i][j] = Math.max(lcs[i - 1][j], lcs[i][j - 1]);

                // when both the characters are equal
                // of s1 and s2
                if (s1.charAt(i - 1) == s2.charAt(j - 1))
                    cnt[i][j] = cnt[i - 1][j - 1] + 1;

                // when length of common segment is
                // more than k, then update lcs answer
                // by adding that segment to the answer
                if (cnt[i][j] >= k)
                {

                    // formulate for all length of segments
                    // to get the longest subsequence with
                    // consecutive Common Segment of length
                    // of min k length
                    for (int a = k; a <= cnt[i][j]; a++)

                        // update lcs value by adding
                        // segment length
                        lcs[i][j] = Math.max(lcs[i][j],
                                        lcs[i - a][j - a] + a);

                }
            }
        }

        return lcs[n][m];
    }

    // driver code to check the above function
    public static void main(String[] args)
    {
        int k = 4;
        String s1 = "aggasdfa";
        String s2 = "aggajasdfa";
        System.out.println(longestSubsequenceCommonSegment(k, s1, s2));
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python3 program to find the Length of Longest
# subsequence formed by consecutive segments
# of at least length K

# Returns the length of the longest common subsequence
# with a minimum of length of K consecutive segments
def longestSubsequenceCommonSegment(k, s1, s2) :

    # length of strings
    n = len(s1)
    m = len(s2)

    # declare the lcs and cnt array
    lcs = [[0 for x in range(m + 1)] for y in range(n + 1)]
    cnt = [[0 for x in range(m + 1)] for y in range(n + 1)]

    # iterate from i=1 to n and j=1 to j=m
    for i in range(1, n + 1) :
        for j in range(1, m + 1) :
            # stores the maximum of lcs[i-1][j] and lcs[i][j-1]
            lcs[i][j] = max(lcs[i - 1][j], lcs[i][j - 1])

            # when both the characters are equal
            # of s1 and s2
            if (s1[i - 1] == s2[j - 1]):
                cnt[i][j] = cnt[i - 1][j - 1] + 1;

            # when length of common segment is
            # more than k, then update lcs answer
            # by adding that segment to the answer
            if (cnt[i][j] >= k) :

                # formulate for all length of segments
                # to get the longest subsequence with
                # consecutive Common Segment of length
                # of min k length
                for a in range(k, cnt[i][j] + 1) :

                    # update lcs value by adding
                    # segment length
                    lcs[i][j] = max(lcs[i][j],lcs[i - a][j - a] + a)

    return lcs[n][m]

# Driver code 
k = 4
s1 = "aggasdfa"
s2 = "aggajasdfa"
print(longestSubsequenceCommonSegment(k, s1, s2))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find the Length of Longest
// subsequence formed by consecutive segments
// of at least length K
using System;

class GFG {

    // Returns the length of the longest common subsequence
    // with a minimum of length of K consecutive segments
    static int longestSubsequenceCommonSegment(int k, string s1,
                                            string s2)
    {
        // length of strings
        int n = s1.Length;
        int m = s2.Length;

        // declare the lcs and cnt array
        int [,]lcs = new int[n + 1,m + 1];
        int [,]cnt = new int[n + 1,m + 1];

        // iterate from i=1 to n and j=1 to j=m
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {

                // stores the maximum of lcs[i-1][j] and lcs[i][j-1]
                lcs[i,j] = Math.Max(lcs[i - 1,j], lcs[i,j - 1]);

                // when both the characters are equal
                // of s1 and s2
                if (s1[i - 1] == s2[j - 1])
                    cnt[i,j] = cnt[i - 1,j - 1] + 1;

                // when length of common segment is
                // more than k, then update lcs answer
                // by adding that segment to the answer
                if (cnt[i,j] >= k)
                {

                    // formulate for all length of segments
                    // to get the longest subsequence with
                    // consecutive Common Segment of length
                    // of min k length
                    for (int a = k; a <= cnt[i,j]; a++)

                        // update lcs value by adding
                        // segment length
                        lcs[i,j] = Math.Max(lcs[i,j],
                                        lcs[i - a,j - a] + a);

                }
            }
        }

        return lcs[n,m];
    }

    // driver code to check the above function
    public static void Main()
    {
        int k = 4;
        string s1 = "aggasdfa";
        string s2 = "aggajasdfa";
    Console.WriteLine(longestSubsequenceCommonSegment(k, s1, s2));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to find the Length of Longest
// subsequence formed by consecutive segments
// of at least length K

// Returns the length of the longest common subsequence
// with a minimum of length of K consecutive segments
function longestSubsequenceCommonSegment(k, s1, s2)
{
    // length of strings
    var n = s1.length;
    var m = s2.length;

    // declare the lcs and cnt array
    var lcs = Array.from(Array(n+1), ()=>Array(m+1).fill(0));
    var cnt = Array.from(Array(n+1), ()=>Array(m+1).fill(0));

    // iterate from i=1 to n and j=1 to j=m
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= m; j++) {

            // stores the maximum of lcs[i-1][j] and lcs[i][j-1]
            lcs[i][j] = Math.max(lcs[i - 1][j], lcs[i][j - 1]);

            // when both the characters are equal
            // of s1 and s2
            if (s1[i - 1] == s2[j - 1])
                cnt[i][j] = cnt[i - 1][j - 1] + 1;

            // when length of common segment is
            // more than k, then update lcs answer
            // by adding that segment to the answer
            if (cnt[i][j] >= k) {

                // formulate for all length of segments
                // to get the longest subsequence with
                // consecutive Common Segment of length
                // of min k length
                for (var a = k; a <= cnt[i][j]; a++)

                    // update lcs value by adding segment length
                    lcs[i][j] = Math.max(lcs[i][j],
                                    lcs[i - a][j - a] + a);

            }
        }
    }

    return lcs[n][m];
}

// driver code to check the above function
var k = 4;
var s1 = "aggasdfa";
var s2 = "aggajasdfa";
document.write( longestSubsequenceCommonSegment(k, s1, s2));

</script>
```

**输出:**

```
8
```