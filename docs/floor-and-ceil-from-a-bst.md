# 从英国标准时间

开始的地板和天花板

> 原文:[https://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/](https://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/)

给定一个二叉树和一个键值(节点)，找到该键值的下限和上限。

**楼层值节点**:数据最大值小于等于键值的节点。
**天花板值节点**:数据最小大于等于键值的节点。

例如，让我们考虑下面的二叉树–

```
          8
        /   \    
      4      12
    /  \    /  \
   2    6  10   14

Key: 11  Floor: 10  Ceil: 12
Key: 1   Floor: -1  Ceil: 2
Key: 6   Floor: 6   Ceil: 6
Key: 15  Floor: 14  Ceil: -1
```

在许多应用中，我们需要找到二叉查找树或排序数组中某个键的下限/上限值。例如，考虑设计一个内存管理系统，其中自由节点排列在 BST 中。找到最适合输入请求的方式。

**算法:**

```
Imagine we are moving down the tree, and assume we are root node. 
The comparison yields three possibilities,

A) Root data is equal to key. We are done, root data is ceil value.

B) Root data < key value, certainly the ceil value can't be in left subtree. 
   Proceed to search on right subtree as reduced problem instance.

C) Root data > key value, the ceil value *may be* in left subtree. 
   We may find a node with is larger data than key value in left subtree, 
   if not the root itself will be ceil node.
```

**这里是天花板值的代码:**

## C++

```
// Program to find ceil of a given value in BST
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has key, left child and right child */
class node {
public:
    int key;
    node* left;
    node* right;
};

/* Helper function that allocates a new node with the given key and
NULL left and right pointers.*/
node* newNode(int key)
{
    node* Node = new node();
    Node->key = key;
    Node->left = NULL;
    Node->right = NULL;
    return (Node);
}

// Function to find ceil of a given input in BST. If input is more
// than the max key in BST, return -1
int Ceil(node* root, int input)
{
    // Base case
    if (root == NULL)
        return -1;

    // We found equal key
    if (root->key == input)
        return root->key;

    // If root's key is smaller, ceil must be in right subtree
    if (root->key < input)
        return Ceil(root->right, input);

    // Else, either left subtree or root has the ceil value
    int ceil = Ceil(root->left, input);
    return (ceil >= input) ? ceil : root->key;
}

// Driver program to test above function
int main()
{
    node* root = newNode(8);

    root->left = newNode(4);
    root->right = newNode(12);

    root->left->left = newNode(2);
    root->left->right = newNode(6);

    root->right->left = newNode(10);
    root->right->right = newNode(14);

    for (int i = 0; i < 16; i++)
        cout << i << " " << Ceil(root, i) << endl;

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// Program to find ceil of a given value in BST
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has key, left child and right child */
struct node {
    int key;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node with the given key and
NULL left and right pointers.*/
struct node* newNode(int key)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// Function to find ceil of a given input in BST. If input is more
// than the max key in BST, return -1
int Ceil(struct node* root, int input)
{
    // Base case
    if (root == NULL)
        return -1;

    // We found equal key
    if (root->key == input)
        return root->key;

    // If root's key is smaller, ceil must be in right subtree
    if (root->key < input)
        return Ceil(root->right, input);

    // Else, either left subtree or root has the ceil value
    int ceil = Ceil(root->left, input);
    return (ceil >= input) ? ceil : root->key;
}

// Driver program to test above function
int main()
{
    struct node* root = newNode(8);

    root->left = newNode(4);
    root->right = newNode(12);

    root->left->left = newNode(2);
    root->left->right = newNode(6);

    root->right->left = newNode(10);
    root->right->right = newNode(14);

    for (int i = 0; i < 16; i++)
        printf("%d %d\n", i, Ceil(root, i));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find ceil of a given value in BST

class Node {

    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinaryTree {

    Node root;

    // Function to find ceil of a given input in BST.
    // If input is more than the max key in BST,
    // return -1
    int Ceil(Node node, int input)
    {

        // Base case
        if (node == null) {
            return -1;
        }

        // We found equal key
        if (node.data == input) {
            return node.data;
        }

        // If root's key is smaller,
        // ceil must be in right subtree
        if (node.data < input) {
            return Ceil(node.right, input);
        }

        // Else, either left subtree or root
        // has the ceil value
        int ceil = Ceil(node.left, input);

        return (ceil >= input) ? ceil : node.data;
    }

    // Driver Code
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(8);
        tree.root.left = new Node(4);
        tree.root.right = new Node(12);
        tree.root.left.left = new Node(2);
        tree.root.left.right = new Node(6);
        tree.root.right.left = new Node(10);
        tree.root.right.right = new Node(14);
        for (int i = 0; i < 16; i++) {

            System.out.println(i + " " + tree.Ceil(tree.root, i));
        }
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find ceil of a given value in BST

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# Function to find ceil of a given input in BST. If input
# is more than the max key in BST, return -1
def ceil(root, inp):

    # Base Case
    if root == None:
        return -1

    # We found equal key
    if root.key == inp :
        return root.key

    # If root's key is smaller, ceil must be in right subtree
    if root.key < inp:
        return ceil(root.right, inp)

    # Else, either left subtre or root has the ceil value
    val = ceil(root.left, inp)
    return val if val >= inp else root.key

# Driver program to test above function
root = Node(8)

root.left = Node(4)
root.right = Node(12)

root.left.left = Node(2)
root.left.right = Node(6)

root.right.left = Node(10)
root.right.right = Node(14)

for i in range(16):
    print "% d % d" %(i, ceil(root, i))

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to find ceil of a given value in BST

public class Node {

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinaryTree {

    public static Node root;

    // Function to find ceil of a given input in BST. If input is more
    // than the max key in BST, return -1
    public virtual int Ceil(Node node, int input)
    {

        // Base case
        if (node == null) {
            return -1;
        }

        // We found equal key
        if (node.data == input) {
            return node.data;
        }

        // If root's key is smaller, ceil must be in right subtree
        if (node.data < input) {
            return Ceil(node.right, input);
        }

        // Else, either left subtree or root has the ceil value
        int ceil = Ceil(node.left, input);
        return (ceil >= input) ? ceil : node.data;
    }

    // Driver program to test the above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        BinaryTree.root = new Node(8);
        BinaryTree.root.left = new Node(4);
        BinaryTree.root.right = new Node(12);
        BinaryTree.root.left.left = new Node(2);
        BinaryTree.root.left.right = new Node(6);
        BinaryTree.root.right.left = new Node(10);
        BinaryTree.root.right.right = new Node(14);
        for (int i = 0; i < 16; i++) {
            Console.WriteLine(i + " " + tree.Ceil(root, i));
        }
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to find ceil
// of a given value in BST

    class Node
    {

        constructor(x) {
            this.data = x;
            this.left = null;
            this.right = null;
          }
    }

    let root;

    // Function to find ceil of
    // a given input in BST.
    // If input is more than the max
    // key in BST,
    // return -1
    function Ceil(node,input)
    {
        // Base case
        if (node == null) {
            return -1;
        }

        // We found equal key
        if (node.data == input) {
            return node.data;
        }

        // If root's key is smaller,
        // ceil must be in right subtree
        if (node.data < input) {
            return Ceil(node.right, input);
        }

        // Else, either left subtree or root
        // has the ceil value
        let ceil = Ceil(node.left, input);

        return (ceil >= input) ? ceil : node.data;
    }

    // Driver Code
    root =new Node(8)

    root.left =new Node(4)
    root.right =new Node(12)

    root.left.left =new Node(2)
    root.left.right =new Node(6)

    root.right.left =new Node(10)
    root.right.right =new Node(14)

    for (let i = 0; i < 16; i++) {

        document.write(i + " " + Ceil(root, i)+"<br>");
    }

    // This code is contributed by unknown2108

</script>
```

**输出:**

```
0  2
1  2
2  2
3  4
4  4
5  6
6  6
7  8
8  8
9  10
10  10
11  12
12  12
13  14
14  14
15  -1
```

**迭代方法–**

```
1. If tree is empty, i.e. root is null, 
   return back to calling function.
2. If current node address is not null, perform the following steps : 
 (a) If current node data matches with the key value - 
             We have found both our floor and ceil value. 
             Hence, we return back to calling function.
 (b) If data in current node is lesser than the key value - 
            We assign the current node data to the variable keeping
            track of current floor value and explore the right subtree,
            as it may contain nodes with values greater than key value.
 (c) If data in current node is greater than the key value - 
            We assign the current node data to the variable keeping track
            of current ceil value and explore the left subtree, as it may
            contain nodes with values lesser than key value.
3. Once we reach null, we return back to the calling function,
   as we have got our required floor and ceil values for the particular key value.
```

下面是上述方法的实现:

## C++

```
// C++ program to find floor and ceil of a given key in BST
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has key, left child and right child */
struct Node {
    int data;
    Node *left, *right;

    Node(int value)
    {
        data = value;
        left = right = NULL;
    }
};

// Helper function to find floor and ceil of a given key in BST
void floorCeilBSTHelper(Node* root, int key, int& floor, int& ceil)
{

    while (root) {

        if (root->data == key) {
            ceil = root->data;
            floor = root->data;
            return;
        }

        if (key > root->data) {
            floor = root->data;
            root = root->right;
        }
        else {
            ceil = root->data;
            root = root->left;
        }
    }
    return;
}

// Display the floor and ceil of a given key in BST.
// If key is less than the min key in BST, floor will be -1;
// If key is more than the max key in BST, ceil will be -1;
void floorCeilBST(Node* root, int key)
{

    // Variables 'floor' and 'ceil' are passed by reference
    int floor = -1, ceil = -1;

    floorCeilBSTHelper(root, key, floor, ceil);

    cout << key << ' ' << floor << ' ' << ceil << '\n';
}

// Driver program to test above function
int main()
{
    Node* root = new Node(8);

    root->left = new Node(4);
    root->right = new Node(12);

    root->left->left = new Node(2);
    root->left->right = new Node(6);

    root->right->left = new Node(10);
    root->right->right = new Node(14);

    for (int i = 0; i < 16; i++)
        floorCeilBST(root, i);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find floor and ceil
// of a given key in BST
import java.io.*;

// A binary tree node has key,
// left child and right child
class Node
{
    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinaryTree{

Node root;
int floor;
int ceil;

// Helper function to find floor and
// ceil of a given key in BST
public void floorCeilBSTHelper(Node root,
                               int key)
{
    while (root != null)
    {
        if (root.data == key)
        {
            ceil = root.data;
            floor = root.data;
            return;
        }

        if (key > root.data)
        {
            floor = root.data;
            root = root.right;
        }
        else
        {
            ceil = root.data;
            root = root.left;
        }
    }
    return;
}

// Display the floor and ceil of a
// given key in BST. If key is less
// than the min key in BST, floor
// will be -1; If key is more than
// the max key in BST, ceil will be -1;
public void floorCeilBST(Node root, int key)
{

    // Variables 'floor' and 'ceil'
    // are passed by reference
    floor = -1;
    ceil = -1;

    floorCeilBSTHelper(root, key);

    System.out.println(key + " " +
                     floor + " " + ceil);
}

// Driver code
public static void main(String[] args)
{
    BinaryTree tree = new BinaryTree();
    tree.root = new Node(8);
    tree.root.left = new Node(4);
    tree.root.right = new Node(12);
    tree.root.left.left = new Node(2);
    tree.root.left.right = new Node(6);
    tree.root.right.left = new Node(10);
    tree.root.right.right = new Node(14);

    for(int i = 0; i < 16; i++)
    {
        tree.floorCeilBST(tree.root, i);
    }
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Python3 program to find floor and
# ceil of a given key in BST

# A binary tree node has key,
#. left child and right child
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Helper function to find floor and
# ceil of a given key in BST
def floorCeilBSTHelper(root, key):

    global floor, ceil

    while (root):
        if (root.data == key):
            ceil = root.data
            floor = root.data
            return
        if (key > root.data):
            floor = root.data
            root = root.right
        else:
            ceil = root.data
            root = root.left

# Display the floor and ceil of a given
# key in BST. If key is less than the min
# key in BST, floor will be -1; If key is
# more than the max key in BST, ceil will be -1;
def floorCeilBST(root, key):

    global floor, ceil

    # Variables 'floor' and 'ceil'
    # are passed by reference
    floor = -1
    ceil = -1

    floorCeilBSTHelper(root, key)

    print(key, floor, ceil)

# Driver code
if __name__ == '__main__':

    floor, ceil = -1, -1

    root = Node(8)
    root.left = Node(4)
    root.right = Node(12)
    root.left.left = Node(2)
    root.left.right = Node(6)
    root.right.left = Node(10)
    root.right.right = Node(14)

    for i in range(16):
        floorCeilBST(root, i)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find floor and ceil
// of a given key in BST
using System;

// A binary tree node has key,
// left child and right child
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

public class BinaryTree{

public static Node root;
int floor;
int ceil;

// Helper function to find floor and
// ceil of a given key in BST
public int floorCeilBSTHelper(Node root, int key)
{
    while (root != null)
    {
        if (root.data == key)
        {
            ceil = root.data;
            floor = root.data;
            return 0;
        }

        if (key > root.data)
        {
            floor = root.data;
            root = root.right;
        }
        else   
        {
            ceil = root.data;
            root = root.left;
        }
    }
    return 0;
}

// Display the floor and ceil of a
// given key in BST. If key is less
// than the min key in BST, floor
// will be -1; If key is more than
// the max key in BST, ceil will be -1;
public void floorCeilBST(Node root, int key)
{

    // Variables 'floor' and 'ceil'
    // are passed by reference
    floor = -1;
    ceil = -1;

    floorCeilBSTHelper(root, key);

    Console.WriteLine(key + " " + floor +
                            " " + ceil);
}

// Driver code
static public void Main()
{
    BinaryTree tree = new BinaryTree();
    BinaryTree.root = new Node(8);
    BinaryTree.root.left = new Node(4);
    BinaryTree.root.right = new Node(12);
    BinaryTree.root.left.left = new Node(2);
    BinaryTree.root.left.right = new Node(6);
    BinaryTree.root.right.left = new Node(10);
    BinaryTree.root.right.right = new Node(14);

    for(int i = 0; i < 16; i++)
    {
        tree.floorCeilBST(BinaryTree.root, i);
    }
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program to find floor and ceil
// of a given key in BST

// A binary tree node has key,
// left child and right child
class Node
{
    constructor(d)
    {
        this.data = d;
        this.left = null;
        this.right = null;
    }
}

var root = null;
var floor;
var ceil;

// Helper function to find floor and
// ceil of a given key in BST
function floorCeilBSTHelper(root, key)
{
    while (root != null)
    {
        if (root.data == key)
        {
            ceil = root.data;
            floor = root.data;
            return 0;
        }

        if (key > root.data)
        {
            floor = root.data;
            root = root.right;
        }
        else   
        {
            ceil = root.data;
            root = root.left;
        }
    }
    return 0;
}

// Display the floor and ceil of a
// given key in BST. If key is less
// than the min key in BST, floor
// will be -1; If key is more than
// the max key in BST, ceil will be -1;
function floorCeilBST(root, key)
{

    // Variables 'floor' and 'ceil'
    // are passed by reference
    floor = -1;
    ceil = -1;

    floorCeilBSTHelper(root, key);

    document.write(key + " " + floor +
                            " " + ceil + "<br>");
}

// Driver code
root = new Node(8);
root.left = new Node(4);
root.right = new Node(12);
root.left.left = new Node(2);
root.left.right = new Node(6);
root.right.left = new Node(10);
root.right.right = new Node(14);

for(var i = 0; i < 16; i++)
{
    floorCeilBST(root, i);
}

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
0 -1 2
1 -1 2
2 2 2
3 2 4
4 4 4
5 4 6
6 6 6
7 6 8
8 8 8
9 8 10
10 10 10
11 10 12
12 12 12
13 12 14
14 14 14
15 14 -1
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)

**锻炼:**
1。修改上面的代码，找到二叉查找树输入键的楼层值。
2。写一个简洁的算法，在一个排序的数组中找到楼层和天花板的值。确保处理所有可能的边界条件。

本文由 [**文基**](http://www.linkedin.com/in/ramanawithu) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。