# 给定二进制字符串的交替子字符串数量

> 原文:[https://www . geeksforgeeks . org/给定二进制字符串的交替子字符串数/](https://www.geeksforgeeks.org/number-of-alternating-substrings-from-a-given-binary-string/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，任务是计算字符串 **S** 中出现的交替[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。

**示例:**

> **输入:**S =“0010”
> **输出:** 7
> **解释:**
> 字符串的所有子串S 为:{“0”“00”“001”“0010”“0”“01”“010”“1”“10”“0”}
> 字符串为交替出现的:{“0”“0”“01”“010”“1”“10”“0”}。
> 因此，答案是 7。
> 
> **输入:**S = " 010 "
> T3】输出: 6

**天真法:**解决这个问题最简单的方法就是首先找到[字符串的所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **S** ，然后检查每一个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)是否交替。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**有效方法:**该问题具有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构属性](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。所以这个问题可以用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。按照以下步骤解决此问题:

*   声明一个 **dp** 数组，其中**DP【I】【j】**存储以 char **i** 开始且在**【j，N-1】**范围内的交替字符串的数量。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代，并执行以下步骤:
    *   如果 **i** 等于 **N-1** ，那么如果当前字符是**‘1’**，那么将 **1** 分配给**DP【1】【I】**，否则将 **1** 分配给**DP【0】【I】**。
    *   否则，如果当前字符为**‘0’**，则将 **dp[0][i]** 更新为 **1+dp[1][i+1]** ，否则，将 **dp[1][i]** 更新为 **1+dp[0][i+1]。**
*   初始化一个变量，比如说**和**为 **0** ，以存储交替出现的子串的数量。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   将**和**更新为 **dp[0][i]** 和 **dp[1][i]的最大值。**
*   最后，打印在**和**中获得的值作为答案。

下面是上述方法的实现:

## C++

```
// c++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of alternating
// substrings from a given binary string
int countAlternatingSubstrings(string S, int N)
{
    // Initialize dp array, where dp[i][j] stores
    // the number of alternating strings starts
    // with i and having j elements.
    vector<vector<int> > dp(2, vector<int>(N, 0));

    // Traverse the string from the end
    for (int i = N - 1; i >= 0; i--) {

        // If i is equal to N - 1
        if (i == N - 1) {

            if (S[i] == '1')
                dp[1][i] = 1;

            else
                dp[0][i] = 1;
        }
        // Otherwise,
        else {

            // Increment count of
            // substrings starting at i
            // and has 0 in the beginning
            if (S[i] == '0')
                dp[0][i] = 1 + dp[1][i + 1];

            // Increment count of
            // substrings starting at i
            // and has 1 in the beginning
            else
                dp[1][i] = 1 + dp[0][i + 1];
        }
    }
    // Stores the result
    int ans = 0;

    // Iterate in the range [0, N-1]
    for (int i = 0; i < N; i++) {

        // Update ans
        ans += max(dp[0][i], dp[1][i]);
    }

    // Return the ans
    return ans;
}

// Driver code
int main()
{
    // Given Input
    string S = "0010";
    int N = S.length();

    // Function call
    cout << countAlternatingSubstrings(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count number of alternating
// substrings from a given binary string
static int countAlternatingSubstrings(String S, int N)
{

    // Initialize dp array, where dp[i][j] stores
    // the number of alternating strings starts
    // with i and having j elements.
    int[][] dp = new int[2][N];
    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < N; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Traverse the string from the end
    for(int i = N - 1; i >= 0; i--)
    {

        // If i is equal to N - 1
        if (i == N - 1)
        {
            if (S.charAt(i) == '1')
                dp[1][i] = 1;

            else
                dp[0][i] = 1;
        }

        // Otherwise,
        else
        {

            // Increment count of
            // substrings starting at i
            // and has 0 in the beginning
            if (S.charAt(i) == '0')
                dp[0][i] = 1 + dp[1][i + 1];

            // Increment count of
            // substrings starting at i
            // and has 1 in the beginning
            else
                dp[1][i] = 1 + dp[0][i + 1];
        }
    }

    // Stores the result
    int ans = 0;

    // Iterate in the range [0, N-1]
    for(int i = 0; i < N; i++)
    {

        // Update ans
        ans += Math.max(dp[0][i], dp[1][i]);
    }

    // Return the ans
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    String S = "0010";
    int N = S.length();

    // Function call
    System.out.print(countAlternatingSubstrings(S, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count number of alternating
# substrings from a given binary string
def countAlternatingSubstrings(S, N):

    # Initialize dp array, where dp[i][j] stores
    # the number of alternating strings starts
    # with i and having j elements.
    dp = [[0 for i in range(N)]
             for i in range(2)]

    # Traverse the string from the end
    for i in range(N - 1, -1, -1):

        # If i is equal to N - 1
        if (i == N - 1):

            if (S[i] == '1'):
                dp[1][i] = 1
            else:
                dp[0][i] = 1

        # Otherwise,
        else:

            # Increment count of
            # substrings starting at i
            # and has 0 in the beginning
            if (S[i] == '0'):
                dp[0][i] = 1 + dp[1][i + 1]

            # Increment count of
            # substrings starting at i
            # and has 1 in the beginning
            else:
                dp[1][i] = 1 + dp[0][i + 1]

    # Stores the result
    ans = 0

    # Iterate in the range [0, N-1]
    for i in range(N):

        # Update ans
        ans += max(dp[0][i], dp[1][i])

    # Return the ans
    return ans

# Driver code
if __name__ == '__main__':

    # Given Input
    S = "0010"
    N = len(S)

    # Function call
    print (countAlternatingSubstrings(S, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count number of alternating
// substrings from a given binary string
static int countAlternatingSubstrings(string S, int N)
{

    // Initialize dp array, where dp[i][j] stores
    // the number of alternating strings starts
    // with i and having j elements.
    int[,] dp = new int[2, N];
    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < N; j++)
        {
            dp[i, j] = 0;
        }
    }

    // Traverse the string from the end
    for(int i = N - 1; i >= 0; i--)
    {

        // If i is equal to N - 1
        if (i == N - 1)
        {
            if (S[i] == '1')
                dp[1, i] = 1;

            else
                dp[0, i] = 1;
        }

        // Otherwise,
        else
        {

            // Increment count of
            // substrings starting at i
            // and has 0 in the beginning
            if (S[i] == '0')
                dp[0, i] = 1 + dp[1, i + 1];

            // Increment count of
            // substrings starting at i
            // and has 1 in the beginning
            else
                dp[1, i] = 1 + dp[0, i + 1];
        }
    }

    // Stores the result
    int ans = 0;

    // Iterate in the range [0, N-1]
    for(int i = 0; i < N; i++)
    {

        // Update ans
        ans += Math.Max(dp[0, i], dp[1, i]);
    }

    // Return the ans
    return ans;
}

// Driver Code
public static void Main()
{

    // Given Input
    string S = "0010";
    int N = S.Length;

    // Function call
    Console.Write(countAlternatingSubstrings(S, N));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count number of alternating
// substrings from a given binary string
function countAlternatingSubstrings(S, N)
{

    // Initialize dp array, where dp[i][j] stores
    // the number of alternating strings starts
    // with i and having j elements.
    var dp = new Array(2);
    dp[0] = Array(N).fill(0);
    dp[1] = Array(N).fill(0);

    var i;

    // Traverse the string from the end
    for(i = N - 1; i >= 0; i--)
    {

        // If i is equal to N - 1
        if (i == N - 1)
        {
            if (S[i] == '1')
                dp[1][i] = 1;
            else
                dp[0][i] = 1;
        }

        // Otherwise,
        else
        {

            // Increment count of
            // substrings starting at i
            // and has 0 in the beginning
            if (S[i] == '0')
                dp[0][i] = 1 + dp[1][i + 1];

            // Increment count of
            // substrings starting at i
            // and has 1 in the beginning
            else
                dp[1][i] = 1 + dp[0][i + 1];
        }
    }

    // Stores the result
    var ans = 0;

    // Iterate in the range [0, N-1]
    for(i = 0; i < N; i++)
    {

        // Update ans
        ans += Math.max(dp[0][i], dp[1][i]);
    }

    // Return the ans
    return ans;
}

// Driver code

// Given Input
var S = "0010";
var N = S.length;

// Function call
document.write(countAlternatingSubstrings(S, N));

// This code is contributed by SURENDRA_GANGWAR

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)