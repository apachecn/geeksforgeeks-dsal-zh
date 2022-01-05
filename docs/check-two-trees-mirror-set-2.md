# 检查两棵树是否镜像|设置 2

> 原文:[https://www.geeksforgeeks.org/check-two-trees-mirror-set-2/](https://www.geeksforgeeks.org/check-two-trees-mirror-set-2/)

给定两个二叉树，如果两个树是彼此的镜像，则返回真，否则返回假。

**镜树:**

![](img/1d400b3adab5b9fbd195ed41164fa688.png)

[前面讨论的方法在这里。](https://www.geeksforgeeks.org/check-if-two-trees-are-mirror/)

**方法:**
找到两个二叉树的有序遍历，检查一个遍历是否与另一个遍历相反。如果它们彼此相反，那么树木就是彼此的镜子，否则就不是。

## C++

```
// C++ code to check two binary trees are
// mirror.
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    Node* left, *right;
};

// inorder traversal of Binary Tree
void inorder(Node *n, vector<int> &v)
{
    if (n->left != NULL)
    inorder(n->left, v);       
    v.push_back(n->data);   
    if (n->right != NULL)
    inorder(n->right, v);
}

// Checking if binary tree is mirror
// of each other or not.
bool areMirror(Node* a, Node* b)
{
  if (a == NULL && b == NULL)
    return true;   
  if (a == NULL || b== NULL)
    return false;

  // Storing inorder traversals of both
  // the trees.
  vector<int> v1, v2;
  inorder(a, v1);
  inorder(b, v2);

  if (v1.size() != v2.size())
     return false;

  // Comparing the two arrays, if they
  // are reverse then return 1, else 0
  for (int i=0, j=v2.size()-1; j >= 0;
                             i++, j--)

      if (v1[i] != v2[j])
        return false;   

  return true;
}

// Helper function to allocate a new node
Node* newNode(int data)
{
  Node* node = new Node;
  node->data  = data;
  node->left  =  node->right  = NULL;

  return(node);
}

// Driver code
int main()
{
  Node *a = newNode(1);
  Node *b = newNode(1);

  a -> left = newNode(2);
  a -> right = newNode(3);
  a -> left -> left  = newNode(4);
  a -> left -> right = newNode(5);

  b -> left = newNode(3);
  b -> right = newNode(2);
  b -> right -> left = newNode(5);
  b -> right -> right = newNode(4);

  areMirror(a, b)? cout << "Yes" : cout << "No";

  return 0;
}
```

## 蟒蛇 3

```
# Python3 code to check two binary trees are
# mirror.
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# inorder traversal of Binary Tree
def inorder(n, v):

    if (n.left != None):
        inorder(n.left, v);       
    v.append(n.data);   
    if (n.right != None):
        inorder(n.right, v);

# Checking if binary tree is mirror
# of each other or not.
def areMirror(a, b):

    if (a == None and b == None):
        return True;   
    if (a == None or b== None):
        return False;

    # Storing inorder traversals of both
    # the trees.
    v1 = []
    v2 = []
    inorder(a, v1);
    inorder(b, v2);

    if (len(v1) != len(v2)):
       return False;

    # Comparing the two arrays, if they
    # are reverse then return 1, else 0
    i = 0
    j = len(v2) - 1

    while j >= 0:

        if (v1[i] != v2[j]):
            return False
        i+=1
        j-=1

    return True;

# Helper function to allocate a new node
def newNode(data):
    node = Node(data)
    return node

# Driver code
if __name__=="__main__":
    a = newNode(1);
    b = newNode(1);

    a.left = newNode(2);
    a.right = newNode(3);
    a.left.left  = newNode(4);
    a.left.right = newNode(5);

    b.left = newNode(3);
    b.right = newNode(2);
    b.right.left = newNode(5);
    b.right.right = newNode(4);

    if areMirror(a, b):
        print("Yes")
    else:
        print("No")

# This code is contributed by rutvik_56
```

## C#

```
// C# code to check two binary trees are
// mirror.
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

class Node
{
    public int data;
    public Node left, right;
};

// inorder traversal of Binary Tree
static void inorder(Node n, ref List<int> v)
{
    if (n.left != null)
        inorder(n.left, ref v);

    v.Add(n.data);   

    if (n.right != null)
        inorder(n.right, ref v);
}

// Checking if binary tree is mirror
// of each other or not.
static bool areMirror(Node a, Node b)
{
    if (a == null && b == null)
        return true;   
    if (a == null || b == null)
        return false;

    // Storing inorder traversals of both
    // the trees.
    List<int> v1 = new List<int>();
    List<int> v2 = new List<int>();

    inorder(a, ref v1);
    inorder(b, ref v2);

    if (v1.Count != v2.Count)
        return false;

    // Comparing the two arrays, if they
    // are reverse then return 1, else 0
    for(int i = 0, j = v2.Count - 1; j >= 0;
            i++, j--)

    if (v1[i] != v2[j])
        return false;   

    return true;
}

// Helper function to allocate a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// Driver code
static void Main(string []args)
{
    Node a = newNode(1);
    Node b = newNode(1);

    a.left = newNode(2);
    a.right = newNode(3);
    a.left.left  = newNode(4);
    a.left.right = newNode(5);

    b.left = newNode(3);
    b.right = newNode(2);
    b.right.left = newNode(5);
    b.right.right = newNode(4);

    if (areMirror(a, b))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// JavaScript code to check two binary trees are
// mirror.

class Node
{
   constructor()
   {
     this.data = 0;
     this.left = null;
     this.right = null;
   }
};

// inorder traversal of Binary Tree
function inorder(n, v)
{
    if (n.left != null)
        inorder(n.left, v);

    v.push(n.data);   

    if (n.right != null)
        inorder(n.right, v);
}

// Checking if binary tree is mirror
// of each other or not.
function areMirror(a, b)
{
    if (a == null && b == null)
        return true;   
    if (a == null || b == null)
        return false;

    // Storing inorder traversals of both
    // the trees.
    var v1 = [];
    var v2 = [];

    inorder(a, v1);
    inorder(b, v2);

    if (v1.length != v2.length)
        return false;

    // Comparing the two arrays, if they
    // are reverse then return 1, else 0
    for(var i = 0, j = v2.length - 1; j >= 0;
            i++, j--)

    if (v1[i] != v2[j])
        return false;   

    return true;
}

// Helper function to allocate a new node
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// Driver code
var a = newNode(1);
var b = newNode(1);

a.left = newNode(2);
a.right = newNode(3);
a.left.left  = newNode(4);
a.left.right = newNode(5);

b.left = newNode(3);
b.right = newNode(2);
b.right.left = newNode(5);
b.right.right = newNode(4);

if (areMirror(a, b))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

</script>
```

**输出:**

```
Yes
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。