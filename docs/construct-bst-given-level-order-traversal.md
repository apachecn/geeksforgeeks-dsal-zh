# 根据给定的层级顺序遍历

构建 BST

> 原文:[https://www . geesforgeks . org/construct-BST-给定级别-顺序-遍历/](https://www.geeksforgeeks.org/construct-bst-given-level-order-traversal/)

根据给定的级别顺序遍历来构造 BST(二叉查找树)。
**例:**

```
Input : arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10}
Output : BST: 
        7        
       / \       
      4   12      
     / \  /     
    3  6 8    
   /  /   \
  1   5   10
```

想法是使用递归:-
我们知道，对于所有剩余的元素，第一个元素将始终是树的根，第二个元素将是左子元素，第三个元素将是右子元素(如果落在范围内)，以此类推。
1)首先拾取数组的第一个元素，使其成为根元素。
2)选择第二个元素，如果它的值小于根节点值，则使它成为左子元素，
3)否则使它成为右子元素
4)现在递归调用步骤(2)和步骤(3)从其级别“顺序遍历”中创建一个 BST。
以下是上述方法的实施:

## C++

```
// C++ implementation to construct a BST
// from its level order traversal
#include <bits/stdc++.h>

using namespace std;

// node of a BST
struct Node
{
    int data;
    Node *left, *right;
};

// function to get a new node
Node* getNode(int data)
{
    // Allocate memory
    Node *newNode =
        (Node*)malloc(sizeof(Node));

    // put in the data   
    newNode->data = data;
    newNode->left = newNode->right = NULL;   
    return newNode;
}

// function to construct a BST from
// its level order traversal
Node *LevelOrder(Node *root , int data)
{
     if(root==NULL){   
        root = getNode(data);
        return root;
     }
     if(data <= root->data)
     root->left = LevelOrder(root->left, data);
     else
     root->right = LevelOrder(root->right, data);
     return root;    
}

Node* constructBst(int arr[], int n)
{
    if(n==0)return NULL;
    Node *root =NULL;

    for(int i=0;i<n;i++)
    root = LevelOrder(root , arr[i]);

    return root;
}

// function to print the inorder traversal
void inorderTraversal(Node* root)
{
    if (!root)
        return;

    inorderTraversal(root->left);
    cout << root->data << " ";
    inorderTraversal(root->right);   
}

// Driver program to test above
int main()
{
    int arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10};
    int n = sizeof(arr) / sizeof(arr[0]);

    Node *root = constructBst(arr, n);

    cout << "Inorder Traversal: ";
    inorderTraversal(root);
    return 0;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to construct a BST
// from its level order traversal
class GFG
{

// node of a BST
static class Node
{
    int data;
    Node left, right;
};

// function to get a new node
static Node getNode(int data)
{
    // Allocate memory
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to construct a BST from
// its level order traversal
static Node LevelOrder(Node root , int data)
{
    if(root == null)
    {
        root = getNode(data);
        return root;
    }
    if(data <= root.data)
    root.left = LevelOrder(root.left, data);
    else
    root.right = LevelOrder(root.right, data);
    return root;    
}

static Node constructBst(int arr[], int n)
{
    if(n == 0)return null;
    Node root = null;

    for(int i = 0; i < n; i++)
    root = LevelOrder(root , arr[i]);

    return root;
}

// function to print the inorder traversal
static void inorderTraversal(Node root)
{
    if (root == null)
        return;

    inorderTraversal(root.left);
    System.out.print( root.data + " ");
    inorderTraversal(root.right);
}

// Driver code
public static void main(String args[])
{
    int arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10};
    int n = arr.length;

    Node root = constructBst(arr, n);

    System.out.print( "Inorder Traversal: ");
    inorderTraversal(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation to construct a BST
# from its level order traversal
import math

# node of a BST
class Node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# function to get a new node
def getNode( data):

    # Allocate memory
    newNode = Node(data)

    # put in the data
    newNode.data = data
    newNode.left =None
    newNode.right = None
    return newNode

# function to construct a BST from
# its level order traversal
def LevelOrder(root , data):
    if(root == None):
        root = getNode(data)
        return root

    if(data <= root.data):
        root.left = LevelOrder(root.left, data)
    else:
        root.right = LevelOrder(root.right, data)
    return root    

def constructBst(arr, n):
    if(n == 0):
        return None
    root = None

    for i in range(0, n):
        root = LevelOrder(root , arr[i])

    return root

# function to print the inorder traversal
def inorderTraversal( root):
    if (root == None):
        return None

    inorderTraversal(root.left)
    print(root.data,end = " ")
    inorderTraversal(root.right)

# Driver program
if __name__=='__main__':

    arr = [7, 4, 12, 3, 6, 8, 1, 5, 10]
    n = len(arr)

    root = constructBst(arr, n)

    print("Inorder Traversal: ", end = "")
    root = inorderTraversal(root)

# This code is contributed by Srathore
```

