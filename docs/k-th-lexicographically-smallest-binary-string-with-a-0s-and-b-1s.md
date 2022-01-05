# 第 K 个字母顺序最小的二进制串，带有 A0 和 B1

> 原文:[https://www . geeksforgeeks . org/k-th-按字典顺序排列-最小-二进制-带-a-0s 和-b-1s 的字符串/](https://www.geeksforgeeks.org/k-th-lexicographically-smallest-binary-string-with-a-0s-and-b-1s/)

给定三个正整数 **A** 、 **B** 和 **K** ，任务是找到 **K <sup>第</sup>个按字典顺序最小的** [**二进制字符串**](https://www.geeksforgeeks.org/tag/binary-string/) ，该字符串恰好包含 **0s** 的 **A** 数和 **B** 的 **1s** 数。

**示例:**

> **输入:** A = 2，B = 2，K = 4
> **输出:** 1001
> **说明:**字符串的字典顺序为 0011，0101，0110，1001。
> 
> **输入:** A = 3，B = 3，K = 7
> T3】输出: 010110

**方法:**上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。请按照以下步骤解决此问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **dp[][]** ，使得 **dp[i][j]** 用 **i** 数 **0s** 和 **j** 数 **1s** 来表示二进制字符串的总数。
*   除了表示空字符串的 **dp[0][0] = 1** 之外，所有 dp 表值最初都用零填充。
*   现在， **dp[i][j]** 可以计算为以 **0** 结尾的字符串总数(使用 dp 状态作为**dp[I–1][j]**)和以 1 结尾的字符串总数(使用 DP 状态作为**DP[I][j–1]**)之和。因此，当前 dp 状态计算为**DP[I][j]= DP[I–1][j]+DP[I][j–1]**。
*   填充此 dp 表后，可使用[递归函数](https://www.geeksforgeeks.org/recursive-functions/)计算第 K 个<sup>字典最小二进制字符串。</sup>
*   因此，定义一个函数 **KthString** ，该函数具有参数 **A、B、K** 和 **dp** 。
*   现在，在这个递归函数的每次调用中:
    *   如果 **dp[A][B]的值至少为 K** ，则在第 K 个字典最小二进制字符串中的该位置只能出现“0”，然后递归调用状态**(A–1，B)** 的函数。
    *   否则“1”出现在这里，递归调用状态 **(A，B–1)**的函数。
*   根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Recursive function to find the Kth
// smallest binary string
string KthString(int A, int B, long long K,
                 vector<vector<int> >& dp)
{
    // Base Case
    if (A == 0) {

        // Return string of all 1's
        // of length B
        return string(B, '1');
    }
    if (B == 0) {

        // Return string of all 0's
        // of length A
        return string(A, '0');
    }

    if (K <= dp[A - 1][B]) {
        return "0" + KthString(
                         A - 1, B, K, dp);
    }

    else {
        return "1"
               + KthString(
                     A, B - 1,
                     K - dp[A - 1][B], dp);
    }
}

// Function to find the Kth lexicographically
// smallest binary string with exactly
// A zeroes and B ones
int KthStringUtil(int A, int B, int K)
{
    // Stores the recurring states
    vector<vector<int> > dp(
        A + 1, vector<int>(B + 1));

    // Calculate the dp values iteratively
    dp[0][0] = 1;
    for (int i = 0; i <= A; ++i) {
        for (int j = 0; j <= B; ++j) {

            if (i > 0) {

                // The last character was '0'
                dp[i][j] += dp[i - 1][j];
            }
            if (j > 0) {

                // The last character was '1'
                dp[i][j] += dp[i][j - 1];
            }
        }
    }

    // Print the binary string obtained
    cout << KthString(A, B, K, dp);

    return 0;
}

// Driver Code
int main()
{
    int A = 3, B = 3, K = 7;
    KthStringUtil(A, B, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Recursive function to find the Kth
    // smallest binary string
    static String KthString(int A, int B, long K, int[][] dp)
    {

        // Base Case
        if (A == 0) {

            // Return string of all 1's
            // of length B
            String ans = "";
            for (int i = 0; i < B; i++) {
                ans += '1';
            }
            return ans;
        }
        if (B == 0) {

            // Return string of all 0's
            // of length A
            String ans = "";
            for (int i = 0; i < A; i++) {
                ans += '0';
            }
            return ans;
        }

        if (K <= dp[A - 1][B]) {
            return "0" + KthString(A - 1, B, K, dp);
        }

        else {
            return "1"
                + KthString(A, B - 1, K - dp[A - 1][B], dp);
        }
    }

    // Function to find the Kth lexicographically
    // smallest binary string with exactly
    // A zeroes and B ones
    static int KthStringUtil(int A, int B, int K)
    {
        // Stores the recurring states
        int[][] dp = new int[A + 1][B + 1];

        // Calculate the dp values iteratively
        dp[0][0] = 1;
        for (int i = 0; i <= A; ++i) {
            for (int j = 0; j <= B; ++j) {

                if (i > 0) {

                    // The last character was '0'
                    dp[i][j] += dp[i - 1][j];
                }
                if (j > 0) {

                    // The last character was '1'
                    dp[i][j] += dp[i][j - 1];
                }
            }
        }

        // Print the binary string obtained
        System.out.println(KthString(A, B, K, dp));

        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A = 3, B = 3, K = 7;
        KthStringUtil(A, B, K);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Recursive function to find the Kth
# smallest binary string
def KthString(A, B, K, dp):

    # Base Case
    if (A == 0):

        # Return string of all 1's
        # of length B
        str = ""
        for i in range(B):
            str += '1'

        return str

    if (B == 0):

        # Return string of all 0's
        # of length A
        str = ""
        for i in range(A):
            str += '0'
        return str

    if (K <= dp[A - 1][B]):
        return "0" + KthString( A - 1, B, K, dp)

    else:
        return "1" + KthString( A, B - 1, K - dp[A - 1][B], dp)

# Function to find the Kth lexicographically
# smallest binary string with exactly
# A zeroes and B ones
def KthStringUtil(A, B, K):

    # Stores the recurring states
    dp = [0] * (A + 1)

    for i in range(len(dp)):
        dp[i] = [0] * (B + 1)

    # Calculate the dp values iteratively
    dp[0][0] = 1
    for i in range(A + 1):
        for j in range(B + 1):

            if (i > 0):

                # The last character was '0'
                dp[i][j] += dp[i - 1][j]

            if (j > 0):

                # The last character was '1'
                dp[i][j] += dp[i][j - 1]

    # Print the binary string obtained
    print(KthString(A, B, K, dp))

# Driver Code
A = 3
B = 3
K = 7
KthStringUtil(A, B, K)

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Recursive function to find the Kth
    // smallest binary string
    static string KthString(int A, int B, long K,
                            int[, ] dp)
    {

        // Base Case
        if (A == 0) {

            // Return string of all 1's
            // of length B
            string ans = "";
            for (int i = 0; i < B; i++) {
                ans += '1';
            }
            return ans;
        }
        if (B == 0) {

            // Return string of all 0's
            // of length A
            string ans = "";
            for (int i = 0; i < A; i++) {
                ans += '0';
            }
            return ans;
        }

        if (K <= dp[A - 1, B]) {
            return "0" + KthString(A - 1, B, K, dp);
        }

        else {
            return "1"
                + KthString(A, B - 1, K - dp[A - 1, B], dp);
        }
    }

    // Function to find the Kth lexicographically
    // smallest binary string with exactly
    // A zeroes and B ones
    static int KthStringUtil(int A, int B, int K)
    {
        // Stores the recurring states
        int[, ] dp = new int[A + 1, B + 1];

        // Calculate the dp values iteratively
        dp[0, 0] = 1;
        for (int i = 0; i <= A; ++i) {
            for (int j = 0; j <= B; ++j) {

                if (i > 0) {

                    // The last character was '0'
                    dp[i, j] += dp[i - 1, j];
                }
                if (j > 0) {

                    // The last character was '1'
                    dp[i, j] += dp[i, j - 1];
                }
            }
        }

        // Print the binary string obtained
        Console.WriteLine(KthString(A, B, K, dp));

        return 0;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int A = 3, B = 3, K = 7;
        KthStringUtil(A, B, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Recursive function to find the Kth
        // smallest binary string
        function KthString(A, B, K,
            dp) {
            // Base Case
            if (A == 0) {

                // Return string of all 1's
                // of length B
                let str = "";
                for (let i = 0; i < B; i++) {
                    str += '1';
                }
                return str;
            }
            if (B == 0) {

                // Return string of all 0's
                // of length A
                let str = "";
                for (let i = 0; i < A; i++) {
                    str += '0';
                }
                return str;

            }

            if (K <= dp[A - 1][B]) {
                return "0" + KthString(
                    A - 1, B, K, dp);
            }

            else {
                return "1"
                    + KthString(
                        A, B - 1,
                        K - dp[A - 1][B], dp);
            }
        }

        // Function to find the Kth lexicographically
        // smallest binary string with exactly
        // A zeroes and B ones
        function KthStringUtil(A, B, K) {
            // Stores the recurring states
            let dp = new Array(A + 1);

            for (let i = 0; i < dp.length; i++) {
                dp[i] = new Array(B + 1).fill(0);
            }

            // Calculate the dp values iteratively
            dp[0][0] = 1;
            for (let i = 0; i <= A; ++i) {
                for (let j = 0; j <= B; ++j) {

                    if (i > 0) {

                        // The last character was '0'
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j > 0) {

                        // The last character was '1'
                        dp[i][j] += dp[i][j - 1];
                    }
                }
            }

            // Print the binary string obtained
            document.write(KthString(A, B, K, dp));

            return 0;
        }

        // Driver Code
        let A = 3, B = 3, K = 7;
        KthStringUtil(A, B, K);

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
010110
```

***时间复杂度:** O(A*B)*
***辅助空间:** O(A*B)*