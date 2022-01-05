# 找出从 1 到 N 正好包含 k 个非零数字的数字

> 原文:[https://www . geesforgeks . org/find-the-numbers-from-1-to-n-the-to-the-the-the-numbers-from-1-1-n-1-n-1-n-1-n-1-1-n-1-n-1-n-1-n-1-1-1-1-1](https://www.geeksforgeeks.org/find-the-numbers-from-1-to-n-that-contains-exactly-k-non-zero-digits/)

**先决条件:** [动态编程](http://www.geeksforgeeks.org/dynamic-programming/)、 [DigitDP](https://www.geeksforgeeks.org/digit-dp-introduction/)
给定两个整数 **N** 和 **K** 。任务是找出 **1** 和 **N** (含)之间的整数个数，当以十为基数书写时正好包含 **K** 个非零数字。

**示例:**

> **输入:** N = 100，K = 1
> **输出:** 19
> **说明:**
> 1 到 100 之间正好有 1 个非零数字的数字是:
> 1、2、3、4、5、6、7、8、9、
> 10、20、30、40、50、60、70、80、90、100
> 
> **输入:** N = 25，K = 2
> **输出:** 14
> **说明:**
> 1 到 25 之间正好有 2 个非零数字的数字是:
> 11、12、13、14、15、16、17、
> 18、19、21、22、23、24、25

**方法:**考虑 **N** 位的整数就够了，必要时用 **0** 填充高位。这个问题可以通过应用名为[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/) 的方法来解决。

*   **dp[i][0][j]** =较高的 **i** 位数已经确定，有 **j** 非零位数，已经确定小于 **N** 。
*   **dp[i][1][j]** =较高的 **i** 位数已经确定，有 **j** 非零位数，尚未确定小于 **N** 。

计算上述 dp 后，期望的答案为 **dp[L][0][K] + dp[L][1][K]** ，其中 **L** 为 **N** 的位数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number less than N
// having k non-zero digits
int k_nonzero_numbers(string s, int n, int k)
{
    // Store the memorised values
    int dp[n + 1][2][k + 1];

    // Initialise
    for (int i = 0; i <= n; i++)
        for (int j = 0; j < 2; j++)
            for (int x = 0; x <= k; x++)
                dp[i][j][x] = 0;

    // Base
    dp[0][0][0] = 1;

    // Calculate all states
    // For every state, from numbers 1 to N,
    // the count of numbers which contain exactly j
    // non zero digits is being computed and updated
    // in the dp array.
    for (int i = 0; i < n; ++i) {
        int sm = 0;
        while (sm < 2) {
            for (int j = 0; j < k + 1; ++j) {
                int x = 0;
                while (x <= (sm ? 9 : s[i] - '0')) {
                    dp[i + 1][sm || x < (s[i] - '0')][j + (x > 0)]
                        += dp[i][sm][j];
                    ++x;
                }
            }
            ++sm;
        }
    }

    // Return the required answer
    return dp[n][0][k] + dp[n][1][k];
}

// Driver code
int main()
{
    string s = "25";

    int k = 2;

    int n = s.size();

    // Function call
    cout << k_nonzero_numbers(s, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class Geeks{

// Function to find number less than N
// having k non-zero digits
static int k_nonzero_numbers(String s, int n, int k)
{

    // Store the memorised values
    int dp[][][] = new int[n + 1][2][k + 1];

    // Initialise
    for(int i = 0; i <= n; i++)
        for(int j = 0; j < 2; j++)
            for(int x = 0; x <= k; x++)
                dp[i][j][x] = 0;

    // Base
    dp[0][0][0] = 1;

    // Calculate all states
    // For every state, from numbers 1 to N,
    // the count of numbers which contain exactly j
    // non zero digits is being computed and updated
    // in the dp array.
    for(int i = 0; i < n; ++i)
    {
        int sm = 0;
        while (sm < 2)
        {
            for(int j = 0; j < k + 1; ++j)
            {
                int x = 0;
                while (x <= (sm !=
                       0 ? 9 :s.charAt(i) - '0'))
                {
                    if (j + (x > 0 ? 1 : 0) < k + 1)
                    {
                        dp[i + 1][(sm != 0 || x <
                                  (s.charAt(i) - '0')) ?
                                   1 : 0][j + (x > 0 ?
                                   1 : 0)] += dp[i][sm][j];
                    }
                    ++x;
                }
            }
            ++sm;
        }
    }

    // Return the required answer
    return dp[n][0][k] + dp[n][1][k];
}

// Driver code
public static void main(String[] args)
{
    String s = "25";

    int k = 2;

    int n = s.length();

    // Function call
    System.out.println(k_nonzero_numbers(s, n, k));
}
}

// This code is contributed by Rajnis09
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find number less than N
# having k non-zero digits
def k_nonzero_numbers(s, n, k):

    # Store the memorised values
    dp = [[[ 0 for i in range(k + 2)]
               for i in range(2)]
               for i in range(n + 2)]

    # Initialise
    for i in range(n + 1):
        for j in range(2):
            for x in range(k + 1):
                dp[i][j][x] = 0

    # Base
    dp[0][0][0] = 1

    # Calculate all states
    # For every state, from numbers 1 to N,
    # the count of numbers which contain
    # exactly j non zero digits is being
    # computed and updated in the dp array.
    for i in range(n):
        sm = 0

        while (sm < 2):
            for j in range(k + 1):
                x = 0
                y = 0
                if sm:
                    y = 9
                else:
                    y = ord(s[i]) - ord('0')

                while (x <= y):
                    dp[i + 1][(sm or x < (
                    ord(s[i]) - ord('0')))][j +
                     (x > 0)] += dp[i][sm][j]
                    x += 1

            sm += 1

    # Return the required answer
    return dp[n][0][k] + dp[n][1][k]

# Driver code
if __name__ == '__main__':

    s = "25"

    k = 2

    n = len(s)

    # Function call
    print(k_nonzero_numbers(s, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG{

// Function to find number less than N
// having k non-zero digits
static int k_nonzero_numbers(string s, int n,
                                       int k)
{

    // Store the memorised values
    int [,,]dp = new int[n + 1, 2, k + 1];

    // Initialise
    for(int i = 0; i <= n; i++)
        for(int j = 0; j < 2; j++)
            for(int x = 0; x <= k; x++)
                dp[i, j, x] = 0;

    // Base
    dp[0, 0, 0] = 1;

    // Calculate all states
    // For every state, from numbers 1 to N,
    // the count of numbers which contain exactly j
    // non zero digits is being computed and updated
    // in the dp array.
    for(int i = 0; i < n; ++i)
    {
        int sm = 0;
        while (sm < 2)
        {
            for(int j = 0; j < k + 1; ++j)
            {
                int x = 0;
                while (x <= (sm !=
                       0 ? 9 : s[i]- '0'))
                {
                    if (j + (x > 0 ? 1 : 0) < k + 1)
                    {
                        dp[i + 1, ((sm != 0 || x <
                        (s[i] - '0')) ? 1 : 0),
                           j + (x > 0 ? 1 : 0)] +=
                         dp[i, sm, j];
                    }
                    ++x;
                }
            }
            ++sm;
        }
    }

    // Return the required answer
    return dp[n, 0, k] + dp[n, 1, k];
}

// Driver code
public static void Main(string[] args)
{
    string s = "25";
    int k = 2;
    int n = s.Length;

    // Function call
    Console.Write(k_nonzero_numbers(s, n, k));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find number less than N
// having k non-zero digits
function k_nonzero_numbers(s,n,k)
{
    // Store the memorised values
    let dp = new Array(n + 1);

    // Initialise
    for(let i = 0; i <= n; i++)
    {
        dp[i]=new Array(2);
        for(let j = 0; j < 2; j++)
        {
            dp[i][j] = new Array(k+1);
            for(let x = 0; x <= k; x++)
                dp[i][j][x] = 0;
        }
    }

    // Base
    dp[0][0][0] = 1;

    // Calculate all states
    // For every state, from numbers 1 to N,
    // the count of numbers which contain exactly j
    // non zero digits is being computed and updated
    // in the dp array.
    for(let i = 0; i < n; ++i)
    {
        let sm = 0;
        while (sm < 2)
        {
            for(let j = 0; j < k + 1; ++j)
            {
                let x = 0;
                while (x <= (sm !=
                       0 ? 9 :s[i].charCodeAt(0) - '0'.charCodeAt(0)))
                {
                    if (j + (x > 0 ? 1 : 0) < k + 1)
                    {
                        dp[i + 1][(sm != 0 || x <
                                  (s[i].charCodeAt(0) - '0'.charCodeAt(0))) ?
                                   1 : 0][j + (x > 0 ?
                                   1 : 0)] += dp[i][sm][j];
                    }
                    ++x;
                }
            }
            ++sm;
        }
    }

    // Return the required answer
    return dp[n][0][k] + dp[n][1][k];
}

// Driver code
let s = "25";

let k = 2;
let n = s.length;

// Function call
document.write(k_nonzero_numbers(s, n, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
14
```

**时间复杂度:** O(LK)，其中 L 为 n 中的位数

**辅助空间:** O(N * K * 2)
**注:**用于计算状态的两个 for 循环分别从[0，1]和[0，9]被认为是常数乘法。