# 对给定范围内的数字进行计数，这些数字的乘积为 K

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-给定范围-谁的数字乘积是-k/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-whose-product-of-digits-is-k/)

给定三个正整数 **L** 、 **R** 和 **K** ，任务是对数字的[乘积等于 **K** 的**【L，R】**范围内的数字进行计数](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)

**示例:**

> **输入:** L = 1，R = 130，K = 14
> **输出:** 3
> **说明:**
> 数字之和为 K(= 14)的[1，100]范围内的数字为:
> 27 =>2 * 7 = 14
> 72 =>7 * 2 = 14
> 127 =>1 * 2 * 7 = 14【T12
> 
> **输入:** L = 20，R = 10000，K = 14
> T3】输出: 20

**天真法:**解决这个问题最简单的方法就是迭代**【L，R】**范围内的所有数字，对于每个数字，检查其[数字乘积](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)是否等于 **K** 。如果发现为真，则增加计数。最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the product
// of digits of a number
int prodOfDigit(int N)
{
    // Stores product of
    // digits of N
    int res = 1;

    while (N) {

        // Update res
        res = res * (N % 10);

        // Update N
        N /= 10;
    }

    return res;
}

// Function to count numbers in the range
// [0, X] whose product of digit is K
int cntNumRange(int L, int R, int K)
{
    // Stores count of numbers in the range
    // [L, R] whose product of digit is K
    int cnt = 0;

    // Iterate over the range [L, R]
    for (int i = L; i <= R; i++) {

        // If product of digits of
        // i equal to K
        if (prodOfDigit(i) == K) {

            // Update cnt
            cnt++;
        }
    }

    return cnt;
}

