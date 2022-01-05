# 从左侧只能看到 K 条的方式数

> 原文:[https://www . geeksforgeeks . org/路数-这样-只有-k-bar-从左侧可见/](https://www.geeksforgeeks.org/number-of-ways-such-that-only-k-bars-are-visible-from-the-left/)

给定从 **1** 到 **N** 的高度的数字 **K** 和 **N** 条，任务是找到排列 **N** 条的方法的数量，使得从左侧只能看到 **K** 条。

**示例**:

> **输入:** N=4，K=3
> **输出:**
> 6
> **说明:**从左边只能看到 3 条的 6 种排列是:
> 
> *   1 2 4 <u>3</u>
> *   1 3 <u>2</u> 4
> *   1 3 4 <u>2</u>
> *   2 <u>1</u> 3 4
> *   2 3 <u>1</u> 4
> *   2 3 4 <u>1</u>
> 
> 下划线条不可见。
> 
> **输入:** N=5，K = 2
> T3】输出:T5】50

**天真的方法**:天真的方法是检查 **1 到 N** 的所有排列，并检查从左侧可见的小节数是否为 **K** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number
// of bars that are visible from
// the left for a particular arrangement
int noOfbarsVisibleFromLeft(vector<int> v)
{
    int last = 0, ans = 0;
    for (auto u : v)

        // If current element is greater
// than the last greater element,
// it is visible
        if (last < u) {
            ans++;
            last = u;
        }
    return ans;
}

// Function to calculate the number
// of rearrangements where
// K bars are visiblef from the left
int KvisibleFromLeft(int N, int K)
{
    // Vector to store current permutation
    vector<int> v(N);
    for (int i = 0; i < N; i++)
        v[i] = i + 1;
    int ans = 0;

    // Check for all permutations
    do {

        // If current permutation meets
// the conditions, increment answer
        if (noOfbarsVisibleFromLeft(v) == K)
            ans++;
    } while (next_permutation(v.begin(), v.end()));

    return ans;
}

// Driver code
int main()
{
    // Input
    int N = 5, K = 2;

    // Function call
    cout << KvisibleFromLeft(N, K) << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the number
# of bars that are visible from
# the left for a particular arrangement
def noOfbarsVisibleFromLeft(v):
    last = 0
    ans = 0

    for u in v:
    # If current element is greater
    # than the last greater element,
    # it is visible
        if (last < u):
            ans += 1
            last = u

    return ans

def nextPermutation(nums):
    i = len(nums) - 2
    while i > -1:
        if nums[i] < nums[i + 1]:
            j = len(nums) - 1
            while j > i:
                if nums[j] > nums[i]:
                    break
                j -= 1
            nums[i], nums[j] = nums[j], nums[i]
            break
        i -= 1
    nums[i + 1:] = reversed(nums[i + 1:])
    return nums

# Function to calculate the number
# of rearrangements where
# K bars are visiblef from the left
def KvisibleFromLeft(N, K):
    # Vector to store current permutation
    v = [0]*(N)
    for i in range(N):
        v[i] = i + 1
    ans = 0

    temp = list(v)

    # Check for all permutations
    while True:
        # If current permutation meets
# the conditions, increment answer
        if (noOfbarsVisibleFromLeft(v) == K):
            ans += 1
        v = nextPermutation(v)

        if v == temp:
            break

    return ans

# Driver code
if __name__ == '__main__':
    # Input
    N = 5
    K = 2

    # Function call
    print (KvisibleFromLeft(N, K))

# This code is contributed by mohit kumar 29.
```

**Output**

```
50
```

***时间复杂度:** O(N！)*
***辅助空间:** O(N)*

**有效方法:**有效方法是使用[递归](https://www.geeksforgeeks.org/recursion/)。按照以下步骤解决问题:

*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **KvisibleFromLeft()** ，该函数将 **N** 和 **K** 作为输入参数，并执行以下操作:
    *   基本案例:
        *   如果 **N** 等于 **K** ，则有一种排列小节的方法，按升序排列。所以，返回 **1** 。
        *   如果 **K==1** ，则有 **(N-1)！**条的排列方式，因为最长的条放置在第一个位置，剩余的 **N-1** 条可以放置在剩余的 **N-1** 位置的任何位置。所以，返回 **(N-1)！**。
    *   对于递归，有两种情况:
        *   最小的条可以放在第一个位置，那么剩下的 **N-1** 条中，只需要 **K-1** 条可见即可。因此，答案与排列 **N-1** 条使得 **K-1** 条可见的方法数量相同。因此，这种情况递归调用 **KvisibleFromLeft(N-1，** **K-1)** 。
        *   除了第一个位置外，最小的杆可以放置在任何一个 **N-1** 位置。这将隐藏最小的小节，因此，答案将与排列 **N-1** 小节的方式数量相同，以便使 **K** 小节可见。因此，这种情况下递归调用 **(N-1)*KvisibleFromLeft(N-1，K)。**

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number of permutations of
// N, where only K bars are visible from the left.
int KvisibleFromLeft(int N, int K)
{

    // Only ascending order is possible
    if (N == K)
        return 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1) {
        int ans = 1;
        for (int i = 1; i < N; i++)
            ans *= i;
        return ans;
    }

    // Recursing
    return KvisibleFromLeft(N - 1, K - 1)
           + (N - 1) * KvisibleFromLeft(N - 1, K);
}
// Driver code
int main()
{
    // Input
    int N = 5, K = 2;

    // Function call
    cout << KvisibleFromLeft(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate the number of
// permutations of N, where only K bars
// are visible from the left.
static int KvisibleFromLeft(int N, int K)
{

    // Only ascending order is possible
    if (N == K)
        return 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1)
    {
        int ans = 1;
        for(int i = 1; i < N; i++)
            ans *= i;

        return ans;
    }

    // Recursing
    return KvisibleFromLeft(N - 1, K - 1) +
        (N - 1) * KvisibleFromLeft(N - 1, K);
}

// Driver code
public static void main(String[] args)
{

    // Input
    int N = 5, K = 2;

    // Function call
    System.out.println(KvisibleFromLeft(N, K));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Function to calculate the number of permutations of
# N, where only K bars are visible from the left.
def KvisibleFromLeft(N, K):

    # Only ascending order is possible
    if (N == K):
        return 1

    # N is placed at the first position
    # The nest N-1 are arranged in (N-1)! ways
    if (K == 1):
        ans = 1
        for i in range(1, N, 1):
            ans *= i
        return ans

    # Recursing
    return KvisibleFromLeft(N - 1, K - 1) + (N - 1) * KvisibleFromLeft(N - 1, K)

# Driver code
if __name__ == '__main__':

    # Input
    N = 5
    K = 2

    # Function call
    print(KvisibleFromLeft(N, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to calculate the number of
// permutations of N, where only K bars
// are visible from the left.
static int KvisibleFromLeft(int N, int K)
{

    // Only ascending order is possible
    if (N == K)
        return 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1)
    {
        int ans = 1;
        for(int i = 1; i < N; i++)
            ans *= i;

        return ans;
    }

    // Recursing
    return KvisibleFromLeft(N - 1, K - 1) +
        (N - 1) * KvisibleFromLeft(N - 1, K);
}

// Driver code
public static void Main(String[] args)
{

    // Input
    int N = 5, K = 2;

    // Function call
    Console.Write(KvisibleFromLeft(N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to calculate the number of permutations of
// N, where only K bars are visible from the left.
function KvisibleFromLeft(N, K) {

    // Only ascending order is possible
    if (N == K)
        return 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1) {
        let ans = 1;
        for (let i = 1; i < N; i++)
            ans *= i;
        return ans;
    }

    // Recursing
    return KvisibleFromLeft(N - 1, K - 1)
        + (N - 1) * KvisibleFromLeft(N - 1, K);
}
// Driver code

// Input
let N = 5, K = 2;

// Function call
document.write(KvisibleFromLeft(N, K) + "<br>");

// This code is contributed by gfgking.
</script>
```

**Output**

```
50
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述递归可以[记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)，因此[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以使用，因为存在[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// dp array
int dp[1005][1005];

// Function to calculate the number
// of permutations of N, where
// only K bars are visible from the left.
int KvisibleFromLeft(int N, int K)
{
    // If subproblem has already
// been calculated, return
    if (dp[N][K] != -1)
        return dp[N][K];

    // Only ascending order is possible
    if (N == K)
        return dp[N][K] = 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1) {
        int ans = 1;
        for (int i = 1; i < N; i++)
            ans *= i;
        return dp[N][K] = ans;
    }

    // Recursing
    return dp[N][K]
           = KvisibleFromLeft(N - 1, K - 1)
             + (N - 1) * KvisibleFromLeft(N - 1, K);
}
// Driver code
int main()
{
    // Input
    int N = 5, K = 2;

    // Initialize dp array
    memset(dp, -1, sizeof(dp));

    // Function call
    cout << KvisibleFromLeft(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG{

// dp array
static int [][]dp = new int[1005][1005];

// Function to calculate the number
// of permutations of N, where
// only K bars are visible from the left.
static int KvisibleFromLeft(int N, int K)
{
    // If subproblem has already
// been calculated, return
    if (dp[N][K] != -1)
        return dp[N][K];

    // Only ascending order is possible
    if (N == K)
        return dp[N][K] = 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1) {
        int ans = 1;
        for (int i = 1; i < N; i++)
            ans *= i;
        return dp[N][K] = ans;
    }

    // Recursing
    return dp[N][K]
           = KvisibleFromLeft(N - 1, K - 1)
             + (N - 1) * KvisibleFromLeft(N - 1, K);
}
// Driver code
public static void main(String[] args)
{
    // Input
    int N = 5, K = 2;

    // Initialize dp array
    for(int i = 0; i < 1005; i++)
  {
    for (int j = 0; j < 1005; j++)
    {
      dp[i][j] = -1;
    }
  }

    // Function call
    System.out.print( KvisibleFromLeft(N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# dp array
dp = [[0 for i in range(1005)] for j in range(1005)]

# Function to calculate the number
# of permutations of N, where
# only K bars are visible from the left.
def KvisibleFromLeft(N, K):

    # If subproblem has already
    # been calculated, return
    if (dp[N][K] != -1):
        return dp[N][K]

    # Only ascending order is possible
    if (N == K):
        dp[N][K] = 1
        return dp[N][K]

    # N is placed at the first position
    # The nest N-1 are arranged in (N-1)! ways
    if (K == 1):
        ans = 1
        for i in range(1, N):
            ans *= i
        dp[N][K] = ans
        return dp[N][K]

    # Recursing
    dp[N][K] = KvisibleFromLeft(N - 1, K - 1) + (N - 1) * KvisibleFromLeft(N - 1, K)
    return dp[N][K]

# Input
N, K = 5, 2

# Initialize dp array
for i in range(1005):
    for j in range(1005):
        dp[i][j] = -1

# Function call
print( KvisibleFromLeft(N, K))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG{

// dp array
static int [,]dp = new int[1005, 1005];

// Function to calculate the number
// of permutations of N, where
// only K bars are visible from the left.
static int KvisibleFromLeft(int N, int K)
{
    // If subproblem has already
// been calculated, return
    if (dp[N ,K] != -1)
        return dp[N,K];

    // Only ascending order is possible
    if (N == K)
        return dp[N,K] = 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1) {
        int ans = 1;
        for (int i = 1; i < N; i++)
            ans *= i;
        return dp[N,K] = ans;
    }

    // Recursing
    return dp[N,K]
           = KvisibleFromLeft(N - 1, K - 1)
             + (N - 1) * KvisibleFromLeft(N - 1, K);
}
// Driver code
public static void Main(String[] args)
{
    // Input
    int N = 5, K = 2;

    // Initialize dp array
    for(int i = 0; i < 1005; i++)
  {
    for (int j = 0; j < 1005; j++)
    {
      dp[i, j] = -1;
    }
  }

    // Function call
    Console.Write( KvisibleFromLeft(N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript implementation for
// the above approach

// dp array
let dp = new Array(1005).fill(0).map(
   () => new Array(1005).fill(-1));

// Function to calculate the number
// of permutations of N, where
// only K bars are visible from the left.
function KvisibleFromLeft(N, K)
{

    // If subproblem has already
    // been calculated, return
    if (dp[N][K] != -1)
        return dp[N][K];

    // Only ascending order is possible
    if (N == K)
        return dp[N][K] = 1;

    // N is placed at the first position
    // The nest N-1 are arranged in (N-1)! ways
    if (K == 1)
    {
        let ans = 1;

        for(let i = 1; i < N; i++)
            ans *= i;

        return dp[N][K] = ans;
    }

    // Recursing
    return dp[N][K] = KvisibleFromLeft(N - 1, K - 1) +
            (N - 1) * KvisibleFromLeft(N - 1, K);
}

// Driver code

// Input
let N = 5, K = 2;

// Function call
document.write(KvisibleFromLeft(N, K) + "<br>")

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
50
```

***时间复杂度:**O(NK)*
T5**辅助空间:** O(NK)