# 将 BST 转换为最小堆

> 原文:[https://www.geeksforgeeks.org/convert-bst-min-heap/](https://www.geeksforgeeks.org/convert-bst-min-heap/)

给定一个二叉查找树，它也是一个完整的二叉树。问题是将给定的 BST 转换成 Min Heap，条件是一个节点的左子树中的所有值都应该小于该节点的右子树中的所有值。该条件应用于如此转换的最小堆中的所有节点。
**例:**

```
Input :          4
               /   \
              2     6
            /  \   /  \
           1   3  5    7  

Output :        1
              /   \
             2     5
           /  \   /  \
          3   4  6    7 

The given BST has been transformed into a
Min Heap.
All the nodes in the Min Heap satisfies the given
condition, that is, values in the left subtree of
a node should be less than the values in the right
subtree of the node. 
```

1.  创建一个大小为 **n** 的数组 **arr[]** ，其中 n 是给定 BST 中的节点数。
2.  执行 BST 的有序遍历，并按排序顺序复制**arr【】**中的节点值。
3.  现在执行树的前序遍历。
4.  在前序遍历过程中遍历根时，将数组**中的值逐个复制到节点中。**

## C++

```
// C++ implementation to convert the given
// BST to Min Heap
#include <bits/stdc++.h>
using namespace std;

// structure of a node of BST
struct Node
{
    int data;
    Node *left, *right;
};

/* Helper function that allocates a new node
   with the given data and NULL left and right
   pointers. */
struct Node* getNode(int data)
{
    struct Node *newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// function prototype for preorder traversal
// of the given tree
void preorderTraversal(Node*);

// function for the inorder traversal of the tree
// so as to store the node values in 'arr' in
// sorted order
void inorderTraversal(Node *root, vector<int>& arr)
{
    if (root == NULL)
        return;

    // first recur on left subtree
    inorderTraversal(root->left, arr);

    // then copy the data of the node
    arr.push_back(root->data);

    // now recur for right subtree
    inorderTraversal(root->right, arr);
}

// function to convert the given BST to MIN HEAP
// performs preorder traversal of the tree
void BSTToMinHeap(Node *root, vector<int> arr, int *i)
{
    if (root == NULL)
        return;

    // first copy data at index 'i' of 'arr' to
    // the node
    root->data = arr[++*i];

    // then recur on left subtree
    BSTToMinHeap(root->left, arr, i);

    // now recur on right subtree
    BSTToMinHeap(root->right, arr, i);
}

// utility function to convert the given BST to
// MIN HEAP
void convertToMinHeapUtil(Node *root)
{
    // vector to store the data of all the
    // nodes of the BST
    vector<int> arr;
    int i = -1;

    // inorder traversal to populate 'arr'
    inorderTraversal(root, arr);

    // BST to MIN HEAP conversion
    BSTToMinHeap(root, arr, &i);
}

// function for the preorder traversal of the tree
void preorderTraversal(Node *root)
{
    if (!root)
        return;

    // first print the root's data
    cout << root->data << " ";

    // then recur on left subtree
    preorderTraversal(root->left);

    // now recur on right subtree
    preorderTraversal(root->right);
}

// Driver program to test above
int main()
{
    // BST formation
    struct Node *root = getNode(4);
    root->left = getNode(2);
    root->right = getNode(6);
    root->left->left = getNode(1);
    root->left->right = getNode(3);
    root->right->left = getNode(5);
    root->right->right = getNode(7);

    convertToMinHeapUtil(root);
    cout << "Preorder Traversal:" << endl;
    preorderTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to convert the given
// BST to Min Heap
import java.util.ArrayList;

class Gfg {

    static class Node{

        int data;
        Node left,right;

        // Constructor
        Node(){
            this.data = 0;
            this.left = this.right = null;
        }

        Node(int data)
        {
            this.data = data;
            this.left = this.right = null;

        }
    }

    private static void preOrder(Node root)
    {
        if(root==null)
            return ;
        System.out.print(root.data + " ");
        preOrder(root.left);
        preOrder(root.right);
    }

    private static void bstToArray(Node root, ArrayList<Integer> arr){
       // ArrayLIst stores elements in inorder fashion
        if(root==null)
            return;

            bstToArray(root.left, arr);

            arr.add(root.data);

            bstToArray(root.right, arr);

    }

    static int  index = 0;
    private static void arrToMinHeap(Node root, ArrayList<Integer> arr){
        if(root== null)
            return;
        root.data = arr.get(index++);

        arrToMinHeap(root.left, arr);
        arrToMinHeap(root.right, arr);

    }
    static void convertToMinHeap(Node root)
    {
        ArrayList<Integer> arr = new ArrayList<Integer>();
        bstToArray(root, arr);

        arrToMinHeap(root,arr);

    }

// Driver program to test above
public static void main(String[] args)
{

    // BST formation
    Node root = new Node(4);
    root.left = new Node(2);
    root.right = new Node(6);
    root.left.left = new Node(1);
    root.left.right = new Node(3);
    root.right.left = new Node(5);
    root.right.right = new Node(7);

    System.out.print("Preorder Traversal Before Conversion :" +"\n");
    preOrder(root);
    convertToMinHeap(root);

    System.out.print("\nPreorder Traversal After Conversion :" +"\n");
    preOrder(root);

    }
}

// Contributed by : @mahi_07

/*
Tip : If interviewer ask not to use global index variable you can use LinkedList Instead of ArrayList
    and  use LinkedList's removeFirst() method
    So instead of this
        root.data = arr.get(index++);
    you can write
        root.data = list.removeFirst();  
    Do not forget to initialize list in converttoMinHeap function
*/
```

## 蟒蛇 3

```
# C++ implementation to convert the
# given BST to Min Heap

# structure of a node of BST
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function for the inorder traversal
# of the tree so as to store the node
# values in 'arr' in sorted order
def inorderTraversal(root, arr):
    if root == None:
        return

    # first recur on left subtree
    inorderTraversal(root.left, arr)

    # then copy the data of the node
    arr.append(root.data)

    # now recur for right subtree
    inorderTraversal(root.right, arr)

# function to convert the given
# BST to MIN HEAP performs preorder
# traversal of the tree
def BSTToMinHeap(root, arr, i):
    if root == None:
        return

    # first copy data at index 'i' of
    # 'arr' to the node
    i[0] += 1
    root.data = arr[i[0]]

    # then recur on left subtree
    BSTToMinHeap(root.left, arr, i)

    # now recur on right subtree
    BSTToMinHeap(root.right, arr, i)

# utility function to convert the
# given BST to MIN HEAP
def convertToMinHeapUtil(root):

    # vector to store the data of
    # all the nodes of the BST
    arr = []
    i = [-1]

    # inorder traversal to populate 'arr'
    inorderTraversal(root, arr);

    # BST to MIN HEAP conversion
    BSTToMinHeap(root, arr, i)

# function for the preorder traversal
# of the tree
def preorderTraversal(root):
    if root == None:
        return

    # first print the root's data
    print(root.data, end = " ")

    # then recur on left subtree
    preorderTraversal(root.left)

    # now recur on right subtree
    preorderTraversal(root.right)

# Driver Code
if __name__ == '__main__':

    # BST formation
    root = Node(4)
    root.left = Node(2)
    root.right = Node(6)
    root.left.left = Node(1)
    root.left.right = Node(3)
    root.right.left = Node(5)
    root.right.right = Node(7)

    convertToMinHeapUtil(root)
    print("Preorder Traversal:")
    preorderTraversal(root)

# This code is contributed
# by PranchalK
```

## C#

```
// C# implementation to convert the given
// BST to Min Heap
using System;
using System.Collections.Generic;
public class GFG
{

// structure of a node of BST
public

 class Node
{
    public
 int data;
    public
 Node left, right;
};

/* Helper function that allocates a new node
   with the given data and null left and right
   pointers. */
static Node getNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function prototype for preorder traversal
// of the given tree

// function for the inorder traversal of the tree
// so as to store the node values in 'arr' in
// sorted order
static void inorderTraversal(Node root)
{
    if (root == null)
        return;

    // first recur on left subtree
    inorderTraversal(root.left);

    // then copy the data of the node
    arr.Add(root.data);

    // now recur for right subtree
    inorderTraversal(root.right);
}

// function to convert the given BST to MIN HEAP
// performs preorder traversal of the tree
static void BSTToMinHeap(Node root)
{
    if (root == null)
        return;

    // first copy data at index 'i' of 'arr' to
    // the node
    root.data = arr[++i];

    // then recur on left subtree
    BSTToMinHeap(root.left);

    // now recur on right subtree
    BSTToMinHeap(root.right);
}
static  List<int> arr = new List<int>();
static int i;

// utility function to convert the given BST to
// MIN HEAP
static void convertToMinHeapUtil(Node root)
{

    // vector to store the data of all the
    // nodes of the BST
     i = -1;

    // inorder traversal to populate 'arr'
    inorderTraversal(root);

    // BST to MIN HEAP conversion
    BSTToMinHeap(root);
}

// function for the preorder traversal of the tree
static void preorderTraversal(Node root)
{
    if (root == null)
        return;

    // first print the root's data
    Console.Write(root.data + " ");

    // then recur on left subtree
    preorderTraversal(root.left);

    // now recur on right subtree
    preorderTraversal(root.right);
}

// Driver program to test above
public static void Main(String[] args)
{

    // BST formation
    Node root = getNode(4);
    root.left = getNode(2);
    root.right = getNode(6);
    root.left.left = getNode(1);
    root.left.right = getNode(3);
    root.right.left = getNode(5);
    root.right.right = getNode(7);

    convertToMinHeapUtil(root);
    Console.Write("Preorder Traversal:" +"\n");
    preorderTraversal(root);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation to convert the given
      // BST to Min Heap
      // structure of a node of BST
      class Node {
        constructor() {
          this.data = 0;
          this.left = null;
          this.right = null;
        }
      }

      /* Helper function that allocates a new node
      with the given data and null left and right
      pointers. */
      function getNode(data) {
        var newNode = new Node();
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
      }

      // function prototype for preorder traversal
      // of the given tree

      // function for the inorder traversal of the tree
      // so as to store the node values in 'arr' in
      // sorted order
      function inorderTraversal(root) {
        if (root == null) return;

        // first recur on left subtree
        inorderTraversal(root.left);

        // then copy the data of the node
        arr.push(root.data);

        // now recur for right subtree
        inorderTraversal(root.right);
      }

      // function to convert the given BST to MIN HEAP
      // performs preorder traversal of the tree
      function BSTToMinHeap(root) {
        if (root == null) return;

        // first copy data at index 'i' of 'arr' to
        // the node
        root.data = arr[++i];

        // then recur on left subtree
        BSTToMinHeap(root.left);

        // now recur on right subtree
        BSTToMinHeap(root.right);
      }
      var arr = [];
      var i;

      // utility function to convert the given BST to
      // MIN HEAP
      function convertToMinHeapUtil(root) {
        // vector to store the data of all the
        // nodes of the BST
        i = -1;

        // inorder traversal to populate 'arr'
        inorderTraversal(root);

        // BST to MIN HEAP conversion
        BSTToMinHeap(root);
      }

      // function for the preorder traversal of the tree
      function preorderTraversal(root) {
        if (root == null) {
          return;
        }

        // first print the root's data
        document.write(root.data + " ");

        // then recur on left subtree
        preorderTraversal(root.left);

        // now recur on right subtree
        preorderTraversal(root.right);
      }

      // Driver program to test above
      // BST formation
      var root = getNode(4);
      root.left = getNode(2);
      root.right = getNode(6);
      root.left.left = getNode(1);
      root.left.right = getNode(3);
      root.right.left = getNode(5);
      root.right.right = getNode(7);

      convertToMinHeapUtil(root);
      document.write("Preorder Traversal:" + "<br>");
      preorderTraversal(root);

</script>
```

**输出:**

```
Preorder Traversal:
1 2 3 4 5 6 7
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。