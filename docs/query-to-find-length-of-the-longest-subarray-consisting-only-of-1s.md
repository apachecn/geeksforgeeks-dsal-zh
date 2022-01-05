# 查询查找仅由 1s 组成的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/query-to-find-最长子阵列长度-仅由-1s 组成/](https://www.geeksforgeeks.org/query-to-find-length-of-the-longest-subarray-consisting-only-of-1s/)

给定大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和包含以下两种类型的 **K** 查询的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **Q[][]** :

*   **1 :** 只打印由 **1** s 组成的最长子阵列的长度。
*   **2 X :** 在**X**T4 索引处翻转元素(*基于 1 的索引*)，即如果当前元素为**“0”**，则将元素更改为**“1”**，反之亦然。

**示例:**

> **输入:** N = 10，arr[] = {1，1，0，1，1，1，0，0，1，1}，K=3，Q[][] = {{1}，{2，3}，{ 1 }
> T3】输出:3 6
> T6】解释:
> **查询 1:**1s 最长子阵长度只有 3。
> **查询 2:** 将索引 **2** 处的字符**“0”**翻转为**“1”**。因此，arr[]修改为{1，1，1，1，1，1，0，0，1，1}。
> **查询 3:**1s 的最长子阵长度只有 6。
> 
> **输入:** N = 7，arr[] = {1，1，1，1，1，0}，K=3，Q[][]={{1}，{2，7}，{1}}
> **输出:** 6 7
> **解释:**
> **查询 1:**1s 最长子阵长度仅为 6。
> **查询 2:** 翻转位置 7 的字符**‘0’**。因此，数组 arr[]修改为{1，1，1，1，1，1，1}。
> **查询 3:**1**s 最长子阵的**长度仅为 7。

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**进行每个查询并执行给定的操作。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the longest subarray
// consisting of 1s only
int longestsubarray(int a[], int N)
{
    // Stores the maximum length of
    // subarray containing 1s only
    int maxlength = 0, sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current element is '1'
        if (a[i] == 1) {

            // Increment length
            sum++;
        }

        // Otherwise
        else {

            // Reset length
            sum = 0;
        }

        // Update maximum subarray length
        maxlength = max(maxlength, sum);
    }
    return maxlength;
}

// Function to perform given queries
void solveQueries(int arr[], int n,
                  vector<vector<int> > Q, int k)
{

    // Stores count of queries
    int cntQuery = Q.size();

    // Traverse each query
    for (int i = 0; i < cntQuery; i++) {

        if (Q[i][0] == 1) {
            cout << longestsubarray(arr, n) << " ";
        }
        else {
            // Flip the character
            arr[Q[i][1] - 1] ^= 1;
        }
    }
}

