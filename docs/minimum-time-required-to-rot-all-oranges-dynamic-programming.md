# 腐烂所有橙子所需的最短时间|动态编程

> 原文:[https://www . geesforgeks . org/最短时间-需要腐烂-所有橙子-动态编程/](https://www.geeksforgeeks.org/minimum-time-required-to-rot-all-oranges-dynamic-programming/)

给定维度为 **m * n** 的矩阵，其中矩阵中的每个单元格可以具有值 **0** 、 **1** 或 **2** ，其含义如下:

```
0: Empty cell

1: Cells have fresh oranges

2: Cells have rotten oranges
```

因此，任务是确定使所有橙子腐烂所需的最短时间。一个指数为**【I，j】**的烂橙，可以指数为**【I–1，j】****【I+1，j】****【I，j–1】****【I，j+1】**(上，下，左，右)腐烂其他鲜橙。如果不可能腐烂每个橙子，那么只需返回 **-1** 。
**示例:**

> **输入:** arr[][] = {
> {2，1，0，2，1}，
> {1，0，1，2，1}，
> {1，0，0，2，1 } }；
> **输出:** 2
> 在第一个单位时间内，除了最后一排
> 的第一个橘子会在第二个单位时间内腐烂外，所有的橘子都会腐烂
> 。
> 
> **输入:** arr[][] =
> {{2，1，0，2，1}，
> {0，0，1，2，1}，
> {1，0，0，2，1 } }；
> **输出:** -1

**方法:**基于 BFS 的方法已经讨论过了[这里](https://www.geeksforgeeks.org/minimum-time-required-so-that-all-oranges-become-rotten/)。

在这篇文章中，我们使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。

每个橘子都需要腐烂。任何橘子都可以被它最近的烂橘子腐烂。所以，对于每一个还没有腐烂的橘子，我们找到它离腐烂的橘子的最小距离，然后我们取最大值，代表腐烂所有橘子所需的最短时间。

设 dp(i，j) =该橙子与任何腐烂橙子的最小距离，因此，dp 状态为:

> dp(i，j)= 0 if arr[I][j]= = 2
> DP(I，j) = INT_MAX if arr[i][j] == 0
> 
> 如果 dp(i，j) >0 和 dp(i，j) <int_max>则 dp(i，j) = min(dp(i，j)，1 + min(dp(i + 1，j)，
> dp(i–1，j)，dp(i，j + 1)，DP(I，j–1))</int_max>
> 
> else dp(i，j) = 1 + min(dp(i + 1，j)、dp(i–1，j)、dp(i，j + 1)、DP(I，j–1))

对于所有 I，j，我们的答案将是 max(dp(i，j))，其中 arr[i][j] == 1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <iostream>
using namespace std;
#define C 5
#define R 3
#define INT_MAX 10000000

// DP table to memoize the values
int table[R][C] = { 0 };

// Visited array to keep
// track of visited nodes
// in order to avoid infinite loops
int visited[R][C] = { 0 };

// Function to return the
// minimum of four numbers
int min(int p, int q, int r, int s)
{
    int temp1 = p < q ? p : q;
    int temp2 = r < s ? r : s;

    if (temp1 < temp2)
        return temp1;
    return temp2;
}

// Function to return the minimum distance
// to any rotten orange from [i, j]
int Distance(int arr[R][C], int i, int j)
{
    // If i, j  lie outside the array
    if (i >= R || j >= C || i < 0 || j < 0)
        return INT_MAX;

    // If 0 then it can't lead to
    // any path so return INT_MAX
    else if (arr[i][j] == 0) {
        table[i][j] = INT_MAX;
        return INT_MAX;
    }

    // If 2 then we have reached
    // our rotten oranges
    // so return from here
    else if (arr[i][j] == 2) {
        table[i][j] = 0;
        return 0;
    }

    // If this node is already visited
    // then return to avoid infinite loops
    else if (visited[i][j]) {
        return INT_MAX;
    }
    else {

        // Mark the current node as visited
        visited[i][j] = 1;

        // Check in all four possible directions
        int temp1 = Distance(arr, i + 1, j);
        int temp2 = Distance(arr, i - 1, j);
        int temp3 = Distance(arr, i, j + 1);
        int temp4 = Distance(arr, i, j - 1);

        // Take the minimum of all
        int min_value = 1 + min(temp1,
                    temp2, temp3, temp4);

        // If result already exists in the table
        // check if min_value is less
        // than existing value
        if (table[i][j] > 0 &&
            table[i][j] < INT_MAX) {
            if (min_value < table[i][j])
                table[i][j] = min_value;
        }
        else
            table[i][j] = min_value;
        visited[i][j] = 0;
        return table[i][j];
    }
}

// Function to return the minimum time
// required to rot all the oranges
int minTime(int arr[][C])
{
    int max = 0;

    // Calculate the minimum
    // distances to any rotten
    // orange from all the fresh oranges
    for (int i = 0; i < R; i++) {
        for (int j = 0; j < C; j++) {
            if (arr[i][j] == 1)
                Distance(arr, i, j);
        }
    }

    // Pick the maximum distance of fresh orange
    // to some rotten orange
    for (int i = 0; i < R; i++) {
        for (int j = 0; j < C; j++) {
            if (arr[i][j] == 1 &&
                table[i][j] > max)
                max = table[i][j];
        }
    }

    // If all oranges can be rotten
    if (max < INT_MAX)
        return max;

    return -1;
}

// Driver Code
int main()
{

    int arr[R][C] = { { 2, 1, 0, 2, 1 },
                      { 0, 0, 1, 2, 1 },
                      { 1, 0, 0, 2, 1 } };

    cout << minTime(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {
    static int C = 5;
    static int R = 3;
    static int INT_MAX = 10000000;

    // DP table to memoize the values
    static int[][] table = new int[R][C];

    // Visited array to keep
    // track of visited nodes
    // in order to avoid infinite loops
    static int[][] visited = new int[R][C];

    // Function to return the
    // minimum of four numbers
    static int min(int p, int q, int r, int s)
    {
        int temp1 = p < q ? p : q;
        int temp2 = r < s ? r : s;

        if (temp1 < temp2)
            return temp1;
        return temp2;
    }

    // Function to return the
    // minimum distance
    // to any rotten orange from [i, j]
    static int Distance(int arr[][], int i, int j)
    {
        // If i, j lie outside the array
        if (i >= R || j >= C || i < 0 || j < 0)
            return INT_MAX;

        // If 0 then it can't lead to
        // any path so return INT_MAX
        else if (arr[i][j] == 0) {
            table[i][j] = INT_MAX;
            return INT_MAX;
        }

        // If 2 then we have reached
        // our rotten oranges
        // so return from here
        else if (arr[i][j] == 2) {
            table[i][j] = 0;
            return 0;
        }

        // If this node is already visited
        // then return to avoid
        // infinite loops
        else if (visited[i][j] == 1) {
            return INT_MAX;
        }
        else {

            // Mark the current node
            // as visited
            visited[i][j] = 1;

            // Check in all four
            // possible directions
            int temp1 = Distance(arr, i + 1, j);
            int temp2 = Distance(arr, i - 1, j);
            int temp3 = Distance(arr, i, j + 1);
            int temp4 = Distance(arr, i, j - 1);

            // Take the minimum of all
            int min_value
                = 1 + min(temp1, temp2, temp3, temp4);
            // If result already exists in
            // the table check if min_value
            // is less than existing value
            if (table[i][j] > 0 &&
                table[i][j] < INT_MAX) {
                if (min_value < table[i][j])
                    table[i][j] = min_value;
            }
            else
                table[i][j] = min_value;

            visited[i][j] = 0;
        }
        return table[i][j];
    }

    // Function to return the minimum time
    // required to rot all the oranges
    static int minTime(int arr[][])
    {
        int max = 0;

        // Calculate the minimum
        // distances to any rotten
        // orange from all the fresh oranges
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (arr[i][j] == 1)
                    Distance(arr, i, j);
            }
        }

        // Pick the maximum distance
        // of fresh orange
        // to some rotten orange
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (arr[i][j] == 1 &&
                    table[i][j] > max)
                    max = table[i][j];
            }
        }

        // If all oranges can be rotten
        if (max < INT_MAX)
            return max;

        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[][] = { { 2, 1, 0, 2, 1 },
                        { 0, 0, 1, 2, 1 },
                        { 1, 0, 0, 2, 1 } };

        System.out.println(minTime(arr));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

C = 5
R = 3
INT_MAX = 10000000

# DP table to memoize the values
table = [[0 for i in range(C)]
         for j in range(R)]

# Visited array to keep track
# of visited nodes
# in order to avoid infinite loops
visited = [[0 for i in range(C)]
           for j in range(R)]

# Function to return the
# minimum of four numbers

def min(p, q, r, s):
    if(p < q):
        temp1 = p
    else:
        temp1 = q
    if(r < s):
        temp2 = r
    else:
        temp2 = s

    if (temp1 < temp2):
        return temp1
    return temp2

# Function to return the
# minimum distance
# to any rotten orange from [i, j]

def Distance(arr, i, j):

    # If i, j lie outside the array
    if (i >= R or j >= C or
            i < 0 or j < 0):
        return INT_MAX

    # If 0 then it can't lead to
    # any path so return INT_MAX
    elif (arr[i][j] == 0):
        table[i][j] = INT_MAX
        return INT_MAX

    # If 2 then we have reached
    # our rotten oranges
    # so return from here
    elif (arr[i][j] == 2):
        table[i][j] = 0
        return 0

    # If this node is already visited
    # then return to avoid infinite loops
    elif (visited[i][j]):
        return INT_MAX
    else:
        # Mark the current node as visited
        visited[i][j] = 1

        # Check in all four
        # possible directions
        temp1 = Distance(arr, i + 1, j)
        temp2 = Distance(arr, i - 1, j)
        temp3 = Distance(arr, i, j + 1)
        temp4 = Distance(arr, i, j - 1)

        # Take the minimum of all
        min_value = 1 + min(temp1, temp2,
                            temp3, temp4)

        if table[i][j] > 0 and \
                table[i][j] < INT_MAX:
            if min_value < table[i][j]:
                table[i][j] = min_value
        else:
            table[i][j] = min_value

        visited[i][j] = 0
    return table[i][j]

# Function to return the minimum time
# required to rot all the oranges

def minTime(arr):
    max = 0

    # Calculate the minimum distances
    # to any rotten
    # orange from all the fresh oranges
    for i in range(R):
        for j in range(C):
            if (arr[i][j] == 1):
                Distance(arr, i, j)

    # Pick the maximum distance
    # of fresh orange
    # to some rotten orange
    for i in range(R):
        for j in range(C):
            if (arr[i][j] == 1 and
                    table[i][j] > max):
                max = table[i][j]

    # If all oranges can be rotten
    if (max < INT_MAX):
        return max
    return -1

# Driver Code
if __name__ == '__main__':
    arr = [[2, 1, 0, 2, 1],
           [0, 0, 1, 2, 1],
           [1, 0, 0, 2, 1]]

    print(minTime(arr))
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

static int C = 5;
static int R = 3;
static int INT_MAX =
           10000000;

// DP table to memoize
// the values
static int[,] table =
       new int[R, C];

// Visited array to keep
// track of visited nodes
// in order to avoid infinite
// loops
static int[,] visited =
       new int[R, C];

// Function to return the
// minimum of four numbers
static int min(int p, int q,
               int r, int s)
{
  int temp1 = p < q ? p : q;
  int temp2 = r < s ? r : s;

  if (temp1 < temp2)
    return temp1;
  return temp2;
}

// Function to return the
// minimum distance
// to any rotten orange
// from [i, j]
static int Distance(int [,]arr,
                    int i, int j)
{
  // If i, j lie outside
  // the array
  if (i >= R || j >= C ||
      i < 0 || j < 0)
    return INT_MAX;

  // If 0 then it can't lead
  // to any path so return
  // INT_MAX
  else if (arr[i, j] == 0)
  {
    table[i, j] = INT_MAX;
    return INT_MAX;
  }

  // If 2 then we have reached
  // our rotten oranges
  // so return from here
  else if (arr[i, j] == 2)
  {
    table[i, j] = 0;
    return 0;
  }

  // If this node is already
  // visited then return to
  // avoid infinite loops
  else if (visited[i, j] == 1)
  {
    return INT_MAX;
  }
  else
  {
    // Mark the current node
    // as visited
    visited[i, j] = 1;

    // Check in all four
    // possible directions
    int temp1 = Distance(arr,
                         i + 1, j);
    int temp2 = Distance(arr,
                         i - 1, j);
    int temp3 = Distance(arr,
                         i, j + 1);
    int temp4 = Distance(arr,
                         i, j - 1);

    // Take the minimum of all
    int min_value = 1 + min(temp1, temp2,
                            temp3, temp4);
    // If result already exists in
    // the table check if min_value
    // is less than existing value
    if (table[i, j] > 0 &&
        table[i, j] < INT_MAX)
    {
      if (min_value < table[i, j])
        table[i, j] = min_value;
    }
    else
      table[i, j] = min_value;

    visited[i, j] = 0;
  }
  return table[i, j];
}

// Function to return the minimum
// time required to rot all the
// oranges
static int minTime(int [,]arr)
{
  int max = 0;

  // Calculate the minimum
  // distances to any rotten
  // orange from all the fresh
  // oranges
  for (int i = 0; i < R; i++)
  {
    for (int j = 0; j < C; j++)
    {
      if (arr[i, j] == 1)
        Distance(arr, i, j);
    }
  }

  // Pick the maximum distance
  // of fresh orange
  // to some rotten orange
  for (int i = 0; i < R; i++)
  {
    for (int j = 0; j < C; j++)
    {
      if (arr[i, j] == 1 &&
          table[i, j] > max)
        max = table[i, j];
    }
  }

  // If all oranges can be
  // rotten
  if (max < INT_MAX)
    return max;

  return -1;
}

// Driver Code
public static void Main(string[] args)
{
  int [,]arr = {{2, 1, 0, 2, 1},
                {0, 0, 1, 2, 1},
                {1, 0, 0, 2, 1}};
  Console.Write(minTime(arr));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let C = 5;
let R = 3;
let INT_MAX = 10000000;

// DP table to memoize the values
let  table = new Array(R);

// Visited array to keep
    // track of visited nodes
    // in order to avoid infinite loops
let visited = new Array(R);
for(let i = 0; i < R; i++)
{
    table[i] = new Array(C);
    visited[i] = new Array(C);
}

    // Function to return the
    // minimum of four numbers
    function min(p, q, r, s)
    {
        let temp1 = p < q ? p : q;
        let temp2 = r < s ? r : s;

        if (temp1 < temp2)
            return temp1;
        return temp2;
    }

    // Function to return the
    // minimum distance
    // to any rotten orange from [i, j]
    function Distance(arr, i, j)
    {
        // If i, j lie outside the array
        if (i >= R || j >= C || i < 0 || j < 0)
            return INT_MAX;

        // If 0 then it can't lead to
        // any path so return INT_MAX
        else if (arr[i][j] == 0) {
            table[i][j] = INT_MAX;
            return INT_MAX;
        }

        // If 2 then we have reached
        // our rotten oranges
        // so return from here
        else if (arr[i][j] == 2) {
            table[i][j] = 0;
            return 0;
        }

        // If this node is already visited
        // then return to avoid
        // infinite loops
        else if (visited[i][j] == 1) {
            return INT_MAX;
        }
        else {

            // Mark the current node
            // as visited
            visited[i][j] = 1;

            // Check in all four
            // possible directions
            let temp1 = Distance(arr, i + 1, j);
            let temp2 = Distance(arr, i - 1, j);
            let temp3 = Distance(arr, i, j + 1);
            let temp4 = Distance(arr, i, j - 1);

            // Take the minimum of all
            let min_value
                = 1 + min(temp1, temp2, temp3, temp4);

            // If result already exists in
            // the table check if min_value
            // is less than existing value
            if (table[i][j] > 0 &&
                table[i][j] < INT_MAX) {
                if (min_value < table[i][j])
                    table[i][j] = min_value;
            }
            else
                table[i][j] = min_value;

            visited[i][j] = 0;
        }
        return table[i][j];
    }

     // Function to return the minimum time
    // required to rot all the oranges
    function minTime(arr)
    {
        let max = 0;

        // Calculate the minimum
        // distances to any rotten
        // orange from all the fresh oranges
        for (let i = 0; i < R; i++) {
            for (let j = 0; j < C; j++) {
                if (arr[i][j] == 1)
                    Distance(arr, i, j);
            }
        }

        // Pick the maximum distance
        // of fresh orange
        // to some rotten orange
        for (let i = 0; i < R; i++) {
            for (let j = 0; j < C; j++) {
                if (arr[i][j] == 1 &&
                    table[i][j] > max)
                    max = table[i][j];
            }
        }

        // If all oranges can be rotten
        if (max < INT_MAX)
            return max;

        return -1;
    }

    // Driver Code
    let arr = [[ 2, 1, 0, 2, 1],[0, 0, 1, 2, 1 ],[1, 0, 0, 2, 1]]
    document.write(minTime(arr));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
-1
```