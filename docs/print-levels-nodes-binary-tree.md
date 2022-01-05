# 打印二叉树中所有节点的级别

> 原文:[https://www . geesforgeks . org/print-levels-nodes-二叉树/](https://www.geeksforgeeks.org/print-levels-nodes-binary-tree/)

给定一个二叉树和一个键，编写一个函数，打印给定二叉树中所有键的级别。
例如，考虑下面的树。如果输入键是 3，那么你的函数应该返回 1。如果输入键是 4，那么你的函数应该返回 3。对于键中不存在的键，您的函数应该返回 0。

![](img/0d1b90ad2012e8b6bbf76e2766bc71bb.png)

```
Input:
       3
      / \
     2   5
    / \
   1   4

output:
 Level of 1 is 3
 Level of 2 is 2
 Level of 3 is 1
 Level of 4 is 3
 Level of 5 is 2
```

我们已经在下面的帖子中讨论了递归解决方案。
[获取二叉树中节点的级别](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/)
本文讨论了一种基于[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)的迭代求解方法。遍历时，我们将队列中每个节点的级别与该节点存储在一起。

## C++

```
// An iterative C++ program to print levels
// of all nodes
#include <bits/stdc++.h>
using namespace std;

/* A tree node structure */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

void printLevel(struct Node* root)
{
    if (!root)
        return;

    // queue to hold tree node with level
    queue<pair<struct Node*, int> > q;

    q.push({root, 1}); // let root node be at level 1

    pair<struct Node*, int> p;

    // Do level Order Traversal of tree
    while (!q.empty()) {
        p = q.front();
        q.pop();

        cout << "Level of " << p.first->data
             << " is " << p.second << "\n";

        if (p.first->left)
            q.push({ p.first->left, p.second + 1 });
        if (p.first->right)
            q.push({ p.first->right, p.second + 1 });
    }
}

/* Utility function to create a new Binary Tree node */
struct Node* newNode(int data)
{
    struct Node* temp = new struct Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

/* Driver function to test above functions */
int main()
{
    struct Node* root = NULL;

    /* Constructing tree given in the above figure */
    root = newNode(3);
    root->left = newNode(2);
    root->right = newNode(5);
    root->left->left = newNode(1);
    root->left->right = newNode(4);

    printLevel(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// levels of all nodes
import java.util.LinkedList;
import java.util.Queue;
public class Print_Level_Btree {

    /* A tree node structure */
    static class Node {
        int data;
        Node left;
        Node right;
        Node(int data){
            this.data = data;
            left = null;
            right = null;
        }
    }

    // User defined class Pair to hold
    // the node and its level
    static class Pair{
        Node n;
        int i;
        Pair(Node n, int i){
            this.n = n;
            this.i = i;
        }

    }

    // function to print the nodes and
    // its corresponding level
    static void printLevel(Node root)
    {
        if (root == null)
            return;

        // queue to hold tree node with level
        Queue<Pair> q = new LinkedList<Pair>();

        // let root node be at level 1
        q.add(new Pair(root, 1));

        Pair p;

        // Do level Order Traversal of tree
        while (!q.isEmpty()) {
            p = q.peek();
            q.remove();

            System.out.println("Level of " + p.n.data +
                    " is " + p.i);
            if (p.n.left != null)
                q.add(new Pair(p.n.left, p.i + 1));
            if (p.n.right != null)
                q.add(new Pair(p.n.right, p.i + 1));
        }
    }

    /* Driver function to test above
        functions */
    public static void main(String args[])
    {
        Node root = null;

        /* Constructing tree given in the
              above figure */
        root = new Node(3);
        root.left = new Node(2);
        root.right = new Node(5);
        root.left.left = new Node(1);
        root.left.right = new Node(4);

        printLevel(root);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to print levels
# of all nodes

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                    
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def prLevel( root):

    if (not root):
        return

    # queue to hold tree node with level
    q = []

    # let root node be at level 1
    q.append([root, 1])

    p = []

    # Do level Order Traversal of tree
    while (len(q)):
        p = q[0]
        q.pop(0)
        print("Level of", p[0].data, "is", p[1])
        if (p[0].left):
            q.append([p[0].left, p[1] + 1])
        if (p[0].right):
            q.append([p[0].right, p[1] + 1 ])

# Driver Code
if __name__ == '__main__':

    """
    Let us create Binary Tree shown
    in above example """
    root = newNode(3)
    root.left = newNode(2)
    root.right = newNode(5)
    root.left.left = newNode(1)
    root.left.right = newNode(4)
    prLevel(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
using System;
using System.Collections.Generic;

// C# program to print 
// levels of all nodes
public class Print_Level_Btree
{

    /* A tree node structure */
    public class Node
    {
        public int data;
        public Node left;
        public Node right;
        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    // User defined class Pair to hold 
    // the node and its level
    public class Pair
    {
        public Node n;
        public int i;
        public Pair(Node n, int i)
        {
            this.n = n;
            this.i = i;
        }

    }

    // function to print the nodes and 
    // its corresponding level
    public static void printLevel(Node root)
    {
        if (root == null)
        {
            return;
        }

        // queue to hold tree node with level
        LinkedList<Pair> q = new LinkedList<Pair>();

        // let root node be at level 1
        q.AddLast(new Pair(root, 1));

        Pair p;

        // Do level Order Traversal of tree
        while (q.Count > 0)
        {
            p = q.First.Value;
            q.RemoveFirst();

            Console.WriteLine("Level of " + p.n.data + " is " + p.i);
            if (p.n.left != null)
            {
                q.AddLast(new Pair(p.n.left, p.i + 1));
            }
            if (p.n.right != null)
            {
                q.AddLast(new Pair(p.n.right, p.i + 1));
            }
        }
    }

    /* Driver function to test above
        functions */
    public static void Main(string[] args)
    {
        Node root = null;

        /* Constructing tree given in the 
              above figure */
        root = new Node(3);
        root.left = new Node(2);
        root.right = new Node(5);
        root.left.left = new Node(1);
        root.left.right = new Node(4);

        printLevel(root);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to print
    // levels of all nodes

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to print the nodes and
    // its corresponding level
    function printLevel(root)
    {
        if (root == null)
            return;

        // queue to hold tree node with level
        let q = [];

        // let root node be at level 1
        q.push([root, 1]);

        let p;

        // Do level Order Traversal of tree
        while (q.length > 0) {
            p = q[0];
            q.shift();

            document.write("Level of " + p[0].data +
                    " is " + p[1] + "</br>");
            if (p[0].left != null)
                q.push([p[0].left, p[1] + 1]);
            if (p[0].right != null)
                q.push([p[0].right, p[1] + 1]);
        }
    }

    let root = null;

    /* Constructing tree given in the
                above figure */
    root = new Node(3);
    root.left = new Node(2);
    root.right = new Node(5);
    root.left.left = new Node(1);
    root.left.right = new Node(4);

    printLevel(root);

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
Level of 3 is 1
Level of 2 is 2
Level of 5 is 2
Level of 1 is 3
Level of 4 is 3
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。

本文由 **Abhishek Rajput** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。