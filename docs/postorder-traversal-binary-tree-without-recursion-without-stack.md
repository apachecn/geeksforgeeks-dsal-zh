# 无递归无栈二叉树后序遍历

> 原文:[https://www . geesforgeks . org/post-order-遍历-二叉树-无递归-无栈/](https://www.geeksforgeeks.org/postorder-traversal-binary-tree-without-recursion-without-stack/)

先决条件–[树的有序/前序/后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)
给定一棵二叉树，执行后序遍历。

下面我们讨论了后序遍历的方法。
1) [递归后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。
2) [使用 Stack 的后置遍历。](https://www.geeksforgeeks.org/iterative-postorder-traversal/)
2) [使用两个堆栈的后置遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal/)。在该方法中，讨论了基于 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的解决方案。我们在散列表中跟踪被访问的节点。

## C++

```
// CPP program or postorder traversal
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node *left, *right;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
void postorder(struct Node* head)
{
    struct Node* temp = head;
    unordered_set<Node*> visited;
    while (temp && visited.find(temp) == visited.end()) {

        // Visited left subtree
        if (temp->left &&
         visited.find(temp->left) == visited.end())
            temp = temp->left;

        // Visited right subtree
        else if (temp->right &&
        visited.find(temp->right) == visited.end())
            temp = temp->right;

        // Print node
        else {
            printf("%d ", temp->data);
            visited.insert(temp);
            temp = head;
        }
    }
}

struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

/* Driver program to test above functions*/
int main()
{
    struct Node* root = newNode(8);
    root->left = newNode(3);
    root->right = newNode(10);
    root->left->left = newNode(1);
    root->left->right = newNode(6);
    root->left->right->left = newNode(4);
    root->left->right->right = newNode(7);
    root->right->right = newNode(14);
    root->right->right->left = newNode(13);
    postorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program or postorder traversal
import java.util.*;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
 class Node
 {
    int data;
    Node left, right;
    Node(int data)
    {
        this.data = data;
        this.left = this.right = null;       
    }
};

class GFG
{

Node root;

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
 void postorder(Node head)
{
    Node temp = root;   
    HashSet<Node> visited = new HashSet<>();
    while ((temp != null  && !visited.contains(temp)))
    {

        // Visited left subtree
        if (temp.left != null &&
         !visited.contains(temp.left))
            temp = temp.left;

        // Visited right subtree
        else if (temp.right != null &&
        !visited.contains(temp.right))
            temp = temp.right;

        // Print node
        else
        {
            System.out.printf("%d ", temp.data);
            visited.add(temp);
            temp = head;
        }
    }
}

/* Driver program to test above functions*/
public static void main(String[] args)
{
    GFG gfg = new GFG();
    gfg.root = new Node(8);
    gfg.root.left = new Node(3);
    gfg.root.right = new Node(10);
    gfg.root.left.left = new Node(1);
    gfg.root.left.right = new Node(6);
    gfg.root.left.right.left = new Node(4);
    gfg.root.left.right.right = new Node(7);
    gfg.root.right.right = new Node(14);
    gfg.root.right.right.left = new Node(13);
    gfg.postorder(gfg.root);
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program or postorder traversal

''' A binary tree node has data, pointer to left child
and a pointer to right child '''
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

''' Helper function that allocates a new node with the
given data and NULL left and right pointers. '''
def postorder(head):

    temp = head
    visited = set()
    while (temp and temp not in visited):

        # Visited left subtree
        if (temp.left and temp.left not in visited):
            temp = temp.left

        # Visited right subtree
        elif (temp.right and temp.right not in visited):
            temp = temp.right

        # Print node
        else:
            print(temp.data, end = " ")
            visited.add(temp)
            temp = head

''' Driver program to test above functions'''
if __name__ == '__main__':

    root = newNode(8)
    root.left = newNode(3)
    root.right = newNode(10)
    root.left.left = newNode(1)
    root.left.right = newNode(6)
    root.left.right.left = newNode(4)
    root.left.right.right = newNode(7)
    root.right.right = newNode(14)
    root.right.right.left = newNode(13)
    postorder(root)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program or postorder traversal
using System;
using System.Collections.Generic;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
public
  class Node
  {
    public
      int data;
    public
      Node left, right;
    public
      Node(int data)
    {
      this.data = data;
      this.left = this.right = null;       
    }
  };

class GFG
{

  Node root;

  /* Helper function that allocates a new node with the
given data and null left and right pointers. */
  void postorder(Node head)
  {
    Node temp = root;   
    HashSet<Node> visited = new HashSet<Node>();
    while ((temp != null  && !visited.Contains(temp)))
    {

      // Visited left subtree
      if (temp.left != null &&
          !visited.Contains(temp.left))
        temp = temp.left;

      // Visited right subtree
      else if (temp.right != null &&
               !visited.Contains(temp.right))
        temp = temp.right;

      // Print node
      else
      {
        Console.Write(temp.data + " ");
        visited.Add(temp);
        temp = head;
      }
    }
  }

  /* Driver code*/
  public static void Main(String[] args)
  {
    GFG gfg = new GFG();
    gfg.root = new Node(8);
    gfg.root.left = new Node(3);
    gfg.root.right = new Node(10);
    gfg.root.left.left = new Node(1);
    gfg.root.left.right = new Node(6);
    gfg.root.left.right.left = new Node(4);
    gfg.root.left.right.right = new Node(7);
    gfg.root.right.right = new Node(14);
    gfg.root.right.right.left = new Node(13);
    gfg.postorder(gfg.root);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program or postorder traversal

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

var root = null;

  /* Helper function that allocates a new node with the
given data and null left and right pointers. */
  function postorder(head)
  {
    var temp = root;   
    var visited = new Set();
    while ((temp != null  && !visited.has(temp)))
    {

      // Visited left subtree
      if (temp.left != null &&
          !visited.has(temp.left))
        temp = temp.left;

      // Visited right subtree
      else if (temp.right != null &&
               !visited.has(temp.right))
        temp = temp.right;

      // Print node
      else
      {
        document.write(temp.data + " ");
        visited.add(temp);
        temp = head;
      }
    }
  }

/* Driver code*/
root = new Node(8);
root.left = new Node(3);
root.right = new Node(10);
root.left.left = new Node(1);
root.left.right = new Node(6);
root.left.right.left = new Node(4);
root.left.right.right = new Node(7);
root.right.right = new Node(14);
root.right.right.left = new Node(13);
postorder(root);

</script>
```

