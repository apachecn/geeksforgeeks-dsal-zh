# 一次 2 步或 3 步到达某点的概率

> 原文:[https://www . geesforgeks . org/概率-到达点-2-3 步-时间/](https://www.geeksforgeeks.org/probability-reaching-point-2-3-steps-time/)

一个人从 X = 0 的位置开始走，如果她只能走 2 步或 3 步，找到恰好到达 X = N 的概率。给出步长 2 的概率，即步长 3 的概率为 1–P
**例:**

```
Input : N = 5, P = 0.20
Output : 0.32
Explanation :-
There are two ways to reach 5.
2+3 with probability = 0.2 * 0.8 = 0.16
3+2 with probability = 0.8 * 0.2 = 0.16
So, total probability = 0.32.
```

这是一个简单的[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)问题。它是这个问题的简单延伸:- [计数-不同方式-表达-n-和-1-3-4](https://www.geeksforgeeks.org/count-ofdifferent-ways-express-n-sum-1-3-4/)
下面是上述方法的实现。

## C++

```
// CPP Program to find probability to
// reach N with P probability to take
// 2 steps (1-P) to take 3 steps
#include <bits/stdc++.h>
using namespace std;

// Returns probability to reach N
float find_prob(int N, float P)
{
    double dp[N + 1];
    dp[0] = 1;
    dp[1] = 0;
    dp[2] = P;
    dp[3] = 1 - P;
    for (int i = 4; i <= N; ++i)
        dp[i] = (P)*dp[i - 2] + (1 - P) * dp[i - 3];

    return dp[N];
}

// Driver code
int main()
{
    int n = 5;
    float p = 0.2;
    cout << find_prob(n, p);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find probability to
// reach N with P probability to take
// 2 steps (1-P) to take 3 steps
import java.io.*;

class GFG {

    // Returns probability to reach N
    static float find_prob(int N, float P)
    {
        double dp[] = new double[N + 1];
        dp[0] = 1;
        dp[1] = 0;
        dp[2] = P;
        dp[3] = 1 - P;

        for (int i = 4; i <= N; ++i)
          dp[i] = (P) * dp[i - 2] +
                        (1 - P) * dp[i - 3];

        return ((float)(dp[N]));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        float p = 0.2f;
        System.out.printf("%.2f",find_prob(n, p));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 Program to find
# probability to reach N with
# P probability to take 2
# steps (1-P) to take 3 steps

# Returns probability to reach N
def find_prob(N, P) :

    dp =[0] * (n + 1)
    dp[0] = 1
    dp[1] = 0
    dp[2] = P
    dp[3] = 1 - P

    for i in range(4, N + 1) :
        dp[i] = (P) * dp[i - 2] + (1 - P) * dp[i - 3]

    return dp[N]

# Driver code
n = 5
p = 0.2
print(round(find_prob(n, p), 2))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find probability to
// reach N with P probability to take
// 2 steps (1-P) to take 3 steps
using System;

class GFG {

    // Returns probability to reach N
    static float find_prob(int N, float P)
    {
        double []dp = new double[N + 1];
        dp[0] = 1;
        dp[1] = 0;
        dp[2] = P;
        dp[3] = 1 - P;

        for (int i = 4; i <= N; ++i)
        dp[i] = (P) * dp[i - 2] +
                (1 - P) * dp[i - 3];

        return ((float)(dp[N]));
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        float p = 0.2f;
        Console.WriteLine(find_prob(n, p));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find probability to
// reach N with P probability to take
// 2 steps (1-P) to take 3 steps

// Returns probability to reach N
function find_prob($N, $P)
{
    $dp;
    $dp[0] = 1;
    $dp[1] = 0;
    $dp[2] = $P;
    $dp[3] = 1 - $P;
    for ($i = 4; $i <= $N; ++$i)
        $dp[$i] = ($P) * $dp[$i - 2] +
                  (1 - $P) * $dp[$i - 3];

    return $dp[$N];
}

// Driver code
$n = 5;
$p = 0.2;
echo find_prob($n, $p);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find probability to
// reach N with P probability to take
// 2 steps (1-P) to take 3 steps

   // Returns probability to reach N
    function find_prob(N, P)
    {
        let dp = [];
        dp[0] = 1;
        dp[1] = 0;
        dp[2] = P;
        dp[3] = 1 - P;

        for (let i = 4; i <= N; ++i)
          dp[i] = (P) * dp[i - 2] +
                        (1 - P) * dp[i - 3];

        return (dp[N]);
    }

// Driver Code
        let n = 5;
        let p = 0.2;
        document.write(find_prob(n, p));

      // This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
0.32
```