## C#

```
// C# implementation to construct a BST
// from its level order traversal
using System;

class GFG
{

// node of a BST
public class Node
{
    public int data;
    public Node left, right;
};

// function to get a new node
static Node getNode(int data)
{
    // Allocate memory
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to construct a BST from
// its level order traversal
static Node LevelOrder(Node root,
                       int data)
{
    if(root == null)
    {
        root = getNode(data);
        return root;
    }

    if(data <= root.data)
        root.left = LevelOrder(root.left, data);
    else
        root.right = LevelOrder(root.right, data);
    return root;    
}

static Node constructBst(int []arr, int n)
{
    if(n == 0) return null;
    Node root = null;

    for(int i = 0; i < n; i++)
    root = LevelOrder(root, arr[i]);

    return root;
}

// function to print the inorder traversal
static void inorderTraversal(Node root)
{
    if (root == null)
        return;

    inorderTraversal(root.left);
    Console.Write( root.data + " ");
    inorderTraversal(root.right);
}

// Driver code
public static void Main(String []args)
{
    int []arr = {7, 4, 12, 3,
                 6, 8, 1, 5, 10};
    int n = arr.Length;

    Node root = constructBst(arr, n);

    Console.Write("Inorder Traversal: ");
    inorderTraversal(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation to construct a BST
      // from its level order traversal
      // node of a BST
      class Node {
        constructor() {
          this.data = 0;
          this.left = null;
          this.right = null;
        }
      }

      // function to get a new node
      function getNode(data) {
        // Allocate memory
        var newNode = new Node();

        // put in the data
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
      }

      // function to construct a BST from
      // its level order traversal
      function LevelOrder(root, data) {
        if (root == null) {
          root = getNode(data);
          return root;
        }

        if (data <= root.data)
        root.left = LevelOrder(root.left, data);
        else
        root.right = LevelOrder(root.right, data);
        return root;
      }

      function constructBst(arr, n) {
        if (n == 0) return null;
        var root = null;

        for (var i = 0; i < n; i++)
        root = LevelOrder(root, arr[i]);

        return root;
      }

      // function to print the inorder traversal
      function inorderTraversal(root) {
        if (root == null) return;

        inorderTraversal(root.left);
        document.write(root.data + " ");
        inorderTraversal(root.right);
      }

      // Driver code
      var arr = [7, 4, 12, 3, 6, 8, 1, 5, 10];
      var n = arr.length;

      var root = constructBst(arr, n);

      document.write("Inorder Traversal: ");
      inorderTraversal(root);

</script>
```

**输出:**

```
Inorder Traversal: 1 3 4 5 6 7 8 10 12
```

**时间复杂度** : O(n <sup>2</sup> )
这是因为上面的程序就像我们在一个 bst 中插入 n 个节点，在最坏的情况下需要 O(n <sup>2</sup> )个时间。
本文由**尼尚·巴拉扬**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。