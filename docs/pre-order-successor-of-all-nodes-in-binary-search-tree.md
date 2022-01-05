# 二叉查找树所有节点的预订单后续

> 原文:[https://www . geesforgeks . org/预排序-二进制搜索树中所有节点的后继节点/](https://www.geeksforgeeks.org/pre-order-successor-of-all-nodes-in-binary-search-tree/)

考虑一个不允许重复的[英国夏令时(二叉查找树)](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。
英国标准时间给了一把钥匙。任务是在这个 BST 中找到它的前序后继，也就是说，如果我们在给定的 BST 上应用一个前序遍历，任务是找到紧挨着给定键的一个键。

**示例:**
以相同的顺序在 BST 中插入以下键:51、39、31、54、92、42、21、10、26、52、36、47、82、5、62。
你会得到一个如下所示的英国标准时间:

![Binary Search Tree formed after inserting the given data.](https://scontent-bom1-1.xx.fbcdn.net/v/t1.15752-0/p280x280/67885387_470395753782451_1434413880230019072_n.png?_nc_cat=103&_nc_oc=AQmNUnoyOjoL1nfLSGSDY-frNi59GBa9lqnYUfCo_OqgLwEM1wGcJTArjCfc2Dei6KY&_nc_ht=scontent-bom1-1.xx&oh=2139f65facc399b958ae5d6fcc1e4b08&oe=5DD612BB)

*预排序遍历*:51 39 31 21 10 5 26 36 42 47 54 52 92 82 62

```
=====================================
Key       Pre-Order Successor
=====================================
51        39
39        31
31        21
21        10 
10        5
5         26
26        36
36        42
42        47
47        54
52        92
92        82
82        62
62        Do Not Exist. 
```

**简单方法:**解决这个问题的一个简单易行的方法是对给定的 BST 应用预序遍历，并将 BST 的键存储在一个数组中。接下来，在数组中搜索给定的键。如果它存在，那么它的下一个键(可能不一定存在)就是它的预排序后继键。如果给定的键不存在于数组中，这意味着给定的键不存在于 BST 中，因此该键不能有任何预先排序的后继键。
但是这个算法有一个时间复杂度 ***O(n)*** 。 ***O(n)*** 的空间复杂性，因此不是解决这个问题的好方法。

**有效方法**:解决这个问题的有效方法基于以下观察:

*   在 BST 中搜索包含给定关键字的节点。
    *   如果它不存在于 BST 中，则不能有任何此密钥的预订购后继者。
    *   如果它存在于 BST 中，那么这个密钥可以有一个预订购后继者。请注意，如果一个密钥存在，那么它没有必要有一个预先排序的后继密钥。这取决于给定键在 BST 中的位置
*   如果包含给定键的节点有一个左子节点，那么它的左子节点就是它的前序后继节点。
*   如果包含给定的节点有一个右子节点而不是左子节点，那么它的右子节点就是它的前序后继节点。
*   如果包含给定关键字的节点是叶子，那么你必须搜索它的最近的祖先，它有一个右子节点，并且这个祖先的关键字大于给定关键字，也就是说你必须在给定关键字存在的左子树中搜索它的最近的祖先。还有两种情况:
    *   这样一个祖先是存在的，如果是这样，那么这个祖先的正确的孩子是给定密钥的预先排序的后继者。
    *   这样的祖先不存在，如果存在，那么对于给定的密钥没有预先排序的后继者。

下面是上述方法的实现:

## C++

```
// C++ program to find pre-Order successor
// of a node in Binary Search Tree
#include <iostream>
using namespace std;

// Declare a structure
struct Node
{

    // Key to be stored in BST
    int key;

    // Pointer to left child
    struct Node *left;

    // Pointer to the right child
    struct Node *right;

    // Pointer to parent
    struct Node *parent;
};

// This function inserts node in BST
struct Node* insert(int key, struct Node *root,
                             struct Node *parent)
{

    // If root is NULL, insert key here
    if (!root)
    {

        // Allocate memory dynamically
        struct Node *node = (struct Node*)malloc(
                      sizeof(struct Node));

        // Validate malloc call
        if (node)
        {

            // Populate the object pointer to by
            // pointer named node
            node->key = key;
            node->left = node->right = NULL;
            node->parent = parent;

            // Return newly created node
            return node;
        }
        else

            // Malloc was not successful to satisfy
            // our request, given an appropriate
            // message to the user
            cout << "Could not allocate memory.";
    }

    // If this is a duplicate key then give
    // a message to user
    else if (key == root->key)
        cout <<"Duplicates are not allowed in BST.";

    // If the key to be inserted is greater than the
    // root's key then it will go to the right subtree of
    // the tree with current root
    else if (key > root->key)
        root->right = insert(key, root->right,root);

    // If the key to be inserted is smaller than the
    // root's key then it will go to a left subtree of
    // the tree with current root
    else
        root->left = insert(key, root->left, root);

    // Return the root
    return root;
}

// This function searched for a given key in BST
struct Node* search(int key, struct Node *root)
{

    // Since the root is empty and hence key
    // does not exist in BST
    if (!root)
        return NULL;

    // Current root contains the given key,
    // so return current root
    else if (key == root->key)
        return root;

    // Key is greater than the root's key and
    // therefore we will search for this key in
    // the right subtree of tree with root as
    // current root because of all of the keys
    // which are greater than the root's key
    // exist in the right subtree   
    else if (key > root->key)
        return search(key, root->right);

    // Key is smaller than the root's key and
    // therefore we will search for this key
    // in the left subtree of the tree with
    // root as the current root because of
    // all of the keys which are smaller
    // than the root's key exists in the
    // left subtree search tree in the left subtree
    else
        return search(key, root->left);
}

// This function returns the node that contains the
// pre-order successor for the given key
struct Node* preOrderSuccessor(int key, struct Node *root)
{

    // Search for a node in BST that contains
    // the given key
    struct Node *node = search(key, root);

    // There is no node in BST that contains
    // the given key, give an appropriate message to user
    if (!node)
    {
        cout << " do not exists in BST.\n" << key;
        return NULL;
    }

    // There exist a node in BST that contains
    // the given key Apply our observations
    if (node->left)

        // If left child of the node that contains the
        // given key exist then it is the pre-order
        // successor for the given key
        return node->left;

    else if (node->right)

        // If right but not left child of node that
        // contains the given key exist then it is
        // the pre-order successor for the given key
        return node->right;

    else
    {

        // Node containing the key has neither left
        // nor right child which means that it is
        // leaf node. In this case we will search
        // for its nearest ancestor with right
        // child which has a key greater than
        // the given key

        // Since node is a leaf node so its
        // parent is guaranteed to exist
        struct Node *temp = node->parent;

        // Search for nearest ancestor with right
        // child that has key greater than the given key
        while (temp)
        {
            if (key < temp->key && temp->right)
                break;

            temp = temp->parent;
        }

        // If such an ancestor exist then right child
        // of this ancestor is the pre-order successor
        // for the given otherwise there do not exist
        // any pre-order successor for the given key
        return temp ? temp->right : NULL;
    }
}

// This function traverse the BST in
// pre-order fashion
void preOrder(struct Node *root)
{
    if (root)
    {

        // First visit the root
        cout << " " << root->key;

        // Next visit its left subtree
        preOrder(root->left);

        // Finally visit its right subtree
        preOrder(root->right);
    }
}

// Driver code
int main()
{

    // Declares a root for our BST
    struct Node *ROOT = NULL;

    // We will create 15 random integers in
    // range 0-99 to populate our BST
    int a[] = { 51, 39, 31, 54, 92, 42, 21, 10,
                26, 52, 36, 47, 82, 5, 62 };

    int n = sizeof(a) / sizeof(a[0]);

    // Insert all elements into BST
    for(int i = 0 ; i < n; i++)
    {

        // Insert the generated number in BST
        cout << "Inserting " << a[i] << " ....." ;

        ROOT = insert(a[i], ROOT, NULL);
        cout << "Finished Insertion.\n";
    }

    // Apply pre-order traversal on BST
    cout << "\nPre-Order Traversal : ";
    preOrder(ROOT);

    // Display pre-order Successors for
    // all of the keys in BST
    cout <<"\n=====================================";
    cout <<"\n\n" << "Key" <<"   " << "Pre-Order Successor" << endl;
    cout <<"=====================================\n";

    // This stores the pre-order successor
    // for a given key
    struct Node *successor = NULL;

    // Iterate through all of the elements inserted
    // in BST to get their pre-order successor
    for(int i = 0 ; i < n; ++i)
    {

        // Get the pre-order successor for the given key
        successor = preOrderSuccessor(a[i], ROOT);

        if (successor)

            // Successor is not NULL and hence it contains
            // the pre-order successor for given key
            cout << "\n" << a[i] << "      "
                 << successor->key;
        else

            // Successor is NULL and hence given key do
            // not have a pre-order successor
            cout << " " << "Do Not Exist.\n" << a[i];
    }
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to find pre-Order successor
// of a node in Binary Search Tree
#include<stdio.h>
#include<stdlib.h>

// Declare a structure
struct Node{
    // Key to be stored in BST
    int key;

    // Pointer to left child
    struct Node *left;

    // Pointer to the right child
    struct Node *right;

    // Pointer to parent
    struct Node *parent;
};

// This function inserts node in BST
struct Node* insert(int key, struct Node *root,
                                   struct Node *parent)
{

    // If root is NULL, insert key here
    if(!root)
    {
        // Allocate memory dynamically
        struct Node *node = (struct Node*)malloc(sizeof(struct Node));

        // Validate malloc call
        if(node)
        {
            // Populate the object pointer to by
            // pointer named node
            node->key = key;
            node->left = node->right = NULL;
            node->parent = parent;

            // Return newly created node
            return node;

        }
        else
            // Malloc was not successful to satisfy our request,
            // given an appropriate message to the user
            printf("Could not allocate memory.");

    }

    // If this is a duplicate key then give a message to user
    else if(key == root->key)
        printf("Duplicates are not allowed in BST.");

    // If the key to be inserted is greater than the root's
    // key then it will go to the right subtree of
    // the tree with current root
    else if(key > root->key)
        root->right = insert(key, root->right,root);

    // If the key to be inserted is smaller than the
    // root's key then it will go to a left subtree of
    // the tree with current root
    else
        root->left = insert(key, root->left, root);

    // Return the root
    return root;
}

// This function searched for a given key in BST
struct Node* search(int key, struct Node *root)
{
    // Since the root is empty and hence key
    // does not exist in BST
    if(!root)
        return NULL;

    // Current root contains the given key,
    // so return current root
    else if( key == root->key)
        return root;

    // Key is greater than the root's key and therefore
    // we will search for this key in the right subtree of
    // tree with root as current root because of all of the keys
    // which are greater than the root's key exist in the right subtree   
    else if(key > root->key)
        return search(key, root->right);

    // Key is smaller than the root's key and therefore we will
    // search for this key in the left subtree of the tree with
    // root as the current root because of all of the keys which are
    // smaller than the root's key exists in the left subtree
    // search tree in the left subtree
    else
        return search(key, root->left);

}

// This function returns the node that contains the
// pre-order successor for the given key
struct Node* preOrderSuccessor(int key, struct Node *root){

    // Search for a node in BST that contains the given key
    struct Node *node = search(key, root);

    // There is no node in BST that contains the given key,
    // give an appropriate message to user
    if(!node){
        printf("%d do not exists in BST.\n", key);
        return NULL;
    }

    // There exist a node in BST that contains the given key
    // Apply our observations
    if(node->left)
        // If left child of the node that contains the
        // given key exist then it is the pre-order
        // successor for the given key
        return node->left;

    else if(node->right)
        // If right but not left child of node that contains
        // the given key exist then it is the pre-order
        // successor for the given key
        return node->right;

    else
    {
        // Node containing the key has neither left nor right child
        // which means that it is leaf node. In this case we will search
        // for its nearest ancestor with right child which has a key
        // greater than the given key

        // Since node is a leaf node so its parent is guaranteed to exist
        struct Node *temp = node->parent;

        // Search for nearest ancestor with right child that has
        // key greater than the given key
        while(temp){
            if(key < temp->key && temp->right)
                break;
            temp = temp->parent;
        }

        // If such an ancestor exist then right child of this ancestor
        // is the pre-order successor for the given otherwise there
        // do not exist any pre-order successor for the given key
        return temp ? temp->right : NULL;
    }
}

// This function traverse the BST in pre-order fashion
void preOrder(struct Node *root)
{
    if(root)
    {
        // First visit the root
        printf("%d ", root->key);

        // Next visit its left subtree
        preOrder(root->left);

        // Finally visit its right subtree
        preOrder(root->right);
    }
}

// Driver code
int main()
{
    // Declares a root for our BST
    struct Node *ROOT = NULL;

    // We will create 15 random integers in
    // range 0-99 to populate our BST
    int a[] = {51, 39, 31, 54, 92, 42, 21, 10,
                          26, 52, 36, 47, 82, 5, 62};

    int n = sizeof(a) / sizeof(a[0]);

    // Insert all elements into BST
    for(int i = 0 ; i < n; i++)
    {
        // Insert the generated number in BST
        printf("Inserting %2d.....", a[i]);

        ROOT = insert(a[i], ROOT, NULL);
        printf("Finished Insertion.\n");
    }

    // Apply pre-order traversal on BST
    printf("\nPre-Order Traversal : ");
    preOrder(ROOT);

    // Display pre-order Successors for all of the keys in BST
    printf("\n=====================================");
    printf("\n%-10s%s\n", "Key", "Pre-Order Successor");
    printf("=====================================\n");

    // This stores the pre-order successor for a given key
    struct Node *successor = NULL;

    // Iterate through all of the elements inserted
    // in BST to get their pre-order successor
    for(int i = 0 ; i < n; ++i)
    {
        // Get the pre-order successor for the given key
        successor = preOrderSuccessor(a[i], ROOT);

        if(successor)
            // Successor is not NULL and hence it contains
            // the pre-order successor for given key
            printf("%-10d%d\n", a[i], successor->key);
        else
            // Successor is NULL and hence given key do
            // not have a pre-order successor
            printf("%-10dDo Not Exist.\n", a[i]);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pre-Order successor
// of a node in Binary Search Tree
import java.util.*;

class GFG
{

// Declare a structure
static class Node
{
    // Key to be stored in BST
    int key;

    // Pointer to left child
    Node left;

    // Pointer to the right child
    Node right;

    // Pointer to parent
    Node parent;
};

// This function inserts node in BST
static Node insert(int key, Node root,
                            Node parent)
{

    // If root is null, insert key here
    if(root == null)
    {
        // Allocate memory dynamically
        Node node = new Node();

        // Validate malloc call
        if(node != null)
        {
            // Populate the object pointer to by
            // pointer named node
            node.key = key;
            node.left = node.right = null;
            node.parent = parent;

            // Return newly created node
            return node;

        }
        else

            // Malloc was not successful to
            // satisfy our request, given
            // an appropriate message to the user
            System.out.printf("Could not allocate memory.");
    }

    // If this is a duplicate key then
    // give a message to user
    else if(key == root.key)
        System.out.printf("Duplicates are not" +
                            " allowed in BST.");

    // If the key to be inserted is greater than
    // the root's key then it will go to the
    // right subtree of the tree with current root
    else if(key > root.key)
        root.right = insert(key, root.right, root);

    // If the key to be inserted is smaller than the
    // root's key then it will go to a left subtree
    // of the tree with current root
    else
        root.left = insert(key, root.left, root);

    // Return the root
    return root;
}

// This function searched for a given key in BST
static Node search(int key, Node root)
{
    // Since the root is empty and hence
    // key does not exist in BST
    if(root == null)
        return null;

    // Current root contains the given key,
    // so return current root
    else if( key == root.key)
        return root;

    // Key is greater than the root's key and 
    // therefore we will search for this key
    // in the right subtree of tree with root
    // as current root because of all of the keys
    // which are greater than the root's key
    // exist in the right subtree
    else if(key > root.key)
        return search(key, root.right);

    // Key is smaller than the root's key and
    // therefore we will search for this key
    // in the left subtree of the tree with root
    // as the current root because of all of the keys
    // which are smaller than the root's key exists in
    // the left subtree search tree in the left subtree
    else
        return search(key, root.left);
}

// This function returns the node
// that contains the pre-order successor
// for the given key
static Node preOrderSuccessor(int key,
                              Node root)
{

    // Search for a node in BST
    // that contains the given key
    Node node = search(key, root);

    // There is no node in BST
    // that contains the given key,
    // give an appropriate message to user
    if(node == null)
    {
        System.out.printf("%d do not exists" +
                           " in BST.\n", key);
        return null;
    }

    // There exist a node in BST that contains
    // the given key. Apply our observations
    if(node.left != null)

        // If left child of the node that
        // contains the given key exist
        // then it is the pre-order successor
        // for the given key
        return node.left;

    else if(node.right != null)

        // If right but not left child of node
        // that contains the given key exist 
        // then it is the pre-order successor
        // for the given key
        return node.right;

    else
    {
        // Node containing the key has neither left
        // nor right child which means that it is
        // leaf node. In this case we will search
        // for its nearest ancestor with right child
        // which has a key greater than the given key

        // Since node is a leaf node
        // so its parent is guaranteed to exist
        Node temp = node.parent;

        // Search for nearest ancestor with right child
        // that has key greater than the given key
        while(temp != null)
        {
            if(key < temp.key && temp.right != null)
                break;
            temp = temp.parent;
        }

        // If such an ancestor exist then right child
        // of this ancestor is the pre-order successor
        // for the given otherwise there do not exist
        // any pre-order successor for the given key
        return temp != null ? temp.right : null;
    }
}

// This function traverse the BST
// in pre-order fashion
static void preOrder(Node root)
{
    if(root != null)
    {
        // First visit the root
        System.out.printf("%d ", root.key);

        // Next visit its left subtree
        preOrder(root.left);

        // Finally visit its right subtree
        preOrder(root.right);
    }
}

// Driver code
public static void main(String args[])
{
    // Declares a root for our BST
    Node ROOT = null;

    // We will create 15 random integers in
    // range 0-99 to populate our BST
    int a[] = {51, 39, 31, 54, 92, 42, 21, 10,
                26, 52, 36, 47, 82, 5, 62};

    int n = a.length;

    // Insert all elements into BST
    for(int i = 0 ; i < n; i++)
    {
        // Insert the generated number in BST
        System.out.printf("Inserting %2d.....", a[i]);

        ROOT = insert(a[i], ROOT, null);
        System.out.printf("Finished Insertion.\n");
    }

    // Apply pre-order traversal on BST
    System.out.printf("\nPre-Order Traversal : ");
    preOrder(ROOT);

    // Display pre-order Successors
    // for all of the keys in BST
    System.out.printf("\n=====================================");
    System.out.printf("\n%-10s%s\n", "Key",
                    "Pre-Order Successor");
    System.out.printf("=====================================\n");

    // This stores the pre-order successor
    // for a given key
    Node successor = null;

    // Iterate through all of the elements inserted
    // in BST to get their pre-order successor
    for(int i = 0 ; i < n; ++i)
    {
        // Get the pre-order successor
        // for the given key
        successor = preOrderSuccessor(a[i], ROOT);

        if(successor != null)

            // Successor is not null and hence
            // it contains the pre-order
            // successor for given key
            System.out.printf("%-10d%d\n", a[i],
                                 successor.key);
        else
            // Successor is null and hence given key do
            // not have a pre-order successor
            System.out.printf("%-10dDo Not Exist.\n", a[i]);
    }
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find pre-Order successor
# of a node in Binary Search Tree

# Declare a structure
class Node:

    def __init__(self):

        # Key to be stored in BST
        self.key = 0

        # Pointer to left child
        self.left = None

        # Pointer to the right child
        self.right = None

        # Pointer to parent
        self.parent = None

# This function inserts node in BST
def insert(key: int, root: Node, parent: Node):

    # If root is None, insert key here
    if not root:

        # Allocate memory dynamically
        node = Node()

        # Validate malloc call
        if (node):

            # Populate the object pointer to by
            # pointer named node
            node.key = key
            node.left = node.right = None
            node.parent = parent

            # Return newly created node
            return node

        else:

            # Malloc was not successful to satisfy our request,
            # given an appropriate message to the user
            print("Could not allocate memory.")

    # If this is a duplicate key then give a message to user
    elif (key == root.key):
        print("Duplicates are not allowed in BST.")

    # If the key to be inserted is greater than the root's
    # key then it will go to the right subtree of
    # the tree with current root
    elif (key > root.key):
        root.right = insert(key, root.right, root)

    # If the key to be inserted is smaller than the
    # root's key then it will go to a left subtree of
    # the tree with current root
    else:
        root.left = insert(key, root.left, root)

    # Return the root
    return root

# This function searched for a given key in BST
def search(key: int, root: Node):

    # Since the root is empty and hence key
    # does not exist in BST
    if not root:
        return None

    # Current root contains the given key,
    # so return current root
    elif (key == root.key):
        return root

    # Key is greater than the root's key and therefore
    # we will search for this key in the right subtree
    # of tree with root as current root because of all
    # of the keys which are greater than the root's key
    # exist in the right subtree
    elif (key > root.key):
        return search(key, root.right)

    # Key is smaller than the root's key and therefore
    # we will search for this key in the left subtree
    # of the tree with root as the current root because
    # of all of the keys which are smaller than the
    # root's key exists in the left subtree search
    # tree in the left subtree
    else:
        return search(key, root.left)

# This function returns the node that contains the
# pre-order successor for the given key
def preOrderSuccessor(key: int, root: Node):

    # Search for a node in BST that
    # contains the given key
    node = search(key, root)

    # There is no node in BST that contains
    # the given key, give an appropriate
    # message to user
    if not node:
        print("%d do not exists in BST.\n" % key, end = "")
        return None

    # There exist a node in BST that contains the
    # given key. Apply our observations
    if (node.left):

        # If left child of the node that contains the
        # given key exist then it is the pre-order
        # successor for the given key
        return node.left

    elif (node.right):

        # If right but not left child of node that
        # contains the given key exist then it is
        # the pre-order successor for the given key
        return node.right

    else:

        # Node containing the key has neither left
        # nor right child which means that it is
        # leaf node. In this case we will search
        # for its nearest ancestor with right
        # child which has a key greater than
        # the given key

        # Since node is a leaf node so its parent
        # is guaranteed to exist
        temp = node.parent

        # Search for nearest ancestor with right
        # child that has key greater than the
        # given key
        while (temp):
            if (key < temp.key and temp.right):
                break

            temp = temp.parent

        # If such an ancestor exist then right child
        # of this ancestor is the pre-order successor
        # for the given otherwise there do not exist
        # any pre-order successor for the given key
        return temp.right if temp != None else None

# This function traverse the BST in
# pre-order fashion
def preOrder(root: Node):

    if (root):

        # First visit the root
        print("%d " % root.key, end = "")

        # Next visit its left subtree
        preOrder(root.left)

        # Finally visit its right subtree
        preOrder(root.right)

# Driver code
if __name__ == "__main__":

    # Declares a root for our BST
    ROOT = None

    # We will create 15 random integers in
    # range 0-99 to populate our BST
    a = [ 51, 39, 31, 54, 92, 42, 21,
          10, 26, 52, 36, 47, 82, 5, 62 ]

    n = len(a)

    # Insert all elements into BST
    for i in range(n):

        # Insert the generated number in BST
        print("Inserting %2d....." % a[i], end = "")

        ROOT = insert(a[i], ROOT, None)
        print("Finished Insertion.")

    # Apply pre-order traversal on BST
    print("\nPre-Order Traversal : ", end = "")
    preOrder(ROOT)

    # Display pre-order Successors for all of the keys in BST
    print("\n=====================================", end = "")
    print("\n%-10s%s\n" % ("Key", "Pre-Order Successor"), end = "")
    print("=====================================")

    # This stores the pre-order successor for a given key
    successor = None

    # Iterate through all of the elements inserted
    # in BST to get their pre-order successor
    for i in range(n):

        # Get the pre-order successor for the given key
        successor = preOrderSuccessor(a[i], ROOT)

        if (successor):

            # Successor is not None and hence it contains
            # the pre-order successor for given key
            print("%-10d%d" % (a[i], successor.key))
        else:

            # Successor is None and hence given key do
            # not have a pre-order successor
            print("%-10dDo Not Exist." % a[i])

# This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>
// Javascript program to find pre-Order successor
// of a node in Binary Search Tree

// Declare a structure
class Node
{
    constructor()
    {
        this.key=0;
        this.left=this.right=this.parent=null;
    }
}

// This function inserts node in BST
function insert(key,root,parent)
{
    // If root is null, insert key here
    if(root == null)
    {
        // Allocate memory dynamically
        let node = new Node();

        // Validate malloc call
        if(node != null)
        {
            // Populate the object pointer to by
            // pointer named node
            node.key = key;
            node.left = node.right = null;
            node.parent = parent;

            // Return newly created node
            return node;

        }
        else

            // Malloc was not successful to
            // satisfy our request, given
            // an appropriate message to the user
            document.write("Could not allocate memory.");
    }

    // If this is a duplicate key then
    // give a message to user
    else if(key == root.key)
        document.write("Duplicates are not" +
                            " allowed in BST.");

    // If the key to be inserted is greater than
    // the root's key then it will go to the
    // right subtree of the tree with current root
    else if(key > root.key)
        root.right = insert(key, root.right, root);

    // If the key to be inserted is smaller than the
    // root's key then it will go to a left subtree
    // of the tree with current root
    else
        root.left = insert(key, root.left, root);

    // Return the root
    return root;
}

// This function searched for a given key in BST
function search(key,root)
{
    // Since the root is empty and hence
    // key does not exist in BST
    if(root == null)
        return null;

    // Current root contains the given key,
    // so return current root
    else if( key == root.key)
        return root;

    // Key is greater than the root's key and
    // therefore we will search for this key
    // in the right subtree of tree with root
    // as current root because of all of the keys
    // which are greater than the root's key
    // exist in the right subtree
    else if(key > root.key)
        return search(key, root.right);

    // Key is smaller than the root's key and
    // therefore we will search for this key
    // in the left subtree of the tree with root
    // as the current root because of all of the keys
    // which are smaller than the root's key exists in
    // the left subtree search tree in the left subtree
    else
        return search(key, root.left);
}

// This function returns the node
// that contains the pre-order successor
// for the given key
function preOrderSuccessor(key,root)
{
    // Search for a node in BST
    // that contains the given key
    let node = search(key, root);

    // There is no node in BST
    // that contains the given key,
    // give an appropriate message to user
    if(node == null)
    {
        document.write(key + " do not exists" +
                           " in BST.<br>");
        return null;
    }

    // There exist a node in BST that contains
    // the given key. Apply our observations
    if(node.left != null)

        // If left child of the node that
        // contains the given key exist
        // then it is the pre-order successor
        // for the given key
        return node.left;

    else if(node.right != null)

        // If right but not left child of node
        // that contains the given key exist
        // then it is the pre-order successor
        // for the given key
        return node.right;

    else
    {
        // Node containing the key has neither left
        // nor right child which means that it is
        // leaf node. In this case we will search
        // for its nearest ancestor with right child
        // which has a key greater than the given key

        // Since node is a leaf node
        // so its parent is guaranteed to exist
        let temp = node.parent;

        // Search for nearest ancestor with right child
        // that has key greater than the given key
        while(temp != null)
        {
            if(key < temp.key && temp.right != null)
                break;
            temp = temp.parent;
        }

        // If such an ancestor exist then right child
        // of this ancestor is the pre-order successor
        // for the given otherwise there do not exist
        // any pre-order successor for the given key
        return temp != null ? temp.right : null;
    }
}

// This function traverse the BST
// in pre-order fashion
function preOrder(root)
{
    if(root != null)
    {
        // First visit the root
        document.write(root.key+" ");

        // Next visit its left subtree
        preOrder(root.left);

        // Finally visit its right subtree
        preOrder(root.right);
    }
}

// Driver code
// Declares a root for our BST
    let ROOT = null;

    // We will create 15 random integers in
    // range 0-99 to populate our BST
    let a = [51, 39, 31, 54, 92, 42, 21, 10,
                26, 52, 36, 47, 82, 5, 62];

    let n = a.length;

    // Insert all elements into BST
    for(let i = 0 ; i < n; i++)
    {
        // Insert the generated number in BST
        document.write("Inserting "+a[i]+".....");

        ROOT = insert(a[i], ROOT, null);
        document.write("Finished Insertion.<br>");
    }

    // Apply pre-order traversal on BST
    document.write("<br>Pre-Order Traversal : ");
    preOrder(ROOT);

    // Display pre-order Successors
    // for all of the keys in BST
    document.write("<br>=====================================<br>");
    document.write("Key"+"          " + "Pre-Order Successor<br>");
    document.write("=====================================<br>");

    // This stores the pre-order successor
    // for a given key
    let successor = null;

    // Iterate through all of the elements inserted
    // in BST to get their pre-order successor
    for(let i = 0 ; i < n; ++i)
    {
        // Get the pre-order successor
        // for the given key
        successor = preOrderSuccessor(a[i], ROOT);

        if(successor != null)

            // Successor is not null and hence
            // it contains the pre-order
            // successor for given key
            document.write(a[i]+"          " +successor.key+"<br>");
        else
            // Successor is null and hence given key do
            // not have a pre-order successor
            document.write(a[i]+ "           Do Not Exist.<br>");
    }

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Inserting 51.....Finished Insertion.
Inserting 39.....Finished Insertion.
Inserting 31.....Finished Insertion.
Inserting 54.....Finished Insertion.
Inserting 92.....Finished Insertion.
Inserting 42.....Finished Insertion.
Inserting 21.....Finished Insertion.
Inserting 10.....Finished Insertion.
Inserting 26.....Finished Insertion.
Inserting 52.....Finished Insertion.
Inserting 36.....Finished Insertion.
Inserting 47.....Finished Insertion.
Inserting 82.....Finished Insertion.
Inserting  5.....Finished Insertion.
Inserting 62.....Finished Insertion.

Pre-Order Traversal : 51 39 31 21 10 5 26 36 42 47 54 52 92 82 62 
=====================================
Key       Pre-Order Successor
=====================================
51        39
39        31
31        21
54        52
92        82
42        47
21        10
10        5
26        36
52        92
36        42
47        54
82        62
5         26
62        Do Not Exist.
```