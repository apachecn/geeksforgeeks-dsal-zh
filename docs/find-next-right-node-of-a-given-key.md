# 找到给定键的下一个右节点

> 原文:[https://www . geesforgeks . org/find-next-right-node-of-a-给定密钥/](https://www.geeksforgeeks.org/find-next-right-node-of-a-given-key/)

给定一棵二叉树和二叉树中的一个键，找到给定键右边的节点。如果右侧没有节点，则返回空值。预期时间复杂度为 O(n)，其中 n 是给定二叉树中的节点数。

例如，考虑下面的二叉树。2 的输出是 6，4 的输出是 5。10、6 和 5 的输出为空。

```
                  10
               /      \
          2         6
           /   \         \ 
     8      4          5
```

**求解:**思路是对给定的二叉树做[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。当我们找到给定的键时，我们只需要检查层次顺序遍历中的下一个节点是否是同一层次的，如果是，我们返回下一个节点，否则返回 NULL。

## C++

```
/* Program to find next right of a given key */
#include <iostream>
#include <queue>
using namespace std;

// A Binary Tree Node
struct node
{
    struct node *left, *right;
    int key;
};

// Method to find next right of given key k, it returns NULL if k is
// not present in tree or k is the rightmost node of its level
node* nextRight(node *root, int k)
{
    // Base Case
    if (root == NULL)
        return 0;

    // Create an empty queue for level order traversal
    queue<node *> qn; // A queue to store node addresses
    queue<int> ql;   // Another queue to store node levels

    int level = 0;  // Initialize level as 0

    // Enqueue Root and its level
    qn.push(root);
    ql.push(level);

    // A standard BFS loop
    while (qn.size())
    {
        // dequeue an node from qn and its level from ql
        node *node = qn.front();
        level = ql.front();
        qn.pop();
        ql.pop();

        // If the dequeued node has the given key k
        if (node->key == k)
        {
            // If there are no more items in queue or given node is
            // the rightmost node of its level, then return NULL
            if (ql.size() == 0 || ql.front() != level)
               return NULL;

            // Otherwise return next node from queue of nodes
            return qn.front();
        }

        // Standard BFS steps: enqueue children of this node
        if (node->left != NULL)
        {
            qn.push(node->left);
            ql.push(level+1);
        }
        if (node->right != NULL)
        {
            qn.push(node->right);
            ql.push(level+1);
        }
    }

    // We reach here if given key x doesn't exist in tree
    return NULL;
}

// Utility function to create a new tree node
node* newNode(int key)
{
    node *temp = new node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to test above functions
void test(node *root, int k)
{
    node *nr = nextRight(root, k);
    if (nr != NULL)
      cout << "Next Right of " << k << " is " << nr->key << endl;
    else
      cout << "No next right node found for " << k << endl;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree given in the above example
    node *root = newNode(10);
    root->left = newNode(2);
    root->right = newNode(6);
    root->right->right = newNode(5);
    root->left->left = newNode(8);
    root->left->right = newNode(4);

    test(root, 10);
    test(root, 2);
    test(root, 6);
    test(root, 5);
    test(root, 8);
    test(root, 4);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next right of a given key

import java.util.LinkedList;
import java.util.Queue;

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // Method to find next right of given key k, it returns NULL if k is
    // not present in tree or k is the rightmost node of its level
    Node nextRight(Node first, int k)
    {
        // Base Case
        if (first == null)
            return null;

        // Create an empty queue for level order traversal
        // A queue to store node addresses
        Queue<Node> qn = new LinkedList<Node>();

        // Another queue to store node levels
        Queue<Integer> ql = new LinkedList<Integer>();  

        int level = 0;  // Initialize level as 0

        // Enqueue Root and its level
        qn.add(first);
        ql.add(level);

        // A standard BFS loop
        while (qn.size() != 0)
        {
            // dequeue an node from qn and its level from ql
            Node node = qn.peek();
            level = ql.peek();
            qn.remove();
            ql.remove();

            // If the dequeued node has the given key k
            if (node.data == k)
            {
                // If there are no more items in queue or given node is
                // the rightmost node of its level, then return NULL
                if (ql.size() == 0 || ql.peek() != level)
                    return null;

                // Otherwise return next node from queue of nodes
                return qn.peek();
            }

            // Standard BFS steps: enqueue children of this node
            if (node.left != null)
            {
                qn.add(node.left);
                ql.add(level + 1);
            }
            if (node.right != null)
            {
                qn.add(node.right);
                ql.add(level + 1);
            }
        }

        // We reach here if given key x doesn't exist in tree
        return null;
    }

    // A utility function to test above functions
    void test(Node node, int k)
    {
        Node nr = nextRight(root, k);
        if (nr != null)
            System.out.println("Next Right of " + k + " is " + nr.data);
        else
            System.out.println("No next right node found for " + k);
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(2);
        tree.root.right = new Node(6);
        tree.root.right.right = new Node(5);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(4);

        tree.test(tree.root, 10);
        tree.test(tree.root, 2);
        tree.test(tree.root, 6);
        tree.test(tree.root, 5);
        tree.test(tree.root, 8);
        tree.test(tree.root, 4);

    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find next right node of given key

# A Binary Tree Node
class Node:

    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Method to find next right of a given key k, it returns
# None if k is not present in tree or k is the rightmost
# node of its level
def nextRight(root, k):

    # Base Case
    if root is None:
        return 0

    # Create an empty queue for level order traversal
    qn =  [] # A queue to store node addresses
    q1 = [] # Another queue to store node levels

    level = 0

    # Enqueue root and its level
    qn.append(root)
    q1.append(level)

    # Standard BFS loop
    while(len(qn) > 0):

        # Dequeu an node from qn and its level from q1
        node = qn.pop(0)
        level = q1.pop(0)

        # If the dequeued node has the given key k
        if node.key == k :

            # If there are no more items in queue or given
            # node is the rightmost node of its level,
            # then return None
            if (len(q1) == 0 or q1[0] != level):
                return None

            # Otherwise return next node from queue of nodes
            return qn[0]

        # Standard BFS steps: enqueue children of this node
        if node.left is not None:
            qn.append(node.left)
            q1.append(level+1)

        if node.right is not None:
            qn.append(node.right)
            q1.append(level+1)

    # We reach here if given key x doesn't exist in tree
    return None

def test(root, k):
    nr = nextRight(root, k)
    if nr is not None:
        print "Next Right of " + str(k) + " is " + str(nr.key)
    else:
        print "No next right node found for " + str(k)

# Driver program to test above function
root = Node(10)
root.left = Node(2)
root.right = Node(6)
root.right.right = Node(5)
root.left.left = Node(8)
root.left.right = Node(4)

test(root, 10)
test(root, 2)
test(root, 6)
test(root, 5)
test(root, 8)
test(root, 4)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to find next right of a given key
using System;
using System.Collections.Generic;

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{
    Node root;

    // Method to find next right of given
    // key k, it returns NULL if k is
    // not present in tree or k is the
    // rightmost node of its level
    Node nextRight(Node first, int k)
    {
        // Base Case
        if (first == null)
            return null;

        // Create an empty queue for
        // level order traversal
        // A queue to store node addresses
        Queue<Node> qn = new Queue<Node>();

        // Another queue to store node levels
        Queue<int> ql = new Queue<int>();

        int level = 0; // Initialize level as 0

        // Enqueue Root and its level
        qn.Enqueue(first);
        ql.Enqueue(level);

        // A standard BFS loop
        while (qn.Count != 0)
        {
            // dequeue an node from
            // qn and its level from ql
            Node node = qn.Peek();
            level = ql.Peek();
            qn.Dequeue();
            ql.Dequeue();

            // If the dequeued node has the given key k
            if (node.data == k)
            {
                // If there are no more items
                // in queue or given node is
                // the rightmost node of its
                // level, then return NULL
                if (ql.Count == 0 || ql.Peek() != level)
                    return null;

                // Otherwise return next
                // node from queue of nodes
                return qn.Peek();
            }

            // Standard BFS steps: enqueue
            // children of this node
            if (node.left != null)
            {
                qn.Enqueue(node.left);
                ql.Enqueue(level + 1);
            }
            if (node.right != null)
            {
                qn.Enqueue(node.right);
                ql.Enqueue(level + 1);
            }
        }

        // We reach here if given
        // key x doesn't exist in tree
        return null;
    }

    // A utility function to test above functions
    void test(Node node, int k)
    {
        Node nr = nextRight(root, k);
        if (nr != null)
            Console.WriteLine("Next Right of " +
                        k + " is " + nr.data);
        else
            Console.WriteLine("No next right node found for " + k);
    }

    // Driver code
    public static void Main(String []args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(2);
        tree.root.right = new Node(6);
        tree.root.right.right = new Node(5);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(4);

        tree.test(tree.root, 10);
        tree.test(tree.root, 2);
        tree.test(tree.root, 6);
        tree.test(tree.root, 5);
        tree.test(tree.root, 8);
        tree.test(tree.root, 4);
    }
}

// This code has been contributed
// by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find next right of a given key

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = this.right = null;
    }
}

let root;

// Method to find next right of given key k,
// it returns NULL if k is not present in
// tree or k is the rightmost node of its level
function nextRight(first, k)
{

    // Base Case
    if (first == null)
        return null;

    // Create an empty queue for level
    // order traversal. A queue to
    // store node addresses
    let qn = [];

    // Another queue to store node levels
    let ql = [];

    // Initialize level as 0
    let level = 0; 

    // Enqueue Root and its level
    qn.push(first);
    ql.push(level);

    // A standard BFS loop
    while (qn.length != 0)
    {

        // dequeue an node from qn and its level from ql
        let node = qn[0];
        level = ql[0];
        qn.shift();
        ql.shift();

        // If the dequeued node has the given key k
        if (node.data == k)
        {

            // If there are no more items in queue
            // or given node is the rightmost node
            // of its level, then return NULL
            if (ql.length == 0 || ql[0] != level)
                return null;

            // Otherwise return next node
            // from queue of nodes
            return qn[0];
        }

        // Standard BFS steps: enqueue
        // children of this node
        if (node.left != null)
        {
            qn.push(node.left);
            ql.push(level + 1);
        }
        if (node.right != null)
        {
            qn.push(node.right);
            ql.push(level + 1);
        }
    }

    // We reach here if given key
    // x doesn't exist in tree
    return null;
}

// A utility function to test above functions
function test(node, k)
{
    let nr = nextRight(root, k);
    if (nr != null)
        document.write("Next Right of " + k +
                       " is " + nr.data + "<br>");
    else
        document.write("No next right node found for " +
                       k + "<br>");
}

// Driver code
root = new Node(10);
root.left = new Node(2);
root.right = new Node(6);
root.right.right = new Node(5);
root.left.left = new Node(8);
root.left.right = new Node(4);

test(root, 10);
test(root, 2);
test(root, 6);
test(root, 5);
test(root, 8);
test(root, 4);

// This code is contributed by rag2127

</script>
```

**输出:**

```
No next right node found for 10
Next Right of 2 is 6
No next right node found for 6
No next right node found for 5
Next Right of 8 is 4
Next Right of 4 is 5

```

**时间复杂度:**上面的代码是一个简单的 BFS 遍历代码，最多访问一个节点的每个入队和出队一次。因此，时间复杂度为 O(n)，其中 n 是给定二叉树中的节点数。
**练习:**写一个函数找到给定节点的左节点。如果左侧没有节点，则返回空值。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息