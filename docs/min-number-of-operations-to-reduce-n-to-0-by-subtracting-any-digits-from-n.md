# 通过从 N 中减去任意数字将 N 减少到 0 的最小操作次数

> 原文:[https://www . geesforgeks . org/min-通过从 n 中减去任意数字将 n 减少到 0 的操作数/](https://www.geeksforgeeks.org/min-number-of-operations-to-reduce-n-to-0-by-subtracting-any-digits-from-n/)

给定一个数字 **N** ，任务是通过将给定的数字减去其中的任意一个数字，找到将数字 **N** 减少到零所需的最小操作数。

**示例:**

> **输入:** N = 4
> **输出:** 1
> **解释:**
> 这里 4 是唯一出现的数字，因此 4–4 = 0，只需要一次操作。
> 
> **输入:** N = 17
> **输出:** 3
> **说明:**
> 给定整数为 17，归约步骤为:
> 17->17–7 = 10
> 10->10–1 = 9
> 9->9–9 = 0。
> 因此需要 3 次操作。

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。
对于任何给定的数字 **N** ，遍历 **N** 中的每个数字，并通过逐个减去每个数字进行递归检查，直到 **N 减少到 0** 。但是执行[递归](https://www.geeksforgeeks.org/recursion/)将使该方法的时间复杂度呈指数增长。
因此，想法是使用大小为 **(N + 1)** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)(比如 **dp[]** )，这样 **dp[i]** 将存储将 **i 减少到 0** 所需的最小操作数。

对于数字 **N** 中的每一个数字 **x** ，所用的递推关系由下式给出:

> dp[i] = min(dp[i]，dp[i-x] + 1)，
> ，其中 dp[i]将存储将 **i 减少到 0** 所需的最小操作数。

我们将使用**自下而上的方法**将数组 **dp[]** 从 **0 填充到**N，然后 **dp[N]** 将给出 **N** 的最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to reduce an integer N
// to Zero in minimum operations by
// removing digits from N
int reduceZero(int N)
{
    // Initialise dp[] to steps
    vector<int> dp(N + 1, 1e9);

    dp[0] = 0;

    // Iterate for all elements
    for (int i = 0; i <= N; i++) {

        // For each digit in number i
        for (char c : to_string(i)) {

            // Either select the number
            // or do not select it
            dp[i] = min(dp[i],
                        dp[i - (c - '0')]
                            + 1);
        }
    }

    // dp[N] will give minimum
    // step for N
    return dp[N];
}

// Driver Code
int main()
{
    // Given Number
    int N = 25;

    // Function Call
    cout << reduceZero(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to reduce an integer N
// to Zero in minimum operations by
// removing digits from N
static int reduceZero(int N)
{
    // Initialise dp[] to steps
    int []dp = new int[N + 1];
    for (int i = 0; i <= N; i++)
        dp[i] = (int) 1e9;
    dp[0] = 0;

    // Iterate for all elements
    for (int i = 0; i <= N; i++)
    {

        // For each digit in number i
        for (char c : String.valueOf(i).toCharArray())
        {

            // Either select the number
            // or do not select it
            dp[i] = Math.min(dp[i],
                             dp[i - (c - '0')] + 1);
        }
    }

    // dp[N] will give minimum
    // step for N
    return dp[N];
}

// Driver Code
public static void main(String[] args)
{
    // Given Number
    int N = 25;

    // Function Call
    System.out.print(reduceZero(N));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to reduce an integer N
# to Zero in minimum operations by
# removing digits from N
def reduceZero(N):

    # Initialise dp[] to steps
    dp = [1e9 for i in range(N + 1)]

    dp[0] = 0

    # Iterate for all elements
    for i in range(N + 1):

        # For each digit in number i
        for c in str(i):

            # Either select the number
            # or do not select it
            dp[i] = min(dp[i],
                        dp[i - (ord(c) - 48)] + 1)

    # dp[N] will give minimum
    # step for N
    return dp[N]

# Driver Code
N = 25

# Function Call
print(reduceZero(N))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to reduce an integer N
// to Zero in minimum operations by
// removing digits from N
static int reduceZero(int N)
{
    // Initialise []dp to steps
    int []dp = new int[N + 1];
    for (int i = 0; i <= N; i++)
        dp[i] = (int) 1e9;
    dp[0] = 0;

    // Iterate for all elements
    for (int i = 0; i <= N; i++)
    {

        // For each digit in number i
        foreach (char c in String.Join("", i).ToCharArray())
        {

            // Either select the number
            // or do not select it
            dp[i] = Math.Min(dp[i],
                             dp[i - (c - '0')] + 1);
        }
    }

    // dp[N] will give minimum
    // step for N
    return dp[N];
}

// Driver Code
public static void Main(String[] args)
{
    // Given Number
    int N = 25;

    // Function Call
    Console.Write(reduceZero(N));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to reduce an integer N
// to Zero in minimum operations by
// removing digits from N
function reduceZero(N)
{
    // Initialise dp[] to steps
    var dp = Array(N + 1).fill(1000000000);

    dp[0] = 0;

    // Iterate for all elements
    for (var i = 0; i <= N; i++) {

        // For each digit in number i
        for (var j =0; j< i.toString().length; j++)
        {
            // Either select the number
            // or do not select it
            dp[i] = Math.min(dp[i],
                        dp[i - (i.toString()[j] - '0')]
                            + 1);
        }
    }

    // dp[N] will give minimum
    // step for N
    return dp[N];
}

// Driver Code

// Given Number
var N = 25;

// Function Call
document.write( reduceZero(N));

</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*