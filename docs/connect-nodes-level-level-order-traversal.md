# 连接同级节点(级序遍历)

> 原文:[https://www . geesforgeks . org/connect-nodes-level-level-order-遍历/](https://www.geeksforgeeks.org/connect-nodes-level-level-order-traversal/)

编写一个函数来连接二叉树中同一级别的所有相邻节点。

示例:

```
Input Tree
       A
      / \
     B   C
    / \   \
   D   E   F

Output Tree
       A--->NULL
      / \
     B-->C-->NULL
    / \   \
   D-->E-->F-->NULL
```

我们已经在[中讨论了 O(n^2)时间和 o 方法连接相同级别的节点](https://www.geeksforgeeks.org/connect-nodes-at-same-level-with-o1-extra-space/),因为 morris 遍历在最坏的情况下可以是 O(n ),调用它来设置右指针会导致 O(n^2)时间复杂度。
在这篇文章中，我们讨论了带有空标记的[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，需要空标记来标记树中的级别。

## C++

```
// Connect nodes at same level using level order
// traversal.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node* left, *right, *nextRight;
};

// Sets nextRight of all nodes of a tree
void connect(struct Node* root)
{
    queue<Node*> q;
    q.push(root);

    // null marker to represent end of current level
    q.push(NULL);

    // Do Level order of tree using NULL markers
    while (!q.empty()) {
        Node *p = q.front();
        q.pop();
        if (p != NULL) {

            // next element in queue represents next
            // node at current Level
            p->nextRight = q.front();

            // push left and right children of current
            // node
            if (p->left)
                q.push(p->left);
            if (p->right)
                q.push(p->right);
        }

        // if queue is not empty, push NULL to mark
        // nodes at this level are visited
        else if (!q.empty())
            q.push(NULL);
    }
}

/* UTILITY FUNCTIONS */
/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node* newnode(int data)
{
    struct Node* node = (struct Node*)
                         malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = node->nextRight = NULL;
    return (node);
}

/* Driver program to test above functions*/
int main()
{

    /* Constructed binary tree is
              10
            /   \
          8      2
        /         \
      3            90
    */
    struct Node* root = newnode(10);
    root->left = newnode(8);
    root->right = newnode(2);
    root->left->left = newnode(3);
    root->right->right = newnode(90);

    // Populates nextRight pointer in all nodes
    connect(root);

    // Let us check the values of nextRight pointers
    printf("Following are populated nextRight pointers in \n"
     "the tree (-1 is printed if there is no nextRight) \n");
    printf("nextRight of %d is %d \n", root->data,
     root->nextRight ? root->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->left->data,
     root->left->nextRight ? root->left->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->right->data,
     root->right->nextRight ? root->right->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->left->left->data,
     root->left->left->nextRight ? root->left->left->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->right->right->data,
     root->right->right->nextRight ? root->right->right->nextRight->data : -1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Connect nodes at same level using level order
// traversal.
import java.util.LinkedList;
import java.util.Queue;
public class Connect_node_same_level {

    // Node class
    static class Node {
        int data;
        Node left, right, nextRight;
        Node(int data){
            this.data = data;
            left = null;
            right = null;
            nextRight = null;
        }
    };

    // Sets nextRight of all nodes of a tree
    static void connect(Node root)
    {
        Queue<Node> q = new LinkedList<Node>();
        q.add(root);

        // null marker to represent end of current level
        q.add(null);

        // Do Level order of tree using NULL markers
        while (!q.isEmpty()) {
            Node p = q.peek();
            q.remove();
            if (p != null) {

                // next element in queue represents next
                // node at current Level
                p.nextRight = q.peek();

                // push left and right children of current
                // node
                if (p.left != null)
                    q.add(p.left);
                if (p.right != null)
                    q.add(p.right);
            }

            // if queue is not empty, push NULL to mark
            // nodes at this level are visited
            else if (!q.isEmpty())
                q.add(null);
        }
    }

    /* Driver program to test above functions*/
    public static void main(String args[])
    {

        /* Constructed binary tree is
                  10
                /   \
              8      2
            /         \
          3            90
        */
        Node root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        connect(root);

        // Let us check the values of nextRight pointers
        System.out.println("Following are populated nextRight pointers in \n" +
      "the tree (-1 is printed if there is no nextRight)");
        System.out.println("nextRight of "+ root.data +" is "+
        ((root.nextRight != null) ? root.nextRight.data : -1));
        System.out.println("nextRight of "+ root.left.data+" is "+
        ((root.left.nextRight != null) ? root.left.nextRight.data : -1));
        System.out.println("nextRight of "+ root.right.data+" is "+
        ((root.right.nextRight != null) ? root.right.nextRight.data : -1));
        System.out.println("nextRight of "+  root.left.left.data+" is "+
        ((root.left.left.nextRight != null) ? root.left.left.nextRight.data : -1));
        System.out.println("nextRight of "+  root.right.right.data+" is "+
        ((root.right.right.nextRight != null) ? root.right.right.nextRight.data : -1));
    }
}   
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
#! /usr/bin/env python3

# connect nodes at same level using level order traversal
import sys

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.nextRight = None

    def __str__(self):
        return '{}'.format(self.data)

def printLevelByLevel(root):
    # print level by level
    if root:
        node = root
        while node:
            print('{}'.format(node.data), end=' ')
            node = node.nextRight
        print()
        if root.left:
            printLevelByLevel(root.left)
        else:
            printLevelByLevel(root.right)

def inorder(root):
    if root:
        inorder(root.left)
        print(root.data, end=' ')
        inorder(root.right)

def connect(root):
    # set nextRight of all nodes of a tree
    queue = []
    queue.append(root)
    # null marker to represent end of current level
    queue.append(None)
    # do level order of tree using None markers
    while queue:
        p = queue.pop(0)
        if p:
            # next element in queue represents
            # next node at current level
            p.nextRight = queue[0]
            # pus left and right children of current node
            if p.left:
                queue.append(p.left)
            if p.right:
                queue.append(p.right)
        elif queue:
            queue.append(None)

def main():
    """Driver program to test above functions.
        Constructed binary tree is
                10
               /  \
             8      2
            /        \
          3            90
    """

    root = Node(10)
    root.left = Node(8)
    root.right = Node(2)
    root.left.left = Node(3)
    root.right.right = Node(90)

    # Populates nextRight pointer in all nodes
    connect(root)

    # Let us check the values of nextRight pointers
    print("Following are populated nextRight pointers in \n"
    "the tree (-1 is printed if there is no nextRight) \n")
    if(root.nextRight != None):
        print("nextRight of %d is %d \n" %(root.data,root.nextRight.data))
    else:
        print("nextRight of %d is %d \n" %(root.data,-1))
    if(root.left.nextRight != None):
        print("nextRight of %d is %d \n" %(root.left.data,root.left.nextRight.data))
    else:
        print("nextRight of %d is %d \n" %(root.left.data,-1))
    if(root.right.nextRight != None):
        print("nextRight of %d is %d \n" %(root.right.data,root.right.nextRight.data))
    else:
        print("nextRight of %d is %d \n" %(root.right.data,-1))
    if(root.left.left.nextRight != None):
        print("nextRight of %d is %d \n" %(root.left.left.data,root.left.left.nextRight.data))
    else:
        print("nextRight of %d is %d \n" %(root.left.left.data,-1))
    if(root.right.right.nextRight != None):
        print("nextRight of %d is %d \n" %(root.right.right.data,root.right.right.nextRight.data))
    else:
        print("nextRight of %d is %d \n" %(root.right.right.data,-1))

    print()

if __name__ == "__main__":
    main()

# This code is contributed by Ram Basnet
```

## C#

```
// Connect nodes at same level using level order
// traversal.
using System;
using System.Collections.Generic;

public class Connect_node_same_level
{

    // Node class
    class Node
    {
        public int data;
        public Node left, right, nextRight;
        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
            nextRight = null;
        }
    };

    // Sets nextRight of all nodes of a tree
    static void connect(Node root)
    {
        Queue<Node> q = new Queue<Node>();
        q.Enqueue(root);

        // null marker to represent end of current level
        q.Enqueue(null);

        // Do Level order of tree using NULL markers
        while (q.Count!=0)
        {
            Node p = q.Peek();
            q.Dequeue();
            if (p != null)
            {

                // next element in queue represents next
                // node at current Level
                p.nextRight = q.Peek();

                // push left and right children of current
                // node
                if (p.left != null)
                    q.Enqueue(p.left);
                if (p.right != null)
                    q.Enqueue(p.right);
            }

            // if queue is not empty, push NULL to mark
            // nodes at this level are visited
            else if (q.Count!=0)
                q.Enqueue(null);
        }
    }

    /* Driver code*/
    public static void Main()
    {

        /* Constructed binary tree is
                10
                / \
            8 2
            /     \
        3     90
        */
        Node root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        connect(root);

        // Let us check the values of nextRight pointers
        Console.WriteLine("Following are populated nextRight pointers in \n" +
    "the tree (-1 is printed if there is no nextRight)");
        Console.WriteLine("nextRight of "+ root.data +" is "+
        ((root.nextRight != null) ? root.nextRight.data : -1));
        Console.WriteLine("nextRight of "+ root.left.data+" is "+
        ((root.left.nextRight != null) ? root.left.nextRight.data : -1));
        Console.WriteLine("nextRight of "+ root.right.data+" is "+
        ((root.right.nextRight != null) ? root.right.nextRight.data : -1));
        Console.WriteLine("nextRight of "+ root.left.left.data+" is "+
        ((root.left.left.nextRight != null) ? root.left.left.nextRight.data : -1));
        Console.WriteLine("nextRight of "+ root.right.right.data+" is "+
        ((root.right.right.nextRight != null) ? root.right.right.nextRight.data : -1));
    }
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>
    // Connect nodes at same level using level order traversal.

    // A Binary Tree Node
    class Node
    {
        constructor(data, nextRight) {
           this.left = null;
           this.right = null;
           this.data = data;
           this.nextRight = nextRight;
        }
    }

    // Sets nextRight of all nodes of a tree
    function connect(root)
    {
        let q = [];
        q.push(root);

        // null marker to represent end of current level
        q.push(null);

        // Do Level order of tree using NULL markers
        while (q.length > 0) {
            let p = q[0];
            q.shift();
            if (p != null) {

                // next element in queue represents next
                // node at current Level
                p.nextRight = q[0];

                // push left and right children of current
                // node
                if (p.left != null)
                    q.push(p.left);
                if (p.right != null)
                    q.push(p.right);
            }

            // if queue is not empty, push NULL to mark
            // nodes at this level are visited
            else if (q.length > 0)
                q.push(null);
        }
    }

    /* Constructed binary tree is
                  10
                /   \
              8      2
            /         \
          3            90
        */
        let root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        connect(root);

        // Let us check the values of nextRight pointers
        document.write("Following are populated nextRight pointers in " + "</br>" +
      "the tree (-1 is printed if there is no nextRight)" + "</br>");
        document.write("nextRight of "+ root.data +" is "+
        ((root.nextRight != null) ? root.nextRight.data : -1) + "</br>");
        document.write("nextRight of "+ root.left.data+" is "+
        ((root.left.nextRight != null) ? root.left.nextRight.data : -1) + "</br>");
        document.write("nextRight of "+ root.right.data+" is "+
        ((root.right.nextRight != null) ? root.right.nextRight.data : -1) + "</br>");
        document.write("nextRight of "+  root.left.left.data+" is "+
        ((root.left.left.nextRight != null) ? root.left.left.nextRight.data : -1) + "</br>");
        document.write("nextRight of "+  root.right.right.data+" is "+
        ((root.right.right.nextRight != null) ? root.right.right.nextRight.data : -1) + "</br>");

// This code is contributed by divyesh072019.
</script>
```

**输出:**

```
Following are populated nextRight pointers in 
the tree (-1 is printed if there is no nextRight) 
nextRight of 10 is -1 
nextRight of 8 is 2 
nextRight of 2 is -1 
nextRight of 3 is 90 
nextRight of 90 is -1 
```

**时间复杂度:** O(n)，其中 n 为节点数

**替代实现:**
我们也可以按照[中讨论的实现逐行打印级别顺序遍历| Set 1](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/) 。我们通过跟踪先前访问过的相同级别的节点来保持连接相同级别的节点。

实现:[https://ide.geeksforgeeks.org/gV1Oc2](https://ide.geeksforgeeks.org/gV1Oc2)
感谢 Akilan Sengottaiyan 提出这个替代实现。

本文由 **Abhishek Rajput** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。