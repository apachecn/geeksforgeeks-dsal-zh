# 反转完美二叉树的交替层次

> 原文:[https://www . geesforgeks . org/reverse-alternate-levels-二叉树/](https://www.geeksforgeeks.org/reverse-alternate-levels-binary-tree/)

给定一个[完美二叉树](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)，反转二叉树的交替级节点。

```
Given tree: 
               a
            /     \
           b       c
         /  \     /  \
        d    e    f    g
       / \  / \  / \  / \
       h  i j  k l  m  n  o 

Modified tree:
               a
            /     \
           c       b
         /  \     /  \
        d    e    f    g
       / \  / \  / \  / \
      o  n m  l k  j  i  h 
```

**方法 1(简单)** :
A **简单解法**是做以下步骤。
**1)** 逐级接入节点。
**2)** 如果当前级别为奇数，则将该级别的节点存储在数组中。
**(3)**反转数组，将元素存储回树中。

**方法 2(使用两个遍历):**
另一个是做两个有序遍历。以下是应遵循的步骤。
**1)** 以有序的方式遍历给定的树，并将所有奇数级节点存储在辅助数组中。对于上面给出的例子树，数组的内容变成{h，I，b，j，k，l，m，c，n，o}
**2)** 反转数组。数组现在变成{o，n，c，m，l，k，j，b，I，h}
**3)** 再次遍历树，以便进行排序。遍历树时，一个接一个地从数组中获取元素，并将数组中的元素存储到每个奇数层遍历的节点。
对于上面的例子，我们先遍历上面数组中的‘h’，用‘o’替换‘h’。然后我们遍历“I”并用 n 替换它
下面是上述算法的实现。

## C++

