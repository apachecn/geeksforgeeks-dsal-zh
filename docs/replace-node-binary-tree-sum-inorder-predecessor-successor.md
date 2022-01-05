# 将二叉树中的每一个节点替换为其前序和后继的总和

> 原文:[https://www . geesforgeks . org/replace-node-binary-tree-sum-in order-predent-后继/](https://www.geeksforgeeks.org/replace-node-binary-tree-sum-inorder-predecessor-successor/)

给定一个包含 **n 个**节点的二叉树。问题是用有序的前一个和有序的后一个的和来替换二叉树中的每个节点。

**示例:**

```
Input :          1
               /   \
              2     3
            /  \  /  \
           4   5  6   7

Output :        11
              /    \
             9      13
            / \    /  \
           2   3   4   3

For 1:
Inorder predecessor = 5
Inorder successor  = 6
Sum = 11

For 4:
Inorder predecessor = 0
(as inorder predecessor is not present)
Inorder successor  = 2
Sum = 2

For 7:
Inorder predecessor = 3
Inorder successor  = 0
(as inorder successor is not present)
Sum = 3
```

**方法:**创建一个数组 **arr** 。将 **0** 存储在索引 0 处。现在，将树的有序遍历存储在数组 **arr** 中。然后，将 **0** 存储在最后一个索引处。 **0 的**被存储为最左边叶的前序，而最右边叶的后序不存在。现在，执行有序遍历，在遍历节点时，用 **arr[i-1] + arr[i+1]** 替换节点的值，然后递增 **i** 。开始时初始化 **i** = 1。对于元素 **arr[i]** ，值 **arr[i-1]** 和 **arr[i+1]** 分别是其前序和后序。

## C++

```
// C++ implementation to replace each node
// in binary tree with the sum of its inorder
// predecessor and successor
#include <bits/stdc++.h>

using namespace std;

// node of a binary tree
struct Node {
    int data;
    struct Node* left, *right;
};

// function to get a new node of a binary tree
struct Node* getNode(int data)
{
    // allocate node
    struct Node* new_node =
       (struct Node*)malloc(sizeof(struct Node));

    // put in the data;
    new_node->data = data;
    new_node->left = new_node->right = NULL;

    return new_node;
}

// function to store the inorder traversal
// of the binary tree in 'arr'
void storeInorderTraversal(struct Node* root,
                                vector<int>& arr)
{
    // if root is NULL
    if (!root)
        return;

    // first recur on left child
    storeInorderTraversal(root->left, arr);

    // then store the root's data in 'arr'
    arr.push_back(root->data);

    // now recur on right child
    storeInorderTraversal(root->right, arr);
}

// function to replace each node with the sum of its
// inorder predecessor and successor
void replaceNodeWithSum(struct Node* root,
                        vector<int> arr, int* i)
{
    // if root is NULL
    if (!root)
        return;

    // first recur on left child
    replaceNodeWithSum(root->left, arr, i);

    // replace node's data with the sum of its
    // inorder predecessor and successor
    root->data = arr[*i - 1] + arr[*i + 1];

    // move 'i' to point to the next 'arr' element
    ++*i;

    // now recur on right child
    replaceNodeWithSum(root->right, arr, i);
}

// Utility function to replace each node in binary
// tree with the sum of its inorder predecessor
// and successor
void replaceNodeWithSumUtil(struct Node* root)
{
    // if tree is empty
    if (!root)
        return;

    vector<int> arr;

    // store the value of inorder predecessor
    // for the leftmost leaf
    arr.push_back(0);

    // store the inorder traversal of the tree in 'arr'
    storeInorderTraversal(root, arr);

    // store the value of inorder successor
    // for the rightmost leaf
    arr.push_back(0); 

    // replace each node with the required sum
    int i = 1;
    replaceNodeWithSum(root, arr, &i);
}

// function to print the preorder traversal
// of a binary tree
void preorderTraversal(struct Node* root)
{
    // if root is NULL
    if (!root)
        return;

    // first print the data of node
    cout << root->data << " ";

    // then recur on left subtree
    preorderTraversal(root->left);

    // now recur on right subtree
    preorderTraversal(root->right);
}

// Driver program to test above
int main()
{
    // binary tree formation
    struct Node* root = getNode(1); /*         1        */
    root->left = getNode(2);        /*       /   \      */
    root->right = getNode(3);       /*     2      3     */
    root->left->left = getNode(4);  /*    /  \  /   \   */
    root->left->right = getNode(5); /*   4   5  6   7   */
    root->right->left = getNode(6);
    root->right->right = getNode(7);

    cout << "Preorder Traversal before tree modification:n";
    preorderTraversal(root);

    replaceNodeWithSumUtil(root);

    cout << "\nPreorder Traversal after tree modification:n";
    preorderTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to replace each node
// in binary tree with the sum of its inorder
// predecessor and successor
import java.util.*;
class Solution
{

// node of a binary tree
static class Node {
    int data;
     Node left, right;
}

//INT class
static class INT
{
    int data;
}

// function to get a new node of a binary tree
static  Node getNode(int data)
{
    // allocate node
     Node new_node =new Node();

    // put in the data;
    new_node.data = data;
    new_node.left = new_node.right = null;

    return new_node;
}

// function to store the inorder traversal
// of the binary tree in 'arr'
static void storeInorderTraversal( Node root,
                                Vector<Integer> arr)
{
    // if root is null
    if (root==null)
        return;

    // first recur on left child
    storeInorderTraversal(root.left, arr);

    // then store the root's data in 'arr'
    arr.add(root.data);

    // now recur on right child
    storeInorderTraversal(root.right, arr);
}

// function to replace each node with the sum of its
// inorder predecessor and successor
static void replaceNodeWithSum( Node root,
                        Vector<Integer> arr, INT i)
{
    // if root is null
    if (root==null)
        return;

    // first recur on left child
    replaceNodeWithSum(root.left, arr, i);

    // replace node's data with the sum of its
    // inorder predecessor and successor
    root.data = arr.get(i.data - 1) + arr.get(i.data + 1);

    // move 'i' to point to the next 'arr' element
    i.data++;

    // now recur on right child
    replaceNodeWithSum(root.right, arr, i);
}

// Utility function to replace each node in binary
// tree with the sum of its inorder predecessor
// and successor
static void replaceNodeWithSumUtil( Node root)
{
    // if tree is empty
    if (root==null)
        return;

    Vector<Integer> arr= new Vector<Integer>();

    // store the value of inorder predecessor
    // for the leftmost leaf
    arr.add(0);

    // store the inorder traversal of the tree in 'arr'
    storeInorderTraversal(root, arr);

    // store the value of inorder successor
    // for the rightmost leaf
    arr.add(0); 

    // replace each node with the required sum
    INT i = new INT();

    i.data=1;

    replaceNodeWithSum(root, arr, i);
}

// function to print the preorder traversal
// of a binary tree
static void preorderTraversal( Node root)
{
    // if root is null
    if (root==null)
        return;

    // first print the data of node
    System.out.print( root.data + " ");

    // then recur on left subtree
    preorderTraversal(root.left);

    // now recur on right subtree
    preorderTraversal(root.right);
}

// Driver program to test above
public static void main(String args[])
{
    // binary tree formation
     Node root = getNode(1);       //         1       
    root.left = getNode(2);        //       /   \     
    root.right = getNode(3);       //     2      3    
    root.left.left = getNode(4);  //    /  \  /   \  
    root.left.right = getNode(5); //   4   5  6   7  
    root.right.left = getNode(6);
    root.right.right = getNode(7);

    System.out.println( "Preorder Traversal before tree modification:");
    preorderTraversal(root);

    replaceNodeWithSumUtil(root);

    System.out.println("\nPreorder Traversal after tree modification:");
    preorderTraversal(root);

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation to replace each
# node in binary tree with the sum of its
# inorder predecessor and successor

# class to get a new node of a
# binary tree
class getNode:
    def __init__(self, data):

        # put in the data
        self.data = data
        self.left = self.right = None

# function to store the inorder traversal
# of the binary tree in 'arr'
def storeInorderTraversal(root, arr):

    # if root is None
    if (not root):
        return

    # first recur on left child
    storeInorderTraversal(root.left, arr)

    # then store the root's data in 'arr'
    arr.append(root.data)

    # now recur on right child
    storeInorderTraversal(root.right, arr)

# function to replace each node with the
# sum of its inorder predecessor and successor
def replaceNodeWithSum(root, arr, i):

    # if root is None
    if (not root):
        return

    # first recur on left child
    replaceNodeWithSum(root.left, arr, i)

    # replace node's data with the sum of its
    # inorder predecessor and successor
    root.data = arr[i[0] - 1] + arr[i[0] + 1]

    # move 'i' to poto the next 'arr' element
    i[0] += 1

    # now recur on right child
    replaceNodeWithSum(root.right, arr, i)

# Utility function to replace each node in
# binary tree with the sum of its inorder 
# predecessor and successor
def replaceNodeWithSumUtil(root):

    # if tree is empty
    if (not root):
        return

    arr = []

    # store the value of inorder predecessor
    # for the leftmost leaf
    arr.append(0)

    # store the inorder traversal of the
    # tree in 'arr'
    storeInorderTraversal(root, arr)

    # store the value of inorder successor
    # for the rightmost leaf
    arr.append(0)

    # replace each node with the required sum
    i = [1]
    replaceNodeWithSum(root, arr, i)

# function to print the preorder traversal
# of a binary tree
def preorderTraversal(root):

    # if root is None
    if (not root):
        return

    # first print the data of node
    print(root.data, end = " ")

    # then recur on left subtree
    preorderTraversal(root.left)

    # now recur on right subtree
    preorderTraversal(root.right)

# Driver Code
if __name__ == '__main__':

    # binary tree formation
    root = getNode(1) #         1    
    root.left = getNode(2)     #     / \    
    root.right = getNode(3)     #     2     3    
    root.left.left = getNode(4) # / \ / \
    root.left.right = getNode(5) # 4 5 6 7
    root.right.left = getNode(6)
    root.right.right = getNode(7)

    print("Preorder Traversal before",
                 "tree modification:")
    preorderTraversal(root)

    replaceNodeWithSumUtil(root)
    print()
    print("Preorder Traversal after",
                "tree modification:")
    preorderTraversal(root)

# This code is contributed by PranchalK
```

## C#

```
// C# implementation to replace each
// node in binary tree with the sum
// of its inorder predecessor and successor
using System;
using System.Collections.Generic;

class GFG
{

// node of a binary tree
public class Node
{
    public int data;
    public Node left, right;
}

// INT class
public class INT
{
    public int data;
}

// function to get a new node
// of a binary tree
public static Node getNode(int data)
{
    // allocate node
    Node new_node = new Node();

    // put in the data;
    new_node.data = data;
    new_node.left = new_node.right = null;

    return new_node;
}

// function to store the inorder traversal
// of the binary tree in 'arr'
public static void storeInorderTraversal(Node root,
                                         List<int> arr)
{
    // if root is null
    if (root == null)
    {
        return;
    }

    // first recur on left child
    storeInorderTraversal(root.left, arr);

    // then store the root's data in 'arr'
    arr.Add(root.data);

    // now recur on right child
    storeInorderTraversal(root.right, arr);
}

// function to replace each node with
// the sum of its inorder predecessor
// and successor
public static void replaceNodeWithSum(Node root,
                                      List<int> arr, INT i)
{
    // if root is null
    if (root == null)
    {
        return;
    }

    // first recur on left child
    replaceNodeWithSum(root.left, arr, i);

    // replace node's data with the
    // sum of its inorder predecessor
    // and successor
    root.data = arr[i.data - 1] + arr[i.data + 1];

    // move 'i' to point to the
    // next 'arr' element
    i.data++;

    // now recur on right child
    replaceNodeWithSum(root.right, arr, i);
}

// Utility function to replace each
// node in binary tree with the sum
// of its inorder predecessor and successor
public static void replaceNodeWithSumUtil(Node root)
{
    // if tree is empty
    if (root == null)
    {
        return;
    }

    List<int> arr = new List<int>();

    // store the value of inorder
    // predecessor for the leftmost leaf
    arr.Add(0);

    // store the inorder traversal
    // of the tree in 'arr'
    storeInorderTraversal(root, arr);

    // store the value of inorder successor
    // for the rightmost leaf
    arr.Add(0);

    // replace each node with
    // the required sum
    INT i = new INT();

    i.data = 1;

    replaceNodeWithSum(root, arr, i);
}

// function to print the preorder
// traversal of a binary tree
public static void preorderTraversal(Node root)
{
    // if root is null
    if (root == null)
    {
        return;
    }

    // first print the data of node
    Console.Write(root.data + " ");

    // then recur on left subtree
    preorderTraversal(root.left);

    // now recur on right subtree
    preorderTraversal(root.right);
}

// Driver Code
public static void Main(string[] args)
{
    // binary tree formation
    Node root = getNode(1); //         1
    root.left = getNode(2); //     / \
    root.right = getNode(3); //     2     3
    root.left.left = getNode(4); // / \ / \
    root.left.right = getNode(5); // 4 5 6 7
    root.right.left = getNode(6);
    root.right.right = getNode(7);

    Console.WriteLine("Preorder Traversal " +
                "before tree modification:");
    preorderTraversal(root);

    replaceNodeWithSumUtil(root);

    Console.WriteLine("\nPreorder Traversal after " +
                               "tree modification:");
    preorderTraversal(root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript implementation to replace each node
// in binary tree with the sum of its inorder
// predecessor and successor
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Function to get a new node of a
// binary tree
function getNode(data)
{

    // Allocate node
    let new_node = new Node(data);
    return new_node;
}

// Function to store the inorder traversal
// of the binary tree in 'arr'
function storeInorderTraversal(root, arr)
{

    // If root is null
    if (root == null)
        return;

    // First recur on left child
    storeInorderTraversal(root.left, arr);

    // then store the root's data in 'arr'
    arr.push(root.data);

    // Now recur on right child
    storeInorderTraversal(root.right, arr);
}

// Function to replace each node with the
// sum of its inorder predecessor and successor
function replaceNodeWithSum(root, arr)
{

    // If root is null
    if (root == null)
        return;

    // First recur on left child
    replaceNodeWithSum(root.left, arr);

    // Replace node's data with the sum of its
    // inorder predecessor and successor
    root.data = arr[data - 1] + arr[data + 1];

    // Move 'i' to point to the next 'arr' element
    data++;

    // Now recur on right child
    replaceNodeWithSum(root.right, arr);
}

// Utility function to replace each node in binary
// tree with the sum of its inorder predecessor
// and successor
function replaceNodeWithSumUtil(root)
{

    // If tree is empty
    if (root == null)
        return;

    let arr = [];

    // Store the value of inorder predecessor
    // for the leftmost leaf
    arr.push(0);

    // Store the inorder traversal of
    // the tree in 'arr'
    storeInorderTraversal(root, arr);

    // Store the value of inorder successor
    // for the rightmost leaf
    arr.push(0); 

    // Replace each node with the required sum
    data = 1;

    replaceNodeWithSum(root, arr);
}

// Function to print the preorder traversal
// of a binary tree
function preorderTraversal(root)
{

    // If root is null
    if (root == null)
        return;

    // First print the data of node
    document.write(root.data + " ");

    // Then recur on left subtree
    preorderTraversal(root.left);

    // Now recur on right subtree
    preorderTraversal(root.right);
}

// Driver code

// Binary tree formation
let root = getNode(1);       //           1       
root.left = getNode(2);        //       /   \     
root.right = getNode(3);       //     2      3    
root.left.left = getNode(4);  //    /  \  /   \  
root.left.right = getNode(5); //   4   5  6   7  
root.right.left = getNode(6);
root.right.right = getNode(7);

document.write("Preorder Traversal before " +
               "tree modification:" + "</br>");
preorderTraversal(root);

replaceNodeWithSumUtil(root);

document.write("</br>" + "Preorder Traversal after " +
               "tree modification:" + "</br>");
preorderTraversal(root);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
Preorder Traversal before tree modification:
1 2 4 5 3 6 7
Preorder Traversal after tree modification:
11 9 2 3 13 4 3
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。