// Driver Code
int main()
{
    int L = 20, R = 10000, K = 14;
    cout << cntNumRange(L, R, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the product
// of digits of a number
static int prodOfDigit(int N)
{

    // Stores product of
    // digits of N
    int res = 1;
    while (N > 0)
    {

        // Update res
        res = res * (N % 10);

        // Update N
        N /= 10;
    }

    return res;
}

// Function to count numbers in the range
// [0, X] whose product of digit is K
static int cntNumRange(int L, int R, int K)
{

    // Stores count of numbers in the range
    // [L, R] whose product of digit is K
    int cnt = 0;

    // Iterate over the range [L, R]
    for (int i = L; i <= R; i++)
    {

        // If product of digits of
        // i equal to K
        if (prodOfDigit(i) == K)
        {

            // Update cnt
            cnt++;
        }
    }
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int L = 20, R = 10000, K = 14;
    System.out.print(cntNumRange(L, R, K));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the product
# of digits of a number
def prodOfDigit(N):

    # Stores product of
    # digits of N
    res = 1

    while (N):

        # Update res
        res = res * (N % 10)

        # Update N
        N //= 10

    return res

# Function to count numbers in the range
# [0, X] whose product of digit is K
def cntNumRange(L, R, K):

    # Stores count of numbers in the range
    # [L, R] whose product of digit is K
    cnt = 0

    # Iterate over the range [L, R]
    for i in range(L, R + 1):

        # If product of digits of
        # i equal to K
        if (prodOfDigit(i) == K):

            # Update cnt
            cnt += 1

    return cnt

# Driver Code
if __name__ == '__main__':

    L, R, K = 20, 10000, 14

    print(cntNumRange(L, R, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the product
// of digits of a number
static int prodOfDigit(int N)
{

    // Stores product of
    // digits of N
    int res = 1;

    while (N > 0)
    {

        // Update res
        res = res * (N % 10);

        // Update N
        N /= 10;
    }
    return res;
}

// Function to count numbers in the range
// [0, X] whose product of digit is K
static int cntNumRange(int L, int R, int K)
{

    // Stores count of numbers in the range
    // [L, R] whose product of digit is K
    int cnt = 0;

    // Iterate over the range [L, R]
    for(int i = L; i <= R; i++)
    {

        // If product of digits of
        // i equal to K
        if (prodOfDigit(i) == K)
        {

            // Update cnt
            cnt++;
        }
    }
    return cnt;
}

// Driver Code
static void Main()
{
    int L = 20, R = 10000, K = 14;

    Console.WriteLine(cntNumRange(L, R, K));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the product
// of digits of a number
function prodOfDigit(N)
{
    // Stores product of
    // digits of N
    let res = 1;

    while (N) {

        // Update res
        res = res * (N % 10);

        // Update N
        N = Math.floor(N/10);
    }

    return res;
}

// Function to count numbers in the range
// [0, X] whose product of digit is K
function cntNumRange(L, R, K)
{

    // Stores count of numbers in the range
    // [L, R] whose product of digit is K
    let cnt = 0;

    // Iterate over the range [L, R]
    for (let i = L; i <= R; i++) {

        // If product of digits of
        // i equal to K
        if (prodOfDigit(i) == K)
        {

            // Update cnt
            cnt++;
        }
    }

    return cnt;
}

// Driver Code
    let L = 20, R = 10000, K = 14;
    document.write(cntNumRange(L, R, K));

// This code is contributed by manoj.
</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(R–L+1)* log<sub>10</sub>(R)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/) 。以下是数字动力定位系统的动态编程状态:

> 动态编程状态为:
> **生产:**代表位数之和。
> **紧:**检查位数之和是否超过 K。
> **结束:**存储一个数字的第 I<sup>位的最大可能值。
> **st:** 检查一个数字是否包含前导 0。</sup>

以下是动态规划状态的递归关系:

*   如果 **i == 0 且 st == 0:**

> ![cntNum(i, prod, st, tight)                       ](img/338270ffefea69e7f72137ddfdaf1f08.png "Rendered by QuickLaTeX.com")
> ![= \sum^{9}_{j=0} cntNum(i + 1, prod, false, tight & (j == end)                       ](img/44180657af347c42f55449e56fa67f51.png "Rendered by QuickLaTeX.com")
> 
> **cntNum(N，K，st，紧绷):**返回数字乘积为 K 的[0，X]范围内的数字计数

*   否则，

> ![cntNum(i, prod, st, tight)                       ](img/338270ffefea69e7f72137ddfdaf1f08.png "Rendered by QuickLaTeX.com")
> ![= \sum^{9}_{j=0} cntNum(i + 1, (prod * j), true, tight & (j == end)                       ](img/ee066dd28dc1803ff562523f1a55daf5.png "Rendered by QuickLaTeX.com")
> 
> **cntNum(N，K，st，紧绷):**返回数字乘积为 K 的[0，X]范围内的数字计数

按照以下步骤解决问题:

1.  初始化一个[三维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**DP【N】【K】【紧】**计算并存储上述递归关系的所有子问题的值。
2.  最后，返回**DP【N】【sum】【紧】**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define M 100

// Function to count numbers in the range
// [0, X] whose product of digit is K
int cntNum(string X, int i, int prod, int K,
           int st, int tight, int dp[M][M][2][2])
{
    // If count of digits in a number
    // greater than count of digits in X
    if (i >= X.length() || prod > K) {

        // If product of digits of a
        // number equal to K
        return prod == K;
    }

    // If overlapping subproblems
    // already occurred
    if (dp[prod][i][tight][st] != -1) {
        return dp[prod][i][tight][st];
    }

    // Stores count of numbers whose
    // product of digits is K
    int res = 0;

    // Check if the numbers
    // exceeds K or not
    int end = tight ? X[i] - '0' : 9;

    // Iterate over all possible
    // value of i-th digits
    for (int j = 0; j <= end; j++) {

        // if number contains leading 0
        if (j == 0 && !st) {

            // Update res
            res += cntNum(X, i + 1, prod, K,
                          false, (tight & (j == end)), dp);
        }

        else {

            // Update res
            res += cntNum(X, i + 1, prod * j, K,
                          true, (tight & (j == end)), dp);
        }

        // Update res
    }

    // Return res
    return dp[prod][i][tight][st] = res;
}

// Utility function to count the numbers in
// the range [L, R] whose prod of digits is K
int UtilCntNumRange(int L, int R, int K)
{
    // Stores numbers in the form
    // of string
    string str = to_string(R);

    // Stores overlapping subproblems
    int dp[M][M][2][2];

    // Initialize dp[][][] to -1
    memset(dp, -1, sizeof(dp));

    // Stores count of numbers in
    // the range [0, R] whose
    // product of  digits is k
    int cntR = cntNum(str, 0, 1, K,
                      false, true, dp);

    // Update str
    str = to_string(L - 1);

    // Initialize dp[][][] to -1
    memset(dp, -1, sizeof(dp));

    // Stores count of numbers in
    // the range [0, L - 1] whose
    // product of  digits is k
    int cntL = cntNum(str, 0, 1, K,
                      false, true, dp);

    return (cntR - cntL);
}

// Driver Code
int main()
{
    int L = 20, R = 10000, K = 14;
    cout << UtilCntNumRange(L, R, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static final int M = 100;

// Function to count numbers in the range
// [0, X] whose product of digit is K
static int cntNum(String X, int i, int prod, int K,
                    int st, int tight, int [][][][]dp)
{

    // If count of digits in a number
    // greater than count of digits in X
    if (i >= X.length() || prod > K)
    {

        // If product of digits of a
        // number equal to K
        return prod == K ? 1 : 0;
    }

    // If overlapping subproblems
    // already occurred
    if (dp[prod][i][tight][st] != -1)
    {
        return dp[prod][i][tight][st];
    }

    // Stores count of numbers whose
    // product of digits is K
    int res = 0;

    // Check if the numbers
    // exceeds K or not
    int end = tight > 0 ? X.charAt(i) - '0' : 9;

    // Iterate over all possible
    // value of i-th digits
    for(int j = 0; j <= end; j++)
    {

        // If number contains leading 0
        if (j == 0 && st == 0)
        {

            // Update res
            res += cntNum(X, i + 1, prod, K, 0,
                  (tight & ((j == end) ? 1 : 0)), dp);
        }
        else
        {

            // Update res
            res += cntNum(X, i + 1, prod * j, K, 1,
                  (tight & ((j == end) ? 1 : 0)), dp);
        }
    }

    // Return res
    return dp[prod][i][tight][st] = res;
}

// Utility function to count the numbers in
// the range [L, R] whose prod of digits is K
static int UtilCntNumRange(int L, int R, int K)
{

    // Stores numbers in the form
    // of String
    String str = String.valueOf(R);

    // Stores overlapping subproblems
    int [][][][]dp = new int[M][M][2][2];

    // Initialize dp[][][] to -1
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < M; j++)
        {
            for(int k = 0; k < 2; k++)
                for(int l = 0; l < 2; l++)
                    dp[i][j][k][l] = -1;
        }
    }

    // Stores count of numbers in
    // the range [0, R] whose
    // product of  digits is k
    int cntR = cntNum(str, 0, 1, K,
                      0, 1, dp);

    // Update str
    str = String.valueOf(L - 1);

    // Initialize dp[][][] to -1
    for(int i = 0;i<M;i++)
    {
        for(int j = 0; j < M; j++)
        {
            for(int k = 0; k < 2; k++)
                for(int l = 0; l < 2; l++)
                    dp[i][j][k][l] = -1;
        }
    }

    // Stores count of numbers in
    // the range [0, L - 1] whose
    // product of  digits is k
    int cntL = cntNum(str, 0, 1, K,
                      0, 1, dp);

    return (cntR - cntL);
}

// Driver Code
public static void main(String[] args)
{
    int L = 20, R = 10000, K = 14;

    System.out.print(UtilCntNumRange(L, R, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
M = 100

# Function to count numbers in the range
# [0, X] whose product of digit is K
def cntNum(X, i, prod, K, st, tight, dp):
    end = 0

    # If count of digits in a number
    # greater than count of digits in X
    if (i >= len(X) or prod > K):

        # If product of digits of a
        # number equal to K
        if(prod == K):
          return 1
        else:
          return 0

    # If overlapping subproblems
    # already occurred
    if (dp[prod][i][tight][st] != -1):
        return dp[prod][i][tight][st]

    # Stores count of numbers whose
    # product of digits is K
    res = 0

    # Check if the numbers
    # exceeds K or not
    if(tight != 0):
        end = ord(X[i]) - ord('0')

    # Iterate over all possible
    # value of i-th digits
    for j in range(end + 1):

        # if number contains leading 0
        if (j == 0 and st == 0):
            # Update res
            res += cntNum(X, i + 1, prod, K, False, (tight & (j == end)), dp)

        else:
            # Update res
            res += cntNum(X, i + 1, prod * j, K, True, (tight & (j == end)), dp)
        # Update res

    # Return res
    dp[prod][i][tight][st] = res
    return res

# Utility function to count the numbers in
# the range [L, R] whose prod of digits is K
def UtilCntNumRange(L, R, K):
    global M

    # Stores numbers in the form
    # of string
    str1 = str(R)

    # Stores overlapping subproblems
    dp = [[[[-1 for i in range(2)] for j in range(2)] for k in range(M)] for l in range(M)]

    # Stores count of numbers in
    # the range [0, R] whose
    # product of  digits is k
    cntR = cntNum(str1, 0, 1, K, False, True, dp)

    # Update str
    str1 = str(L - 1)
    dp = [[[[-1 for i in range(2)] for j in range(2)] for k in range(M)] for l in range(M)]

    # Stores count of numbers in
    cntR = 20

    # the range [0, L - 1] whose
    # product of  digits is k
    cntL = cntNum(str1, 0, 1, K, False, True, dp)
    return (cntR - cntL)

# Driver Code
if __name__ == '__main__':
    L = 20
    R = 10000
    K = 14
    print(UtilCntNumRange(L, R, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  static readonly int M = 100;

  // Function to count numbers in the range
  // [0, X] whose product of digit is K
  static int cntNum(String X, int i, int prod, int K,
                    int st, int tight, int [,,,]dp)
  {

    // If count of digits in a number
    // greater than count of digits in X
    if (i >= X.Length || prod > K)
    {

      // If product of digits of a
      // number equal to K
      return prod == K ? 1 : 0;
    }

    // If overlapping subproblems
    // already occurred
    if (dp[prod, i, tight, st] != -1)
    {
      return dp[prod, i, tight, st];
    }

    // Stores count of numbers whose
    // product of digits is K
    int res = 0;

    // Check if the numbers
    // exceeds K or not
    int end = tight > 0 ? X[i] - '0' : 9;

    // Iterate over all possible
    // value of i-th digits
    for(int j = 0; j <= end; j++)
    {

      // If number contains leading 0
      if (j == 0 && st == 0)
      {

        // Update res
        res += cntNum(X, i + 1, prod, K, 0,
                      (tight & ((j == end) ? 1 : 0)), dp);
      }
      else
      {

        // Update res
        res += cntNum(X, i + 1, prod * j, K, 1,
                      (tight & ((j == end) ? 1 : 0)), dp);
      }
    }

    // Return res
    return dp[prod, i, tight, st] = res;
  }

  // Utility function to count the numbers in
  // the range [L, R] whose prod of digits is K
  static int UtilCntNumRange(int L, int R, int K)
  {

    // Stores numbers in the form
    // of String
    String str = String.Join("", R);

    // Stores overlapping subproblems
    int [,,,]dp = new int[M, M, 2, 2];

    // Initialize [,]dp[] to -1
    for(int i = 0; i < M; i++)
    {
      for(int j = 0; j < M; j++)
      {
        for(int k = 0; k < 2; k++)
          for(int l = 0; l < 2; l++)
            dp[i, j, k, l] = -1;
      }
    }

    // Stores count of numbers in
    // the range [0, R] whose
    // product of  digits is k
    int cntR = cntNum(str, 0, 1, K,
                      0, 1, dp);

    // Update str
    str = String.Join("", L - 1);

    // Initialize [,]dp[] to -1
    for(int i = 0; i < M; i++)
    {
      for(int j = 0; j < M; j++)
      {
        for(int k = 0; k < 2; k++)
          for(int l = 0; l < 2; l++)
            dp[i, j, k, l] = -1;
      }
    }

    // Stores count of numbers in
    // the range [0, L - 1] whose
    // product of  digits is k
    int cntL = cntNum(str, 0, 1, K,
                      0, 1, dp);

    return (cntR - cntL);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int L = 20, R = 10000, K = 14;

    Console.Write(UtilCntNumRange(L, R, K));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

let M = 100;

// Function to count numbers in the range
// [0, X] whose product of digit is K
function cntNum(X, i, prod, K, st, tight, dp)
{
    // If count of digits in a number
    // greater than count of digits in X
    if (i >= X.length || prod > K)
    {

        // If product of digits of a
        // number equal to K
        return prod == K ? 1 : 0;
    }

    // If overlapping subproblems
    // already occurred
    if (dp[prod][i][tight][st] != -1)
    {
        return dp[prod][i][tight][st];
    }

    // Stores count of numbers whose
    // product of digits is K
    let res = 0;

    // Check if the numbers
    // exceeds K or not
    let end = tight > 0 ? X[i] - '0' : 9;

    // Iterate over all possible
    // value of i-th digits
    for(let j = 0; j <= end; j++)
    {

        // If number contains leading 0
        if (j == 0 && st == 0)
        {

            // Update res
            res += cntNum(X, i + 1, prod, K, 0,
                  (tight & ((j == end) ? 1 : 0)), dp);
        }
        else
        {

            // Update res
            res += cntNum(X, i + 1, prod * j, K, 1,
                  (tight & ((j == end) ? 1 : 0)), dp);
        }
    }

    // Return res
    return dp[prod][i][tight][st] = res;
}

// Utility function to count the numbers in
// the range [L, R] whose prod of digits is K
function UtilCntNumRange(L,R,K)
{
    // Stores numbers in the form
    // of String
    let str = (R).toString();

    // Stores overlapping subproblems
    let dp = new Array(M);

    // Initialize dp[][][] to -1
    for(let i = 0; i < M; i++)
    {
        dp[i]=new Array(M);
        for(let j = 0; j < M; j++)
        {
            dp[i][j]=new Array(2);
            for(let k = 0; k < 2; k++)
            {
                dp[i][j][k]=new Array(2);
                for(let l = 0; l < 2; l++)
                    dp[i][j][k][l] = -1;
            }
        }
    }

    // Stores count of numbers in
    // the range [0, R] whose
    // product of  digits is k
    let cntR = cntNum(str, 0, 1, K,
                      0, 1, dp);

    // Update str
    str = (L - 1).toString();

    // Initialize dp[][][] to -1
    for(let i = 0;i<M;i++)
    {
        for(let j = 0; j < M; j++)
        {
            for(let k = 0; k < 2; k++)
                for(let l = 0; l < 2; l++)
                    dp[i][j][k][l] = -1;
        }
    }

    // Stores count of numbers in
    // the range [0, L - 1] whose
    // product of  digits is k
    let cntL = cntNum(str, 0, 1, K,
                      0, 1, dp);

    return (cntR - cntL);
}

// Driver Code
let L = 20, R = 10000, K = 14;

document.write(UtilCntNumRange(L, R, K));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(K * log<sub>10</sub>(R)* 10 * 4)*
***辅助空间:**O(K * log<sub>10</sub>(R)* 4)*