```
// C++ program to reverse alternate
// levels of a binary tree
#include<bits/stdc++.h>
#define MAX 100
using namespace std;

// A Binary Tree node
struct Node
{
    char data;
    struct Node *left, *right;
};

// A utility function to create a
// new Binary Tree Node
struct Node *newNode(char item)
{
    struct Node *temp =  new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to store nodes of
// alternate levels in an array
void storeAlternate(Node *root, char arr[],
                        int *index, int l)
{
    // Base case
    if (root == NULL) return;

    // Store elements of left subtree
    storeAlternate(root->left, arr, index, l+1);

    // Store this node only if this is a odd level node
    if (l%2 != 0)
    {
        arr[*index] = root->data;
        (*index)++;
    }

    // Store elements of right subtree
    storeAlternate(root->right, arr, index, l+1);
}

// Function to modify Binary Tree
// (All odd level nodes are
// updated by taking elements from
// array in inorder fashion)
void modifyTree(Node *root, char arr[],
                           int *index, int l)
{
    // Base case
    if (root == NULL) return;

    // Update nodes in left subtree
    modifyTree(root->left, arr, index, l+1);

    // Update this node only if this
    // is an odd level node
    if (l%2 != 0)
    {
        root->data = arr[*index];
        (*index)++;
    }

    // Update nodes in right subtree
    modifyTree(root->right, arr, index, l+1);
}

// A utility function to reverse an array from index
// 0 to n-1
void reverse(char arr[], int n)
{
    int l = 0, r = n-1;
    while (l < r)
    {
        int temp = arr[l];
        arr[l] = arr[r];
        arr[r] = temp;
        l++; r--;
    }
}

// The main function to reverse
// alternate nodes of a binary tree
void reverseAlternate(struct Node *root)
{
    // Create an auxiliary array to store
    // nodes of alternate levels
    char *arr = new char[MAX];
    int index = 0;

    // First store nodes of alternate levels
    storeAlternate(root, arr, &index, 0);

    // Reverse the array
    reverse(arr, index);

    // Update tree by taking elements from array
    index = 0;
    modifyTree(root, arr, &index, 0);
}

// A utility function to print indorder traversal of a
// binary tree
void printInorder(struct Node *root)
{
    if (root == NULL) return;
    printInorder(root->left);
    cout << root->data << " ";
    printInorder(root->right);
}

// Driver Program to test above functions
int main()
{
    struct Node *root = newNode('a');
    root->left = newNode('b');
    root->right = newNode('c');
    root->left->left = newNode('d');
    root->left->right = newNode('e');
    root->right->left = newNode('f');
    root->right->right = newNode('g');
    root->left->left->left = newNode('h');
    root->left->left->right = newNode('i');
    root->left->right->left = newNode('j');
    root->left->right->right = newNode('k');
    root->right->left->left = newNode('l');
    root->right->left->right = newNode('m');
    root->right->right->left = newNode('n');
    root->right->right->right = newNode('o');

    cout << "Inorder Traversal of given tree\n";
    printInorder(root);

    reverseAlternate(root);

    cout << "\n\nInorder Traversal of modified tree\n";
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse alternate
// levels of  perfect binary tree
// A binary tree node
class Node {

    char data;
    Node left, right;

    Node(char item) {
        data = item;
        left = right = null;
    }
}

// class to access index value by reference
class Index {

    int index;
}

class BinaryTree {

    Node root;
    Index index_obj = new Index();

    // function to store alternate levels in a tree
    void storeAlternate(Node node, char arr[],
                         Index index, int l)
    {
        // base case
        if (node == null) {
            return;
        }
        // store elements of left subtree
        storeAlternate(node.left, arr, index, l + 1);

        // store this node only if level is odd
        if (l % 2 != 0) {
            arr[index.index] = node.data;
            index.index++;
        }

        storeAlternate(node.right, arr, index, l + 1);
    }

    // Function to modify Binary Tree
    // (All odd level nodes are
    // updated by taking elements from
    // array in inorder fashion)
    void modifyTree(Node node, char arr[],
                      Index index, int l)
    {

        // Base case
        if (node == null) {
            return;
        }

        // Update nodes in left subtree
        modifyTree(node.left, arr, index, l + 1);

        // Update this node only if
        // this is an odd level node
        if (l % 2 != 0) {
            node.data = arr[index.index];
            (index.index)++;
        }

        // Update nodes in right subtree
        modifyTree(node.right, arr, index, l + 1);
    }

    // A utility function to reverse an array from index
    // 0 to n-1
    void reverse(char arr[], int n) {
        int l = 0, r = n - 1;
        while (l < r) {
            char temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            l++;
            r--;
        }
    }

    void reverseAlternate()
    {
        reverseAlternate(root);
    }

    // The main function to reverse
    // alternate nodes of a binary tree
    void reverseAlternate(Node node)
    {

        // Create an auxiliary array to store
        // nodes of alternate levels
        char[] arr = new char[100];

        // First store nodes of alternate levels
        storeAlternate(node, arr, index_obj, 0);

        //index_obj.index = 0;

        // Reverse the array
        reverse(arr, index_obj.index);

        // Update tree by taking elements from array
        index_obj.index = 0;
        modifyTree(node, arr, index_obj, 0);
    }

    void printInorder() {
        printInorder(root);
    }

    // A utility function to print
    // indorder traversal of a
    // binary tree
    void printInorder(Node node) {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test the above functions
    public static void main(String args[]) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node('a');
        tree.root.left = new Node('b');
        tree.root.right = new Node('c');
        tree.root.left.left = new Node('d');
        tree.root.left.right = new Node('e');
        tree.root.right.left = new Node('f');
        tree.root.right.right = new Node('g');
        tree.root.left.left.left = new Node('h');
        tree.root.left.left.right = new Node('i');
        tree.root.left.right.left = new Node('j');
        tree.root.left.right.right = new Node('k');
        tree.root.right.left.left = new Node('l');
        tree.root.right.left.right = new Node('m');
        tree.root.right.right.left = new Node('n');
        tree.root.right.right.right = new Node('o');
        System.out.println("Inorder Traversal of given tree");
        tree.printInorder();

        tree.reverseAlternate();
        System.out.println("");
        System.out.println("");
        System.out.println("Inorder Traversal of modified tree");
        tree.printInorder();
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to reverse
# alternate levels of a binary tree
MAX = 100

# A Binary Tree node
class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.data = data

# A utility function to
# create a new Binary Tree
# Node
def newNode(item):

    temp = Node(item)
    return temp

# Function to store nodes of
# alternate levels in an array
def storeAlternate(root, arr,
                   index, l):

    # Base case
    if (root == None):
        return index;

    # Store elements of
    # left subtree
    index = storeAlternate(root.left,
                           arr, index,
                           l + 1);

    # Store this node only if
    # this is a odd level node
    if(l % 2 != 0):   
        arr[index] = root.data;
        index += 1;   

    # Store elements of right
    # subtree
    index=storeAlternate(root.right,
                         arr, index,
                         l + 1);
    return index

# Function to modify Binary Tree
# (All odd level nodes are
# updated by taking elements from
# array in inorder fashion)
def modifyTree(root, arr, index, l):

    # Base case
    if (root == None):
        return index;

    # Update nodes in left subtree
    index=modifyTree(root.left,
                     arr, index,
                     l + 1);

    # Update this node only
    # if this is an odd level
    # node
    if (l % 2 != 0):   
        root.data = arr[index];
        index += 1;   

    # Update nodes in right
    # subtree
    index=modifyTree(root.right,
                     arr, index,
                     l + 1);
    return index

# A utility function to
# reverse an array from
# index 0 to n-1
def reverse(arr, n):

    l = 0
    r = n - 1;

    while (l < r):       
        arr[l], arr[r] = (arr[r],
                          arr[l]);       
        l += 1
        r -= 1

# The main function to reverse
# alternate nodes of a binary tree
def reverseAlternate(root):

    # Create an auxiliary array
    # to store nodes of alternate
    # levels
    arr = [0 for i in range(MAX)]
    index = 0;

    # First store nodes of
    # alternate levels
    index=storeAlternate(root, arr,
                         index, 0);

    # Reverse the array
    reverse(arr, index);

    # Update tree by taking
    # elements from array
    index = 0;
    index=modifyTree(root, arr,
                     index, 0);

# A utility function to print
# indorder traversal of a
# binary tree
def printInorder(root):

    if(root == None):
        return;
    printInorder(root.left);
    print(root.data, end = ' ')
    printInorder(root.right);

# Driver code
if __name__=="__main__":

    root = newNode('a');
    root.left = newNode('b');
    root.right = newNode('c');
    root.left.left = newNode('d');
    root.left.right = newNode('e');
    root.right.left = newNode('f');
    root.right.right = newNode('g');
    root.left.left.left = newNode('h');
    root.left.left.right = newNode('i');
    root.left.right.left = newNode('j');
    root.left.right.right = newNode('k');
    root.right.left.left = newNode('l');
    root.right.left.right = newNode('m');
    root.right.right.left = newNode('n');
    root.right.right.right = newNode('o');

    print("Inorder Traversal of given tree")
    printInorder(root);

    reverseAlternate(root);

    print("\nInorder Traversal of modified tree")
    printInorder(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# program to reverse alternate
// levels of perfect binary tree
using System;

// A binary tree node
public class Node
{
    public char data;
    public Node left, right;

    public Node(char item)
    {
        data = item;
        left = right = null;
    }
}

// class to access index value
// by reference
public class Index
{
    public int index;
}

class GFG
{
public Node root;
public Index index_obj = new Index();

// function to store alternate
// levels in a tree
public virtual void storeAlternate(Node node, char[] arr,
                                   Index index, int l)
{
    // base case
    if (node == null)
    {
        return;
    }

    // store elements of left subtree
    storeAlternate(node.left, arr, index, l + 1);

    // store this node only if level is odd
    if (l % 2 != 0)
    {
        arr[index.index] = node.data;
        index.index++;
    }

    storeAlternate(node.right, arr, index, l + 1);
}

// Function to modify Binary Tree (All odd
// level nodes are updated by taking elements
// from array in inorder fashion)
public virtual void modifyTree(Node node, char[] arr,
                               Index index, int l)
{

    // Base case
    if (node == null)
    {
        return;
    }

    // Update nodes in left subtree
    modifyTree(node.left, arr, index, l + 1);

    // Update this node only if this
    // is an odd level node
    if (l % 2 != 0)
    {
        node.data = arr[index.index];
        (index.index)++;
    }

    // Update nodes in right subtree
    modifyTree(node.right, arr, index, l + 1);
}

// A utility function to reverse an
// array from index 0 to n-1
public virtual void reverse(char[] arr, int n)
{
    int l = 0, r = n - 1;
    while (l < r)
    {
        char temp = arr[l];
        arr[l] = arr[r];
        arr[r] = temp;
        l++;
        r--;
    }
}

public virtual void reverseAlternate()
{
    reverseAlternate(root);
}

// The main function to reverse
// alternate nodes of a binary tree
public virtual void reverseAlternate(Node node)
{

    // Create an auxiliary array to
    // store nodes of alternate levels
    char[] arr = new char[100];

    // First store nodes of alternate levels
    storeAlternate(node, arr, index_obj, 0);

    //index_obj.index = 0;

    // Reverse the array
    reverse(arr, index_obj.index);

    // Update tree by taking elements from array
    index_obj.index = 0;
    modifyTree(node, arr, index_obj, 0);
}

public virtual void printInorder()
{
    printInorder(root);
}

// A utility function to print indorder
// traversal of a binary tree
public virtual void printInorder(Node node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    Console.Write(node.data + " ");
    printInorder(node.right);
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node('a');
    tree.root.left = new Node('b');
    tree.root.right = new Node('c');
    tree.root.left.left = new Node('d');
    tree.root.left.right = new Node('e');
    tree.root.right.left = new Node('f');
    tree.root.right.right = new Node('g');
    tree.root.left.left.left = new Node('h');
    tree.root.left.left.right = new Node('i');
    tree.root.left.right.left = new Node('j');
    tree.root.left.right.right = new Node('k');
    tree.root.right.left.left = new Node('l');
    tree.root.right.left.right = new Node('m');
    tree.root.right.right.left = new Node('n');
    tree.root.right.right.right = new Node('o');
    Console.WriteLine("Inorder Traversal of given tree");
    tree.printInorder();

    tree.reverseAlternate();
    Console.WriteLine("");
    Console.WriteLine("");
    Console.WriteLine("Inorder Traversal of modified tree");
    tree.printInorder();
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to reverse alternate
// levels of  perfect binary tree
// A binary tree node
 class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }

// class to access index value by reference
 var index = 0;

    // function to store alternate levels in a tree
    function storeAlternate(node,  arr , l) {
        // base case
        if (node == null) {
            return;
        }
        // store elements of left subtree
        storeAlternate(node.left, arr, l + 1);

        // store this node only if level is odd
        if (l % 2 != 0) {
            arr[index] = node.data;
            index++;
        }

        storeAlternate(node.right, arr, l + 1);
    }

    // Function to modify Binary Tree
    // (All odd level nodes are
    // updated by taking elements from
    // array in inorder fashion)
    function modifyTree(node,  arr , l) {

        // Base case
        if (node == null) {
            return;
        }

        // Update nodes in left subtree
        modifyTree(node.left, arr, l + 1);

        // Update this node only if
        // this is an odd level node
        if (l % 2 != 0) {
            node.data = arr[index];
            (index)++;
        }

        // Update nodes in right subtree
        modifyTree(node.right, arr, l + 1);
    }

    // A utility function to reverse an array from index
    // 0 to n-1
    function reverse( arr , n) {
        var l = 0, r = n - 1;
        while (l < r) {
            var temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            l++;
            r--;
        }
    }

    // The main function to reverse
    // alternate nodes of a binary tree
    function reverseAlternate(node) {

        // Create an auxiliary array to store
        // nodes of alternate levels
        var arr = Array(100).fill('');

        // First store nodes of alternate levels
        storeAlternate(node, arr, 0);

         //index_obj.index = 0;

        // Reverse the array
        reverse(arr, index);

        // Update tree by taking elements from array
        index = 0;
        modifyTree(node, arr, 0);
    }

    // A utility function to print
    // indorder traversal of a
    // binary tree
    function printInorder(node) {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        document.write(node.data + " ");
        printInorder(node.right);
    }
 function newNode(key) {
var temp = new Node();
        temp.left = temp.right = null;
        temp.data =  key;
        return temp;
    }
    // Driver program to test the above functions

        var root = newNode('a');
        root.left = newNode('b');
        root.right = newNode('c');
        root.left.left = newNode('d');
        root.left.right = newNode('e');
        root.right.left = newNode('f');
        root.right.right = newNode('g');
        root.left.left.left = newNode('h');
        root.left.left.right = newNode('i');
        root.left.right.left = newNode('j');
        root.left.right.right = newNode('k');
        root.right.left.left = newNode('l');
        root.right.left.right = newNode('m');
        root.right.right.left = newNode('n');
        root.right.right.right = newNode('o');
        document.write("Inorder Traversal of given tree<br/>");
        printInorder(root);

        reverseAlternate(root);
        document.write("<br/>");
        document.write("<br/>");
        document.write("Inorder Traversal of modified tree<br/>");
        printInorder(root);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Inorder Traversal of given tree
h d i b j e k a l f m c n g o

Inorder Traversal of modified tree
o d n c m e l a k f j b i g h
```

