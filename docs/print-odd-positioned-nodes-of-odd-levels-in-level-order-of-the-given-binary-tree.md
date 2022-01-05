# 按照给定二叉树的级别顺序打印奇数级别的奇数位置节点

> 原文:[https://www . geeksforgeeks . org/print-奇数层节点-给定二叉树的逐层排序/](https://www.geeksforgeeks.org/print-odd-positioned-nodes-of-odd-levels-in-level-order-of-the-given-binary-tree/)

给定一棵二叉树，任务是在树的级别顺序遍历中打印奇数级别的奇数位置节点。根被认为是级别 **0** ，任何级别的最左边的节点被认为是位置 **0** 的节点。
**例:**

```
Input:
           1
         /    \
        2       3
      / \      /  \
     4   5    6    7
        /  \     
       8    9
      /      \
     10       11
Output: 3 9

Input:
      2
    /   \
   4     15
  /     /
 45   17
Output: 15
```

先决条件–[偶数层的偶数定位元素](https://www.geeksforgeeks.org/print-even-positioned-nodes-of-even-levels-in-level-order-of-the-given-binary-tree/)
**方法:**要逐层打印节点，请使用层级顺序遍历。思路基于[逐行打印级次遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)。为此，逐级遍历节点，并在每一级后切换奇数级标志。同样，将每一级中的第二个节点标记为奇数位置，并在每次处理下一个节点后切换它。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
};

// Iterative method to do level order
// traversal line by line
void printOddLevelOddNodes(Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue for level
    // order traversal
    queue<Node*> q;

    // Enqueue root and initialize level as even
    q.push(root);
    bool evenLevel = true;

    while (1) {

        // nodeCount (queue size) indicates
        // number of nodes in the current level
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Mark 1st node as even positioned
        bool evenNodePosition = true;

        // Dequeue all the nodes of current level
        // and Enqueue all the nodes of next level
        while (nodeCount > 0) {
            Node* node = q.front();

            // Print only even positioned
            // nodes of even levels
            if (!evenLevel && !evenNodePosition)
                cout << node->data << " ";
            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;

            // Switch the even position flag
            evenNodePosition = !evenNodePosition;
        }

        // Switch the even level flag
        evenLevel = !evenLevel;
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
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->right->left = newNode(8);
    root->left->right->right = newNode(9);
    root->left->right->left->left = newNode(10);
    root->left->right->right->right = newNode(11);

    printOddLevelOddNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{

static class Node
{
    int data;
    Node left, right;
};

// Iterative method to do level order
// traversal line by line
static void printOddLevelOddNodes(Node root)
{
    // Base Case
    if (root == null)
        return;

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new LinkedList<>();

    // Enqueue root and initialize level as even
    q.add(root);
    boolean evenLevel = true;

    while (true)
    {

        // nodeCount (queue size) indicates
        // number of nodes in the current level
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Mark 1st node as even positioned
        boolean evenNodePosition = true;

        // Dequeue all the nodes of current level
        // and Enqueue all the nodes of next level
        while (nodeCount > 0)
        {
            Node node = q.peek();

            // Print only even positioned
            // nodes of even levels
            if (!evenLevel && !evenNodePosition)
                System.out.print(node.data + " ");
            q.remove();
            if (node.left != null)
                q.add(node.left);
            if (node.right != null)
                q.add(node.right);
            nodeCount--;

            // Switch the even position flag
            evenNodePosition = !evenNodePosition;
        }

        // Switch the even level flag
        evenLevel = !evenLevel;
    }
}

// Utility method to create a node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
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
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.left.left = newNode(10);
    root.left.right.right.right = newNode(11);

    printOddLevelOddNodes(root);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of the approach

# Utility method to create a node
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Iterative method to do level order
# traversal line by line
def printOddLevelOddNodes(root):
    # Base Case
    if (root == None):
        return

    # Create an empty queue for level
    # order traversal
    q =[]

    # Enqueue root and initialize level as even
    q.append(root)
    evenLevel = True

    while (1):

        # nodeCount (queue size) indicates
        # number of nodes in the current level
        nodeCount = len(q)
        if (nodeCount == 0):
            break

        # Mark 1st node as even positioned
        evenNodePosition = True

        # Dequeue all the nodes of current level
        # and Enqueue all the nodes of next level
        while (nodeCount > 0):
            node = q[0]
            # Pronly even positioned
            # nodes of even levels
            if not evenLevel and not evenNodePosition:
                print(node.data, end =" ")
            q.pop(0)
            if (node.left != None):
                q.append(node.left)
            if (node.right != None):
                q.append(node.right)
            nodeCount-= 1

            # Switch the even position flag
            evenNodePosition = not evenNodePosition

        # Switch the even level flag
        evenLevel = not evenLevel

# Driver code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    root.left.right.left = newNode(8)
    root.left.right.right = newNode(9)
    root.left.right.left.left = newNode(10)
    root.left.right.right.right = newNode(11)

    printOddLevelOddNodes(root)
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

public class Node
{
    public int data;
    public Node left, right;
};

// Iterative method to do level order
// traversal line by line
static void printOddLevelOddNodes(Node root)
{
    // Base Case
    if (root == null)
        return;

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new Queue<Node>();

    // Enqueue root and initialize level as even
    q.Enqueue(root);
    bool evenLevel = true;

    while (true)
    {

        // nodeCount (queue size) indicates
        // number of nodes in the current level
        int nodeCount = q.Count;
        if (nodeCount == 0)
            break;

        // Mark 1st node as even positioned
        bool evenNodePosition = true;

        // Dequeue all the nodes of current level
        // and Enqueue all the nodes of next level
        while (nodeCount > 0)
        {
            Node node = q.Peek();

            // Print only even positioned
            // nodes of even levels
            if (!evenLevel && !evenNodePosition)
                Console.Write(node.data + " ");
            q.Dequeue();
            if (node.left != null)
                q.Enqueue(node.left);
            if (node.right != null)
                q.Enqueue(node.right);
            nodeCount--;

            // Switch the even position flag
            evenNodePosition = !evenNodePosition;
        }

        // Switch the even level flag
        evenLevel = !evenLevel;
    }
}

// Utility method to create a node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
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
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.left.left = newNode(10);
    root.left.right.right.right = newNode(11);

    printOddLevelOddNodes(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Iterative method to do level order
    // traversal line by line
    function printOddLevelOddNodes(root)
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty queue for level
        // order traversal
        let q = [];

        // Enqueue root and initialize level as even
        q.push(root);
        let evenLevel = true;

        while (true)
        {

            // nodeCount (queue size) indicates
            // number of nodes in the current level
            let nodeCount = q.length;
            if (nodeCount == 0)
                break;

            // Mark 1st node as even positioned
            let evenNodePosition = true;

            // Dequeue all the nodes of current level
            // and Enqueue all the nodes of next level
            while (nodeCount > 0)
            {
                let node = q[0];

                // Print only even positioned
                // nodes of even levels
                if (!evenLevel && !evenNodePosition)
                    document.write(node.data + " ");
                q.shift();
                if (node.left != null)
                    q.push(node.left);
                if (node.right != null)
                    q.push(node.right);
                nodeCount--;

                // Switch the even position flag
                evenNodePosition = !evenNodePosition;
            }

            // Switch the even level flag
            evenLevel = !evenLevel;
        }
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
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.left.left = newNode(10);
    root.left.right.right.right = newNode(11);

    printOddLevelOddNodes(root);

</script>
```

**Output:** 

```
3 9
```