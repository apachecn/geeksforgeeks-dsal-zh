# 检查 BST 是否包含死胡同的简单递归解法

> 原文:[https://www . geesforgeks . org/simple-recursive-solution-check-是否-bst-contains-dead-end/](https://www.geeksforgeeks.org/simple-recursive-solution-check-whether-bst-contains-dead-end/)

给定包含大于 0 的正整数值的二叉查找树。任务是检查 BST 是否包含死胡同。这里的死胡同是指，我们不能在那个节点后插入任何整数元素。
**例:**

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

Output :Yes
Explanation : We can't insert any element at
              node 9.
```

我们在下面的帖子中讨论了一个解决方案。
[检查 BST 是否包含死路](https://www.geeksforgeeks.org/check-whether-bst-contains-dead-end-not/)
本文思路基于[检查二叉树是否为 BST 的方法 3](https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)。
首先给出它是一个 BST，节点大于零，根节点可以在[1，∞]范围内，如果根 val 是说 val，那么左子树可以有[1，val-1]范围内的值，右子树可以有[val+1，∞]范围内的值。
我们需要递归遍历，当范围的最小值和最大值一致时，这意味着我们不能在树中再添加任何节点。
于是我们遇到了死胡同。
下面是这个问题的简单递归解法。

## C++

```
// CPP Program to check if there is a dead end
// in BST or not.
#include <bits/stdc++.h>
using namespace std;

// A BST node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

/* A utility function to insert a new Node
  with given key in BST */
struct Node* insert(struct Node* node, int key)
{
    /* If the tree is empty, return a new Node */
    if (node == NULL)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);

    /* return the (unchanged) Node pointer */
    return node;
}

// Returns true if tree with given root contains
// dead end or not. min and max indicate range
// of allowed values for current node. Initially
// these values are full range.
bool deadEnd(Node* root, int min=1, int max=INT_MAX)
{
    // if the root is null or the recursion moves
    // after leaf node it will return false
    // i.e no dead end.
    if (!root)
        return false;

    // if this occurs means dead end is present.
    if (min == max)
        return true;

    // heart of the recursion lies here.
    return deadEnd(root->left, min, root->data - 1) ||
           deadEnd(root->right, root->data + 1, max);
}

