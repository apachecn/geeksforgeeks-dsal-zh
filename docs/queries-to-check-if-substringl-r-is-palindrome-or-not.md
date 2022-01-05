# 查询子串【L…R】是否回文

> 原文:[https://www . geesforgeks . org/query-to-check-if-substring-r-is-回文-or-not/](https://www.geeksforgeeks.org/queries-to-check-if-substringl-r-is-palindrome-or-not/)

给定一个字符串**字符串**和 **Q** 查询。每个查询由两个数字组成 **L** 和 **R** 。任务是打印**子串【L…R】**是否回文。

**示例:**

> **输入:** str = "abacccde "，Q[][] = {{0，2}，{1，2}，{2，4}，{3，5}}
> **输出:**
> 是
> 否
> 否
> 是
> 
> **输入:** str = "abaaab "，Q[][] = {{0，1}，{1，5}}
> **输出:**
> 否
> 是

**简单方法**:一个比较天真的方法就是检查每个子串是不是回文。在最坏的情况下，每个查询最多可以占用 **O(Q)** 。

**高效的方法**:一种高效的方法是使用动态规划来解决上述问题。我们可以首先创建 **DP** 表，该表存储**子串【I。j]** 是不是回文。我们维护一个布尔**DP【n】【n】**以自下而上的方式填充。如果子串是回文， **dp[i][j]** 的值为真，否则为假。为了计算 dp[i][j]，我们首先检查 **dp[i+1][j-1]** 的值，如果该值为真且 **s[i]** 与 **s[j]** 相同，则我们使 **dp[i][j]** 为真。否则， **dp[i][j]** 的值为假。
现在，对于每个查询，检查 **dp[l][r]** 是否为真。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100

// Pre-processing function
void pre_process(bool dp[N][N], string s)
{

    // Get the size of the string
    int n = s.size();

    // Initially mark every
    // position as false
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            dp[i][j] = false;
    }

    // For the length
    for (int j = 1; j <= n; j++) {

        // Iterate for every index with
        // length j
        for (int i = 0; i <= n - j; i++) {

            // If the length is less than 2
            if (j <= 2) {

                // If characters are equal
                if (s[i] == s[i + j - 1])
                    dp[i][i + j - 1] = true;
            }

            // Check for equal
            else if (s[i] == s[i + j - 1])
                dp[i][i + j - 1] = dp[i + 1][i + j - 2];
        }
    }
}

// Function to answer every query in O(1)
void answerQuery(int l, int r, bool dp[N][N])
{
    if (dp[l][r])
        cout << "Yes\n";
    else
        cout << "No\n";
}

// Driver code
int main()
{
    string s = "abaaab";
    bool dp[N][N];
    pre_process(dp, s);

    int queries[][2] = { { 0, 1 }, { 1, 5 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    for (int i = 0; i < q; i++)
        answerQuery(queries[i][0], queries[i][1], dp);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int N = 100;

    // Pre-processing function
    static void pre_process(boolean dp[][], char[] s)
    {

        // Get the size of the string
        int n = s.length;

        // Initially mark every
        // position as false
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                dp[i][j] = false;
            }
        }

        // For the length
        for (int j = 1; j <= n; j++) {

            // Iterate for every index with
            // length j
            for (int i = 0; i <= n - j; i++) {

                // If the length is less than 2
                if (j <= 2) {

                    // If characters are equal
                    if (s[i] == s[i + j - 1]) {
                        dp[i][i + j - 1] = true;
                    }
                }

                // Check for equal
                else if (s[i] == s[i + j - 1]) {
                    dp[i][i + j - 1] = dp[i + 1][i + j - 2];
                }
            }
        }
    }

    // Function to answer every query in O(1)
    static void answerQuery(int l, int r, boolean dp[][])
    {
        if (dp[l][r]) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abaaab";
        boolean[][] dp = new boolean[N][N];
        pre_process(dp, s.toCharArray());

        int queries[][] = { { 0, 1 }, { 1, 5 } };
        int q = queries.length;

        for (int i = 0; i < q; i++) {
            answerQuery(queries[i][0], queries[i][1], dp);
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100

# Pre-processing function
def pre_process(dp, s):

    # Get the size of the string
    n = len(s)

    # Initially mark every
    # position as false
    for i in range(n):
        for j in range(n):
            dp[i][j] = False

    # For the length
    for j in range(1, n + 1):

        # Iterate for every index with
        # length j
        for i in range(n - j + 1):

            # If the length is less than 2
            if (j <= 2):

                # If characters are equal
                if (s[i] == s[i + j - 1]):
                    dp[i][i + j - 1] = True

            # Check for equal
            elif (s[i] == s[i + j - 1]):
                dp[i][i + j - 1] = dp[i + 1][i + j - 2]

# Function to answer every query in O(1)
def answerQuery(l, r, dp):

    if (dp[l][r]):
        print("Yes")
    else:
        print("No")

# Driver code
s = "abaaab"
dp = [[0 for i in range(N)]
         for i in range(N)]
pre_process(dp, s)

queries = [[0, 1], [1, 5]]
q = len(queries)

for i in range(q):
    answerQuery(queries[i][0],
                queries[i][1], dp)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    static int N = 100;

    // Pre-processing function
    static void pre_process(bool[, ] dp, char[] s)
    {

        // Get the size of the string
        int n = s.Length;

        // Initially mark every
        // position as false
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                dp[i, j] = false;
            }
        }

        // For the length
        for (int j = 1; j <= n; j++) {

            // Iterate for every index with
            // length j
            for (int i = 0; i <= n - j; i++) {

                // If the length is less than 2
                if (j <= 2) {

                    // If characters are equal
                    if (s[i] == s[i + j - 1]) {
                        dp[i, i + j - 1] = true;
                    }
                }

                // Check for equal
                else if (s[i] == s[i + j - 1]) {
                    dp[i, i + j - 1] = dp[i + 1, i + j - 2];
                }
            }
        }
    }

    // Function to answer every query in O(1)
    static void answerQuery(int l, int r, bool[, ] dp)
    {
        if (dp[l, r]) {
            Console.WriteLine("Yes");
        }
        else {
            Console.WriteLine("No");
        }
    }

    // Driver code
    public static void Main()
    {
        string s = "abaaab";
        bool[, ] dp = new bool[N, N];
        pre_process(dp, s.ToCharArray());

        int[, ] queries = { { 0, 1 }, { 1, 5 } };
        int q = queries.Length;

        for (int i = 0; i < q; i++) {
            answerQuery(queries[i, 0], queries[i, 1], dp);
        }
    }
}

