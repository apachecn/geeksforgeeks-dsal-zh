# BST 中第二大元素

> 原文:[https://www . geesforgeks . org/二进制搜索树中第二大元素-bst/](https://www.geeksforgeeks.org/second-largest-element-in-binary-search-tree-bst/)

给定一个二叉查找树，找到第二大元素。
**例:**

```
Input: Root of below BST
    10
   /
  5

Output:  5

Input: Root of below BST
        10
      /   \
    5      20
             \ 
              30 

Output:  20
```

来源:[微软采访](https://www.geeksforgeeks.org/microsoft-interview-experience-set-53/)

想法类似于下面的帖子。
[不允许修改 BST 时 BST 中的第 K 个最大元素](https://www.geeksforgeeks.org/kth-largest-element-in-bst-when-modification-to-bst-is-not-allowed/)
第二大元素是有序遍历中的倒数第二个元素，反向有序遍历中的第二个元素。我们以相反的顺序遍历给定的二叉查找树，并记录访问的节点数。一旦计数变成 2，我们就打印节点。
下面是上面想法的实现。

## C++

```
// C++ program to find 2nd largest element in BST
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int key;
    Node *left, *right;
};

// A utility function to create a new BST node
Node *newNode(int item)
{
    Node *temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A function to find 2nd largest element in a given tree.
void secondLargestUtil(Node *root, int &c)
{
    // Base cases, the second condition is important to
    // avoid unnecessary recursive calls
    if (root == NULL || c >= 2)
        return;

    // Follow reverse inorder traversal so that the
    // largest element is visited first
    secondLargestUtil(root->right, c);

    // Increment count of visited nodes
    c++;

    // If c becomes k now, then this is the 2nd largest
    if (c == 2)
    {
        cout << "2nd largest element is "
             << root->key << endl;
        return;
    }

    // Recur for left subtree
    secondLargestUtil(root->left, c);
}

// Function to find 2nd largest element
void secondLargest(Node *root)
{
    // Initialize count of nodes visited as 0
    int c = 0;

    // Note that c is passed by reference
    secondLargestUtil(root, c);
}

/* A utility function to insert a new node with given key in BST */
Node* insert(Node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left  = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    Node *root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    secondLargest(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find second largest element in BST

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinarySearchTree {

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree()
    {
        root = null;
    }

    // function to insert new nodes
    public void insert(int data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node with given
    key in BST */
    Node insertRec(Node node, int data)
    {
        /* If the tree is empty, return a new node */
        if (node == null) {
            this.root = new Node(data);
            return this.root;
        }

        /* Otherwise, recur down the tree */
        if (data < node.data) {
            node.left = this.insertRec(node.left, data);
        } else {
            node.right = this.insertRec(node.right, data);
        }
        return node;
    }

    // class that stores the value of count
    public class count {
        int c = 0;
    }

    // Function to find 2nd largest element
    void secondLargestUtil(Node node, count C)
    {  
        // Base cases, the second condition is important to
        // avoid unnecessary recursive calls
        if (node == null || C.c >= 2)
            return;

        // Follow reverse inorder traversal so that the
        // largest element is visited first
        this.secondLargestUtil(node.right, C);

         // Increment count of visited nodes
        C.c++;

        // If c becomes k now, then this is the 2nd largest
        if (C.c == 2) {
            System.out.print("2nd largest element is "+
                                              node.data);
            return;
        }

         // Recur for left subtree
        this.secondLargestUtil(node.left, C);
    }

    // Function to find 2nd largest element
    void secondLargest(Node node)
    {  
        // object of class count
        count C = new count();
        this.secondLargestUtil(this.root, C);
    }

    // Driver function
    public static void main(String[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        tree.secondLargest(tree.root);
    }
}

// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 code to find second largest
# element in BST
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# A function to find 2nd largest
# element in a given tree.
def secondLargestUtil(root, c):

    # Base cases, the second condition
    # is important to avoid unnecessary
    # recursive calls
    if root == None or c[0] >= 2:
        return

    # Follow reverse inorder traversal so that
    # the largest element is visited first
    secondLargestUtil(root.right, c)

    # Increment count of visited nodes
    c[0] += 1

    # If c becomes k now, then this is
    # the 2nd largest
    if c[0] == 2:
        print("2nd largest element is",
                              root.key)
        return

    # Recur for left subtree
    secondLargestUtil(root.left, c)

# Function to find 2nd largest element
def secondLargest(root):

    # Initialize count of nodes
    # visited as 0
    c = [0]

    # Note that c is passed by reference
    secondLargestUtil(root, c)

# A utility function to insert a new
# node with given key in BST
def insert(node, key):

    # If the tree is empty, return a new node
    if node == None:
        return Node(key)

    # Otherwise, recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
    elif key > node.key:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer
    return node

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    #         50
    #     /     \
    #     30     70
    #     / \ / \
    # 20 40 60 80
    root = None
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)

    secondLargest(root)

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# code to find second largest element in BST

// A binary tree node
public class Node
{

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinarySearchTree
{

    // Root of BST
    public Node root;

    // Constructor
  public BinarySearchTree()
    {
        root = null;
    }

    // function to insert new nodes
    public virtual void insert(int data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node with given 
    key in BST */
    public virtual Node insertRec(Node node, int data)
    {
        /* If the tree is empty, return a new node */
        if (node == null)
        {
            this.root = new Node(data);
            return this.root;
        }

        /* Otherwise, recur down the tree */
        if (data < node.data)
        {
            node.left = this.insertRec(node.left, data);
        }
        else
        {
            node.right = this.insertRec(node.right, data);
        }
        return node;
    }

    // class that stores the value of count
    public class count
    {
        private readonly BinarySearchTree outerInstance;

        public count(BinarySearchTree outerInstance)
        {
            this.outerInstance = outerInstance;
        }

        public int c = 0;
    }

    // Function to find 2nd largest element
    public virtual void secondLargestUtil(Node node, count C)
    {
        // Base cases, the second condition is important to
        // avoid unnecessary recursive calls
        if (node == null || C.c >= 2)
        {
            return;
        }

        // Follow reverse inorder traversal so that the
        // largest element is visited first
        this.secondLargestUtil(node.right, C);

         // Increment count of visited nodes
        C.c++;

        // If c becomes k now, then this is the 2nd largest
        if (C.c == 2)
        {
            Console.Write("2nd largest element is " + node.data);
            return;
        }

         // Recur for left subtree
        this.secondLargestUtil(node.left, C);
    }

    // Function to find 2nd largest element
    public virtual void secondLargest(Node node)
    {
        // object of class count
        count C = new count(this);
        this.secondLargestUtil(this.root, C);
    }

    // Driver function
    public static void Main(string[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        tree.secondLargest(tree.root);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript code to find second largest
// element in BST

// A binary tree node
class Node {
    constructor(d)
    {
        this.data = d;
        this.left = this.right = null;
    }
}

    // Root of BST
    var root = null;

    // function to insert new nodes
     function insert(data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a
    new node with given key in BST */
    function insertRec(node , data)
    {
        /* If the tree is empty, return a new node */
        if (node == null) {
            this.root = new Node(data);
            return this.root;
        }

        /* Otherwise, recur down the tree */
        if (data < node.data) {
            node.left = this.insertRec(node.left, data);
        } else {
            node.right = this.insertRec(node.right, data);
        }
        return node;
    }

    // class that stores the value of count
     class count {
     constructor(){
        this.c = 0;
        }
    }

    // Function to find 2nd largest element
    function secondLargestUtil(node,  C)
    {  
        // Base cases, the second condition is important to
        // avoid unnecessary recursive calls
        if (node == null || C.c >= 2)
            return;

        // Follow reverse inorder traversal so that the
        // largest element is visited first
        this.secondLargestUtil(node.right, C);

         // Increment count of visited nodes
        C.c++;

        // If c becomes k now, then this is the 2nd largest
        if (C.c == 2) {
            document.write("2nd largest element is "+
                                              node.data);
            return;
        }

         // Recur for left subtree
        this.secondLargestUtil(node.left, C);
    }

    // Function to find 2nd largest element
    function secondLargest(node)
    {  
        // object of class count
        var C = new count();
        this.secondLargestUtil(this.root, C);
    }

    // Driver function

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */

        insert(50);
        insert(30);
        insert(20);
        insert(40);
        insert(70);
        insert(60);
        insert(80);

        secondLargest(root);

// This code contributed by aashish1995

</script>
```

**输出:**

```
2nd largest element is 70
```

上述解的时间复杂度为 O(h)，其中 h 为 BST 的高度。

本文由**拉维**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息