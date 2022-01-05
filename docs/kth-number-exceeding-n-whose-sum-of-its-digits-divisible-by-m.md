# 超过 N 的第 k 个数，其位数之和可被 M 整除

> 原文:[https://www . geesforgeks . org/kth-number-exclusive-n-其位数之和可被 m 整除/](https://www.geeksforgeeks.org/kth-number-exceeding-n-whose-sum-of-its-digits-divisible-by-m/)

给定整数 **N** 、 **K** 和 **M** ，任务是找到大于 **N** 的 **K <sup>th</sup>** 数，其[位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)可被 **M** 整除。

**示例:**

> **输入:** N = 6，K = 5，M = 5
> **输出:** 32
> **说明:**
> 大于 N = 6 且其位数之和可被 5 整除的数为{14，19，23，28，32，…}。第 K <sup>个</sup>号，即第 5 个<sup>个</sup>号为 32。
> 
> **输入:** N = 40，K = 4，M = 5
> **输出:** 55
> **说明:**
> 大于 N = 40 且其位数之和可被 5 整除的数为{41，46，50，55，…}。第 K <sup>个</sup>号，即第 4 个<sup>个</sup>号为 55。

**简单方法:**最简单的方法是检查每个大于 **N** 的数字，如果其数字的[和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)可被 **M** 整除，则将计数器增加 **1** 。继续检查数字，直到计数器等于 **K** 。

***时间复杂度:** O(K)*
***辅助空间:** O(1)*

**高效方法:**思路是使用[**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) 和 [**二分搜索法**](https://www.geeksforgeeks.org/binary-search/) 。按照以下步骤解决问题:

*   首先创建一个[递归记忆函数](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)，求小于等于 **S** 的整数总数，其位数之和可被 **M** 整除，如下图:

> dp 过渡将是:
> 
> **dp(S，指数，和，紧，M) = dp(指数+1，(和+i)%M，紧，M)** 其中，
> 
> *   **S** 给出了一个极限，对于这个极限，需要找到所有小于或等于 S 且位数之和可被 M 整除的数。
> *   **索引**是当前需要放置一个数字的索引。
> *   **求和**取 0 到 4 之间的值。
> *   基本条件是，如果索引变得大于 S 的长度，并且总和可被 M 整除，则返回 1。
> *   **M** 为除数。
> 
> 如果前面的数字已经被放置成小于 S，那么
> 
> *   **紧**将变为等于 0。
> *   **i** 将从 0 迭代到 9。
> 
> 如果前面所有的数字都与 S 中相应的数字匹配，那么
> 
> *   **紧**会变成 1，表示这个数字仍然没有变得小于 s。
> *   **i** 将从 0 迭代到数字 S【索引】。

*   现在使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，其中下限为 **N+1** ，上限为某个大整数。
*   初始化一个变量**左侧**，用于存储小于或等于 **N** 的总数，其位数之和可被 **M** 整除。
*   求下限和上限的中点，然后用上述 dp 函数求小于或等于中点且位数之和可被 **M** 整除的数。顺其自然**对**。
*   如果**左+ K** 等于**右**，则将答案更新为中间，并将上限设置为**中点–1**。
*   否则，如果**左+ K** 小于右，则将上限设置为**中点-1** 。
*   如果**左+ K** 大于右，则将下限设置为**中点+1** 。
*   重复上述步骤，同时下限小于或等于上限。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Initialize dp array
int dp[100000][100][2];

// Function to find the numbers <= S
// having digits sum divisible by M
int solve(string s, int index, int sum,
                    int tight, int z)
{

    // Base Case
    if (index >= s.size())
    {
        if (sum % z == 0)
            return 1;

        return 0;
    }

    // Visited state
    if (dp[index][sum][tight] != -1)
        return dp[index][sum][tight];

    // Store answer
    int ans = 0;

    // If number still does not
    // become smaller than S
    if (tight == 1)
    {

        // Find limit
        int l = s[index] - '0';

        // Iterate through all
        // the digits
        for(int i = 0; i <= l; i++)
        {

            // If current digit is limit
            if (i == l)
            {
                ans += solve(s, index + 1,
                                 (sum + i) % z, 1, z);
            }

            // Number becomes smaller than S
            else {
                ans += solve(s, index + 1,
                                 (sum + i) % z, 0, z);
            }
        }
    }
    else
    {

        // If number already becomes
        // smaller than S
        for(int i = 0; i <= 9; i++)
            ans += solve(s, index + 1,
                             (sum + i) % z, 0, z);
    }

    // Return and store the answer
    // for the current state
    return dp[index][sum][tight] = ans;
}

// Function to find the Kth number
// > N whose sum of the digits is
// divisible by M
int search(int n, int k, int z)
{

    // Initialize lower limit
    int low = n + 1;

    // Initialize upper limit
    int high = 1e9;

    // Mask dp states unvisited
    memset(dp, -1, sizeof(dp));

    // Numbers <= N except 0 with
    // digits sum divisible by M
    int left = solve(to_string(n),
                     0, 0, 1, z) - 1;

    // Initialize answer with -1
    int ans = -1;
    while (low <= high)
    {

        // Calculate mid
        int mid = low + (high - low) / 2;

        // Mark dp states unvisited
        memset(dp, -1, sizeof(dp));

        // Numbers < mid with digits
        // sum divisible by M
        int right = solve(to_string(mid),
                          0, 0, 1, z) - 1;

        // If the current mid is
        // satisfy the condition
        if (left + k == right)
        {

            // Might be the answer
            ans = mid;

            // Update upper limit
            high = mid - 1;
        }
        else if (left + k < right)
        {

            // Update upper limit
            high = mid - 1;
        }
        else
        {

            // Update lower limit
            low = mid + 1;
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{

    // Given N, K, and M
    int N = 40;
    int K = 4;
    int M = 2;

    // Function Call
    cout << search(N, K, M) << endl;
}

// This code is contributed by bolliranadheer
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
public class Main {

    static int dp[][][];

    // Function to find the Kth number
    // > N whose sum of the digits is
    // divisible by M
    public static int search(
        int n, int k, int z)
    {

        // Initialize dp array
        dp = new int[100000 + 1][z][2];

        // Initialize lower limit
        int low = n + 1;

        // Initialize upper limit
        int high = Integer.MAX_VALUE / 2;

        // Mask dp states unvisited
        clear();

        // Numbers <= N except 0 with
        // digits sum divisible by M
        int left = solve(n + "", 0,
                         0, 1, z)
                   - 1;

        // Initialize answer with -1
        int ans = -1;
        while (low <= high) {

            // Calculate mid
            int mid = low + (high - low) / 2;

            // Mark dp states unvisited
            clear();

            // Numbers < mid with digits
            // sum divisible by M
            int right = solve(mid + "", 0,
                              0, 1, z)
                        - 1;

            // If the current mid is
            // satisfy the condition
            if (left + k == right) {

                // Might be the answer
                ans = mid;

                // Update upper limit
                high = mid - 1;
            }
            else if (left + k < right) {

                // Update upper limit
                high = mid - 1;
            }
            else {

                // Update lower limit
                low = mid + 1;
            }
        }

        // Return the answer
        return ans;
    }

    // Function to find the numbers <= S
    // having digits sum divisible by M
    public static int solve(
        String s, int index, int sum,
        int tight, int z)
    {
        // Base Case
        if (index >= s.length()) {
            if (sum % z == 0)
                return 1;
            return 0;
        }

        // Visited state
        if (dp[index][sum][tight] != -1)
            return dp[index][sum][tight];

        // Store answer
        int ans = 0;

        // If number still does not
        // become smaller than S
        if (tight == 1) {

            // Find limit
            int l = s.charAt(index) - '0';

            // Iterate through all
            // the digits
            for (int i = 0; i <= l; i++) {

                // If current digit is limit
                if (i == l) {
                    ans += solve(s, index + 1,
                                 (sum + i) % z,
                                 1, z);
                }

                // Number becomes smaller than S
                else {
                    ans += solve(s, index + 1,
                                 (sum + i) % z,
                                 0, z);
                }
            }
        }
        else {

            // If number already becomes
            // smaller than S
            for (int i = 0; i <= 9; i++)
                ans += solve(s, index + 1,
                             (sum + i) % z, 0,
                             z);
        }

        // Return and store the answer
        // for the current state
        return dp[index][sum][tight] = ans;
    }

    // Function to clear the states
    public static void clear()
    {
        for (int i[][] : dp) {
            for (int j[] : i)
                Arrays.fill(j, -1);
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given N, K, and M
        int N = 40;
        int K = 4;
        int M = 2;

        // Function Call
        System.out.println(search(N, K, M));
    }
}
```

## 蟒蛇 3

```
# Python program for the
# above approach

# Initialize dp array
dp = [[[]]]

# Function to find the
# numbers <= S having
# digits sum divisible
# by M
def solve(s, index,
          sum,tight, z):

    # Base Case
    if (index >= len(s)):   
        if (sum % z == 0):
            return 1

        return 0

    # Visited state
    if (dp[index][sum][tight] != -1):
        return dp[index][sum][tight]

    # Store answer
    ans = 0

    # If number still does not
    # become smaller than S
    if(tight == 1):

        # Find limit
        l = int(ord(s[index]) -
                ord('0'))

        # Iterate through all
        # the digits
        for i in range(0, l + 1):

            # If current digit is
            # limit
            if (i == l):

                ans += solve(s, index + 1,
                            (sum + i) % z,
                             1, z)

            # Number becomes smaller
            # than S
            else:
                ans += solve(s, index + 1,
                            (sum + i) % z,
                             0, z)

    else:

        # If number already becomes
        # smaller than S
        for i in range(0,10):

            ans += solve(s, index + 1,
                        (sum + i) % z,
                         0, z)

    # Return and store the answer
    # for the current state
    dp[index][sum][tight] = ans
    return ans

# Function to find the Kth number
# > N whose sum of the digits is
# divisible by M
def search(n, k, z):

    global dp
    dp = [[[-1, -1] for j in range(z)]
                    for i in range(100001)]

    # Initialize lower limit
    low = n + 1

    # Initialize upper limit
    high = 1000000009

    # Numbers <= N except 0 with
    # digits sum divisible by M
    left = solve(str(n), 0,
                 0, 1, z) - 1

    # Initialize answer with -1
    ans = -1
    while (low <= high):

        # Calculate mid
        mid = low + (high -
                     low) // 2

        # Mark dp states unvisited
        dp = [[[-1, -1] for j in range(z)]
                        for i in range(100000)]

        # Numbers < mid with digits
        # sum divisible by M
        right = solve(str(mid), 0,
                      0, 1, z) - 1

        # If the current mid is
        # satisfy the condition
        if (left + k == right):

            # Might be the answer
            ans = mid

            # Update upper limit
            high = mid - 1

        elif (left + k < right):

            # Update upper limit
            high = mid - 1

        else:

            # Update lower limit
            low = mid + 1

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    # Given N, K, and M
    N = 40
    K = 4
    M = 2

    # Function Call
    print(search(N, K, M))

# This code is contributed by Rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int [,,]dp;

// Function to find the Kth number
// > N whose sum of the digits is
// divisible by M
public static int search(int n, int k,
                         int z)
{

    // Initialize dp array
    dp = new int[100000 + 1, z, 2];

    // Initialize lower limit
    int low = n + 1;

    // Initialize upper limit
    int high = int.MaxValue / 2;

    // Mask dp states unvisited
    Clear(z);

    // Numbers <= N except 0 with
    // digits sum divisible by M
    int left = solve(n + "", 0,
                     0, 1, z) - 1;

    // Initialize answer with -1
    int ans = -1;
    while (low <= high)
    {

        // Calculate mid
        int mid = low + (high - low) / 2;

        // Mark dp states unvisited
        Clear(z);

        // Numbers < mid with digits
        // sum divisible by M
        int right = solve(mid + "", 0,
                          0, 1, z) - 1;

        // If the current mid is
        // satisfy the condition
        if (left + k == right)
        {

            // Might be the answer
            ans = mid;

            // Update upper limit
            high = mid - 1;
        }
        else if (left + k < right)
        {

            // Update upper limit
            high = mid - 1;
        }
        else
        {

            // Update lower limit
            low = mid + 1;
        }
    }

    // Return the answer
    return ans;
}

// Function to find the numbers <= S
// having digits sum divisible by M
public static int solve(String s, int index,
                        int sum, int tight,
                        int z)
{

    // Base Case
    if (index >= s.Length)
    {
        if (sum % z == 0)
            return 1;

        return 0;
    }

    // Visited state
    if (dp[index, sum, tight] != -1)
        return dp[index, sum, tight];

    // Store answer
    int ans = 0;

    // If number still does not
    // become smaller than S
    if (tight == 1)
    {

        // Find limit
        int l = s[index] - '0';

        // Iterate through all
        // the digits
        for(int i = 0; i <= l; i++)
        {

            // If current digit is limit
            if (i == l)
            {
                ans += solve(s, index + 1,
                            (sum + i) % z,
                             1, z);
            }

            // Number becomes smaller than S
            else
            {
                ans += solve(s, index + 1,
                            (sum + i) % z,
                             0, z);
            }
        }
    }
    else
    {

        // If number already becomes
        // smaller than S
        for(int i = 0; i <= 9; i++)
            ans += solve(s, index + 1,
                        (sum + i) % z, 0,
                         z);
    }

    // Return and store the answer
    // for the current state
    return dp[index, sum, tight] = ans;
}

// Function to clear the states
public static void Clear(int z)
{
    for(int i = 0; i < 100001; i++)
    {
        for(int j = 0; j < z; j++)
        {
            for(int l = 0; l < 2; l++)
                dp[i, j, l] = -1;
        }
    }
}

// Driver Code
public static void Main(String []args)
{

    // Given N, K, and M
    int N = 40;
    int K = 4;
    int M = 2;

    // Function Call
    Console.WriteLine(search(N, K, M));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let dp;

// Function to find the Kth number
    // > N whose sum of the digits is
    // divisible by M
function search(n,k,z)
{
    // Initialize dp array
        dp = new Array(100000 + 1);
        for(let i=0;i<100000+1;i++)
        {
            dp[i]=new Array(z);
            for(let j=0;j<z;j++)
            {
                dp[i][j]=new Array(2);
            }
        }

        // Initialize lower limit
        let low = n + 1;

        // Initialize upper limit
        let high = Math.floor(Number.MAX_VALUE / 2);

        // Mask dp states unvisited
        clear();

        // Numbers <= N except 0 with
        // digits sum divisible by M
        let left = solve(n + "", 0,
                         0, 1, z)
                   - 1;

        // Initialize answer with -1
        let ans = -1;
        while (low <= high) {

            // Calculate mid
            let mid = low + Math.floor((high - low) / 2);

            // Mark dp states unvisited
            clear();

            // Numbers < mid with digits
            // sum divisible by M
            let right = solve(mid + "", 0,
                              0, 1, z)
                        - 1;

            // If the current mid is
            // satisfy the condition
            if (left + k == right) {

                // Might be the answer
                ans = mid;

                // Update upper limit
                high = mid - 1;
            }
            else if (left + k < right) {

                // Update upper limit
                high = mid - 1;
            }
            else {

                // Update lower limit
                low = mid + 1;
            }
        }

        // Return the answer
        return ans;
}

// Function to find the numbers <= S
    // having digits sum divisible by M
function solve(s,index,sum,tight,z)
{
    // Base Case
        if (index >= s.length) {
            if (sum % z == 0)
                return 1;
            return 0;
        }

        // Visited state
        if (dp[index][sum][tight] != -1)
            return dp[index][sum][tight];

        // Store answer
        let ans = 0;

        // If number still does not
        // become smaller than S
        if (tight == 1) {

            // Find limit
            let l = s[index].charCodeAt(0) - '0'.charCodeAt(0);

            // Iterate through all
            // the digits
            for (let i = 0; i <= l; i++) {

                // If current digit is limit
                if (i == l) {
                    ans += solve(s, index + 1,
                                 (sum + i) % z,
                                 1, z);
                }

                // Number becomes smaller than S
                else {
                    ans += solve(s, index + 1,
                                 (sum + i) % z,
                                 0, z);
                }
            }
        }
        else {

            // If number already becomes
            // smaller than S
            for (let i = 0; i <= 9; i++)
                ans += solve(s, index + 1,
                             (sum + i) % z, 0,
                             z);
        }

        // Return and store the answer
        // for the current state
        return dp[index][sum][tight] = ans;
}

// Function to clear the states
function clear()
{
    for(let i=0;i<dp.length;i++)
    {
        for(let j=0;j<dp[i].length;j++)
        {
            for(let k=0;k<dp[i][j].length;k++)
            {
                dp[i][j][k]=-1;
            }
        }
    }
}

// Driver Code
// Given N, K, and M
let N = 40;
let K = 4;
let M = 2;

// Function Call
document.write(search(N, K, M)+"<br>");

// This code is contributed by patel2127
</script>
```

**Output**

```
48
```

***时间复杂度:**O(log(INT _ MAX))*
***辅助空间:** O(K * M * log(INT_MAX))*