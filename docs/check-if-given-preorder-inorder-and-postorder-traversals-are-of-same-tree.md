# 检查给定的前序、中序和后序遍历是否在同一棵树上

> 原文:[https://www . geesforgeks . org/check-if-given-preorder-in-order-and-post-traversals-同树/](https://www.geeksforgeeks.org/check-if-given-preorder-inorder-and-postorder-traversals-are-of-same-tree/)

给定某棵树的[前序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)、[中序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)和[后序](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历。编写一个程序来检查它们是否都属于同一棵树。
**示例:**

```
Input : Inorder -> 4 2 5 1 3
        Preorder -> 1 2 4 5 3
        Postorder -> 4 5 2 3 1
Output : Yes
Exaplanation : All of the above three traversals are of 
the same tree              1
                         /   \
                        2     3
                      /   \
                     4     5

Input : Inorder -> 4 2 5 1 3
        Preorder -> 1 5 4 2 3
        Postorder -> 4 1 2 3 5
Output : No 
```

解决这个问题最基本的方法是首先使用三个给定遍历中的两个来构造一棵树，然后在这个构造的树上进行第三次遍历，并将其与给定的遍历进行比较。如果两个遍历相同，则打印是，否则打印否。在这里，我们使用有序遍历和预有序遍历来构建树。对于树的构造，我们也可以使用顺序遍历和顺序遍历来代替顺序遍历。你可以参考[这篇](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)的帖子，了解如何根据给定的有序和预有序遍历来构建一棵树。在构造树之后，我们将获得该树的后序遍历，并将其与给定的后序遍历进行比较。
以下是上述办法的实施情况:

## C++

```
/* C++ program to check if all three given
   traversals are of the same tree */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

/* Function to find index of value in arr[start...end]
   The function assumes that value is present in in[] */
int search(int arr[], int strt, int end, int value)
{
    for (int i = strt; i <= end; i++)
    {
        if(arr[i] == value)
            return i;
    }
}

/* Recursive function to construct binary tree
   of size len from Inorder traversal in[] and
   Preorder traversal pre[].  Initial values
   of inStrt and inEnd should be 0 and len -1. 
   The function doesn't do any error checking for
   cases where inorder and preorder do not form a
   tree */
Node* buildTree(int in[], int pre[], int inStrt,
                                      int inEnd)
{
    static int preIndex = 0;

    if(inStrt > inEnd)
        return NULL;

    /* Pick current node from Preorder traversal
       using preIndex and increment preIndex */
    Node *tNode = newNode(pre[preIndex++]);

    /* If this node has no children then return */
    if (inStrt == inEnd)
        return tNode;

    /* Else find the index of this node in
       Inorder traversal */
    int inIndex = search(in, inStrt, inEnd, tNode->data);

    /* Using index in Inorder traversal,
       construct left and right subtress */
    tNode->left = buildTree(in, pre, inStrt, inIndex-1);
    tNode->right = buildTree(in, pre, inIndex+1, inEnd);

    return tNode;
}

/* function to compare Postorder traversal
   on constructed tree and given Postorder */
int checkPostorder(Node* node, int postOrder[], int index)
{
    if (node == NULL)
        return index;

    /* first recur on left child */
    index = checkPostorder(node->left,postOrder,index);

    /* now recur on right child */
    index = checkPostorder(node->right,postOrder,index);   

    /* Compare if data at current index in
       both Postorder traversals are same */
    if (node->data == postOrder[index])
        index++;
    else
        return -1;

    return index;
}

// Driver program to test above functions
int main()
{
    int inOrder[] = {4, 2, 5, 1, 3};
    int preOrder[] = {1, 2, 4, 5, 3};
    int postOrder[] = {4, 5, 2, 3, 1};

    int len = sizeof(inOrder)/sizeof(inOrder[0]);

    // build tree from given
    // Inorder and Preorder traversals
    Node *root = buildTree(inOrder, preOrder, 0, len - 1);

    // compare postorder traversal on constructed
    // tree with given Postorder traversal
    int index = checkPostorder(root,postOrder,0);

    // If both postorder traversals are same
    if (index == len)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to check if all three given
traversals are of the same tree */
import java.util.*;
class GfG {
    static int preIndex = 0;

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

/* Function to find index of value in arr[start...end]
The function assumes that value is present in in[] */
static int search(int arr[], int strt, int end, int value)
{
    for (int i = strt; i <= end; i++)
    {
        if(arr[i] == value)
            return i;
    }
    return -1;
}

/* Recursive function to construct binary tree
of size len from Inorder traversal in[] and
Preorder traversal pre[]. Initial values
of inStrt and inEnd should be 0 and len -1.
The function doesn't do any error checking for
cases where inorder and preorder do not form a
tree */
static Node buildTree(int in[], int pre[], int inStrt, int inEnd)
{

    if(inStrt > inEnd)
        return null;

    /* Pick current node from Preorder traversal
    using preIndex and increment preIndex */
    Node tNode = newNode(pre[preIndex++]);

    /* If this node has no children then return */
    if (inStrt == inEnd)
        return tNode;

    /* Else find the index of this node in
    Inorder traversal */
    int inIndex = search(in, inStrt, inEnd, tNode.data);

    /* Using index in Inorder traversal,
    construct left and right subtress */
    tNode.left = buildTree(in, pre, inStrt, inIndex-1);
    tNode.right = buildTree(in, pre, inIndex+1, inEnd);

    return tNode;
}

/* function to compare Postorder traversal
on constructed tree and given Postorder */
static int checkPostorder(Node node, int postOrder[], int index)
{
    if (node == null)
        return index;

    /* first recur on left child */
    index = checkPostorder(node.left,postOrder,index);

    /* now recur on right child */
    index = checkPostorder(node.right,postOrder,index);    

    /* Compare if data at current index in
    both Postorder traversals are same */
    if (node.data == postOrder[index])
        index++;
    else
        return -1;

    return index;
}

// Driver program to test above functions
public static void main(String[] args)
{
    int inOrder[] = {4, 2, 5, 1, 3};
    int preOrder[] = {1, 2, 4, 5, 3};
    int postOrder[] = {4, 5, 2, 3, 1};

    int len = inOrder.length;

    // build tree from given
    // Inorder and Preorder traversals
    Node root = buildTree(inOrder, preOrder, 0, len - 1);

    // compare postorder traversal on constructed
    // tree with given Postorder traversal
    int index = checkPostorder(root,postOrder,0);

    // If both postorder traversals are same
    if (index == len)
        System.out.println("Yes");
    else
        System.out.println("No");

}
}
```

## 蟒蛇 3

```
# Python3 program to check if
# all three given traversals
# are of the same tree
class node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

preIndex = 0

# Function to find index of value
# in arr[start...end]. The function
# assumes that value is present in in
def search(arr, strt, end, value):

    for i in range(strt, end + 1):
        if(arr[i] == value):
            return i

# Recursive function to construct
# binary tree of size lenn from
# Inorder traversal in and Preorder
# traversal pre[].  Initial values
# of inStrt and inEnd should be 0
# and lenn -1\. The function doesn't
# do any error checking for cases
# where inorder and preorder do not
# form a tree
def buildTree(inn, pre, inStrt, inEnd):

    global preIndex

    if(inStrt > inEnd):
        return None

    # Pick current node from Preorder
    # traversal using preIndex and
    # increment preIndex
    tNode = node(pre[preIndex])
    preIndex += 1

    # If this node has no children
    # then return
    if (inStrt == inEnd):
        return tNode

    # Else find the index of this
    # node in Inorder traversal
    inIndex = search(inn, inStrt,
                     inEnd, tNode.data)

    # Using index in Inorder traversal,
    # construct left and right subtress
    tNode.left = buildTree(inn, pre, inStrt,
                           inIndex - 1)
    tNode.right = buildTree(inn, pre,
                            inIndex + 1, inEnd)

    return tNode

# function to compare Postorder traversal
# on constructed tree and given Postorder
def checkPostorder(node, postOrder, index):
    if (node == None):
        return index

    # first recur on left child
    index = checkPostorder(node.left,
                           postOrder,
                           index)

    # now recur on right child
    index = checkPostorder(node.right,
                           postOrder,
                           index)

    # Compare if data at current index in
    # both Postorder traversals are same
    if (node.data == postOrder[index]):
        index += 1
    else:
        return - 1

    return index

# Driver code
if __name__ == '__main__':

    inOrder = [4, 2, 5, 1, 3]
    preOrder = [1, 2, 4, 5, 3]
    postOrder = [4, 5, 2, 3, 1]
    lenn = len(inOrder)

    # build tree from given
    # Inorder and Preorder traversals
    root = buildTree(inOrder, preOrder,
                     0, lenn - 1)

    # compare postorder traversal on
    # constructed tree with given
    # Postorder traversal
    index = checkPostorder(root, postOrder, 0)

    # If both postorder traversals are same
    if (index == lenn):
        print("Yes")
    else:
        print("No")

# This code is contributed by Mohit Kumar 29
```

## C#

```
/* C# program to check if all three given
traversals are of the same tree */
using System;

public class GfG
{
    static int preIndex = 0;

    // A Binary Tree Node
    class Node
    {
        public int data;
        public Node left, right;
    }

    // Utility function to create a new tree node
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    /* Function to find index of
    value in arr[start...end]
    The function assumes that
    value is present in in[] */
    static int search(int []arr, int strt,
                        int end, int value)
    {
        for (int i = strt; i <= end; i++)
        {
            if(arr[i] == value)
                return i;
        }
        return -1;
    }

    /* Recursive function to construct
    binary tree of size len from Inorder
    traversal in[] and Preorder traversal
    pre[]. Initial values of inStrt and
    inEnd should be 0 and len -1\. The
    function doesn't do any error checking for
    cases where inorder and preorder do not form a
    tree */
    static Node buildTree(int []In, int []pre,
                            int inStrt, int inEnd)
    {

        if(inStrt > inEnd)
            return null;

        /* Pick current node from Preorder traversal
        using preIndex and increment preIndex */
        Node tNode = newNode(pre[preIndex++]);

        /* If this node has no children then return */
        if (inStrt == inEnd)
            return tNode;

        /* Else find the index of this node in
        Inorder traversal */
        int inIndex = search(In, inStrt, inEnd, tNode.data);

        /* Using index in Inorder traversal,
        construct left and right subtress */
        tNode.left = buildTree(In, pre, inStrt, inIndex - 1);
        tNode.right = buildTree(In, pre, inIndex + 1, inEnd);

        return tNode;
    }

    /* function to compare Postorder traversal
    on constructed tree and given Postorder */
    static int checkPostorder(Node node, int []postOrder, int index)
    {
        if (node == null)
            return index;

        /* first recur on left child */
        index = checkPostorder(node.left,postOrder,index);

        /* now recur on right child */
        index = checkPostorder(node.right,postOrder,index);    

        /* Compare if data at current index in
        both Postorder traversals are same */
        if (node.data == postOrder[index])
            index++;
        else
            return -1;

        return index;
    }

    // Driver code
    public static void Main()
    {
        int []inOrder = {4, 2, 5, 1, 3};
        int []preOrder = {1, 2, 4, 5, 3};
        int []postOrder = {4, 5, 2, 3, 1};

        int len = inOrder.Length;

        // build tree from given
        // Inorder and Preorder traversals
        Node root = buildTree(inOrder, preOrder, 0, len - 1);

        // compare postorder traversal on constructed
        // tree with given Postorder traversal
        int index = checkPostorder(root, postOrder, 0);

        // If both postorder traversals are same
        if (index == len)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

    }
}

/* This code is contributed PrinciRaj1992 */
```

## java 描述语言

```
<script>
/* Javascript program to check if all three given
traversals are of the same tree */

    let preIndex = 0;
    // A Binary Tree Node
    class Node
    {
        // Utility function to create a new tree node
        constructor(data)
        {
            this.data=data;
            this.left=this.right=null;
        }
    }

/* Function to find index of value in arr[start...end]
The function assumes that value is present in in[] */   
function search(arr,strt,end,value)
{
    for (let i = strt; i <= end; i++)
    {
        if(arr[i] == value)
            return i;
    }
    return -1;
}

/* Recursive function to construct binary tree
of size len from Inorder traversal in[] and
Preorder traversal pre[]. Initial values
of inStrt and inEnd should be 0 and len -1.
The function doesn't do any error checking for
cases where inorder and preorder do not form a
tree */
function buildTree(In,pre,inStrt,inEnd)
{
    if(inStrt > inEnd)
        return null;

    /* Pick current node from Preorder traversal
    using preIndex and increment preIndex */
    let tNode = new Node(pre[preIndex++]);

    /* If this node has no children then return */
    if (inStrt == inEnd)
        return tNode;

    /* Else find the index of this node in
    Inorder traversal */
    let inIndex = search(In, inStrt, inEnd, tNode.data);

    /* Using index in Inorder traversal,
    construct left and right subtress */
    tNode.left = buildTree(In, pre, inStrt, inIndex-1);
    tNode.right = buildTree(In, pre, inIndex+1, inEnd);

    return tNode;
}

/* function to compare Postorder traversal
on constructed tree and given Postorder */
function checkPostorder(node,postOrder,index)
{
    if (node == null)
        return index;

    /* first recur on left child */
    index = checkPostorder(node.left,postOrder,index);

    /* now recur on right child */
    index = checkPostorder(node.right,postOrder,index);   

    /* Compare if data at current index in
    both Postorder traversals are same */
    if (node.data == postOrder[index])
        index++;
    else
        return -1;

    return index;
}

// Driver program to test above functions
let inOrder=[4, 2, 5, 1, 3];
let preOrder=[1, 2, 4, 5, 3];
let postOrder=[4, 5, 2, 3, 1];

let len = inOrder.length;

    // build tree from given
    // Inorder and Preorder traversals
    let root = buildTree(inOrder, preOrder, 0, len - 1);

    // compare postorder traversal on constructed
    // tree with given Postorder traversal
    let index = checkPostorder(root,postOrder,0);

    // If both postorder traversals are same
    if (index == len)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by patel2127
</script>
```

**Output**

```
Yes
```

**时间复杂度** : O( n * n)，其中 n 为树中节点数。
本文由 [**严酷的阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。

**使用哈希映射存储有序元素索引的高效算法:**

当从有序和前序遍历构建树时，我们需要检查有序和前序遍历对于某棵树本身是否有效，如果是，则继续构建树，但是如果不能从给定的有序和前序遍历构建有效的二叉树，那么我们必须停止构建树并返回 false。此外，我们还可以使用 hashmap 存储有序元素数组的索引，在 O(n)时间内通过有序和前序遍历来构建树。

## C++

```
#include <bits/stdc++.h>
using namespace std;
struct Node {
    int data;
    Node *left, *right;

    Node(int val)
    {
        data = val;
        left = right = NULL;
    }
};
Node* buildTreeFromInorderPreorder(
    int inStart, int inEnd, int& preIndex, int preorder[],
    unordered_map<int, int>& inorderIndexMap,
    bool& notPossible)
{
    if (inStart > inEnd)
        return NULL;

    // build the current Node
    int rootData = preorder[preIndex];
    Node* root = new Node(rootData);
    preIndex++;

    // find the node in inorderIndexMap
    if (inorderIndexMap.find(rootData)
        == inorderIndexMap.end()) {
        notPossible = true;
        return root;
    }

    int inorderIndex = inorderIndexMap[rootData];
    if (!(inStart <= inorderIndex
          && inorderIndex <= inEnd)) {
        notPossible = true;
        return root;
    }

    int leftInorderStart = inStart,
        leftInorderEnd = inorderIndex - 1,
        rightInorderStart = inorderIndex + 1,
        rightInorderEnd = inEnd;

    root->left = buildTreeFromInorderPreorder(
        leftInorderStart, leftInorderEnd, preIndex,
        preorder, inorderIndexMap, notPossible);

    if (notPossible)
        return root;

    root->right = buildTreeFromInorderPreorder(
        rightInorderStart, rightInorderEnd, preIndex,
        preorder, inorderIndexMap, notPossible);

    return root;
}

bool checkPostorderCorrect(Node* root, int& postIndex,
                           int postorder[])
{
    if (!root)
        return true;

    if (!checkPostorderCorrect(root->left, postIndex,
                               postorder))
        return false;
    if (!checkPostorderCorrect(root->right, postIndex,
                               postorder))
        return false;

    return (root->data == postorder[postIndex++]);
}

void printPostorder(Node* root)
{
    if (!root)
        return;

    printPostorder(root->left);
    printPostorder(root->right);

    cout << root->data << ", ";
}

void printInorder(Node* root)
{
    if (!root)
        return;

    printInorder(root->left);
    cout << root->data << ", ";
    printInorder(root->right);
}

bool checktree(int preorder[], int inorder[],
               int postorder[], int N)
{
    // Your code goes here
    if (N == 0)
        return true;

    unordered_map<int, int> inorderIndexMap;
    for (int i = 0; i < N; i++)
        inorderIndexMap[inorder[i]] = i;

    int preIndex = 0;

    // return checkInorderPreorder(0, N - 1, preIndex,
    // preorder, inorderIndexMap) &&
    // checkInorderPostorder(0, N - 1, postIndex, postorder,
    // inorderIndexMap);

    bool notPossible = false;

    Node* root = buildTreeFromInorderPreorder(
        0, N - 1, preIndex, preorder, inorderIndexMap,
        notPossible);

    if (notPossible)
        return false;

    int postIndex = 0;

    return checkPostorderCorrect(root, postIndex,
                                 postorder);
}

// Driver program to test above functions
int main()
{
    int inOrder[] = { 4, 2, 5, 1, 3 };
    int preOrder[] = { 1, 2, 4, 5, 3 };
    int postOrder[] = { 4, 5, 2, 3, 1 };

    int len = sizeof(inOrder) / sizeof(inOrder[0]);

    // If both postorder traversals are same
    if (checktree(preOrder, inOrder, postOrder, len))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)，其中 N 为树中节点数。