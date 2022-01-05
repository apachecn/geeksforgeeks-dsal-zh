# 最大的行和列排序子矩阵

> 原文:[https://www . geeksforgeeks . org/最大行和列排序子矩阵/](https://www.geeksforgeeks.org/largest-row-wise-and-column-wise-sorted-sub-matrix/)

给定一个 **N * M** 矩阵**mat【】【】**，任务是找到面积最大的矩形子矩阵，使得子矩阵的每一列和每一行严格递增。

**示例:**

> **输入:** mat[][] =
> {{1，2，3}，
> {4，5，6}，
> {1，2，3}}
> **输出:** 6
> 最大的子矩阵将是{{1，2，3}，{4，5，6}}。
> 该子矩阵的元素个数= 6。
> 
> **输入:** mat[][] =
> {{1，2，3}，
> {4，5，3}，
> {1，2，3}}
> **输出:** 4
> 最大的子矩阵将是
> {{1，2}，{4，5}}

**方法:**解决这个问题的方法有很多，从 O(N <sup>3</sup> * M <sup>3</sup> )到 O(N * M)不等。在本文中，将讨论一种使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)的时间复杂度为 0(N * M)的方法。
在进一步进行之前，建议先解决[这个。](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)问题。

让我们试着广泛地理解这种方法，然后讨论算法。对于矩阵的每一列，尝试找到最大的按行和按列排序的子矩阵，其左边缘位于该列。为了执行相同的操作，创建一个矩阵 **pre[][]** ，其中 **pre[i][j]** 将存储从数组 **arr[i]** 的索引 **j** 开始的最长递增子数组的长度。
现在使用这个矩阵，对于每一列 **j** ，找到最长的行方向和列方向排序数组的长度。要处理一列，需要数组中所有递增的子段 **pre[][j]** 。使用[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)技术也可以找到相同的结果。在这些子段中的每一个中，只需在直方图下找到最大的区域，将逐行增加的子段视为条形。

*   为每一行“I”创建一个前缀和数组，它存储在该行的每一列“j”处结束的最大递增子数组的长度。
*   一旦我们有了这个数组，对于每个列“j”。
    *   初始化“I”等于 0。
    *   当“I”小于“N”时，在“I”上运行循环
        *   初始化“k”等于 i+1。
        *   当 k 小于 N 且 arr[k][j]大于 arr[k-1][j]时，增加 k
        *   将子阵列 pre[i][j]上的直方图问题应用于 pre[k-1][j]，以找到其下的最大区域。让我们称这个值为“V”。将最终答案更新为 ans = max(ans，val)。
        *   更新“I”等于 k-1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// area under a histogram
int histo(vector<int> q)
{

    // Stack
    stack<int> q1;

    // Length of the vector
    int n = q.size();

    // Function to store the next smaller
    // and previous smaller index
    int pre_smaller[q.size()];
    int next_smaller[q.size()];

    // Finding the next smaller
    for (int i = 0; i < n; i++)
        pre_smaller[i] = -1, next_smaller[i] = n;
    for (int i = 0; i < n; i++) {
        while (q1.size() and q[q1.top()] > q[i]) {
            next_smaller[q1.top()] = i;
            q1.pop();
        }
        q1.push(i);
    }

    // Finding the previous smaller element
    while (q1.size())
        q1.pop();
    for (int i = n - 1; i >= 0; i--) {
        while (q1.size() and q[q1.top()] > q[i]) {
            pre_smaller[q1.top()] = i;
            q1.pop();
        }
        q1.push(i);
    }

    // To store the final answer
    int ans = 0;

    // Finding the final answer
    for (int i = 0; i < n; i++)
        ans = max(ans, (next_smaller[i]
                        - pre_smaller[i] - 1)
                           * q[i]);

    // Returning the final answer
    return ans;
}

