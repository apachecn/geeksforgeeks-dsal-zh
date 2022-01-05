# 计数 k 次出现在相邻两个设置位的二进制字符串

> 原文:[https://www . geesforgeks . org/count-binary-strings-k-times-出现-相邻-两个设置位/](https://www.geeksforgeeks.org/count-binary-strings-k-times-appearing-adjacent-two-set-bits/)

给定两个整数 n 和 k，计算长度为 n 的二进制字符串的数量，其中 k 是相邻 1 出现的次数。

**示例:**

```
Input  : n = 5, k = 2
Output : 6
Explanation:
Binary strings of length 5 in which k number of times
two adjacent set bits appear.
00111  
01110
11100
11011
10111
11101

Input  : n = 4, k = 1
Output : 3
Explanation:
Binary strings of length 3 in which k number of times
two adjacent set bits appear.
0011  
1100
0110
```

让我们尝试为上面的问题语句编写递归函数:
1) n = 1，只有两个长度为 1 的二进制字符串存在，没有任何相邻的 1
字符串 1:“0”
字符串 2:“1”
2)对于所有的 n > 1 和所有的 k， 出现两种情况
a)以 0 结尾的字符串:长度为 n 的字符串可以通过将 0 附加到所有长度为 n-1 的**字符串上来创建，这些字符串具有 k 倍的两个以 0 和 1 结尾的相邻 1** (在第 n 个位置具有 0 不会改变相邻 1 的计数)。
b)以 1 结尾的字符串:长度为 n 的字符串可以通过将 1 附加到长度为 n-1 的所有字符串上来创建，其中 n-1 的长度为 k 倍，以 0 结尾，长度为 n-1 的所有字符串的长度为 k-1，以 1 结尾。

例如:假设 s = 011，即以 1 结尾的字符串，相邻计数为 1。加 1，s = 0111 增加相邻 1 的计数。

```
Let there be an array dp[i][j][2] where dp[i][j][0]
denotes number of binary strings with length i having
j number of two adjacent 1's and ending with 0.
Similarly dp[i][j][1] denotes the same binary strings
with length i and j adjacent 1's but ending with 1.
Then: 
    dp[1][0][0] = 1 and dp[1][0][1] = 1
    For all other i and j,
        dp[i][j][0] = dp[i-1][j][0] + dp[i-1][j][1]
        dp[i][j][1] = dp[i-1][j][0] + dp[i-1][j-1][1]

Then, output dp[n][k][0] + dp[n][k][1]
```

## C++

