# 删除给定节点后，打印二叉树的森林

> 原文：[https://www.geeksforgeeks.org/print-the-forests-of-a-binary-tree-after-removal-of-given-nodes/](https://www.geeksforgeeks.org/print-the-forests-of-a-binary-tree-after-removal-of-given-nodes/)

给定[**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/)和由要删除的节点值组成的数组`arr[]`，任务是打印[有序遍历](http://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) 删除节点后的[森林](https://www.geeksforgeeks.org/count-number-trees-forest/)中的一个。

**示例**：

> **输入**：`arr[] = {10, 5}`
> 
> ```
>         10
>        /  \
>       20   30
>      / \    \
>     4   5    7
> 
> ```
> 
> **输出**：
>
> ```
> 4 20
> 30 7
> ```
> 
> **输入**：`arr[] = {5}`
> 
> ```
>          1
>        /   \
>       5     6
>      /       \
>     10       12 
> 
> ```
> 
> **输出**：
>
> ```
> 10
> 1 6 12
> ```

**方法**：请按照以下步骤解决问题：

1.  执行二叉树的[后序遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal/)。
2.  对于每个节点，检查它是否包含要删除的值。
3.  如果发现是真的，则将其子级存储为森林的根。 通过[有序遍历](http://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)打印森林。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 

// the above approach 

#include <bits/stdc++.h> 

using namespace std; 

// Stores the nodes to be deleted 

unordered_map<int, bool> mp; 

// Structure of a Tree node 

struct Node { 

    int key; 

    struct Node *left, *right; 

}; 

// Function to create a new node 

Node* newNode(int key) 

{ 

    Node* temp = new Node; 

    temp->key = key; 

    temp->left = temp->right = NULL; 

    return (temp); 

} 

// Function to check whether the node 

// needs to be deleted or not 

bool deleteNode(int nodeVal) 

{ 

    return mp.find(nodeVal) != mp.end(); 

} 

// Function to perform tree pruning 

// by performing post order traversal 

Node* treePruning(Node* root, vector<Node*>& result) 

{ 

    if (root == NULL) 

        return NULL; 

    root->left = treePruning(root->left, result); 

    root->right = treePruning(root->right, result); 

    // If the node needs to be deleted 

    if (deleteNode(root->key)) { 

        // Store the its subtree 

        if (root->left) { 

            result.push_back(root->left); 

        } 

        if (root->right) { 

            result.push_back(root->right); 

        } 

        return NULL; 

    } 

    return root; 

} 

// Perform Inorder Traversal 

void printInorderTree(Node* root) 

{ 

    if (root == NULL) 

        return; 

    printInorderTree(root->left); 

    cout << root->key << " "; 

    printInorderTree(root->right); 

} 

// Function to print the forests 

void printForests(Node* root, int arr[], int n) 

{ 

    for (int i = 0; i < n; i++) { 

        mp[arr[i]] = true; 

    } 

    // Stores the remaining nodes 

    vector<Node*> result; 

    if (treePruning(root, result)) 

        result.push_back(root); 

    // Print the inorder traversal of Forests 

    for (int i = 0; i < result.size(); i++) { 

        printInorderTree(result[i]); 

        cout << endl; 

    } 

} 

// Driver Code 

int main() 

{ 

    Node* root = newNode(1); 

    root->left = newNode(12); 

    root->right = newNode(13); 

    root->right->left = newNode(14); 

    root->right->right = newNode(15); 

    root->right->left->left = newNode(21); 

    root->right->left->right = newNode(22); 

    root->right->right->left = newNode(23); 

    root->right->right->right = newNode(24); 

    int arr[] = { 14, 23, 1 }; 

    int n = sizeof(arr) / sizeof(arr[0]); 

    printForests(root, arr, n); 

} 

```

## Java

```java

// Java Program to implement 

// the above approach 

import java.util.*; 

class GFG{ 

// Stores the nodes to be deleted 

static HashMap<Integer,  

                 Boolean> mp  = new HashMap<>(); 

// Structure of a Tree node 

static class Node 

{ 

    int key; 

    Node left, right; 

}; 

// Function to create a new node 

static Node newNode(int key) 

{ 

    Node temp = new Node(); 

    temp.key = key; 

    temp.left = temp.right = null; 

    return (temp); 

} 

// Function to check whether the node 

// needs to be deleted or not 

static boolean deleteNode(int nodeVal) 

{ 

    return mp.containsKey(nodeVal); 

} 

// Function to perform tree pruning 

// by performing post order traversal 

static Node treePruning(Node root,  

                        Vector<Node> result) 

{ 

    if (root == null) 

        return null; 

    root.left = treePruning(root.left, result); 

    root.right = treePruning(root.right, result); 

    // If the node needs to be deleted 

    if (deleteNode(root.key))  

    { 

        // Store the its subtree 

        if (root.left != null)  

        { 

            result.add(root.left); 

        } 

        if (root.right != null) 

        { 

            result.add(root.right); 

        } 

        return null; 

    } 

    return root; 

} 

// Perform Inorder Traversal 

static void printInorderTree(Node root) 

{ 

    if (root == null) 

        return; 

    printInorderTree(root.left); 

    System.out.print(root.key + " "); 

    printInorderTree(root.right); 

} 

// Function to print the forests 

static void printForests(Node root,  

                         int arr[], int n) 

{ 

    for (int i = 0; i < n; i++) 

    { 

        mp.put(arr[i], true); 

    } 

    // Stores the remaining nodes 

    Vector<Node> result  = new Vector<>(); 

    if (treePruning(root, result) != null) 

        result.add(root); 

    // Print the inorder traversal of Forests 

    for (int i = 0; i < result.size(); i++)  

    { 

        printInorderTree(result.get(i)); 

        System.out.println(); 

    } 

} 

// Driver Code 

public static void main(String[] args) 

{ 

    Node root = newNode(1); 

    root.left = newNode(12); 

    root.right = newNode(13); 

    root.right.left = newNode(14); 

    root.right.right = newNode(15); 

    root.right.left.left = newNode(21); 

    root.right.left.right = newNode(22); 

    root.right.right.left = newNode(23); 

    root.right.right.right = newNode(24); 

    int arr[] = { 14, 23, 1 }; 

    int n = arr.length; 

    printForests(root, arr, n); 

} 

} 

// This code is contributed by Rajput-Ji

```

## C#

```cs

// C# program to implement 

// the above approach 

using System; 

using System.Collections.Generic; 

class GFG{ 

// Stores the nodes to be deleted 

static Dictionary<int,  

                  Boolean> mp = new Dictionary<int, 

                                               Boolean>(); 

// Structure of a Tree node 

class Node 

{ 

    public int key; 

    public Node left, right; 

}; 

// Function to create a new node 

static Node newNode(int key) 

{ 

    Node temp = new Node(); 

    temp.key = key; 

    temp.left = temp.right = null; 

    return (temp); 

} 

// Function to check whether the node 

// needs to be deleted or not 

static bool deleteNode(int nodeVal) 

{ 

    return mp.ContainsKey(nodeVal); 

} 

// Function to perform tree pruning 

// by performing post order traversal 

static Node treePruning(Node root,  

                        List<Node> result) 

{ 

    if (root == null) 

        return null; 

    root.left = treePruning(root.left, result); 

    root.right = treePruning(root.right, result); 

    // If the node needs to be deleted 

    if (deleteNode(root.key))  

    { 

        // Store the its subtree 

        if (root.left != null)  

        { 

            result.Add(root.left); 

        } 

        if (root.right != null) 

        { 

            result.Add(root.right); 

        } 

        return null; 

    } 

    return root; 

} 

// Perform Inorder Traversal 

static void printInorderTree(Node root) 

{ 

    if (root == null) 

        return; 

    printInorderTree(root.left); 

    Console.Write(root.key + " "); 

    printInorderTree(root.right); 

} 

// Function to print the forests 

static void printForests(Node root,  

                         int []arr, int n) 

{ 

    for(int i = 0; i < n; i++) 

    { 

        mp.Add(arr[i], true); 

    } 

    // Stores the remaining nodes 

    List<Node> result = new List<Node>(); 

    if (treePruning(root, result) != null) 

        result.Add(root); 

    // Print the inorder traversal of Forests 

    for(int i = 0; i < result.Count; i++)  

    { 

        printInorderTree(result[i]); 

        Console.WriteLine(); 

    } 

} 

// Driver Code 

public static void Main(String[] args) 

{ 

    Node root = newNode(1); 

    root.left = newNode(12); 

    root.right = newNode(13); 

    root.right.left = newNode(14); 

    root.right.right = newNode(15); 

    root.right.left.left = newNode(21); 

    root.right.left.right = newNode(22); 

    root.right.right.left = newNode(23); 

    root.right.right.right = newNode(24); 

    int []arr = { 14, 23, 1 }; 

    int n = arr.Length; 

    printForests(root, arr, n); 

} 

} 

// This code is contributed by Amit Katiyar  

```

**输出**： 

```

21 

22 

12 

13 15 24

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。



* * *

* * *



