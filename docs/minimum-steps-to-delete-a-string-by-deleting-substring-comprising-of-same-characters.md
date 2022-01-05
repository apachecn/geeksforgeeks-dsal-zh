# 通过删除包含相同字符的子串来删除字符串的最少步骤

> 原文:[https://www . geesforgeks . org/通过删除由相同字符组成的子串来删除字符串的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-to-delete-a-string-by-deleting-substring-comprising-of-same-characters/)

给定一根弦**弦**。如果在一次操作中所有字符都相同，则只允许删除一些连续的字符。任务是找到完全删除字符串所需的最小操作数。
**例:**

> **输入:**str = " abcdcba "
> T3】输出: 4
> 删除 dd，则字符串为“abcdcba”
> 删除 cc，则字符串为“ABBA”
> 删除 bb，则字符串为“aa”
> 删除 aa，则字符串为空。
> **输入:** str = "abc"
> **输出:** 3

**方法:**使用<a href = " http://wwl<= iDynamic Programming 和[分治](https://www.geeksforgeeks.org/divide-and-conquer/)技术可以解决问题。
让 **dp[l][r]** 成为子串 s[l，l+1，l+2，…r]的答案。那么我们有两种情况:

*   子串首字母与其余分开删除，然后 **dp[l][r] = 1 + dp[l+1][r]** 。
*   如果 **l ≤ i ≤ r** 和 **s[i] = s[l]** ，子字符串的第一个字母将与其他字母一起删除(两个字母必须相等)，然后**DP[l][r]= DP[l+1][I-1]+DP[I][r]**。

以下两种情况可以和[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)一起递归调用，避免重复的函数调用。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int N = 10;

// Function to return the minimum number of
// delete operations
int findMinimumDeletion(int l, int r, int dp[N][N], string s)
{

    if (l > r)
        return 0;
    if (l == r)
        return 1;
    if (dp[l][r] != -1)
        return dp[l][r];

    // When a single character is deleted
    int res = 1 + findMinimumDeletion(l + 1, r, dp, s);

    // When a group of consecutive characters
    // are deleted if any of them matches
    for (int i = l + 1; i <= r; ++i) {

        // When both the characters are same then
        // delete the letters in between them
        if (s[l] == s[i])
            res = min(res, findMinimumDeletion(l + 1, i - 1, dp, s)
                               + findMinimumDeletion(i, r, dp, s));
    }

    // Memoize
    return dp[l][r] = res;
}

// Driver code
int main()
{
    string s = "abcddcba";
    int n = s.length();
    int dp[N][N];
    memset(dp, -1, sizeof dp);
    cout << findMinimumDeletion(0, n - 1, dp, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int N = 10;

    // Function to return the minimum number of
    // delete operations
    static int findMinimumDeletion(int l, int r,
                            int dp[][], String s)
    {

        if (l > r)
        {
            return 0;
        }
        if (l == r)
        {
            return 1;
        }
        if (dp[l][r] != -1)
        {
            return dp[l][r];
        }

        // When a single character is deleted
        int res = 1 + findMinimumDeletion(l + 1, r, dp, s);

        // When a group of consecutive characters
        // are deleted if any of them matches
        for (int i = l + 1; i <= r; ++i)
        {

            // When both the characters are same then
            // delete the letters in between them
            if (s.charAt(l) == s.charAt(i))
            {
                res = Math.min(res, findMinimumDeletion(l + 1, i - 1, dp, s)
                        + findMinimumDeletion(i, r, dp, s));
            }
        }

        // Memoize
        return dp[l][r] = res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abcddcba";
        int n = s.length();
        int dp[][] = new int[N][N];
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                dp[i][j] = -1;
            }
        }
        System.out.println(findMinimumDeletion(0, n - 1, dp, s));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# number of delete operations
def findMinimumDeletion(l, r, dp, s):

    if l > r:
        return 0
    if l == r:
        return 1
    if dp[l][r] != -1:
        return dp[l][r]

    # When a single character is deleted
    res = 1 + findMinimumDeletion(l + 1, r,
                                     dp, s)

    # When a group of consecutive characters
    # are deleted if any of them matches
    for i in range(l + 1, r + 1):

        # When both the characters are same then
        # delete the letters in between them
        if s[l] == s[i]:
            res = min(res, findMinimumDeletion(l + 1, i - 1, dp, s) +
                           findMinimumDeletion(i, r, dp, s))

    # Memoize
    dp[l][r] = res
    return res

# Driver code
if __name__ == "__main__":

    s = "abcddcba"
    n = len(s)
    N = 10
    dp = [[-1 for i in range(N)]
              for j in range(N)]
    print(findMinimumDeletion(0, n - 1, dp, s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int N = 10;

    // Function to return the minimum number of
    // delete operations
    static int findMinimumDeletion(int l, int r,
                            int [,]dp, String s)
    {

        if (l > r)
        {
            return 0;
        }
        if (l == r)
        {
            return 1;
        }
        if (dp[l, r] != -1)
        {
            return dp[l, r];
        }

        // When a single character is deleted
        int res = 1 + findMinimumDeletion(l + 1, r, dp, s);

        // When a group of consecutive characters
        // are deleted if any of them matches
        for (int i = l + 1; i <= r; ++i)
        {

            // When both the characters are same then
            // delete the letters in between them
            if (s[l] == s[i])
            {
                res = Math.Min(res, findMinimumDeletion(l + 1, i - 1, dp, s)
                        + findMinimumDeletion(i, r, dp, s));
            }
        }

        // Memoize
        return dp[l,r] = res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "abcddcba";
        int n = s.Length;
        int [,]dp = new int[N, N];
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                dp[i, j] = -1;
            }
        }
        Console.WriteLine(findMinimumDeletion(0, n - 1, dp, s));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$GLOBALS['N'] = 10;

// Function to return the minimum
// number of delete operations
function findMinimumDeletion($l, $r, $dp, $s)
{
    if ($l > $r)
        return 0;
    if ($l == $r)
        return 1;
    if ($dp[$l][$r] != -1)
        return $dp[$l][$r];

    // When a single character is deleted
    $res = 1 + findMinimumDeletion($l + 1, $r,
                                      $dp, $s);

    // When a group of consecutive characters
    // are deleted if any of them matches
    for ($i = $l + 1; $i <= $r; ++$i)
    {

        // When both the characters are same then
        // delete the letters in between them
        if ($s[$l] == $s[$i])
            $res = min($res, findMinimumDeletion($l + 1, $i - 1, $dp, $s) +
                             findMinimumDeletion($i, $r, $dp, $s));
    }

    // Memoize
    return $dp[$l][$r] = $res;
}

// Driver code
$s = "abcddcba";
$n = strlen($s);
$dp = array(array());
for($i = 0; $i < $GLOBALS['N']; $i++)
    for($j = 0; $j < $GLOBALS['N']; $j++)
        $dp[$i][$j] = -1 ;

echo findMinimumDeletion(0, $n - 1, $dp, $s);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var N = 10;

// Function to return the minimum number of
// delete operations
function findMinimumDeletion(l, r, dp, s)
{

    if (l > r)
        return 0;
    if (l == r)
        return 1;
    if (dp[l][r] != -1)
        return dp[l][r];

    // When a single character is deleted
    var res = 1 + findMinimumDeletion(l + 1, r, dp, s);

    // When a group of consecutive characters
    // are deleted if any of them matches
    for (var i = l + 1; i <= r; ++i) {

        // When both the characters are same then
        // delete the letters in between them
        if (s[l] == s[i])
            res =
            Math.min(res, findMinimumDeletion(l + 1, i - 1, dp, s)
                               + findMinimumDeletion(i, r, dp, s));
    }

    // Memoize
    return dp[l][r] = res;
}

// Driver code
var s = "abcddcba";
var n = s.length;
var dp = Array.from(Array(N), ()=> Array(N).fill(-1));
document.write( findMinimumDeletion(0, n - 1, dp, s));

</script>
```

**Output:** 

```
4
```