```
// C++ program to count number of binary strings
// with k times appearing consecutive 1's.
#include <bits/stdc++.h>
using namespace std;

int countStrings(int n, int k)
{
    // dp[i][j][0] stores count of binary
    // strings of length i with j consecutive
    // 1's and ending at 0.
    // dp[i][j][1] stores count of binary
    // strings of length i with j consecutive
    // 1's and ending at 1.
    int dp[n + 1][k + 1][2];
    memset(dp, 0, sizeof(dp));

    // If n = 1 and k = 0.
    dp[1][0][0] = 1;
    dp[1][0][1] = 1;

    for (int i = 2; i <= n; i++) {

        // number of adjacent 1's can not exceed i-1
        for (int j = 0; j <= k; j++) {
            dp[i][j][0] = dp[i - 1][j][0] + dp[i - 1][j][1];
            dp[i][j][1] = dp[i - 1][j][0];

            if (j - 1 >= 0)
                dp[i][j][1] += dp[i - 1][j - 1][1];
        }
    }

    return dp[n][k][0] + dp[n][k][1];
}

// Driver code
int main()
{
    int n = 5, k = 2;
    cout << countStrings(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of binary strings
// with k times appearing consecutive 1's.
class GFG {

    static int countStrings(int n, int k)
    {
        // dp[i][j][0] stores count of binary
        // strings of length i with j consecutive
        // 1's and ending at 0.
        // dp[i][j][1] stores count of binary
        // strings of length i with j consecutive
        // 1's and ending at 1.
        int dp[][][] = new int[n + 1][k + 1][2];

        // If n = 1 and k = 0.
        dp[1][0][0] = 1;
        dp[1][0][1] = 1;

        for (int i = 2; i <= n; i++) {

            // number of adjacent 1's can not exceed i-1
            for (int j = 0; j < i && j < k + 1; j++) {
                dp[i][j][0] = dp[i - 1][j][0] + dp[i - 1][j][1];
                dp[i][j][1] = dp[i - 1][j][0];

                if (j - 1 >= 0) {
                    dp[i][j][1] += dp[i - 1][j - 1][1];
                }
            }
        }

        return dp[n][k][0] + dp[n][k][1];
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5, k = 2;
        System.out.println(countStrings(n, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count number of
# binary strings with k times appearing
# consecutive 1's.
def countStrings(n, k):

    # dp[i][j][0] stores count of binary
    # strings of length i with j consecutive
    # 1's and ending at 0.
    # dp[i][j][1] stores count of binary
    # strings of length i with j consecutive
    # 1's and ending at 1.
    dp = [[[0, 0] for __ in range(k + 1)]
                  for _ in range(n + 1)]

    # If n = 1 and k = 0.
    dp[1][0][0] = 1
    dp[1][0][1] = 1

    for i in range(2, n + 1):

        # number of adjacent 1's can not exceed i-1
        for j in range(k + 1):
            dp[i][j][0] = (dp[i - 1][j][0] +
                           dp[i - 1][j][1])
            dp[i][j][1] = dp[i - 1][j][0]
            if j >= 1:
                dp[i][j][1] += dp[i - 1][j - 1][1]

    return dp[n][k][0] + dp[n][k][1]

# Driver Code
if __name__ == '__main__':
    n = 5
    k = 2
    print(countStrings(n, k))

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# program to count number of binary strings
// with k times appearing consecutive 1's.
using System;

class GFG {

    static int countStrings(int n, int k)
    {
        // dp[i][j][0] stores count of binary
        // strings of length i with j consecutive
        // 1's and ending at 0.
        // dp[i][j][1] stores count of binary
        // strings of length i with j consecutive
        // 1's and ending at 1.
        int[,, ] dp = new int[n + 1, k + 1, 2];

        // If n = 1 and k = 0.
        dp[1, 0, 0] = 1;
        dp[1, 0, 1] = 1;

        for (int i = 2; i <= n; i++) {

            // number of adjacent 1's can not exceed i-1
            for (int j = 0; j < i && j < k + 1; j++) {
                dp[i, j, 0] = dp[i - 1, j, 0] + dp[i - 1, j, 1];
                dp[i, j, 1] = dp[i - 1, j, 0];

                if (j - 1 >= 0) {
                    dp[i, j, 1] += dp[i - 1, j - 1, 1];
                }
            }
        }

        return dp[n, k, 0] + dp[n, k, 1];
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 5, k = 2;
        Console.WriteLine(countStrings(n, k));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of binary strings
// with k times appearing consecutive 1's.

function countStrings($n, $k)
{
    // dp[i][j][0] stores count of binary
    // strings of length i with j consecutive
    // 1's and ending at 0.
    // dp[i][j][1] stores count of binary
    // strings of length i with j consecutive
    // 1's and ending at 1.
    $dp=array_fill(0, $n + 1, array_fill(0, $k + 1, array_fill(0, 2, 0)));

    // If n = 1 and k = 0.
    $dp[1][0][0] = 1;
    $dp[1][0][1] = 1;

    for ($i = 2; $i <= $n; $i++)
    {
        // number of adjacent 1's can not exceed i-1
        for ($j = 0; $j < $i; $j++)
        {
            if(isset($dp[$i][$j][0])||isset($dp[$i][$j][1])){
              $dp[$i][$j][0] = $dp[$i - 1][$j][0] + $dp[$i - 1][$j][1];
              $dp[$i][$j][1] = $dp[$i - 1][$j][0];
            }
            if ($j - 1 >= 0 && isset($dp[$i][$j][1]))
                $dp[$i][$j][1] += $dp[$i - 1][$j - 1][1];
        }
    }

    return $dp[$n][$k][0] + $dp[$n][$k][1];
}

// Driver code
$n=5;
$k=2;
echo countStrings($n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count number
// of binary strings with k times
// appearing consecutive 1's.
function countStrings(n, k)
{

    // dp[i][j][0] stores count of binary
    // strings of length i with j consecutive
    // 1's and ending at 0.
    // dp[i][j][1] stores count of binary
    // strings of length i with j consecutive
    // 1's and ending at 1.
    let dp = new Array(n + 1);
    for(let i = 0; i < n + 1; i++)
    {
        dp[i] = new Array(k + 1);
        for(let j = 0; j < k + 1; j++)
        {
            dp[i][j] = new Array(2);
            for(let l = 0 ; l < 2; l++)
            {
                dp[i][j][l] = 0;
            }
        }
    }

    // If n = 1 and k = 0.
    dp[1][0][0] = 1;
    dp[1][0][1] = 1;

    for(let i = 2; i <= n; i++)
    {

        // Number of adjacent 1's can not exceed i-1
        for(let j = 0; j < i && j < k + 1; j++)
        {
            dp[i][j][0] = dp[i - 1][j][0] +
                          dp[i - 1][j][1];
            dp[i][j][1] = dp[i - 1][j][0];

            if (j - 1 >= 0)
            {
                dp[i][j][1] += dp[i - 1][j - 1][1];
            }
        }
    }
    return dp[n][k][0] + dp[n][k][1];
}

// Driver code
let n = 5, k = 2;

document.write(countStrings(n, k));

// This code is contributed by rag2127

</script>
```

**输出:**

```
6
```

**时间复杂度:** O(n <sup>2</sup>

本文由 **Ekta Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。