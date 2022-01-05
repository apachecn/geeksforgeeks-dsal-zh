# 对给定范围内相邻数字不是同素的数字进行计数

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-给定范围-其相邻数字不是-co-prime/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-whose-adjacent-digits-are-not-co-prime/)

给定一个整数 **N** ，打印相邻数字不是[同素的**【1，N】**范围内的计数值的任务。](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)

> 如果两个数字的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 1，则两个数字 **A** 和 **B** 被称为**同素**。

**示例:**

> **输入:** N = 30
> **输出:** 15
> **说明:**从【1，30】开始有非同素相邻数字的数字为{1，2，3，4，5，6，7，8，9，20，22，24，26，28，30}。
> 
> **输入:**N = 10000
> T3】输出: 1361

**天真法:**解决问题最简单的方法是迭代范围 **1** 到 **N** ，对于范围内的每个数字，检查其相邻数字的 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 是否等于 **1** ，并相应更新答案。

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)* 。

**高效法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为它有重叠子问题和最优子结构。子问题可以使用记忆存储在**DP[][][][][]表**中，其中**DP[I][bound][prev][all zero]**存储从**的第 I 个**位置到末端的答案，其中 **bound** 是布尔变量，它确保数字不超过 **N** ， **prev** 存储先前选择的数字**，all zero**是用于

