# 二叉树的简洁编码

> 原文:[https://www . geesforgeks . org/binary-encoding-of-二叉树/](https://www.geeksforgeeks.org/succinct-encoding-of-binary-tree/)

二叉树的简洁编码占用了接近最小的可能空间。n 个节点上结构不同的二叉树的个数为[第 n 个加泰罗尼亚数](https://www.geeksforgeeks.org/program-nth-catalan-number/)。对于大 n，这大约是 4<sup>n</sup>；因此，我们至少需要大约 log <sub>2</sub> 4 <sup>n</sup> = 2n 位来编码它。因此，简洁的二叉树将占用 2n+o(n)位。

满足这一界限的一种简单表示是按顺序访问树的节点，内部节点输出“1”，叶子输出“0”。如果树包含数据，我们可以简单地同时将它存储在一个连续的数组中。

下面是编码算法:

```
function EncodeSuccinct(node n, bitstring structure, array data) {
    if n = nil then
        append 0 to structure;
    else
        append 1 to structure;
        append n.data to data;
        EncodeSuccinct(n.left, structure, data);
        EncodeSuccinct(n.right, structure, data);
}
```

下面是解码算法

```
function DecodeSuccinct(bitstring structure, array data) {
    remove first bit of structure and put it in b
    if b = 1 then
        create a new node n
        remove first element of data and put it in n.data
        n.left = DecodeSuccinct(structure, data)
        n.right = DecodeSuccinct(structure, data)
        return n
    else
        return nil
}
```

来源:[https://en . Wikipedia . org/wiki/Binary _ tree #简洁 _ 编码](https://en.wikipedia.org/wiki/Binary_tree#Succinct_encodings)
示例:

```
Input:   
        10
     /      \
   20       30
  /  \        \
 40   50      70 

Data Array (Contains preorder traversal)
10 20 40 50 30 70

Structure Array
1 1 1 0 0 1 0 0 1 0 1 0 0 
1 indicates data and 0 indicates NULL
```

下面是上述算法的实现。

## C++

```
// C++ program to demonstrate Succinct Tree Encoding and decoding
#include<bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int key;
    struct Node* left, *right;
};

// Utility function to create new Node
Node *newNode(int key)
{
    Node *temp = new Node;
    temp->key  = key;
    temp->left  = temp->right = NULL;
    return (temp);
}

// This function fills lists 'struc' and 'data'.  'struc' list
// stores structure information. 'data' list stores tree data
void EncodeSuccinct(Node *root, list<bool> &struc, list<int> &data)
{
    // If root is NULL, put 0 in structure array and return
    if (root == NULL)
    {
        struc.push_back(0);
        return;
    }

    // Else place 1 in structure array, key in 'data' array
    // and recur for left and right children
    struc.push_back(1);
    data.push_back(root->key);
    EncodeSuccinct(root->left, struc, data);
    EncodeSuccinct(root->right, struc, data);
}

// Constructs tree from 'struc' and 'data'
Node *DecodeSuccinct(list<bool> &struc, list<int> &data)
{
    if (struc.size() <= 0)
        return NULL;

    // Remove one item from structure list
    bool b = struc.front();
    struc.pop_front();

    // If removed bit is 1,
    if (b == 1)
    {
         // remove an item from data list
        int key = data.front();
        data.pop_front();

        // Create a tree node with the removed data
        Node *root = newNode(key);

        // And recur to create left and right subtrees
        root->left = DecodeSuccinct(struc, data);
        root->right = DecodeSuccinct(struc, data);
        return root;
    }

    return NULL;
}

// A utility function to print tree
void preorder(Node* root)
{
    if (root)
    {
        cout << "key: "<< root->key;
        if (root->left)
            cout << " | left child: " << root->left->key;
        if (root->right)
            cout << " | right child: " << root->right->key;
        cout << endl;
        preorder(root->left);
        preorder(root->right);
    }
}

// Driver program
int main()
{
    // Let us construct the Tree shown in the above figure
    Node *root         = newNode(10);
    root->left         = newNode(20);
    root->right        = newNode(30);
    root->left->left   = newNode(40);
    root->left->right  = newNode(50);
    root->right->right = newNode(70);

    cout << "Given Tree\n";
    preorder(root);
    list<bool> struc;
    list<int>  data;
    EncodeSuccinct(root, struc, data);

    cout << "\nEncoded Tree\n";
    cout << "Structure List\n";
    list<bool>::iterator si; // Structure iterator
    for (si = struc.begin(); si != struc.end(); ++si)
        cout << *si << " ";

    cout << "\nData List\n";
    list<int>::iterator di; // Data iIterator
    for (di = data.begin(); di != data.end(); ++di)
        cout << *di << " ";

    Node *newroot = DecodeSuccinct(struc, data);

    cout << "\n\nPreorder traversal of decoded tree\n";
    preorder(newroot);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate Succinct
// Tree Encoding and decoding
import java.util.*;

class GFG{

// A Binary Tree Node
static class Node
{
    int key;
    Node left, right;
};

// Utility function to create new Node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key  = key;
    temp.left  = temp.right = null;
    return (temp);
}

static Vector<Boolean> struc;
static Vector<Integer> data;
static Node root;

// This function fills lists 'struc' and
// 'data'. 'struc' list stores structure
// information. 'data' list stores tree data
static void EncodeSuccinct(Node root)
{

    // If root is null, put 0 in
    // structure array and return
    if (root == null)
    {
        struc.add(false);
        return;
    }

    // Else place 1 in structure array,
    // key in 'data' array and recur
    // for left and right children
    struc.add(true);
    data.add(root.key);
    EncodeSuccinct(root.left);
    EncodeSuccinct(root.right);
}

// Constructs tree from 'struc' and 'data'
static Node DecodeSuccinct()
{
    if (struc.size() <= 0)
        return null;

    // Remove one item from structure list
    boolean b = struc.get(0);
    struc.remove(0);

    // If removed bit is 1,
    if (b == true)
    {

        // Remove an item from data list
        int key = data.get(0);
        data.remove(0);

        // Create a tree node with the
        // removed data
        Node root = newNode(key);

        // And recur to create left and
        // right subtrees
        root.left = DecodeSuccinct();
        root.right = DecodeSuccinct();
        return root;
    }
    return null;
}

// A utility function to print tree
static void preorder(Node root)
{
    if (root != null)
    {
        System.out.print("key: "+ root.key);
        if (root.left != null)
            System.out.print(" | left child: " + 
                             root.left.key);
        if (root.right != null)
            System.out.print(" | right child: " + 
                             root.right.key);
        System.out.println();

        preorder(root.left);
        preorder(root.right);
    }
}

// Driver code
public static void main(String[] args)
{

    // Let us construct Tree shown in
    // the above figure
    Node root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);
    root.left.left = newNode(40);
    root.left.right = newNode(50);
    root.right.right = newNode(70);

    System.out.print("Given Tree\n");
    preorder(root);
    struc = new Vector<>();
    data = new Vector<>();
    EncodeSuccinct(root);

    System.out.print("\nEncoded Tree\n");
    System.out.print("Structure List\n");

    for(boolean  si : struc)
    {
        if (si == true)
            System.out.print(1 + " ");
        else
            System.out.print(0 + " ");
    }

    System.out.print("\nData List\n");
    for(int di : data)
        System.out.print(di + " ");

    Node newroot = DecodeSuccinct();

    System.out.print("\n\nPreorder traversal" +
                     "of decoded tree\n");

    preorder(newroot);
}
}

// This code is contributed by aashish1995
```

## 计算机编程语言

```
# Python program to demonstrate Succinct Tree Encoding and Decoding

# Node structure
class Node:
    # Utility function to create new Node
    def __init__(self , key):
        self.key = key
        self.left = None
        self.right = None

def EncodeSuccint(root , struc , data):

    # If root is None , put 0 in structure array and return
    if root is None :
        struc.append(0)
        return

    # Else place 1 in structure array, key in 'data' array
    # and recur for left and right children
    struc.append(1)
    data.append(root.key)
    EncodeSuccint(root.left , struc , data)
    EncodeSuccint(root.right , struc ,data)

# Constructs tree from 'struc' and 'data'
def DecodeSuccinct(struc , data):
    if(len(struc) <= 0):
        return None

    # Remove one item from structure list
    b = struc[0]
    struc.pop(0)

    # If removed bit is 1
    if b == 1:
        key = data[0]
        data.pop(0)

        #Create a tree node with removed data
        root = Node(key)

        #And recur to create left and right subtrees
        root.left = DecodeSuccinct(struc , data);
        root.right = DecodeSuccinct(struc , data);
        return root

    return None

def preorder(root):
    if root is not None:
        print "key: %d" %(root.key),

        if root.left is not None:
            print "| left child: %d" %(root.left.key),
        if root.right is not None:
            print "| right child %d" %(root.right.key),
        print ""
        preorder(root.left)
        preorder(root.right)

# Driver Program
root = Node(10)
root.left = Node(20)
root.right = Node(30)
root.left.left = Node(40)
root.left.right = Node(50)
root.right.right = Node(70)        

print "Given Tree"
preorder(root)
struc = []
data = []
EncodeSuccint(root , struc , data)

print "\nEncoded Tree"
print "Structure List"

for i in struc:
    print i ,

print "\nDataList"
for value in data:
    print value,

newroot = DecodeSuccinct(struc , data)

print "\n\nPreorder Traversal of decoded tree"
preorder(newroot)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to demonstrate Succinct
// Tree Encoding and decoding
using System;
using System.Collections.Generic;
class GFG{

  // A Binary Tree Node
  public
    class Node
    {
      public
        int key;
      public
        Node left, right;
    };

  // Utility function to create new Node
  static Node newNode(int key)
  {
    Node temp = new Node();
    temp.key  = key;
    temp.left  = temp.right = null;
    return (temp);
  }
  static List<Boolean> struc;
  static List<int> data;
  static Node root;

  // This function fills lists 'struc' and
  // 'data'. 'struc' list stores structure
  // information. 'data' list stores tree data
  static void EncodeSuccinct(Node root)
  {

    // If root is null, put 0 in
    // structure array and return
    if (root == null)
    {
      struc.Add(false);
      return;
    }

    // Else place 1 in structure array,
    // key in 'data' array and recur
    // for left and right children
    struc.Add(true);
    data.Add(root.key);
    EncodeSuccinct(root.left);
    EncodeSuccinct(root.right);
  }

  // Constructs tree from 'struc' and 'data'
  static Node DecodeSuccinct()
  {
    if (struc.Count <= 0)
      return null;

    // Remove one item from structure list
    bool b = struc[0];
    struc.RemoveAt(0);

    // If removed bit is 1,
    if (b == true)
    {

      // Remove an item from data list
      int key = data[0];
      data.Remove(0);

      // Create a tree node with the
      // removed data
      Node root = newNode(key);

      // And recur to create left and
      // right subtrees
      root.left = DecodeSuccinct();
      root.right = DecodeSuccinct();
      return root;
    }
    return null;
  }

  // A utility function to print tree
  static void preorder(Node root)
  {
    if (root != null)
    {
      Console.Write("key: "+ root.key);
      if (root.left != null)
        Console.Write(" | left child: " + 
                      root.left.key);
      if (root.right != null)
        Console.Write(" | right child: " + 
                      root.right.key);
      Console.WriteLine();
      preorder(root.left);
      preorder(root.right);
    }
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Let us construct Tree shown in
    // the above figure
    Node root = newNode(10);
    root.left = newNode(20);
    root.right = newNode(30);
    root.left.left = newNode(40);
    root.left.right = newNode(50);
    root.right.right = newNode(70);
    Console.Write("Given Tree\n");
    preorder(root);
    struc = new List<Boolean>();
    data = new List<int>();
    EncodeSuccinct(root);
    Console.Write("\nEncoded Tree\n");
    Console.Write("Structure List\n");
    foreach(bool  si in struc)
    {
      if (si == true)
        Console.Write(1 + " ");
      else
        Console.Write(0 + " ");
    }

    Console.Write("\nData List\n");
    foreach(int di in data)
      Console.Write(di + " ");
    Node newroot = DecodeSuccinct();
    Console.Write("\n\nPreorder traversal" +
                  "of decoded tree\n");                    
    preorder(newroot);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to demonstrate Succinct
// Tree Encoding and decoding
// A Binary Tree Node
class Node
{
  constructor()
  {
    this.key = 0;
    this.left = null;
    this.right = null;
  }
};

// Utility function to create new Node
function newNode(key)
{
  var temp = new Node();
  temp.key  = key;
  temp.left  = temp.right = null;
  return (temp);
}

var struc = [];
var data = [];
var root = null;

// This function fills lists 'struc' and
// 'data'. 'struc' list stores structure
// information. 'data' list stores tree data
function EncodeSuccinct(root)
{

  // If root is null, put 0 in
  // structure array and return
  if (root == null)
  {
    struc.push(false);
    return;
  }

  // Else place 1 in structure array,
  // key in 'data' array and recur
  // for left and right children
  struc.push(true);
  data.push(root.key);
  EncodeSuccinct(root.left);
  EncodeSuccinct(root.right);
}

// Constructs tree from 'struc' and 'data'
function DecodeSuccinct()
{
  if (struc.length <= 0)
    return null;

  // Remove one item from structure list
  var b = struc[0];
  struc.shift(0);

  // If removed bit is 1,
  if (b == true)
  {

    // Remove an item from data list
    var key = data[0];
    data.shift();

    // Create a tree node with the
    // removed data
    var root = newNode(key);

    // And recur to create left and
    // right subtrees
    root.left = DecodeSuccinct();
    root.right = DecodeSuccinct();
    return root;
  }
  return null;
}

// A utility function to print tree
function preorder(root)
{
  if (root != null)
  {
    document.write("key: "+ root.key);
    if (root.left != null)
      document.write(" | left child: " + 
                    root.left.key);
    if (root.right != null)
      document.write(" | right child: " + 
                    root.right.key);
    document.write("<br>");
    preorder(root.left);
    preorder(root.right);
  }
}

// Driver code
// Let us construct Tree shown in
// the above figure
var root = newNode(10);
root.left = newNode(20);
root.right = newNode(30);
root.left.left = newNode(40);
root.left.right = newNode(50);
root.right.right = newNode(70);
document.write("Given Tree<br>");
preorder(root);
struc = [];
data = [];
EncodeSuccinct(root);
document.write("<br>Encoded Tree<br>");
document.write("Structure List<br>");
for(var si of struc)
{
  if (si == true)
    document.write(1 + " ");
  else
    document.write(0 + " ");
}
document.write("<br>Data List<br>");
for(var di of data)
  document.write(di + " ");
var newroot = DecodeSuccinct();
document.write("<br><br>Preorder traversal" +
              "of decoded tree<br>");                    
preorder(newroot);

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Given Tree
key: 10 | left child: 20 | right child: 30
key: 20 | left child: 40 | right child: 50
key: 40
key: 50
key: 30 | right child: 70
key: 70

Encoded Tree
Structure List
1 1 1 0 0 1 0 0 1 0 1 0 0 
Data List
10 20 40 50 30 70 

Preorder traversal of decoded tree
key: 10 | left child: 20 | right child: 30
key: 20 | left child: 40 | right child: 50
key: 40
key: 50
key: 30 | right child: 70
key: 70
```

本文由 **Shivam** 投稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息