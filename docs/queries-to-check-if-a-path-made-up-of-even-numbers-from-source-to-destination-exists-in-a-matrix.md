# 检查从源到目的地的偶数路径是否存在于矩阵中的查询

> 原文:[https://www . geesforgeks . org/query-to-check-a-path-由从源到目的地的偶数组成-是否存在于矩阵中/](https://www.geeksforgeeks.org/queries-to-check-if-a-path-made-up-of-even-numbers-from-source-to-destination-exists-in-a-matrix/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **R[]** 和 **C[]** ，它们由 **N** 个整数组成，从而可以形成尺寸 **N x N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)，其索引 **(i，j)** 处的元素由 **(R[i] + C[j])** 给出，用于两个数组中所有可能的对。给定一个矩阵**查询[][]** ，每行代表一个类型为 **{A，B，X，Y}** 的查询，每个查询的任务是检查在仅由[偶数](https://www.geeksforgeeks.org/python-program-to-print-even-numbers-in-a-list/)组成的矩阵中是否存在从单元格 **(A，B)** 到 **(X，Y)** 的路径。如果发现是真的，打印“**是”**。否则，打印“**否”**。

***注:**对于从当前单元格 **(i，j)** 开始的路径，唯一可能的移动是 **(i + 1，j)** 、 **(i，j + 1)** 、**(I–1，j)** 和 **(i，j–1)**。*

**示例:**

> **输入:** R[] = {6，2，7，8，3}，C[] = {3，4，8，5，1}，query[][]= { { 2 2 1 3 }，{4 2 4 3}，{5 1 3 4}}
> **输出:**是否
> **解释:**
> 形成的矩阵为:
> {{9，10，14，11，7}
> {5，6，10 4}}
> **查询 1:** 存在一条从单元格(2，2)到(1，3)的偶数路径，所有单元格为偶数。 路径是(2，2) - > (2，3) - > (1，3)。
> **查询 2:** 存在一条从单元格(4，2)到(4，3)的偶数路径，所有单元格为偶数。路径是(4，2) - > (4，3)。
> **查询 3:** 即使所有元素都存在，也没有路径。
> 
> **输入:** R[] = {1，2，4，8，5}，C[] = {2，5，9，7，6}，query[][]= { { 2 2 2 1 3 }，{1 4 1 3}，{ 5 1 3 4 } }
> T3】输出:否是否
> T6】解释:T8】形成的矩阵为:
> {{3，6，10，8，7}
> {4，7，11，9
> **查询 2:** 存在一条从单元格(1，4)到(1，3)的偶数路径，所有单元格为偶数。路径是(1，4) - > (1，3)。
> **查询 3:** 即使所有元素都存在，也没有路径。

**方法:**思想是预先计算数组 **R[]** 和 **C[]** 的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，然后在给定条件下检查有效路径。以下是步骤:

1.  其思想是只有当 **R[r]** 和 **R[r + 1]** 的宇称相同时，才能从单元格 **(r，c)** 迭代到 **(r + 1，c)** 因为只有一个元素在变化。
2.  同理，对于 **(r，c)** 到 **(r，c + 1)** 的列来说， **C** 和 **C** 的宇称应该相同。
3.  对**(r–1，c)** 和 **(r，c–1)**执行上述操作。
4.  现在，对于每个查询，继续检查从 **r = (min(A，B)** 到 **max(A，B))** 的所有元素是否具有相同的奇偶性，以及从 **c = (min(X，Y)** 到 **max(X，Y))** 的所有元素是否具有相同的奇偶性。通过预计算元素奇偶校验的前缀和，可以在每个查询中检查 O(1)次。
5.  如果上述条件对所有单元格都成立，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find whether the path
// exists with all element even or not
void answerQueries(int n, int q,
                vector<int>& a,
                vector<int>& b,
                vector<vector<int> >& Queries)
{
    // Add 0 to beginning to make
    // 1-based-indexing
    a.insert(a.begin(), 0);
    b.insert(b.begin(), 0);

    // Change elements based on parity
    // and take prefix sum

    // 1 is odd and 0 is even

    // Traverse the array R[]
    for (int i = 1; i <= n; i++) {

        // Taking & to check parity
        if (a[i] & 1)
            a[i] = 1;
        else
            a[i] = 0;

        // Build prefix sum array
        a[i] += a[i - 1];
    }

    // Traverse the array C[]
    for (int i = 1; i <= n; i++) {

        // Taking & to check parity
        if (b[i] & 1)
            b[i] = 1;
        else
            b[i] = 0;

        // Build prefix sum array
        b[i] += b[i - 1];
    }

    // Traverse the matrix Queries[][]
    for (int i = 0; i < q; i++) {

        int ra = Queries[i][0];
        int ca = Queries[i][1];
        int rb = Queries[i][2];
        int cb = Queries[i][3];

        int r2 = max(ra, rb), r1 = min(ra, rb);
        int c2 = max(ca, cb), c1 = min(ca, cb);

        // Check if all numbers are of
        // same parity between (r1 to r2)
        if ((a[r2] - a[r1 - 1] == 0)
            || (a[r2] - a[r1 - 1]
                == r2 - r1 + 1)) {

            // Check if all numbers are of
            // same parity between (r1 to r2)
            if ((b[c2] - b[c1 - 1] == 0)
                || (b[c2] - b[c1 - 1]
                    == c2 - c1 + 1)) {

                // Path exists
                cout << "Yes" << ' ';
                continue;
            }
        }

        // No path exists
        cout << "No" << ' ';
    }
}

// Driver Code
int main()
{
    // Given N, Q
    int N = 5, Q = 3;

    // Given array R[] and C[]
    vector<int> R{ 6, 2, 7, 8, 3 };
    vector<int> C{ 3, 4, 8, 5, 1 };

    // Given queries[][]
    vector<vector<int> > Queries{ { 2, 2, 1, 3 },
                                { 4, 2, 4, 3 },
                                { 5, 1, 3, 4 } };

    // Function Call
    answerQueries(N, Q, R, C, Queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find whether the path
// exists with all element even or not
static void answerQueries(int n, int q,
                          int[] a, int[] b,
                          int[][] Queries)
{

    // Add 0 to beginning to make
    // 1-based-indexing
    // a[0]=0;
    // b[0]=0;

    // Change elements based on parity
    // and take prefix sum

    // 1 is odd and 0 is even

    // Traverse the array R[]
    for(int i = 1; i <= n; i++)
    {

        // Taking & to check parity
        if ((a[i] & 1) != 0)
            a[i] = 1;
        else
            a[i] = 0;

        // Build prefix sum array
        a[i] += a[i - 1];
    }

    // Traverse the array C[]
    for(int i = 1; i <= n; i++)
    {

        // Taking & to check parity
        if ((b[i] & 1) != 0)
            b[i] = 1;
        else
            b[i] = 0;

        // Build prefix sum array
        b[i] += b[i - 1];
    }

    // Traverse the matrix Queries[][]
    for(int i = 0; i < q; i++)
    {
        int ra = Queries[i][0];
        int ca = Queries[i][1];
        int rb = Queries[i][2];
        int cb = Queries[i][3];

        int r2 = Math.max(ra, rb),
            r1 = Math.min(ra, rb);
        int c2 = Math.max(ca, cb),
            c1 = Math.min(ca, cb);

        // Check if all numbers are of
        // same parity between (r1 to r2)
        if ((a[r2] - a[r1 - 1] == 0) ||
            (a[r2] - a[r1 - 1] == r2 - r1 + 1))
        {

            // Check if all numbers are of
            // same parity between (r1 to r2)
            if ((b[c2] - b[c1 - 1] == 0) ||
                (b[c2] - b[c1 - 1] == c2 - c1 + 1))
            {

                // Path exists
                System.out.print("Yes" + " ");
                continue;
            }
        }

        // No path exists
        System.out.print("No" + " ");
    }
}

// Driver Code
public static void main (String[] args)
throws java.lang.Exception
{

    // Given N, Q
    int N = 5, Q = 3;

    // Given array R[] and C[]
    int R[] = { 0, 6, 2, 7, 8, 3 };
    int C[] = { 0, 3, 4, 8, 5, 1 };

    // Given queries[][]
    int[][] Queries = { { 2, 2, 1, 3 },
                        { 4, 2, 4, 3 },
                        { 5, 1, 3, 4 }};

    // Function call
    answerQueries(N, Q, R, C, Queries);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find whether the path
# exists with all element even or not
def answerQueries(n, q, a, b, Queries):

    # Add 0 to beginning to make
    # 1-based-indexing
    # a[0]=0;
    # b[0]=0;
    # Change elements based on parity
    # and take prefix sum
    # 1 is odd and 0 is even
    # Traverse the array R
    for i in range(1, n + 1):

        # Taking & to check parity
        if ((a[i] & 1) != 0):
            a[i] = 1;
        else:
            a[i] = 0;

        # Build prefix sum array
        a[i] += a[i - 1];

    # Traverse the array C
    for i in range(1, n + 1):

        # Taking & to check parity
        if ((b[i] & 1) != 0):
            b[i] = 1;
        else:
            b[i] = 0;

        # Build prefix sum array
        b[i] += b[i - 1];

    # Traverse the matrix Queries
    for i in range(0, q):
        ra = Queries[i][0];
        ca = Queries[i][1];
        rb = Queries[i][2];
        cb = Queries[i][3];

        r2 = max(ra, rb); r1 = min(ra, rb);
        c2 = max(ca, cb); c1 = min(ca, cb);

        # Check if all numbers are of
        # same parity between (r1 to r2)
        if ((a[r2] - a[r1 - 1] == 0) or
            (a[r2] - a[r1 - 1] == r2 - r1 + 1)):

            # Check if all numbers are of
            # same parity between (r1 to r2)
            if ((b[c2] - b[c1 - 1] == 0) or
                (b[c2] - b[c1 - 1] == c2 - c1 + 1)):

                # Path exists
                print("Yes", end = " ");
                continue;

        # No path exists
        print("No", end = " ");

# Driver Code
if __name__ == '__main__':

    # Given N, Q
    N = 5;
    Q = 3;

    # Given array R and C
    R = [0, 6, 2, 7, 8, 3];
    C = [0, 3, 4, 8, 5, 1];

    # Given queries
    Queries = [[2, 2, 1, 3],
               [4, 2, 4, 3],
               [5, 1, 3, 4]];

    # Function call
    answerQueries(N, Q, R, C, Queries);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find whether the path
// exists with all element even or not
static void answerQueries(int n, int q,
                          int[] a, int[] b,
                          int[,] Queries)
{
  // Add 0 to beginning to make
  // 1-based-indexing
  // a[0]=0;
  // b[0]=0;

  // Change elements based on parity
  // and take prefix sum

  // 1 is odd and 0 is even

  // Traverse the array R[]
  for(int i = 1; i <= n; i++)
  {
    // Taking & to check parity
    if ((a[i] & 1) != 0)
      a[i] = 1;
    else
      a[i] = 0;

    // Build prefix sum array
    a[i] += a[i - 1];
  }

  // Traverse the array C[]
  for(int i = 1; i <= n; i++)
  {
    // Taking & to check parity
    if ((b[i] & 1) != 0)
      b[i] = 1;
    else
      b[i] = 0;

    // Build prefix sum array
    b[i] += b[i - 1];
  }

  // Traverse the matrix Queries[,]
  for(int i = 0; i < q; i++)
  {
    int ra = Queries[i, 0];
    int ca = Queries[i, 1];
    int rb = Queries[i, 2];
    int cb = Queries[i, 3];

    int r2 = Math.Max(ra, rb),
        r1 = Math.Min(ra, rb);
    int c2 = Math.Max(ca, cb),
        c1 = Math.Min(ca, cb);

    // Check if all numbers are of
    // same parity between (r1 to r2)
    if ((a[r2] - a[r1 - 1] == 0) ||
        (a[r2] - a[r1 - 1] == r2 - r1 + 1))
    {
      // Check if all numbers are of
      // same parity between (r1 to r2)
      if ((b[c2] - b[c1 - 1] == 0) ||
          (b[c2] - b[c1 - 1] == c2 - c1 + 1))
      {
        // Path exists
        Console.Write("Yes" + " ");
        continue;
      }
    }

    // No path exists
    Console.Write("No" + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given N, Q
  int N = 5, Q = 3;

  // Given array R[] and C[]
  int []R = {0, 6, 2, 7, 8, 3};
  int []C = {0, 3, 4, 8, 5, 1};

  // Given [,]queries
  int[,] Queries = {{2, 2, 1, 3},
                    {4, 2, 4, 3},
                    {5, 1, 3, 4}};

  // Function call
  answerQueries(N, Q, R, C, Queries);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find whether the path
// exists with all element even or not
function answerQueries(n, q, a, b,Queries)
{

    // Add 0 to beginning to make
    // 1-based-indexing
    // a[0]=0;
    // b[0]=0;

    // Change elements based on parity
    // and take prefix sum

    // 1 is odd and 0 is even

    // Traverse the array R[]
    for(let i = 1; i <= n; i++)
    {

        // Taking & to check parity
        if ((a[i] & 1) != 0)
            a[i] = 1;
        else
            a[i] = 0;

        // Build prefix sum array
        a[i] += a[i - 1];
    }

    // Traverse the array C[]
    for(let i = 1; i <= n; i++)
    {

        // Taking & to check parity
        if ((b[i] & 1) != 0)
            b[i] = 1;
        else
            b[i] = 0;

        // Build prefix sum array
        b[i] += b[i - 1];
    }

    // Traverse the matrix Queries[][]
    for(let i = 0; i < q; i++)
    {
        let ra = Queries[i][0];
        let ca = Queries[i][1];
        let rb = Queries[i][2];
        let cb = Queries[i][3];

        let r2 = Math.max(ra, rb),
            r1 = Math.min(ra, rb);
        let c2 = Math.max(ca, cb),
            c1 = Math.min(ca, cb);

        // Check if all numbers are of
        // same parity between (r1 to r2)
        if ((a[r2] - a[r1 - 1] == 0) ||
            (a[r2] - a[r1 - 1] == r2 - r1 + 1))
        {

            // Check if all numbers are of
            // same parity between (r1 to r2)
            if ((b[c2] - b[c1 - 1] == 0) ||
                (b[c2] - b[c1 - 1] == c2 - c1 + 1))
            {

                // Path exists
                document.write("Yes" + " ");
                continue;
            }
        }

        // No path exists
        document.write("No" + " ");
    }
}

// Driver Code

     // Given N, Q
    let N = 5, Q = 3;

    // Given array R[] and C[]
    let R = [0, 6, 2, 7, 8, 3 ];
    let C = [0, 3, 4, 8, 5, 1 ];

    // Given queries[][]
    let Queries = [[2, 2, 1, 3],
                        [4, 2, 4, 3 ],
                        [5, 1, 3, 4 ]];

    // Function call
    answerQueries(N, Q, R, C, Queries);

 // This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
Yes Yes No 
```

***时间复杂度:** O(N + Q)*
***辅助空间:** O(1)*