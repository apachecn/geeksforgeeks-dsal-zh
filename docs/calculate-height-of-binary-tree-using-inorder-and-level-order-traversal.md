# 使用有序和水平顺序遍历计算二叉树的高度

> 原文:[https://www . geeksforgeeks . org/计算二叉树的高度-使用顺序和级别-顺序-遍历/](https://www.geeksforgeeks.org/calculate-height-of-binary-tree-using-inorder-and-level-order-traversal/)

给定二叉树的有序遍历和水平顺序遍历。任务是计算树的高度，而不构建它。

**示例:**

```
Input : Input: Two arrays that represent Inorder
       and level order traversals of a 
       Binary Tree
       in[]    = {4, 8, 10, 12, 14, 20, 22};
       level[] = {20, 8, 22, 4, 12, 10, 14};
Output : 4

The binary tree that can be constructed from the 
given traversals is:
```

![](img/6ff52d250332ea7fd79970a957e63dac.png)

```
We can clearly see in the above image that the 
height of the tree is 4.
```

计算高度的方法类似于在文章[中讨论的从有序和水平顺序遍历](https://www.geeksforgeeks.org/construct-tree-inorder-level-order-traversals/)构建树的方法。
让我们考虑一下上面的例子。
in[] = {4，8，10，12，14，20，22 }；
等级[] = {20，8，22，4，12，10，14 }；
在 Levelorder 序列中，第一个元素是树的根。所以我们知道‘20’是给定序列的根。通过按顺序搜索“20”，我们可以发现“20”左侧的所有元素都在左子树中，右侧的元素都在右子树中。所以我们现在知道下面的结构。

```
             20
           /    \
          /      \ 
 {4, 8, 10, 12, 14}  {22}   
```

让我们将{4，8，10，12，14}称为有序遍历中的左子数组，将{22}称为有序遍历中的右子数组。
在级序遍历中，左右子树的键不连续。因此，我们从水平顺序遍历中提取出所有位于有序遍历的左子阵中的节点。为了计算根的左子树的高度，我们对从水平顺序遍历和顺序遍历的左子数组中提取的元素进行递归。在上面的例子中，我们重现了下面两个数组。

```
// Recur for following arrays to 
// calculate the height of the left subtree
In[]    = {4, 8, 10, 12, 14}
level[] = {8, 4, 12, 10, 14} 
```

同样，我们重复下面两个数组，并计算右边子树的高度。

```
// Recur for following arrays to calculate
// height of the right subtree
In[]    = {22}
level[] = {22} 
```

下面是上述方法的实现:

## C++

```
// C++ program to caulate height of Binary Tree
// from InOrder and LevelOrder Traversals
#include <iostream>
using namespace std;

/* Function to find index of value
   in the InOrder Traversal array */
int search(int arr[], int strt, int end, int value)
{
    for (int i = strt; i <= end; i++)
        if (arr[i] == value)
            return i;
    return -1;
}

// Function to calculate the height
// of the Binary Tree
int getHeight(int in[], int level[], int start,
              int end, int& height, int n)
{

    // Base Case
    if (start > end)
        return 0;

    // Get index of current root in InOrder Traversal
    int getIndex = search(in, start, end, level[0]);

    if (getIndex == -1)
        return 0;

    // Count elements in Left Subtree
    int leftCount = getIndex - start;

    // Count elements in right Subtree
    int rightCount = end - getIndex;

    // Declare two arrays for left and
    // right subtrees
    int* newLeftLevel = new int[leftCount];
    int* newRightLevel = new int[rightCount];

    int lheight = 0, rheight = 0;
    int k = 0;

    // Extract values from level order traversal array
    // for current left subtree
    for (int i = 0; i < n; i++) {
        for (int j = start; j < getIndex; j++) {
            if (level[i] == in[j]) {
                newLeftLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    k = 0;

    // Extract values from level order traversal array
    // for current right subtree
    for (int i = 0; i < n; i++) {
        for (int j = getIndex + 1; j <= end; j++) {
            if (level[i] == in[j]) {
                newRightLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    // Recursively call to calculate height of left Subtree
    if (leftCount > 0)
        lheight = getHeight(in, newLeftLevel, start,
                            getIndex - 1, height, leftCount);

    // Recursively call to calculate height of right Subtree
    if (rightCount > 0)
        rheight = getHeight(in, newRightLevel,
                            getIndex + 1, end, height, rightCount);

    // Current height
    height = max(lheight + 1, rheight + 1);

    // Delete Auxiliary arrays
    delete[] newRightLevel;
    delete[] newLeftLevel;

    // return height
    return height;
}

// Driver program to test above functions
int main()
{
    int in[] = { 4, 8, 10, 12, 14, 20, 22 };
    int level[] = { 20, 8, 22, 4, 12, 10, 14 };
    int n = sizeof(in) / sizeof(in[0]);

    int h = 0;

    cout << getHeight(in, level, 0, n - 1, h, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to caulate height of Binary Tree
// from InOrder and LevelOrder Traversals
import java.util.*;
class GFG
{
static int height;

/* Function to find index of value
in the InOrder Traversal array */
static int search(int arr[], int strt,
                  int end, int value)
{
    for (int i = strt; i <= end; i++)
        if (arr[i] == value)
            return i;
    return -1;
}

// Function to calculate the height
// of the Binary Tree
static int getHeight(int in[], int level[],
                     int start, int end, int n)
{

    // Base Case
    if (start > end)
        return 0;

    // Get index of current root in InOrder Traversal
    int getIndex = search(in, start, end, level[0]);

    if (getIndex == -1)
        return 0;

    // Count elements in Left Subtree
    int leftCount = getIndex - start;

    // Count elements in right Subtree
    int rightCount = end - getIndex;

    // Declare two arrays for left and
    // right subtrees
    int []newLeftLevel = new int[leftCount];
    int []newRightLevel = new int[rightCount];

    int lheight = 0, rheight = 0;
    int k = 0;

    // Extract values from level order traversal array
    // for current left subtree
    for (int i = 0; i < n; i++)
    {
        for (int j = start; j < getIndex; j++)
        {
            if (level[i] == in[j])
            {
                newLeftLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    k = 0;

    // Extract values from level order traversal array
    // for current right subtree
    for (int i = 0; i < n; i++)
    {
        for (int j = getIndex + 1; j <= end; j++)
        {
            if (level[i] == in[j])
            {
                newRightLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    // Recursively call to calculate
    // height of left Subtree
    if (leftCount > 0)
        lheight = getHeight(in, newLeftLevel, start,
                  getIndex - 1, leftCount);

    // Recursively call to calculate
    // height of right Subtree
    if (rightCount > 0)
        rheight = getHeight(in, newRightLevel,
                  getIndex + 1, end, rightCount);

    // Current height
    height = Math.max(lheight + 1, rheight + 1);

    // Delete Auxiliary arrays
    newRightLevel=null;
    newLeftLevel=null;

    // return height
    return height;
}

// Driver program to test above functions
public static void main(String[] args)
{
    int in[] = {4, 8, 10, 12, 14, 20, 22};
    int level[] = {20, 8, 22, 4, 12, 10, 14};
    int n = in.length;

    height = 0;

    System.out.println(getHeight(in, level, 0, n - 1, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to calculate height of Binary Tree from
# InOrder and LevelOrder Traversals

'''
Function to find the index of value in the InOrder
Traversal list
'''

def search(arr, start, end, value):
    for i in range(start, end + 1):
        if arr[i] == value:
            return i
    return -1

'''
Function to calculate the height of the Binary Tree
'''
def getHeight(inOrder, levelOrder,
              start, end, height, n):

    # Base Case
    if start > end:
        return 0

    # Get Index of current root in InOrder Traversal
    getIndex = search(inOrder, start, end, levelOrder[0])

    if getIndex == -1:
        return 0

    # Count elements in Left Subtree
    leftCount = getIndex - start

    # Count elements in Right Subtree
    rightCount = end - getIndex

    # Declare two lists for left and right subtrees
    newLeftLevel = [None for _ in range(leftCount)]
    newRightLevel = [None for _ in range(rightCount)]

    lheight, rheight, k = 0, 0, 0

    # Extract values from level order traversal list
    # for current left subtree
    for i in range(n):
        for j in range(start, getIndex):
            if levelOrder[i] == inOrder[j]:
                newLeftLevel[k] = levelOrder[i]
                k += 1
                break

    k = 0

    # Extract values from level order traversal list
    # for current right subtree
    for i in range(n):
        for j in range(getIndex + 1, end + 1):
            if levelOrder[i] == inOrder[j]:
                newRightLevel[k] = levelOrder[i]
                k += 1
                break

    # Recursively call to calculate height
    # of left subtree
    if leftCount > 0:
        lheight = getHeight(inOrder, newLeftLevel, start,
                            getIndex - 1, height, leftCount)

    # Recursively call to calculate height
    # of right subtree
    if rightCount > 0:
        rheight = getHeight(inOrder, newRightLevel,
                            getIndex + 1, end, height, rightCount)

    # current height
    height = max(lheight + 1, rheight + 1)

    # return height
    return height

# Driver Code
if __name__=='__main__':
    inOrder = [4, 8, 10, 12, 14, 20, 22]
    levelOrder = [20, 8, 22, 4, 12, 10, 14]
    n, h = len(inOrder), 0
    print(getHeight(inOrder, levelOrder, 0, n - 1, h, n))

# This code is contributed by harshraj22
```

## C#

```
// C# program to caulate height of Binary Tree
// from InOrder and LevelOrder Traversals
using System;
using System.Collections.Generic;

class GFG
{
static int height;

/* Function to find index of value
in the InOrder Traversal array */
static int search(int []arr, int strt,
                  int end, int value)
{
    for (int i = strt; i <= end; i++)
        if (arr[i] == value)
            return i;
    return -1;
}

// Function to calculate the height
// of the Binary Tree
static int getHeight(int []In, int []level,
                     int start, int end, int n)
{

    // Base Case
    if (start > end)
        return 0;

    // Get index of current root in
    // InOrder Traversal
    int getIndex = search(In, start, end, level[0]);

    if (getIndex == -1)
        return 0;

    // Count elements in Left Subtree
    int leftCount = getIndex - start;

    // Count elements in right Subtree
    int rightCount = end - getIndex;

    // Declare two arrays for left and
    // right subtrees
    int []newLeftLevel = new int[leftCount];
    int []newRightLevel = new int[rightCount];

    int lheight = 0, rheight = 0;
    int k = 0;

    // Extract values from level order traversal array
    // for current left subtree
    for (int i = 0; i < n; i++)
    {
        for (int j = start; j < getIndex; j++)
        {
            if (level[i] == In[j])
            {
                newLeftLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    k = 0;

    // Extract values from level order traversal array
    // for current right subtree
    for (int i = 0; i < n; i++)
    {
        for (int j = getIndex + 1; j <= end; j++)
        {
            if (level[i] == In[j])
            {
                newRightLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    // Recursively call to calculate
    // height of left Subtree
    if (leftCount > 0)
        lheight = getHeight(In, newLeftLevel, start,
                  getIndex - 1, leftCount);

    // Recursively call to calculate
    // height of right Subtree
    if (rightCount > 0)
        rheight = getHeight(In, newRightLevel,
                  getIndex + 1, end, rightCount);

    // Current height
    height = Math.Max(lheight + 1, rheight + 1);

    // Delete Auxiliary arrays
    newRightLevel = null;
    newLeftLevel = null;

    // return height
    return height;
}

// Driver Code
public static void Main(String[] args)
{
    int []In = {4, 8, 10, 12, 14, 20, 22};
    int []level = {20, 8, 22, 4, 12, 10, 14};
    int n = In.Length;

    height = 0;

    Console.WriteLine(getHeight(In, level, 0, n - 1, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

//Javascript program to caulate height of Binary Tree
// from InOrder and LevelOrder Traversals

var height = 0;

/* Function to find index of value
in the InOrder Traversal array */
function search(arr, strt, end, value)
{
    for (var i = strt; i <= end; i++)
        if (arr[i] == value)
            return i;
    return -1;
}

// Function to calculate the height
// of the Binary Tree
function getHeight(In, level, start, end, n)
{

    // Base Case
    if (start > end)
        return 0;

    // Get index of current root in
    // InOrder Traversal
    var getIndex = search(In, start, end, level[0]);

    if (getIndex == -1)
        return 0;

    // Count elements in Left Subtree
    var leftCount = getIndex - start;

    // Count elements in right Subtree
    var rightCount = end - getIndex;

    // Declare two arrays for left and
    // right subtrees
    var newLeftLevel = Array(leftCount);
    var newRightLevel = Array(rightCount);

    var lheight = 0, rheight = 0;
    var k = 0;

    // Extract values from level order traversal array
    // for current left subtree
    for (var i = 0; i < n; i++)
    {
        for (var j = start; j < getIndex; j++)
        {
            if (level[i] == In[j])
            {
                newLeftLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    k = 0;

    // Extract values from level order traversal array
    // for current right subtree
    for (var i = 0; i < n; i++)
    {
        for (var j = getIndex + 1; j <= end; j++)
        {
            if (level[i] == In[j])
            {
                newRightLevel[k] = level[i];
                k++;
                break;
            }
        }
    }

    // Recursively call to calculate
    // height of left Subtree
    if (leftCount > 0)
        lheight = getHeight(In, newLeftLevel, start,
                  getIndex - 1, leftCount);

    // Recursively call to calculate
    // height of right Subtree
    if (rightCount > 0)
        rheight = getHeight(In, newRightLevel,
                  getIndex + 1, end, rightCount);

    // Current height
    height = Math.max(lheight + 1, rheight + 1);

    // Delete Auxiliary arrays
    newRightLevel = null;
    newLeftLevel = null;

    // return height
    return height;
}

// Driver Code
var In = [4, 8, 10, 12, 14, 20, 22];
var level = [20, 8, 22, 4, 12, 10, 14];
var n = In.length;
height = 0;
document.write(getHeight(In, level, 0, n - 1, n));

</script>
```

**输出**:

```
4
```