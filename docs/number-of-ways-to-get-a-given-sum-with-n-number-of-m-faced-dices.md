# 用 n 个 m 面骰子获得给定和的方法数

> 原文:[https://www . geeksforgeeks . org/获得给定 m 面骰子点数的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-get-a-given-sum-with-n-number-of-m-faced-dices/)

给定 n 个骰子，每个骰子有 m 个面，从 1 到 m，找出获得给定和 X 的方法数。X 是所有骰子投掷时每个面上的值的总和。
**例:**

> **输入:**面= 4 投= 2 和=4
> **输出:**3
> 2 投中达到和等于 4 的方式可以是{ (1，3)，(2，2)，(3，1) }
> **输入:**面= 6 投= 3 和= 12
> **输出:** 25

**方法:**
基本上，要求使用[1…m]范围内的值实现 n 次运算的和。
对此问题使用动态规划自上而下的方法。步骤是:

*   基本案例:
    1.  *If (sum == 0 且 noofthrowsleft = = 0)返回 1* 。这意味着总和 x 已经达到
        。
    2.  *If(将< 0 和 noofthrowsleft = = 0 相加)返回 0* 。这意味着 x 总和并没有在所有的投掷中达到
        。
*   如果当前 noofthrowsleft 的当前和已经实现，那么从表中返回它，而不是重新计算。
*   然后我们将循环遍历 i=[1..m]并递归移动以实现 sum-i，同时将 noofthrowsleft 减少 1。
*   最后，我们将在 dp 数组中存储当前值

以下是上述方法的实现:

## C++

```
// C++ function to calculate the number of
// ways to achieve sum x in n no of throws
#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007
int dp[55][55];

// Function to calculate recursively the
// number of ways to get sum in given
// throws and [1..m] values
int NoofWays(int face, int throws, int sum)
{
    // Base condition 1
    if (sum == 0 && throws == 0)
        return 1;

    // Base condition 2
    if (sum < 0 || throws == 0)
        return 0;

    // If value already calculated dont
    // move into re-computation
    if (dp[throws][sum] != -1)
        return dp[throws][sum];

    int ans = 0;
    for (int i = 1; i <= face; i++) {

        // Recursively moving for sum-i in
        // throws-1 no of throws left
        ans += NoofWays(face, throws - 1, sum - i);
    }

    // Inserting present values in dp
    return dp[throws][sum] = ans;
}

// Driver function
int main()
{
    int faces = 6, throws = 3, sum = 12;

    memset(dp, -1, sizeof dp);

    cout << NoofWays(faces, throws, sum) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java function to calculate the number of
// ways to achieve sum x in n no of throwsVal
class GFG
{

    static int mod = 1000000007;
    static int[][] dp = new int[55][55];

    // Function to calculate recursively the
    // number of ways to get sum in given
    // throwsVal and [1..m] values
    static int NoofWays(int face, int throwsVal, int sum)
    {
        // Base condition 1
        if (sum == 0 && throwsVal == 0)
        {
            return 1;
        }

        // Base condition 2
        if (sum < 0 || throwsVal == 0)
        {
            return 0;
        }

        // If value already calculated dont
        // move into re-computation
        if (dp[throwsVal][sum] != -1)
        {
            return dp[throwsVal][sum];
        }

        int ans = 0;
        for (int i = 1; i <= face; i++)
        {

            // Recursively moving for sum-i in
            // throwsVal-1 no of throwsVal left
            ans += NoofWays(face, throwsVal - 1, sum - i);
        }

        // Inserting present values in dp
        return dp[throwsVal][sum] = ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int faces = 6, throwsVal = 3, sum = 12;
        for (int i = 0; i < 55; i++)
        {
            for (int j = 0; j < 55; j++)
            {
                dp[i][j] = -1;
            }
        }

        System.out.println(NoofWays(faces, throwsVal, sum));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 function to calculate the number of
# ways to achieve sum x in n no of throws
import numpy as np

mod = 1000000007;

dp = np.zeros((55,55));

# Function to calculate recursively the
# number of ways to get sum in given
# throws and [1..m] values
def NoofWays(face, throws, sum) :

    # Base condition 1
    if (sum == 0 and throws == 0) :
        return 1;

    # Base condition 2
    if (sum < 0 or throws == 0) :
        return 0;

    # If value already calculated dont
    # move into re-computation
    if (dp[throws][sum] != -1) :
        return dp[throws][sum];

    ans = 0;
    for i in range(1, face + 1) :

        # Recursively moving for sum-i in
        # throws-1 no of throws left
        ans += NoofWays(face, throws - 1, sum - i);

    # Inserting present values in dp
    dp[throws][sum] = ans;

    return ans;

# Driver function
if __name__ == "__main__" :

    faces = 6; throws = 3; sum = 12;

    for i in range(55) :
        for j in range(55) :
            dp[i][j] = -1

    print(NoofWays(faces, throws, sum)) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# function to calculate the number of
// ways to achieve sum x in n no of throwsVal
using System;

class GFG
{

    static int[,]dp = new int[55,55];

    // Function to calculate recursively the
    // number of ways to get sum in given
    // throwsVal and [1..m] values
    static int NoofWays(int face, int throwsVal, int sum)
    {
        // Base condition 1
        if (sum == 0 && throwsVal == 0)
        {
            return 1;
        }

        // Base condition 2
        if (sum < 0 || throwsVal == 0)
        {
            return 0;
        }

        // If value already calculated dont
        // move into re-computation
        if (dp[throwsVal,sum] != -1)
        {
            return dp[throwsVal,sum];
        }

        int ans = 0;
        for (int i = 1; i <= face; i++)
        {

            // Recursively moving for sum-i in
            // throwsVal-1 no of throwsVal left
            ans += NoofWays(face, throwsVal - 1, sum - i);
        }

        // Inserting present values in dp
        return dp[throwsVal,sum] = ans;
    }

    // Driver code
    static public void Main ()
    {
        int faces = 6, throwsVal = 3, sum = 12;
        for (int i = 0; i < 55; i++)
        {
            for (int j = 0; j < 55; j++)
            {
                dp[i,j] = -1;
            }
        }

    Console.WriteLine(NoofWays(faces, throwsVal, sum));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript function to calculate the number of
// ways to achieve sum x in n no of throws

const mod = 1000000007;
let dp = new Array(55);
for (let i = 0; i < 55; i++)
    dp[i] = new Array(55).fill(-1);

// Function to calculate recursively the
// number of ways to get sum in given
// throws and [1..m] values
function NoofWays(face, throws, sum)
{
    // Base condition 1
    if (sum == 0 && throws == 0)
        return 1;

    // Base condition 2
    if (sum < 0 || throws == 0)
        return 0;

    // If value already calculated dont
    // move into re-computation
    if (dp[throws][sum] != -1)
        return dp[throws][sum];

    let ans = 0;
    for (let i = 1; i <= face; i++) {

        // Recursively moving for sum-i in
        // throws-1 no of throws left
        ans += NoofWays(face, throws - 1, sum - i);
    }

    // Inserting present values in dp
    return dp[throws][sum] = ans;
}

// Driver function
    let faces = 6, throws = 3, sum = 12;
    document.write(NoofWays(faces, throws, sum));

</script>
```

**Output:** 

```
25
```

**时间复杂度:** O(投掷*脸*和)
T3】空间复杂度: O(脸*和)