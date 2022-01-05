# 不允许修改 BST 时 BST 中的第 K 大元素

> 原文:[https://www . geesforgeks . org/kth-当不允许修改为 bst 时-bst 中的最大元素/](https://www.geeksforgeeks.org/kth-largest-element-in-bst-when-modification-to-bst-is-not-allowed/)

给定一个二叉查找树和一个正整数 k，求二叉查找树中第 k 大的元素。
比如下面的 BST，如果 k = 3，那么输出应该是 14，如果 k = 5，那么输出应该是 10。

![](img/f3de33cd4ef95a6fd382c7c28efff4f0.png)

我们在这个帖子里讨论了两种方法。方法 1 需要 O(n)个时间。方法 2 需要 O(h)时间，其中 h 是 BST 的高度，但是需要增加 BST(用每个节点存储左子树中的节点数)。
我们能在优于 0(n)的时间内找到第 k 大元素而不增加吗？

**进场:**

1.  这个想法是反向遍历 BST。记录访问的节点数。
2.  反向有序遍历以递减顺序遍历所有节点，即先访问右边的节点，然后居中再向左，并继续递归遍历节点。
3.  遍历时，记录到目前为止访问的节点数。
4.  当计数等于 k 时，停止遍历并打印密钥。

## C++

```
// C++ program to find k'th largest element in BST
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

// A function to find k'th largest element in a given tree.
void kthLargestUtil(Node *root, int k, int &c)
{
    // Base cases, the second condition is important to
    // avoid unnecessary recursive calls
    if (root == NULL || c >= k)
        return;

    // Follow reverse inorder traversal so that the
    // largest element is visited first
    kthLargestUtil(root->right, k, c);

    // Increment count of visited nodes
    c++;

    // If c becomes k now, then this is the k'th largest
    if (c == k)
    {
        cout << "K'th largest element is "
             << root->key << endl;
        return;
    }

    // Recur for left subtree
    kthLargestUtil(root->left, k, c);
}

// Function to find k'th largest element
void kthLargest(Node *root, int k)
{
    // Initialize count of nodes visited as 0
    int c = 0;

    // Note that c is passed by reference
    kthLargestUtil(root, k, c);
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

    int c = 0;
    for (int k=1; k<=7; k++)
        kthLargest(root, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find k'th largest element in BST

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

    // function to insert nodes
    public void insert(int data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node
    with given key in BST */
    Node insertRec(Node node, int data)
    {  
        /* If the tree is empty, return a new node */
        if (node == null) {
            this.root = new Node(data);
            return this.root;
        }

        if (data == node.data) {
            return node;
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

    // utility function to find kth largest no in
    // a given tree
    void kthLargestUtil(Node node, int k, count C)
    {
        // Base cases, the second condition is important to
        // avoid unnecessary recursive calls
        if (node == null || C.c >= k)
            return;

        // Follow reverse inorder traversal so that the
        // largest element is visited first
        this.kthLargestUtil(node.right, k, C);

        // Increment count of visited nodes
        C.c++;

        // If c becomes k now, then this is the k'th largest
        if (C.c == k) {
            System.out.println(k + "th largest element is " +
                                                 node.data);
            return;
        }

        // Recur for left subtree
        this.kthLargestUtil(node.left, k, C);
    }

    // Method to find the kth largest no in given BST
    void kthLargest(int k)
    {
        count c = new count(); // object of class count
        this.kthLargestUtil(this.root, k, c);
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

        for (int i = 1; i <= 7; i++) {
            tree.kthLargest(i);
        }
    }
}

// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to find k'th largest
# element in BST

class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# A function to find k'th largest
# element in a given tree.
def kthLargestUtil(root, k, c):

    # Base cases, the second condition
    # is important to avoid unnecessary
    # recursive calls
    if root == None or c[0] >= k:
        return

    # Follow reverse inorder traversal
    # so that the largest element is
    # visited first
    kthLargestUtil(root.right, k, c)

    # Increment count of visited nodes
    c[0] += 1

    # If c becomes k now, then this is
    # the k'th largest
    if c[0] == k:
        print("K'th largest element is",
                               root.key)
        return

    # Recur for left subtree
    kthLargestUtil(root.left, k, c)

# Function to find k'th largest element
def kthLargest(root, k):

    # Initialize count of nodes
    # visited as 0
    c = [0]

    # Note that c is passed by reference
    kthLargestUtil(root, k, c)

# A utility function to insert a new
# node with given key in BST */
def insert(node, key):

    # If the tree is empty,
    # return a new node
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
    # / \ / \
    # 20 40 60 80 */
    root = None
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)

    for k in range(1,8):
        kthLargest(root, k)

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# code to find k'th largest element in BST

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

    // function to insert nodes
    public virtual void insert(int data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node 
    with given key in BST */
    public virtual Node insertRec(Node node, int data)
    {
        /* If the tree is empty, return a new node */
        if (node == null)
        {
            this.root = new Node(data);
            return this.root;
        }

        if (data == node.data)
        {
            return node;
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

        internal int c = 0;
    }

    // utility function to find kth largest no in 
    // a given tree
    public virtual void kthLargestUtil(Node node, int k, count C)
    {
        // Base cases, the second condition is important to
        // avoid unnecessary recursive calls
        if (node == null || C.c >= k)
        {
            return;
        }

        // Follow reverse inorder traversal so that the
        // largest element is visited first
        this.kthLargestUtil(node.right, k, C);

        // Increment count of visited nodes
        C.c++;

        // If c becomes k now, then this is the k'th largest 
        if (C.c == k)
        {
            Console.WriteLine(k + "th largest element is " + node.data);
            return;
        }

        // Recur for left subtree
        this.kthLargestUtil(node.left, k, C);
    }

    // Method to find the kth largest no in given BST
    public virtual void kthLargest(int k)
    {
        count c = new count(this); // object of class count
        this.kthLargestUtil(this.root, k, c);
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

        for (int i = 1; i <= 7; i++)
        {
            tree.kthLargest(i);
        }
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript code to find k'th largest element in BST

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

    // Constructor

    // function to insert nodes
    function insert(data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node
    with given key in BST */
    function insertRec( node , data)
    {  
        /* If the tree is empty, return a new node */
        if (node == null) {
            this.root = new Node(data);
            return this.root;
        }

        if (data == node.data) {
            return node;
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
        constructor(){this.c = 0;}

    }

    // utility function to find kth largest no in
    // a given tree
    function kthLargestUtil( node , k,  C)
    {
        // Base cases, the second condition is important to
        // avoid unnecessary recursive calls
        if (node == null || C.c >= k)
            return;

        // Follow reverse inorder traversal so that the
        // largest element is visited first
        this.kthLargestUtil(node.right, k, C);

        // Increment count of visited nodes
        C.c++;

        // If c becomes k now, then this is the k'th largest
        if (C.c == k) {
            document.write(k + "th largest element is " +
                                                 node.data+"<br/>");
            return;
        }

        // Recur for left subtree
        this.kthLargestUtil(node.left, k, C);
    }

    // Method to find the kth largest no in given BST
    function kthLargest(k)
    {
         c = new count(); // object of class count
        this.kthLargestUtil(this.root, k, c);
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

        for (i = 1; i <= 7; i++) {
            kthLargest(i);
        }

// This code contributed by gauravrajput1
</script>
```

**输出:**

```
K'th largest element is 80
K'th largest element is 70
K'th largest element is 60
K'th largest element is 50
K'th largest element is 40
K'th largest element is 30
K'th largest element is 20 
```

**复杂度分析:**

1.  **时间复杂度:** O(h + k)。
    代码首先向下遍历到最右边的节点，这需要 O(h)时间，然后在 O(k)时间内遍历 k 个元素。因此整体时间复杂度为 O(h + k)。
2.  **辅助空间:** O(h)。
    给定时间高度 h 的最大递归栈。

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由 **Chirag Sharma** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息