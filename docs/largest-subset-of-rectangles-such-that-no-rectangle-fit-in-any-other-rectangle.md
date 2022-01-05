# 矩形的最大子集，使得没有矩形适合任何其他矩形

> 原文:[https://www . geeksforgeeks . org/最大矩形子集-这样-没有矩形适合任何其他矩形/](https://www.geeksforgeeks.org/largest-subset-of-rectangles-such-that-no-rectangle-fit-in-any-other-rectangle/)

给定 **N** 矩形的**高度**和**宽度**。任务是找到最大子集的大小，使得没有一对矩形彼此适合。**注意**如果 **H1 ≤ H2** 和 **W1 ≤ W2** ，则矩形 1 适合矩形 2。
**示例:**

> **输入:** arr[] = {{1，3}、{2，2}、{1，3}}
> **输出:** 2
> 所需的子集为{{1，3}、{2，2}}
> {1，3}只包含一次，因为它可以放入{1，3}
> **输入:** arr[] = {{1，5}、{2，4}、{1，1}、{3，3 } } }

**方式:**上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)解决。最初，我们可以根据高度对 N 对进行排序。递归函数可以写成两种状态。
第一种状态是，如果当前矩形不适合前一个矩形，反之亦然，那么我们调用下一个状态，当前矩形是前一个矩形，并移动到下一个矩形。

> DP[现在][以前] =最大值(DP[现在][以前]，1+DP[现在+1][现在])

如果它确实适合，我们调用上一个矩形的下一个状态，并移动到下一个矩形。

> DP[现在][以前] =最大值(DP[现在][以前]，DP[现在+1][以前])

[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)还可以用来避免重复调用相同的状态。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 10
int dp[N][N];

// Recursive function to get the largest subset
int findLongest(pair<int, int> a[], int n,
                int present, int previous)
{
    // Base case when it exceeds
    if (present == n) {
        return 0;
    }

    // If the state has been visited previously
    else if (previous != -1) {
        if (dp[present][previous] != -1)
            return dp[present][previous];
    }

    // Initialize
    int ans = 0;

    // No elements in subset yet
    if (previous == -1) {

        // First state which includes current index
        ans = 1 + findLongest(a, n,
                              present + 1, present);

        // Second state which does not include current index
        ans = max(ans, findLongest(a, n,
                                   present + 1, previous));
    }
    else {
        int h1 = a[previous].first;
        int h2 = a[present].first;
        int w1 = a[previous].second;
        int w2 = a[present].second;

        // If the rectangle fits in, then do not include
        // the current index in subset
        if ((h1 <= h2 && w1 <= w2)) {
            ans = max(ans, findLongest(a, n,
                                       present + 1, previous));
        }
        else {

            // First state which includes current index
            ans = 1 + findLongest(a, n,
                                  present + 1, present);

            // Second state which does not include current index
            ans = max(ans, findLongest(a, n,
                                       present + 1, previous));
        }
    }

    return dp[present][previous] = ans;
}

// Function to get the largest subset
int getLongest(pair<int, int> a[], int n)
{
    // Initialize the DP table with -1
    memset(dp, -1, sizeof dp);

    // Sort the array
    sort(a, a + n);

    // Get the answer
    int ans = findLongest(a, n, 0, -1);
    return ans;
}

// Driver code
int main()
{

    // (height, width) pairs
    pair<int, int> a[] = { { 1, 5 },
                           { 2, 4 },
                           { 1, 1 },
                           { 3, 3 } };
    int n = sizeof(a) / sizeof(a[0]);

    cout << getLongest(a, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to get the
# largest subset
def findLongest(a, n, present, previous):

    # Base case when it exceeds
    if present == n:
        return 0

    # If the state has been visited
    # previously
    elif previous != -1:
        if dp[present][previous] != -1:
            return dp[present][previous]

    # Initialize
    ans = 0

    # No elements in subset yet
    if previous == -1:

        # First state which includes
        # current index
        ans = 1 + findLongest(a, n, present + 1,
                                    present)

        # Second state which does not
        # include current index
        ans = max(ans, findLongest(a, n, present + 1,
                                         previous))

    else:
        h1 = a[previous][0]
        h2 = a[present][0]
        w1 = a[previous][1]
        w2 = a[present][1]

        # If the rectangle fits in, then do
        # not include the current index in subset
        if h1 <= h2 and w1 <= w2:
            ans = max(ans, findLongest(a, n, present + 1,
                                             previous))

        else:

            # First state which includes
            # current index
            ans = 1 + findLongest(a, n, present + 1,
                                        present)

            # Second state which does not
            # include current index
            ans = max(ans, findLongest(a, n, present + 1,
                                             previous))

    dp[present][previous] = ans
    return ans

# Function to get the largest subset
def getLongest(a, n):

    # Sort the array
    a.sort()

    # Get the answer
    ans = findLongest(a, n, 0, -1)
    return ans

# Driver code
if __name__ == "__main__":

    # (height, width) pairs
    a = [[1, 5], [2, 4], [1, 1], [3, 3]]

    N = 10

    # Initialize the DP table with -1
    dp = [[-1 for i in range(N)]
              for j in range(N)]

    n = len(a)
    print(getLongest(a, n))

# This code is contributed
# by Rituraj Jain
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var N = 10;
var dp = Array.from(Array(N), ()=>Array(N).fill(-1));

// Recursive function to get the largest subset
function findLongest(a, n, present, previous)
{
    // Base case when it exceeds
    if (present == n) {
        return 0;
    }

    // If the state has been visited previously
    else if (previous != -1) {
        if (dp[present][previous] != -1)
            return dp[present][previous];
    }

    // Initialize
    var ans = 0;

    // No elements in subset yet
    if (previous == -1) {

        // First state which includes current index
        ans = 1 + findLongest(a, n,
                              present + 1, present);

        // Second state which does not include current index
        ans = Math.max(ans, findLongest(a, n,
                                   present + 1, previous));
    }
    else {
        var h1 = a[previous][0];
        var h2 = a[present][0];
        var w1 = a[previous][1];
        var w2 = a[present][1];

        // If the rectangle fits in, then do not include
        // the current index in subset
        if ((h1 <= h2 && w1 <= w2)) {
            ans = Math.max(ans, findLongest(a, n,
                                       present + 1, previous));
        }
        else {

            // First state which includes current index
            ans = 1 + findLongest(a, n,
                                  present + 1, present);

            // Second state which does not include current index
            ans = Math.max(ans, findLongest(a, n,
                                       present + 1, previous));
        }
    }

    return dp[present][previous] = ans;
}

// Function to get the largest subset
function getLongest(a, n)
{
    // Initialize the DP table with -1
    dp = Array.from(Array(N), ()=>Array(N).fill(-1));

    // Sort the array
    a.sort((a,b)=>a-b);

    // Get the answer
    var ans = findLongest(a, n, 0, -1);
    return ans;
}

// Driver code
// (height, width) pairs
var a = [ [ 1, 5 ],
          [ 2, 4 ],
          [ 1, 1 ],
          [ 3, 3 ] ];
var n = a.length;
document.write( getLongest(a, n));

</script>
```

**Output:** 

```
3
```