// Driver Code
int main()
{
    // Size of array
    int N = 10;

    // Given array
    int arr[] = { 1, 1, 0, 1, 1,
                  1, 0, 0, 1, 1 };

    // Given queries
    vector<vector<int> > Q = { { 1 }, { 2, 3 }, { 1 } };

    // Number of queries
    int K = 3;

    solveQueries(arr, N, Q, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;
public class Main
{
  // Function to calculate the longest subarray
  // consisting of 1s only
  static int longestsubarray(int a[], int N)
  {

    // Stores the maximum length of
    // subarray containing 1s only
    int maxlength = 0, sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If current element is '1'
      if (a[i] == 1)
      {

        // Increment length
        sum++;
      }

      // Otherwise
      else
      {

        // Reset length
        sum = 0;
      }

      // Update maximum subarray length
      maxlength = Math.max(maxlength, sum);
    }
    return maxlength;
  }

  // Function to perform given queries
  static void solveQueries(int arr[], int n,
                           Vector<Vector<Integer>> Q, int k)
  {

    // Stores count of queries
    int cntQuery = Q.size();

    // Traverse each query
    for (int i = 0; i < cntQuery; i++)
    {

      if (Q.get(i).get(0) == 1)
      {
        System.out.print(longestsubarray(arr, n) + " ");
      }
      else
      {

        // Flip the character
        arr[Q.get(i).get(1) - 1] ^= 1;
      }
    }
  }

  public static void main(String[] args) {
    // Size of array
    int N = 10;

    // Given array
    int arr[] = { 1, 1, 0, 1, 1,
                 1, 0, 0, 1, 1 };

    // Given queries
    Vector<Vector<Integer>> Q = new Vector<Vector<Integer>>();
    Vector<Integer> v1 = new Vector<Integer>();
    Vector<Integer> v2 = new Vector<Integer>();
    Vector<Integer> v3 = new Vector<Integer>();
    v1.add(1);
    v2.add(2);
    v2.add(3);
    v3.add(1);
    Q.add(v1);
    Q.add(v2);
    Q.add(v3);

    // Number of queries
    int K = 3;

    solveQueries(arr, N, Q, K);
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to calculate the longest subarray
# consisting of 1s only
def longestsubarray(a, N) :

    # Stores the maximum length of
    # subarray containing 1s only
    maxlength = 0
    sum = 0

    # Traverse the array
    for i in range(N):

        # If current element is '1'
        if (a[i] == 1) :

            # Increment length
            sum += 1

        # Otherwise
        else :

            # Reset length
            sum = 0

        # Update maximum subarray length
        maxlength = max(maxlength, sum)   
    return maxlength

# Function to perform given queries
def solveQueries(arr, n, Q, k) :

    # Stores count of queries
    cntQuery = len(Q)

    # Traverse each query
    for i in range(cntQuery):

        if (Q[i][0] == 1) :
            print(longestsubarray(arr, n), end = " ")

        else :
            # Flip the character
            arr[Q[i][1] - 1] ^= 1

# Driver Code

# Size of array
N = 10

# Given array
arr = [ 1, 1, 0, 1, 1,
        1, 0, 0, 1, 1]

# Given queries
Q = [[1], [ 2, 3 ], [1]] 

# Number of queries
K = 3
solveQueries(arr, N, Q, K)

# This code is contributed by sanjoy_62
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to calculate the longest subarray
    // consisting of 1s only
    static int longestsubarray(int[] a, int N)
    {

        // Stores the maximum length of
        // subarray containing 1s only
        int maxlength = 0, sum = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // If current element is '1'
            if (a[i] == 1)
            {

                // Increment length
                sum++;
            }

            // Otherwise
            else
            {

                // Reset length
                sum = 0;
            }

            // Update maximum subarray length
            maxlength = Math.Max(maxlength, sum);
        }
        return maxlength;
    }

    // Function to perform given queries
    static void solveQueries(int[] arr, int n,
                      List<List<int>> Q, int k)
    {

        // Stores count of queries
        int cntQuery = Q.Count;

        // Traverse each query
        for (int i = 0; i < cntQuery; i++)
        {

            if (Q[i][0] == 1)
            {
                Console.Write(longestsubarray(arr, n) + " ");
            }
            else
            {

                // Flip the character
                arr[Q[i][1] - 1] ^= 1;
            }
        }
    }

  // Driver code
  static void Main()
  {

    // Size of array
    int N = 10;

    // Given array
    int[] arr = { 1, 1, 0, 1, 1,
                  1, 0, 0, 1, 1 };

    // Given queries
    List<List<int>> Q = new List<List<int>>();
    Q.Add(new List<int> { 1 });
    Q.Add(new List<int> { 2, 3 });
    Q.Add(new List<int> { 1 });

    // Number of queries
    int K = 3;

    solveQueries(arr, N, Q, K);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

// Function to calculate the longest subarray
// consisting of 1s only
function longestsubarray(a, N)
{
    // Stores the maximum length of
    // subarray containing 1s only
    var maxlength = 0, sum = 0;

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // If current element is '1'
        if (a[i] == 1) {

            // Increment length
            sum++;
        }

        // Otherwise
        else {

            // Reset length
            sum = 0;
        }

        // Update maximum subarray length
        maxlength = Math.max(maxlength, sum);
    }
    return maxlength;
}

// Function to perform given queries
function solveQueries(arr, n, Q, k)
{

    // Stores count of queries
    var cntQuery = Q.length;

    // Traverse each query
    for (var i = 0; i < cntQuery; i++) {

        if (Q[i][0] == 1) {
            document.write( longestsubarray(arr, n) + " ");
        }
        else {
            // Flip the character
            arr[Q[i][1] - 1] ^= 1;
        }
    }
}

// Driver Code
// Size of array
var N = 10;
// Given array
var arr = [1, 1, 0, 1, 1,
              1, 0, 0, 1, 1 ];
// Given queries
var Q = [ [ 1 ], [ 2, 3 ], [ 1 ] ];
// Number of queries
var K = 3;
solveQueries(arr, N, Q, K);

</script>
```

**Output:** 

```
3 6
```

***时间复杂度:** (N * K)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)数据结构进行优化。给定的问题可以基于以下观察来解决:

> *   It is easy to observe that at least three things are needed to merge the two nodes of segment tree . Therefore, three segments of trees are needed, such as **max [], pref[],** and **suf []** . **Max []:** Storing the length of the longest sub-array consisting of **1** s, **Pre []** and **SUF []** will store the longest lengths of prefixes and suffixes respectively.
> *   The merging of two nodes can be done in the following ways:
>     *   **MAX[I]= MAX(MAX[2 * I])、max(MAX[2*i + 1]、suf[2 * v+ 1]+pref[2 * I])**
>     *   **前缀[v]=最大值(pref[v * 2]【pref[2 * v]= TM-TL+1)*前缀[v * 2+1])suf[2 * v+1]+suf[v * 2]*(suf[2 * v+1]= = tr-TM)]**
>     *   Here **I, 2*i and 2 * I+1** are the current node, the left child node and the right child node respectively, **TL and TR** are the current range.

按照以下步骤解决问题:

*   对于类型 1 的查询，打印段树的根节点**MAX【1】**，该段树包含仅在范围**【1，N】**中由 1 组成的子阵列的最长长度
*   对于类型 2 的查询，翻转给定位置[更新线段树。](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define INF 1000000

// Arrays to store prefix sums, suffix
// and MAX's node respectively
int pref[500005];
int suf[500005];
int MAX[500005];

// Function to construct Segment Tree
void build(int a[], int tl, int tr, int v)
{
    if (tl == tr) {

        // MAX array for node MAX
        MAX[v] = a[tl];

        // Array for prefix sum node
        pref[v] = a[tl];
        // Array for suffix sum node
        suf[v] = a[tl];
    }
    else {
        int tm = (tl + tr) / 2;
        build(a, tl, tm, v * 2);
        build(a, tm + 1, tr, v * 2 + 1);

        // Calculate MAX node
        MAX[v] = max(MAX[v * 2],
                     max(MAX[v * 2 + 1],
                         suf[v * 2] + pref[v * 2 + 1]));

        pref[v] = max(pref[v * 2],
                      pref[2 * v]
                          + (pref[2 * v] == tm - tl + 1)
                                * pref[v * 2 + 1]);

        suf[v] = max(
            suf[v * 2 + 1],
            suf[2 * v + 1]
                + suf[v * 2] * (suf[2 * v + 1] == tr - tm));
    }
}

// Function to update Segment Tree
void update(int a[], int pos, int tl,
            int tr, int v)
{
    if (tl > pos || tr < pos) {
        return;
    }

    // Update at position
    if (tl == tr && tl == pos) {

        MAX[v] = a[pos];
        pref[v] = a[pos];
        suf[v] = a[pos];
    }
    else {

        // Update sums from bottom to the
        // top of Segment Tree
        int tm = (tl + tr) / 2;
        update(a, pos, tl, tm, v * 2);
        update(a, pos, tm + 1, tr, v * 2 + 1);

        // Update MAX tree
        MAX[v] = max(MAX[v * 2],
                     max(MAX[v * 2 + 1],
                         suf[v * 2] + pref[v * 2 + 1]));
        // Update pref tree
        pref[v] = max(pref[v * 2],
                      pref[2 * v]
                          + (pref[2 * v] == tm - tl + 1)
                                * pref[v * 2 + 1]);
        // Update suf tree
        suf[v] = max(suf[v * 2 + 1],
                     suf[2 * v + 1]
                         + (suf[2 * v + 1] == tr - tm)
                               * suf[v * 2]);
    }
}

// Function to perform given queries
void solveQueries(int arr[], int n,
                  vector<vector<int> > Q, int k)
{
    // Stores count of queries
    int cntQuery = Q.size();

    build(arr, 0, n - 1, 1);

    // Traverse each query
    for (int i = 0; i < cntQuery; i++) {
        if (Q[i][0] == 1) {

            // Print longest length of subarray in [1, N]
            cout << MAX[1] << " ";
        }

        else {

            // Flip the character
            arr[Q[i][1] - 1] ^= 1;
            update(arr, Q[i][1] - 1, 0, n - 1, 1);
        }
    }
}

// Driver Code
int main()
{
    // Size of array
    int N = 10;

    // Given array
    int arr[] = { 1, 1, 0, 1, 1,
                  1, 0, 0, 1, 1 };

    // Given queries
    vector<vector<int> > Q = { { 1 }, { 2, 3 }, { 1 } };

    // Number of queries
    int K = 3;

    solveQueries(arr, N, Q, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;
class GFG
{
static final int INF = 1000000;

// Arrays to store prefix sums, suffix
// and MAX's node respectively
static int []pref = new int[500005];
static int []suf = new int[500005];
static int []MAX = new int[500005];

// Function to conSegment Tree
static void build(int a[], int tl, int tr, int v)
{
    if (tl == tr) {

        // MAX array for node MAX
        MAX[v] = a[tl];

        // Array for prefix sum node
        pref[v] = a[tl];
        // Array for suffix sum node
        suf[v] = a[tl];
    }
    else {
        int tm = (tl + tr) / 2;
        build(a, tl, tm, v * 2);
        build(a, tm + 1, tr, v * 2 + 1);

        // Calculate MAX node
        MAX[v] = Math.max(MAX[v * 2],
                     Math.max(MAX[v * 2 + 1],
                         suf[v * 2] + pref[v * 2 + 1]));

        pref[v] = Math.max(pref[v * 2],
                      pref[2 * v]
                          + (pref[2 * v] == (tm - tl + 1)?1:0)
                                * pref[v * 2 + 1]);
        suf[v] = Math.max(
            suf[v * 2 + 1],
            suf[2 * v + 1]
                + suf[v * 2] * (suf[2 * v + 1] == (tr - tm)?1:0));
    }
}

// Function to update Segment Tree
static void update(int a[], int pos, int tl,
            int tr, int v)
{
    if (tl > pos || tr < pos) {
        return;
    }

    // Update at position
    if (tl == tr && tl == pos)
    {
        MAX[v] = a[pos];
        pref[v] = a[pos];
        suf[v] = a[pos];
    }
    else {

        // Update sums from bottom to the
        // top of Segment Tree
        int tm = (tl + tr) / 2;
        update(a, pos, tl, tm, v * 2);
        update(a, pos, tm + 1, tr, v * 2 + 1);

        // Update MAX tree
        MAX[v] = Math.max(MAX[v * 2],
                     Math.max(MAX[v * 2 + 1],
                         suf[v * 2] + pref[v * 2 + 1]));
        // Update pref tree
        pref[v] = Math.max(pref[v * 2],
                      pref[2 * v]
                          + (pref[2 * v] == (tm - tl + 1)?1:0)
                                * pref[v * 2 + 1]);
        // Update suf tree
        suf[v] = Math.max(suf[v * 2 + 1],
                     suf[2 * v + 1]
                         + (suf[2 * v + 1] == (tr - tm)?1:0)
                               * suf[v * 2]);
    }
}

// Function to perform given queries
static void solveQueries(int arr[], int n,
                  int[][] Q, int k)
{
    // Stores count of queries
    int cntQuery = Q.length;
    build(arr, 0, n - 1, 1);

    // Traverse each query
    for (int i = 0; i < cntQuery; i++)
    {
        if (Q[i][0] == 1)
        {

            // Print longest length of subarray in [1, N]
            System.out.print(MAX[1]+ " ");
        }

        else
        {

            // Flip the character
            arr[Q[i][1] - 1] ^= 1;
            update(arr, Q[i][1] - 1, 0, n - 1, 1);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    // Size of array
    int N = 10;

    // Given array
    int arr[] = { 1, 1, 0, 1, 1,
                  1, 0, 0, 1, 1 };

    // Given queries
    int [][]Q = { { 1 }, { 2, 3 }, { 1 } };

    // Number of queries
    int K = 3;

    solveQueries(arr, N, Q, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 Program for the above approach
INF = 1000000

# Arrays to store prefix sums, suffix
# and MAX's node respectively
pref = [0 for i in range(500005)]
suf = [0 for i in range(500005)]
MAX = [0 for i in range(500005)]

# Function to construct Segment Tree
def build(a, tl,tr,v):
    global MAX
    global pref
    global suf
    if (tl == tr):

        # MAX array for node MAX
        MAX[v] = a[tl]

        # Array for prefix sum node
        pref[v] = a[tl]

        # Array for suffix sum node
        suf[v] = a[tl]
    else:
        tm = (tl + tr) // 2
        build(a, tl, tm, v * 2)
        build(a, tm + 1, tr, v * 2 + 1)

        # Calculate MAX node
        MAX[v] = max(MAX[v * 2], max(MAX[v * 2 + 1], suf[v * 2] + pref[v * 2 + 1]))

        pref[v] = max(pref[v * 2], pref[2 * v] + (pref[2 * v] == tm - tl + 1)* pref[v * 2 + 1])

        suf[v] = max(suf[v * 2 + 1],suf[2 * v + 1]+suf[v * 2] * (suf[2 * v + 1] == tr - tm))

# Function to update Segment Tree
def update(a,pos,tl,tr,v):
    global pref
    global suf
    global MAX
    if (tl > pos or tr < pos):
        return

    # Update at position
    if (tl == tr and tl == pos):
        MAX[v] = a[pos]
        pref[v] = a[pos]
        suf[v] = a[pos]
    else:
        # Update sums from bottom to the
        # top of Segment Tree
        tm = (tl + tr) // 2
        update(a, pos, tl, tm, v * 2)
        update(a, pos, tm + 1, tr, v * 2 + 1)

        # Update MAX tree
        MAX[v] = max(MAX[v * 2], max(MAX[v * 2 + 1], suf[v * 2] + pref[v * 2 + 1]))

        # Update pref tree
        pref[v] = max(pref[v * 2], pref[2 * v] + (pref[2 * v] == tm - tl + 1) * pref[v * 2 + 1])

        # Update suf tree
        suf[v] = max(suf[v * 2 + 1], suf[2 * v + 1] + (suf[2 * v + 1] == tr - tm) * suf[v * 2])

# Function to perform given queries
def solveQueries(arr, n, Q, k):
    global MAX

    # Stores count of queries
    cntQuery = len(Q)
    build(arr, 0, n - 1, 1)

    # Traverse each query
    for i in range(cntQuery):
        if (Q[i][0] == 1):

            # Print longest length of subarray in [1, N]
            print(MAX[1],end = " ")

        else:
            # Flip the character
            arr[Q[i][1] - 1] ^= 1
            update(arr, Q[i][1] - 1, 0, n - 1, 1)

# Driver Code
if __name__ == '__main__':

    # Size of array
    N = 10

    # Given array
    arr =  [1, 1, 0, 1, 1, 1, 0, 0, 1, 1]

    # Given queries
    Q =  [[1], [2, 3], [1]]

    # Number of queries
    K = 3
    solveQueries(arr, N, Q, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# Program for the above approach
using System;
class GFG
{

static readonly int INF = 1000000;

// Arrays to store prefix sums, suffix
// and MAX's node respectively
static int []pref = new int[500005];
static int []suf = new int[500005];
static int []MAX = new int[500005];

// Function to conSegment Tree
static void build(int []a, int tl, int tr, int v)
{
    if (tl == tr)
    {

        // MAX array for node MAX
        MAX[v] = a[tl];

        // Array for prefix sum node
        pref[v] = a[tl];

        // Array for suffix sum node
        suf[v] = a[tl];
    }
    else
    {
        int tm = (tl + tr) / 2;
        build(a, tl, tm, v * 2);
        build(a, tm + 1, tr, v * 2 + 1);

        // Calculate MAX node
        MAX[v] = Math.Max(MAX[v * 2],
                     Math.Max(MAX[v * 2 + 1],
                         suf[v * 2] + pref[v * 2 + 1]));
        pref[v] = Math.Max(pref[v * 2],
                      pref[2 * v]
                          + (pref[2 * v] == (tm - tl + 1)?1:0)
                                * pref[v * 2 + 1]);
        suf[v] = Math.Max(
            suf[v * 2 + 1],
            suf[2 * v + 1]
                + suf[v * 2] * (suf[2 * v + 1] == (tr - tm)?1:0));
    }
}

// Function to update Segment Tree
static void update(int []a, int pos, int tl,
            int tr, int v)
{
    if (tl > pos || tr < pos)
    {
        return;
    }

    // Update at position
    if (tl == tr && tl == pos)
    {
        MAX[v] = a[pos];
        pref[v] = a[pos];
        suf[v] = a[pos];
    }
    else
    {

        // Update sums from bottom to the
        // top of Segment Tree
        int tm = (tl + tr) / 2;
        update(a, pos, tl, tm, v * 2);
        update(a, pos, tm + 1, tr, v * 2 + 1);

        // Update MAX tree
        MAX[v] = Math.Max(MAX[v * 2],
                     Math.Max(MAX[v * 2 + 1],
                         suf[v * 2] + pref[v * 2 + 1]));

      // Update pref tree
        pref[v] = Math.Max(pref[v * 2],
                      pref[2 * v]
                          + (pref[2 * v] == (tm - tl + 1)?1:0)
                                * pref[v * 2 + 1]);

      // Update suf tree
        suf[v] = Math.Max(suf[v * 2 + 1],
                     suf[2 * v + 1]
                         + (suf[2 * v + 1] == (tr - tm)?1:0)
                               * suf[v * 2]);
    }
}

// Function to perform given queries
static void solveQueries(int []arr, int n,
                  int[,] Q, int k)
{

    // Stores count of queries
    int cntQuery = Q.GetLength(0);
    build(arr, 0, n - 1, 1);

    // Traverse each query
    for (int i = 0; i < cntQuery; i++)
    {
        if (Q[i, 0] == 1)
        {

            // Print longest length of subarray in [1, N]
            Console.Write(MAX[1] + " ");
        }

        else
        {

            // Flip the character
            arr[Q[i, 1] - 1] ^= 1;
            update(arr, Q[i, 1] - 1, 0, n - 1, 1);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Size of array
    int N = 10;

    // Given array
    int []arr = { 1, 1, 0, 1, 1,
                  1, 0, 0, 1, 1 };

    // Given queries
    int [,]Q = { { 1,0 }, { 2, 3 }, { 1,0 } };

    // Number of queries
    int K = 3;
    solveQueries(arr, N, Q, K);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
3 6
```

***时间复杂度:** O(max(K*log(N)，N * log(N))*
***辅助空间:** O(4*N)*