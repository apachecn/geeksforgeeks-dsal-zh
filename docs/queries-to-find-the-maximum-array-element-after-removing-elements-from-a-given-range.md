# 从给定范围内移除元素后查询最大数组元素

> 原文:[https://www . geesforgeks . org/query-to-find-最大数组-从给定范围中移除元素后的元素/](https://www.geeksforgeeks.org/queries-to-find-the-maximum-array-element-after-removing-elements-from-a-given-range/)

给定一个由形式为 **{L，R}** 的查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个数组 **Q[][]** ，每个查询的任务是在从索引范围**【L，R】**中移除数组元素后[找到最大数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。如果从给定范围的索引中删除元素后数组变为空，则打印 **0** 。

**示例:**

> **输入:** arr[] = {5，6，8，10，15}，Q = {{0，1}，{0，2}，{1，4}}
> **输出:**
> 15
> 15
> 5
> **解释:**
> 对于第一个查询{0 1}:移除范围[0，1]中的数组元素，数组修改为{8，10，15}。因此，最大元素是 15。
> 对于第二个查询{0，2}:移除范围[0，2]中的数组元素，数组修改为{10，15}。因此，最大元素是 15。
> 对于第三个查询{1 4}:移除范围[1，4]中的数组元素，数组修改为{5}。因此，最大元素是 5。
> 
> **输入:** arr[] = {8，12，14，10，13}，Q = {{0，3}，{0，4}，{4，4}}
> **输出:**
> 13
> -1
> 14

**天真法:**最简单的方法是[遍历数组，在每个查询中移除给定范围内的数组元素后，找到最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*

**高效方式:**优化上述方式，思路是使用两个辅助数组:一个存储前缀最大值(范围**【0，I】**中的最大元素)，另一个存储后缀最大值(范围**【I，N–1】**中的最大元素)。那么对于每个查询**【L，R】**，答案将是**prefixMax【L–1】**和**sufixmax【R+1】**的最大值。按照以下步骤解决问题:

*   初始化两个辅助数组: **prefixMax** 和**大小为 **N + 1** 的后缀 Max** ，并将**prefixMax【0】**初始化为**arr【0】**，将**后缀 max【N–1】**初始化为**arr【N–1】**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**，并将 **prefixMax[i]** 设置为**prefixMax[I–1]**和 **arr[i]** 的[最大值。](https://www.geeksforgeeks.org/stdmax-in-cpp/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N–2，0】**，并将**后缀 Max[i]** 设置为**后缀 Max[i + 1]** 和 **arr[i]** 的最大值[。](https://www.geeksforgeeks.org/stdmax-in-cpp/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** ，对于每个查询，检查以下条件:
    *   如果**L = 0****R = N–1**，则打印 **0** 作为结果。
    *   否则，如果 **L = 0** ，则打印**后缀 max【R+1】**作为结果。
    *   否则，如果**R = N–1**，则打印**前缀【L–1】**作为结果。
    *   对于所有其他情况，打印**前缀【L–1】**和**后缀【R+1】**T5 的[最大值。](https://www.geeksforgeeks.org/stdmax-in-cpp/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum element
// after removing elements in range [l, r]
int findMaximum(int arr[], int N, int Q,
                int queries[][2])
{
    // Store prefix maximum element
    int prefix_max[N + 1] = { 0 };

    // Store suffix maximum element
    int suffix_max[N + 1] = { 0 };

    // Prefix max till first index
    // is first index itself
    prefix_max[0] = arr[0];

    // Traverse the array to fill
    // prefix max array
    for (int i = 1; i < N; i++) {

        // Store maximum till index i
        prefix_max[i]
            = max(prefix_max[i - 1],
                  arr[i]);
    }

    // Suffix max till last index
    // is last index itself
    suffix_max[N - 1] = arr[N - 1];

    // Traverse the array to fill
    // suffix max array
    for (int i = N - 2; i >= 0; i--) {

        // Store maximum till index i
        suffix_max[i]
            = max(suffix_max[i + 1],
                  arr[i]);
    }

    // Traverse all queries
    for (int i = 0; i < Q; i++) {

        // Store the starting and the
        // ending index of the query
        int l = queries[i][0];
        int r = queries[i][1];

        // Edge Cases
        if (l == 0 && r == (N - 1))
            cout << "0\n";

        else if (l == 0)
            cout << suffix_max[r + 1]
                 << "\n";

        else if (r == (N - 1))
            cout << prefix_max[l - 1]
                 << "\n";

        // Otherwise
        else
            cout << max(prefix_max[l - 1],
                        suffix_max[r + 1])
                 << "\n";
    }
}

// Driver Code
int main()
{
    int arr[] = { 5, 6, 8, 10, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int queries[][2] = { { 0, 1 }, { 0, 2 }, { 1, 4 } };
    int Q = sizeof(queries) / sizeof(queries[0]);

    findMaximum(arr, N, Q, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the maximum element
// after removing elements in range [l, r]
static void findMaximum(int arr[], int N, int Q,
                int queries[][])
{

    // Store prefix maximum element
    int prefix_max[] = new int[N + 1];

    // Store suffix maximum element
    int suffix_max[] = new int[N + 1];

    // Prefix max till first index
    // is first index itself
    prefix_max[0] = arr[0];

    // Traverse the array to fill
    // prefix max array
    for (int i = 1; i < N; i++) {

        // Store maximum till index i
        prefix_max[i]
            = Math.max(prefix_max[i - 1],
                  arr[i]);
    }

    // Suffix max till last index
    // is last index itself
    suffix_max[N - 1] = arr[N - 1];

    // Traverse the array to fill
    // suffix max array
    for (int i = N - 2; i >= 0; i--) {

        // Store maximum till index i
        suffix_max[i]
            = Math.max(suffix_max[i + 1],
                  arr[i]);
    }

    // Traverse all queries
    for (int i = 0; i < Q; i++) {

        // Store the starting and the
        // ending index of the query
        int l = queries[i][0];
        int r = queries[i][1];

        // Edge Cases
        if (l == 0 && r == (N - 1))
            System.out.print("0\n");
        else if (l == 0)
            System.out.print(suffix_max[r + 1]
                + "\n");
        else if (r == (N - 1))
            System.out.print(prefix_max[l - 1]
                + "\n");

        // Otherwise
        else
            System.out.print(Math.max(prefix_max[l - 1],
                        suffix_max[r + 1])
                + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 8, 10, 15 };
    int N = arr.length;
    int queries[][] = { { 0, 1 }, { 0, 2 }, { 1, 4 } };
    int Q = queries.length;
    findMaximum(arr, N, Q, queries);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum element
# after removing elements in range [l, r]
def findMaximum(arr, N, Q, queries):

    # Store prefix maximum element
    prefix_max = [0]*(N + 1)

    # Store suffix maximum element
    suffix_max = [0]*(N + 1)

    # Prefix max till first index
    # is first index itself
    prefix_max[0] = arr[0]

    # Traverse the array to fill
    # prefix max array
    for i in range(1, N):

        # Store maximum till index i
        prefix_max[i]= max(prefix_max[i - 1], arr[i])

    # Suffix max till last index
    # is last index itself
    suffix_max[N - 1] = arr[N - 1]

    # Traverse the array to fill
    # suffix max array
    for i in range(N - 2, -1, -1):

        # Store maximum till index i
        suffix_max[i] = max(suffix_max[i + 1], arr[i])

    # Traverse all queries
    for i in range(Q):

        # Store the starting and the
        # ending index of the query
        l = queries[i][0]
        r = queries[i][1]

        # Edge Cases
        if (l == 0 and r == (N - 1)):
            print("0")
        elif (l == 0):
            print(suffix_max[r + 1])
        elif (r == (N - 1)):
            print(prefix_max[l - 1])

        # Otherwise
        else:
            print(max(prefix_max[l - 1], suffix_max[r + 1]))

# Driver Code
if __name__ == '__main__':
    arr = [5, 6, 8, 10, 15]
    N = len(arr)
    queries = [ [ 0, 1 ], [ 0, 2 ], [ 1, 4 ] ]
    Q = len(queries)
    findMaximum(arr, N, Q, queries)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to find the maximum element
// after removing elements in range [l, r]
static void findMaximum(int[] arr, int N, int Q,
                int[,] queries)
{

    // Store prefix maximum element
    int[] prefix_max = new int[N + 1];

    // Store suffix maximum element
    int[] suffix_max = new int[N + 1];

    // Prefix max till first index
    // is first index itself
    prefix_max[0] = arr[0];

    // Traverse the array to fill
    // prefix max array
    for (int i = 1; i < N; i++)
    {

        // Store maximum till index i
        prefix_max[i]
            = Math.Max(prefix_max[i - 1],
                  arr[i]);
    }

    // Suffix max till last index
    // is last index itself
    suffix_max[N - 1] = arr[N - 1];

    // Traverse the array to fill
    // suffix max array
    for (int i = N - 2; i >= 0; i--)
    {

        // Store maximum till index i
        suffix_max[i]
            = Math.Max(suffix_max[i + 1],
                  arr[i]);
    }

    // Traverse all queries
    for (int i = 0; i < Q; i++)
    {

        // Store the starting and the
        // ending index of the query
        int l = queries[i, 0];
        int r = queries[i, 1];

        // Edge Cases
        if (l == 0 && r == (N - 1))
            Console.Write("0\n");
        else if (l == 0)
            Console.Write(suffix_max[r + 1]
                + "\n");
        else if (r == (N - 1))
            Console.Write(prefix_max[l - 1]
                + "\n");

        // Otherwise
        else
            Console.Write(Math.Max(prefix_max[l - 1],
                        suffix_max[r + 1])
                + "\n");
    }
}

// Driver Code
static public void Main ()
{
    int[] arr = { 5, 6, 8, 10, 15 };
    int N = arr.Length;
    int[,] queries = { { 0, 1 }, { 0, 2 }, { 1, 4 } };
    int Q = queries.GetLength(0);
    findMaximum(arr, N, Q, queries);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program of the above approach

// Function to find the maximum element
// after removing elements in range [l, r]
function findMaximum(arr, N, Q,
                queries)
{

    // Store prefix maximum element
    let prefix_max = [];

    // Store suffix maximum element
    let suffix_max = [];

    // Prefix max till first index
    // is first index itself
    prefix_max[0] = arr[0];

    // Traverse the array to fill
    // prefix max array
    for (let i = 1; i < N; i++) {

        // Store maximum till index i
        prefix_max[i]
            = Math.max(prefix_max[i - 1],
                  arr[i]);
    }

    // Suffix max till last index
    // is last index itself
    suffix_max[N - 1] = arr[N - 1];

    // Traverse the array to fill
    // suffix max array
    for (let i = N - 2; i >= 0; i--) {

        // Store maximum till index i
        suffix_max[i]
            = Math.max(suffix_max[i + 1],
                  arr[i]);
    }

    // Traverse all queries
    for (let i = 0; i < Q; i++)
    {

        // Store the starting and the
        // ending index of the query
        let l = queries[i][0];
        let r = queries[i][1];

        // Edge Cases
        if (l == 0 && r == (N - 1))
            document.write("0");
        else if (l == 0)
            document.write(suffix_max[r + 1]
                + "<br/>");
        else if (r == (N - 1))
            document.write(prefix_max[l - 1]
                + "<br/>");

        // Otherwise
        else
            document.write(Math.max(prefix_max[l - 1],
                        suffix_max[r + 1])
                + "<br/>");
    }
}

    // Driver Code   
    let arr = [ 5, 6, 8, 10, 15 ];
    let N = arr.length;
    let queries = [[ 0, 1 ], [ 0, 2 ], [ 1, 4 ]];
    let Q = queries.length;
    findMaximum(arr, N, Q, queries);

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
15
15
5
```

***时间复杂度:** O(N + Q)*
***辅助空间:** O(N)*