1.  通过执行以下步骤定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **非素数(I，bound，prev，all zero)**。
    1.  将极限 **N** 转换为一个字符串，这样它将只在字符串的长度上迭代，而不是**N**的实际极限
    2.  检查基本情况，即如果整个字符串被完全遍历 **(i == N)** ，则返回 **1** 作为已经构造的范围**【1，N】**内的有效数字。
    3.  如果状态**DP[I][绑定][上一个][全零]** 的结果已经计算出来，则返回存储在**DP[I][绑定][上一个][全零]中的值。**
    4.  在当前位置**‘I’**可以放置[0，9]中的任何数字。放置数字时，借助变量**绑定**，确保数字不超过**‘R’**。还要检查当前数字和前一个数字(存储在 **prev** 中)的 [**GCD**](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 是否大于 1。这里有两种边缘情况:
        1.  如果当前索引为 0，请将任意数字放在第一个位置。
        2.  如果到目前为止填充的所有数字都是零，即**全零**为真，那么尽管[**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)T6(0，1) = 1 为最高有效数字，但将 1 放在当前位置是有效的。然后将**全零**设置为**假**。
    5.  在当前位置放置一个有效数字后，递归调用索引(i + 1)处元素的**非质数**函数。
    6.  返回所有可能的有效数字位置的总和作为答案。

*   完成以上步骤后，打印**nooptimecount(0)**值作为结果。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int dp[100][2][10][2];

// Function to count numbers whose
// adjacent digits are not co-prime
int noncoprimeCount(int i, int N, string& S,
                    bool bound, int prev,
                    bool allZeros)
{
    // Base Case
    // If the entire string
    // is traversed
    if (i == N)
        return 1;

    int& val = dp[i][bound][prev][allZeros];

    // If the subproblem has
    // already been computed
    if (val != -1)
        return val;

    int cnt = 0;

    for (int j = 0; j <= (bound ? (S[i] - '0') : 9); ++j) {

        // A digit can be placed at
        // the current position if:

        // GCD of current and previous
        // digits is not equal to 1
        if ((__gcd(j, prev) != 1)

            // Current position is 0
            || (i == 0)

            // All encountered digits
            // until now are 0s
            || allZeros == 1) {

            cnt += noncoprimeCount(
                i + 1, N, S, bound
                                 & (j == (S[i] - '0')),
                j,
                allZeros & (j == 0));
        }
    }

    // Return the total
    // possible valid numbers
    return val = cnt;
}

// Function to count numbers whose
// adjacent digits are not co-prime
void noncoprimeCountUtil(int R)
{
    // Convert R to string.
    string S = to_string(R);

    // Length of string
    int N = S.length();

    // Initialize dp array with -1
    memset(dp, -1, sizeof dp);

    // Function call with initial values of
    // bound, allZeros, previous as 1, 1, 0
    int ans = noncoprimeCount(0, N, S, 1, 0, 1);

    // Subtract 1 from the answer, as 0 is included
    cout << ans - 1 << endl;
}

// Driver Code
int main()
{
    // Input
    int N = 10000;
    // Function call
    noncoprimeCountUtil(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static int [][][][]dp = new int[100][2][10][2];
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}
// Function to count numbers whose
// adjacent digits are not co-prime
static int noncoprimeCount(int i, int N, char []S,
                    int bound, int prev,
                    int allZeros)
{
    // Base Case
    // If the entire String
    // is traversed
    if (i == N)
        return 1;

    int val = dp[i][bound][prev][allZeros];

    // If the subproblem has
    // already been computed
    if (val != -1)
        return val;

    int cnt = 0;

    for (int j = 0; j <= (bound!=0 ? (S[i] - '0') : 9); ++j) {

        // A digit can be placed at
        // the current position if:

        // GCD of current and previous
        // digits is not equal to 1
        if ((__gcd(j, prev) != 1)

            // Current position is 0
            || (i == 0)

            // All encountered digits
            // until now are 0s
            || allZeros == 1) {

            cnt += noncoprimeCount(
                i + 1, N, S, bound!=0
                                 & (j == (S[i] - '0'))?1:0,
                j,
                (allZeros!=0 & (j == 0))?1:0);
        }
    }

    // Return the total
    // possible valid numbers
    return val = cnt;
}

// Function to count numbers whose
// adjacent digits are not co-prime
static void noncoprimeCountUtil(int R)
{
    // Convert R to String.
    String S = String.valueOf(R);

    // Length of String
    int N = S.length();

    // Initialize dp array with -1
    for (int i = 0; i < 100; i++)
         for (int j = 0; j < 2; j++)
             for (int k = 0; k < 10; k++)
                 for (int l = 0; l < 2; l++)
                     dp[i][j][k][l] = -1;

    // Function call with initial values of
    // bound, allZeros, previous as 1, 1, 0
    int ans = noncoprimeCount(0, N, S.toCharArray(), 1, 0, 1);

    // Subtract 1 from the answer, as 0 is included
    System.out.print(ans - 1 +"\n");
}

// Driver Code
public static void main(String[] args)
{
    // Input
    int N = 10000;
    // Function call
    noncoprimeCountUtil(N);

}
}

// This code contributed by shikhasingrajput
```

## C#

```
using System;

class GFG{

static int[,,,] dp = new int[100, 2, 10, 2];

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Function to count numbers whose
// adjacent digits are not co-prime
static int noncoprimeCount(int i, int N, char[] S, int bound,
                           int prev, int allZeros)
{

    // Base Case
    // If the entire String
    // is traversed
    if (i == N)
        return 1;

    int val = dp[i, bound, prev, allZeros];

    // If the subproblem has
    // already been computed
    if (val != -1)
        return val;

    int cnt = 0;

    for(int j = 0;
            j <= (bound != 0 ? (S[i] - '0') : 9); ++j)
    {

        // A digit can be placed at
        // the current position if:

        // GCD of current and previous
        // digits is not equal to 1
        if ((__gcd(j, prev) != 1)

                // Current position is 0
                || (i == 0)

                // All encountered digits
                // until now are 0s
                || allZeros == 1)
        {
            cnt += noncoprimeCount(i + 1, N, S, bound != 0 &
                                  (j == (S[i] - '0')) ? 1 : 0, j,
                           (allZeros != 0 & (j == 0)) ? 1 : 0);
        }
    }

    // Return the total
    // possible valid numbers
    return val = cnt;
}

// Function to count numbers whose
// adjacent digits are not co-prime
static void noncoprimeCountUtil(int R)
{

    // Convert R to String.
    String S = String.Join("", R);

    // Length of String
    int N = S.Length;

    // Initialize dp array with -1
    for(int i = 0; i < 100; i++)
        for(int j = 0; j < 2; j++)
            for(int k = 0; k < 10; k++)
                for(int l = 0; l < 2; l++)
                    dp[i, j, k, l] = -1;

    // Function call with initial values of
    // bound, allZeros, previous as 1, 1, 0
    int ans = noncoprimeCount(0, N, S.ToCharArray(), 1, 0, 1);

    // Subtract 1 from the answer, as 0 is included
    Console.Write(ans - 1 + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Input
    int N = 10000;

    // Function call
    noncoprimeCountUtil(N);
}
}

// This code is contributed by umadevi9616
```

**Output:** 

```
1361
```

***时间复杂度:** O(log <sub>10</sub> N * 2 * 10 * 2 * 10)。在每次递归调用中，当所有数字[0，9]都被迭代时，10 的额外因子出现。*
***辅助空间:**O(log<sub>10</sub>N * 2 * 10 * 2)*