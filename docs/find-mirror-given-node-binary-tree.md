# 在二叉树中找到给定节点的镜像

> 原文:[https://www . geesforgeks . org/find-mirror-给定-节点-二叉树/](https://www.geeksforgeeks.org/find-mirror-given-node-binary-tree/)

给定一棵二叉树，问题是找到给定节点的镜像。节点的镜像是存在于根的相对子树中该节点的镜像位置的节点。

**例:**

![mirror_nodes](img/49180a4311854c574e8be20bda1bacef.png)

```
In above tree-
Node 2 and 3 are mirror nodes
Node 4 and 6 are mirror nodes. 
```

我们可以有一个寻找镜像节点的递归解决方案。算法如下–

```
1) Start from the root of the tree and recur 
   nodes from both subtree simultaneously 
   using two pointers for left and right nodes.
2) First recur all the external nodes and 
   store returned value in mirror variable.
3) If current node value is equal to target node, 
   return the value of opposite pointer else 
   repeat step 2.
4) If no external node is left and mirror is 
   none, recur internal nodes.
```

## C++

```
// C++ program to find the mirror Node
// in Binary tree
#include <bits/stdc++.h>

using namespace std;

/* A binary tree Node has data,
pointer to left child and
a pointer to right child */
struct Node
{
    int key;
    struct Node* left, *right;
};

// create new Node and initialize it
struct Node* newNode(int key)
{
    struct Node* n = (struct Node*)
                      malloc(sizeof(struct Node*));
    if (n != NULL)
    {
        n->key = key;
        n->left = NULL;
        n->right = NULL;
        return n;
    }
    else
    {
        cout << "Memory allocation failed!"
             << endl;
        exit(1);
    }
}

// recursive function to find mirror of Node
int findMirrorRec(int target, struct Node* left,
                              struct Node* right)
{
    /* if any of the Node is none then Node itself
    and decendent have no mirror, so return
    none, no need to further explore! */
    if (left == NULL || right == NULL)
        return 0;

    /* if left Node is target Node, then return
    right's key (that is mirror) and vice
    versa */
    if (left->key == target)
        return right->key;

    if (right->key == target)
        return left->key;

    // first recur external Nodes
    int mirror_val = findMirrorRec(target,
                                   left->left,
                                   right->right);
    if (mirror_val)
        return mirror_val;

    // if no mirror found, recur internal Nodes
    findMirrorRec(target, left->right, right->left);
}

// interface for mirror search
int findMirror(struct Node* root, int target)
{
    if (root == NULL)
        return 0;
    if (root->key == target)
        return target;
    return findMirrorRec(target, root->left,
                                 root->right);
}

// Driver Code
int main()
{
    struct Node* root = newNode(1);
    root-> left = newNode(2);
    root->left->left = newNode(4);
    root->left->left->right    = newNode(7);
    root->right    = newNode(3);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->left    = newNode(8);
    root->right->left->right = newNode(9);

    // target Node whose mirror have to be searched
    int target = root->left->left->key;

    int mirror = findMirror(root, target);

    if (mirror)
        cout << "Mirror of Node " << target
             << " is Node " << mirror << endl;
    else
        cout << "Mirror of Node " << target
             << " is NULL! " << endl;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program to find the mirror Node in Binary tree
#include <stdio.h>
#include <stdlib.h>

/* A binary tree Node has data, pointer to left child
  and a pointer to right child */
struct Node
{
    int key;
    struct Node* left, *right;
};

// create new Node and initialize it
struct Node* newNode(int key)
{
    struct Node* n = (struct Node*)
                     malloc(sizeof(struct Node*));
    if (n != NULL)
    {
        n->key = key;
        n->left = NULL;
        n->right = NULL;
        return n;
    }
    else
    {
        printf("Memory allocation failed!");
        exit(1);
    }
}

// recursive function to find mirror of Node
int findMirrorRec(int target, struct Node* left,
                              struct Node* right)
{
    /* if any of the Node is none then Node itself
       and decendent have no mirror, so return
       none, no need to further explore! */
    if (left==NULL || right==NULL)
        return 0;

    /* if left Node is target Node, then return
       right's key (that is mirror) and vice
       versa */
    if (left->key == target)
        return right->key;

    if (right->key == target)
        return left->key;

    // first recur external Nodes
    int mirror_val = findMirrorRec(target,
                                     left->left,
                                     right->right);
    if (mirror_val)
        return mirror_val;

    // if no mirror found, recur internal Nodes
    findMirrorRec(target, left->right, right->left);
}

// interface for mirror search
int findMirror(struct Node* root, int target)
{
    if (root == NULL)
        return 0;
    if (root->key == target)
        return target;
    return findMirrorRec(target, root->left, root->right);
}

// Driver
int main()
{
    struct Node* root           = newNode(1);
    root-> left                 = newNode(2);
    root->left->left            = newNode(4);
    root->left->left->right     = newNode(7);
    root->right                 = newNode(3);
    root->right->left           = newNode(5);
    root->right->right          = newNode(6);
    root->right->left->left     = newNode(8);
    root->right->left->right    = newNode(9);

    // target Node whose mirror have to be searched
    int target = root->left->left->key;

    int mirror = findMirror(root, target);

    if (mirror)
        printf("Mirror of Node %d is Node %d\n",
                                    target, mirror);
    else
        printf("Mirror of Node %d is NULL!\n", target);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the mirror Node in Binary tree
class GfG {

/* A binary tree Node has data, pointer to left child
and a pointer to right child */
static class Node
{
    int key;
    Node left, right;
}

// create new Node and initialize it
static Node newNode(int key)
{
    Node n = new Node();

        n.key = key;
        n.left = null;
        n.right = null;
        return n;
}

// recursive function to find mirror of Node
static int findMirrorRec(int target, Node left, Node right)
{
    /* if any of the Node is none then Node itself
    and decendent have no mirror, so return
    none, no need to further explore! */
    if (left==null || right==null)
        return 0;

    /* if left Node is target Node, then return
    right's key (that is mirror) and vice
    versa */
    if (left.key == target)
        return right.key;

    if (right.key == target)
        return left.key;

    // first recur external Nodes
    int mirror_val = findMirrorRec(target, left.left, right.right);
    if (mirror_val != 0)
        return mirror_val;

    // if no mirror found, recur internal Nodes
    return findMirrorRec(target, left.right, right.left);
}

// interface for mirror search
static int findMirror(Node root, int target)
{
    if (root == null)
        return 0;
    if (root.key == target)
        return target;
    return findMirrorRec(target, root.left, root.right);
}

// Driver
public static void main(String[] args)
{
    Node root         = newNode(1);
    root.left                 = newNode(2);
    root.left.left         = newNode(4);
    root.left.left.right     = newNode(7);
    root.right                 = newNode(3);
    root.right.left         = newNode(5);
    root.right.right         = newNode(6);
    root.right.left.left     = newNode(8);
    root.right.left.right = newNode(9);

    // target Node whose mirror have to be searched
    int target = root.left.left.key;

    int mirror = findMirror(root, target);

    if (mirror != 0)
        System.out.println("Mirror of Node " + target + " is Node " + mirror);
    else
        System.out.println("Mirror of Node " + target + " is null ");
}
}
```

## 蟒蛇 3

```
# Python3 program to find the mirror node in
# Binary tree

class Node:
    '''A binary tree node has data, reference to left child
         and a reference to right child '''

    def __init__(self, key, lchild=None, rchild=None):
        self.key = key
        self.lchild = None
        self.rchild = None

# recursive function to find mirror
def findMirrorRec(target, left, right):

    # If any of the node is none then node itself
    # and decendent have no mirror, so return
    # none, no need to further explore!
    if left == None or right == None:
        return None

    # if left node is target node, then return
    # right's key (that is mirror) and vice versa
    if left.key == target:
        return right.key
    if right.key == target:
        return left.key

    # first recur external nodes
    mirror_val = findMirrorRec(target, left.lchild, right.rchild)
    if mirror_val != None:
        return mirror_val

    # if no mirror found, recur internal nodes
    findMirrorRec(target, left.rchild, right.lchild)

# interface for mirror search
def findMirror(root, target):
    if root == None:
        return None

    if root.key == target:
        return target

    return findMirrorRec(target, root.lchild, root.rchild)

# Driver
def main():
    root = Node(1)
    n1 = Node(2)
    n2 = Node(3)
    root.lchild = n1
    root.rchild = n2
    n3 = Node(4)
    n4 = Node(5)
    n5 = Node(6)
    n1.lchild = n3
    n2.lchild = n4
    n2.rchild = n5
    n6 = Node(7)
    n7 = Node(8)
    n8 = Node(9)
    n3.rchild = n6
    n4.lchild = n7
    n4.rchild = n8

    # target node whose mirror have to be searched
    target = n3.key

    mirror = findMirror(root, target)
    print("Mirror of node {} is node {}".format(target, mirror))

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to find the
// mirror Node in Binary tree
using System;

class GfG
{

    /* A binary tree Node has data,
        pointer to left child and a
        pointer to right child */
    class Node
    {
        public int key;
        public Node left, right;
    }

    // create new Node and initialize it
    static Node newNode(int key)
    {
        Node n = new Node();

            n.key = key;
            n.left = null;
            n.right = null;
            return n;
    }

    // recursive function to find mirror of Node
    static int findMirrorRec(int target, Node left,
                                        Node right)
    {
        /* if any of the Node is none then Node itself
        and decendent have no mirror, so return
        none, no need to further explore! */
        if (left==null || right==null)
            return 0;

        /* if left Node is target Node, then return
        right's key (that is mirror) and vice
        versa */
        if (left.key == target)
            return right.key;

        if (right.key == target)
            return left.key;

        // first recur external Nodes
        int mirror_val = findMirrorRec(target,
                        left.left, right.right);
        if (mirror_val != 0)
            return mirror_val;

        // if no mirror found, recur internal Nodes
        return findMirrorRec(target,
                left.right, right.left);
    }

    // interface for mirror search
    static int findMirror(Node root, int target)
    {
        if (root == null)
            return 0;
        if (root.key == target)
            return target;
        return findMirrorRec(target,
                root.left, root.right);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.left.left = newNode(4);
        root.left.left.right = newNode(7);
        root.right = newNode(3);
        root.right.left    = newNode(5);
        root.right.right = newNode(6);
        root.right.left.left = newNode(8);
        root.right.left.right = newNode(9);

        // target Node whose mirror have to be searched
        int target = root.left.left.key;

        int mirror = findMirror(root, target);

        if (mirror != 0)
            Console.WriteLine("Mirror of Node " +
                                target + " is Node " +
                                            mirror);
        else
            Console.WriteLine("Mirror of Node " + target +
                                            " is null ");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the mirror
// Node in Binary tree

/* A binary tree Node has data, pointer
to left child and a pointer to right child */
class Node
{

    // Create new Node and initialize it
    constructor(key)
    {
        this.key = key;
        this.left = this.right = null;
    }
}

// Recursive function to find mirror of Node
function findMirrorRec(target, left, right)
{

    /* If any of the Node is none then Node itself
    and decendent have no mirror, so return
    none, no need to further explore! */
    if (left == null || right == null)
        return 0;

    /* If left Node is target Node, then return
    right's key (that is mirror) and vice
    versa */
    if (left.key == target)
        return right.key;

    if (right.key == target)
        return left.key;

    // First recur external Nodes
    let mirror_val = findMirrorRec(
        target, left.left, right.right);
    if (mirror_val != 0)
        return mirror_val;

    // If no mirror found, recur internal Nodes
    return findMirrorRec(target, left.right,
                                 right.left);
}

// Interface for mirror search
function findMirror(root, target)
{
    if (root == null)
        return 0;
    if (root.key == target)
        return target;

    return findMirrorRec(target, root.left,
                                 root.right);
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.left.left = new Node(4);
root.left.left.right = new Node(7);
root.right = new Node(3);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.right.left.left = new Node(8);
root.right.left.right = new Node(9);

// Target Node whose mirror have to be searched
let target = root.left.left.key;

let mirror = findMirror(root, target);

if (mirror != 0)
    document.write("Mirror of Node " + target +
                   " is Node " + mirror + "<br>");
else
    document.write("Mirror of Node " + target +
                   " is null " + "<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Mirror of node 4 is node 6
```

**时间复杂度:** ![O(n)  ](img/69f7999e946d6357e54f231406a5980f.png "Rendered by QuickLaTeX.com")

本文由 [**阿图尔·库马尔**](https://www.linkedin.com/in/atul-kumar-733b32136/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。