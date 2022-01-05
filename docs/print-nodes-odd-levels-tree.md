# 打印树的奇数层节点

> 原文:[https://www.geeksforgeeks.org/print-nodes-odd-levels-tree/](https://www.geeksforgeeks.org/print-nodes-odd-levels-tree/)

给定一个二叉树，以任意顺序打印奇数层的节点。根被认为是级别 1。

```
For example consider the following tree
          1
       /     \
      2       3
    /   \       \
   4     5       6
        /  \     /
       7    8   9

Output  1 4 5 6
```

**方法 1(递归)**

其思想是将初始级别作为奇数传递，并在每次递归调用中切换级别标志。对于每个节点，如果设置了奇数标志，则打印它。

## C++

```
// Recursive C++ program to print odd level nodes
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* left, *right;
};

void printOddNodes(Node *root, bool isOdd = true)
{
    // If empty tree
    if (root == NULL)
      return;

    // If current node is of odd level
    if (isOdd)
       cout << root->data << " " ;

    // Recur for children with isOdd
    // switched.
    printOddNodes(root->left, !isOdd);
    printOddNodes(root->right, !isOdd);
}

// Utility method to create a node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    printOddNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to print odd level nodes
class GfG {

static class Node {
    int data;
    Node left, right;
}

static void printOddNodes(Node root, boolean isOdd)
{
    // If empty tree
    if (root == null)
    return;

    // If current node is of odd level
    if (isOdd == true)
    System.out.print(root.data + " ");

    // Recur for children with isOdd
    // switched.
    printOddNodes(root.left, !isOdd);
    printOddNodes(root.right, !isOdd);
}

// Utility method to create a node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    printOddNodes(root, true);

}
}
```

## 蟒蛇 3

```
# Recursive Python3 program to print
# odd level nodes

# Utility method to create a node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

def printOddNodes(root, isOdd = True):

    # If empty tree
    if (root == None):
        return

    # If current node is of odd level
    if (isOdd):
        print(root.data, end = " ")

    # Recur for children with isOdd
    # switched.
    printOddNodes(root.left, not isOdd)
    printOddNodes(root.right, not isOdd)

# Driver code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    printOddNodes(root)

# This code is contributed by PranchalK
```

## C#

```
using System;

// Recursive C# program to print odd level nodes 
public class GfG
{

public class Node
{
    public int data;
    public Node left, right;
}

public static void printOddNodes(Node root, bool isOdd)
{
    // If empty tree 
    if (root == null)
    {
    return;
    }

    // If current node is of odd level 
    if (isOdd == true)
    {
    Console.Write(root.data + " ");
    }

    // Recur for children with isOdd 
    // switched. 
    printOddNodes(root.left, !isOdd);
    printOddNodes(root.right, !isOdd);
}

// Utility method to create a node 
public static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Driver code 
public static void Main(string[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    printOddNodes(root, true);

}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // Recursive JavaScript program to print odd level nodes

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    function printOddNodes(root, isOdd)
    {
        // If empty tree
        if (root == null)
        return;

        // If current node is of odd level
        if (isOdd == true)
        document.write(root.data + " ");

        // Recur for children with isOdd
        // switched.
        printOddNodes(root.left, !isOdd);
        printOddNodes(root.right, !isOdd);
    }

    // Utility method to create a node
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    printOddNodes(root, true);

</script>
```

**输出:**

```
1 4 5
```

**时间复杂度:** O(n)

**方法 2(迭代)**

上面的代码以预定的方式打印节点。如果我们希望逐级打印节点，我们可以使用级别顺序遍历。这个想法是基于[打印级别顺序逐行遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)
我们逐级遍历节点。我们在每一级后切换奇数级标志。

## C++

```
// Iterative C++ program to print odd level nodes
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* left, *right;
};

// Iterative method to do level order traversal line by line
void printOddNodes(Node *root)
{
    // Base Case
    if (root == NULL)  return;

    // Create an empty queue for level
    // order traversal
    queue<Node *> q;

    // Enqueue root and initialize level as odd
    q.push(root);
    bool isOdd = true; 

    while (1)
    {
        // nodeCount (queue size) indicates
        // number of nodes at current level.
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            Node *node = q.front();
            if (isOdd)
               cout << node->data << " ";
            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;
        }

        isOdd = !isOdd;
    }
}

// Utility method to create a node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    printOddNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to print odd level nodes
import java.util.*;
class GfG {

static class Node {
    int data;
    Node left, right;
}

// Iterative method to do level order traversal line by line
static void printOddNodes(Node root)
{
    // Base Case
    if (root == null) return;

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new LinkedList<Node> ();

    // Enqueue root and initialize level as odd
    q.add(root);
    boolean isOdd = true;

    while (true)
    {
        // nodeCount (queue size) indicates
        // number of nodes at current level.
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            Node node = q.peek();
            if (isOdd == true)
            System.out.print(node.data + " ");
            q.remove();
            if (node.left != null)
                q.add(node.left);
            if (node.right != null)
                q.add(node.right);
            nodeCount--;
        }

        isOdd = !isOdd;
    }
}

// Utility method to create a node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    printOddNodes(root);
}
}
```

## 蟒蛇 3

```
# Iterative Python3 program to prodd
# level nodes

# A Binary Tree Node
# Utility function to create a
# new tree Node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Iterative method to do level order
# traversal line by line
def printOddNodes(root) :

    # Base Case
    if (root == None):
        return

    # Create an empty queue for 
    # level order traversal
    q = []

    # Enqueue root and initialize
    # level as odd
    q.append(root)
    isOdd = True

    while (1) :

        # nodeCount (queue size) indicates
        # number of nodes at current level.
        nodeCount = len(q)
        if (nodeCount == 0) :
            break

        # Dequeue all nodes of current level
        # and Enqueue all nodes of next level
        while (nodeCount > 0):

            node = q[0]
            if (isOdd):
                print(node.data, end = " ")
            q.pop(0)
            if (node.left != None) :
                q.append(node.left)
            if (node.right != None) :
                q.append(node.right)
            nodeCount -= 1

        isOdd = not isOdd

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    printOddNodes(root)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// Iterative C# program to
// print odd level nodes
using System;
using System.Collections.Generic;

public class GfG
{
    public class Node
    {
        public int data;
        public Node left, right;
    }

    // Iterative method to do level
    // order traversal line by line
    static void printOddNodes(Node root)
    {
        // Base Case
        if (root == null) return;

        // Create an empty queue for level
        // order traversal
        Queue<Node> q = new Queue<Node> ();

        // Enqueue root and initialize level as odd
        q.Enqueue(root);
        bool isOdd = true;

        while (true)
        {
            // nodeCount (queue size) indicates
            // number of nodes at current level.
            int nodeCount = q.Count;
            if (nodeCount == 0)
                break;

            // Dequeue all nodes of current level
            // and Enqueue all nodes of next level
            while (nodeCount > 0)
            {
                Node node = q.Peek();
                if (isOdd == true)
                    Console.Write(node.data + " ");
                q.Dequeue();
                if (node.left != null)
                    q.Enqueue(node.left);
                if (node.right != null)
                    q.Enqueue(node.right);
                nodeCount--;
            }
            isOdd = !isOdd;
        }
    }

    // Utility method to create a node
    static Node newNode(int data)
    {
        Node node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;
        return (node);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        printOddNodes(root);
    }
}

// This code has been contributed
// by 29AjayKumar
```

## java 描述语言

```
<script>
// Iterative Javascript program to print odd level nodes

class Node
{
    constructor(data)
    {
        this.data=data;
        this.left=this.right=null;
    }
}

function printOddNodes(root)
{
    // Base Case
    if (root == null) return;

    // Create an empty queue for level
    // order traversal
    let q = [];

    // Enqueue root and initialize level as odd
    q.push(root);
    let isOdd = true;

    while (true)
    {
        // nodeCount (queue size) indicates
        // number of nodes at current level.
        let nodeCount = q.length;
        if (nodeCount == 0)
            break;

        // Dequeue all nodes of current level
        // and Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            let node = q[0];
            if (isOdd == true)
                document.write(node.data + " ");
            q.shift();
            if (node.left != null)
                q.push(node.left);
            if (node.right != null)
                q.push(node.right);
            nodeCount--;
        }

        isOdd = !isOdd;
    }
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
printOddNodes(root);

// This code is contributed by rag2127
</script>
```

**输出:**

```
1 4 5
```

**时间复杂度:** O(n)

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。