# 将矩阵中所有路径从左上方到右下方转换为回文路径的最小步骤

> 原文:[https://www . geesforgeks . org/矩阵中所有路径从左上方到右下方转换为回文路径的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-convert-all-paths-in-matrix-from-top-left-to-bottom-right-as-palindromic-paths/)

给定一个有 N 行 M 列的矩阵 **mat[][]** 。任务是找到矩阵中所需的最小变化数，使得从左上角到右下角的每条路径都是回文路径。在路径中，从一个单元格到另一个单元格只允许向右和向下移动。
**例:**

> **输入:** mat[][] = {{1，2}，{3，1}}
> **输出:** 0
> **解释:**
> 矩阵中从左上角到右下角的每一条路径都是回文。
> 路径= > {1，2，1}、{1，3，1}
> **输入:** mat[][] = {{1，2}、{3，5}}
> **输出:** 1
> **解释:**
> 每条路径回文只需要一次修改。
> 即=>mat[1][1]= 1
> path =>{1，2，1}，{ 1，3，1}

**简单方法:**

问题中的关键观察是，与前端或后端距离相同的元素是相等的。因此，在距离(0，0)和(N-1，M-1)相等的距离处找到所有元素，然后在最小数量的变化中使它们都相等。维护一个计数变量以获取更改的总数。以下是该方法的示例:

*   从左上角到右下角的可能距离是 0 到 N+M–2。
*   保持[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)一个在左上角，即距离为 0，另一个在 N+M–2。
*   迭代矩阵，对于所有距离，在当前距离保持矩阵元素的[散列图](https://www.geeksforgeeks.org/hashing-data-structure/)。
*   用所需的最小更改数更新矩阵元素。
*   最后，将左距离增加 1，右距离减少 1。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of changes required
// such that every path from top left
// to the bottom right
// are palindromic paths

#include <bits/stdc++.h>
using namespace std;
#define M 3
#define N 3

// Function to find the minimum number
// of the changes required for the
// every path to be palindromic
int minchanges(int mat[N][M])
{
    // count variable for
    // maintaining total changes.
    int count = 0;

    // left and right variables for
    // keeping distance values
    // from cell(0, 0) and
    // (N-1, M-1) respectively.
    int left = 0, right = N + M - 2;

    while (left < right) {

        unordered_map<int, int> mp;
        int totalsize = 0;

        // Iterating over the matrix
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (i + j == left) {
                    mp[mat[i][j]]++;
                    totalsize++;
                }
                else if (i + j == right) {
                    mp[mat[i][j]]++;
                    totalsize++;
                }
            }
        }

        // Finding minimum number
        // of changes required.
        unordered_map<int, int>::iterator itr = mp.begin();
        int changes = 0;
        for (; itr != mp.end(); itr++)
            changes = max(changes, itr->second);

        // Minimum no. of changes will
        // be the the minimum no.
        // of different values and
        // we will assume to
        // make them equals to value
        // with maximum frequency element
        count += totalsize - changes;

        // Moving ahead with
        // greater distance
        left++;
        right--;
    }
    return count;
}

