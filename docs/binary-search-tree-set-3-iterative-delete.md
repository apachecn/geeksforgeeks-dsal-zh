# 二叉查找树|第 3 集(迭代删除)

> 原文:[https://www . geesforgeks . org/binary-search-tree-set-3-iterative-delete/](https://www.geeksforgeeks.org/binary-search-tree-set-3-iterative-delete/)

给定二叉查找树的一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)和一个**节点**，任务是从二叉查找树迭代器中删除该节点。
以下是在 BST 上执行删除操作时出现的三种情况:

**1。情况 1:** 要删除的节点是叶节点。直接从树中删除节点。

```

             10                             10
           /     \         delete(5)      /     \
          7       15       --------->    7       15 
         /  \    /  \                     \     /  \ 
        5    8  11   18                    8   11   18
```

**2。案例二:**待删除节点是有两个子节点的内部节点。复制要删除节点的上级后续节点的内容，删除上级后续节点。通过在节点的右子树中找到最小的元素，可以找到更高级的后继节点。
无后继者(10) = 11。

```
             10                              11
           /     \         delete(10)      /     \
          7       15       --------->    7        15 
         /  \    /  \                   /  \        \ 
        5    8  11   18                5    8        18
```

**3。案例三:**待删除节点是有一个子节点的内部节点。在这种情况下，删除该节点并将其子节点上移以取代它。

```
             10                              10
           /     \         delete(15)      /     \
          7       15       --------->    7       11 
         /  \    /                      /  \      
        5    8  11                     5    8
```

在情况 2 中删除有序后继节点背后的直觉是，具有两个子节点的节点的有序后继节点将总是大于该节点的左子树中的所有元素，因为它是该节点的右子树中的最小节点，并且该节点的有序后继节点将总是小于该节点的右子树中的所有其他节点。

这保留了给定节点的左子树中的所有节点都小于给定节点并且给定节点的右子树中的所有节点都大于给定节点的 BST 属性。

下面是上述方法的实现:

## C++

```
// C++ implementation to delete
// a node in the BST

#include <bits/stdc++.h>
using namespace std;

// Structure of the node
typedef struct treeNode {
    int data;
    struct treeNode* left;
    struct treeNode* right;
} treeNode;

// Utility function to print
// the inorder traversal of the BST.
void inorder(treeNode* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->data << ' ';
        inorder(root->right);
    }
}

// Utility function to insert
// nodes into our BST
treeNode* insert(treeNode* root, int key)
{
    // Check if tree is empty
    if (root == NULL) {
        treeNode* temp;
        temp = (treeNode*)malloc(sizeof(treeNode));
        temp->data = key;
        temp->left = NULL;
        temp->right = NULL;
        return temp;
    }
    if (key < root->data) {

        // if the key to be inserted
        // is lesser than the root,
        // insert into the left subtree,
        // and recursively call
        // the insert function with the
        // root->left as the new root.
        root->left = insert(root->left, key);
    }
    else {

        // if the key to be inserted
        // is greater than the root,
        // insert into the right subtree,
        // and recursively call
        // the insert function with the
        // root->right as the new root.
        root->right = insert(root->right, key);
    }
    return root;
}

// Iterative Function to delete
// 'key' from the BST.
treeNode* deleteIterative(treeNode* root, int key)
{
    treeNode* curr = root;
    treeNode* prev = NULL;

    // Check if the key is actually
    // present in the BST.
    // the variable prev points to
    // the parent of the key to be deleted.
    while (curr != NULL && curr->data != key) {
        prev = curr;
        if (key < curr->data)
            curr = curr->left;
        else
            curr = curr->right;
    }

    if (curr == NULL) {
        cout << "Key " << key << " not found in the"
             << " provided BST.\n";
        return root;
    }

    // Check if the node to be
    // deleted has atmost one child.
    if (curr->left == NULL || curr->right == NULL) {

        // newCurr will replace
        // the node to be deleted.
        treeNode* newCurr;

        // if the left child does not exist.
        if (curr->left == NULL)
            newCurr = curr->right;
        else
            newCurr = curr->left;

        // check if the node to
        // be deleted is the root.
        if (prev == NULL)
            return newCurr;

        // check if the node to be deleted
        // is prev's left or right child
        // and then replace this with newCurr
        if (curr == prev->left)
            prev->left = newCurr;
        else
            prev->right = newCurr;

        // free memory of the
        // node to be deleted.
        free(curr);
    }

    // node to be deleted has
    // two children.
    else {
        treeNode* p = NULL;
        treeNode* temp;

        // Compute the inorder successor
        temp = curr->right;
        while (temp->left != NULL) {
            p = temp;
            temp = temp->left;
        }

        // check if the parent of the inorder
        // successor is the curr or not(i.e. curr=
        // the node which has the same data as
        // the given data by the user to be
        // deleted). if it isn't, then make the
        // the left child of its parent equal to
        // the inorder successor'd right child.
        if (p != NULL)
            p->left = temp->right;

        // if the inorder successor was the
        // curr (i.e. curr = the node which has the
        // same data as the given data by the
        // user to be deleted), then make the
        // right child of the node to be
        // deleted equal to the right child of
        // the inorder successor.
        else
            curr->right = temp->right;

        curr->data = temp->data;
        free(temp);
    }
    return root;
}

// Driver Code
int main()
{
    /*
         10
        /  \
       7    15
      / \   / \
      5  8 11 18

    */
    treeNode* root = NULL;
    root = insert(root, 10);
    root = insert(root, 7);
    root = insert(root, 5);
    root = insert(root, 8);
    root = insert(root, 15);
    root = insert(root, 11);
    root = insert(root, 18);

    cout << "Inorder traversal "
         << "of original BST:\n";
    inorder(root);
    cout << '\n';

    // delete node with data value 11 (leaf)
    root = deleteIterative(root, 11);
    cout << "\nDeletion of 11\n";
    cout << "Inorder traversal post deletion:\n";
    inorder(root);
    cout << '\n';

    // delete node with data value 15
    // (internal node with one child)
    root = deleteIterative(root, 15);
    cout << "\nDeletion of 15\n";
    cout << "Inorder traversal post deletion:\n";
    inorder(root);
    cout << '\n';

    // delete node with data value 10
    // (root, two children)
    root = deleteIterative(root, 10);
    cout << "\nDeletion of 10\n";
    cout << "Inorder traversal post deletion:\n";
    inorder(root);
    cout << '\n';

    return 0;
}
```

