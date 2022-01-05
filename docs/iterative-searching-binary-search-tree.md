# 二叉查找树迭代搜索

> 原文:[https://www . geesforgeks . org/iterative-search-binary-search-tree/](https://www.geeksforgeeks.org/iterative-searching-binary-search-tree/)

给了二叉查找树和一把钥匙。检查给定的键是否存在于 BST 中，如果存在，则不进行递归。

递归搜索请参考[二叉查找树插入](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。

## C++

```
// C++ program to demonstrate searching operation
// in binary search tree without recursion
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node *left, *right;
};

// Function to check the given key exist or not
bool iterativeSearch(struct Node* root, int key)
{
    // Traverse until root reaches to dead end
    while (root != NULL) {
        // pass right subtree as new tree
        if (key > root->data)
            root = root->right;

        // pass left subtree as new tree
        else if (key < root->data)
            root = root->left;
        else
            return true; // if the key is found return 1
    }
    return false;
}

// A utility function to create a new BST Node
struct Node* newNode(int item)
{
    struct Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* A utility function to insert a new Node with
   given key in BST */
struct Node* insert(struct Node* Node, int data)
{
    /* If the tree is empty, return a new Node */
    if (Node == NULL)
        return newNode(data);

    /* Otherwise, recur down the tree */
    if (data < Node->data)
        Node->left = insert(Node->left, data);
    else if (data > Node->data)
        Node->right = insert(Node->right, data);

    /* return the (unchanged) Node pointer */
    return Node;
}

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
              50
            /    \
          30      70
         /  \    /  \
       20   40  60   80 */
    struct Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);
    if (iterativeSearch(root, 15))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate searching operation
// in binary search tree without recursion
import java.util.*;

class GFG {

    static class Node {
        int data;
        Node left, right;
    };

    // Function to check the given key exist or not
    static boolean iterativeSearch(Node root, int key)
    {
        // Traverse until root reaches to dead end
        while (root != null) {
            // pass right subtree as new tree
            if (key > root.data)
                root = root.right;

            // pass left subtree as new tree
            else if (key < root.data)
                root = root.left;
            else
                return true; // if the key is found return 1
        }
        return false;
    }

    // A utility function to create a new BST Node
    static Node newNode(int item)
    {
        Node temp = new Node();
        temp.data = item;
        temp.left = temp.right = null;
        return temp;
    }

    /* A utility function to insert a new Node with
given key in BST */
    static Node insert(Node Node, int data)
    {
        /* If the tree is empty, return a new Node */
        if (Node == null)
            return newNode(data);

        /* Otherwise, recur down the tree */
        if (data < Node.data)
            Node.left = insert(Node.left, data);
        else if (data > Node.data)
            Node.right = insert(Node.right, data);

        /* return the (unchanged) Node pointer */
        return Node;
    }

    // Driver code
    public static void main(String args[])
    {
        /* Let us create following BST
            50
            / \
        30 70
        / \ / \
    20 40 60 80 */
        Node root = null;
        root = insert(root, 50);
        insert(root, 30);
        insert(root, 20);
        insert(root, 40);
        insert(root, 70);
        insert(root, 60);
        insert(root, 80);
        if (iterativeSearch(root, 15))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to demonstrate searching operation
# in binary search tree without recursion
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to check the given
# key exist or not
def iterativeSearch(root, key):

    # Traverse until root reaches
    # to dead end
    while root != None:

        # pass right subtree as new tree
        if key > root.data:
            root = root.right

        # pass left subtree as new tree
        elif key < root.data:
            root = root.left
        else:
            return True # if the key is found return 1
    return False

# A utility function to insert a
# new Node with given key in BST
def insert(Node, data):

    # If the tree is empty, return
    # a new Node
    if Node == None:
        return newNode(data)

    # Otherwise, recur down the tree
    if data < Node.data:
        Node.left = insert(Node.left, data)
    elif data > Node.data:
        Node.right = insert(Node.right, data)

    # return the (unchanged) Node pointer
    return Node

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    # 50
    # 30     70
    # / \ / \
    # 20 40 60 80
    root = None
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)
    if iterativeSearch(root, 15):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
// C# program to demonstrate searching operation
// in binary search tree without recursion
using System;

class GFG {

    public class Node {
        public int data;
        public Node left, right;
    };

    // Function to check the given key exist or not
    static bool iterativeSearch(Node root, int key)
    {
        // Traverse until root reaches to dead end
        while (root != null) {
            // pass right subtree as new tree
            if (key > root.data)
                root = root.right;

            // pass left subtree as new tree
            else if (key < root.data)
                root = root.left;
            else
                return true; // if the key is found return 1
        }
        return false;
    }

    // A utility function to create a new BST Node
    static Node newNode(int item)
    {
        Node temp = new Node();
        temp.data = item;
        temp.left = temp.right = null;
        return temp;
    }

    /* A utility function to insert a new Node with
given key in BST */
    static Node insert(Node Node, int data)
    {
        /* If the tree is empty, return a new Node */
        if (Node == null)
            return newNode(data);

        /* Otherwise, recur down the tree */
        if (data < Node.data)
            Node.left = insert(Node.left, data);
        else if (data > Node.data)
            Node.right = insert(Node.right, data);

        /* return the (unchanged) Node pointer */
        return Node;
    }

    // Driver code
    public static void Main(String[] args)
    {
        /* Let us create following BST
            50
            / \
        30 70
        / \ / \
    20 40 60 80 */
        Node root = null;
        root = insert(root, 50);
        insert(root, 30);
        insert(root, 20);
        insert(root, 40);
        insert(root, 70);
        insert(root, 60);
        insert(root, 80);
        if (iterativeSearch(root, 15))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to
// demonstrate searching operation
// in binary search tree without recursion

class Node {
    constructor() {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

    // Function to check the given key exist or not
    function iterativeSearch(root , key)
    {
        // Traverse until root reaches to dead end
        while (root != null) {
            // pass right subtree as new tree
            if (key > root.data)
                root = root.right;

            // pass left subtree as new tree
            else if (key < root.data)
                root = root.left;
            else
            // if the key is found return 1
                return true;
        }
        return false;
    }

    // A utility function to create a new BST Node
    function newNode(item)
    {
        var temp = new Node();
        temp.data = item;
        temp.left = temp.right = null;
        return temp;
    }

    /* A utility function to insert a new Node with
given key in BST */
    function insert(Node , data)
    {
        /* If the tree is empty, return a new Node */
        if (Node== null)
            return newNode(data);

        /* Otherwise, recur down the tree */
        if (data < Node.data)
            Node.left = insert(Node.left, data);
        else if (data > Node.data)
            Node.right = insert(Node.right, data);

        /* return the (unchanged) Node pointer */
        return Node;
    }

    // Driver code

        /* Let us create following BST
            50
            / \
        30 70
        / \ / \
    20 40 60 80 */
        var root = null;
        root = insert(root, 50);
        insert(root, 30);
        insert(root, 20);
        insert(root, 40);
        insert(root, 70);
        insert(root, 60);
        insert(root, 80);
        if (iterativeSearch(root, 15))
            document.write("YES");
        else
            document.write("NO");

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
No
```