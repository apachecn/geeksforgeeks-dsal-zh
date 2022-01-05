# 二叉查找树的叶节

> 原文:[https://www . geesforgeks . org/leaf-nodes-preorder-binary-search-tree/](https://www.geeksforgeeks.org/leaf-nodes-preorder-binary-search-tree/)

给定一个二叉查找树的预序遍历。任务是打印给定订单中二叉查找树的叶节点。
**例:**

```
Input : preorder[] = {890, 325, 290, 530, 965};
Output : 290 530 965
Explanation : Tree represented is,
      890
     /   \
  325    965
  /  \
290   530

Input : preorder[] = { 3, 2, 4 };
Output : 2 4
```

**方法一:(简单)**

想法是找到 Iorder，然后以前序方式遍历树(使用有序和后序遍历)，同时遍历打印叶节点。
如何使用两个表示有序和有序遍历的数组以有序方式遍历？
我们迭代前序数组，并为每个元素找到有序数组中的那个元素。对于搜索，我们可以使用二分搜索法，因为二叉查找树的有序遍历总是排序的。现在，对于前序数组的每个元素，在二分搜索法，我们设置范围[L，R]。
当 L == R 时，找到叶节点。所以，最初，对于前序数组的第一个元素(即根)，L = 0，R = n–1。现在，要搜索根的左子树上的元素，请设置 L = 0，R =根的索引–1。同样，对于右子树集的所有元素，L =根的索引+ 1，R = n -1。
递归地，遵循这个，直到 L == R.
下面是这个方法的实现:

## C++

```
// C++ program to print leaf node from
// preorder of binary search tree.
#include<bits/stdc++.h>
using namespace std;

// Binary Search
int binarySearch(int inorder[], int l, int r, int d)
{
    int mid = (l + r)>>1;

    if (inorder[mid] == d)
        return mid;

    else if (inorder[mid] > d)
        return binarySearch(inorder, l, mid - 1, d);

    else
        return binarySearch(inorder, mid + 1, r, d);
}

// Function to print Leaf Nodes by doing preorder
// traversal of tree using preorder and inorder arrays.
void leafNodesRec(int preorder[], int inorder[],
                  int l, int r, int *ind, int n)
{
    // If l == r, therefore no right or left subtree.
    // So, it must be leaf Node, print it.
    if(l == r)
    {
        printf("%d ", inorder[l]);
        *ind = *ind + 1;
        return;
    }

    // If array is out of bound, return.
    if (l < 0 || l > r || r >= n)
        return;

    // Finding the index of preorder element
    // in inorder array using binary search.
    int loc = binarySearch(inorder, l, r, preorder[*ind]);

    // Incrementing the index.
    *ind = *ind + 1;

    // Finding on the left subtree.
    leafNodesRec(preorder, inorder, l, loc - 1, ind, n);

    // Finding on the right subtree.
    leafNodesRec(preorder, inorder, loc + 1, r, ind, n);
}

// Finds leaf nodes from given preorder traversal.
void leafNodes(int preorder[], int n)
{
    int inorder[n];  // To store inorder traversal

    // Copy the preorder into another array.
    for (int i = 0; i < n; i++)
        inorder[i] = preorder[i];

    // Finding the inorder by sorting the array.
    sort(inorder, inorder + n);

    // Point to the index in preorder.
    int ind = 0;

    // Print the Leaf Nodes.
    leafNodesRec(preorder, inorder, 0, n - 1, &ind, n);
}

// Driven Program
int main()
{
    int preorder[] = { 890, 325, 290, 530, 965 };
    int n = sizeof(preorder)/sizeof(preorder[0]);

    leafNodes(preorder, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print leaf node from
// preorder of binary search tree.
import java.util.*;

class GFG
{

// Binary Search
static int binarySearch(int inorder[], int l,
                        int r, int d)
{
    int mid = (l + r) >> 1;

    if (inorder[mid] == d)
        return mid;

    else if (inorder[mid] > d)
        return binarySearch(inorder, l,
                            mid - 1, d);

    else
        return binarySearch(inorder,
                            mid + 1, r, d);
}

// Point to the index in preorder.
static int ind;

// Function to print Leaf Nodes by
// doing preorder traversal of tree
// using preorder and inorder arrays.
static void leafNodesRec(int preorder[],
                         int inorder[],
                         int l, int r, int n)
{
    // If l == r, therefore no right or left subtree.
    // So, it must be leaf Node, print it.
    if(l == r)
    {
        System.out.printf("%d ", inorder[l]);
        ind = ind + 1;
        return;
    }

    // If array is out of bound, return.
    if (l < 0 || l > r || r >= n)
        return;

    // Finding the index of preorder element
    // in inorder array using binary search.
    int loc = binarySearch(inorder, l, r,
                           preorder[ind]);

    // Incrementing the index.
    ind = ind + 1;

    // Finding on the left subtree.
    leafNodesRec(preorder, inorder,
                    l, loc - 1, n);

    // Finding on the right subtree.
    leafNodesRec(preorder, inorder,
                    loc + 1, r, n);
}

// Finds leaf nodes from given preorder traversal.
static void leafNodes(int preorder[], int n)
{
    // To store inorder traversal
    int inorder[] = new int[n];

    // Copy the preorder into another array.
    for (int i = 0; i < n; i++)
        inorder[i] = preorder[i];

    // Finding the inorder by sorting the array.
    Arrays.sort(inorder);

    // Print the Leaf Nodes.
    leafNodesRec(preorder, inorder, 0, n - 1, n);
}

// Driver Code
public static void main(String args[])
{
    int preorder[] = { 890, 325, 290, 530, 965 };
    int n = preorder.length;

    leafNodes(preorder, n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print leaf node from
# preorder of binary search tree.

# Binary Search
def binarySearch(inorder, l, r, d):

    mid = (l + r) >> 1
    if (inorder[mid] == d):
        return mid
    elif (inorder[mid] > d):
        return binarySearch(inorder, l,
                            mid - 1, d)
    else:
        return binarySearch(inorder,
                            mid + 1, r, d)

# Function to prLeaf Nodes by doing
# preorder traversal of tree using
# preorder and inorder arrays.
def leafNodesRec(preorder, inorder,
                      l, r, ind, n):

    # If l == r, therefore no right or left subtree.
    # So, it must be leaf Node, print it.
    if(l == r):
        print(inorder[l], end = " ")
        ind[0] = ind[0] + 1
        return

    # If array is out of bound, return.
    if (l < 0 or l > r or r >= n):
        return

    # Finding the index of preorder element
    # in inorder array using binary search.
    loc = binarySearch(inorder, l, r,
                       preorder[ind[0]])

    # Incrementing the index.
    ind[0] = ind[0] + 1

    # Finding on the left subtree.
    leafNodesRec(preorder, inorder,    
                 l, loc - 1, ind, n)

    # Finding on the right subtree.
    leafNodesRec(preorder, inorder,
                 loc + 1, r, ind, n)

# Finds leaf nodes from
# given preorder traversal.
def leafNodes(preorder, n):

    # To store inorder traversal
    inorder = [0] * n

    # Copy the preorder into another array.
    for i in range(n):
        inorder[i] = preorder[i]

    # Finding the inorder by sorting the array.
    inorder.sort()

    # Poto the index in preorder.
    ind = [0]

    # Print the Leaf Nodes.
    leafNodesRec(preorder, inorder, 0,
                 n - 1, ind, n)

# Driver Code
preorder = [890, 325, 290, 530, 965]
n = len(preorder)
leafNodes(preorder, n)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to print leaf node from
// preorder of binary search tree.
using System;

class GFG
{

// Binary Search
static int binarySearch(int []inorder, int l,
                        int r, int d)
{
    int mid = (l + r) >> 1;

    if (inorder[mid] == d)
        return mid;

    else if (inorder[mid] > d)
        return binarySearch(inorder, l,
                            mid - 1, d);

    else
        return binarySearch(inorder,
                            mid + 1, r, d);
}

// Point to the index in preorder.
static int ind;

// Function to print Leaf Nodes by
// doing preorder traversal of tree
// using preorder and inorder arrays.
static void leafNodesRec(int []preorder,
                        int []inorder,
                        int l, int r, int n)
{
    // If l == r, therefore no right or left subtree.
    // So, it must be leaf Node, print it.
    if(l == r)
    {
        Console.Write("{0} ", inorder[l]);
        ind = ind + 1;
        return;
    }

    // If array is out of bound, return.
    if (l < 0 || l > r || r >= n)
        return;

    // Finding the index of preorder element
    // in inorder array using binary search.
    int loc = binarySearch(inorder, l, r,
                        preorder[ind]);

    // Incrementing the index.
    ind = ind + 1;

    // Finding on the left subtree.
    leafNodesRec(preorder, inorder,
                    l, loc - 1, n);

    // Finding on the right subtree.
    leafNodesRec(preorder, inorder,
                    loc + 1, r, n);
}

// Finds leaf nodes from given preorder traversal.
static void leafNodes(int []preorder, int n)
{
    // To store inorder traversal
    int []inorder = new int[n];

    // Copy the preorder into another array.
    for (int i = 0; i < n; i++)
        inorder[i] = preorder[i];

    // Finding the inorder by sorting the array.
    Array.Sort(inorder);

    // Print the Leaf Nodes.
    leafNodesRec(preorder, inorder, 0, n - 1, n);
}

// Driver Code
public static void Main(String []args)
{
    int []preorder = { 890, 325, 290, 530, 965 };
    int n = preorder.Length;

    leafNodes(preorder, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript program to print leaf node from
      // preorder of binary search tree.
      // Binary Search
      function binarySearch(inorder, l, r, d) {
        var mid = parseInt((l + r) / 2);

        if (inorder[mid] == d) return mid;
        else if (inorder[mid] > d)
        return binarySearch(inorder, l, mid - 1, d);
        else
        return binarySearch(inorder, mid + 1, r, d);
      }

      // Point to the index in preorder.
      var ind = 0;

      // Function to print Leaf Nodes by
      // doing preorder traversal of tree
      // using preorder and inorder arrays.
      function leafNodesRec(preorder, inorder, l, r, n) {
        // If l == r, therefore no right or left subtree.
        // So, it must be leaf Node, print it.
        if (l == r) {
          document.write(inorder[l] + " ");
          ind = ind + 1;
          return;
        }

        // If array is out of bound, return.
        if (l < 0 || l > r || r >= n) return;

        // Finding the index of preorder element
        // in inorder array using binary search.
        var loc = binarySearch(inorder, l, r, preorder[ind]);

        // Incrementing the index.
        ind = ind + 1;

        // Finding on the left subtree.
        leafNodesRec(preorder, inorder, l, loc - 1, n);

        // Finding on the right subtree.
        leafNodesRec(preorder, inorder, loc + 1, r, n);
      }

      // Finds leaf nodes from given preorder traversal.
      function leafNodes(preorder, n) {
        // To store inorder traversal
        var inorder = new Array(n).fill(0);

        // Copy the preorder into another array.
        for (var i = 0; i < n; i++) inorder[i] = preorder[i];

        // Finding the inorder by sorting the array.
        inorder.sort();

        // Print the Leaf Nodes.
        leafNodesRec(preorder, inorder, 0, n - 1, n);
      }

      // Driver Code
      var preorder = [890, 325, 290, 530, 965];
      var n = preorder.length;

      leafNodes(preorder, n);

</script>
```

**输出:**

```
290 530 965
```

**时间复杂度:**O(n log n)
T3】辅助空间: O(n)

**方法二:(使用 Stack)**

这个想法是利用二叉查找树和斯塔克的财产。
使用指向数组的两个指针 I 和 j 遍历数组，最初 i = 0，j = 1。每当 a[i] > a[j]时，我们可以说 a[j]是 a[i]的左边部分，因为前序遍历遵循 Visit - > Left - > Right。因此，我们在堆栈中插入一个[i]。
对于那些违反规则的点，我们开始从堆栈中弹出元素，直到堆栈的一个【I】>顶部元素，当它没有弹出时，我们会断开，并打印相应的 j <sup>th</sup> 值。
算法:

```
1\. Set i = 0, j = 1.
2\. Traverse the preorder array.
3\. If a[i] > a[j], push a[i] to the stack.
4\. Else
   While (stack is not empty)
     if (a[j] > top of stack)
       pop element from the stack;
       set found = true;
     else
       break;
5\. if (found == true)
     print a[i];
```

**这个算法是如何工作的？**
前序遍历按顺序遍历:访问、左、右。
并且我们知道 BST 中任意节点的左节点总是小于该节点。所以前序遍历将首先从根节点遍历到最左边的节点。因此，预订单将首先按降序排列。现在，在降序之后，可能有一个节点更大或者打破了降序。所以，可能会有这样的情况:

![](img/34f9302e036ad26e56f11cf840ab30b1.png)

在情况 1 中，20 是叶节点，而在情况 2 中，20 不是叶节点。
那么，我们的问题是如何识别是否要打印 20 作为叶节点？
这是使用堆栈解决的。
当在情况 1 和情况 2 上运行上述算法时，当 i = 2 和 j = 3 时，两种情况下堆栈的状态将相同:

![](img/be5ce52738aaa480a6de251d29f7b956.png)

因此，节点 65 将从堆栈中弹出 20 和 50。这是因为 65 是 20 之前的节点的右子节点。我们使用找到的变量存储这些信息。所以，20 是根节点。
而在情况 2 中，40 将不能从堆栈中弹出任何元素。因为 40 是 20 之后的节点的右节点。所以，20 不是叶节点。
注意:在算法中，我们将无法检查前序最右节点或最右元素的叶节点的情况。所以，只需打印最右边的节点，因为我们知道这将始终是一个叶节点在预序遍历。
以下是本办法的实施情况:

## C++

```
// Stack based C++ program to print leaf nodes
// from preorder traversal.
#include<bits/stdc++.h>
using namespace std;

// Print the leaf node from the given preorder of BST.
void leafNode(int preorder[], int n)
{
    stack<int> s;
    for (int i = 0, j = 1; j < n; i++, j++)
    {
        bool found = false;

        if (preorder[i] > preorder[j])
            s.push(preorder[i]);

        else
        {
            while (!s.empty())
            {
                if (preorder[j] > s.top())
                {
                    s.pop();
                    found = true;
                }
                else
                    break;
            }
        }

        if (found)
            cout << preorder[i] << " ";
    }

    // Since rightmost element is always leaf node.
    cout << preorder[n - 1];
}

// Driver code
int main()
{
    int preorder[] = { 890, 325, 290, 530, 965 };
    int n = sizeof(preorder)/sizeof(preorder[0]);

    leafNode(preorder, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Stack based Java program to print leaf nodes
// from preorder traversal.
import java.util.*;
class GfG {

// Print the leaf node from the given preorder of BST.
static void leafNode(int preorder[], int n)
{
    Stack<Integer> s = new Stack<Integer> ();
    for (int i = 0, j = 1; j < n; i++, j++)
    {
        boolean found = false;

        if (preorder[i] > preorder[j])
            s.push(preorder[i]);

        else
        {
            while (!s.isEmpty())
            {
                if (preorder[j] > s.peek())
                {
                    s.pop();
                    found = true;
                }
                else
                    break;
            }
        }

        if (found)
            System.out.print(preorder[i] + " ");
    }

    // Since rightmost element is always leaf node.
    System.out.println(preorder[n - 1]);
}

// Driver code
public static void main(String[] args)
{
    int preorder[] = { 890, 325, 290, 530, 965 };
    int n = preorder.length;

    leafNode(preorder, n);
}
}
```

## 蟒蛇 3

```
# Stack based Python program to print
# leaf nodes from preorder traversal.

# Print the leaf node from the given
# preorder of BST.
def leafNode(preorder, n):
    s = []
    i = 0
    for j in range(1, n):
        found = False
        if preorder[i] > preorder[j]:
            s.append(preorder[i])

        else:
            while len(s) != 0:
                if preorder[j] > s[-1]:
                    s.pop(-1)
                    found = True
                else:
                    break

        if found:
            print(preorder[i], end = " ")
        i += 1

    # Since rightmost element is
    # always leaf node.
    print(preorder[n - 1])

# Driver code
if __name__ == '__main__':
    preorder = [890, 325, 290, 530, 965]
    n = len(preorder)

    leafNode(preorder, n)

# This code is contributed by PranchalK
```

## C#

```
using System;
using System.Collections.Generic;

// Stack based C# program to print leaf nodes 
// from preorder traversal.
public class GfG
{

// Print the leaf node from the given preorder of BST. 
public static void leafNode(int[] preorder, int n)
{
    Stack<int> s = new Stack<int> ();
    for (int i = 0, j = 1; j < n; i++, j++)
    {
        bool found = false;

        if (preorder[i] > preorder[j])
        {
            s.Push(preorder[i]);
        }

        else
        {
            while (s.Count > 0)
            {
                if (preorder[j] > s.Peek())
                {
                    s.Pop();
                    found = true;
                }
                else
                {
                    break;
                }
            }
        }

        if (found)
        {
            Console.Write(preorder[i] + " ");
        }
    }

    // Since rightmost element is always leaf node. 
    Console.WriteLine(preorder[n - 1]);
}

// Driver code 
public static void Main(string[] args)
{
    int[] preorder = new int[] {890, 325, 290, 530, 965};
    int n = preorder.Length;

    leafNode(preorder, n);
}
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Stack based Javascript program to print leaf nodes
    // from preorder traversal.

    // Print the leaf node from the given preorder of BST.
    function leafNode(preorder, n)
    {
        let s = [];
        for (let i = 0, j = 1; j < n; i++, j++)
        {
            let found = false;

            if (preorder[i] > preorder[j])
                s.push(preorder[i]);

            else
            {
                while (s.length > 0)
                {
                    if (preorder[j] > s[s.length - 1])
                    {
                        s.pop();
                        found = true;
                    }
                    else
                        break;
                }
            }

            if (found)
                document.write(preorder[i] + " ");
        }

        // Since rightmost element is always leaf node.
        document.write(preorder[n - 1]);
    }

    let preorder = [ 890, 325, 290, 530, 965 ];
    let n = preorder.length;

    leafNode(preorder, n);

 // This code is contributed by mukesh07.
</script>
```

**输出:**

```
290 530 965
```

**时间复杂度:** O(n)
[**二叉查找树(使用递归)**](https://www.geeksforgeeks.org/leaf-nodes-preorder-binary-search-treeusing-recursion/)
叶节点本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。