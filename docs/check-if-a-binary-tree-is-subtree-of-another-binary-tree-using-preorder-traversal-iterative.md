# 使用前序遍历检查一棵二叉树是否是另一棵二叉树的子树:迭代

> 原文:[https://www . geesforgeks . org/check-如果一棵二叉树是另一棵二叉树的子树-使用-preorder-遍历-迭代/](https://www.geeksforgeeks.org/check-if-a-binary-tree-is-subtree-of-another-binary-tree-using-preorder-traversal-iterative/)

给定两个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/) S 和 T，任务是检查 S 是否是树 T 的子树

**例如:**

```
Input:
Tree T - 
         1            
       /   \         
      2     3
    /  \   /  \  
   4   5  6    7

Tree S - 
      2
    /  \  
   4    5
Output: YES
Explanation:
The above tree is the subtree of the tree T,
Hence the output is YES
```

**方法:**想法是在预序遍历中遍历两棵树，并检查树的每个节点，该树的预序遍历与树 S 的预序遍历相同，注意空值，即通过将空值包括在遍历列表中，因为如果空值不被注意，那么两个不同的树可以具有相同的预序遍历。例如在树下的情况下–

```
    1           1
   /  \        /  \
  2    N      N    2  
 / \              / \
N   N            N   N

Pre-order Traversal of both the trees will be -
{1, 2} - In case of without taking care of null values
{1, 2, N, N, N} and {1, N, 2, N, N}
In case of taking care of null values.
```

**算法:**

*   声明一个堆栈，以跟踪节点的左右子节点。
*   推树 t 的根节点。
*   在堆栈不为空时运行一个循环，然后检查堆栈顶部节点的前序遍历是否相同，然后返回 true。
*   如果前序遍历与树不匹配，则从堆栈中弹出顶部节点，并推其弹出节点的左右子节点。

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// if a tree is a subtree of
// another binary tree

#include <bits/stdc++.h>
using namespace std;

// Structure of the
// binary tree node
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to create
// new node
Node* newNode(int x)
{
    Node* temp = (Node*)malloc(
                   sizeof(Node));
    temp->data = x;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}
// Function to check if two trees
// have same pre-order traversal
bool areTreeIdentical(Node* t1, Node* t2)
{
    stack<Node*> s1;
    stack<Node*> s2;
    Node* temp1;
    Node* temp2;
    s1.push(t1);
    s2.push(t2);

    // Loop to iterate over the stacks
    while (!s1.empty() && !s2.empty()) {
        temp1 = s1.top();
        temp2 = s2.top();
        s1.pop();
        s2.pop();
        // Both are None
        // hence they are equal
        if (temp1 == NULL &&
            temp2 == NULL)
            continue;

        // nodes are unequal
        if ((temp1 == NULL && temp2 != NULL) ||
           (temp1 != NULL && temp2 == NULL))
            return false;

        // nodes have unequal data
        if (temp1->data != temp2->data)
            return false;

        s1.push(temp1->right);
        s2.push(temp2->right);

        s1.push(temp1->left);
        s2.push(temp2->left);
    }
    // if both tree are identical
    // both stacks must be empty.
    if (s1.empty() && s2.empty())
        return true;
    else
        return false;
}
// Function to check if the Tree s
// is the subtree of the Tree T
bool isSubTree(Node* s, Node* t)
{
    // first we find the root of s in t
    // by traversing in pre order fashion
    stack<Node*> stk;
    Node* temp;
    stk.push(t);
    while (!stk.empty()) {
        temp = stk.top();
        stk.pop();
        // if current node data is equal
        // to root of s then
        if (temp->data == s->data) {
            if (areTreeIdentical(s, temp))
                return true;
        }
        if (temp->right)
            stk.push(temp->right);
        if (temp->left)
            stk.push(temp->left);
    }
    return false;
}

