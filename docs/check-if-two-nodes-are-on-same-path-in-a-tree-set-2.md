# 检查树中两个节点是否在同一路径上|集合 2

> 原文:[https://www . geesforgeks . org/check-if-two-nodes-on-同路径树中-set-2/](https://www.geeksforgeeks.org/check-if-two-nodes-are-on-same-path-in-a-tree-set-2/)

给定二叉树的两个节点 **v1** 和 **v2** ，任务是检查一棵树中的两个节点是否在同一路径上。
**例:**

```
Input:  v1 = 1, v2 = 5
       1
    /  |  \
   2   3   4
  /    |    \
 5     6     7

Output: Yes
Explanation:
Both nodes 1 and 5
lie in the path 1 -> 2 -> 5.

Input: v1 = 2, v2 = 6
       1
    /  |  \
   2   3   4
  /    |    \
 5     6     7

Output: NO
```

**DFS 方法:**参考[检查](https://www.geeksforgeeks.org/check-if-two-nodes-are-on-same-path-in-a-tree/) [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 方法的树中的两个节点是否在同一路径上。
**生命周期评价方法:**想法是使用[最低共同祖先](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。求给定顶点 **v1** 和 **v2** 的 LCA。如果生命周期评价等于任意给定的两个顶点，打印**是**。否则，打印**否**。
以下是上述方法的实施:

## C++

```
// C++ program to check if two nodes
// are on same path in a tree without
// using any extra space
#include <bits/stdc++.h>
using namespace std;

// Function to filter
// the return Values
int filter(int x, int y, int z)
{
    if (x != -1 && y != -1) {
        return z;
    }
    return x == -1 ? y : x;
}

// Utility function to check if nodes
// are on same path or not
int samePathUtil(int mtrx[][7], int vrtx,
                 int v1, int v2, int i)
{
    int ans = -1;

    // Condition to check
    // if any vertex
    // is equal to given two
    // vertex or not
    if (i == v1 || i == v2)
        return i;

    for (int j = 0; j < vrtx; j++) {

        // Check if the current
        // position has 1
        if (mtrx[i][j] == 1) {
            // Recursive call
            ans
                = filter(ans,
                         samePathUtil(mtrx,
                                      vrtx,
                                      v1,
                                      v2,
                                      j),
                         i);
        }
    }

    // Return LCA
    return ans;
}

// Function to check if nodes
// lies on same path or not
bool isVertexAtSamePath(int mtrx[][7],
                        int vrtx, int v1,
                        int v2, int i)
{
    int lca = samePathUtil(mtrx,
                           vrtx, v1 - 1,
                           v2 - 1, i);

    if (lca == v1 - 1 || lca == v2 - 1)
        return true;

    return false;
}

// Driver Program
int main()
{
    int vrtx = 7, edge = 6;
    int mtrx[7][7] = {
        { 0, 1, 1, 1, 0, 0, 0 },
        { 0, 0, 0, 0, 1, 0, 0 },
        { 0, 0, 0, 0, 0, 1, 0 },
        { 0, 0, 0, 0, 0, 0, 1 },
        { 0, 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0, 0 }

    };

    int v1 = 1, v2 = 5;

    if (isVertexAtSamePath(mtrx,
                           vrtx, v1,
                           v2, 0))
        cout << "Yes";

    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two nodes
// are on same path in a tree without
// using any extra space
class GFG{

// Function to filter
// the return Values
static int filter(int x, int y, int z)
{
    if (x != -1 && y != -1)
    {
        return z;
    }
    return x == -1 ? y : x;
}

// Utility function to check if nodes
// are on same path or not
static int samePathUtil(int mtrx[][], int vrtx,
                        int v1, int v2, int i)
{
    int ans = -1;

    // Condition to check
    // if any vertex
    // is equal to given two
    // vertex or not
    if (i == v1 || i == v2)
        return i;

    for(int j = 0; j < vrtx; j++)
    {

        // Check if the current
        // position has 1
        if (mtrx[i][j] == 1)
        {

            // Recursive call
            ans = filter(ans, samePathUtil(
                         mtrx, vrtx, v1,
                         v2, j), i);
        }
    }

    // Return LCA
    return ans;
}

// Function to check if nodes
// lies on same path or not
static boolean isVertexAtSamePath(int mtrx[][],
                                  int vrtx, int v1,
                                  int v2, int i)
{
    int lca = samePathUtil(mtrx, vrtx, v1 - 1,
                                       v2 - 1, i);

    if (lca == v1 - 1 || lca == v2 - 1)
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int vrtx = 7;
    int mtrx[][] = { { 0, 1, 1, 1, 0, 0, 0 },
                     { 0, 0, 0, 0, 1, 0, 0 },
                     { 0, 0, 0, 0, 0, 1, 0 },
                     { 0, 0, 0, 0, 0, 0, 1 },
                     { 0, 0, 0, 0, 0, 0, 0 },
                     { 0, 0, 0, 0, 0, 0, 0 },
                     { 0, 0, 0, 0, 0, 0, 0 } };

    int v1 = 1, v2 = 5;

    if (isVertexAtSamePath(mtrx, vrtx,
                           v1, v2, 0))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if two nodes
# are on same path in a tree without
# using any extra space

# Function to filter
# the return Values
def filter(x, y, z):

    if (x != -1 and y != -1):
        return z

    return y if x == -1 else x

# Utility function to check if nodes
# are on same path or not
def samePathUtil(mtrx, vrtx, v1, v2, i):

    ans = -1

    # Condition to check
    # if any vertex
    # is equal to given two
    # vertex or not
    if (i == v1 or i == v2):
        return i

    for j in range(0, vrtx):

        # Check if the current
        # position has 1
        if (mtrx[i][j] == 1):

            # Recursive call
            ans = filter(ans,
                         samePathUtil(mtrx, vrtx,
                                   v1, v2, j), i)

    # Return LCA
    return ans

# Function to check if nodes
# lies on same path or not
def isVertexAtSamePath(mtrx, vrtx, v1, v2, i):

    lca = samePathUtil(mtrx, vrtx, v1 - 1,
                                   v2 - 1, i)

    if (lca == v1 - 1 or lca == v2 - 1):
        return True

    return False

# Driver code
vrtx = 7
edge = 6

mtrx = [ [ 0, 1, 1, 1, 0, 0, 0 ] ,
         [ 0, 0, 0, 0, 1, 0, 0 ],
         [ 0, 0, 0, 0, 0, 1, 0 ],
         [ 0, 0, 0, 0, 0, 0, 1 ],
         [ 0, 0, 0, 0, 0, 0, 0 ],
         [ 0, 0, 0, 0, 0, 0, 0 ],
         [ 0, 0, 0, 0, 0, 0, 0 ] ]

v1 = 1
v2 = 5

if (isVertexAtSamePath(mtrx, vrtx, v1, v2, 0)):
    print("Yes")
else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to check if two nodes
// are on same path in a tree without
// using any extra space
using System;
class GFG{

// Function to filter
// the return Values
static int filter(int x, int y, int z)
{
    if (x != -1 && y != -1)
    {
        return z;
    }
    return x == -1 ? y : x;
}

// Utility function to check if nodes
// are on same path or not
static int samePathUtil(int [,]mtrx, int vrtx,
                        int v1, int v2, int i)
{
    int ans = -1;

    // Condition to check
    // if any vertex
    // is equal to given two
    // vertex or not
    if (i == v1 || i == v2)
        return i;

    for(int j = 0; j < vrtx; j++)
    {

        // Check if the current
        // position has 1
        if (mtrx[i,j] == 1)
        {

            // Recursive call
            ans = filter(ans, samePathUtil(
                         mtrx, vrtx, v1,
                         v2, j), i);
        }
    }

    // Return LCA
    return ans;
}

// Function to check if nodes
// lies on same path or not
static bool isVertexAtSamePath(int [,]mtrx,
                               int vrtx, int v1,
                               int v2, int i)
{
    int lca = samePathUtil(mtrx, vrtx, v1 - 1,
                                       v2 - 1, i);

    if (lca == v1 - 1 || lca == v2 - 1)
        return true;

    return false;
}

// Driver code
public static void Main(String[] args)
{
    int vrtx = 7;
    int [,]mtrx = { { 0, 1, 1, 1, 0, 0, 0 },
                    { 0, 0, 0, 0, 1, 0, 0 },
                    { 0, 0, 0, 0, 0, 1, 0 },
                    { 0, 0, 0, 0, 0, 0, 1 },
                    { 0, 0, 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0, 0, 0 } };

    int v1 = 1, v2 = 5;

    if (isVertexAtSamePath(mtrx, vrtx,
                           v1, v2, 0))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
    // Javascript program to check if two nodes
    // are on same path in a tree without
    // using any extra space

    // Function to filter
    // the return Values
    function filter(x, y, z)
    {
        if (x != -1 && y != -1)
        {
            return z;
        }
        return x == -1 ? y : x;
    }

    // Utility function to check if nodes
    // are on same path or not
    function samePathUtil(mtrx, vrtx, v1, v2, i)
    {
        let ans = -1;

        // Condition to check
        // if any vertex
        // is equal to given two
        // vertex or not
        if (i == v1 || i == v2)
            return i;

        for(let j = 0; j < vrtx; j++)
        {

            // Check if the current
            // position has 1
            if (mtrx[i][j] == 1)
            {

                // Recursive call
                ans = filter(ans, samePathUtil(
                             mtrx, vrtx, v1,
                             v2, j), i);
            }
        }

        // Return LCA
        return ans;
    }

    // Function to check if nodes
    // lies on same path or not
    function isVertexAtSamePath(mtrx, vrtx, v1, v2, i)
    {
        let lca = samePathUtil(mtrx, vrtx, v1 - 1, v2 - 1, i);

        if (lca == v1 - 1 || lca == v2 - 1)
            return true;

        return false;
    }

    let vrtx = 7;
    let mtrx = [ [ 0, 1, 1, 1, 0, 0, 0 ],
                  [ 0, 0, 0, 0, 1, 0, 0 ],
                  [ 0, 0, 0, 0, 0, 1, 0 ],
                  [ 0, 0, 0, 0, 0, 0, 1 ],
                  [ 0, 0, 0, 0, 0, 0, 0 ],
                  [ 0, 0, 0, 0, 0, 0, 0 ],
                  [ 0, 0, 0, 0, 0, 0, 0 ] ];

    let v1 = 1, v2 = 5;

    if (isVertexAtSamePath(mtrx, vrtx,
                           v1, v2, 0))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by mukesh07.   
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*