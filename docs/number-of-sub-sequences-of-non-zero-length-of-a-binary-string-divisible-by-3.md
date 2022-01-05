# 可被 3 整除的二进制字符串的非零长度的子序列数

> 原文:[https://www . geesforgeks . org/非零长度二进制字符串可被 3 整除的子序列数/](https://www.geeksforgeeks.org/number-of-sub-sequences-of-non-zero-length-of-a-binary-string-divisible-by-3/)

给定一个长度为 **N** 的二进制字符串 **S** ，任务是找出长度为非零且可被 **3** 整除的子序列的数量。子序列中的前导零是允许的。
**举例:**

> **输入:** S = "1001"
> **输出:**5
> “11”“1001”“0”“0”“00”是
> 唯一可被 3 整除的子序列。
> **输入:** S = "1"
> **输出:** 0

**天真方法:**生成所有可能的子序列，检查它们是否能被 3 整除。时间复杂度为(2 <sup>N</sup> ) * N。
**更好的做法:**动态规划可以解决这个问题。让我们看看民主党的状态。
**DP[i][r]** 将存储子串 **S[i…N-1]** 的子序列数，使得当除以 **3** 时，它们给出**(3–r)% 3**的余数。
现在写递归关系。

> DP[i][r] = DP[i + 1][（r * 2 + s[i]） % 3] + DP[i + 1][r]

递归是因为以下两个选择而导出的:

1.  将当前索引 **i** 包含在子序列中。因此， **r** 将更新为 **r = (r * 2 + s[i]) % 3** 。
2.  不要在子序列中包含当前索引。

以下是上述方法的实现:

## C++

```
// C++ implementation of th approach
#include <bits/stdc++.h>
using namespace std;
#define N 100

int dp[N][3];
bool v[N][3];

// Function to return the number of
// sub-sequences divisible by 3
int findCnt(string& s, int i, int r)
{
    // Base-cases
    if (i == s.size()) {
        if (r == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved
    // before then return its value
    if (v[i][r])
        return dp[i][r];

    // Marking the state as solved
    v[i][r] = 1;

    // Recurrence relation
    dp[i][r]
        = findCnt(s, i + 1, (r * 2 + (s[i] - '0')) % 3)
          + findCnt(s, i + 1, r);

    return dp[i][r];
}

// Driver code
int main()
{
    string s = "11";

    cout << (findCnt(s, 0, 0) - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of th approach
class GFG
{

    static final int N = 100;

    static int dp[][] = new int[N][3];
    static int v[][] = new int[N][3];

    // Function to return the number of
    // sub-sequences divisible by 3
    static int findCnt(String s, int i, int r)
    {
        // Base-cases
        if (i == s.length())
        {
            if (r == 0)
                return 1;
            else
                return 0;
        }

        // If the state has been solved
        // before then return its value
        if (v[i][r] == 1)
            return dp[i][r];

        // Marking the state as solved
        v[i][r] = 1;

        // Recurrence relation
        dp[i][r] = findCnt(s, i + 1, (r * 2 + (s.charAt(i) - '0')) % 3)
                    + findCnt(s, i + 1, r);

        return dp[i][r];
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "11";

        System.out.print(findCnt(s, 0, 0) - 1);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of th approach
import numpy as np
N = 100

dp = np.zeros((N, 3));
v = np.zeros((N, 3));

# Function to return the number of
# sub-sequences divisible by 3
def findCnt(s, i, r) :

    # Base-cases
    if (i == len(s)) :

        if (r == 0) :
            return 1;
        else :
            return 0;

    # If the state has been solved
    # before then return its value
    if (v[i][r]) :
        return dp[i][r];

    # Marking the state as solved
    v[i][r] = 1;

    # Recurrence relation
    dp[i][r] = findCnt(s, i + 1, (r * 2 +
                      (ord(s[i]) - ord('0'))) % 3) + \
               findCnt(s, i + 1, r);

    return dp[i][r];

# Driver code
if __name__ == "__main__" :

    s = "11";

    print(findCnt(s, 0, 0) - 1);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of th approach
using System;

class GFG
{

    static readonly int N = 100;

    static int [,]dp = new int[N, 3];
    static int [,]v = new int[N, 3];

    // Function to return the number of
    // sub-sequences divisible by 3
    static int findCnt(String s, int i, int r)
    {
        // Base-cases
        if (i == s.Length)
        {
            if (r == 0)
                return 1;
            else
                return 0;
        }

        // If the state has been solved
        // before then return its value
        if (v[i, r] == 1)
            return dp[i, r];

        // Marking the state as solved
        v[i, r] = 1;

        // Recurrence relation
        dp[i, r] = findCnt(s, i + 1, (r * 2 + (s[i] - '0')) % 3)
                    + findCnt(s, i + 1, r);

        return dp[i, r];
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "11";

        Console.Write(findCnt(s, 0, 0) - 1);

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of th approach
var N = 100

var dp = Array.from(Array(N), ()=> Array(3));
var v = Array.from(Array(N), ()=> Array(3));

// Function to return the number of
// sub-sequences divisible by 3
function findCnt(s, i, r)
{
    // Base-cases
    if (i == s.length) {
        if (r == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved
    // before then return its value
    if (v[i][r])
        return dp[i][r];

    // Marking the state as solved
    v[i][r] = 1;

    // Recurrence relation
    dp[i][r]
        = findCnt(s, i + 1, (r * 2 + (s[i] - '0')) % 3)
          + findCnt(s, i + 1, r);

    return dp[i][r];
}

// Driver code
var s = "11";
document.write( (findCnt(s, 0, 0) - 1));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n)