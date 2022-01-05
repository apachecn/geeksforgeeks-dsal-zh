# 检查二叉树中的两个节点是否是表兄弟| Set-2

> 原文:[https://www . geeksforgeeks . org/check-如果两个节点是二进制树集中的表亲-2/](https://www.geeksforgeeks.org/check-if-two-nodes-are-cousins-in-a-binary-tree-set-2/)

给定一棵二叉树，两个节点说' a '和' b '，确定两个给定的节点是否是彼此的表兄弟。
如果两个节点处于同一级别，并且有不同的父节点，则它们是彼此的表亲。
**例**:

```
     6
   /   \
  3     5
 / \   / \
7   8 1   3
Say two node be 7 and 1, result is TRUE.
Say two nodes are 3 and 5, result is FALSE.
Say two nodes are 7 and 5, result is FALSE.
```

在[集合-1](https://www.geeksforgeeks.org/check-two-nodes-cousins-binary-tree/) 中，已经讨论了通过执行二叉树的三次遍历来发现给定节点是否是表兄弟的解决方案。这个问题可以通过执行级别顺序遍历来解决。其思想是使用队列来执行级别顺序遍历，其中每个队列元素都是一对节点和该节点的父节点。对于在级别顺序遍历中访问的每个节点，检查该节点是第一个给定节点还是第二个给定节点。如果找到任何节点，存储该节点的父节点。执行级别顺序遍历时，一次遍历一个级别。如果在给定的级别中找到两个节点，则比较它们的父值，以检查它们是否是兄弟节点。如果在给定级别找到一个节点，而没有找到另一个节点，则给定节点不是表兄弟。
以下是上述办法的实施:

## C++

```
// CPP program to check if two Nodes in
// a binary tree are cousins
// using level-order traversals
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new
// Binary Tree Node
struct Node* newNode(int item)
{
    struct Node* temp = (struct Node*)malloc(sizeof(struct Node));
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Returns true if a and b are cousins,
// otherwise false.
bool isCousin(Node* root, Node* a, Node* b)
{
    if (root == NULL)
        return false;

    // To store parent of node a.
    Node* parA = NULL;

    // To store parent of node b.
    Node* parB = NULL;

    // queue to perform level order
    // traversal. Each element of
    // queue is a pair of node and
    // its parent.
    queue<pair<Node*, Node*> > q;

    // Dummy node to act like parent
    // of root node.
    Node* tmp = newNode(-1);

    // To store front element of queue.
    pair<Node*, Node*> ele;

    // Push root to queue.
    q.push(make_pair(root, tmp));
    int levSize;

    while (!q.empty()) {

        // find number of elements in
        // current level.
        levSize = q.size();
        while (levSize) {

            ele = q.front();
            q.pop();

            // check if current node is node a
            // or node b or not.
            if (ele.first->data == a->data) {
                parA = ele.second;
            }

            if (ele.first->data == b->data) {
                parB = ele.second;
            }

            // push children of current node
            // to queue.
            if (ele.first->left) {
                q.push(make_pair(ele.first->left, ele.first));
            }

            if (ele.first->right) {
                q.push(make_pair(ele.first->right, ele.first));
            }

            levSize--;

            // If both nodes are found in
            // current level then no need
            // to traverse current level further.
            if (parA && parB)
                break;
        }

        // Check if both nodes are siblings
        // or not.
        if (parA && parB) {
            return parA != parB;
        }

        // If one node is found in current level
        // and another is not found, then
        // both nodes are not cousins.
        if ((parA && !parB) || (parB && !parA)) {
            return false;
        }
    }

    return false;
}
// Driver Code
int main()
{
    /*
            1
           /  \
          2    3
         / \  / \
        4   5 6  7
             \ \
             15 8
    */

    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->right->right = newNode(15);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    struct Node *Node1, *Node2;
    Node1 = root->left->left;
    Node2 = root->right->right;

    isCousin(root, Node1, Node2) ? puts("Yes") : puts("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two Nodes in
// a binary tree are cousins
// using level-order traversals
import java.util.*;
import javafx.util.Pair;

// User defined node class
class Node
{
    int data;
    Node left, right;

    // Constructor to create a new tree node
    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // Returns true if a and b are cousins,
    // otherwise false.
    boolean isCousin(Node node, Node a, Node b)
    {
        if(node == null)
            return false;

        // To store parent of node a.
        Node parA = null;

        // To store parent of node b.
        Node parB = null;

        // queue to perform level order
        // traversal. Each element of
        // queue is a pair of node and
        // its parent.
        Queue<Pair <Node,Node>> q = new LinkedList<> ();

        // Dummy node to act like parent
        // of root node.
        Node tmp = new Node(-1);

        // To store front element of queue.
        Pair<Node, Node> ele;

        // Push root to queue.
        q.add(new Pair <Node,Node> (node, tmp));

        int levelSize;

        while(!q.isEmpty())
        {

            // find number of elements in
            // current level.
            levelSize = q.size();
            while(levelSize != 0)
            {
                ele = q.peek();
                q.remove();

                // check if current node is node a
                // or node b or not.
                if(ele.getKey().data == a.data)
                    parA = ele.getValue();

                if(ele.getKey().data == b.data)
                    parB = ele.getValue();

                // push children of current node
                // to queue.
                if(ele.getKey().left != null)
                    q.add(new Pair<Node, Node>(ele.getKey().left, ele.getKey()));

                if(ele.getKey().right != null)
                    q.add(new Pair<Node, Node>(ele.getKey().right, ele.getKey()));

                levelSize--;

                // If both nodes are found in
                // current level then no need
                // to traverse current level further.
                if(parA != null && parB != null)
                    break;
            }

            // Check if both nodes are siblings
            // or not.
            if(parA != null && parB != null)
                return parA != parB;

            // If one node is found in current level
            // and another is not found, then
            // both nodes are not cousins.
            if ((parA!=null && parB==null) || (parB!=null && parA==null))
                return false;
        }

        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.left.right.right = new Node(15);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);

        Node Node1, Node2;
        Node1 = tree.root.left.right.right;
        Node2 = tree.root.right.left.right;
        if (tree.isCousin(tree.root, Node1, Node2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by shubham96301
```

## 蟒蛇 3

```
# Python3 program to check if two
# Nodes in a binary tree are cousins
# using level-order traversals

# A Binary Tree Node
class Node: 

    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None

# Returns True if a and b
# are cousins, otherwise False.
def isCousin(root, a, b):

    if root == None:
        return False

    # To store parent of node a.
    parA = None

    # To store parent of node b.
    parB = None

    # queue to perform level order
    # traversal. Each element of queue
    # is a pair of node and its parent.
    q = []

    # Dummy node to act like
    # parent of root node.
    tmp = Node(-1)

    # Push root to queue.
    q.append((root, tmp))

    while len(q) > 0: 

        # find number of elements in
        # current level.
        levSize = len(q)
        while levSize: 

            ele = q.pop(0)

            # check if current node is
            # node a or node b or not.
            if ele[0].data == a.data: 
                parA = ele[1]

            if ele[0].data == b.data: 
                parB = ele[1]

            # push children of
            # current node to queue.
            if ele[0].left: 
                q.append((ele[0].left, ele[0]))

            if ele[0].right: 
                q.append((ele[0].right, ele[0]))
            levSize -= 1

            # If both nodes are found in
            # current level then no need
            # to traverse current level further.
            if parA and parB:
                break

        # Check if both nodes
        # are siblings or not.
        if parA and parB: 
            return parA != parB

        # If one node is found in current level
        # and another is not found, then
        # both nodes are not cousins.
        if (parA and not parB) or (parB and not parA):
            return False

    return False

# Driver Code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.left.right.right = Node(15)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.right.left.right = Node(8)

    Node1 = root.left.left
    Node2 = root.right.right

    if isCousin(root, Node1, Node2):
        print('Yes')
    else:
        print('No')

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to check if two Nodes in
// a binary tree are cousins
// using level-order traversals
using System;
using System.Collections.Generic;

// User defined node class
public class Node
{
    public int data;
    public Node left, right;

    // Constructor to create a new tree node
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}
// User defined pair class
public class Pair
{

    public Node first, second;

    // Constructor to create a new tree node
    public Pair(Node first, Node second)
    {
        this.first = first;
        this.second = second;
    }
}

class BinaryTree
{
    Node root;

    // Returns true if a and b are cousins,
    // otherwise false.
    Boolean isCousin(Node node, Node a, Node b)
    {
        if(node == null)
            return false;

        // To store parent of node a.
        Node parA = null;

        // To store parent of node b.
        Node parB = null;

        // queue to perform level order
        // traversal. Each element of
        // queue is a pair of node and
        // its parent.
        Queue<Pair > q = new Queue<Pair > ();

        // Dummy node to act like parent
        // of root node.
        Node tmp = new Node(-1);

        // To store front element of queue.
        Pair ele;

        // Push root to queue.
        q.Enqueue(new Pair (node, tmp));

        int levelSize;

        while(q.Count>0)
        {

            // find number of elements in
            // current level.
            levelSize = q.Count;
            while(levelSize != 0)
            {
                ele = q.Peek();
                q.Dequeue();

                // check if current node is node a
                // or node b or not.
                if(ele.first.data == a.data)
                    parA = ele.second;

                if(ele.first.data == b.data)
                    parB = ele.second;

                // push children of current node
                // to queue.
                if(ele.first.left != null)
                    q.Enqueue(new Pair(ele.first.left, ele.first));

                if(ele.first.right != null)
                    q.Enqueue(new Pair(ele.first.right, ele.first));

                levelSize--;

                // If both nodes are found in
                // current level then no need
                // to traverse current level further.
                if(parA != null && parB != null)
                    break;
            }

            // Check if both nodes are siblings
            // or not.
            if(parA != null && parB != null)
                return parA != parB;

            // If one node is found in current level
            // and another is not found, then
            // both nodes are not cousins.
            if ((parA != null && parB == null) || (parB != null && parA == null))
                return false;
        }

        return false;
    }

    // Driver code
    public static void Main(String []args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.left.right.right = new Node(15);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);

        Node Node1, Node2;
        Node1 = tree.root.left.right.right;
        Node2 = tree.root.right.left.right;
        if (tree.isCousin(tree.root, Node1, Node2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript program to check if two Nodes in
// a binary tree are cousins
// using level-order traversals

// User defined node class
class Node
{

    // Constructor to create a new tree node
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }

}
// User defined pair class
class Pair
{

    // Constructor to create a new tree node
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }

}

var root = null;
// Returns true if a and b are cousins,
// otherwise false.
function isCousin(node, a, b)
{
    if(node == null)
        return false;

    // To store parent of node a.
    var parA = null;
    // To store parent of node b.
    var parB = null;
    // queue to perform level order
    // traversal. Each element of
    // queue is a pair of node and
    // its parent.
    var q = [];
    // Dummy node to act like parent
    // of root node.
    var tmp = new Node(-1);
    // To store front element of queue.
    var ele;
    // Push root to queue.
    q.push(new Pair (node, tmp));
    var levelSize;
    while(q.length>0)
    {
        // find number of elements in
        // current level.
        levelSize = q.length;
        while(levelSize != 0)
        {
            ele = q[0];
            q.shift();
            // check if current node is node a
            // or node b or not.
            if(ele.first.data == a.data)
                parA = ele.second;
            if(ele.first.data == b.data)
                parB = ele.second;
            // push children of current node
            // to queue.
            if(ele.first.left != null)
                q.push(new Pair(ele.first.left, ele.first));
            if(ele.first.right != null)
                q.push(new Pair(ele.first.right, ele.first));
            levelSize--;
            // If both nodes are found in
            // current level then no need
            // to traverse current level further.
            if(parA != null && parB != null)
                break;
        }
        // Check if both nodes are siblings
        // or not.
        if(parA != null && parB != null)
            return parA != parB;
        // If one node is found in current level
        // and another is not found, then
        // both nodes are not cousins.
        if ((parA != null && parB == null) || (parB != null
        && parA == null))
            return false;
    }
    return false;
}
// Driver code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.left.right.right = new Node(15);
root.right.left = new Node(6);
root.right.right = new Node(7);
root.right.left.right = new Node(8);
var Node1, Node2;
Node1 = root.left.right.right;
Node2 = root.right.left.right;
if (isCousin(root, Node1, Node2))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)