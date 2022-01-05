# 使用堆栈

反转完美二叉树的交替层次

> 原文:[https://www . geesforgeks . org/反向-交替-层次-完美-二叉树-使用-栈/](https://www.geeksforgeeks.org/reverse-alternate-levels-of-a-perfect-binary-tree-using-stack/)

给定一个[完美二叉树](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)，任务是反转二叉树的交替级节点。
**例:**

```
Input:
               a
            /     \
           b       c
         /  \     /  \
        d    e    f    g
       / \  / \  / \  / \
       h  i j  k l  m  n  o  
Output:
Inorder Traversal of given tree
h d i b j e k a l f m c n g o 
Inorder Traversal of modified tree
o d n c m e l a k f j b i g h

Input:
               a
              / \
             b   c
Output:
Inorder Traversal of given tree
b a c 
Inorder Traversal of modified tree
c a b
```

**方法:**问题的另一种方法在这里[讨论](https://www.geeksforgeeks.org/reverse-alternate-levels-binary-tree/)。在本文中，我们讨论一种涉及[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)的方法。
以深度优先的方式遍历树，对于每个级别，

*   如果**级别为奇数**，则按下堆栈中的左右子级(如果存在)。
*   如果**级别为偶数**，用栈顶替换当前节点的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A tree node
struct Node {
    char key;
    struct Node *left, *right;
};

// Utility function to create new Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
void inorder(Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

// Function to reverse alternate nodes
void reverseAlternate(Node* root)
{

    // Queue for depth first traversal
    queue<Node*> q;
    q.push(root);
    Node* temp;

    // Level of root considered to be 1
    int n, level = 1;

    // Stack to store nodes of a level
    stack<int> s;

    while (!q.empty()) {
        n = q.size();
        while (n--) {
            temp = q.front();
            q.pop();

            // If level is odd
            if (level % 2) {

                // Store the left and right child
                // in the stack
                if (temp->left) {
                    q.push(temp->left);
                    s.push(temp->left->key);
                }

                if (temp->right) {
                    q.push(temp->right);
                    s.push(temp->right->key);
                }
            }

            // If level is even
            else {

                // Replace the value of node
                // with top of the stack
                temp->key = s.top();
                s.pop();

                if (temp->left)
                    q.push(temp->left);
                if (temp->right)
                    q.push(temp->right);
            }
        }

        // Increment the level
        level++;
    }
}

// Driver code
int main()
{
    struct Node* root = newNode('a');
    root->left = newNode('b');
    root->right = newNode('c');
    root->left->left = newNode('d');
    root->left->right = newNode('e');
    root->right->left = newNode('f');
    root->right->right = newNode('g');
    root->left->left->left = newNode('h');
    root->left->left->right = newNode('i');
    root->left->right->left = newNode('j');
    root->left->right->right = newNode('k');
    root->right->left->left = newNode('l');
    root->right->left->right = newNode('m');
    root->right->right->left = newNode('n');
    root->right->right->right = newNode('o');

    cout << "Inorder Traversal of given tree\n";
    inorder(root);

    reverseAlternate(root);

    cout << "\nInorder Traversal of modified tree\n";
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GfG
{

// A tree node
static class Node
{
    char key;
    Node left, right;
}

// Utility function to create new Node
static Node newNode(char key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        System.out.print(root.key + " ");
        inorder(root.right);
    }
}

// Function to reverse alternate nodes
static void reverseAlternate(Node root)
{

    // Queue for depth first traversal
    Queue<Node> q = new LinkedList<Node> ();
    q.add(root);
    Node temp;

    // Level of root considered to be 1
    int n, level = 1;

    // Stack to store nodes of a level
    Stack<Character> s = new Stack<Character> ();

    while (!q.isEmpty())
    {
        n = q.size();
        while (n != 0)
        {
            if(!q.isEmpty())
            {
                temp = q.peek();
                q.remove();
            }
            else
            temp = null;

            // If level is odd
            if (level % 2 != 0)
            {

                // Store the left and right child
                // in the stack
                if (temp != null && temp.left != null)
                {
                    q.add(temp.left);
                    s.push(temp.left.key);
                }

                if (temp != null && temp.right != null)
                {
                    q.add(temp.right);
                    s.push(temp.right.key);
                }
            }

            // If level is even
            else
            {

                // Replace the value of node
                // with top of the stack
                temp.key = s.peek();
                s.pop();

                if (temp.left != null)
                    q.add(temp.left);
                if (temp.right != null)
                    q.add(temp.right);
            }
            n--;
        }

        // Increment the level
        level++;
    }
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode('a');
    root.left = newNode('b');
    root.right = newNode('c');
    root.left.left = newNode('d');
    root.left.right = newNode('e');
    root.right.left = newNode('f');
    root.right.right = newNode('g');
    root.left.left.left = newNode('h');
    root.left.left.right = newNode('i');
    root.left.right.left = newNode('j');
    root.left.right.right = newNode('k');
    root.right.left.left = newNode('l');
    root.right.left.right = newNode('m');
    root.right.right.left = newNode('n');
    root.right.right.right = newNode('o');

    System.out.println("Inorder Traversal of given tree");
    inorder(root);

    reverseAlternate(root);

    System.out.println("\nInorder Traversal of modified tree");
    inorder(root);
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# A tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Utility function to
# create new Node
def newNode(key):

    temp = Node(key)
    return temp

# Utility function to perform
# inorder traversal of the tree
def inorder(root):

    if (root != None):
        inorder(root.left);
        print(root.key,
              end = ' ')
        inorder(root.right);   

# Function to reverse
# alternate nodes
def reverseAlternate(root):

    # Queue for depth
    # first traversal
    q = []
    q.append(root);

    temp = None

    # Level of root considered
    # to be 1
    n = 0
    level = 1;

    # Stack to store nodes
    # of a level
    s = []

    while (len(q) != 0):       
        n = len(q);       
        while (n != 0):           
            n -= 1
            temp = q[0];
            q.pop(0);

            # If level is odd
            if (level % 2 != 0):

                # Store the left and
                # right child in the stack
                if (temp.left != None):
                    q.append(temp.left);
                    s.append(temp.left.key);

                if (temp.right != None):
                    q.append(temp.right);
                    s.append(temp.right.key);

            # If level is even
            else:

                # Replace the value of node
                # with top of the stack
                temp.key = s[-1];
                s.pop();

                if (temp.left != None):
                    q.append(temp.left);
                if (temp.right != None):
                    q.append(temp.right);

        # Increment the level
        level += 1;   

# Driver code
if __name__ == "__main__":

    root = newNode('a');
    root.left = newNode('b');
    root.right = newNode('c');
    root.left.left = newNode('d');
    root.left.right = newNode('e');
    root.right.left = newNode('f');
    root.right.right = newNode('g');
    root.left.left.left = newNode('h');
    root.left.left.right = newNode('i');
    root.left.right.left = newNode('j');
    root.left.right.right = newNode('k');
    root.right.left.left = newNode('l');
    root.right.left.right = newNode('m');
    root.right.right.left = newNode('n');
    root.right.right.right = newNode('o');

    print("Inorder Traversal of given tree")
    inorder(root);

    reverseAlternate(root);

    print("\nInorder Traversal of modified tree")
    inorder(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GfG
{

// A tree node
public class Node
{
    public char key;
    public Node left, right;
}

// Utility function to create new Node
static Node newNode(char key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + " ");
        inorder(root.right);
    }
}

// Function to reverse alternate nodes
static void reverseAlternate(Node root)
{

    // Queue for depth first traversal
    Queue q = new Queue ();
    q.Enqueue(root);
    Node temp;

    // Level of root considered to be 1
    int n, level = 1;

    // Stack to store nodes of a level
    Stack s = new Stack ();

    while (q.Count > 0)
    {
        n = q.Count;
        while (n != 0)
        {
            if(q.Count > 0)
            {
                temp = (Node)q.Peek();
                q.Dequeue();
            }
            else
            temp = null;

            // If level is odd
            if (level % 2 != 0)
            {

                // Store the left and right child
                // in the stack
                if (temp != null && temp.left != null)
                {
                    q.Enqueue(temp.left);
                    s.Push(temp.left.key);
                }

                if (temp != null && temp.right != null)
                {
                    q.Enqueue(temp.right);
                    s.Push(temp.right.key);
                }
            }

            // If level is even
            else
            {

                // Replace the value of node
                // with top of the stack
                temp.key =(char)s.Peek();
                s.Pop();

                if (temp.left != null)
                    q.Enqueue(temp.left);
                if (temp.right != null)
                    q.Enqueue(temp.right);
            }
            n--;
        }

        // Increment the level
        level++;
    }
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode('a');
    root.left = newNode('b');
    root.right = newNode('c');
    root.left.left = newNode('d');
    root.left.right = newNode('e');
    root.right.left = newNode('f');
    root.right.right = newNode('g');
    root.left.left.left = newNode('h');
    root.left.left.right = newNode('i');
    root.left.right.left = newNode('j');
    root.left.right.right = newNode('k');
    root.right.left.left = newNode('l');
    root.right.left.right = newNode('m');
    root.right.right.left = newNode('n');
    root.right.right.right = newNode('o');

    Console.WriteLine("Inorder Traversal of given tree");
    inorder(root);

    reverseAlternate(root);

    Console.WriteLine("\nInorder Traversal of modified tree");
    inorder(root);
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// A tree node
class Node
{
    constructor()
    {
        this.key = '';
        this.left = null;
        this.right = null;
    }
}

// Utility function to create new Node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
function inorder(root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write(root.key + " ");
        inorder(root.right);
    }
}

// Function to reverse alternate nodes
function reverseAlternate(root)
{

    // Queue for depth first traversal
    var q = [];
    q.push(root);
    var temp = null;

    // Level of root considered to be 1
    var n, level = 1;

    // Stack to store nodes of a level
    var s = [];

    while (q.length > 0)
    {
        n = q.length;
        while (n != 0)
        {
            if(q.length > 0)
            {
                temp = q[0];
                q.shift();
            }
            else
            temp = null;

            // If level is odd
            if (level % 2 != 0)
            {

                // Store the left and right child
                // in the stack
                if (temp != null && temp.left != null)
                {
                    q.push(temp.left);
                    s.push(temp.left.key);
                }

                if (temp != null && temp.right != null)
                {
                    q.push(temp.right);
                    s.push(temp.right.key);
                }
            }

            // If level is even
            else
            {

                // Replace the value of node
                // with top of the stack
                temp.key = s[s.length-1];
                s.pop();

                if (temp.left != null)
                    q.push(temp.left);
                if (temp.right != null)
                    q.push(temp.right);
            }
            n--;
        }

        // Increment the level
        level++;
    }
}

// Driver code
var root = newNode('a');
root.left = newNode('b');
root.right = newNode('c');
root.left.left = newNode('d');
root.left.right = newNode('e');
root.right.left = newNode('f');
root.right.right = newNode('g');
root.left.left.left = newNode('h');
root.left.left.right = newNode('i');
root.left.right.left = newNode('j');
root.left.right.right = newNode('k');
root.right.left.left = newNode('l');
root.right.left.right = newNode('m');
root.right.right.left = newNode('n');
root.right.right.right = newNode('o');
document.write("Inorder Traversal of given tree<br>");
inorder(root);
reverseAlternate(root);
document.write("<br>Inorder Traversal of modified tree<br>");
inorder(root);

</script>
```

**Output:** 

```
Inorder Traversal of given tree
h d i b j e k a l f m c n g o 
Inorder Traversal of modified tree
o d n c m e l a k f j b i g h
```