// Driver program
int main()
{
    /*   8
       /   \
      5    11
     /  \
    2    7
     \
      3
       \
        4 */
    Node* root = NULL;
    root = insert(root, 8);
    root = insert(root, 5);
    root = insert(root, 2);
    root = insert(root, 3);
    root = insert(root, 7);
    root = insert(root, 11);
    root = insert(root, 4);
    if (deadEnd(root) == true)
        cout << "Yes " << endl;
    else
        cout << "No " << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if there
// is a dead end in BST or not.
class BinarySearchTree {

    // Class containing left and right
    // child of current node and key value
    class Node {
        int data;
        Node left, right;

        public Node(int item) {
            data = item;
            left = right = null;
        }
    }

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree() {
        root = null;
    }

    // This method mainly calls insertRec()
    void insert(int data) {
    root = insertRec(root, data);
    }

    // A recursive function
    // to insert a new key in BST
    Node insertRec(Node root, int data) {

        // If the tree is empty,
        // return a new node
        if (root == null) {
            root = new Node(data);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (data < root.data)
            root.left = insertRec(root.left, data);
        else if (data > root.data)
            root.right = insertRec(root.right, data);

        /* return the (unchanged) node pointer */
        return root;
    }

// Returns true if tree with given root contains
// dead end or not. min and max indicate range
// of allowed values for current node. Initially
// these values are full range.
boolean deadEnd(Node root, int min, int max)
{
    // if the root is null or the recursion moves
    // after leaf node it will return false
    // i.e no dead end.
    if (root==null)
        return false;

    // if this occurs means dead end is present.
    if (min == max)
        return true;

    // heart of the recursion lies here.
    return deadEnd(root.left, min, root.data - 1)||
                deadEnd(root.right, root.data + 1, max);
}

    // Driver Program
    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();

        /*       8
               /   \
              5    11
             /  \
            2    7
             \
              3
               \
                4 */
        tree.insert(8);
        tree.insert(5);
        tree.insert(2);
        tree.insert(3);
        tree.insert(7);
        tree.insert(11);
        tree.insert(4);

        if (tree.deadEnd(tree.root ,1 ,
                Integer.MAX_VALUE) == true)

        System.out.println("Yes ");
        else
        System.out.println("No " );
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python 3 Program to check if there
# is a dead end in BST or not.

class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A utility function to insert a
# new Node with given key in BST
def insert(node, key):

    # If the tree is empty,
    # return a new Node
    if node == None:
        return Node(key)

    # Otherwise, recur down the tree
    if key < node.data:
        node.left = insert(node.left, key)
    elif key > node.data:
        node.right = insert(node.right, key)

    # return the (unchanged) Node pointer
    return node

# Returns true if tree with given
# root contains dead end or not.
# min and max indicate range
# of allowed values for current node.
# Initially these values are full range.
def deadEnd(root, Min, Max):

    # if the root is null or the recursion
    # moves after leaf node it will return 
    # false i.e no dead end.
    if root == None:
        return False

    # if this occurs means dead
    # end is present.
    if Min == Max:
        return True

    # heart of the recursion lies here.
    return (deadEnd(root.left, Min, root.data - 1) or
            deadEnd(root.right, root.data + 1, Max))

# Driver Code
if __name__ == '__main__':

    #         8
    #     / \
    #     5 11
    #     / \
    # 2 7
    #     \
    #     3
    #     \
    #     4
    root = None
    root = insert(root, 8)
    root = insert(root, 5)
    root = insert(root, 2)
    root = insert(root, 3)
    root = insert(root, 7)
    root = insert(root, 11)
    root = insert(root, 4)
    if deadEnd(root, 1, 9999999999) == True:
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# Program to check if there
// is a dead end in BST or not.
public class BinarySearchTree
{

    // Class containing left and right
    // child of current node and key value
    public class Node
    {
        private readonly BinarySearchTree outerInstance;

        public int data;
        public Node left, right;

        public Node(BinarySearchTree outerInstance, int item)
        {
            this.outerInstance = outerInstance;
            data = item;
            left = right = null;
        }
    }

    // Root of BST
    public Node root;

    // Constructor
    public BinarySearchTree()
    {
        root = null;
    }

    // This method mainly calls insertRec()
    public virtual void insert(int data)
    {
    root = insertRec(root, data);
    }

    // A recursive function
    // to insert a new key in BST
    public virtual Node insertRec(Node root, int data)
    {

        // If the tree is empty,
        // return a new node
        if (root == null)
        {
            root = new Node(this, data);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (data < root.data)
        {
            root.left = insertRec(root.left, data);
        }
        else if (data > root.data)
        {
            root.right = insertRec(root.right, data);
        }

        /* return the (unchanged) node pointer */
        return root;
    }

// Returns true if tree with given root contains
// dead end or not. min and max indicate range
// of allowed values for current node. Initially
// these values are full range.
public virtual bool deadEnd(Node root, int min, int max)
{
    // if the root is null or the recursion moves
    // after leaf node it will return false
    // i.e no dead end.
    if (root == null)
    {
        return false;
    }

    // if this occurs means dead end is present.
    if (min == max)
    {
        return true;
    }

    // heart of the recursion lies here.
    return deadEnd(root.left, min, root.data - 1) || deadEnd(root.right, root.data + 1, max);
}

    // Driver Program
    public static void Main(string[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /*       8
               /   \
              5    11
             /  \
            2    7
             \
              3
               \
                4 */
        tree.insert(8);
        tree.insert(5);
        tree.insert(2);
        tree.insert(3);
        tree.insert(7);
        tree.insert(11);
        tree.insert(4);

        if (tree.deadEnd(tree.root,1, int.MaxValue) == true)
        {

        Console.WriteLine("Yes ");
        }
        else
        {
        Console.WriteLine("No ");
        }
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript Program to check if there
// is a dead end in BST or not.

    // Class containing left and right
    // child of current node and key value
    class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }

    // Root of BST
    var root = null;

    // This method mainly calls insertRec()
    function insert(data) {
    root = insertRec(root, data);
    }

    // A recursive function
    // to insert a new key in BST
    function insertRec(root , data) {

        // If the tree is empty,
        // return a new node
        if (root == null) {
            root = new Node(data);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (data < root.data)
            root.left = insertRec(root.left, data);
        else if (data > root.data)
            root.right = insertRec(root.right, data);

        /* return the (unchanged) node pointer */
        return root;
    }

// Returns true if tree with given root contains
// dead end or not. min and max indicate range
// of allowed values for current node. Initially
// these values are full range.
function deadEnd(root , min , max)
{
    // if the root is null or the recursion moves
    // after leaf node it will return false
    // i.e no dead end.
    if (root==null)
        return false;

    // if this occurs means dead end is present.
    if (min == max)
        return true;

    // heart of the recursion lies here.
    return deadEnd(root.left, min, root.data - 1)||
                deadEnd(root.right, root.data + 1, max);
}   // Driver Program

        /*       8
               /   \
              5    11
             /  \
            2    7
             \
              3
               \
                4 */
        insert(8);
        insert(5);
        insert(2);
        insert(3);
        insert(7);
        insert(11);
        insert(4);

        if (deadEnd(root ,1 ,
                Number.MAX_VALUE) == true)

        document.write("Yes ");
        else
        document.write("No " );

// This code contributed by Rajput-Ji
</script>
```

**输出:**

```
Yes
```