// Function to return the largest area
// for the required submatrix
int findLargest(vector<vector<int> > arr)
{
    // n and m store the number of
    // rows and columns respectively
    int n = arr.size();
    int m = arr[0].size();

    // To store the prefix_sum
    int pre[n][m];

    // To store the final answer
    int ans = 0;

    // Loop to create the prefix-sum
    // using two pointers
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {
            if (j == 0) {
                pre[i][j] = 1;
                continue;
            }
            if (arr[i][j] > arr[i][j - 1])
                pre[i][j] = pre[i][j - 1] + 1;
            else
                pre[i][j] = 1;
        }

    // For each column run the loop
    for (int j = 0; j < m; j++) {

        // Find the largest row-wise sorted arrays
        for (int i = 0; i < n; i++) {
            int k = i + 1;
            vector<int> q;
            q.push_back(pre[i][j]);
            while (k < n and arr[k] > arr[k - 1])
                q.push_back(pre[k][j]), k++;

            // Applying the largest area
            // under the histogram
            ans = max(ans, histo(q));
            i = k - 1;
        }
    }

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    vector<vector<int> > arr = { { 1, 2, 3 },
                                 { 4, 5, 6 },
                                 { 1, 2, 3 } };

    cout << findLargest(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to return the largest
  // area under a histogram
  static int histo(ArrayList<Integer> q)
  {

    // Stack
    Stack<Integer> q1 = new Stack<Integer>();

    // Length of the vector
    int n = q.size();

    // Function to store the next smaller
    // and previous smaller index
    int[] pre_smaller = new int[q.size()];
    int[] next_smaller = new int[q.size()];

    // Finding the next smaller
    for (int i = 0; i < n; i++)
    {
      pre_smaller[i] = -1;
      next_smaller[i] = n;
    }
    for (int i = 0; i < n; i++)
    {
      while (q1.size() > 0 && q.get(q1.peek()) > q.get(i))
      {
        next_smaller[q1.peek()] = i;
        q1.pop();
      }
      q1.push(i);
    }

    // Finding the previous smaller element
    while (q1.size() > 0)
    {
      q1.pop();
    }
    for (int i = n - 1; i >= 0; i--)
    {
      while (q1.size() > 0 && q.get(q1.peek()) > q.get(i))
      {
        pre_smaller[q1.peek()] = i;
        q1.pop();
      }
      q1.push(i);
    }

    // To store the final answer
    int ans = 0;

    // Finding the final answer
    for (int i = 0; i < n; i++)
    {
      ans = Math.max(ans, (next_smaller[i] -
                           pre_smaller[i] - 1) *
                     q.get(i));

    }

    // Returning the final answer
    return ans;
  }

  // Function to return the largest area
  // for the required submatrix
  static int findLargest(ArrayList<ArrayList<Integer>> arr)
  {

    // n and m store the number of
    // rows and columns respectively
    int n = arr.size();
    int m = arr.get(0).size();

    // To store the prefix_sum
    int[][] pre=new int[n][m];

    // To store the final answer
    int ans = 0;

    // Loop to create the prefix-sum
    // using two pointers
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < m; j++)
      {
        if (j == 0)
        {
          pre[i][j] = 1;
          continue;
        }
        if(arr.get(i).get(j) > arr.get(i).get(j - 1))
        {
          pre[i][j] = pre[i][j - 1] + 1;
        }
        else
        {
          pre[i][j] = 1;
        }
      }
    }

    // For each column run the loop
    for (int j = 0; j < m; j++)
    {

      // Find the largest row-wise sorted arrays
      for (int i = 0; i < n; i++)
      {
        int k = i + 1;
        ArrayList<Integer> q = new ArrayList<Integer>();
        q.add(pre[i][j]);
        while (k < n && arr.get(k).get(0) > arr.get(k - 1).get(0))
        {
          q.add(pre[k][j]);
          k++;
        }

        // Applying the largest area
        // under the histogram
        ans = Math.max(ans, histo(q));
        i = k - 1;
      }
    }

    // Return the final answer
    return ans;
  }

  // Driver code
  public static void main (String[] args)
  {
    ArrayList<ArrayList<Integer>> arr = new ArrayList<ArrayList<Integer>>();
    arr.add(new ArrayList<Integer>(Arrays.asList(1, 2, 3 )));
    arr.add(new ArrayList<Integer>(Arrays.asList(4, 5, 6 )));
    arr.add(new ArrayList<Integer>(Arrays.asList(1, 2, 3 )));
    System.out.println(findLargest(arr));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Pythono3 implementation of the approach

# Function to return the largest
# area under a histogram
def histo(q):

    # Stack
    q1 = []

    # Length of the vector
    n = len(q)

    # Function to store the next smaller
    # and previous smaller index
    pre_smaller = [0 for i in range(len(q))]
    next_smaller = [0 for i in range(len(q))]

    # Finding the next smaller
    for i in range(n):
        pre_smaller[i] = -1
        next_smaller[i] = n
    for i in range(n):
        while (len(q1) > 0 and q[q1[-1]] > q[i]):
            next_smaller[q1[-1]] = i
            del q1[-1]
        q1.append(i)

    # Finding the previous smaller element
    while (len(q1) > 0):
        del q1[-1]

    for i in range(n - 1, -1, -1):
        while (len(q1) > 0 and q[q1[-1]] > q[i]):
            pre_smaller[q1[-1]] = i
            del q1[-1]

        q1.append(i)

    # To store the final answer
    ans = 0

    # Finding the final answer
    for i in range(n):
        ans = max(ans, (next_smaller[i]- pre_smaller[i] - 1)* q[i])

    # Returning the final answer
    return ans

# Function to return the largest area
# for the required submatrix
def findLargest(arr):

    # n and m store the number of
    # rows and columns respectively
    n = len(arr)
    m = len(arr[0])

    # To store the prefix_sum
    pre = [[0 for i in range(m)] for i in range(n)]

    # To store the final answer
    ans = 0

    # Loop to create the prefix-sum
    # using two pointers
    for i in range(n):
        for j in range(m):
            if (j == 0):
                pre[i][j] = 1
                continue

            if (arr[i][j] > arr[i][j - 1]):
                pre[i][j] = pre[i][j - 1] + 1
            else:
                pre[i][j] = 1

    # For each column run the loop
    for j in range(m):

        # Find the largest row-wise sorted arrays
        for i in range(n):
            k = i + 1
            q = []
            q.append(pre[i][j])
            while (k < n and arr[k] > arr[k - 1]):
                q.append(pre[k][j])
                k += 1

            # Applying the largest area
            # under the histogram
            ans = max(ans, histo(q))
            i = k - 1

    # Return the final answer
    return ans

# Driver code

arr = [ [ 1, 2, 3 ],
    [ 4, 5, 6 ],
    [ 1, 2, 3 ] ]

print(findLargest(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the largest
// area under a histogram
static int histo(List<int> q)
{

    // Stack
    Stack<int> q1 = new Stack<int>();

    // Length of the vector
    int n = q.Count;

    // Function to store the next smaller
    // and previous smaller index
    int[] pre_smaller = new int[q.Count];
    int[] next_smaller = new int[q.Count];

    // Finding the next smaller
    for(int i = 0; i < n; i++)
    {
        pre_smaller[i] = -1;
        next_smaller[i] = n;
    }
    for(int i = 0; i < n; i++)
    {
        while (q1.Count > 0 && q[q1.Peek()] > q[i])
        {
            next_smaller[q1.Peek()] = i;
            q1.Pop();
        }
        q1.Push(i);
    }

    // Finding the previous smaller element
    while (q1.Count > 0)
    {
        q1.Pop();
    }

    for(int i = n - 1; i >= 0; i--)
    {
        while (q1.Count > 0 && q[q1.Peek()] > q[i])
        {
            pre_smaller[q1.Peek()] = i;
            q1.Pop();
        }
        q1.Push(i);
    }

    // To store the final answer
    int ans = 0;

    // Finding the final answer
    for(int i = 0; i < n; i++)
    {
        ans = Math.Max(ans, (next_smaller[i] -
                              pre_smaller[i] - 1) * q[i]);
    }

    // Returning the
    // final answer
    return ans;
}

// Function to return the largest area
// for the required submatrix
static int findLargest(List<List<int>> arr)
{

    // n and m store the number of
    // rows and columns respectively
    int n = arr.Count;
    int m = arr[0].Count;

    // To store the prefix_sum
    int[,] pre = new int[n, m];

    // To store the final answer
    int ans = 0;

    // Loop to create the prefix-sum
    // using two pointers
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            if (j == 0)
            {
                pre[i, j] = 1;
                continue;
            }

            if (arr[i][j] > arr[i][j - 1])
            {
                pre[i, j] = pre[i,j - 1] + 1;
            }
            else
            {
                pre[i, j] = 1;
            }
        }
    }

    // For each column run the loop
    for(int j = 0; j < m; j++)
    {

        // Find the largest row-wise sorted arrays
        for(int i = 0; i < n; i++)
        {
            int k = i + 1;
            List<int> q = new List<int>();
            q.Add(pre[i, j]);

            while(k < n && arr[k][0] > arr[k - 1][0])
            {
                q.Add(pre[k, j]);
                k++;
            }

            // Applying the largest area
            // under the histogram
            ans = Math.Max(ans, histo(q));
            i = k - 1;
        }
    }

    // Return the final answer
    return ans;
}

// Driver code
static public void Main()
{
    List<List<int>> arr = new List<List<int>>();
    arr.Add(new List<int>(){1, 2, 3});
    arr.Add(new List<int>(){4, 5, 6 });
    arr.Add(new List<int>(){1, 2, 3});

    Console.WriteLine(findLargest(arr));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the largest
  // area under a histogram
function histo(q)
{
    // Stack
    let q1 = [];

    // Length of the vector
    let n = q.length;

    // Function to store the next smaller
    // and previous smaller index
    let pre_smaller = new Array(q.length);
    let next_smaller = new Array(q.length);

    // Finding the next smaller
    for (let i = 0; i < n; i++)
    {
      pre_smaller[i] = -1;
      next_smaller[i] = n;
    }
    for (let i = 0; i < n; i++)
    {
      while (q1.length > 0 && q[q1[q1.length-1]] > q[i])
      {
        next_smaller[q1[q1.length-1]] = i;
        q1.pop();
      }
      q1.push(i);
    }

    // Finding the previous smaller element
    while (q1.length > 0)
    {
      q1.pop();
    }
    for (let i = n - 1; i >= 0; i--)
    {
      while (q1.length > 0 && q[q1[q1.length-1]] > q[i])
      {
        pre_smaller[q1[q1.length-1]] = i;
        q1.pop();
      }
      q1.push(i);
    }

    // To store the final answer
    let ans = 0;

    // Finding the final answer
    for (let i = 0; i < n; i++)
    {
      ans = Math.max(ans, (next_smaller[i] -
                           pre_smaller[i] - 1) *
                     q[i]);

    }

    // Returning the final answer
    return ans;
}

// Function to return the largest area
  // for the required submatrix
function findLargest(arr)
{
    // n and m store the number of
    // rows and columns respectively
    let n = arr.length;
       let m = arr[0].length;

    // To store the prefix_sum
    let pre=new Array(n);
    for(let i=0;i<n;i++)
    {
        pre[i]=new Array(m);
        for(let j=0;j<m;j++)
        {
            pre[i][j]=0;
        }
    }

    // To store the final answer
    let ans = 0;

    // Loop to create the prefix-sum
    // using two pointers
    for (let i = 0; i < n; i++)
    {
      for (let j = 0; j < m; j++)
      {
        if (j == 0)
        {
          pre[i][j] = 1;
          continue;
        }
        if(arr[i][j] > arr[i][j - 1])
        {
          pre[i][j] = pre[i][j - 1] + 1;
        }
        else
        {
          pre[i][j] = 1;
        }
      }
    }

    // For each column run the loop
    for (let j = 0; j < m; j++)
    {

      // Find the largest row-wise sorted arrays
      for (let i = 0; i < n; i++)
      {
        let k = i + 1;
        let q = [];
        q.push(pre[i][j]);
        while (k < n && arr[k][0] > arr[k - 1][0])
        {
          q.push(pre[k][j]);
          k++;
        }

        // Applying the largest area
        // under the histogram
        ans = Math.max(ans, histo(q));
        i = k - 1;
      }
    }

    // Return the final answer
    return ans;
}

 // Driver code
let arr=[[1, 2, 3],[4, 5, 6 ],[1, 2, 3]];
document.write(findLargest(arr));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
6
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间 : O(N <sup>2</sup> )。