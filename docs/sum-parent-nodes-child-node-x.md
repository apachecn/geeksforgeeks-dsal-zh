# 具有子节点 x 的所有父节点的总和

> 原文:[https://www . geesforgeks . org/sum-父节点-子节点-x/](https://www.geeksforgeeks.org/sum-parent-nodes-child-node-x/)

给定一个包含 **n 个**节点的二叉树。问题是找到所有父节点的和，这些父节点有一个值为 **x** 的子节点。
**例:**

```
Input : Binary tree with x = 2:
        4        
       / \       
      2   5      
     / \ / \     
    7  2 2  3    
Output : 11

        4        
       / \       
      2   5      
     / \ / \     
    7  2 2  3    

The highlighted nodes (4, 2, 5) above
are the nodes having 2 as a child node.
```

**算法:**

```
sumOfParentOfX(root,sum,x)
    if root == NULL
        return

    if (root->left && root->left->data == x) ||
       (root->right && root->right->data == x)
        sum += root->data

    sumOfParentOfX(root->left, sum, x)
    sumOfParentOfX(root->right, sum, x)

sumOfParentOfXUtil(root,x)
    Declare sum = 0
    sumOfParentOfX(root, sum, x)
    return sum
```

## C++

```
// C++ implementation to find the sum of all
// the parent nodes having child node x
#include <bits/stdc++.h>

using namespace std;

// Node of a binary tree
struct Node
{
    int data;
    Node *left, *right;
};

// function to get a new node
Node* getNode(int data)
{
    // allocate memory for the node
    Node *newNode =
        (Node*)malloc(sizeof(Node));

    // put in the data   
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;   
}

// function to find the sum of all the
// parent nodes having child node x
void sumOfParentOfX(Node* root, int& sum, int x)
{
    // if root == NULL
    if (!root)
        return;

    // if left or right child of root is 'x', then
    // add the root's data to 'sum'
    if ((root->left && root->left->data == x) ||
        (root->right && root->right->data == x))
        sum += root->data;

    // recursively find the required parent nodes
    // in the left and right subtree   
    sumOfParentOfX(root->left, sum, x);
    sumOfParentOfX(root->right, sum, x);

}

// utility function to find the sum of all
// the parent nodes having child node x
int sumOfParentOfXUtil(Node* root, int x)
{
    int sum = 0;
    sumOfParentOfX(root, sum, x);

    // required sum of parent nodes
    return sum;
}

// Driver program to test above
int main()
{
    // binary tree formation
    Node *root = getNode(4);           /*        4        */
    root->left = getNode(2);           /*       / \       */
    root->right = getNode(5);          /*      2   5      */
    root->left->left = getNode(7);     /*     / \ / \     */
    root->left->right = getNode(2);    /*    7  2 2  3    */
    root->right->left = getNode(2);
    root->right->right = getNode(3);

    int x = 2;

    cout << "Sum = "
         << sumOfParentOfXUtil(root, x);

    return 0;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the sum of all the parent
// nodes having child node x
class GFG
{
// sum
static int sum = 0;

// Node of a binary tree
static class Node
{
    int data;
    Node left, right;
};

// function to get a new node
static Node getNode(int data)
{
    // allocate memory for the node
    Node newNode = new Node();

    // put in the data    
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;    
}

// function to find the sum of all the
// parent nodes having child node x
static void sumOfParentOfX(Node root, int x)
{
    // if root == NULL
    if (root == null)
        return;

    // if left or right child
    // of root is 'x', then
    // add the root's data to 'sum'
    if ((root.left != null && root.left.data == x) ||
        (root.right != null && root.right.data == x))
        sum += root.data;

    // recursively find the required
    // parent nodes in the left and
    // right subtree    
    sumOfParentOfX(root.left, x);
    sumOfParentOfX(root.right, x);

}

// utility function to find the
// sum of all the parent nodes
// having child node x
static int sumOfParentOfXUtil(Node root,   
                              int x)
{
    sum = 0;
    sumOfParentOfX(root, x);

    // required sum of parent nodes
    return sum;
}

// Driver Code
public static void main(String args[])
{
    // binary tree formation
    Node root = getNode(4);         //     4    
    root.left = getNode(2);         //     / \    
    root.right = getNode(5);         //     2 5    
    root.left.left = getNode(7);     //     / \ / \    
    root.left.right = getNode(2); // 7 2 2 3
    root.right.left = getNode(2);
    root.right.right = getNode(3);

    int x = 2;

    System.out.println( "Sum = " +
           sumOfParentOfXUtil(root, x));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation to find the Sum of
# all the parent nodes having child node x

# function to get a new node
class getNode:
    def __init__(self, data):

        # put in the data    
        self.data = data
        self.left = self.right = None

# function to find the Sum of all the
# parent nodes having child node x
def SumOfParentOfX(root, Sum, x):

    # if root == None
    if (not root):
        return

    # if left or right child of root is 'x',
    # then add the root's data to 'Sum'
    if ((root.left and root.left.data == x) or
        (root.right and root.right.data == x)):
        Sum[0] += root.data

    # recursively find the required parent
    # nodes in the left and right subtree    
    SumOfParentOfX(root.left, Sum, x)
    SumOfParentOfX(root.right, Sum, x)

# utility function to find the Sum of all
# the parent nodes having child node x
def SumOfParentOfXUtil(root, x):
    Sum = [0]
    SumOfParentOfX(root, Sum, x)

    # required Sum of parent nodes
    return Sum[0]

# Driver Code
if __name__ == '__main__':

    # binary tree formation
    root = getNode(4)         #     4    
    root.left = getNode(2)         #     / \    
    root.right = getNode(5)         #     2 5    
    root.left.left = getNode(7)     #     / \ / \    
    root.left.right = getNode(2) # 7 2 2 3
    root.right.left = getNode(2)
    root.right.right = getNode(3)

    x = 2

    print("Sum = ", SumOfParentOfXUtil(root, x))

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# implementation to find
// the sum of all the parent
// nodes having child node x
public class GFG
{
// sum
public static int sum = 0;

// Node of a binary tree
public class Node
{
    public int data;
    public Node left, right;
}

// function to get a new node
public static Node getNode(int data)
{
    // allocate memory for the node
    Node newNode = new Node();

    // put in the data    
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to find the sum of all the
// parent nodes having child node x
public static void sumOfParentOfX(Node root, int x)
{
    // if root == NULL
    if (root == null)
    {
        return;
    }

    // if left or right child
    // of root is 'x', then
    // add the root's data to 'sum'
    if ((root.left != null && root.left.data == x) ||
       (root.right != null && root.right.data == x))
    {
        sum += root.data;
    }

    // recursively find the required
    // parent nodes in the left and
    // right subtree    
    sumOfParentOfX(root.left, x);
    sumOfParentOfX(root.right, x);

}

// utility function to find the
// sum of all the parent nodes
// having child node x
public static int sumOfParentOfXUtil(Node root, int x)
{
    sum = 0;
    sumOfParentOfX(root, x);

    // required sum of parent nodes
    return sum;
}

// Driver Code
public static void Main(string[] args)
{
    // binary tree formation
    Node root = getNode(4); //     4
    root.left = getNode(2); //     / \
    root.right = getNode(5); //     2 5
    root.left.left = getNode(7); //     / \ / \
    root.left.right = getNode(2); // 7 2 2 3
    root.right.left = getNode(2);
    root.right.right = getNode(3);

    int x = 2;

    Console.WriteLine("Sum = " + sumOfParentOfXUtil(root, x));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript implementation to find
    // the sum of all the parent
    // nodes having child node x

    // sum
    let sum = 0;

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to get a new node
    function getNode(data)
    {
        // allocate memory for the node
        let newNode = new Node(data);
        return newNode;    
    }

    // function to find the sum of all the
    // parent nodes having child node x
    function sumOfParentOfX(root, x)
    {
        // if root == NULL
        if (root == null)
            return;

        // if left or right child
        // of root is 'x', then
        // add the root's data to 'sum'
        if ((root.left != null && root.left.data == x) ||
            (root.right != null && root.right.data == x))
            sum += root.data;

        // recursively find the required
        // parent nodes in the left and
        // right subtree    
        sumOfParentOfX(root.left, x);
        sumOfParentOfX(root.right, x);

    }

    // utility function to find the
    // sum of all the parent nodes
    // having child node x
    function sumOfParentOfXUtil(root, x)
    {
        sum = 0;
        sumOfParentOfX(root, x);

        // required sum of parent nodes
        return sum;
    }

    // binary tree formation
    let root = getNode(4);         //         4    
    root.left = getNode(2);         //       / \    
    root.right = getNode(5);         //      2 5    
    root.left.left = getNode(7);     //    / \ / \    
    root.left.right = getNode(2); //       7 2 2 3
    root.right.left = getNode(2);
    root.right.right = getNode(3);

    let x = 2;

    document.write( "Sum = " +
           sumOfParentOfXUtil(root, x));

</script>
```

**输出:**

```
Sum = 11
```

**时间复杂度:** O(n)。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。