## 蟒蛇 3

```
# Python implementation to delete
# a node in the Binary Search Tree

# Class for a node of BST.

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function to print
# the inorder traversal of the BST

def inorder(root):
    if root != None:
        inorder(root.left)
        print(root.data, end=" ")
        inorder(root.right)

# Utility function to insert
# nodes into our BST

def insert(root, key):
    # check if tree is empty
    if root == None:
        temp = Node(key)
        return temp

    if key < root.data:

        """
        if the key to be inserted is
        lesser than the root,
        insert into the left subtree,
        and recursively call
        the insert function with
        the root.left as the new root.
        """
        root.left = insert(root.left, key)

    else:
        """
        if the key to be inserted is
        greater than the root,
        insert into the right subtree,
        and recursively call
        the insert function with the
        root->right as the new root.
        """
        root.right = insert(root.right, key)

    return root

# Iterative approach to
# delete 'key' from the BST.

def deleteIterative(root, key):
    curr = root
    prev = None

    # First check if the key is
    # actually present in the BST.
    # the variable prev points to the
    # parent of the key to be deleted
    while(curr != None and curr.data != key):
        prev = curr
        if curr.data < key:
            curr = curr.right
        else:
            curr = curr.left

    if curr == None:
        print("Key % d not found in\
           the provided BST." % key)
        return root

    # Check if the node to be
    # deleted has atmost one child
    if curr.left == None or\
            curr.right == None:

        # newCurr will replace
        # the node to be deleted.
        newCurr = None

        # if the left child does not exist.
        if curr.left == None:
            newCurr = curr.right
        else:
            newCurr = curr.left

        # check if the node to
        # be deleted is the root.
        if prev == None:
            return newCurr

        # Check if the node to be
        # deleted is prev's left or
        # right child and then
        # replace this with newCurr
        if curr == prev.left:
            prev.left = newCurr
        else:
            prev.right = newCurr

        curr = None

    # node to be deleted
    # has two children.
    else:
        p = None
        temp = None

        # Compute the inorder
        # successor of curr.
        temp = curr.right
        while(temp.left != None):
            p = temp
            temp = temp.left

        # check if the parent of the
        # inorder successor is the root or not.
        # if it isn't, then make the left
        # child of its parent equal to the
        # inorder successor's right child.
        if p != None:
            p.left = temp.right

        else:

            # if the inorder successor was
            # the root, then make the right child
            # of the node to be deleted equal
            # to the right child of the inorder
            # successor.
            curr.right = temp.right

        curr.data = temp.data
        temp = None

    return root

# Function to create the BST
# and call the Delete Function

def main():
    """
         10        
        /   \        
       7     15    
      / \   / \    
      5 8  11 18    
    """
    root = None
    root = insert(root, 10)
    root = insert(root, 7)
    root = insert(root, 5)
    root = insert(root, 8)
    root = insert(root, 15)
    root = insert(root, 11)
    root = insert(root, 18)

    print("Inorder traversal of original BST:")
    inorder(root)
    print("\n")

    # delete node with data value 11 (leaf)
    root = deleteIterative(root, 11)
    print("Deletion of 11")
    print("Inorder traversal post deletion:")
    inorder(root)
    print("\n")

    # delete node with data value 15
    # (internal node with one child)
    root = deleteIterative(root, 15)
    print("Deletion of 15")
    print("Inorder traversal post deletion:")
    inorder(root)
    print("\n")

    # delete node with data value 10
    # (root, two children)
    root = deleteIterative(root, 10)
    print("Deletion of 10")
    print("Inorder traversal post deletion:")
    inorder(root)
    print()

# Driver Code
if __name__ == "__main__":
    main()
```

**Output:** 

```
Inorder traversal of original BST:
5 7 8 10 11 15 18 

Deletion of 11
Inorder traversal post deletion:
5 7 8 10 15 18 

Deletion of 15
Inorder traversal post deletion:
5 7 8 10 18 

Deletion of 10
Inorder traversal post deletion:
5 7 8 18
```