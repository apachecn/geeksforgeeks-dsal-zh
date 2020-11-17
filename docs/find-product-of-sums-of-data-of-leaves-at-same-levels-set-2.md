# 查找相同级别的叶子数据总和的乘积 | 系列 2

> 原文：[https://www.geeksforgeeks.org/find-product-of-sums-of-data-of-leaves-at-same-levels-set-2/](https://www.geeksforgeeks.org/find-product-of-sums-of-data-of-leaves-at-same-levels-set-2/)

给定二叉树，为其返回以下值。

*   对于每个级别，如果此级别上有叶子，则计算所有叶子的总和。 否则忽略它。

*   返回所有总和的乘积。

**示例**：

```
Input: Root of below tree
         2
       /   \
      7     5
             \
              9
Output: 63
First levels doesn't have leaves. Second level
has one leaf 7 and third level also has one 
leaf 9\. Therefore result is 7*9 = 63

Input: Root of below tree
         2
       /   \
     7      5
    / \      \
   8   6      9
      / \    /  \
     1  11  4    10 

Output: 208
First two levels don't have leaves. Third
level has single leaf 8\. Last level has four
leaves 1, 11, 4 and 10\. Therefore result is 
8 * (1 + 11 + 4 + 10)  

```

在[先前的文章](https://www.geeksforgeeks.org/find-multiplication-of-sums-of-data-of-all-leaves-at-sane-levels/)中，我们看到了使用[层次顺序遍历](http://www.geeksforgeeks.org/level-order-tree-traversal/)的基于[队列](http://www.geeksforgeeks.org/queue-data-structure/)的解决方案。

在这里，我们只是在对二叉树进行[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，并且在 C++ STL 中使用了[`unordered_map`](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)在存储相同级别的叶节点的总和。 然后，在一次遍历映射的过程中，我们计算了级别总和的最终乘积。

下面是上述方法的实现：

```cpp
// C++ program to find product of sums 
// of data of leaves at same levels 
// using map in STL 
#include <bits/stdc++.h> 
using namespace std; 
  
// Binary Tree Node 
struct Node { 
    int data; 
    Node* left; 
    Node* right; 
}; 
  
// Utitlity function to create 
// a new Tree node 
Node* newNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->left = temp->right = NULL; 
    return temp; 
} 
  
// Helper function to calculate sum of 
// leaf nodes at same level and store in 
// an unordered_map 
void productOfLevelSumUtil(Node* root, 
       unordered_map<int, int>& level_sum, 
                                int level) 
{ 
  
    if (!root) 
        return; 
  
    // Check if current node is a leaf node 
    // If yes add it to sum of current level 
    if (!root->left && !root->right) 
        level_sum[level] += root->data; 
  
    // Traverse left subtree 
    productOfLevelSumUtil(root->left, level_sum, 
                          level + 1); 
  
    // Traverse right subtree 
    productOfLevelSumUtil(root->right, level_sum, 
                          level + 1); 
} 
  
// Function to calculate product of level sums 
int productOfLevelSum(Node* root) 
{ 
    // Create a map to store sum of leaf 
    // nodes at same levels. 
    unordered_map<int, int> level_sum; 
  
    // Call the helper function to 
    // calculate level sums of leaf nodes 
    productOfLevelSumUtil(root, level_sum, 0); 
  
    // variable to store final product 
    int prod = 1; 
  
    // Traverse the map to calculate product 
    // of level sums 
    for (auto it = level_sum.begin();  
                it != level_sum.end(); it++) 
        prod *= it->second; 
  
    // Return the result 
    return prod; 
} 
  
// Driver Code 
int main() 
{ 
    // Creating Binary Tree 
    Node* root = newNode(2); 
    root->left = newNode(7); 
    root->right = newNode(5); 
    root->left->right = newNode(6); 
    root->left->left = newNode(8); 
    root->left->right->left = newNode(1); 
    root->left->right->right = newNode(11); 
    root->right->right = newNode(9); 
    root->right->right->left = newNode(4); 
    root->right->right->right = newNode(10); 
  
    cout << "Final product is = "
         << productOfLevelSum(root) << endl; 
  
    return 0; 
} 
```

**输出**：

```
Final product is = 208

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。

其中`N`是二叉树中节点的数量。



* * *

* * *



