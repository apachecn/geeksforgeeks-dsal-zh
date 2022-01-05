# 二叉查找树|第 1 集(搜索和插入)

> 原文:[https://www . geesforgeks . org/binary-search-tree-set-1-search-and-insert/](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)

以下是根据[维基百科](http://en.wikipedia.org/wiki/Binary_search_tree)
对二叉查找树(BST)的定义二叉查找树是一个基于节点的二叉树数据结构，具有以下性质:

*   节点的左子树只包含键小于节点键的节点。
*   节点的右子树只包含键大于节点键的节点。
*   左右子树也必须是二叉查找树树。
    不能有重复节点。

![200px-Binary_search_tree.svg](img/2bb297fb1a678d9c862d10acac5302e9.png)

二叉查找树的上述属性提供了键之间的排序，因此像搜索、最小值和最大值这样的操作可以快速完成。如果没有排序，那么我们可能必须比较每个键来搜索给定的键。

**搜索一个键**
为了搜索一个值，如果我们有一个排序的数组，我们可以执行一个二分搜索法。假设我们想在数组中搜索一个数字，我们在二分搜索法做的是我们首先定义完整的列表作为我们的搜索空间，这个数字只能存在于搜索空间内。现在，我们将要搜索的数字或元素与搜索空间的中间元素或中间值进行比较，如果要搜索的记录较少，我们在左半部分搜索，否则我们在右半部分搜索，在相等的情况下，我们找到了元素。在二分搜索法，我们从搜索空间中的**‘n’**元素开始，然后如果中间元素不是我们正在寻找的元素，我们将搜索空间缩小到**‘n/2’**，并且我们继续缩小搜索空间，直到我们找到我们正在寻找的记录，或者我们在搜索空间中只找到一个元素，并且完成整个缩小。

在二叉查找树的搜索行动将非常相似。假设我们想搜索数字，我们要做的是从根开始，然后我们将待搜索的值与根的值进行比较，如果相等，我们就完成搜索，如果较小，我们知道我们需要转到左子树，因为在二叉查找树中，左子树中的所有元素都较小，右子树中的所有元素都较大。在二叉查找树中搜索一个元素基本上就是这样的遍历，在每一步中，我们要么向左要么向右，因此在每一步中，我们丢弃一个子树。如果树是平衡的，如果所有节点的左右子树的高度差不大于 1，我们称之为平衡树， 我们将从 **'n'** 节点的搜索空间开始，当我们丢弃其中一个子树时，我们将丢弃 **'n/2'** 节点，因此我们的搜索空间将减少到 **'n/2'** ，然后在下一步中，我们将搜索空间减少到 **'n/4'** ，我们将继续这样减少，直到找到元素，或者直到我们的搜索空间减少到只有一个节点。 这里的搜索也是一个二分搜索法，这就是为什么二叉查找树这个名字。

## C++

```
// C function to search a given key in a given BST
struct node* search(struct node* root, int key)
{
    // Base Cases: root is null or key is present at root
    if (root == NULL || root->key == key)
       return root;

    // Key is greater than root's key
    if (root->key < key)
       return search(root->right, key);

    // Key is smaller than root's key
    return search(root->left, key);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A utility function to search a given key in BST
public Node search(Node root, int key)
{
    // Base Cases: root is null or key is present at root
    if (root==null || root.key==key)
        return root;

    // Key is greater than root's key
    if (root.key < key)
       return search(root.right, key);

    // Key is smaller than root's key
    return search(root.left, key);
}
```

## 计算机编程语言

```
# A utility function to search a given key in BST
def search(root,key):

    # Base Cases: root is null or key is present at root
    if root is None or root.val == key:
        return root

    # Key is greater than root's key
    if root.val < key:
        return search(root.right,key)

    # Key is smaller than root's key
    return search(root.left,key)

# This code is contributed by Bhavya Jain
```

## C#

```
// A utility function to search
// a given key in BST
public Node search(Node root,
                   int key)
{
    // Base Cases: root is null
    // or key is present at root
    if (root == null ||
        root.key == key)
        return root;

   // Key is greater than root's key
    if (root.key < key)
       return search(root.right, key);

    // Key is smaller than root's key
    return search(root.left, key);
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// A utility function to search
// a given key in BST
function search(root, key)
{
    // Base Cases: root is null
    // or key is present at root
    if (root == null ||
        root.key == key)
        return root;

   // Key is greater than root's key
    if (root.key < key)
       return search(root.right, key);

    // Key is smaller than root's key
    return search(root.left, key);
}

// This code is contributed by rrrtnx.
</script>
```

**插图在下图树中搜索 6:**
1。从根开始。
2。将搜索元素与根进行比较，如果小于根，则向左递归，否则向右递归。
3。如果要搜索的元素在任何地方都找到，则返回 true，否则返回 false。

![bstsearch](img/2bb297fb1a678d9c862d10acac5302e9.png)

**插入一把钥匙**
一把新钥匙总是插在叶子上。我们从根开始搜索一个键，直到碰到一个叶节点。一旦找到叶节点，新节点将作为叶节点的子节点添加。

```
         100                               100
        /   \        Insert 40            /    \
      20     500    --------->          20     500 
     /  \                              /  \  
    10   30                           10   30
                                              \   
                                              40
```

## C++

```
// C++ program to demonstrate insertion
// in a BST recursively.
#include <iostream>
using namespace std;

class BST
{
    int data;
    BST *left, *right;

public:
    // Default constructor.
    BST();

    // Parameterized constructor.
    BST(int);

    // Insert function.
    BST* Insert(BST*, int);

    // Inorder traversal.
    void Inorder(BST*);
};

// Default Constructor definition.
BST ::BST()
    : data(0)
    , left(NULL)
    , right(NULL)
{
}

// Parameterized Constructor definition.
BST ::BST(int value)
{
    data = value;
    left = right = NULL;
}

// Insert function definition.
BST* BST ::Insert(BST* root, int value)
{
    if (!root)
    {
        // Insert the first node, if root is NULL.
        return new BST(value);
    }

    // Insert data.
    if (value > root->data)
    {
        // Insert right node data, if the 'value'
        // to be inserted is greater than 'root' node data.

        // Process right nodes.
        root->right = Insert(root->right, value);
    }
    else
    {
        // Insert left node data, if the 'value'
        // to be inserted is greater than 'root' node data.

        // Process left nodes.
        root->left = Insert(root->left, value);
    }

    // Return 'root' node, after insertion.
    return root;
}

// Inorder traversal function.
// This gives data in sorted order.
void BST ::Inorder(BST* root)
{
    if (!root) {
        return;
    }
    Inorder(root->left);
    cout << root->data << endl;
    Inorder(root->right);
}

// Driver code
int main()
{
    BST b, *root = NULL;
    root = b.Insert(root, 50);
    b.Insert(root, 30);
    b.Insert(root, 20);
    b.Insert(root, 40);
    b.Insert(root, 70);
    b.Insert(root, 60);
    b.Insert(root, 80);

    b.Inorder(root);
    return 0;
}

// This code is contributed by pkthapa
```

## C

```
// C program to demonstrate insert
// operation in binary
// search tree.
#include <stdio.h>
#include <stdlib.h>

struct node {
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node* newNode(int item)
{
    struct node* temp
        = (struct node*)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(struct node* root)
{
    if (root != NULL) {
        inorder(root->left);
        printf("%d \n", root->key);
        inorder(root->right);
    }
}

/* A utility function to insert
   a new node with given key in
 * BST */
struct node* insert(struct node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Driver Code
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    struct node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    // print inoder traversal of the BST
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate
// insert operation in binary
// search tree
class BinarySearchTree {

    /* Class containing left
       and right child of current node
     * and key value*/
    class Node
    {
        int key;
        Node left, right;

        public Node(int item)
        {
            key = item;
            left = right = null;
        }
    }

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree()
    {
         root = null;
    }

    // This method mainly calls insertRec()
    void insert(int key)
    {
         root = insertRec(root, key);
    }

    /* A recursive function to
       insert a new key in BST */
    Node insertRec(Node root, int key)
    {

        /* If the tree is empty,
           return a new node */
        if (root == null)
        {
            root = new Node(key);
            return root;
        }

        /* Otherwise, recur down the tree */
        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);

        /* return the (unchanged) node pointer */
        return root;
    }

    // This method mainly calls InorderRec()
    void inorder()
    {
         inorderRec(root);
    }

    // A utility function to
    // do inorder traversal of BST
    void inorderRec(Node root)
    {
        if (root != null) {
            inorderRec(root.left);
            System.out.println(root.key);
            inorderRec(root.right);
        }
    }

    // Driver Code
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

        // print inorder traversal of the BST
        tree.inorder();
    }
}
// This code is contributed by Ankur Narain Verma
```

## 计算机编程语言

```
# Python program to demonstrate
# insert operation in binary search tree

# A utility class that represents
# an individual node in a BST

class Node:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key

# A utility function to insert
# a new node with the given key

def insert(root, key):
    if root is None:
        return Node(key)
    else:
        if root.val == key:
            return root
        elif root.val < key:
            root.right = insert(root.right, key)
        else:
            root.left = insert(root.left, key)
    return root

# A utility function to do inorder tree traversal

def inorder(root):
    if root:
        inorder(root.left)
        print(root.val)
        inorder(root.right)

# Driver program to test the above functions
# Let us create the following BST
#    50
#  /     \
# 30     70
#  / \ / \
# 20 40 60 80

r = Node(50)
r = insert(r, 30)
r = insert(r, 20)
r = insert(r, 40)
r = insert(r, 70)
r = insert(r, 60)
r = insert(r, 80)

# Print inoder traversal of the BST
inorder(r)
```

## C#

```
// C# program to demonstrate
// insert operation in binary
// search tree
using System;

class BinarySearchTree{

// Class containing left and
// right child of current node
// and key value
public class Node
{
    public int key;
    public Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

// Root of BST
Node root;

// Constructor
BinarySearchTree()
{
    root = null;
}

// This method mainly calls insertRec()
void insert(int key)
{
    root = insertRec(root, key);
}

// A recursive function to insert
// a new key in BST
Node insertRec(Node root, int key)
{

    // If the tree is empty,
    // return a new node
    if (root == null)
    {
        root = new Node(key);
        return root;
    }

    // Otherwise, recur down the tree
    if (key < root.key)
        root.left = insertRec(root.left, key);
    else if (key > root.key)
        root.right = insertRec(root.right, key);

    // Return the (unchanged) node pointer
    return root;
}

// This method mainly calls InorderRec()
void inorder()
{
    inorderRec(root);
}

// A utility function to
// do inorder traversal of BST
void inorderRec(Node root)
{
    if (root != null)
    {
        inorderRec(root.left);
        Console.WriteLine(root.key);
        inorderRec(root.right);
    }
}

// Driver Code
public static void Main(String[] args)
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

    // Print inorder traversal of the BST
    tree.inorder();
}
}

// This code is contributed by aashish1995
```

**Output**

```
20
30
40
50
60
70
80
```

**在下图树中插入 2 的插图:**
1。从根开始。
2。将插入元素与根元素进行比较，如果小于根元素，则向左递归，否则向右递归。
3。到达终点后，只需在左侧(如果小于当前值)或右侧插入该节点。

![bstsearch](img/2bb297fb1a678d9c862d10acac5302e9.png)

**时间复杂度:**搜索和插入操作的最坏情况时间复杂度是 O(h)，其中 h 是二叉查找树的高度。在最坏的情况下，我们可能不得不从根走到最深的叶节点。倾斜树的高度可能变成 n，搜索和插入操作的时间复杂度可能变成 O(n)。

**使用循环插入:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
import java.io.*;

class GFG {
    public static void main (String[] args) {
         BST tree=new BST();
        tree.insert(30);
        tree.insert(50);
        tree.insert(15);
        tree.insert(20);
        tree.insert(10);
        tree.insert(40);
        tree.insert(60);
        tree.inorder();
    }
}

class Node{
    Node left;
    int val;
    Node right;
    Node(int val){
        this.val=val;
    }
}

class BST{
  Node root;

  public void insert(int key){
        Node node=new Node(key);
        if(root==null) {
            root = node;
            return;
        }
        Node prev=null;
        Node temp=root;
        while (temp!=null){
            if(temp.val>key){
                prev=temp;
                temp=temp.left;
            }
            else if (temp.val<key){
                prev=temp;
                temp=temp.right;
            }
        }
        if(prev.val>key)
            prev.left=node;
        else prev.right=node;
    }

   public void inorder(){
        Node temp=root;
        Stack<Node> stack=new Stack<>();
        while (temp!=null||!stack.isEmpty()){
            if(temp!=null){
                stack.add(temp);
                temp=temp.left;
            }
            else {
                temp=stack.pop();
                System.out.print(temp.val+" ");
                temp=temp.right;
            }
        }
    }
}
```

**Output**

```
10 15 20 30 40 50 60 
```

**一些有趣的事实:**

*   对 BST 的有序遍历总是产生排序的输出。
*   我们可以构造一个只有前序或后序或水平顺序遍历的 BST。请注意，我们总是可以通过对唯一给定的遍历进行排序来获得有序遍历。
*   [具有 n 个不同键的唯一 BST 的数量是加泰罗尼亚数字](https://www.geeksforgeeks.org/total-number-of-possible-binary-search-trees-using-catalan-number/)

**相关链接:**

*   [二叉查找树删除操作](https://www.geeksforgeeks.org/binary-search-tree-set-2-delete/)
*   [二叉查找树小测验](https://www.geeksforgeeks.org/data-structure-gq/binary-search-trees-gq/)
*   [BST 上的编码练习](https://practice.geeksforgeeks.org/tag-page.php?tag=BST&isCmp=0)
*   [英国标准时间](https://www.geeksforgeeks.org/binary-search-tree/)上的所有文章

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。