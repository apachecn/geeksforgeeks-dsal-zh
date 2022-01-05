# 可被 n 整除的字符串中的子序列数

> 原文:[https://www . geesforgeks . org/number-subseries-string-除尽-n/](https://www.geeksforgeeks.org/number-subsequences-string-divisible-n/)

给定一个由数字 0-9 组成的字符串，计算其中可被 m 整除的子序列数
**示例:**

```
Input  : str = "1234", n = 4
Output : 4
The subsequences 4, 12, 24 and 124 are 
divisible by 4.

Input  : str = "330", n = 6
Output : 4
The subsequences 30, 30, 330 and 0 are 
divisible by n.

Input  : str = "676", n = 6
Output : 3
The subsequences 6, 6 and 66
```

这个问题可以递归定义。当用 n 除时，让值为 x 的字符串的余数为“r”。向该字符串中再添加一个字符会将其余数更改为(r*10 +新数字)% n。对于每个新字符，我们有两个选择，要么将其添加到所有当前子序列中，要么忽略它。因此，我们有一个最佳的子结构。以下是这个的暴力版本:

```
string str = "330";
int n = 6

// idx is value of current index in str
// rem is current remainder
int count(int idx, int rem)
{
    // If last character reached
    if (idx == n)
        return (rem == 0)? 1 : 0;

    int ans = 0;

    // we exclude it, thus remainder
    // remains the same
    ans += count(idx+1, rem);

    // we include it and thus new remainder
    ans += count(idx+1, (rem*10 + str[idx]-'0')%n);

    return ans;
}
```

上面的递归解有重叠的子问题，如下递归树所示。

```
          input string = "330"
             (0,0) ===> at 0th index with 0 remainder
(exclude 0th /      (include 0th character)
 character) /      
       (1,0)      (1,3) ======> at index 1 with 3 as 
      (E)/  (I)     /(E)       the current remainder
     (2,0)  (2,3)   (2,3)
             |-------|
     These two subproblems overlap  
```

因此，我们可以应用动态规划。下面是实现。

## C++

```
// C++ program to count subsequences of a
// string divisible by n.
#include<bits/stdc++.h>
using namespace std;

// Returns count of subsequences of str
// divisible by n.
int countDivisibleSubseq(string str, int n)
{
    int len = str.length();

    // division by n can leave only n remainder
    // [0..n-1]. dp[i][j] indicates number of
    // subsequences in string [0..i] which leaves
    // remainder j after division by n.
    int dp[len][n];
    memset(dp, 0, sizeof(dp));

    // Filling value for first digit in str
    dp[0][(str[0]-'0')%n]++;

    for (int i=1; i<len; i++)
    {
        // start a new subsequence with index i
        dp[i][(str[i]-'0')%n]++;

        for (int j=0; j<n; j++)
        {
            // exclude i'th character from all the
            // current subsequences of string [0...i-1]
            dp[i][j] += dp[i-1][j];

            // include i'th character in all the current
            // subsequences of string [0...i-1]
            dp[i][(j*10 + (str[i]-'0'))%n] += dp[i-1][j];
        }
    }

    return dp[len-1][0];
}

// Driver code
int main()
{
    string str = "1234";
    int n = 4;
    cout << countDivisibleSubseq(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to count subsequences of a
// string divisible by n

class GFG {

// Returns count of subsequences of str
// divisible by n.
    static int countDivisibleSubseq(String str, int n) {
        int len = str.length();

        // division by n can leave only n remainder
        // [0..n-1]. dp[i][j] indicates number of
        // subsequences in string [0..i] which leaves
        // remainder j after division by n.
        int dp[][] = new int[len][n];

        // Filling value for first digit in str
        dp[0][(str.charAt(0) - '0') % n]++;

        for (int i = 1; i < len; i++) {
            // start a new subsequence with index i
            dp[i][(str.charAt(i) - '0') % n]++;

            for (int j = 0; j < n; j++) {
                // exclude i'th character from all the
                // current subsequences of string [0...i-1]
                dp[i][j] += dp[i - 1][j];

                // include i'th character in all the current
                // subsequences of string [0...i-1]
                dp[i][(j * 10 + (str.charAt(i) - '0')) % n] += dp[i - 1][j];
            }
        }

        return dp[len - 1][0];
    }

// Driver code
    public static void main(String[] args) {
        String str = "1234";
        int n = 4;
        System.out.print(countDivisibleSubseq(str, n));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count subsequences
# of a string divisible by n.

# Returns count of subsequences of
# str divisible by n.
def countDivisibleSubseq(str, n):
    l = len(str)

    # division by n can leave only n remainder
    # [0..n-1]. dp[i][j] indicates number of
    # subsequences in string [0..i] which leaves
    # remainder j after division by n.
    dp = [[0 for x in range(l)]
             for y in range(n)]

    # Filling value for first digit in str
    dp[0][(ord(str[0]) - ord('0')) % n] += 1

    for i in range(1, l):

        # start a new subsequence with index i
        dp[i][(ord(str[i]) - ord('0')) % n] += 1

        for j in range(n):

            # exclude i'th character from all the
            # current subsequences of string [0...i-1]
            dp[i][j] += dp[i - 1][j]

            # include i'th character in all the current
            # subsequences of string [0...i-1]
            dp[i][(j * 10 + (ord(str[i]) -
                             ord('0'))) % n] += dp[i - 1][j]

    return dp[l - 1][0]

# Driver code
if __name__ == "__main__":

    str = "1234"
    n = 4
    print(countDivisibleSubseq(str, n))

# This code is contributed by ita_c
```

## C#

```
//C# program to count subsequences of a
// string divisible by n

using System;
class GFG {

// Returns count of subsequences of str
// divisible by n.
    static int countDivisibleSubseq(string str, int n) {
        int len = str.Length;

        // division by n can leave only n remainder
        // [0..n-1]. dp[i][j] indicates number of
        // subsequences in string [0..i] which leaves
        // remainder j after division by n.
        int[,] dp = new int[len,n];

        // Filling value for first digit in str
        dp[0,(str[0] - '0') % n]++;

        for (int i = 1; i < len; i++) {
            // start a new subsequence with index i
            dp[i,(str[i] - '0') % n]++;

            for (int j = 0; j < n; j++) {
                // exclude i'th character from all the
                // current subsequences of string [0...i-1]
                dp[i,j] += dp[i - 1,j];

                // include i'th character in all the current
                // subsequences of string [0...i-1]
                dp[i,(j * 10 + (str[i] - '0')) % n] += dp[i - 1,j];
            }
        }

        return dp[len - 1,0];
    }

// Driver code
    public static void Main() {
        String str = "1234";
        int n = 4;
        Console.Write(countDivisibleSubseq(str, n));
    }
}
```

## java 描述语言

```
<script>
//Javascript program to count subsequences of a
// string divisible by n

    // Returns count of subsequences of str
    // divisible by n.
    function countDivisibleSubseq(str,n)
    {
        let len = str.length;

        // division by n can leave only n remainder
        // [0..n-1]. dp[i][j] indicates number of
        // subsequences in string [0..i] which leaves
        // remainder j after division by n.
        let dp = new Array(len);
        for(let i = 0; i < len; i++)
        {
            dp[i] = new Array(n);
            for(let j = 0; j < n; j++)
            {
                dp[i][j] = 0;
            }
        }

        // Filling value for first digit in str
        dp[0][(str[0] - '0') % n]++;

        for (let i = 1; i < len; i++) {
            // start a new subsequence with index i
            dp[i][(str[i] - '0') % n]++;

            for (let j = 0; j < n; j++) {
                // exclude i'th character from all the
                // current subsequences of string [0...i-1]
                dp[i][j] += dp[i - 1][j];

                // include i'th character in all the current
                // subsequences of string [0...i-1]
                dp[i][(j * 10 + (str[i] - '0')) % n] += dp[i - 1][j];
            }
        }

        return dp[len - 1][0];
    }

    // Driver code
    let str = "1234";
    let n = 4;
    document.write(countDivisibleSubseq(str, n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
4
```

**时间复杂度:**O(len * n)
T3】辅助空间: O(len * n)
本文由 **Ekta Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。