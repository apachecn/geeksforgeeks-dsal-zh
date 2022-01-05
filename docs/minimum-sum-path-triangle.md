# 三角形中的最小和路径

> 原文:[https://www.geeksforgeeks.org/minimum-sum-path-triangle/](https://www.geeksforgeeks.org/minimum-sum-path-triangle/)

给定一个三角形的数字结构，求从上到下的最小路径和。每一步你可以移动到下一行的相邻数字。

**示例:**

```
Input : 
   2
  3 7
 8 5 6
6 1 9 3
Output : 11
Explanation : 2 + 3 + 5 + 1 = 11

Input :
   3
  6 4
 5 2 7
9 1 8 6
Output : 10
Explanation : 3 + 4 + 2 + 1 = 10
```

**天真方法:**通过遍历每一条可能的路径来经历天真方法。但是，这是昂贵的。因此，在这里使用动态编程来降低时间复杂度。
有两种方法可以解决这个问题:

1.记忆–从顶部节点开始，递归遍历每个节点，直到计算出该节点的路径和。然后将结果存储在数组中。但这将占用 O(N^2)空间来维护阵列。

2.自下而上–从最下面一行的节点开始；这些节点的最小路径总和是节点本身的值。然后，第 k 行的第 I 个节点处的最小路径和将是其两个子节点的路径和+该节点的值的最小值，即:

```
memo[k][i] = min( memo[k+1][i], memo[k+1][i+1]) + A[k][i];
```

或者
简单地将 memo 设置为 1D 数组，并更新它
这也将节省空间:

对于行 k:

```
memo[i] = min( memo[i], memo[i+1]) + A[k][i];
```

下面是上述动态编程方法的实现:

## C++

```
// C++ program for Dynamic
// Programming implementation of
// Min Sum Path in a Triangle
#include <bits/stdc++.h>
using namespace std;

// Util function to find minimum sum for a path
int minSumPath(vector<vector<int> >& A)
{
    // For storing the result in a 1-D array,
    // and simultaneously updating the result.
    int memo[A.size()];
    int n = A.size() - 1;

    // For the bottom row
    for (int i = 0; i < A[n].size(); i++)
        memo[i] = A[n][i];   

    // Calculation of the remaining rows,
    // in bottom up manner.
    for (int i = A.size() - 2; i >= 0; i--)
        for (int j = 0; j < A[i].size(); j++)
            memo[j] = A[i][j] + min(memo[j],
                                    memo[j + 1]);

    // return the top element
    return memo[0];
}

/* Driver program to test above functions */
int main()
{
    vector<vector<int> > A{ { 2 },
                            { 3, 9 },
                            { 1, 6, 7 } };
    cout << minSumPath(A);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Dynamic
// Programming implementation of
// Min Sum Path in a Triangle
import java.io.*;
import java.util.*;

class GFG
{
    static int A[][] = {{2},
                        {3, 9},
                        {1, 6, 7}};

    // Util function to find
    // minimum sum for a path
    static int minSumPath()
    {
        // For storing the result
        // in a 1-D array, and
        // simultaneously updating
        // the result.
        int []memo = new int[A.length];
        int n = A.length - 1;

        // For the bottom row
        for (int i = 0;
                 i < A[n].length; i++)
            memo[i] = A[n][i];

        // Calculation of the
        // remaining rows, in
        // bottom up manner.
        for (int i = A.length - 2;
                 i >= 0; i--)
            for (int j = 0;
                     j < A[i].length; j++)
                memo[j] = A[i][j] +
                          (int)Math.min(memo[j],
                                   memo[j + 1]);

        // return the
        // top element
        return memo[0];
    }

    // Driver Code
    public static void main(String args[])
    {
        System.out.print(minSumPath());
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program for Dynamic
# Programming implementation of
# Min Sum Path in a Triangle

# Util function to find
# minimum sum for a path
def minSumPath(A):

    # For storing the result in
    # a 1-D array, and simultaneously
    # updating the result.
    memo = [None] * len(A)
    n = len(A) - 1

    # For the bottom row
    for i in range(len(A[n])):
        memo[i] = A[n][i]

    # Calculation of the
    # remaining rows,
    # in bottom up manner.
    for i in range(len(A) - 2, -1,-1):
        for j in range( len(A[i])):
            memo[j] = A[i][j] + min(memo[j],
                                    memo[j + 1]);

    # return the top element
    return memo[0]

# Driver Code
A = [[ 2 ],
    [3, 9 ],
    [1, 6, 7 ]]
print(minSumPath(A))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program for Dynamic
// Programming implementation of
// Min Sum Path in a Triangle
using System;
using System.Collections.Generic;
using System.Linq;

class GFG {

    // Util function to find
    // minimum sum for a path
    static int minSumPath(ref List<List<int>> A)
    {

        // For storing the result in a 1-D array,
        // and simultaneously updating the result.
        int []memo = new int[A.Count];
        int n = A.Count - 1;

        // For the bottom row
        for (int i = 0; i < A[n].Count; i++)
            memo[i] = A[n][i];

        // Calculation of the remaining rows,
        // in bottom up manner.
        for (int i = A.Count - 2; i >= 0; i--)
            for (int j = 0; j < A[i + 1].Count - 1; j++)
                memo[j] = A[i][j] +
                          (int)Math.Min(memo[j],
                                   memo[j + 1]);

        // return the top element
        return memo[0];
    }

    // Driver Code
    public static void Main()
    {
        List<List<int>> A = new List<List<int>>();
        A.Add(new List<int> {2});
        A.Add(new List<int> {3, 9});
        A.Add(new List<int> {1, 6, 7});
        Console.WriteLine(minSumPath(ref A));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Dynamic
// Programming implementation of
// Min Sum Path in a Triangle

// Util function to find
// minimum sum for a path
function minSumPath(&$A)
{
    // For storing the result
    // in a 1-D array, and
    // simultaneously updating
    // the result.
    $memo = array();
    for ($i = 0; $i < count($A); $i++)
        $memo[$i] = 0;

    $n = count($A) - 1;

    // For the bottom row
    for ($i = 0;
         $i < count($A[$n]); $i++)
        $memo[$i] = $A[$n][$i];

    // Calculation of
    // the remaining rows,
    // in bottom up manner.
    for ($i = count($A) - 2; $i >= 0; $i--)
        for ($j = 0;
             $j < count($A[$i + 1]) - 1; $j++)
            $memo[$j] = $A[$i][$j] +
                        min($memo[$j],
                        $memo[$j + 1]);

    // return the
    // top element
    return $memo[0];
}

// Driver Code
$A = array(array(2),
           array(3, 9),
           array(1, 6, 7));
echo (minSumPath($A));

// This code is contributed
// by Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program for Dynamic
// Programming implementation of
// Min Sum Path in a Triangle
let A = [[2], [3, 9], [1, 6, 7]];

// Util function to find
// minimum sum for a path
function minSumPath()
{

    // For storing the result
    // in a 1-D array, and
    // simultaneously updating
    // the result.
    let memo = [];
    let n = A.length - 1;

    // For the bottom row
    for(let i = 0; i < A[n].length; i++)
        memo[i] = A[n][i];

    // Calculation of the
    // remaining rows, in
    // bottom up manner.
    for(let i = A.length - 2; i >= 0; i--)
        for(let j = 0;
                j < A[i].length; j++)
            memo[j] = A[i][j] +
                      Math.min(memo[j],
                               memo[j + 1]);

    // Return the
    // top element
    return memo[0];
}

// Driver code
document.write(minSumPath());

// This code is contributed by splevel62

</script>
```

**Output:** 

```
6
```