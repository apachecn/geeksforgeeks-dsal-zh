# 检查给定的顺序和前序遍历是否对任何二叉树有效，而无需构建树

> 原文:[https://www . geeksforgeeks . org/check-if-given-order-and-preorder-traversals-对任何没有构建树的二叉树都有效/](https://www.geeksforgeeks.org/check-if-given-inorder-and-preorder-traversals-are-valid-for-any-binary-tree-without-building-the-tree/)

给定两个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**pre【】**和**in【】**代表二叉树的[前序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)和[后序遍历，任务是检查给定的遍历对于任何](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)是否有效，而无需[构建树](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)。如果可能，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** pre[] = {1，2，4，5，7，3，6，8}，in[] = {4，2，5，7，1，6，8，3}
> **输出:** Yes
> **解释:**
> 两个遍历对以下二叉树都有效:
> 1
> /
> 2 3
> /\
> 4 5 6
> \ \
> 7
> 
> **输入:** pre[] = {1，2，69，5，7，3，6，8}，in[] = {4，2，5，7，1，6，8，3}
> **输出:**否

**方法:**想法是使用类似的技术[从有序和前序遍历](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)构建二叉树，除了不构建树，而是检查该树(子树)的当前有序遍历和当前前序索引在每个[递归调用](https://www.geeksforgeeks.org/recursion/)中是否有效。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// C++ program to check if given inorder
// and preorder traversals of size N are
// valid for a binary tree or not
bool checkInorderPreorderUtil(
    int inStart, int inEnd,
    int& preIndex, int preorder[],
    unordered_map<int, int>& inorderIndexMap)
{
    if (inStart > inEnd)
        return true;

    // Build the current Node
    int rootData = preorder[preIndex];
    preIndex++;

    // If the element at current Index
    // is not present in the inorder
    // then tree can't be built
    if (inorderIndexMap.find(rootData)
        == inorderIndexMap.end())
        return false;

    int inorderIndex = inorderIndexMap[rootData];

    // If the inorderIndex does not fall
    // within the range of the inorder
    // traversal of the current tree
    // then return false
    if (!(inStart <= inorderIndex
          && inorderIndex <= inEnd))
        return false;

    int leftInorderStart = inStart;
    int leftInorderEnd = inorderIndex - 1;
    int rightInorderStart = inorderIndex + 1;
    int rightInorderEnd = inEnd;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    if (!checkInorderPreorderUtil(
            leftInorderStart, leftInorderEnd,
            preIndex, preorder, inorderIndexMap))
        return false;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    else
        return checkInorderPreorderUtil(
            rightInorderStart, rightInorderEnd,
            preIndex, preorder, inorderIndexMap);
}

// Function to check for the validation of
// inorder and preorder
string checkInorderPreorder(
    int pre[], int in[], int n)
{
    unordered_map<int, int> inorderIndexMap;

    for (int i = 0; i < n; i++)
        inorderIndexMap[in[i]] = i;

    int preIndex = 0;
    if (checkInorderPreorderUtil(
            0, n - 1, preIndex,
            pre, inorderIndexMap)) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
int main()
{
    int pre[] = { 1, 2, 4, 5, 7, 3, 6, 8 };
    int in[] = { 4, 2, 5, 7, 1, 6, 8, 3 };
    int N = sizeof(pre) / sizeof(pre[0]);
    cout << checkInorderPreorder(pre, in, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given inorder
// and preorder traversals of size N are
// valid for a binary tree or not
import java.util.*;

class GFG
{
    static int preIndex;
    static HashMap<Integer,Integer> inorderIndexMap = new HashMap<Integer,Integer>();

static boolean checkInorderPreorderUtil(
    int inStart, int inEnd,
     int preorder[])
{
    if (inStart > inEnd)
        return true;

    // Build the current Node
    int rootData = preorder[preIndex];
    preIndex++;

    // If the element at current Index
    // is not present in the inorder
    // then tree can't be built
    if (!inorderIndexMap.containsKey(rootData))
        return false;

    int inorderIndex = inorderIndexMap.get(rootData);

    // If the inorderIndex does not fall
    // within the range of the inorder
    // traversal of the current tree
    // then return false
    if (!(inStart <= inorderIndex
          && inorderIndex <= inEnd))
        return false;

    int leftInorderStart = inStart;
    int leftInorderEnd = inorderIndex - 1;
    int rightInorderStart = inorderIndex + 1;
    int rightInorderEnd = inEnd;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    if (!checkInorderPreorderUtil(
            leftInorderStart, leftInorderEnd,preorder))
        return false;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    else
        return checkInorderPreorderUtil(
            rightInorderStart, rightInorderEnd,
             preorder);
}

// Function to check for the validation of
// inorder and preorder
static String checkInorderPreorder(
    int pre[], int in[], int n)
{

    //HashMap<Integer,Integer> inorderIndexMap = new HashMap<Integer,Integer>();
    for (int i = 0; i < n; i++)
        inorderIndexMap.put(in[i], i);

    preIndex = 0;
    if (checkInorderPreorderUtil(
            0, n - 1,
            pre)) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
public static void main(String[] args)
{
    int pre[] = { 1, 2, 4, 5, 7, 3, 6, 8 };
    int in[] = { 4, 2, 5, 7, 1, 6, 8, 3 };
    int N = pre.length;
    System.out.print(checkInorderPreorder(pre, in, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program to check if given inorder
# and preorder traversals of size N are
# valid for a binary tree or not
def checkInorderPreorderUtil(inStart, inEnd, preIndex, preorder, inorderIndexMap):
    if (inStart > inEnd):
        return True

    # Build the current Node
    rootData = preorder[preIndex]
    preIndex += 1

    # If the element at current Index
    # is not present in the inorder
    # then tree can't be built
    if (rootData in inorderIndexMap):
        return False

    inorderIndex = inorderIndexMap[rootData]

    # If the inorderIndex does not fall
    # within the range of the inorder
    # traversal of the current tree
    # then return false
    if ((inStart <= inorderIndex and inorderIndex <= inEnd)==False):
        return False

    leftInorderStart = inStart
    leftInorderEnd = inorderIndex - 1
    rightInorderStart = inorderIndex + 1
    rightInorderEnd = inEnd

    # Check if the left subtree can be
    # built from the inorder traversal
    # of the left subtree and preorder
    if(checkInorderPreorderUtil(leftInorderStart,leftInorderEnd,preIndex,preorder,inorderIndexMap)==False):
        return False

    # Check if the left subtree can be
    # built from the inorder traversal
    # of the left subtree and preorder
    else:
        return checkInorderPreorderUtil(rightInorderStart, rightInorderEnd,preIndex, preorder, inorderIndexMap)

# Function to check for the validation of
# inorder and preorder
def checkInorderPreorder(pre, inv,n):
    inorderIndexMap = {}

    for i in range(n):
        inorderIndexMap[inv[i]] = i

    preIndex = 0
    if (checkInorderPreorderUtil(0, n - 1, preIndex,pre, inorderIndexMap)):
        return "No"
    else:
        return "Yes"

# Driver Code
if __name__ == '__main__':
    pre = [1, 2, 4, 5, 7, 3, 6, 8]
    inv = [4, 2, 5, 7, 1, 6, 8, 3]
    N = len(pre)
    print(checkInorderPreorder(pre, inv, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program to check if given inorder
// and preorder traversals of size N are
// valid for a binary tree or not
using System;
using System.Collections.Generic;

public class GFG
{
    static int preIndex;
    static Dictionary<int,int> inorderIndexMap = new Dictionary<int,int>();

static bool checkInorderPreorderUtil(
    int inStart, int inEnd,
     int []preorder)
{
    if (inStart > inEnd)
        return true;

    // Build the current Node
    int rootData = preorder[preIndex];
    preIndex++;

    // If the element at current Index
    // is not present in the inorder
    // then tree can't be built
    if (!inorderIndexMap.ContainsKey(rootData))
        return false;

    int inorderIndex = inorderIndexMap[rootData];

    // If the inorderIndex does not fall
    // within the range of the inorder
    // traversal of the current tree
    // then return false
    if (!(inStart <= inorderIndex
          && inorderIndex <= inEnd))
        return false;

    int leftInorderStart = inStart;
    int leftInorderEnd = inorderIndex - 1;
    int rightInorderStart = inorderIndex + 1;
    int rightInorderEnd = inEnd;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    if (!checkInorderPreorderUtil(
            leftInorderStart, leftInorderEnd,preorder))
        return false;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    else
        return checkInorderPreorderUtil(
            rightInorderStart, rightInorderEnd,
             preorder);
}

// Function to check for the validation of
// inorder and preorder
static String checkInorderPreorder(
    int []pre, int []inn, int n)
{

    // Dictionary<int,int> inorderIndexMap = new Dictionary<int,int>();
    for (int i = 0; i < n; i++)
        inorderIndexMap.Add(inn[i], i);

    preIndex = 0;
    if (checkInorderPreorderUtil(
            0, n - 1,
            pre)) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []pre = { 1, 2, 4, 5, 7, 3, 6, 8 };
    int []inn = { 4, 2, 5, 7, 1, 6, 8, 3 };
    int N = pre.Length;
    Console.Write(checkInorderPreorder(pre, inn, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach
let inorderIndexMap = new Map();
let preIndex;

function checkInorderPreorderUtil( inStart, inEnd, preorder)
{
    if (inStart > inEnd)
        return true;

    // Build the current Node
    let rootData = preorder[preIndex];
    preIndex++;

    // If the element at current Index
    // is not present in the inorder
    // then tree can't be built
    if (!inorderIndexMap.has(rootData))
        return false;

    let inorderIndex = inorderIndexMap.get(rootData);

    // If the inorderIndex does not fall
    // within the range of the inorder
    // traversal of the current tree
    // then return false
    if (!(inStart <= inorderIndex
          && inorderIndex <= inEnd))
        return false;

    let leftInorderStart = inStart;
    let leftInorderEnd = inorderIndex - 1;
    let rightInorderStart = inorderIndex + 1;
    let rightInorderEnd = inEnd;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    if (!checkInorderPreorderUtil(
            leftInorderStart, leftInorderEnd, preorder))
        return false;

    // Check if the left subtree can be
    // built from the inorder traversal
    // of the left subtree and preorder
    else
        return checkInorderPreorderUtil(
            rightInorderStart, rightInorderEnd, preorder);
}

// Function to check for the validation of
// inorder and preorder
function checkInorderPreorder(pre, inn, n)
{

    for (let i = 0; i < n; i++)
        inorderIndexMap.set(inn[i], i);

    preIndex = 0;
    if (checkInorderPreorderUtil(
            0, n - 1,
            pre )) {
        return "Yes";
    }
    else {
        return "No";
    }
}

// Driver Code
    let pre = [ 1, 2, 4, 5, 7, 3, 6, 8 ];
    let inn = [ 4, 2, 5, 7, 1, 6, 8, 3 ];
    let N = pre.length;
    document.write(checkInorderPreorder(pre, inn, N));

    // This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)