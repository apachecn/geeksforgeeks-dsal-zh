# 压平一个二叉查找树，将树转换成波浪列表，只需就位

> 原文:[https://www . geesforgeks . org/flat-a-binary-search-tree-convert-the-tree-a-wave-list-in-place-only/](https://www.geeksforgeeks.org/flatten-a-binary-search-tree-to-convert-the-tree-into-a-wave-list-in-place-only/)

给定一个由 **N** 个不同节点组成的[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)，任务是[展平给定的二叉查找树](https://www.geeksforgeeks.org/flatten-a-binary-tree-into-linked-list/)，将树转换成波浪列表。a 波列表 **arr[0..如果**arr[0]>= arr[1]<= arr[2]>= arr[3]<= arr[4]>=…**，则 n-1]** 称为波列表。

**示例:**

> **输入:**
> **1
> /\
> 0 10
> **输出:**
> **0
> \
> 10
> \
> 1****
> 
> ******输入:**3
> /\
> 1 7
> /\/\
> 0 2 5 10
> 
> **输出:**
> 0
> \
> 10
> \
> 1
> \
> 7
> \
> 2
> \
> 5
> \
> 3****

******方法:**给定的问题可以通过观察[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)的[有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)以非递减顺序给出节点来解决。因此，使用树[的迭代有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)和树的有序遍历的反向分别将第一个 **N/2** 和最后一个 **N/2** 节点的给定树的有序遍历存储在两个[栈](https://www.geeksforgeeks.org/stack-data-structure/) **S1** 和 **S2** 中，并获取栈中节点的右指针**波列表**。完成这些步骤后，将树的所有左指针 [**设为空**](https://www.geeksforgeeks.org/few-bytes-on-null-pointer-in-c/) 使其变平。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Tree Node Structure
struct TreeNode {

    int data;
    TreeNode* right;
    TreeNode* left;

    // Constructor
    TreeNode(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Function to insert nodes in the
// binary tree
TreeNode* insertNode(int data,
                     TreeNode* root)
{
    if (root == NULL) {
        TreeNode* node
            = new TreeNode(data);
        return node;
    }
    else if (data > root->data) {
        root->right = insertNode(
            data, root->right);
    }
    else if (data <= root->data) {
        root->left = insertNode(
            data, root->left);
    }

    // Return the root node
    return root;
}

// Function to count number of nodes
int countNodes(TreeNode* root)
{
    if (root == NULL)
        return 0;

    else
        return countNodes(root->left)
               + countNodes(root->right) + 1;
}

// Function to create an array
// to wave array
TreeNode* toWaveList(TreeNode* root)
{
    int count = countNodes(root);
    vector<int> ans;

    // For inorder traversal
    stack<TreeNode*> s1;

    // For reverse Inorder traversal
    stack<TreeNode*> s2;

    TreeNode *root1 = root, *root2 = root;
    TreeNode *curr1 = NULL, *curr2 = NULL;

    // To store the root pointer of tree
    // after flattening
    TreeNode* head = NULL;

    // Flatten the tree
    TreeNode* temp = NULL;

    int l = 0;
    while (l++ < ceil(count / 2.0)) {

        // Iterative inorder traversal
        while (root1) {
            s1.push(root1);
            root1 = root1->left;
        }
        curr1 = s1.top();
        s1.pop();
        root1 = curr1->right;

        // Iterative reverse inorder
        // traversal
        while (root2) {
            s2.push(root2);
            root2 = root2->right;
        }
        curr2 = s2.top();
        s2.pop();
        root2 = curr2->left;

        // Condition for handling situation
        // where both curr1 and curr2 points
        // to the same data
        if (curr1->data == curr2->data) {
            temp->right = curr1;
            temp = temp->right;
            break;
        }

        // Flattening the tree
        if (head == NULL) {
            head = curr1;
            temp = curr1;

            temp->right = curr2;

            // temp->left = NULL
            temp = temp->right;
        }
        else {

            temp->right = curr1;
            temp = temp->right;

            temp->right = curr2;
            temp = temp->right;
        }
    }
    temp->right = NULL;

    // Setting all the left pointers
    // to NULL
    temp = head;
    while (temp) {
        temp->left = NULL;
        temp = temp->right;
    }

    return head;
}

// Driver Code
int main()
{
    TreeNode* root = NULL;
    int tree[] = { 1, 0, 10 };
    for (int i = 0; i < 3; i++) {
        root = insertNode(tree[i], root);
    }

    // Function Call
    TreeNode* head = toWaveList(root);
    while (head) {
        cout << head->data << " ";
        head = head->right;
    }

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;
class GFG{

// Tree Node Structure
static class TreeNode {

    int data;
    TreeNode right;
    TreeNode left;

    // Constructor
    TreeNode(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Function to insert nodes in the
// binary tree
static TreeNode insertNode(int data,
                     TreeNode root)
{
    if (root == null) {
        TreeNode node
            = new TreeNode(data);
        return node;
    }
    else if (data > root.data) {
        root.right = insertNode(
            data, root.right);
    }
    else if (data <= root.data) {
        root.left = insertNode(
            data, root.left);
    }

    // Return the root node
    return root;
}

// Function to count number of nodes
static int countNodes(TreeNode root)
{
    if (root == null)
    return 0;

    else
        return countNodes(root.left)
               + countNodes(root.right) + 1;
}

// Function to create an array
// to wave array
static TreeNode toWaveList(TreeNode root)
{
    int count = countNodes(root);
    Vector<Integer> ans = new Vector<>();

    // For inorder traversal
    Stack<TreeNode> s1 = new Stack<>();

    // For reverse Inorder traversal
    Stack<TreeNode> s2 = new Stack<>();

    TreeNode root1 = root, root2 = root;
    TreeNode curr1 = null, curr2 = null;

    // To store the root pointer of tree
    // after flattening
    TreeNode head = null;

    // Flatten the tree
    TreeNode temp = null;

    int l = 0;
    while (l++ < Math.ceil(count / 2.0)) {

        // Iterative inorder traversal
        while (root1 != null) {
            s1.add(root1);
            root1 = root1.left;
        }
        curr1 = s1.peek();
        s1.pop();
        root1 = curr1.right;

        // Iterative reverse inorder
        // traversal
        while (root2 != null) {
            s2.add(root2);
            root2 = root2.right;
        }
        curr2 = s2.peek();
        s2.pop();
        root2 = curr2.left;

        // Condition for handling situation
        // where both curr1 and curr2 points
        // to the same data
        if (curr1.data == curr2.data) {
            temp.right = curr1;
            temp = temp.right;
            break;
        }

        // Flattening the tree
        if (head == null) {
            head = curr1;
            temp = curr1;

            temp.right = curr2;

            // temp.left = null
            temp = temp.right;
        }
        else {

            temp.right = curr1;
            temp = temp.right;

            temp.right = curr2;
            temp = temp.right;
        }
    }
    temp.right = null;

    // Setting all the left pointers
    // to null
    temp = head;
    while (temp!=null) {
        temp.left = null;
        temp = temp.right;
    }

    return head;
}

// Driver Code
public static void main(String[] args)
{
    TreeNode root = null;
    int tree[] = { 1, 0, 10 };
    for (int i = 0; i < 3; i++) {
        root = insertNode(tree[i], root);
    }

    // Function Call
    TreeNode head = toWaveList(root);
    while (head!=null) {
        System.out.print(head.data+ " ");
        head = head.right;
    }

}
}

// This code is contributed by gauravrajput1**
```

## ****java 描述语言****

```
**<script>

// Javascript program for the above approach

// Tree Node Structure
class TreeNode {

    // Constructor
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Function to insert nodes in the
// binary tree
function insertNode(data, root)
{
    if (root == null) {
        let node = new TreeNode(data);
        return node;
    }
    else if (data > root.data) {
        root.right = insertNode(
            data, root.right);
    }
    else if (data <= root.data) {
        root.left = insertNode(
            data, root.left);
    }

    // Return the root node
    return root;
}

// Function to count number of nodes
function countNodes(root)
{
    if (root == null)
        return 0;

    else
        return countNodes(root.left)
               + countNodes(root.right) + 1;
}

// Function to create an array
// to wave array
function toWaveList(root)
{
    let count = countNodes(root);
    let ans = [];

    // For inorder traversal
    let s1 = [];

    // For reverse Inorder traversal
    let s2 = [];

    let root1 = root, root2 = root;
    let curr1 = null, curr2 = null;

    // To store the root pointer of tree
    // after flattening
    let head = null;

    // Flatten the tree
    let temp = null;

    let l = 0;
    while (l++ < Math.ceil(count / 2.0)) {

        // Iterative inorder traversal
        while (root1) {
            s1.push(root1);
            root1 = root1.left;
        }
        curr1 = s1[s1.length - 1];
        s1.pop();
        root1 = curr1.right;

        // Iterative reverse inorder
        // traversal
        while (root2) {
            s2.push(root2);
            root2 = root2.right;
        }
        curr2 = s2[s2.length - 1]
        s2.pop();
        root2 = curr2.left;

        // Condition for handling situation
        // where both curr1 and curr2 points
        // to the same data
        if (curr1.data == curr2.data) {
            temp.right = curr1;
            temp = temp.right;
            break;
        }

        // Flattening the tree
        if (head == null) {
            head = curr1;
            temp = curr1;

            temp.right = curr2;

            // temp.left = null
            temp = temp.right;
        }
        else {

            temp.right = curr1;
            temp = temp.right;

            temp.right = curr2;
            temp = temp.right;
        }
    }
    temp.right = null;

    // Setting all the left pointers
    // to null
    temp = head;
    while (temp) {
        temp.left = null;
        temp = temp.right;
    }

    return head;
}

// Driver Code

    let root = null;
    let tree = [ 1, 0, 10 ];
    for (let i = 0; i < 3; i++) {
        root = insertNode(tree[i], root);
    }

    // Function Call
    let head = toWaveList(root);
    while (head) {
        document.write(head.data +" ");
        head = head.right;
    }

// This code is contributed by saurabh_jaiswal.

</script>**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

  // Tree Node Structure
  public    class TreeNode {

    public    int data;
    public    TreeNode right;
    public    TreeNode left;

    // Constructor
    public    TreeNode(int data) {
      this.data = data;
      this.left = null;
      this.right = null;
    }
  };

  // Function to insert nodes in the
  // binary tree
  static TreeNode insertNode(int data, TreeNode root) {
    if (root == null) {
      TreeNode node = new TreeNode(data);
      return node;
    } else if (data > root.data) {
      root.right = insertNode(data, root.right);
    } else if (data <= root.data) {
      root.left = insertNode(data, root.left);
    }

    // Return the root node
    return root;
  }

  // Function to count number of nodes
  static int countNodes(TreeNode root) {
    if (root == null)
      return 0;

    else
      return countNodes(root.left) + countNodes(root.right) + 1;
  }

  // Function to create an array
  // to wave array
  static TreeNode toWaveList(TreeNode root) {
    int count = countNodes(root);
    List<int> ans = new List<int>();

    // For inorder traversal
    Stack<TreeNode> s1 = new Stack<TreeNode>();

    // For reverse Inorder traversal
    Stack<TreeNode> s2 = new Stack<TreeNode>();

    TreeNode root1 = root, root2 = root;
    TreeNode curr1 = null, curr2 = null;

    // To store the root pointer of tree
    // after flattening
    TreeNode head = null;

    // Flatten the tree
    TreeNode temp = null;

    int l = 0;
    while (l++ < Math.Ceiling(count / 2.0)) {

      // Iterative inorder traversal
      while (root1 != null) {
        s1.Push(root1);
        root1 = root1.left;
      }
      curr1 = s1.Peek();
      s1.Pop();
      root1 = curr1.right;

      // Iterative reverse inorder
      // traversal
      while (root2 != null) {
        s2.Push(root2);
        root2 = root2.right;
      }
      curr2 = s2.Peek();
      s2.Pop();
      root2 = curr2.left;

      // Condition for handling situation
      // where both curr1 and curr2 points
      // to the same data
      if (curr1.data == curr2.data) {
        temp.right = curr1;
        temp = temp.right;
        break;
      }

      // Flattening the tree
      if (head == null) {
        head = curr1;
        temp = curr1;

        temp.right = curr2;

        // temp.left = null
        temp = temp.right;
      } else {

        temp.right = curr1;
        temp = temp.right;

        temp.right = curr2;
        temp = temp.right;
      }
    }
    temp.right = null;

    // Setting all the left pointers
    // to null
    temp = head;
    while (temp != null) {
      temp.left = null;
      temp = temp.right;
    }

    return head;
  }

  // Driver Code
  public static void Main(String[] args) {
    TreeNode root = null;
    int []tree = { 1, 0, 10 };
    for (int i = 0; i < 3; i++) {
      root = insertNode(tree[i], root);
    }

    // Function Call
    TreeNode head = toWaveList(root);
    while (head != null) {
      Console.Write(head.data + " ");
      head = head.right;
    }

  }
}

// This code is contributed by gauravrajput1**
```

******Output:** 

```
0 10 1
```**** 

*******时间复杂度:** O(N)*
***辅助空间:** O(H)，其中 H 是* [*高度的 BST*](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/) *。*****