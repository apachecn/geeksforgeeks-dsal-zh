# 给定范围查询的按位“与”非零范围内的最小删除量

> 原文:[https://www . geeksforgeeks . org/范围内最小移除量对给定范围的查询进行按位运算和非零运算/](https://www.geeksforgeeks.org/minimum-removals-in-range-to-make-bitwise-and-non-zero-for-given-range-queries/)

给定一个 **Q** 范围查询的[数组](https://www.geeksforgeeks.org/array-data-structure/) **查询[][]** ，任务是从范围**【l，r】**中找到最小删除量，使得范围的[位**和**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 为非零值。

**示例:**

> **输入:**查询[][] = { {1，5}、{3，4}、{5，10}、{10，15}}
> **输出:** 2 1 3 0
> **解释:**T8】查询-1: l = 1，r = 5 {1，2，3，4，5} (2，4)应该被移除，以使数组的 AND 非零，因此最小移除量为 2。
> 查询-2: l = 3，r = 4 {3，4}应该移除 3 或 4，以使数组的“与”非零，因此最小移除量为 1。
> 查询-3: l = 5，r = 10 {5，6，7，8，9，10} (5，6，7)或(8，9，10)应被删除，以使范围的“与”不为零。最低清除量。
> Query-4: l = 10，r = 15 {10，11，12，13，14，15}数组的 AND 最初为非零，因此 0 个删除。
> 
> **输入:**查询[][] = { {100，115}，{30，40}，{101，190 } }；
> T3【输出: 0 2 27

**简单方法:**这可以通过[遍历每个范围](https://www.geeksforgeeks.org/range-based-loop-c/)并检查具有公共设置位的范围内元素的最大计数，并从元素的总计数中删除该计数，即**(r–l+1)**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function the find the minimum removals
// to make the bitwise AND of range non-zero
void solve_queries(vector<vector<int> > q)
{
    for (int i = 0; i < q.size(); i++) {
        int l = q[i][0];
        int r = q[i][1];

        // Initialize the max_set to check
        // what count of set bit majority of
        // numbers in the range was set
        int max_set = 0;
        for (int i = 0; i < 31; i++) {
            int cnt = 0;
            for (int j = l; j <= r; j++) {

                // Check if is set
                if ((1 << i) & j) {
                    cnt++;
                }
            }
            max_set = max(max_set, cnt);
        }

        // Total length of range - count of
        // max numbers having 1 bit set in range
        cout << (r - l + 1) - max_set << " ";
    }
}

// Driver Code
int main()
{
    // Initialize the queries
    vector<vector<int> > queries
        = { { 1, 5 }, { 3, 4 }, { 5, 10 }, { 10, 15 } };

    solve_queries(queries);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;
public class GFG
{

  // Function the find the minimum removals
  // to make the bitwise AND of range non-zero
  static void solve_queries(int [][]q)
  {
    for (int i = 0; i < q.length; i++) {
      int l = q[i][0];
      int r = q[i][1];

      // Initialize the max_set to check
      // what count of set bit majority of
      // numbers in the range was set
      int max_set = 0;
      for (int k = 0; k < 31; k++) {
        int cnt = 0;
        for (int j = l; j <= r; j++) {

          // Check if is set
          if (((1 << k) & j) != 0) {
            cnt++;
          }
        }
        max_set = Math. max(max_set, cnt);
      }

      // Total length of range - count of
      // max numbers having 1 bit set in range
      System.out.print((r - l + 1) - max_set + " ");
    }
  }

  // Driver code
  public static void main(String args[])
  {
    // Initialize the queries
    int [][]queries
      = { { 1, 5 }, { 3, 4 }, { 5, 10 }, { 10, 15 } };

    solve_queries(queries);
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function the find the minimum removals
// to make the bitwise AND of range non-zero
const solve_queries = (q) => {

    for(let i = 0; i < q.length; i++)
    {
        let l = q[i][0];
        let r = q[i][1];

        // Initialize the max_set to check
        // what count of set bit majority of
        // numbers in the range was set
        let max_set = 0;
        for(let i = 0; i < 31; i++)
        {
            let cnt = 0;
            for(let j = l; j <= r; j++)
            {

                // Check if is set
                if ((1 << i) & j)
                {
                    cnt++;
                }
            }
            max_set = Math.max(max_set, cnt);
        }

        // Total length of range - count of
        // max numbers having 1 bit set in range
        document.write(`${(r - l + 1) - max_set} `);
    }
}

// Driver Code

// Initialize the queries
let queries = [ [ 1, 5 ], [ 3, 4 ],
                [ 5, 10 ], [ 10, 15 ] ];

solve_queries(queries);

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
2 1 3 0 
```

***时间复杂度:** O (31 * Q * n)其中 n 为最大范围的长度。*
***辅助空间:** O(1)*

**高效方法:**该方法基于[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)和[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术。这可以通过在 31 位的每个位置使用 **dp[]** 阵列存储总设置位的计数直到该范围来实现。这里 **dp[i][j]** 的状态是指从**【1，I】**到 **i** 的 jth 位位置的总设定位。按照以下步骤解决上述问题:

*   使用**前缀和**调用 **count_set_bits()** 函数[预先计算 **dp[][]** 数组。](https://www.geeksforgeeks.org/functions-in-c/)
*   现在[遍历查询](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)并分配 **l = q[i][0]，r = q[i][1]** 。
    *   初始化 **max_set = INT_MIN** 以存储设置了**第 j 位**的范围内元素的最大计数。
    *   [迭代**【0，30】**的位](https://www.geeksforgeeks.org/c-program-to-count-zeros-and-ones-in-binary-representation-of-a-number/)。
    *   计算由**total _ set =(DP[r][j]–DP[l–1][j])**设置的第**j-位**的元素数量。
    *   通过取 **max(max_set，total_set)** ，存储第 **j 位**位设置的元素的最大计数。
*   从总长度 **(r-l+1)** 中减去 **max_set** 打印所需的最小清除量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[200005][31];

// Function to build the dp array
// which stores the set bits for
// each bit position till 200005.
void count_set_bits()
{
    int N = 2e5 + 5;
    for (int i = 1; i < N; i++) {
        for (int j = 0; j <= 30; j++) {
            // If j th bit is set assign
            // dp[i][j] =1 where dp[i][j] means
            // number of jth bits set till i
            if (i & (1 << j))
                dp[i][j] = 1;

            // Calculate the pefix sum
            dp[i][j] += dp[i - 1][j];
        }
    }
}

// Function to solve the queries
void solve_queries(vector<vector<int> > q)
{
    // Call the function to
    // precalculate the dp array
    count_set_bits();
    for (int i = 0; i < q.size(); i++) {

        int l = q[i][0];
        int r = q[i][1];

        // Initialize the max_set = INT_MIN to
        // check what count of set bit
        // majority of numbers in the range was set
        int max_set = INT_MIN;

        // For each bit check the
        // maximum numbers in the range
        // having the j th bit set
        for (int j = 0; j <= 30; j++) {
            int total_set = (dp[r][j] - dp[l - 1][j]);

            max_set = max(max_set, total_set);
        }

        // Total length of range - count of max
        // numbers having 1 bit set in the range
        cout << (r - l + 1) - max_set << " ";
    }
}

// Driver Code
int main()
{

    // Initialize the queries
    vector<vector<int> > queries
        = { { 1, 5 }, { 3, 4 }, { 5, 10 }, { 10, 15 } };

    solve_queries(queries);
    return 0;
}
```

**Output**

```
2 1 3 0 
```

***时间复杂度:** O(31 * Q)*
***辅助空间:** O(n)*