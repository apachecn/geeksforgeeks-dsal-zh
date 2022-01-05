# 在 M 名学生中分发 N 套试卷的方式数量

> 原文:[https://www . geeksforgeeks . org/在 m 学生中分发 n 套纸张的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-distribute-n-paper-set-among-m-students/)

给定 **N** 个学生，共 **M** 套试卷，其中 **M ≤ N** 。所有的 **M** 套都不一样，每套都有足够的数量。所有的学生都坐在一排。任务是找到分发试卷的方法，这样如果有任何 **M** 连续的学生被选中，那么每个学生都有一个独特的试卷集。答案可能很大，所以以 **10 <sup>9</sup> + 7** 为模打印答案。
**例:**

> **输入:** N = 2，M = 2
> T3】输出: 2
> (A，B)和(B，A)是唯一可能的方式。
> **输入:** N = 15，M = 4
> **输出:** 24

**进路:**可以观察到进路数与 **N** 无关，只依赖于 **M** 。先给 **M** 的学生发 **M** 套，然后重复同样的花样。这样分发试题纸的方式数量是 **M！**。例如

> N = 6，M = 3
> A、B、C、A、B、C
> A、C、B、A、C、B
> B、C、A、B、C、A
> B、A、C、B、A、C
> C、A、B、C、A、B
> C、B、A、C、B、A

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = 1000000007;

// Function to return n! % 1000000007
int factMod(int n)
{

    // To store the factorial
    long fact = 1;

    // Find the factorial
    for (int i = 2; i <= n; i++) {
        fact *= (i % MOD);
        fact %= MOD;
    }

    return fact;
}

// Function to return the
// count of possible ways
int countWays(int n, int m)
{
    return factMod(m);
}

// Driver code
int main()
{
    int n = 2, m = 2;

    cout << countWays(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MOD = 1000000007;

// Function to return n! % 1000000007
static int factMod(int n)
{

    // To store the factorial
    long fact = 1;

    // Find the factorial
    for (int i = 2; i <= n; i++)
    {
        fact *= (i % MOD);
        fact %= MOD;
    }
    return (int)fact;
}

// Function to return the
// count of possible ways
static int countWays(int n, int m)
{
    return factMod(m);
}

// Driver code
public static void main(String args[])
{
    int n = 2, m = 2;

    System.out.print(countWays(n, m));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MOD = 1000000007;

# Function to return n! % 1000000007
def factMod(n) :

    # To store the factorial
    fact = 1;

    # Find the factorial
    for i in range(2, n + 1) :
        fact *= (i % MOD);
        fact %= MOD;

    return fact;

# Function to return the
# count of possible ways
def countWays(n, m) :

    return factMod(m);

# Driver code
if __name__ == "__main__" :

    n = 2; m = 2;

    print(countWays(n, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MOD = 1000000007;

    // Function to return n! % 1000000007
    static int factMod(int n)
    {
        // To store the factorial
        int fact = 1;

        // Find the factorial
        for (int i = 2; i <= n; i++)
        {
            fact *= (i % MOD);
            fact %= MOD;
        }
        return fact;
    }

    // Function to return the
    // count of possible ways
    static int countWays(int n, int m)
    {
        return factMod(m);
    }

    // Driver code
    public static void Main()
    {
        int n = 2, m = 2;
        Console.Write(countWays(n, m));
    }
}

// This code is contributed by Sanjit Prasad
```

## java 描述语言

```
<script>
// javascript implementation of the approach
     MOD = 1000000007;

    // Function to return n! % 1000000007
    function factMod(n) {

        // To store the factorial
        var fact = 1;

        // Find the factorial
        for (i = 2; i <= n; i++) {
            fact *= (i % MOD);
            fact %= MOD;
        }
        return parseInt( fact);
    }

    // Function to return the
    // count of possible ways
    function countWays(n , m) {
        return factMod(m);
    }

    // Driver code

        var n = 2, m = 2;

        document.write(countWays(n, m));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
2
```