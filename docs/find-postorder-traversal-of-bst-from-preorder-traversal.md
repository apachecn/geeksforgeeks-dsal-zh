# 从前序遍历

找到 BST 的后序遍历

> 原文:[https://www . geesforgeks . org/find-post-order-遍历-of-BST-from-preorder-遍历/](https://www.geeksforgeeks.org/find-postorder-traversal-of-bst-from-preorder-traversal/)

给定一个表示 BST 前序遍历的数组，打印它的后序遍历。

**示例:**

```
Input : 40 30 35 80 100
Output : 35 30 100 80 40

Input : 40 30 32 35 80 90 100 120
Output : 35 32 30 120 100 90 80 40
```

**先决条件:** [根据给定的前序遍历](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)构建 BST

**简单方法**:一个简单的解决方案是首先根据给定的前序遍历来构建 BST，如[这篇](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)文章中所述。构造树后，对其执行后序遍历。

**高效方法**:一种高效的方法是在不构建树的情况下找到后序遍历。其思想是遍历给定的前序数组，并保持当前元素应该位于的范围。这是为了确保始终满足 BST 属性。最初，范围设置为{minval = INT_MIN，maxval = INT_MAX}。在预序遍历中，第一个元素总是根，它肯定会位于初始范围内。所以存储前序数组的第一个元素。在后置遍历中，首先打印左右子树，然后打印根数据。所以首先对左右子树进行递归调用，然后打印根的值。对于左子树范围更新为{minval，root- > data}，对于右子树范围更新为{root- > data，maxval}。如果当前的 preorder 数组元素不在为其指定的范围内，则它不属于当前的子树，从递归调用返回，直到找不到该元素的正确位置。

下面是上述方法的实现:

## C++

```
// C++ program for finding postorder
// traversal of BST from preorder traversal
#include <bits/stdc++.h>
using namespace std;

// Function to find postorder traversal from
// preorder traversal.
void findPostOrderUtil(int pre[], int n, int minval,
                       int maxval, int& preIndex)
{

    // If entire preorder array is traversed then
    // return as no more element is left to be
    // added to post order array.
    if (preIndex == n)
        return;

    // If array element does not lie in range specified,
    // then it is not part of current subtree.
    if (pre[preIndex] < minval || pre[preIndex] > maxval) {
        return;
    }

    // Store current value, to be printed later, after
    // printing left and right subtrees. Increment
    // preIndex to find left and right subtrees,
    // and pass this updated value to recursive calls.
    int val = pre[preIndex];
    preIndex++;

    // All elements with value between minval and val
    // lie in left subtree.
    findPostOrderUtil(pre, n, minval, val, preIndex);

    // All elements with value between val and maxval
    // lie in right subtree.
    findPostOrderUtil(pre, n, val, maxval, preIndex);

    cout << val << " ";
}

// Function to find postorder traversal.
void findPostOrder(int pre[], int n)
{

    // To store index of element to be
    // traversed next in preorder array.
    // This is passed by reference to
    // utility function.
    int preIndex = 0;

    findPostOrderUtil(pre, n, INT_MIN, INT_MAX, preIndex);
}

// Driver code
int main()
{
    int pre[] = { 40, 30, 35, 80, 100 };

    int n = sizeof(pre) / sizeof(pre[0]);

    // Calling function
    findPostOrder(pre, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding postorder
// traversal of BST from preorder traversal

import java.util.*;

class Solution {
    static class INT {
        int data;
        INT(int d) { data = d; }
    }

    // Function to find postorder traversal from
    // preorder traversal.
    static void findPostOrderUtil(int pre[], int n,
                                  int minval, int maxval,
                                  INT preIndex)
    {

        // If entire preorder array is traversed then
        // return as no more element is left to be
        // added to post order array.
        if (preIndex.data == n)
            return;

        // If array element does not lie in range specified,
        // then it is not part of current subtree.
        if (pre[preIndex.data] < minval
            || pre[preIndex.data] > maxval) {
            return;
        }

        // Store current value, to be printed later, after
        // printing left and right subtrees. Increment
        // preIndex to find left and right subtrees,
        // and pass this updated value to recursive calls.
        int val = pre[preIndex.data];
        preIndex.data++;

        // All elements with value between minval and val
        // lie in left subtree.
        findPostOrderUtil(pre, n, minval, val, preIndex);

        // All elements with value between val and maxval
        // lie in right subtree.
        findPostOrderUtil(pre, n, val, maxval, preIndex);

        System.out.print(val + " ");
    }

    // Function to find postorder traversal.
    static void findPostOrder(int pre[], int n)
    {

        // To store index of element to be
        // traversed next in preorder array.
        // This is passed by reference to
        // utility function.
        INT preIndex = new INT(0);

        findPostOrderUtil(pre, n, Integer.MIN_VALUE,
                          Integer.MAX_VALUE, preIndex);
    }

    // Driver code
    public static void main(String args[])
    {
        int pre[] = { 40, 30, 35, 80, 100 };

        int n = pre.length;

        // Calling function
        findPostOrder(pre, n);
    }
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
"""Python3 program for finding postorder 
traversal of BST from preorder traversal"""

INT_MIN = -2**31
INT_MAX = 2**31

# Function to find postorder traversal
# from preorder traversal.

def findPostOrderUtil(pre, n, minval,
                      maxval, preIndex):

    # If entire preorder array is traversed
    # then return as no more element is left
    # to be added to post order array.
    if (preIndex[0] == n):
        return

    # If array element does not lie in
    # range specified, then it is not
    # part of current subtree.
    if (pre[preIndex[0]] < minval or
            pre[preIndex[0]] > maxval):
        return

    # Store current value, to be printed later,
    # after printing left and right subtrees.
    # Increment preIndex to find left and right
    # subtrees, and pass this updated value to
    # recursive calls.
    val = pre[preIndex[0]]
    preIndex[0] += 1

    # All elements with value between minval
    # and val lie in left subtree.
    findPostOrderUtil(pre, n, minval,
                      val, preIndex)

    # All elements with value between val
    # and maxval lie in right subtree.
    findPostOrderUtil(pre, n, val,
                      maxval, preIndex)

    print(val, end=" ")

# Function to find postorder traversal.

def findPostOrder(pre, n):

    # To store index of element to be
    # traversed next in preorder array.
    # This is passed by reference to
    # utility function.
    preIndex = [0]

    findPostOrderUtil(pre, n, INT_MIN,
                      INT_MAX, preIndex)

# Driver Code
if __name__ == '__main__':
    pre = [40, 30, 35, 80, 100]

    n = len(pre)

    # Calling function
    findPostOrder(pre, n)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program for finding postorder
// traversal of BST from preorder traversal
using System;

class GFG {
    public class INT {
        public int data;
        public INT(int d) { data = d; }
    }

    // Function to find postorder traversal from
    // preorder traversal.
    public static void findPostOrderUtil(int[] pre, int n,
                                         int minval,
                                         int maxval,
                                         INT preIndex)
    {

        // If entire preorder array is traversed
        // then return as no more element is left
        // to be added to post order array.
        if (preIndex.data == n) {
            return;
        }

        // If array element does not lie in
        // range specified, then it is not
        // part of current subtree.
        if (pre[preIndex.data] < minval
            || pre[preIndex.data] > maxval) {
            return;
        }

        // Store current value, to be printed
        // later, after printing left and right
        // subtrees. Increment preIndex to find
        // left and right subtrees, and pass this
        // updated value to recursive calls.
        int val = pre[preIndex.data];
        preIndex.data++;

        // All elements with value between
        // minval and val lie in left subtree.
        findPostOrderUtil(pre, n, minval, val, preIndex);

        // All elements with value between
        // val and maxval lie in right subtree.
        findPostOrderUtil(pre, n, val, maxval, preIndex);

        Console.Write(val + " ");
    }

    // Function to find postorder traversal.
    public static void findPostOrder(int[] pre, int n)
    {

        // To store index of element to be
        // traversed next in preorder array.
        // This is passed by reference to
        // utility function.
        INT preIndex = new INT(0);

        findPostOrderUtil(pre, n, int.MinValue,
                          int.MaxValue, preIndex);
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] pre = new int[] { 40, 30, 35, 80, 100 };

        int n = pre.Length;

        // Calling function
        findPostOrder(pre, n);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// Javascript program for finding postorder
// traversal of BST from preorder traversal

class INT
{
    constructor(d)
    {
        this.data=d;
    }
}

// Function to find postorder traversal from
    // preorder traversal.
function findPostOrderUtil(pre,n,minval,maxval,preIndex)
{
    // If entire preorder array is traversed then
        // return as no more element is left to be
        // added to post order array.
        if (preIndex.data == n)
            return;

        // If array element does not lie in range specified,
        // then it is not part of current subtree.
        if (pre[preIndex.data] < minval
            || pre[preIndex.data] > maxval) {
            return;
        }

        // Store current value, to be printed later, after
        // printing left and right subtrees. Increment
        // preIndex to find left and right subtrees,
        // and pass this updated value to recursive calls.
        let val = pre[preIndex.data];
        preIndex.data++;

        // All elements with value between minval and val
        // lie in left subtree.
        findPostOrderUtil(pre, n, minval, val, preIndex);

        // All elements with value between val and maxval
        // lie in right subtree.
        findPostOrderUtil(pre, n, val, maxval, preIndex);

        document.write(val + " ");
}

 // Function to find postorder traversal.
function findPostOrder(pre,n)
{
    // To store index of element to be
        // traversed next in preorder array.
        // This is passed by reference to
        // utility function.
        let preIndex = new INT(0);

        findPostOrderUtil(pre, n, Number.MIN_VALUE,
                          Number.MAX_VALUE, preIndex);
}

// Driver code
let pre=[40, 30, 35, 80, 100];
let n = pre.length;
// Calling function
findPostOrder(pre, n);

// This code is contributed by unknown2108
</script>
```

**Output**

```
35 30 100 80 40
```

**时间复杂度:** O(N)，其中 N 为节点数。
**辅助空间:** O(N)(函数调用栈大小)