**输出:**

```
1 4 7 6 3 13 14 10 8 
```

**替代方案:**
我们可以用每个节点保持访问标志，而不是单独的哈希表。

## C++

```
// CPP program or postorder traversal
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node *left, *right;
    bool visited;
};

void postorder(struct Node* head)
{
    struct Node* temp = head;
    while (temp && temp->visited == false) {

        // Visited left subtree
        if (temp->left && temp->left->visited == false)
            temp = temp->left;

        // Visited right subtree
        else if (temp->right && temp->right->visited == false)
            temp = temp->right;

        // Print node
        else {
            printf("%d ", temp->data);
            temp->visited = true;
            temp = head;
        }
    }
}

struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->visited = false;
    return (node);
}

/* Driver program to test above functions*/
int main()
{
    struct Node* root = newNode(8);
    root->left = newNode(3);
    root->right = newNode(10);
    root->left->left = newNode(1);
    root->left->right = newNode(6);
    root->left->right->left = newNode(4);
    root->left->right->right = newNode(7);
    root->right->right = newNode(14);
    root->right->right->left = newNode(13);
    postorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program or postorder traversal
class GFG
{

/* A binary tree node has data,
    pointer to left child
    and a pointer to right child */
static class Node
{
    int data;
    Node left, right;
    boolean visited;
}

static void postorder( Node head)
{
    Node temp = head;
    while (temp != null &&
            temp.visited == false)
    {

        // Visited left subtree
        if (temp.left != null &&
            temp.left.visited == false)
            temp = temp.left;

        // Visited right subtree
        else if (temp.right != null &&
                temp.right.visited == false)
            temp = temp.right;

        // Print node
        else
        {
            System.out.printf("%d ", temp.data);
            temp.visited = true;
            temp = head;
        }
    }
}

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    node.visited = false;
    return (node);
}

/* Driver code*/
public static void main(String []args)
{
    Node root = newNode(8);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.left.right.left = newNode(4);
    root.left.right.right = newNode(7);
    root.right.right = newNode(14);
    root.right.right.left = newNode(13);
    postorder(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
"""Python3 program or postorder traversal """

# A Binary Tree Node
# Utility function to create a
# new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.visited = False

def postorder(head) :

    temp = head
    while (temp and temp.visited == False):

        # Visited left subtree
        if (temp.left and
            temp.left.visited == False):
            temp = temp.left

        # Visited right subtree
        elif (temp.right and
              temp.right.visited == False):
            temp = temp.right

        # Print node
        else:
            print(temp.data, end = " ")
            temp.visited = True
            temp = head

# Driver Code
if __name__ == '__main__':

    root = newNode(8)
    root.left = newNode(3)
    root.right = newNode(10)
    root.left.left = newNode(1)
    root.left.right = newNode(6)
    root.left.right.left = newNode(4)
    root.left.right.right = newNode(7)
    root.right.right = newNode(14)
    root.right.right.left = newNode(13)
    postorder(root)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program or postorder traversal
using System;

class GFG
{

/* A binary tree node has data,
    pointer to left child
    and a pointer to right child */
class Node
{
    public int data;
    public Node left, right;
    public bool visited;
}

static void postorder( Node head)
{
    Node temp = head;
    while (temp != null &&
            temp.visited == false)
    {

        // Visited left subtree
        if (temp.left != null &&
            temp.left.visited == false)
            temp = temp.left;

        // Visited right subtree
        else if (temp.right != null &&
                temp.right.visited == false)
            temp = temp.right;

        // Print node
        else
        {
            Console.Write("{0} ", temp.data);
            temp.visited = true;
            temp = head;
        }
    }
}

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    node.visited = false;
    return (node);
}

/* Driver code*/
public static void Main(String []args)
{
    Node root = newNode(8);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.left.right.left = newNode(4);
    root.left.right.right = newNode(7);
    root.right.right = newNode(14);
    root.right.right.left = newNode(13);
    postorder(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program or postorder traversal

    /* A binary tree node has data,
    pointer to left child
    and a pointer to right child */
    class Node
    {
        constructor() {
               this.data;
            this.left;
            this.right;
            this.visited;
        }
    }

    function postorder(head)
    {
        let temp = head;
        while (temp != null &&
                temp.visited == false)
        {

            // Visited left subtree
            if (temp.left != null &&
                temp.left.visited == false)
                temp = temp.left;

            // Visited right subtree
            else if (temp.right != null &&
                    temp.right.visited == false)
                temp = temp.right;

            // Print node
            else
            {
                document.write(temp.data + " ");
                temp.visited = true;
                temp = head;
            }
        }
    }

    function newNode(data)
    {
        let node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;
        node.visited = false;
        return (node);
    }

    let root = newNode(8);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.left.right.left = newNode(4);
    root.left.right.right = newNode(7);
    root.right.right = newNode(14);
    root.right.right.left = newNode(13);
    postorder(root);

</script>
```