// This code is contributed by Ankit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$N = 100;

// Pre-processing function
function pre_process($dp, $s)
{

    // Get the size of the string
    $n = strlen($s);

    // Initially mark every
    // position as false
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
            $dp[$i][$j] = false;
    }

    // For the length
    for ($j = 1; $j <= $n; $j++)
    {

        // Iterate for every index with
        // length j
        for ($i = 0; $i <= $n - $j; $i++)
        {

            // If the length is less than 2
            if ($j <= 2)
            {

                // If characters are equal
                if ($s[$i] == $s[$i + $j - 1])
                    $dp[$i][$i + $j - 1] = true;
            }

            // Check for equal
            else if ($s[$i] == $s[$i + $j - 1])
                $dp[$i][$i + $j - 1] = $dp[$i + 1][$i + $j - 2];
        }
    }
    return $dp;
}

// Function to answer every query in O(1)
function answerQuery($l, $r, $dp)
{
    if ($dp[$l][$r])
        echo "Yes\n";
    else
        echo "No\n";
}

// Driver code
$s = "abaaab";
$dp = array(array());
$dp = pre_process($dp, $s);

$queries = array(array(0, 1),
                 array(1, 5));
$q = count($queries);

for ($i = 0; $i < $q; $i++)
    answerQuery($queries[$i][0],
                $queries[$i][1], $dp);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // javascript implementation of the approach   
    var N = 100;

    // Pre-processing function
    function pre_process( dp,  s) {

        // Get the size of the string
        var n = s.length;

        // Initially mark every
        // position as false
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                dp[i][j] = false;
            }
        }

        // For the length
        for (j = 1; j <= n; j++) {

            // Iterate for every index with
            // length j
            for (i = 0; i <= n - j; i++) {

                // If the length is less than 2
                if (j <= 2) {

                    // If characters are equal
                    if (s[i] == s[i + j - 1]) {
                        dp[i][i + j - 1] = true;
                    }
                }

                // Check for equal
                else if (s[i] == s[i + j - 1]) {
                    dp[i][i + j - 1] = dp[i + 1][i + j - 2];
                }
            }
        }
    }

    // Function to answer every query in O(1)
    function answerQuery(l , r,  dp) {
        if (dp[l][r]) {
            document.write("Yes<br/>");
        }
        else {
            document.write("No<br/>");
        }
    }

    // Driver code

    var s = "abaaab";
    var dp = Array(N).fill().map(()=>Array(N).fill());
    pre_process(dp, s);

    var queries = [ [ 0, 1 ], [ 1, 5 ] ];
    var q = queries.length;

    for (i = 0; i < q; i++) {
        answerQuery(queries[i][0], queries[i][1], dp);
    }

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
No
Yes
```