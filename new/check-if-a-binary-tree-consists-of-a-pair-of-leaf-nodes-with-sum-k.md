# 检查二叉树是否包含一对总和为`K`的叶节点

> 原文：[https://www.geeksforgeeks.org/check-if-a-binary-tree-consists-of-a-pair-of-leaf-nodes-with-sum-k/](https://www.geeksforgeeks.org/check-if-a-binary-tree-consists-of-a-pair-of-leaf-nodes-with-sum-k/)

给定[**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/)和整数`K`，任务是检查树是否由一对叶节点组成，它们的总和为`K`。 如果有多对，则打印其中任何一对。 否则打印 -1。

**注意**：假定给定的二叉树将始终具有多个 1 个叶节点。

**示例**：

> **输入**：`X = 13`
> 
> ```
>              1
>            /   \
>           2     3
>          / \   / \
>         4   5 6   7
>                \
>                 8
> 
> ```
> 
> **输出**：`[5, 8]`
> 
> **说明**：
> 
> 给定的二叉树由 4 个叶节点`[4, 5, 6, 8]`组成。
>
> 这对值 5 和 8 的节点对之和为 13。
> 
> **输入**：`X = 6`
> 
> ```
>            -1        
>            /  \
>           2    3
>          / \   
>         4   5 
> 
> ```
> 
> **输出**：`[-1]`
> 
> **说明**：
>
> 给定的二叉树由 3 个叶节点`[4, 5, 3]`组成。
>
> 不存在其值之和等于 6 的有效节点对。
>
> 因此，打印 -1。

**朴素的方法**：解决该问题的最简单方法是[遍历树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)并将所有叶节点存储在一个数组中。 然后[对数组排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)，并使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)查找是否存在所需的对。

**时间复杂度**：`O(NlogN)`

**辅助空间**：`O(n)`

**有效方法**：可以使用[`HashSet`](http://www.geeksforgeeks.org/hashset-in-java/)优化上述方法。 请按照以下步骤解决问题：

*   创建[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)以存储叶节点的值。
*   [遍历树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，对于每个叶子节点，检查**叶子节点的`K`值**是否存在于[无序集合](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)中。
*   如果发现为真，则打印所有节点值。
*   否则，将当前节点的值存储到无序集中。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 

// the above approach 

#include <bits/stdc++.h> 

using namespace std; 

// Stores if a pair exists or not 

bool pairFound = false; 

// Struct binary tree node 

struct Node { 

    int data; 

    Node *left, *right; 

}; 

// Creates a new node 

Node* newNode(int data) 

{ 

    Node* temp = new Node(); 

    temp->data = data; 

    temp->left = temp->right = NULL; 

    return temp; 

} 

// Function to check if a pair of leaf 

// nodes exists with sum K 

void pairSum(Node* root, int target, 

             unordered_set<int>& S) 

{ 

    // checks if root is NULL 

    if (!root) 

        return; 

    // Checks if the current node is a leaf node 

    if (!root->left and !root->right) { 

        // Checks for a valid pair of leaf nodes 

        if (S.count(target - root->data)) { 

            cout << target - root->data << " "

                 << root->data; 

            pairFound = true; 

            return; 

        } 

        // Insert value of current node 

        // into the set 

        else

            S.insert(root->data); 

    } 

    // Traverse left and right subtree 

    pairSum(root->left, target, S); 

    pairSum(root->right, target, S); 

} 

// Driver Code 

int main() 

{ 

    // Construct binary tree 

    Node* root = newNode(1); 

    root->left = newNode(2); 

    root->left->left = newNode(4); 

    root->left->right = newNode(5); 

    root->right = newNode(3); 

    root->right->left = newNode(6); 

    root->right->right = newNode(7); 

    root->right->right->right = newNode(8); 

    // Stores the leaf nodes 

    unordered_set<int> S; 

    int K = 13; 

    pairSum(root, K, S); 

    if (pairFound == false) 

        cout << "-1"; 

    return 0; 

} 

```

## Java

```java

// Java program to implement 

// the above approach 

import java.util.*; 

class GFG{ 

// Stores if a pair exists or not 

static boolean pairFound = false; 

// Struct binary tree node 

static class Node  

{ 

    int data; 

    Node left, right; 

}; 

// Creates a new node 

static Node newNode(int data) 

{ 

    Node temp = new Node(); 

    temp.data = data; 

    temp.left = temp.right = null; 

    return temp; 

} 

// Function to check if a pair of leaf 

// nodes exists with sum K 

static void pairSum(Node root, int target, 

                    HashSet<Integer> S) 

{ 

    // Checks if root is null 

    if (root == null) 

        return; 

    // Checks if the current node is a leaf node 

    if (root.left == null && root.right == null) 

    { 

        // Checks for a valid pair of leaf nodes 

        if (S.contains(target - root.data))  

        { 

            System.out.print(target - root.data +  

                                " " + root.data); 

            pairFound = true; 

            return; 

        } 

        // Insert value of current node 

        // into the set 

        else

            S.add(root.data); 

    } 

    // Traverse left and right subtree 

    pairSum(root.left, target, S); 

    pairSum(root.right, target, S); 

} 

// Driver Code 

public static void main(String[] args) 

{ 

    // Construct binary tree  

    Node root = newNode(1); 

    root.left = newNode(2); 

    root.left.left = newNode(4); 

    root.left.right = newNode(5); 

    root.right = newNode(3); 

    root.right.left = newNode(6); 

    root.right.right = newNode(7); 

    root.right.right.right = newNode(8); 

    // Stores the leaf nodes 

    HashSet<Integer> S = new HashSet<Integer>(); 

    int K = 13; 

    pairSum(root, K, S); 

    if (pairFound == false) 

        System.out.print("-1"); 

} 

} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# program to implement 

// the above approach 

using System; 

using System.Collections.Generic; 

class GFG{ 

// Stores if a pair exists or not 

static bool pairFound = false; 

// Struct binary tree node 

class Node  

{ 

    public int data; 

    public Node left, right; 

}; 

// Creates a new node 

static Node newNode(int data) 

{ 

    Node temp = new Node(); 

    temp.data = data; 

    temp.left = temp.right = null; 

    return temp; 

} 

// Function to check if a pair of leaf 

// nodes exists with sum K 

static void pairSum(Node root, int target, 

                    HashSet<int> S) 

{ 

    // Checks if root is null 

    if (root == null) 

        return; 

    // Checks if the current node is a leaf node 

    if (root.left == null && root.right == null) 

    { 

        // Checks for a valid pair of leaf nodes 

        if (S.Contains(target - root.data))  

        { 

            Console.Write(target - root.data +  

                             " " + root.data); 

            pairFound = true; 

            return; 

        } 

        // Insert value of current node 

        // into the set 

        else

            S.Add(root.data); 

    } 

    // Traverse left and right subtree 

    pairSum(root.left, target, S); 

    pairSum(root.right, target, S); 

} 

// Driver Code 

public static void Main(String[] args) 

{ 

    // Construct binary tree  

    Node root = newNode(1); 

    root.left = newNode(2); 

    root.left.left = newNode(4); 

    root.left.right = newNode(5); 

    root.right = newNode(3); 

    root.right.left = newNode(6); 

    root.right.right = newNode(7); 

    root.right.right.right = newNode(8); 

    // Stores the leaf nodes 

    HashSet<int> S = new HashSet<int>(); 

    int K = 13; 

    pairSum(root, K, S); 

    if (pairFound == false) 

        Console.Write("-1"); 

} 

} 

// This code is contributed by 29AjayKumar 

```

**输出**： 

```

5 8

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



