# 从二叉树中移除 K 的所有倍数

> 原文:[https://www . geesforgeks . org/从二叉树中移除 k 的所有倍数/](https://www.geeksforgeeks.org/remove-all-multiples-of-k-from-binary-tree/)

给定一棵二叉树和一个整数 **K** ，任务是从给定的二叉树中移除所有为 **K** 倍数的节点。

**示例:**

```
Input:
           1
         /    \
        2      3
       / \    /
      4   5  8
     / \    /
    6   7  9
Output:
Level Order Traversal of Given Binary Tree:
1 
2 3 
4 5 8 
6 7 9 

Level Order Traversal of Updated Binary Tree:
1 
5 3 
7 9

```

**进场:**

1.  将给定的[二叉树转换为双链表](https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)。
2.  从创建的双向链表中删除所有为 **K** 倍数的节点。
3.  将更新后的双向链表转换回二叉树。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

struct node {
    int data;
    node *left, *right;
};

node* newnode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Level order traversal of the tree
void printTree(node* root)
{

    if (!root)
        return;

    queue<node*> q;
    q.push(root);

    while (!q.empty()) {

        int n = q.size();
        while (n--) {
            node* temp = q.front();
            q.pop();

            cout << temp->data << " ";

            if (temp->left)
                q.push(temp->left);

            if (temp->right)
                q.push(temp->right);
        }
        cout << endl;
    }
}

// Function to convert binary tree
// to doubly linked list
void BT2DLL(node* root, node*& head)
{
    // Base Case
    if (root == NULL)
        return;

    static node* left = NULL;

    // Traverse the left subtree
    BT2DLL(root->left, head);

    // Assign head to leftmost node
    if (left == NULL)
        head = root;

    else {
        root->left = left;
        left->right = root;
    }

    left = root;

    // Traverse the right subtree
    BT2DLL(root->right, head);
}

// Function to delete the current node
// from the doubly linked list
void deletenode(node*& head, node* del)
{
    // Base case
    if (head == NULL || del == NULL)
        return;

    // If node to be deleted is head node
    if (head == del)
        head = del->right;

    // Change right only if node to be deleted
    // is NOT the last node
    if (del->right != NULL)
        del->right->left = del->left;

    // Change left only if node to be deleted
    // is NOT the first node
    if (del->left != NULL)
        del->left->right = del->right;

    // Finally, free the memory occupied by del
    free(del);
}

// Function to remove the multiples of k
// from doubly linked list
void removeKeys(node*& head, int k)
{

    if (head == NULL)
        return;

    node* current = head;
    node* right;

    while (current != NULL) {

        // If multiple of k then remove this node
        if (current->data % k == 0) {

            // Save current's right node in the
            // pointer 'right'
            right = current->right;

            // Delete the node pointed to by
            // 'current'
            deletenode(head, current);

            // Update current
            current = right;
        }

        // Else simply move to the right node
        else
            current = current->right;
    }
}

// Function to convert doubly linked list
// to binary tree
node* DLLtoBT(node*& head, int n)
{

    if (n <= 0)
        return NULL;

    node* left = DLLtoBT(head, n / 2);
    node* root = head;
    root->left = left;
    head = head->right;
    root->right = DLLtoBT(head, n - n / 2 - 1);

    return root;
}

// Function that removes the multiples
// of k from the given binary tree
node* removeMultiplesUtil(node* root, int k)
{

    node* head = NULL;

    // Convert Binary Tree to DLL
    BT2DLL(root, head);

    // Remove multiples of k from DLL
    removeKeys(head, k);

    node* temp = head;
    int n = 0;

    // Get Size of the updated list
    while (temp) {
        ++n;
        temp = temp->right;
    }

    // Convert DLL to Binary Tree
    return DLLtoBT(head, n);
}

// Function to call the utility function
// that removes the multiples of k
// from the given binary tree
void removeMultiples(node*& root, int k)
{

    if (!root)
        return;

    root = removeMultiplesUtil(root, k);
}

// Driver code
int main()
{

    int k = 2;
    node* root = newnode(1);
    root->left = newnode(2);
    root->right = newnode(3);
    root->left->left = newnode(4);
    root->left->right = newnode(5);
    root->left->left->left = newnode(6);
    root->left->left->right = newnode(7);
    root->right->left = newnode(8);
    root->right->left->left = newnode(9);

    cout << "Level Order Traversal of Given Binary Tree:\n";
    printTree(root);

    removeMultiples(root, k);

    cout << "\nLevel Order Traversal of Updated Binary Tree:\n";
    printTree(root);

    return 0;
}
```

**Output:**

```
Level Order Traversal of Given Binary Tree:
1 
2 3 
4 5 8 
6 7 9 

Level Order Traversal of Updated Binary Tree:
1 
5 3 
7 9

```