# 计算可能的 N 位数字，使每个数字连续出现的次数不超过给定次数

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-这样-每个数字-不会出现-超过给定的次数-连续/](https://www.geeksforgeeks.org/count-n-digits-numbers-such-that-each-digit-does-not-appear-more-than-given-number-of-times-consecutively/)

给定一个整数 **N** 和一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **最大数字[]** ，任务是计算所有不同的 **N** 位数，使得数字 **i** 出现的次数不超过**最大数字【I】**次。由于计数会很大，打印出来[模 **10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 2，maxDigit[] = {1，1，1，1，1，1，1，1，1}
> **输出:** 90
> **说明:**
> 任意一个数字不能连续出现一次以上。因此，数字[00，11，22，33，44，55，66，77，88，99]无效。
> 因此，没有任何限制的总数是 10×10 = 100。
> 因此，计数为 100–10 = 90。
> 
> **输入:** N = 3，maxDigit[] = {2，1，1，1，1，2，1，1，1，2 }
> T3】输出: 864

**天真方法:**最简单的方法是迭代所有的 **N** 位数字，并计算那些满足给定条件的数字。核对所有数字后，以 **10 <sup>9</sup> + 7** 为模打印总计数。

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[数字动态规划](https://www.geeksforgeeks.org/digit-dp-introduction/)的概念。该问题的动态规划状态解释如下:

*   在 Digit-DP 中，想法是通过在每个位置放置一个数字**【0，9】**从左到右构建一个数字。所以，要跟踪当前位置，需要有一个**位置**状态。该状态将具有从 **0** 到**(N–1)**的可能值。
*   根据问题，一个数字 **i** 连续出现的次数不能超过**最大数字【I】**，因此要跟踪之前填充的数字。所以，需要一个状态**之前的**。该状态将具有从 **0** 到 **9** 的可能值。
*   需要一个状态**计数**，它将提供一个数字可以连续出现的次数。该状态将具有从 **1** 到**最大数字【I】**的可能值。

按照以下步骤解决此问题:

*   第一个位置可以有任何数字，没有任何限制。
*   从第二个位置开始，跟踪先前填充的数字及其给定的计数，直到它可以连续出现。
*   如果相同的数字出现在下一个位置，那么递减它的计数，如果这个计数变为零，在下一个递归调用中简单地忽略这个数字。
*   如果下一个位置出现不同的数字，则根据**maxdigest[]**中的给定值更新其计数。
*   在上面的每一个[递归](https://www.geeksforgeeks.org/recursion/)调用中，当产生结果数时，增加该数的计数。
*   完成上述步骤后，打印总计**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Macros for modulus
#define MOD 1000000007

// DP array for memoization
int dp[5005][12][12];

// Utility function to count N digit
// numbers with digit i not appearing
// more than max_digit[i] consecutively
int findCountUtil(int N, int maxDigit[],
                  int position = 0,
                  int previous = 0,
                  int count = 1)
{

    // If number with N digits
    // is generated
    if (position == N) {
        return 1;
    }

    // Create a reference variable
    int& ans = dp[position][previous][count];

    // Check if the current state is
    // already computed before
    if (ans != -1) {
        return ans;
    }

    // Initialize ans as zero
    ans = 0;

    for (int i = 0; i <= 9; ++i) {

        // Check if count of previous
        // digit has reached zero or not
        if (count == 0 && previous != i) {

            // Fill current position
            // only with digits that
            // are unequal to previous digit
            ans = (ans
                   + (findCountUtil(N, maxDigit,
                                    position + 1, i,
                                    maxDigit[i] - 1))
                         % MOD)
                  % MOD;
        }

        else if (count != 0) {

            // If by placing the same digit
            // as previous on the current
            // position, decrement count by 1

            // Else set the value of count
            // for this new digit
            // accordingly from max_digit[]
            ans = (ans
                   + (findCountUtil(
                         N, maxDigit, position + 1, i,
                         (previous == i && position != 0)
                             ? count - 1
                             : maxDigit[i] - 1))
                         % MOD)
                  % MOD;
        }
    }
    return ans;
}

// Function to count N digit numbers
// with digit i not appearing more
// than max_digit[i] consecutive times
void findCount(int N, int maxDigit[])
{

    // Stores the final count
    int ans = findCountUtil(N, maxDigit);

    // Print the total count
    cout << ans;
}

// Driver Code
int main()
{
    int N = 2;
    int maxDigit[10] = { 1, 1, 1, 1, 1,
                         1, 1, 1, 1, 1 };

    // Initialize the dp array with -1
    memset(dp, -1, sizeof(dp));

    // Function Call
    findCount(N, maxDigit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
import java.util.*;

class GFG{

// Macros for modulus
static int MOD = 1000000007;

// DP array for memoization
static int dp[][][] = new int[5005][12][12];

// Utility function to count N digit
// numbers with digit i not appearing
// more than max_digit[i] consecutively
static int findCountUtil(int N, int maxDigit[],
                         int position,
                         int previous,
                         int count)
{

    // If number with N digits
    // is generated
    if (position == N)
    {
        return 1;
    }

    // Create a reference variable
    int ans = dp[position][previous][count];

    // Check if the current state is
    // already computed before
    if (ans != -1)
    {
        return ans;
    }

    // Initialize ans as zero
    ans = 0;

    for(int i = 0; i <= 9; ++i)
    {

        // Check if count of previous
        // digit has reached zero or not
        if (count == 0 && previous != i)
        {

            // Fill current position
            // only with digits that
            // are unequal to previous digit
            ans = (ans + (findCountUtil(
                  N, maxDigit, position + 1, i,
                  maxDigit[i] - 1)) % MOD) % MOD;
        }

        else if (count != 0)
        {

            // If by placing the same digit
            // as previous on the current
            // position, decrement count by 1

            // Else set the value of count
            // for this new digit
            // accordingly from max_digit[]
            ans = (ans + (findCountUtil(
                  N, maxDigit, position + 1, i,
                  (previous == i && position != 0) ?
                  count - 1 : maxDigit[i] - 1)) % MOD) % MOD;
        }
    }

    return ans;
}

// Function to count N digit numbers
// with digit i not appearing more
// than max_digit[i] consecutive times
static void findCount(int N, int maxDigit[])
{
    int position = 0;
    int previous = 0;
    int count = 1;

    // Stores the final count
    int ans = findCountUtil(N, maxDigit, position,
                            previous, count);

    // Print the total count
    System.out.println(ans);
}

// Driver Code   
public static void main (String[] args)   
{   
    int N = 2;
    int[] maxDigit = { 1, 1, 1, 1, 1,
                       1, 1, 1, 1, 1 };

    // Initialize the dp array with -1
    // Fill each row with -1. 
    for(int[][] row : dp)
    {
        for(int[] rowColumn : row)
        {
            Arrays.fill(rowColumn, -1);
        }
    }

    // Function Call
    findCount(N, maxDigit);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach
# Macros for modulus

# DP array for memoization
dp = [[[ -1 for i in range(5005)] for i in range(12) ] for i in range(12)]

# Utility function to count N digit
# numbers with digit i not appearing
# more than max_digit[i] consecutively
def findCountUtil(N, maxDigit, position ,previous ,count):
    global dp

    # If number with N digits
    # is generated
    if (position == N):
        return 1

    # Create a reference variable
    ans = dp[position][previous][count]

    # Check if the current state is
    # already computed before
    if (ans != -1):
        return ans

    # Initialize ans as zero
    ans = 0
    for i in range(10):

        # Check if count of previous
        # digit has reached zero or not
        if (count == 0 and previous != i):

            # Fill current position
            # only with digits that
            # are unequal to previous digit
            ans = (ans + (findCountUtil(N, maxDigit, position + 1, i, maxDigit[i] - 1)) % 1000000007)% 1000000007
        elif (count != 0):

            # If by placing the same digit
            # as previous on the current
            # position, decrement count by 1

            # Else set the value of count
            # for this new digit
            # accordingly from max_digit[]
            ans = (ans + (findCountUtil(N, maxDigit, position + 1, i, count - 1 if (previous == i and position != 0) else maxDigit[i] - 1)) % 1000000007)% 1000000007

    dp[position][previous][count] = ans
    return ans

# Function to count N digit numbers
# with digit i not appearing more
# than max_digit[i] consecutive times
def findCount(N, maxDigit):

    # Stores the final count
    ans = findCountUtil(N, maxDigit, 0, 0, 1)

    # Print the total count
    print (ans)

# Driver Code
if __name__ == '__main__':
    N = 2
    maxDigit = [1, 1, 1, 1, 1,1, 1, 1, 1, 1]

    # Function Call
    findCount(N, maxDigit)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach 
using System;
using System.Collections.Generic;

using System;
using System.Collections.Generic;
public class GFG{

// Macros for modulus
static int MOD = 1000000007;

// DP array for memoization
static int [,,]dp = new int[5005, 12, 12];

// Utility function to count N digit
// numbers with digit i not appearing
// more than max_digit[i] consecutively
static int findCountUtil(int N, int []maxDigit,
                         int position,
                         int previous,
                         int count)
{

    // If number with N digits
    // is generated
    if (position == N)
    {
        return 1;
    }

    // Create a reference variable
    int ans = dp[position, previous, count];

    // Check if the current state is
    // already computed before
    if (ans != -1)
    {
        return ans;
    }

    // Initialize ans as zero
    ans = 0;

    for(int i = 0; i <= 9; ++i)
    {

        // Check if count of previous
        // digit has reached zero or not
        if (count == 0 && previous != i)
        {

            // Fill current position
            // only with digits that
            // are unequal to previous digit
            ans = (ans + (findCountUtil(
                  N, maxDigit, position + 1, i,
                  maxDigit[i] - 1)) % MOD) % MOD;
        }

        else if (count != 0)
        {

            // If by placing the same digit
            // as previous on the current
            // position, decrement count by 1

            // Else set the value of count
            // for this new digit
            // accordingly from max_digit[]
            ans = (ans + (findCountUtil(
                  N, maxDigit, position + 1, i,
                  (previous == i && position != 0) ?
                  count - 1 : maxDigit[i] - 1)) % MOD) % MOD;
        }
    }   
    return ans;
}

// Function to count N digit numbers
// with digit i not appearing more
// than max_digit[i] consecutive times
static void findCount(int N, int []maxDigit)
{
    int position = 0;
    int previous = 0;
    int count = 1;

    // Stores the readonly count
    int ans = findCountUtil(N, maxDigit, position,
                            previous, count);

    // Print the total count
    Console.WriteLine(ans);
}

// Driver Code   
public static void Main(String[] args)   
{   
    int N = 2;
    int[] maxDigit = { 1, 1, 1, 1, 1,
                       1, 1, 1, 1, 1 };

    // Initialize the dp array with -1
    // Fill each row with -1. 
    for(int i = 0; i < dp.GetLength(0); i++)
    {
        for (int j = 0; j < dp.GetLength(1); j++)
        {
            for (int k = 0; k < dp.GetLength(2); k++)
                dp[i, j, k] = -1;
        }
    }

    // Function Call
    findCount(N, maxDigit);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Macros for modulus
    let MOD = 1000000007;

    // DP array for memoization
    let dp = new Array(5005);
    for(let i = 0; i < 12; i++)
    {
        dp[i] = new Array(12);
        for(let j = 0; j < 12; j++)
        {
            dp[i][j] = new Array(12);   
            for(let k = 0; k < 12; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }

    // Utility function to count N digit
    // numbers with digit i not appearing
    // more than max_digit[i] consecutively
    function findCountUtil(N, maxDigit, position, previous, count)
    {

        // If number with N digits
        // is generated
        if (position == N)
        {
            return 1;
        }

        // Create a reference variable
        let ans = dp[position][previous][count];

        // Check if the current state is
        // already computed before
        if (ans != -1)
        {
            return ans;
        }

        // Initialize ans as zero
        ans = 0;

        for(let i = 0; i <= 9; ++i)
        {

            // Check if count of previous
            // digit has reached zero or not
            if (count == 0 && previous != i)
            {

                // Fill current position
                // only with digits that
                // are unequal to previous digit
                ans = (ans + (findCountUtil(
                      N, maxDigit, position + 1, i,
                      maxDigit[i] - 1)) % MOD) % MOD;
            }

            else if (count != 0)
            {

                // If by placing the same digit
                // as previous on the current
                // position, decrement count by 1

                // Else set the value of count
                // for this new digit
                // accordingly from max_digit[]
                ans = (ans + (findCountUtil(
                      N, maxDigit, position + 1, i,
                      (previous == i && position != 0) ?
                      count - 1 : maxDigit[i] - 1)) % MOD) % MOD;
            }
        }

        return ans;
    }

    // Function to count N digit numbers
    // with digit i not appearing more
    // than max_digit[i] consecutive times
    function findCount(N, maxDigit)
    {
        let position = 0;
        let previous = 0;
        let count = 1;

        // Stores the final count
        let ans = findCountUtil(N, maxDigit, position, previous, count);

        // Print the total count
        document.write(ans);
    }

    let N = 2;
    let maxDigit = [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ];

    // Function Call
    findCount(N, maxDigit);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
90
```

***时间复杂度:**O(N * 10 * 10)*
T5**辅助空间:** O(N*10*10)