# 成对交换二叉树中的叶节点

> 原文:[https://www . geesforgeks . org/pair-swap-leaf-nodes-二叉树/](https://www.geeksforgeeks.org/pairwise-swap-leaf-nodes-binary-tree/)

给定一棵二叉树，我们需要编写一个程序，从左到右成对地交换给定二叉树中的叶节点，如下所示。

交换前的树:

![](img/909a1c04e02efb05f7e7340542a1a532.png)

交换后的树:

![](img/e881715b30b4804c24256a926d8c9986.png)
原始二叉树中叶节点从左到右的顺序为(4，6，7，9，10)。现在，如果我们试图从这个序列形成对，我们将有两对，如(4，6)，(7，9)。最后一个节点(10)无法与任何节点配对，因此保持未配对。

解决这个问题的思路是先[从左到右遍历二叉树的叶节点。](https://www.geeksforgeeks.org/print-leaf-nodes-left-right-binary-tree/)
在遍历叶节点时，我们维护两个指针来跟踪一对中的第一个和第二个叶节点，以及一个变量 *count* 来跟踪遍历的叶节点的计数。
现在，如果我们仔细观察，那么我们看到，当遍历时，如果遍历的叶节点数是偶数，这意味着我们可以形成一对叶节点。为了跟踪这一对，我们采用两个指针*第一个指针*和*第二个指针*，如上所述。每次我们遇到一个叶节点，我们就用这个叶节点初始化 *secondPtr* 。现在如果*计数*为奇数，我们用*秒 Ptr* 初始化*第一个 Ptr* ，否则我们简单地交换这两个节点。

下面是上述思想的 C++实现:

```
/* C++ program to pairwise swap
   leaf nodes from left to right */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// function to swap two Node
void Swap(Node **a, Node **b)
{
    Node * temp = *a;
    *a = *b;
    *b = temp;
}

// two pointers to keep track of
// first and second nodes in a pair
Node **firstPtr;
Node **secondPtr;

// function to pairwise swap leaf
// nodes from left to right
void pairwiseSwap(Node **root, int &count)
{
    // if node is null, return
    if (!(*root))
        return;

    // if node is leaf node, increment count
    if(!(*root)->left&&!(*root)->right)
    {
        // initialize second pointer
        // by current node
        secondPtr  = root;

        // increment count
        count++;

        // if count is even, swap first
        // and second pointers
        if (count%2 == 0)
            Swap(firstPtr, secondPtr);

        else

            // if count is odd, initialize
            // first pointer by second pointer
            firstPtr  = secondPtr;
    }

    // if left child exists, check for leaf
    // recursively
    if ((*root)->left)
        pairwiseSwap(&(*root)->left, count);

    // if right child exists, check for leaf
    // recursively
    if ((*root)->right)
        pairwiseSwap(&(*root)->right, count);

}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// function to print inorder traversal
// of binary tree
void printInorder(Node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    printInorder(node->right);
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree shown in
    // above diagram
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(8);
    root->right->left->left = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->left = newNode(9);
    root->right->right->right = newNode(10);

    // print inorder traversal before swapping
    cout << "Inorder traversal before swap:\n";
    printInorder(root);
    cout << "\n";

    // variable to keep track
    // of leafs traversed
    int c = 0;

    // Pairwise swap of leaf nodes
    pairwiseSwap(&root, c);

    // print inorder traversal after swapping
    cout << "Inorder traversal after swap:\n";
    printInorder(root);
    cout << "\n";

    return 0;
}
```

输出:

```
Inorder traversal before swap:
4 2 1 6 5 7 3 9 8 10 
Inorder traversal after swap:
6 2 1 4 5 9 3 7 8 10 

```

**时间复杂度** : O( n)，其中 n 为二叉树中的节点数。
**辅助空间** : O( 1 )
本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。