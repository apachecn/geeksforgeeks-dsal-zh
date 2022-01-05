# 结对人数

> 原文:[https://www . geesforgeks . org/配对人数/](https://www.geeksforgeeks.org/number-of-ways-to-pair-people/)

假设一个派对上有 p 个人。每个人可以作为一个单独的个体加入舞蹈，也可以作为一对与任何其他人一起加入。任务是找出 p 人可以加入舞蹈的不同方式的数量。
**例:**

```
Input : p = 3
Output : 4
Let the three people be P1, P2 and P3
Different ways are: {P1, P2, P3}, {{P1, P2}, P3},
{{P1, P3}, P2} and {{P2, P3}, P1}.

Input : p = 2
Output : 2
The groups are: {P1, P2} and {{P1, P2}}.
```

**做法:**思路是用动态规划来解决这个问题。有两种情况:要么这个人作为单个个体加入舞蹈，要么作为一对加入舞蹈。对于第一种情况，问题简化为为 p-1 人员找到解决方案。对于第二种情况，有 p-1 个选择来选择要配对的个体，并且在选择要配对的个体之后，问题简化为为 p-2 个人找到解决方案，因为 p 中的两个人已经配对了。
所以 dp 的公式是:

```
dp[p] = dp[p-1] + (p-1) * dp[p-2].
```

以下是上述方法的实现:

## C++

```
// CPP program to find number of ways to
// pair people in party

#include <bits/stdc++.h>
using namespace std;

// Function to find number of ways to
// pair people in party
int findWaysToPair(int p)
{
    // To store count of number of ways.
    int dp[p + 1];

    dp[1] = 1;
    dp[2] = 2;

    // Using the recurrence defined find
    // count for different values of p.
    for (int i = 3; i <= p; i++) {
        dp[i] = dp[i - 1] + (i - 1) * dp[i - 2];
    }

    return dp[p];
}

// Driver code
int main()
{
    int p = 3;
    cout << findWaysToPair(p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways to
// pair people in party

class GFG
{

// Function to find number of ways to
// pair people in party
static int findWaysToPair(int p)
{
    // To store count of number of ways.
    int dp[] = new int[p + 1];

    dp[1] = 1;
    dp[2] = 2;

    // Using the recurrence defined find
    // count for different values of p.
    for (int i = 3; i <= p; i++)
    {
        dp[i] = dp[i - 1] + (i - 1) * dp[i - 2];
    }

    return dp[p];
}

// Driver code
public static void main(String args[])
{
    int p = 3;
    System.out.println(findWaysToPair(p));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find number of
# ways to pair people in party

# Function to find number of ways
# to pair people in party
def findWays(p):

    # To store count of number of ways.
    dp = [0] * (p + 1)
    dp[1] = 1
    dp[2] = 2

    # Using the recurrence defined find
    # count for different values of p.
    for i in range(3, p + 1):
        dp[i] = (dp[i - 1] +
                   (i - 1) * dp[i - 2])
    return dp[p]

# Driver code
p = 3
print(findWays(p))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find number of ways to
// pair people in party
using System;

class GFG
{

// Function to find number of ways to
// pair people in party
public static int findWaysToPair(int p)
{
    // To store count of number of ways.
    int[] dp = new int[p + 1];

    dp[1] = 1;
    dp[2] = 2;

    // Using the recurrence defined find
    // count for different values of p.
    for (int i = 3; i <= p; i++)
    {
        dp[i] = dp[i - 1] + (i - 1) * dp[i - 2];
    }
    return dp[p];
}

// Driver code
public static void Main(string[] args)
{
    int p = 3;
    Console.WriteLine(findWaysToPair(p));
}
}

// This code is contributed by shrikanth13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of ways
// to pair people in party

// Function to find number of ways to
// pair people in party
function findWaysToPair($p)
{
    // To store count of number of ways.
    $dp = array();

    $dp[1] = 1;
    $dp[2] = 2;

    // Using the recurrence defined find
    // count for different values of p.
    for ($i = 3; $i <= $p; $i++)
    {
        $dp[$i] = $dp[$i - 1] +
                     ($i - 1) * $dp[$i - 2];
    }

    return $dp[$p];
}

// Driver code
$p = 3;
echo findWaysToPair($p);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to find number of ways to
// pair people in party

// Function to find number of ways to
// pair people in party
function findWaysToPair(p)
{
    // To store count of number of ways.
    var dp = Array(p+1);

    dp[1] = 1;
    dp[2] = 2;

    // Using the recurrence defined find
    // count for different values of p.
    for (var i = 3; i <= p; i++) {
        dp[i] = dp[i - 1] + (i - 1) * dp[i - 2];
    }

    return dp[p];
}

// Driver code
var p = 3;
document.write( findWaysToPair(p));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(p)
T3】辅助空间: O(p)