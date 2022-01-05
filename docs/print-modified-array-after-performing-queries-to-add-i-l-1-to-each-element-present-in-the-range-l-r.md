# 在执行查询以将(I–L+1)添加到范围[L，R]

中存在的每个元素后，打印修改后的数组

> 原文:[https://www . geesforgeks . org/print-modified-array-执行查询后-add-I-l-1-to-每个元素-范围内存在-l-r/](https://www.geeksforgeeks.org/print-modified-array-after-performing-queries-to-add-i-l-1-to-each-element-present-in-the-range-l-r/)

给定由**N**T6】0s(*1 基索引*)和另一个数组**查询【】**组成的[数组**arr【】**，表格的每一行 **{L，R}** ，每个查询 **(L，R)** 的任务是在范围**上添加一个值**(I–L+1)****](https://www.geeksforgeeks.org/array-data-structure/)

**示例:**

> **输入:** arr[] = {0，0，0}，query[][] = {{1，3}，{2，3}}
> **输出:** 1 3 5
> **解释:**最初数组为{0，0，0}。
> **查询 1:** 涉及的指标范围:[1，3]。范围内每个索引 I 的值(I–1+1)为{1，2，3}。添加这些值会将数组修改为{1，2，3}。
> **查询 2:** 涉及的指标范围:[2，3]。范围内每个索引 I 的值(I–2+1)为{0，1，2}。添加这些值会将数组修改为{1，3，5}。
> 因此，修改后的数组为{1，3，5}。
> 
> **输入:** arr[] = {0，0，0，0，0，0，0}，查询[][] = {{1，7}，{3，6}，{4，5}}
> **输出:** 1 2 4 7 10 10 7

**天真方法:**解决给定问题的最简单方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的范围**【L，R】**并将值**(I–L+1)**添加到每个查询的范围内的每个元素。完成所有查询后，[打印修改后的数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)得到 **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform the given queries
// in the given empty array of size N
void updateQuery(vector<vector<int> > queries,
                 int N)
{
    // Initialize an array a[]
    vector<int> a(N + 1, 0);

    // Stores the size of the array
    int n = N + 1;

    int q = queries.size();

    // Traverse the queries
    for (int i = 0; i < q; i++) {

        // Starting index
        int l = queries[i][0];

        // Ending index
        int r = queries[i][1];

        // Increment each index from L to
        // R in a[] by (j - l + 1)
        for (int j = l; j <= r; j++) {
            a[j] += (j - l + 1);
        }
    }

    // Print the modified array
    for (int i = 1; i <= N; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    int N = 7;
    vector<vector<int> > queries
        = { { 1, 7 }, { 3, 6 }, { 4, 5 } };

    // Function Call
    updateQuery(queries, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to perform the given queries
// in the given empty array of size N
static void updateQuery(int [][]queries, int N)
{

    // Initialize an array a[]
    ArrayList<Integer> a = new ArrayList<Integer>();
    for(int i = 0; i < N + 1; i++)
        a.add(0);

    // Stores the size of the array
    int q = 3;

    // Traverse the queries
    for(int i = 0; i < q; i++)
    {

        // Starting index
        int l = queries[i][0];

        // Ending index
        int r = queries[i][1];

        // Increment each index from L to
        // R in a[] by (j - l + 1)
        for(int j = l; j <= r; j++)
        {
            a.set(j, a.get(j)+(j - l + 1));
        }
    }

    // Print the modified array
    for(int i = 1; i < a.size(); i++)
    {
        System.out.print(a.get(i) + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 7;
    int[][] queries =  { { 1, 7 },
                         { 3, 6 },
                         { 4, 5 } };

    // Function Call
    updateQuery(queries, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to perform the given queries
# in the given empty array of size N
def updateQuery(queries, N):

    # Initialize an array a[]
    a = [0 for i in range(N + 1)]

    # Stores the size of the array
    n = N + 1

    q = len(queries)

    # Traverse the queries
    for i in range(q):

        # Starting index
        l = queries[i][0]

        # Ending index
        r = queries[i][1]

        # Increment each index from L to
        # R in a[] by (j - l + 1)
        for j in range(l, r + 1, 1):
            a[j] += (j - l + 1)

    # Print the modified array
    for i in range(1, N + 1, 1):
        print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':
    N = 7
    queries =  [[1, 7],[3, 6],[4, 5]]

    # Function Call
    updateQuery(queries, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to perform the given queries
// in the given empty array of size N
static void updateQuery(int [,]queries, int N)
{

    // Initialize an array a[]
    List<int> a = new List<int>();
    for(int i = 0; i < N + 1; i++)
        a.Add(0);

    // Stores the size of the array
    int q = 3;

    // Traverse the queries
    for(int i = 0; i < q; i++)
    {

        // Starting index
        int l = queries[i, 0];

        // Ending index
        int r = queries[i, 1];

        // Increment each index from L to
        // R in a[] by (j - l + 1)
        for(int j = l; j <= r; j++)
        {
            a[j] += (j - l + 1);
        }
    }

    // Print the modified array
    for(int i = 1; i < a.Count; i++)
    {
        Console.Write(a[i] + " ");
    }
}

// Driver Code
public static void Main()
{
    int N = 7;
    int[,] queries = new int[3, 2] { { 1, 7 },
                                     { 3, 6 },
                                     { 4, 5 } };

    // Function Call
    updateQuery(queries, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

**Output:** 

```
1 2 4 7 10 10 7
```

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)进行优化。按照以下步骤解决此问题:

*   初始化一个数组**ans【】**，所有元素为 **0** ，以存储当前索引受查询影响的次数。
*   初始化一个数组 **res[]** ，所有元素为 **0** ，存储某个查询范围结束后要删除的值。
*   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**查询[]** ，并执行以下步骤:
    *   将 1 加到 **ans【查询[I][0]】**上，从 **ans【查询[I][1]+1】**中减去 **1** 。
    *   从 **res【查询[I][1]+1】**中减去**(查询[I][1]–查询[i][0] + 1)** 。
*   找到数组**和**的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **res[]** 并将每个元素 **res[i]** 更新为**RES[I]+RES[I–1]+ans[I]**。
*   完成上述步骤后，在执行给定查询后，将数组 **res[]** 打印为修改后的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform the given queries
// in the given empty array of size N
void updateQuery(vector<vector<int> > queries,
                 int N)
{
    // Stores the resultant array
    // and the difference array
    vector<int> ans(N + 2, 0),
        res(N + 2, 0);

    int q = queries.size();

    // Traverse the given queries
    for (int i = 0; i < q; i++) {

        // Starting index
        int l = queries[i][0];

        // Ending index
        int r = queries[i][1];

        // Increment l-th index by 1
        ans[l]++;

        // Decrease r-th index by 1
        ans[r + 1]--;

        // Decrease (r + 1)th index by
        // the length of each query
        res[r + 1] -= (r - l + 1);
    }

    // Find the prefix sum of ans[]
    for (int i = 1; i <= N; i++)
        ans[i] += ans[i - 1];

    // Find the final array
    for (int i = 1; i <= N; i++)
        res[i] += res[i - 1] + ans[i];

    // Printing the modified array
    for (int i = 1; i <= N; i++) {
        cout << res[i] << " ";
    }
    cout << "\n";
}

// Driver Code
int main()
{
    int N = 7;
    vector<vector<int> > queries
        = { { 1, 7 }, { 3, 6 }, { 4, 5 } };

    updateQuery(queries, N);

    return 0;
}
```

**Output:** 

```
1 2 4 7 10 10 7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)