// Drive Code
int main()
{
    int mat[][M]
        = { { 1, 4, 1 }, { 2, 5, 3 }, { 1, 3, 1 } };

    // Function Call
    cout << minchanges(mat);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of changes required
// such that every path from top left
// to the bottom right are palindromic
// paths
import java.io.*;
import java.util.*;

class GFG {

    static final int M = 3;
    static final int N = 3;

    // Function to find the minimum number
    // of the changes required for the
    // every path to be palindromic
    static int minchanges(int[][] mat)
    {

        // count variable for
        // maintaining total changes.
        int count = 0;

        // left and right variables for
        // keeping distance values
        // from cell(0, 0) and
        // (N-1, M-1) respectively.
        int left = 0, right = N + M - 2;

        while (left < right) {
            Map<Integer, Integer> mp = new HashMap<>();

            int totalsize = 0;

            // Iterating over the matrix
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < M; j++) {
                    if (i + j == left) {
                        mp.put(mat[i][j],
                               mp.getOrDefault(mat[i][j], 0)
                                   + 1);
                        totalsize++;
                    }
                    else if (i + j == right) {
                        mp.put(mat[i][j],
                               mp.getOrDefault(mat[i][j], 0)
                                   + 1);
                        totalsize++;
                    }
                }
            }

            // Finding minimum number
            // of changes required.
            int changes = 0;
            for (Map.Entry<Integer, Integer> itr :
                 mp.entrySet())
                changes = Math.max(changes, itr.getValue());

            // Minimum no. of changes will
            // be the the minimum no.
            // of different values and
            // we will assume to
            // make them equals to value
            // with maximum frequency element
            count += totalsize - changes;

            // Moving ahead with
            // greater distance
            left++;
            right--;
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int mat[][]
            = { { 1, 4, 1 }, { 2, 5, 3 }, { 1, 3, 1 } };

        // Function Call
        System.out.println(minchanges(mat));
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of changes required
# such that every path from top left
# to the bottom right
# are palindromic paths
M = 3
N = 3

# Function to find the minimum number
# of the changes required for the
# every path to be palindromic

def minchanges(mat):

    # count variable for
    # maintaining total changes.
    count = 0

    # left and right variables for
    # keeping distance values
    # from cell(0, 0) and
    # (N-1, M-1) respectively.
    left = 0
    right = N + M - 2

    while (left < right):
        mp = {}
        totalsize = 0

        # Iterating over the matrix
        for i in range(N):
            for j in range(M):
                if (i + j == left):
                    mp[mat[i][j]] =
                    mp.get(mat[i][j], 0) + 1
                    totalsize += 1
                elif (i + j == right):
                    mp[mat[i][j]] =
                    mp.get(mat[i][j], 0) + 1
                    totalsize += 1

        # Finding minimum number
        # of changes required.
        changes = 0
        for itr in mp:
            changes = max(changes, mp[itr])

        # Minimum no. of changes will
        # be the the minimum no.
        # of different values and
        # we will assume to
        # make them equals to value
        # with maximum frequency element
        count += totalsize - changes

        # Moving ahead with
        # greater distance
        left += 1
        right -= 1
    return count

# Driver Code
if __name__ == '__main__':
    mat = [[1, 4, 1],
           [2, 5, 3],
           [1, 3, 1]]

    # Function Call
    print(minchanges(mat))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# implementation to find the
// minimum number of changes required
// such that every path from top left
// to the bottom right are palindromic
// paths
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {

    static int M = 3;
    static int N = 3;

    // Function to find the minimum number
    // of the changes required for the
    // every path to be palindromic
    static int minchanges(int[, ] mat)
    {

        // count variable for
        // maintaining total changes.
        int count = 0;

        // left and right variables for
        // keeping distance values
        // from cell(0, 0) and
        // (N-1, M-1) respectively.
        int left = 0, right = N + M - 2;

        while (left < right) {
            Dictionary<int, int> mp
                = new Dictionary<int, int>();
            int totalsize = 0;

            // Iterating over the matrix
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < M; j++) {
                    if (i + j == left) {
                        if (mp.ContainsKey(mat[i, j])) {
                            mp[mat[i, j]]++;
                        }
                        else {
                            mp[mat[i, j]] = 1;
                        }
                        totalsize++;
                    }
                    else if (i + j == right) {
                        if (mp.ContainsKey(mat[i, j])) {
                            mp[mat[i, j]]++;
                        }
                        else {
                            mp[mat[i, j]] = 1;
                        }
                        totalsize++;
                    }
                }
            }

            // Finding minimum number
            // of changes required.
            int changes = 0;
            foreach(KeyValuePair<int, int> itr in mp)
            {
                changes = Math.Max(changes, itr.Value);
            }

            // Minimum no. of changes will
            // be the the minimum no.
            // of different values and
            // we will assume to
            // make them equals to value
            // with maximum frequency element
            count += totalsize - changes;

            // Moving ahead with
            // greater distance
            left++;
            right--;
        }
        return count;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[, ] mat
            = { { 1, 4, 1 }, { 2, 5, 3 }, { 1, 3, 1 } };

        // Function Call
        Console.Write(minchanges(mat));
    }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum number of changes required
// such that every path from top left
// to the bottom right
// are palindromic paths
var M = 3
var N = 3;

// Function to find the minimum number
// of the changes required for the
// every path to be palindromic
function minchanges(mat)
{
    // count variable for
    // maintaining total changes.
    var count = 0;

    // left and right variables for
    // keeping distance values
    // from cell(0, 0) and
    // (N-1, M-1) respectively.
    var left = 0, right = N + M - 2;

    while (left < right) {

        var mp = new Map();
        var totalsize = 0;

        // Iterating over the matrix
        for (var i = 0; i < N; i++) {
            for (var j = 0; j < M; j++) {
                if (i + j == left || i + j == right) {
                    if(mp.has(mat[i][j]))
                        mp.set(mat[i][j], mp.get(mat[i][j])+1)
                    else
                        mp.set(mat[i][j], 1)
                    totalsize++;
                }
            }
        }

        var changes = 0;
        // Finding minimum number
        // of changes required.
        mp.forEach((value, key) => {
            changes = Math.max(changes, value);
        });

        // Minimum no. of changes will
        // be the the minimum no.
        // of different values and
        // we will assume to
        // make them equals to value
        // with maximum frequency element
        count += totalsize - changes;

        // Moving ahead with
        // greater distance
        left++;
        right--;
    }
    return count;
}

// Drive Code
var mat
    = [ [ 1, 4, 1 ], [ 2, 5, 3 ], [ 1, 3, 1 ] ];
// Function Call
document.write( minchanges(mat));

// This code is contributed by importantly.
</script>
```

**Output:** 

```
2
```

**性能分析:**

*   **时间复杂度:** O(N <sup>3</sup> )
*   **辅助空间:** O(N)

**有效方法:**

算法:

*   我们将使用一个 hashmap 来计算每个元素的频率，这些元素从顶部到底部的距离是相同的。
*   我们将使用一个 2D 地图，其中的关键将是索引，值将是另一个地图，将计数频率
*   计数频率后，我们将迭代 l=0 到 r=m+n-1，而 l
*   我们将用频率最大的元素替换(sum-f)元素，并存储结果+=(sum-f)
*   打印结果

下面是上述方法的实现:

## C++

```
// C++ Program to count minimum change
// required to convert all the paths
// pallindromic from top left to
// right bottom cell.
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of the changes required for the
// every path to be palindromic
int minchanges(vector<vector<int> >& a)
{
    int res = 0; // use to store final result

    // Row and column
    int N = a.size(), M = a[0].size();

    // mp_key -> (i+j) , mp_value -> nw_map
    // nw_map_key -> elements_of_matrix
    // nw_map_value -> frequency of elements

    // 2-D map
    map<int, map<int, int> > mp;

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            // calculating position
            int ind = i + j;

            // increase the frequency of a[i][j]
            // at position ind
            mp[ind][a[i][j]]++;
        }
    }

    // Define left and right limit
    int r = M + N - 2, l = 0;
    while (l < r) {

        // s-> count total number of elements
        // at index l and r
        // mx-> store maximum frequency of any element
        int s = 0, mx = 0;

        // store all elements frequency at index l
        for (auto x : mp[r]) {
            mp[l][x.first] += x.second;
        }

        // Count total elements and mx->max_frequency
        for (auto x : mp[l]) {
            s += x.second;
            mx = max(x.second, mx);
        }

        // We will replace (s-mx) elements with
        // the element whose frequency is mx
        res += (s - mx);
        l++;
        r--;
    }

    // return res
    return res;
}

// Driver Code
int main()
{
    // Function Call
    vector<vector<int> > mat
        = { { 1, 4, 1 }, { 2, 5, 3 }, { 1, 3, 1 } };
    cout << "Total number of changes requires "
         << minchanges(mat) << "\n";

    // Function Call
    vector<vector<int> > mat1
        = { { 1, 4 }, { 2, 5 }, { 1, 3 }, { 2, 5 } };
    cout << "Total number of changes requires "
         << minchanges(mat1) << "\n";

    return 0;
}

// This code is contributed by ajaykr00kj
```

**Output**

```
Total number of changes requires 2
Total number of changes requires 3
```

***时间复杂度:** O(m*n)*

***空间复杂度:** O(m*n)*