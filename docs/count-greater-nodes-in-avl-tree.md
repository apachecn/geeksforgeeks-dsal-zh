# 计算 AVL 树中更大的节点

> 原文:[https://www . geesforgeks . org/count-greater-nodes-in-AVL-tree/](https://www.geeksforgeeks.org/count-greater-nodes-in-avl-tree/)

在本文中我们将看到如何计算 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)中大于给定值的元素个数。
例子:

```
Input : x = 5
        Root of below AVL tree
           9
          /  \
         1    10
        /  \     \
       0    5     11
      /    /  \
     -1   2    6
Output : 4

Explanation: there are 4 values which are 
greater than 5 in AVL tree which are 6, 9, 
10 and 11.

```

先决条件:

*   [插入 AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)
*   [AVL 树中的删除](https://www.geeksforgeeks.org/avl-tree-set-2-deletion/)

1.我们维护一个额外的字段“ **desc** ”，用于存储每个节点的后代节点数。像上面的例子一样，值为 5 的节点具有等于 2 的 desc 场值。

2.为了计算大于给定值的节点数，我们简单地遍历树。当遍历三个案例时-

**I Case-** x(给定值)大于当前节点的值。因此，我们转到当前节点的右子节点。
**案例二-** x 小于当前节点的值。我们通过当前节点的右子节点的后继数增加当前计数，然后再次将两个加到当前计数中(一个用于当前节点，一个用于右子节点。).在这一步中，首先，我们要确定正确的孩子是否存在。然后我们移动到当前节点的左子节点。
**III 情况-** x 等于当前节点的值。在这种情况下，我们将当前节点的右子节点的 **desc** 字段的值添加到当前计数中，然后再添加一个(用于计数右子节点)。同样在这种情况下，我们看到正确的孩子存在与否。

**计算 **desc** 场**的数值

1.  **插入**–当我们插入一个节点时，我们将新节点的每个预解码器的子字段递增 1。在左旋转和右旋转函数中，我们对节点的子字段值进行了适当的更改。
2.  **删除**–当我们删除一个节点时，我们从被删除节点的每个处理器节点中减少一个。同样，在左旋转和右旋转函数中，我们对节点的子字段的值进行了适当的更改。

```
// C program to find number of elements
// greater than a given value in AVL
#include <stdio.h>
#include <stdlib.h>
struct Node {
    int key;
    struct Node* left, *right;
    int height;
    int desc;
};

int height(struct Node* N)
{
    if (N == NULL)
        return 0;
    return N->height;
}

// A utility function to get maximum
// of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

struct Node* newNode(int key)
{
    struct Node* node = (struct Node*)
                    malloc(sizeof(struct Node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    node->height = 1; // initially added at leaf
    node->desc = 0;
    return (node);
}

// A utility function to right rotate subtree
// rooted with y
struct Node* rightRotate(struct Node* y)
{
    struct Node* x = y->left;
    struct Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // calculate the number of children of x and y
    // which are changed due to rotation.
    int val = (T2 != NULL) ? T2->desc : -1;
    y->desc = y->desc - (x->desc + 1) + (val + 1);
    x->desc = x->desc - (val + 1) + (y->desc + 1);

    return x;
}

// A utility function to left rotate subtree rooted
// with x
struct Node* leftRotate(struct Node* x)
{
    struct Node* y = x->right;
    struct Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // calculate the number of children of x and y
    // which are changed due to rotation.
    int val = (T2 != NULL) ? T2->desc : -1;
    x->desc = x->desc - (y->desc + 1) + (val + 1);
    y->desc = y->desc - (val + 1) + (x->desc + 1);

    return y;
}

// Get Balance factor of node N
int getBalance(struct Node* N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}

struct Node* insert(struct Node* node, int key)
{
    /* 1\. Perform the normal BST rotation */
    if (node == NULL)
        return (newNode(key));

    if (key < node->key) {
        node->left = insert(node->left, key);
        node->desc++;
    }

    else if (key > node->key) {
        node->right = insert(node->right, key);
        node->desc++;
    }

    else // Equal keys not allowed
        return node;

    /* 2\. Update height of this ancestor node */
    node->height = 1 + max(height(node->left),
                           height(node->right));

    /* 3\. Get the balance factor of this ancestor
        node to check whether this node became
        unbalanced */
    int balance = getBalance(node);

    // If node becomes unbalanced, 4 cases arise

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    /* return the (unchanged) node pointer */
    return node;
}

/* Given a non-empty binary search tree, return the
   node with minimum key value found in that tree.
   Note that the entire tree does not need to be
   searched. */
struct Node* minValueNode(struct Node* node)
{
    struct Node* current = node;

    /* loop down to find the leftmost leaf */
    while (current->left != NULL)
        current = current->left;

    return current;
}

// Recursive function to delete a node with given key
// from subtree with given root. It returns root of
// the modified subtree.
struct Node* deleteNode(struct Node* root, int key)
{
    // STEP 1: PERFORM STANDARD BST DELETE

    if (root == NULL)
        return root;

    // If the key to be deleted is smaller than the
    // root's key, then it lies in left subtree
    if (key < root->key) {
        root->left = deleteNode(root->left, key);
        root->desc = root->desc - 1;
    }

    // If the key to be deleted is greater than the
    // root's key, then it lies in right subtree
    else if (key > root->key) {
        root->right = deleteNode(root->right, key);
        root->desc = root->desc - 1;
    }

    // if key is same as root's key, then This is
    // the node to be deleted
    else {
        // node with only one child or no child
        if ((root->left == NULL) || (root->right == NULL)) {

            struct Node* temp = root->left ? 
                                root->left : root->right;

            // No child case
            if (temp == NULL) {
                temp = root;
                root = NULL;
                free(temp);

            } 
            else // One child case
            {
                *root = *temp; // Copy the contents of
                               // the non-empty child
                free(temp);
            }
        } else {
            // node with two children: Get the inorder
            // successor (smallest in the right subtree)
            struct Node* temp = minValueNode(root->right);

            // Copy the inorder successor's data to this node
            root->key = temp->key;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
            root->desc = root->desc - 1;
        }
    }

    // If the tree had only one node then return
    if (root == NULL)
        return root;

    // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
    root->height = 1 + max(height(root->left),
                           height(root->right));

    // STEP 3: GET THE BALANCE FACTOR OF THIS NODE (to
    // check whether this node became unbalanced)
    int balance = getBalance(root);

    // If this node becomes unbalanced, 4 cases arise

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

// A utility function to print preorder traversal of
// the tree.
void preOrder(struct Node* root)
{
    if (root != NULL) {
        printf("%d ", root->key);
        preOrder(root->left);
        preOrder(root->right);
    }
}

// Returns count of
int CountGreater(struct Node* root, int x)
{
    int res = 0;

    // Search for x. While searching, keep
    // updating res if x is greater than
    // current node.
    while (root != NULL) {

        int desc = (root->right != NULL) ? 
                   root->right->desc : -1;

        if (root->key > x) {
            res = res + desc + 1 + 1;
            root = root->left;
        } else if (root->key < x)
            root = root->right;
        else {
            res = res + desc + 1;
            break;
        }
    }
    return res;
}

/* Driver program to test above function*/
int main()
{
    struct Node* root = NULL;
    root = insert(root, 9);
    root = insert(root, 5);
    root = insert(root, 10);
    root = insert(root, 0);
    root = insert(root, 6);
    root = insert(root, 11);
    root = insert(root, -1);
    root = insert(root, 1);
    root = insert(root, 2);

    /* The constructed AVL Tree would be
          9
        /   \
        1   10
       / \     \
       0  5     11
      /  / \
    -1  2   6    */

    printf("Preorder traversal of the constructed AVL "
           "tree is \n");
    preOrder(root);
    printf("\nNumber of elements greater than 9 are %d",
           CountGreater(root, 9));

    root = deleteNode(root, 10);

    /* The AVL Tree after deletion of 10
         1
        / \
        0 9
       /  / \
     -1  5  11
        / \
        2  6 */

    printf("\nPreorder traversal after deletion of 10 \n");
    preOrder(root);
    printf("\nNumber of elements greater than 9 are %d",
           CountGreater(root, 9));
    return 0;
}
```

输出:

```
Preorder traversal of the constructed AVL tree is
9 1 0 -1 5 2 6 10 11
Number of elements greater than 9 are 2
Preorder traversal after deletion of 10
1 0 -1 9 5 2 6 11
Number of elements greater than 9 are 1

```

时间复杂度:count 的时间复杂度更大的函数是 O(log(n))，其中 n 是 avl 树中的节点数，因为我们基本上是在 avl 中搜索给定的需要 O(log(n))时间的数。

本文由 [**阿诗夏玛**](https://auth.geeksforgeeks.org/profile.php?user=ashish136) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。