# 普通树(每个节点可以有任意数量的子节点)级序遍历

> 原文:[https://www . geesforgeks . org/generic-tree-level-order-遍历/](https://www.geeksforgeeks.org/generic-tree-level-order-traversal/)

给定一个类属树，执行级别顺序遍历并打印其所有节点
**示例:**

```
Input :            10
             /   /    \   \
            2  34    56   100
           / \        |   / | \
          77  88      1   7  8  9

Output : 10
         2 34 56 100
         77 88 1 7 8 9

Input :             1
             /   /    \   \
            2  3      4    5
           / \        |  /  | \
          6   7       8 9  10  11
Output : 1
         2 3 4 5
         6 7 8 9 10 11
```

这个问题的解决方法类似于二叉树中的[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。我们从推送队列中的根节点开始，对于每个节点，我们弹出它，打印它，并推送它在队列中的所有子节点。
在一般树的情况下，我们将子节点存储在向量中。因此，我们将向量的所有元素放入队列中。

## C++

```
// CPP program to do level order traversal
// of a generic tree
#include <bits/stdc++.h>
using namespace std;

// Represents a node of an n-ary tree
struct Node
{
    int key;
    vector<Node *>child;
};

 // Utility function to create a new tree node
Node *newNode(int key)
{
    Node *temp = new Node;
    temp->key = key;
    return temp;
}

// Prints the n-ary tree level wise
void LevelOrderTraversal(Node * root)
{
    if (root==NULL)
        return;

    // Standard level order traversal code
    // using queue
    queue<Node *> q;  // Create a queue
    q.push(root); // Enqueue root
    while (!q.empty())
    {
        int n = q.size();

        // If this node has children
        while (n > 0)
        {
            // Dequeue an item from queue and print it
            Node * p = q.front();
            q.pop();
            cout << p->key << " ";

            // Enqueue all children of the dequeued item
            for (int i=0; i<p->child.size(); i++)
                q.push(p->child[i]);
            n--;
        }

        cout << endl; // Print new line between two levels
    }
}

// Driver program
int main()
{
    /*   Let us create below tree
    *              10
    *        /   /    \   \
    *        2  34    56   100
    *       / \         |   /  | \
    *      77  88       1   7  8  9
    */
    Node *root = newNode(10);
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(34));
    (root->child).push_back(newNode(56));
    (root->child).push_back(newNode(100));
    (root->child[0]->child).push_back(newNode(77));
    (root->child[0]->child).push_back(newNode(88));
    (root->child[2]->child).push_back(newNode(1));
    (root->child[3]->child).push_back(newNode(7));
    (root->child[3]->child).push_back(newNode(8));
    (root->child[3]->child).push_back(newNode(9));

    cout << "Level order traversal Before Mirroring\n";
    LevelOrderTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to do level order traversal
// of a generic tree
import java.util.*;

class GFG
{

// Represents a node of an n-ary tree
static class Node
{
    int key;
    Vector<Node >child = new Vector<>();
};

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    return temp;
}

// Prints the n-ary tree level wise
static void LevelOrderTraversal(Node root)
{
    if (root == null)
        return;

    // Standard level order traversal code
    // using queue
    Queue<Node > q = new LinkedList<>(); // Create a queue
    q.add(root); // Enqueue root
    while (!q.isEmpty())
    {
        int n = q.size();

        // If this node has children
        while (n > 0)
        {
            // Dequeue an item from queue
            // and print it
            Node p = q.peek();
            q.remove();
            System.out.print(p.key + " ");

            // Enqueue all children of
            // the dequeued item
            for (int i = 0; i < p.child.size(); i++)
                q.add(p.child.get(i));
            n--;
        }

        // Print new line between two levels
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{

    /* Let us create below tree
    *             10
    *     / / \ \
    *     2 34 56 100
    *     / \         | / | \
    *     77 88     1 7 8 9
    */
    Node root = newNode(10);
    (root.child).add(newNode(2));
    (root.child).add(newNode(34));
    (root.child).add(newNode(56));
    (root.child).add(newNode(100));
    (root.child.get(0).child).add(newNode(77));
    (root.child.get(0).child).add(newNode(88));
    (root.child.get(2).child).add(newNode(1));
    (root.child.get(3).child).add(newNode(7));
    (root.child.get(3).child).add(newNode(8));
    (root.child.get(3).child).add(newNode(9));

    System.out.println("Level order traversal " +
                            "Before Mirroring ");
    LevelOrderTraversal(root);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to do level order traversal
# of a generic tree

# Represents a node of an n-ary tree
class Node:

    def __init__(self, key):

        self.key = key
        self.child = []

 # Utility function to create a new tree node
def newNode(key):   
    temp = Node(key)
    return temp

# Prints the n-ary tree level wise
def LevelOrderTraversal(root):

    if (root == None):
        return;

    # Standard level order traversal code
    # using queue
    q = []  # Create a queue
    q.append(root); # Enqueue root
    while (len(q) != 0):

        n = len(q);

        # If this node has children
        while (n > 0):

            # Dequeue an item from queue and print it
            p = q[0]
            q.pop(0);
            print(p.key, end=' ')

            # Enqueue all children of the dequeued item
            for i in range(len(p.child)):

                q.append(p.child[i]);
            n -= 1

        print() # Print new line between two levels

# Driver program
if __name__=='__main__':

    '''   Let us create below tree
                  10
            /   /    \   \
            2  34    56   100
           / \         |   /  | \
          77  88       1   7  8  9
    '''
    root = newNode(10);
    (root.child).append(newNode(2));
    (root.child).append(newNode(34));
    (root.child).append(newNode(56));
    (root.child).append(newNode(100));
    (root.child[0].child).append(newNode(77));
    (root.child[0].child).append(newNode(88));
    (root.child[2].child).append(newNode(1));
    (root.child[3].child).append(newNode(7));
    (root.child[3].child).append(newNode(8));
    (root.child[3].child).append(newNode(9));

    print("Level order traversal Before Mirroring")
    LevelOrderTraversal(root);

    # This code is contributed by rutvik_56.
```

## C#

```
// C# program to do level order traversal
// of a generic tree
using System;
using System.Collections.Generic;

class GFG
{

// Represents a node of an n-ary tree
public class Node
{
    public int key;
    public List<Node >child = new List<Node>();
};

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    return temp;
}

// Prints the n-ary tree level wise
static void LevelOrderTraversal(Node root)
{
    if (root == null)
        return;

    // Standard level order traversal code
    // using queue
    Queue<Node > q = new Queue<Node >(); // Create a queue
    q.Enqueue(root); // Enqueue root
    while (q.Count != 0)
    {
        int n = q.Count;

        // If this node has children
        while (n > 0)
        {
            // Dequeue an item from queue
            // and print it
            Node p = q.Peek();
            q.Dequeue();
            Console.Write(p.key + " ");

            // Enqueue all children of
            // the dequeued item
            for (int i = 0; i < p.child.Count; i++)
                q.Enqueue(p.child[i]);
            n--;
        }

        // Print new line between two levels
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{

    /* Let us create below tree
    *             10
    *     / / \ \
    *     2 34 56 100
    *     / \         | / | \
    *     77 88     1 7 8 9
    */
    Node root = newNode(10);
    (root.child).Add(newNode(2));
    (root.child).Add(newNode(34));
    (root.child).Add(newNode(56));
    (root.child).Add(newNode(100));
    (root.child[0].child).Add(newNode(77));
    (root.child[0].child).Add(newNode(88));
    (root.child[2].child).Add(newNode(1));
    (root.child[3].child).Add(newNode(7));
    (root.child[3].child).Add(newNode(8));
    (root.child[3].child).Add(newNode(9));

    Console.WriteLine("Level order traversal " +
                           "Before Mirroring ");
    LevelOrderTraversal(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to do level order traversal
// of a generic tree

// Represents a node of an n-ary tree
class Node
{
    constructor()
    {
        this.key = 0;
        this.child = [];
    }
};

// Utility function to create a new tree node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    return temp;
}

// Prints the n-ary tree level wise
function LevelOrderTraversal(root)
{
    if (root == null)
        return;

    // Standard level order traversal code
    // using queue
    var q = []; // Create a queue
    q.push(root); // push root
    while (q.length != 0)
    {
        var n = q.length;

        // If this node has children
        while (n > 0)
        {
            // Dequeue an item from queue
            // and print it
            var p = q[0];
            q.shift();
            document.write(p.key + " ");

            // push all children of
            // the dequeued item
            for (var i = 0; i < p.child.length; i++)
                q.push(p.child[i]);
            n--;
        }

        // Print new line between two levels
        document.write("<br>");
    }
}

// Driver Code
/* Let us create below tree
*             10
*     / / \ \
*     2 34 56 100
*     / \         | / | \
*     77 88     1 7 8 9
*/
var root = newNode(10);
(root.child).push(newNode(2));
(root.child).push(newNode(34));
(root.child).push(newNode(56));
(root.child).push(newNode(100));
(root.child[0].child).push(newNode(77));
(root.child[0].child).push(newNode(88));
(root.child[2].child).push(newNode(1));
(root.child[3].child).push(newNode(7));
(root.child[3].child).push(newNode(8));
(root.child[3].child).push(newNode(9));
document.write("Level order traversal " +
                       "Before Mirroring <br>");
LevelOrderTraversal(root);

</script>
```

**输出:**

```
10 
2 34 56 100 
77 88 1 7 8 9
```

本文由 **Raghav Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。