**输出:**

```
1 4 7 6 3 13 14 10 8 
```

上述解决方案的时间复杂度为 O(n <sup>2</sup> )最坏的情况是我们在访问每个节点后将指针移回头部。
使用[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)的替代解决方案，其中我们不必将指针移回头部，因此时间复杂度为 O(n)。

## C++

```
// CPP program or postorder traversal
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node *left, *right;
    bool visited;
};

void postorder(Node* root)
{
    Node* n = root;
    unordered_map<Node*, Node*> parentMap;
    parentMap.insert(pair<Node*, Node*>(root, nullptr));

    while (n) {
        if (n->left && parentMap.find(n->left) == parentMap.end()) {
            parentMap.insert(pair<Node*, Node*>(n->left, n));
            n = n->left;
        }
        else if (n->right && parentMap.find(n->right) == parentMap.end()) {
            parentMap.insert(pair<Node*, Node*>(n->right, n));
            n = n->right;
        }
        else {
            cout << n->data << " ";
            n = (parentMap.find(n))->second;
        }
    }
}
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->visited = false;
    return (node);
}

/* Driver program to test above functions*/
int main()
{
    struct Node* root = newNode(8);
    root->left = newNode(3);
    root->right = newNode(10);
    root->left->left = newNode(1);
    root->left->right = newNode(6);
    root->left->right->left = newNode(4);
    root->left->right->right = newNode(7);
    root->right->right = newNode(14);
    root->right->right->left = newNode(13);
    postorder(root);
    return 0;
}
```

**输出:**

```
1 4 7 6 3 13 14 10 8 
```