// Driver Code
int main()
{
    /*
            1
           / \
          2      3
         / \ / \
        4  5 6  7
    */
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    /*
         2
        / \
       4   5
    */

    Node* root2 = newNode(2);
    root2->left = newNode(4);
    root2->right = newNode(5);
    if (isSubTree(root2, root))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if a tree is a subtree of
// another binary tree
import java.util.*;

class GFG{

// Structure of the
// binary tree node
static class Node {
    int data;
    Node left;
    Node right;
};

// Function to create
// new node
static Node newNode(int x)
{
    Node temp = new Node();
    temp.data = x;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to check if two trees
// have same pre-order traversal
static boolean areTreeIdentical(Node t1, Node t2)
{
    Stack<Node> s1 = new Stack<Node>();
    Stack<Node> s2 = new Stack<Node>();
    Node temp1;
    Node temp2;
    s1.add(t1);
    s2.add(t2);

    // Loop to iterate over the stacks
    while (!s1.isEmpty() && !s2.isEmpty()) {
        temp1 = s1.peek();
        temp2 = s2.peek();
        s1.pop();
        s2.pop();

        // Both are None
        // hence they are equal
        if (temp1 == null &&
            temp2 == null)
            continue;

        // nodes are unequal
        if ((temp1 == null && temp2 != null) ||
           (temp1 != null && temp2 == null))
            return false;

        // nodes have unequal data
        if (temp1.data != temp2.data)
            return false;

        s1.add(temp1.right);
        s2.add(temp2.right);

        s1.add(temp1.left);
        s2.add(temp2.left);
    }

    // if both tree are identical
    // both stacks must be empty.
    if (s1.isEmpty() && s2.isEmpty())
        return true;
    else
        return false;
}
// Function to check if the Tree s
// is the subtree of the Tree T
static boolean isSubTree(Node s, Node t)
{
    // first we find the root of s in t
    // by traversing in pre order fashion
    Stack<Node> stk = new Stack<Node>();
    Node temp;
    stk.add(t);
    while (!stk.isEmpty()) {
        temp = stk.peek();
        stk.pop();

        // if current node data is equal
        // to root of s then
        if (temp.data == s.data) {
            if (areTreeIdentical(s, temp))
                return true;
        }
        if (temp.right != null)
            stk.add(temp.right);
        if (temp.left != null)
            stk.add(temp.left);
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    /*
            1
           / \
          2      3
         / \ / \
        4  5 6  7
    */
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    /*
         2
        / \
       4   5
    */

    Node root2 = newNode(2);
    root2.left = newNode(4);
    root2.right = newNode(5);
    if (isSubTree(root2, root))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a tree is a subtree of
# another binary tree

# Structure of the
# binary tree node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to check if two trees
# have same pre-order traversal
def areTreeIdentical(t1 : Node,
                     t2 : Node) -> bool:
    s1 = []
    s2 = []
    s1.append(t1)
    s2.append(t2)

    # Loop to iterate
    # over the stacks
    while s1 and s2:
        temp1 = s1.pop()
        temp2 = s2.pop()

        # Both are None
        # hence they are equal
        if (temp1 is None and
            temp2 is None):
            continue

        # Nodes are unequal
        if ((temp1 is None and
             temp2 is not None) or
            (temp1 is not None and
             temp2 is None)):
            return False

        # Nodes have unequal data
        if (temp1.data != temp2.data):
            return False

        s1.append(temp1.right)
        s2.append(temp2.right)

        s1.append(temp1.left)
        s2.append(temp2.left)

    # If both tree are identical
    # both stacks must be empty.
    if s1 and s2:
        return False
    return True

# Function to check if the Tree s
# is the subtree of the Tree T
def isSubTree(s : Node,
              t : Node) -> Node:

    # First we find the
    # root of s in t
    # by traversing in
    # pre order fashion
    stk = []
    stk.append(t)

    while stk:
        temp = stk.pop()

        # If current node data is equal
        # to root of s then
        if (temp.data == s.data):
            if (areTreeIdentical(s, temp)):
                return True
        if (temp.right):
            stk.append(temp.right)
        if (temp.left):
            stk.append(temp.left)

    return False

# Driver Code
if __name__ == "__main__":

    '''
            1
           / \
          2      3
         / \ / \
        4  5 6  7
    '''
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)

    '''
         2
        / \
       4   5
    '''
    root2 = Node(2)
    root2.left = Node(4)
    root2.right = Node(5)
    if (isSubTree(root2, root)):
        print("Yes")
    else:
        print("No")

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation to check
// if a tree is a subtree of
// another binary tree
using System;
using System.Collections.Generic;

class GFG{

// Structure of the
// binary tree node
class Node {
    public int data;
    public Node left;
    public Node right;
};

// Function to create
// new node
static Node newNode(int x)
{
    Node temp = new Node();
    temp.data = x;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to check if two trees
// have same pre-order traversal
static bool areTreeIdentical(Node t1, Node t2)
{
    Stack<Node> s1 = new Stack<Node>();
    Stack<Node> s2 = new Stack<Node>();
    Node temp1;
    Node temp2;
    s1.Push(t1);
    s2.Push(t2);

    // Loop to iterate over the stacks
    while (s1.Count != 0 && s2.Count != 0) {
        temp1 = s1.Peek();
        temp2 = s2.Peek();
        s1.Pop();
        s2.Pop();

        // Both are None
        // hence they are equal
        if (temp1 == null &&
            temp2 == null)
            continue;

        // nodes are unequal
        if ((temp1 == null && temp2 != null) ||
           (temp1 != null && temp2 == null))
            return false;

        // nodes have unequal data
        if (temp1.data != temp2.data)
            return false;

        s1.Push(temp1.right);
        s2.Push(temp2.right);

        s1.Push(temp1.left);
        s2.Push(temp2.left);
    }

    // if both tree are identical
    // both stacks must be empty.
    if (s1.Count == 0 && s2.Count == 0)
        return true;
    else
        return false;
}

// Function to check if the Tree s
// is the subtree of the Tree T
static bool isSubTree(Node s, Node t)
{
    // first we find the root of s in t
    // by traversing in pre order fashion
    Stack<Node> stk = new Stack<Node>();
    Node temp;
    stk.Push(t);
    while (stk.Count != 0) {
        temp = stk.Peek();
        stk.Pop();

        // if current node data is equal
        // to root of s then
        if (temp.data == s.data) {
            if (areTreeIdentical(s, temp))
                return true;
        }
        if (temp.right != null)
            stk.Push(temp.right);
        if (temp.left != null)
            stk.Push(temp.left);
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    /*
            1
           / \
          2      3
         / \ / \
        4  5 6  7
    */
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    /*
         2
        / \
       4   5
    */

    Node root2 = newNode(2);
    root2.left = newNode(4);
    root2.right = newNode(5);
    if (isSubTree(root2, root))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to check
// if a tree is a subtree of
// another binary tree

// Structure of the
// binary tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to create
// new node
function newNode(x)
{
    var temp = new Node();
    temp.data = x;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to check if two trees
// have same pre-order traversal
function areTreeIdentical(t1, t2)
{
    var s1 = [];
    var s2 = [];
    var temp1 = null;
    var temp2 = null;
    s1.push(t1);
    s2.push(t2);

    // Loop to iterate over the stacks
    while (s1.length != 0 && s2.length != 0)
    {
        temp1 = s1[s1.length - 1];
        temp2 = s2[s2.length - 1];
        s1.pop();
        s2.pop();

        // Both are None
        // hence they are equal
        if (temp1 == null &&
            temp2 == null)
            continue;

        // Nodes are unequal
        if ((temp1 == null && temp2 != null) ||
           (temp1 != null && temp2 == null))
            return false;

        // Nodes have unequal data
        if (temp1.data != temp2.data)
            return false;

        s1.push(temp1.right);
        s2.push(temp2.right);

        s1.push(temp1.left);
        s2.push(temp2.left);
    }

    // If both tree are identical
    // both stacks must be empty.
    if (s1.length == 0 && s2.length == 0)
        return true;
    else
        return false;
}

// Function to check if the Tree s
// is the subtree of the Tree T
function isSubTree(s, t)
{

    // First we find the root of s in t
    // by traversing in pre order fashion
    var stk = [];
    var temp;
    stk.push(t);

    while (stk.length != 0)
    {
        temp = stk[stk.length - 1];
        stk.pop();

        // If current node data is equal
        // to root of s then
        if (temp.data == s.data)
        {
            if (areTreeIdentical(s, temp))
                return true;
        }
        if (temp.right != null)
            stk.push(temp.right);
        if (temp.left != null)
            stk.push(temp.left);
    }
    return false;
}

// Driver Code
/*
        1
       / \
      2   3
     / \ / \
    4  5 6  7
*/
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);
/*
     2
    / \
   4   5
*/

var root2 = newNode(2);
root2.left = newNode(4);
root2.right = newNode(5);

if (isSubTree(root2, root))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
Yes
```