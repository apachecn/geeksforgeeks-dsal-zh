# 在二叉树中迭代搜索一个键‘x’

> 原文:[https://www . geesforgeks . org/iterative-search-for-a-key-x-in-binary-tree/](https://www.geeksforgeeks.org/iterative-search-for-a-key-x-in-binary-tree/)

给定一个二叉树和一个要在其中搜索的关键字，编写一个迭代方法，如果关键字出现在二叉树中，则返回 true，否则返回 false。
例如，在下面的树中，如果搜索到的键是 3，那么函数应该返回 true，如果搜索到的键是 12，那么函数应该返回 false。

![1T](img/ae2af2a037bc95a8e26f7645a87a1dbc.png)

有一点是肯定的，我们需要遍历完整的树来决定键是否存在。我们可以使用以下任何遍历来迭代搜索给定二叉树中的一个关键字。
1)迭代[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
2) [迭代顺序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)
3) [迭代顺序遍历](https://www.geeksforgeeks.org/iterative-preorder-traversal/)
4) [迭代顺序遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal/)
下面是基于迭代 [**级别顺序遍历**](https://www.geeksforgeeks.org/level-order-tree-traversal/) 的解决方案来搜索二叉树中的项 x。

## C++

```
// Iterative level order traversal
// based method to search in Binary Tree
#include<bits/stdc++.h>

using namespace std;

/* A binary tree node has data,
left child and right child */
class node
{
    public:
    int data;
    node* left;
    node* right;

    /* Constructor that allocates a new node with the
    given data and NULL left and right pointers. */
    node(int data){
        this->data = data;
        this->left = NULL;
        this->right = NULL;

    }
};

// An iterative process to search
// an element x in a given binary tree
bool iterativeSearch(node *root, int x)
{
    // Base Case
    if (root == NULL)
        return false;

    // Create an empty queue for
    // level order traversal
    queue<node *> q;

    // Enqueue Root and initialize height
    q.push(root);

    // Queue based level order traversal
    while (q.empty() == false)
    {
        // See if current node is same as x
        node *node = q.front();
        if (node->data == x)
            return true;

        // Remove current node and enqueue its children
        q.pop();
        if (node->left != NULL)
            q.push(node->left);
        if (node->right != NULL)
            q.push(node->right);
    }

    return false;
}

// Driver code
int main()
{
    node* NewRoot=NULL;
    node *root = new node(2);
    root->left = new node(7);
    root->right = new node(5);
    root->left->right = new node(6);
    root->left->right->left=new node(1);
    root->left->right->right=new node(11);
    root->right->right=new node(9);
    root->right->right->left=new node(4);

    iterativeSearch(root, 6)? cout <<
    "Found\n": cout << "Not Found\n";
    iterativeSearch(root, 12)? cout <<
    "Found\n": cout << "Not Found\n";
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// Iterative level order traversal based method to search in Binary Tree
#include <iostream>
#include <queue>
using namespace std;

/* A binary tree node has data, left child and right child */
struct node
{
    int data;
    struct node* left, *right;
};

/* Helper function that allocates a new node with the given data and
   NULL left and right  pointers.*/
struct node* newNode(int data)
{
    struct node* node = new struct node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

// An iterative process to search an element x in a given binary tree
bool iterativeSearch(node *root, int x)
{
    // Base Case
    if (root == NULL)
        return false;

    // Create an empty queue for level order traversal
    queue<node *> q;

    // Enqueue Root and initialize height
    q.push(root);

    // Queue based level order traversal
    while (q.empty() == false)
    {
        // See if current node is same as x
        node *node = q.front();
        if (node->data == x)
            return true;

        // Remove current node and enqueue its children
        q.pop();
        if (node->left != NULL)
            q.push(node->left);
        if (node->right != NULL)
            q.push(node->right);
    }

    return false;
}

// Driver program
int main(void)
{
    struct node*NewRoot=NULL;
    struct node *root = newNode(2);
    root->left        = newNode(7);
    root->right       = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left=newNode(1);
    root->left->right->right=newNode(11);
    root->right->right=newNode(9);
    root->right->right->left=newNode(4);

    iterativeSearch(root, 6)? cout << "Found\n": cout << "Not Found\n";
    iterativeSearch(root, 12)? cout << "Found\n": cout << "Not Found\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative level order traversal
// based method to search in Binary Tree
import java.util.*;

class GFG
{

/* A binary tree node has data,
left child and right child */
static class node
{
    int data;
    node left;
    node right;

    /* Constructor that allocates a new node with the
    given data and null left and right pointers. */
    node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;

    }
};

// An iterative process to search
// an element x in a given binary tree
static boolean iterativeSearch(node root, int x)
{
    // Base Case
    if (root == null)
        return false;

    // Create an empty queue for
    // level order traversal
    Queue<node > q = new LinkedList();

    // Enqueue Root and initialize height
    q.add(root);

    // Queue based level order traversal
    while (q.size() > 0)
    {
        // See if current node is same as x
        node node = q.peek();
        if (node.data == x)
            return true;

        // Remove current node and enqueue its children
        q.remove();
        if (node.left != null)
            q.add(node.left);
        if (node.right != null)
            q.add(node.right);
    }

    return false;
}

// Driver code
public static void main(String ags[])
{
    node NewRoot = null;
    node root = new node(2);
    root.left = new node(7);
    root.right = new node(5);
    root.left.right = new node(6);
    root.left.right.left = new node(1);
    root.left.right.right = new node(11);
    root.right.right = new node(9);
    root.right.right.left = new node(4);

    System.out.print((iterativeSearch(root, 6)?
    "Found\n": "Not Found\n"));
    System.out.print((iterativeSearch(root, 12)?
    "Found\n": "Not Found\n"));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Iterative level order traversal based
# method to search in Binary Tree

# importing Queue
from queue import Queue

# Helper function that allocates a
# new node with the given data and
# None left and right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# An iterative process to search an
# element x in a given binary tree
def iterativeSearch(root, x):

    # Base Case
    if (root == None):
        return False

    # Create an empty queue for level
    # order traversal
    q = Queue()

    # Enqueue Root and initialize height
    q.put(root)

    # Queue based level order traversal
    while (q.empty() == False):

        # See if current node is same as x
        node = q.queue[0]
        if (node.data == x):
            return True

        # Remove current node and
        # enqueue its children
        q.get()
        if (node.left != None):
            q.put(node.left)
        if (node.right != None):
            q.put(node.right)

    return False

# Driver Code
if __name__ == '__main__':

    root = newNode(2)
    root.left = newNode(7)
    root.right = newNode(5)
    root.left.right = newNode(6)
    root.left.right.left = newNode(1)
    root.left.right.right = newNode(11)
    root.right.right = newNode(9)
    root.right.right.left = newNode(4)

    if iterativeSearch(root, 6):
        print("Found")
    else:
        print("Not Found")
    if iterativeSearch(root, 12):
        print("Found")
    else:
        print("Not Found")

# This code is contributed by PranchalK
```

## C#

```
// Iterative level order traversal
// based method to search in Binary Tree
using System;
using System.Collections.Generic;

class GFG
{

/* A binary tree node has data,
left child and right child */
public class node
{
    public int data;
    public node left;
    public node right;

    /* Constructor that allocates a new node
    with the given data and null left and
    right pointers. */
    public node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// An iterative process to search
// an element x in a given binary tree
static Boolean iterativeSearch(node root,
                               int x)
{
    // Base Case
    if (root == null)
        return false;

    // Create an empty queue for
    // level order traversal
    Queue<node > q = new Queue<node>();

    // Enqueue Root and initialize height
    q.Enqueue(root);

    // Queue based level order traversal
    while (q.Count > 0)
    {
        // See if current node is same as x
        node node = q.Peek();
        if (node.data == x)
            return true;

        // Remove current node and
        // enqueue its children
        q.Dequeue();
        if (node.left != null)
            q.Enqueue(node.left);
        if (node.right != null)
            q.Enqueue(node.right);
    }
    return false;
}

// Driver code
public static void Main(String []ags)
{
    node root = new node(2);
    root.left = new node(7);
    root.right = new node(5);
    root.left.right = new node(6);
    root.left.right.left = new node(1);
    root.left.right.right = new node(11);
    root.right.right = new node(9);
    root.right.right.left = new node(4);

    Console.WriteLine((iterativeSearch(root, 6) ?
                                      "Found\n" :
                                   "Not Found"));
    Console.Write((iterativeSearch(root, 12) ?
                                   "Found\n" :
                              "Not Found\n"));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Iterative level order traversal
// based method to search in Binary Tree

/* A binary tree node has data,
left child and right child */
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// An iterative process to search
// an element x in a given binary tree
function iterativeSearch(root,x)
{
    // Base Case
    if (root == null)
        return false;

    // Create an empty queue for
    // level order traversal
    let q = [];

    // Enqueue Root and initialize height
    q.push(root);

    // Queue based level order traversal
    while (q.length > 0)
    {
        // See if current node is same as x
        let node = q[0];
        if (node.data == x)
            return true;

        // Remove current node and enqueue its children
        q.shift();
        if (node.left != null)
            q.push(node.left);
        if (node.right != null)
            q.push(node.right);
    }

    return false;
}

// Driver code
let NewRoot = null;
let root = new node(2);
root.left = new node(7);
root.right = new node(5);
root.left.right = new node(6);
root.left.right.left = new node(1);
root.left.right.right = new node(11);
root.right.right = new node(9);
root.right.right.left = new node(4);

document.write((iterativeSearch(root, 6)?
                  "Found<br>": "Not Found<br>"));
document.write((iterativeSearch(root, 12)?
                  "Found<br>": "Not Found<br>"));

// This code is contributed by rag2127
</script>
```

**输出:**

```
Found
Not Found
```

下面的实现使用 [**迭代前序遍历**](https://www.geeksforgeeks.org/iterative-preorder-traversal/) 在二叉树

中寻找 x

## C++

```
// An iterative method to search an item in Binary Tree
#include <iostream>
#include <stack>
using namespace std;

/* A binary tree node has data, left child and right child */
struct node
{
    int data;
    struct node* left, *right;
};

/* Helper function that allocates a new node with the given data and
NULL left and right pointers.*/
struct node* newNode(int data)
{
    struct node* node = new struct node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

// iterative process to search an element x in a given binary tree
bool iterativeSearch(node *root, int x)
{
    // Base Case
    if (root == NULL)
        return false;

    // Create an empty stack and push root to it
    stack<node *> nodeStack;
    nodeStack.push(root);

    // Do iterative preorder traversal to search x
    while (nodeStack.empty() == false)
    {
        // See the top item from stack and check if it is same as x
        struct node *node = nodeStack.top();
        if (node->data == x)
            return true;
        nodeStack.pop();

        // Push right and left children of the popped node to stack
        if (node->right)
            nodeStack.push(node->right);
        if (node->left)
            nodeStack.push(node->left);
    }

    return false;
}

// Driver program
int main(void)
{
    struct node*NewRoot=NULL;
    struct node *root = newNode(2);
    root->left     = newNode(7);
    root->right     = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left=newNode(1);
    root->left->right->right=newNode(11);
    root->right->right=newNode(9);
    root->right->right->left=newNode(4);

    iterativeSearch(root, 6)? cout << "Found\n": cout << "Not Found\n";
    iterativeSearch(root, 12)? cout << "Found\n": cout << "Not Found\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An iterative method to search an item in Binary Tree
import java.util.*;

class GFG
{

/* A binary tree node has data,
left child and right child */
static class node
{
    int data;
    node left, right;
};

/* Helper function that allocates a
new node with the given data and
null left and right pointers.*/
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// iterative process to search
// an element x in a given binary tree
static boolean iterativeSearch(node root, int x)
{
    // Base Case
    if (root == null)
        return false;

    // Create an empty stack and push root to it
    Stack<node> nodeStack = new Stack<node>();
    nodeStack.push(root);

    // Do iterative preorder traversal to search x
    while (nodeStack.empty() == false)
    {
        // See the top item from stack and
        // check if it is same as x
        node node = nodeStack.peek();
        if (node.data == x)
            return true;
        nodeStack.pop();

        // Push right and left children
        // of the popped node to stack
        if (node.right != null)
            nodeStack.push(node.right);
        if (node.left != null)
            nodeStack.push(node.left);
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    node NewRoot = null;
    node root = newNode(2);
    root.left = newNode(7);
    root.right = newNode(5);
    root.left.right = newNode(6);
    root.left.right.left = newNode(1);
    root.left.right.right = newNode(11);
    root.right.right = newNode(9);
    root.right.right.left = newNode(4);

    if(iterativeSearch(root, 6))
        System.out.println("Found");
    else
        System.out.println("Not Found");
    if(iterativeSearch(root, 12))
        System.out.println("Found");
    else
        System.out.println("Not Found");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# An iterative Python3 code to search
# an item in Binary Tree

''' A binary tree node has data,
left child and right child '''
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# iterative process to search an element x
# in a given binary tree
def iterativeSearch(root,x):

    # Base Case
    if (root == None):
        return False

    # Create an empty stack and
    # append root to it
    nodeStack = []
    nodeStack.append(root)

    # Do iterative preorder traversal to search x
    while (len(nodeStack)):

        # See the top item from stack and
        # check if it is same as x
        node = nodeStack[0]
        if (node.data == x):
            return True
        nodeStack.pop(0)

        # append right and left children
        # of the popped node to stack
        if (node.right):
            nodeStack.append(node.right)
        if (node.left):
            nodeStack.append(node.left)

    return False

# Driver Code
root = newNode(2)
root.left = newNode(7)
root.right = newNode(5)
root.left.right = newNode(6)
root.left.right.left = newNode(1)
root.left.right.right = newNode(11)
root.right.right = newNode(9)
root.right.right.left = newNode(4)

if iterativeSearch(root, 6):
    print("Found")
else:
    print("Not Found")

if iterativeSearch(root, 12):
    print("Found")
else:
    print("Not Found")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// An iterative method to search an item in Binary Tree
using System;
using System.Collections.Generic;

class GFG
{

/* A binary tree node has data,
left child and right child */
class node
{
    public int data;
    public node left, right;
};

/* Helper function that allocates a
new node with the given data and
null left and right pointers.*/
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// iterative process to search
// an element x in a given binary tree
static bool iterativeSearch(node root, int x)
{
    // Base Case
    if (root == null)
        return false;

    // Create an empty stack and.Push root to it
    Stack<node> nodeStack = new Stack<node>();
    nodeStack.Push(root);

    // Do iterative preorder traversal to search x
    while (nodeStack.Count != 0)
    {
        // See the top item from stack and
        // check if it is same as x
        node node = nodeStack.Peek();
        if (node.data == x)
            return true;
        nodeStack.Pop();

        // Push right and left children
        // of the.Popped node to stack
        if (node.right != null)
            nodeStack.Push(node.right);
        if (node.left != null)
            nodeStack.Push(node.left);
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    node root = newNode(2);
    root.left = newNode(7);
    root.right = newNode(5);
    root.left.right = newNode(6);
    root.left.right.left = newNode(1);
    root.left.right.right = newNode(11);
    root.right.right = newNode(9);
    root.right.right.left = newNode(4);

    if(iterativeSearch(root, 6))
        Console.WriteLine("Found");
    else
        Console.WriteLine("Not Found");
    if(iterativeSearch(root, 12))
        Console.WriteLine("Found");
    else
        Console.WriteLine("Not Found");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// An iterative method to search an item in Binary Tree

/* A binary tree node has data,
left child and right child */
class Node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
};

/* Helper function that allocates a
new node with the given data and
null left and right pointers.*/
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// iterative process to search
// an element x in a given binary tree
function iterativeSearch(root, x)
{
    // Base Case
    if (root == null)
        return false;

    // Create an empty stack and.push root to it
    var nodeStack = [];
    nodeStack.push(root);

    // Do iterative preorder traversal to search x
    while (nodeStack.length != 0)
    {
        // See the top item from stack and
        // check if it is same as x
        var node = nodeStack[nodeStack.length - 1];
        if (node.data == x)
            return true;
        nodeStack.pop();

        // push right and left children
        // of the.Popped node to stack
        if (node.right != null)
            nodeStack.push(node.right);
        if (node.left != null)
            nodeStack.push(node.left);
    }
    return false;
}

// Driver Code
var root = newNode(2);
root.left = newNode(7);
root.right = newNode(5);
root.left.right = newNode(6);
root.left.right.left = newNode(1);
root.left.right.right = newNode(11);
root.right.right = newNode(9);
root.right.right.left = newNode(4);
if(iterativeSearch(root, 6))
    document.write("Found<br>");
else
    document.write("Not Found<br>");
if(iterativeSearch(root, 12))
    document.write("Found<br>");
else
    document.write("Not Found<br>");

</script>
```

**输出:**

```
Found
Not Found
```

类似地，可以使用[迭代顺序](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)和[迭代顺序后](https://www.geeksforgeeks.org/iterative-postorder-traversal/)遍历。

https://www.youtube.com/watch?v=-jREIGMJ8Tg

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。