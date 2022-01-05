# 三进制字符串中相邻字符不相等的最小替换数| Set-2

> 原文:[https://www . geeksforgeeks . org/最小替换使相邻字符不相等三进制字符串集-2/](https://www.geeksforgeeks.org/minimum-replacements-to-make-adjacent-characters-unequal-in-a-ternary-string-set-2/)

给定一个由“0”、“1”和“2”组成的字符串。任务是找到最小数量的替换，使相邻字符不相等。
**例:**

> **输入:** s = "201220211"
> **输出:** 2
> 变化后的合成串为 201210210
> **输入:** s = "0120102"
> **输出** : 0

**方法:**问题已经在[之前的](https://www.geeksforgeeks.org/minimum-replacements-to-make-adjacent-characters-unequal-in-a-ternary-string/)帖子中用贪婪的方法解决了。在这篇文章中，我们将讨论解决同样问题的动态编程方法。创建一个函数**字符**，根据字符返回 0、1 或 2。
递归函数调用 charVal 函数得到第 I 个值，如果这个值等于前一个值，那么在第 I 个字符处只使用另外两个状态(1 或 2，0 或 1，0 或 2)。如果它不等于前一个，则不会进行任何更改。dp[][]数组用于[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)。基本情况是所有位置都已填满。如果任何状态被重新访问，则返回存储在 dp[][]数组中的值。 *DP[i][j]表示第 I 个位置用第 j 个字符填充。*
下面是上面问题的实现:

## C++

```
// C++ program to count the minimal
// replacements such that adjacent characters
// are unequal
#include <bits/stdc++.h>
using namespace std;

// function to return integer value
// of i-th character in the string
int charVal(string s, int i)
{
    if (s[i] == '0')
        return 0;
    else if (s[i] == '1')
        return 1;
    else
        return 2;
}

// Function to count the number of
// minimal replacements
int countMinimalReplacements(string s, int i,
                        int prev, int dp[][3], int n)
{

    // If the string has reached the end
    if (i == n) {
        return 0;
    }

    // If the state has been visited previously
    if (dp[i][prev] != -1)
        return dp[i][prev];

    // Get the current value of character
    int val = charVal(s, i);
    int ans = INT_MAX;

    // If it is equal then change it
    if (val == prev) {
        int val = 0;

        // All possible changes
        for (int cur = 0; cur <= 2; cur++) {
            if (cur == prev)
                continue;

            // Change done
            val = 1 + countMinimalReplacements(s, i + 1, cur, dp, n);

            ans = min(ans, val);
        }
    }
    else // If same no change
        ans = countMinimalReplacements(s, i + 1, val, dp, n);

    return dp[i][val] = ans;
}

// Driver Code
int main()
{
    string s = "201220211";

    // Length of string
    int n = s.length();

    // Create a DP array
    int dp[n][3];

    memset(dp, -1, sizeof dp);

    // First character
    int val = charVal(s, 0);

    // Function to find minimal replacements
    cout << countMinimalReplacements(s, 1, val, dp, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the minimal
// replacements such that adjacent characters
// are unequal
class GFG
{

    // function to return integer value
    // of i-th character in the string
    static int charVal(String s, int i)
    {
        if (s.charAt(i) == '0')
        {
            return 0;
        }
        else if (s.charAt(i) == '1')
        {
            return 1;
        }
        else
        {
            return 2;
        }
    }

    // Function to count the number of
    // minimal replacements
    static int countMinimalReplacements(String s, int i,
                            int prev, int dp[][], int n)
    {

        // If the string has reached the end
        if (i == n)
        {
            return 0;
        }

        // If the state has been visited previously
        if (dp[i][prev] != -1)
        {
            return dp[i][prev];
        }

        // Get the current value of character
        int val = charVal(s, i);
        int ans = Integer.MAX_VALUE;

        // If it is equal then change it
        if (val == prev)
        {
            val = 0;

            // All possible changes
            for (int cur = 0; cur <= 2; cur++)
            {
                if (cur == prev)
                {
                    continue;
                }

                // Change done
                val = 1 + countMinimalReplacements(s,
                                    i + 1, cur, dp, n);

                ans = Math.min(ans, val);
            }
        } else // If same no change
        {
            ans = countMinimalReplacements(s, i + 1,
                                        val, dp, n);
        }

        return dp[i][val] = ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "201220211";

        // Length of string
        int n = s.length();

        // Create a DP array
        int dp[][] = new int[n][3];
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                dp[i][j] = -1;
            }
        }

        // First character
        int val = charVal(s, 0);

        // Function to find minimal replacements
        System.out.println(countMinimalReplacements(s, 1,
                                            val, dp, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to count the minimal
# replacements such that adjacent characters
# are unequal
import sys

# function to return integer value
# of i-th character in the string
def charVal(s, i):
    if (s[i] == '0'):
        return 0
    elif (s[i] == '1'):
        return 1
    else:
        return 2

# Function to count the number of
# minimal replacements
def countMinimalReplacements(s,i,prev, dp, n):

    # If the string has reached the end
    if (i == n):
        return 0

    # If the state has been visited previously
    if (dp[i][prev] != -1):
        return dp[i][prev]

    # Get the current value of character
    val = charVal(s, i)
    ans = sys.maxsize

    # If it is equal then change it
    if (val == prev):
        val = 0

        # All possible changes
        for cur in range(3):
            if (cur == prev):
                continue

            # Change done
            val = 1 + countMinimalReplacements(s, i + 1, cur, dp, n)
            ans = min(ans, val)

        # If same no change
    else:
        ans = countMinimalReplacements(s, i + 1, val, dp, n)

    dp[i][val] = ans

    return dp[i][val]

# Driver Code
if __name__ == '__main__':
    s = "201220211"

    # Length of string
    n = len(s)

    # Create a DP array
    dp = [[-1 for i in range(3)] for i in range(n)]

    # First character
    val = charVal(s, 0)

    # Function to find minimal replacements
    print(countMinimalReplacements(s, 1, val, dp, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count the minimal
// replacements such that adjacent
// characters are unequal
using System;

class GFG
{

    // function to return integer value
    // of i-th character in the string
    static int charVal(string s, int i)
    {
        if (s[i] == '0')
        {
            return 0;
        }
        else if (s[i] == '1')
        {
            return 1;
        }
        else
        {
            return 2;
        }
    }

    // Function to count the number of
    // minimal replacements
    static int countMinimalReplacements(string s, int i,
                            int prev, int [,]dp, int n)
    {

        // If the string has reached the end
        if (i == n)
        {
            return 0;
        }

        // If the state has been visited previously
        if (dp[i,prev] != -1)
        {
            return dp[i,prev];
        }

        // Get the current value of character
        int val = charVal(s, i);
        int ans = int.MaxValue;

        // If it is equal then change it
        if (val == prev)
        {
            val = 0;

            // All possible changes
            for (int cur = 0; cur <= 2; cur++)
            {
                if (cur == prev)
                {
                    continue;
                }

                // Change done
                val = 1 + countMinimalReplacements(s,
                                    i + 1, cur, dp, n);

                ans = Math.Min(ans, val);
            }
        }
        else // If same no change
        {
            ans = countMinimalReplacements(s, i + 1,
                                        val, dp, n);
        }

        return dp[i,val] = ans;
    }

    // Driver Code
    public static void Main()
    {
        string s = "201220211";

        // Length of string
        int n = s.Length;

        // Create a DP array
        int [,]dp = new int[n,3];
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                dp[i,j] = -1;
            }
        }

        // First character
        int val = charVal(s, 0);

        // Function to find minimal replacements
        Console.WriteLine(countMinimalReplacements(s, 1,
                                            val, dp, n));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript program to count the minimal
// replacements such that adjacent characters
// are unequal   

// function to return integer value
    // of i-th character in the string
    function charVal( s , i) {
        if (s.charAt(i) == '0') {
            return 0;
        } else if (s.charAt(i) == '1') {
            return 1;
        } else {
            return 2;
        }
    }

    // Function to count the number of
    // minimal replacements
    function countMinimalReplacements( s , i , prev , dp , n)
    {

        // If the string has reached the end
        if (i == n) {
            return 0;
        }

        // If the state has been visited previously
        if (dp[i][prev] != -1) {
            return dp[i][prev];
        }

        // Get the current value of character
        var val = charVal(s, i);
        var ans = Number.MAX_VALUE;

        // If it is equal then change it
        if (val == prev) {
            val = 0;

            // All possible changes
            for (var cur = 0; cur <= 2; cur++) {
                if (cur == prev) {
                    continue;
                }

                // Change done
                val = 1 +
                countMinimalReplacements(s, i + 1, cur, dp, n);

                ans = Math.min(ans, val);
            }
        } else // If same no change
        {
            ans =
            countMinimalReplacements(s, i + 1, val, dp, n);
        }

        return dp[i][val] = ans;
    }

    // Driver Code

        var s = "201220211";

        // Length of string
        var n = s.length;

        // Create a DP array
        var dp = Array(n).fill().map(()=>Array(3).fill(0));
        for (var i = 0; i < n; i++) {
            for (var j = 0; j < 3; j++) {
                dp[i][j] = -1;
            }
        }

        // First character
        var val = charVal(s, 0);

        // Function to find minimal replacements
 document.write(countMinimalReplacements(s, 1, val, dp, n));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```