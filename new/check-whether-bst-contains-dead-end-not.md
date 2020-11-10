# 检查 BST 是否包含死角

> 原文：[https://www.geeksforgeeks.org/check-whether-bst-contains-dead-end-not/](https://www.geeksforgeeks.org/check-whether-bst-contains-dead-end-not/)

给定[二分搜索树](http://quiz.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)，其中包含大于 0 的正整数值。任务是检查 BST 是否包含死角。 此处的“死角”意味着，我们无法在该节点之后插入任何元素。

例子：

```
Input :        8
             /   \ 
           5      9
         /   \
        2     7
       /
      1               
Output : Yes
Explanation : Node "1" is the dead End because
         after that we cant insert any element.       

Input :       8
            /   \ 
           7     10
         /      /   \
        2      9     13

Output : Yes
Explanation : We can't insert any element at 
              node 9\.  

```

如果我们仔细研究问题，我们可以注意到，我们基本上需要检查是否存在值`x`的叶节点，使得`x = 1`时 BST 中存在`x + 1`和`x-1`。对于`x = 1`， 我们不能插入 0，因为问题陈述说 BST 仅包含正整数。

为了实现上述想法，我们首先遍历整个 BST 并将所有节点存储在哈希映射中。 我们还将所有叶子存储在单独的哈希中，以避免重新遍历 BST。 最后，我们检查每个叶节点`x`，是否在哈希映射中存在`x-1`和`x + 1`。

下面是上述思想的 C++ 实现。

```
// C++ program check weather BST contains
// dead end or not
#include<bits/stdc++.h>
using namespace std;
[
// A BST node
struct Node
{
int data;
struct Node *left, *right;
};
// A utility function to create a new node
Node *newNode( int data)
{
Node *temp = new Node;
temp->data = data;
temp->left = temp->right = NULL;
return temp;
}
[
/* A utility function to insert a new Node
with given key in BST */
struct Node* insert( struct Node* node, int key)
{
/* If the tree is empty, return a new Node */
if (node == NULL) return newNode(key);
/* Otherwise, recur down the tree */
if (key < node->data)
node->left = insert(node->left, key);
else if (key > node->data)
node->right = insert(node->right, key);
[
/* return the (unchanged) Node pointer */
return node;
}
// Function to store all node of given binary search tree
void storeNodes(Node * root, unordered_set< int > &all_nodes,
unordered_set< int > &leaf_nodes)
{
if (root == NULL)
return ;
// store all node of binary search tree
all_nodes.insert(root->data);
// store leaf node in leaf_hash
if (root->left==NULL && root->right==NULL)
{
leaf_nodes.insert(root->data);
return ;
}
// recur call rest tree
storeNodes(root-> left, all_nodes, leaf_nodes);
storeNodes(root->right, all_nodes, leaf_nodes);
}
[
// Returns true if there is a dead end in tree,
// else false.
bool isDeadEnd(Node *root)
{
// Base case
if (root == NULL)
return false ;
// create two empty hash sets that store all
// BST elements and leaf nodes respectively.
unordered_set< int > all_nodes, leaf_nodes;
// insert 0 in 'all_nodes' for handle case
// if bst contain value 1
all_nodes.insert(0);
// Call storeNodes function to store all BST Node
storeNodes(root, all_nodes, leaf_nodes);
// Traversal leaf node and check Tree contain
// continuous sequence of
// size tree or Not
for ( auto i = leaf_nodes.begin() ; i != leaf_nodes.end(); i++)
{
int x = (*i);
// Here we check first and last element of
// continuous sequence that are x-1 & x+1
if (all_nodes.find(x+1) != all_nodes.end() &&
all_nodes.find(x-1) != all_nodes.end())
return true ;
}
return false ;
}
// Driver program
int main()
{
/*       8
/   \
5    11
/  \
2    7
\
3
\
4 */
Node *root = NULL;
root = insert(root, 8);
root = insert(root, 5);
root = insert(root, 2);
root = insert(root, 3);
root = insert(root, 7);
root = insert(root, 11);
root = insert(root, 4);
if (isDeadEnd(root) == true )
cout << "Yes " << endl;
else
cout << "No " << endl;
return 0;
}
```

输出：

```
Yes

```

时间复杂度：`O(n)`

[简单递归解决方案，用于检查 BST 是否包含死端](https://www.geeksforgeeks.org/simple-recursive-solution-check-whether-bst-contains-dead-end/)

本文由 [**Nishant_Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