上述解决方案的时间复杂度是 O(n)，因为它进行了二叉树的两次有序遍历。

**方法 3(使用一次遍历)**

如果当前节点处于偶数级别，此方法只交换子节点的值。
因为这最终会在奇数层交换元素。
例如给定的例子:

我们发现节点 a，在 0 级上，我们交换节点 a 的左右值。
结果:1 级(奇数)元素被交换。
现在树变成了:

```
      a
    /   \
   c     b
  / \   / \
 ... ... ...
```

这是第一次递归的预期结果。
因此，我们进一步为子元素调用相同的递归函数。

对于递归堆栈，因为这是一个完美的二叉树，它可能是一个普通的二叉树

## C++

```
// C++ program to reverse
// alternate levels of a tree
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    char key;
    Node *left, *right;
};

void preorder(struct Node *root1, struct Node*
                               root2, int lvl)
{
    // Base cases
    if (root1 == NULL || root2==NULL)
        return;

    // Swap subtrees if level is even
    if (lvl%2 == 0)
        swap(root1->key, root2->key);

    // Recur for left and right
    // subtrees (Note : left of root1
    // is passed and right of root2 in
    // first call and opposite
    // in second call.
    preorder(root1->left, root2->right, lvl+1);
    preorder(root1->right, root2->left, lvl+1);
}

// This function calls preorder()
// for left and right children
// of root
void reverseAlternate(struct Node *root)
{
   preorder(root->left, root->right, 0);
}

// Inorder traversal (used to print initial and
// modified trees)
void printInorder(struct Node *root)
{
    if (root == NULL)
       return;
    printInorder(root->left);
    cout << root->key << " ";
    printInorder(root->right);
}

// A utility function to create a new node
Node *newNode(int key)
{
    Node *temp = new Node;
    temp->left = temp->right = NULL;
    temp->key = key;
    return temp;
}

// Driver program to test above functions
int main()
{
    struct Node *root = newNode('a');
    root->left = newNode('b');
    root->right = newNode('c');
    root->left->left = newNode('d');
    root->left->right = newNode('e');
    root->right->left = newNode('f');
    root->right->right = newNode('g');
    root->left->left->left = newNode('h');
    root->left->left->right = newNode('i');
    root->left->right->left = newNode('j');
    root->left->right->right = newNode('k');
    root->right->left->left = newNode('l');
    root->right->left->right = newNode('m');
    root->right->right->left = newNode('n');
    root->right->right->right = newNode('o');

    cout << "Inorder Traversal of given tree\n";
    printInorder(root);

    reverseAlternate(root);

    cout << "\n\nInorder Traversal of modified tree\n";
    printInorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse
// alternate levels of a tree
class Sol
{

    static class Node
    {
        char key;
        Node left, right;
    };

    static void preorder(Node root1,
                       Node root2, int lvl)
    {
        // Base cases
        if (root1 == null || root2 == null)
            return;

        // Swap subtrees if level is even
        if (lvl % 2 == 0) {
            char t = root1.key;
            root1.key = root2.key;
            root2.key = t;
        }

        // Recur for left and right subtrees
        // (Note : left of root1
        // is passed and right of root2 in first
        // call and opposite
        // in second call.
        preorder(root1.left, root2.right,
                                  lvl + 1);
        preorder(root1.right, root2.left,
                                    lvl + 1);
    }

    // This function calls preorder()
    // for left and right
    // children of root
    static void reverseAlternate(Node root)
    {
        preorder(root.left, root.right, 0);
    }

    // Inorder traversal (used to
    // print initial and
    // modified trees)
    static void printInorder(Node root)
    {
        if (root == null)
            return;
        printInorder(root.left);
        System.out.print(root.key + " ");
        printInorder(root.right);
    }

    // A utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.left = temp.right = null;
        temp.key = (char)key;
        return temp;
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        Node root = newNode('a');
        root.left = newNode('b');
        root.right = newNode('c');
        root.left.left = newNode('d');
        root.left.right = newNode('e');
        root.right.left = newNode('f');
        root.right.right = newNode('g');
        root.left.left.left = newNode('h');
        root.left.left.right = newNode('i');
        root.left.right.left = newNode('j');
        root.left.right.right = newNode('k');
        root.right.left.left = newNode('l');
        root.right.left.right = newNode('m');
        root.right.right.left = newNode('n');
        root.right.right.right = newNode('o');

        System.out.print(
            "Inorder Traversal of given tree\n");
        printInorder(root);

        reverseAlternate(root);

        System.out.print(
            "\n\nInorder Traversal of modified tree\n");
        printInorder(root);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to reverse
# alternate levels of a tree

# A Binary Tree Node
# Utility function to create
# a new tree node
class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

def preorder(root1, root2, lvl):

    # Base cases
    if (root1 == None or root2 == None):
        return

    # Swap subtrees if level is even
    if (lvl % 2 == 0):
        t = root1.key
        root1.key = root2.key
        root2.key = t

    # Recur for left and right subtrees
    # (Note : left of root1 is passed and
    # right of root2 in first call and
    # opposite in second call.
    preorder(root1.left, root2.right, lvl + 1)
    preorder(root1.right, root2.left, lvl + 1)

# This function calls preorder()
# for left and right children of root
def reverseAlternate(root):
    preorder(root.left, root.right, 0)

# Inorder traversal (used to print
# initial and modified trees)
def printInorder(root):
    if (root == None):
        return
    printInorder(root.left)
    print( root.key, end = " ")
    printInorder(root.right)

# A utility function to create a new node
def newNode(key):
    temp = Node(' ')
    temp.left = temp.right = None
    temp.key = key
    return temp

# Driver Code
if __name__ == '__main__':
    root = newNode('a')
    root.left = newNode('b')
    root.right = newNode('c')
    root.left.left = newNode('d')
    root.left.right = newNode('e')
    root.right.left = newNode('f')
    root.right.right = newNode('g')
    root.left.left.left = newNode('h')
    root.left.left.right = newNode('i')
    root.left.right.left = newNode('j')
    root.left.right.right = newNode('k')
    root.right.left.left = newNode('l')
    root.right.left.right = newNode('m')
    root.right.right.left = newNode('n')
    root.right.right.right = newNode('o')

    print( "Inorder Traversal of given tree")
    printInorder(root)

    reverseAlternate(root)

    print("\nInorder Traversal of modified tree")
    printInorder(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to reverse alternate
// levels of a tree
using System;

class GFG
{

public class Node
{
    public char key;
    public Node left, right;
};

static void preorder( Node root1,
                       Node root2, int lvl)
{
    // Base cases
    if (root1 == null || root2==null)
        return;

    // Swap subtrees if level is even
    if (lvl % 2 == 0)
        {
            char t = root1.key;
            root1.key = root2.key;
            root2.key = t;
        }

    // Recur for left and right subtrees
    // (Note : left of root1
    // is passed and right of root2 in
    // first call and opposite
    // in second call.
    preorder(root1.left, root2.right, lvl+1);
    preorder(root1.right, root2.left, lvl+1);
}

// This function calls preorder() for left
// and right children
// of root
static void reverseAlternate( Node root)
{
    preorder(root.left, root.right, 0);
}

// Inorder traversal (used to print initial and
// modified trees)
static void printInorder( Node root)
{
    if (root == null)
        return;
    printInorder(root.left);
    Console.Write( root.key + " ");
    printInorder(root.right);
}

// A utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.left = temp.right = null;
    temp.key = (char)key;
    return temp;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode('a');
    root.left = newNode('b');
    root.right = newNode('c');
    root.left.left = newNode('d');
    root.left.right = newNode('e');
    root.right.left = newNode('f');
    root.right.right = newNode('g');
    root.left.left.left = newNode('h');
    root.left.left.right = newNode('i');
    root.left.right.left = newNode('j');
    root.left.right.right = newNode('k');
    root.right.left.left = newNode('l');
    root.right.left.right = newNode('m');
    root.right.right.left = newNode('n');
    root.right.right.right = newNode('o');

    Console.Write("Inorder Traversal of given tree\n");
    printInorder(root);

    reverseAlternate(root);

    Console.Write("\n\nInorder Traversal of modified tree\n");
    printInorder(root);

}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript program to reverse
// alternate levels of a tree
     class Node {
            constructor(val) {
                this.key = val;
                this.left = null;
                this.right = null;
            }
        }
    function preorder(root1,  root2 , lvl)
    {

        // Base cases
        if (root1 == null || root2 == null)
            return;

        // Swap subtrees if level is even
        if (lvl % 2 == 0) {
            var t = root1.key;
            root1.key = root2.key;
            root2.key = t;
        }

        // Recur for left and right subtrees
        // (Note : left of root1
        // is passed and right of root2 in first
        // call and opposite
        // in second call.
        preorder(root1.left, root2.right, lvl + 1);
        preorder(root1.right, root2.left, lvl + 1);
    }

    // This function calls preorder()
    // for left and right
    // children of root
    function reverseAlternate(root) {
        preorder(root.left, root.right, 0);
    }

    // Inorder traversal (used to
    // print initial and
    // modified trees)
    function printInorder(root) {
        if (root == null)
            return;
        printInorder(root.left);
        document.write(root.key + " ");
        printInorder(root.right);
    }

    // A utility function to create a new node
    function newNode(key) {
var temp = new Node();
        temp.left = temp.right = null;
        temp.key =  key;
        return temp;
    }

    // Driver program to test above functions

var root = newNode('a');
        root.left = newNode('b');
        root.right = newNode('c');
        root.left.left = newNode('d');
        root.left.right = newNode('e');
        root.right.left = newNode('f');
        root.right.right = newNode('g');
        root.left.left.left = newNode('h');
        root.left.left.right = newNode('i');
        root.left.right.left = newNode('j');
        root.left.right.right = newNode('k');
        root.right.left.left = newNode('l');
        root.right.left.right = newNode('m');
        root.right.right.left = newNode('n');
        root.right.right.right = newNode('o');

        document.write("Inorder Traversal of given tree<br\>");
        printInorder(root);

        reverseAlternate(root);

        document.write("<br\><br\>Inorder Traversal of modified tree<br\>");
        printInorder(root);

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Inorder Traversal of given tree
h d i b j e k a l f m c n g o 

Inorder Traversal of modified tree
o d n c m e l a k f j b i g h 
```

**时间复杂度:** O(N)

**空间复杂度:** O(log N)
感谢 Soumyajit Bhattacharyay 提出上述解决方案。

本文由**克里帕尔·高拉夫**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。