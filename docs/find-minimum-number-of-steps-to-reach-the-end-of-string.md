# 找到到达字符串末尾的最小步数

> 原文:[https://www . geesforgeks . org/find-到达字符串末尾的最小步骤数/](https://www.geeksforgeeks.org/find-minimum-number-of-steps-to-reach-the-end-of-string/)

给定一个长度为 **N** 的二进制字符串 **str** 和一个整数 **K** ，任务是找到从**str【0】**移动到**str【N–1】**所需的最小步数，移动如下:

1.  从指数 **i** 来看，唯一有效的移动是 **i + 1** 、 **i + 2** 和 **i + K**
2.  只有当**字符串[i] = '1'** 时，才能访问索引 **i**

**例:**

> **输入:**str =“101000011”，K = 5
> **输出:**3
> str[0]->str[2]->str[7]->str[8]
> **输入:**str =“1100000100111”，K = 6
> **输出:** -1
> 没有可能的路径。
> **输入:**str = " 101010101111010101 "，K = 4
> **输出:** 6

**做法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决问题。

*   给出了对于任何指数 **i** ，都有可能移动到指数 i+1、i+2 或 i+K。
*   三种可能性中的一种将给出所需的结果，即到达终点的最小步数。
*   因此，dp[]数组是以自下而上的方式创建和填充的。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of steps to reach the end
int minSteps(string str, int n, int k)
{

    // If the end can't be reached
    if (str[n - 1] == '0')
        return -1;

    // Already at the end
    if (n == 1)
        return 0;

    // If the length is 2 or 3 then the end
    // can be reached in a single step
    if (n < 4)
        return 1;

    // For the other cases, solve the problem
    // using dynamic programming
    int dp[n];

    // It requires no move from the
    // end to reach the end
    dp[n - 1] = 0;

    // From the 2nd last and the 3rd last
    // index, only a single move is required
    dp[n - 2] = 1;
    dp[n - 3] = 1;

    // Update the answer for every index
    for (int i = n - 4; i >= 0; i--) {

        // If the current index is not reachable
        if (str[i] == '0')
            continue;

        // To store the minimum steps required
        // from the current index
        int steps = INT_MAX;

        // If it is a valid move then update
        // the minimum steps required
        if (i + k < n && str[i + k] == '1')
            steps = min(steps, dp[i + k]);

        if (str[i + 1] == '1')
            steps = min(steps, dp[i + 1]);

        if (str[i + 2] == '1')
            steps = min(steps, dp[i + 2]);

        // Update the minimum steps required starting
        // from the current index
        dp[i] = (steps == INT_MAX) ? steps : 1 + steps;
    }

    // Cannot reach the end starting from str[0]
    if (dp[0] == INT_MAX)
        return -1;

    // Return the minimum steps required
    return dp[0];
}

// Driver code
int main()
{
    string str = "101000011";
    int n = str.length();
    int k = 5;

    cout << minSteps(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    final static int INT_MAX = Integer.MAX_VALUE ;

    // Function to return the minimum number
    // of steps to reach the end
    static int minSteps(String str, int n, int k)
    {

        // If the end can't be reached
        if (str.charAt(n - 1) == '0')
            return -1;

        // Already at the end
        if (n == 1)
            return 0;

        // If the length is 2 or 3 then the end
        // can be reached in a single step
        if (n < 4)
            return 1;

        // For the other cases, solve the problem
        // using dynamic programming
        int dp[] = new int[n];

        // It requires no move from the
        // end to reach the end
        dp[n - 1] = 0;

        // From the 2nd last and the 3rd last
        // index, only a single move is required
        dp[n - 2] = 1;
        dp[n - 3] = 1;

        // Update the answer for every index
        for (int i = n - 4; i >= 0; i--)
        {

            // If the current index is not reachable
            if (str.charAt(i) == '0')
                continue;

            // To store the minimum steps required
            // from the current index
            int steps =INT_MAX ;

            // If it is a valiINT_MAXd move then update
            // the minimum steps required
            if (i + k < n && str.charAt(i + k) == '1')
                steps = Math.min(steps, dp[i + k]);

            if (str.charAt(i + 1) == '1')
                steps = Math.min(steps, dp[i + 1]);

            if (str.charAt(i + 2) == '1')
                steps = Math.min(steps, dp[i + 2]);

            // Update the minimum steps required starting
            // from the current index
            dp[i] = (steps == INT_MAX) ? steps : 1 + steps;
        }

        // Cannot reach the end starting from str[0]
        if (dp[0] == INT_MAX)
            return -1;

        // Return the minimum steps required
        return dp[0];
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "101000011";
        int n = str.length();
        int k = 5;

        System.out.println(minSteps(str, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

INT_MAX = sys.maxsize;

# Function to return the minimum number
# of steps to reach the end
def minSteps(string , n, k) :

    # If the end can't be reached
    if (string[n - 1] == '0') :
        return -1;

    # Already at the end
    if (n == 1) :
        return 0;

    # If the length is 2 or 3 then the end
    # can be reached in a single step
    if (n < 4) :
        return 1;

    # For the other cases, solve the problem
    # using dynamic programming
    dp = [0] * n;

    # It requires no move from the
    # end to reach the end
    dp[n - 1] = 0;

    # From the 2nd last and the 3rd last
    # index, only a single move is required
    dp[n - 2] = 1;
    dp[n - 3] = 1;

    # Update the answer for every index
    for i in range(n - 4, -1, -1) :

        # If the current index is not reachable
        if (string[i] == '0') :
            continue;

        # To store the minimum steps required
        # from the current index
        steps = INT_MAX;

        # If it is a valid move then update
        # the minimum steps required
        if (i + k < n and string[i + k] == '1') :
            steps = min(steps, dp[i + k]);

        if (string[i + 1] == '1') :
            steps = min(steps, dp[i + 1]);

        if (string[i + 2] == '1') :
            steps = min(steps, dp[i + 2]);

        # Update the minimum steps required starting
        # from the current index
        dp[i] = steps if (steps == INT_MAX) else (1 + steps);

    # Cannot reach the end starting from str[0]
    if (dp[0] == INT_MAX) :
        return -1;

    # Return the minimum steps required
    return dp[0];

# Driver code
if __name__ == "__main__" :

    string = "101000011";
    n = len(string);
    k = 5;

    print(minSteps(string, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int INT_MAX = int.MaxValue ;

    // Function to return the minimum number
    // of steps to reach the end
    static int minSteps(string str, int n, int k)
    {

        // If the end can't be reached
        if (str[n - 1] == '0')
            return -1;

        // Already at the end
        if (n == 1)
            return 0;

        // If the length is 2 or 3 then the end
        // can be reached in a single step
        if (n < 4)
            return 1;

        // For the other cases, solve the problem
        // using dynamic programming
        int []dp = new int[n];

        // It requires no move from the
        // end to reach the end
        dp[n - 1] = 0;

        // From the 2nd last and the 3rd last
        // index, only a single move is required
        dp[n - 2] = 1;
        dp[n - 3] = 1;

        // Update the answer for every index
        for (int i = n - 4; i >= 0; i--)
        {

            // If the current index is not reachable
            if (str[i] == '0')
                continue;

            // To store the minimum steps required
            // from the current index
            int steps = INT_MAX ;

            // If it is a valiINT_MAXd move then update
            // the minimum steps required
            if (i + k < n && str[i + k] == '1')
                steps = Math.Min(steps, dp[i + k]);

            if (str[i + 1] == '1')
                steps = Math.Min(steps, dp[i + 1]);

            if (str[i + 2] == '1')
                steps = Math.Min(steps, dp[i + 2]);

            // Update the minimum steps required starting
            // from the current index
            dp[i] = (steps == INT_MAX) ? steps : 1 + steps;
        }

        // Cannot reach the end starting from str[0]
        if (dp[0] == INT_MAX)
            return -1;

        // Return the minimum steps required
        return dp[0];
    }

    // Driver code
    public static void Main()
    {
        string str = "101000011";
        int n = str.Length;
        int k = 5;

        Console.WriteLine(minSteps(str, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum number
// of steps to reach the end
function minSteps(str, n, k)
{

    // If the end can't be reached
    if (str[n - 1] == '0')
        return -1;

    // Already at the end
    if (n == 1)
        return 0;

    // If the length is 2 or 3 then the end
    // can be reached in a single step
    if (n < 4)
        return 1;

    // For the other cases, solve the problem
    // using dynamic programming
    var dp = Array(n);

    // It requires no move from the
    // end to reach the end
    dp[n - 1] = 0;

    // From the 2nd last and the 3rd last
    // index, only a single move is required
    dp[n - 2] = 1;
    dp[n - 3] = 1;

    // Update the answer for every index
    for (var i = n - 4; i >= 0; i--) {

        // If the current index is not reachable
        if (str[i] == '0')
            continue;

        // To store the minimum steps required
        // from the current index
        var steps = 1000000000;

        // If it is a valid move then update
        // the minimum steps required
        if (i + k < n && str[i + k] == '1')
            steps = Math.min(steps, dp[i + k]);

        if (str[i + 1] == '1')
            steps = Math.min(steps, dp[i + 1]);

        if (str[i + 2] == '1')
            steps = Math.min(steps, dp[i + 2]);

        // Update the minimum steps required starting
        // from the current index
        dp[i] = (steps == 1000000000) ? steps : 1 + steps;
    }

    // Cannot reach the end starting from str[0]
    if (dp[0] == 1000000000)
        return -1;

    // Return the minimum steps required
    return dp[0];
}

// Driver code
var str = "101000011";
var n = str.length;
var k = 5;
document.write( minSteps(str, n, k));

// This code is contributed by famously.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)，其中 N 是字符串的长度。