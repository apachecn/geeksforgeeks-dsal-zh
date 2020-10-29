# 根据顺序和级别顺序遍历构造树 | 系列 2

> 原文：[https://www.geeksforgeeks.org/construct-tree-inorder-level-order-traversals-set-2/](https://www.geeksforgeeks.org/construct-tree-inorder-level-order-traversals-set-2/)

给定二叉树的有序遍历和层级遍历，构造二叉树。 下面是一个示例来说明此问题。

例子：

```
Input: Two arrays that represent Inorder
       and level order traversals of a 
       Binary Tree
in[]    = {4, 8, 10, 12, 14, 20, 22};
level[] = {20, 8, 22, 4, 12, 10, 14};

Output: Construct the tree represented 
        by the two arrays.
        For the above two arrays, the 
        constructed tree is shown.

```

我们在[下面的文章](https://www.geeksforgeeks.org/construct-tree-inorder-level-order-traversals/)中讨论了一种可用于`O(N ^ 3)`解决方案。

**方法**：以下算法使用`O(N ^ 2)`时间复杂度来解决上述问题，它使用 C++ 中的[`unordered_set`](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)数据结构（基本上是创建哈希表）来放入 当前根的左子树以及以后的子树，我们将检查`O(1)`的复杂度，以确定当前的`levelOrder`节点是否是左子树的一部分。

如果它是左侧子树的一部分，则为左侧添加一个`lLevel`数组，否则将其添加到右侧子树的`rLevel`数组中。

以下是具有上述想法的 C++ 实现

```
/* program to construct tree using inorder
and levelorder traversals */
#include <iostream>
#include<set>
using namespace std;
。
/* A binary tree node */
struct Node
{
int key;
struct Node* left, *right;
};
Node* makeNode( int data){
Node* newNode = new Node();
newNode->key = data;
newNode->right = newNode->right = NULL;
return newNode;
}
// Function to build tree from given
// levelorder and inorder
Node* buildTree( int inorder[], int levelOrder[],
int iStart, int iEnd, int n)
{
if (n <= 0)
return NULL;
// First node of level order is root
Node* root = makeNode(levelOrder[0]);
// Search root in inorder
int index = -1;
]
for ( int i=iStart; i<=iEnd; i++){
if (levelOrder[0] == inorder[i]){
index = i;
break ;
}
}
// Insert all left nodes in hash table
unordered_set< int > s;
for ( int i=iStart;i<index;i++)
s.insert(inorder[i]);
// Separate level order traversals
// of left and right subtrees.
int [HT G107] // Left
int rLevel[iEnd-iStart-s.size()]; // Right
int li = 0, ri = 0;
for ( int i=1;i<n;i++) {
if (s.find(levelOrder[i]) != s.end())
lLevel[li++] = levelOrder[i];
else
rLevel[ri++] = levelOrder[i];
}
// Recursively build left and right
// subtrees and return root.
root->left = buildTree(inorder, lLevel,
iStart, index-1, index-iStart);
root->right = buildTree(inorder, rLevel,
index+1, iEnd, iEnd-index);
return root;
}
] /* Utility function to print inorder
traversal of binary tree */
void printInorder(Node* node)
{
if (node == NULL)
return ;
printInorder(node->left);
cout << node->key << " " ;
printInorder(node->right);
}
// Driver Code
int main()
{
int in[] = {4, 8, 10, 12, 14, 20, 22};
int level[] = {20, 8, 22, 4, 12, 10, 14};
int n = sizeof (in)/ sizeof (in[0]);
Node *root = buildTree(in, level, 0,
n - 1, n);
[
/* Let us test the built tree by
printing Insorder traversal */
cout << "Inorder traversal of the "
"constructed tree is \n" ;
printInorder(root);
return 0;
}
```

输出：

```
Inorder traversal of the
constructed tree is 4 8 10 12 14 
20 22 
```

时间复杂度：`O(N ^ 2)`



* * *

* * *



