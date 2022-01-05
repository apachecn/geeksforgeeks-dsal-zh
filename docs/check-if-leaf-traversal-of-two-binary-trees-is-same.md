# 检查两个二叉树的叶子遍历是否相同？

> 原文:[https://www . geesforgeks . org/check-if-leaf-遍历两个二叉树-是否相同/](https://www.geeksforgeeks.org/check-if-leaf-traversal-of-two-binary-trees-is-same/)

叶子遍历是叶子从左向右遍历的序列。问题是检查两个给定二叉树的叶遍历是否相同。
预期时间复杂度 O(n)。期望辅助空间 O(h1 + h2)，其中 h1 和 h2 是两个二叉树的高度。

**示例:**

```
Input: Roots of below Binary Trees
         1            
        / \
       2   3      
      /   / \          
     4   6   7

          0
        /   \
       5     8      
        \   / \        
        4   6  7
Output: same
Leaf order traversal of both trees is 4 6 7     

Input: Roots of below Binary Trees
         0            
        / \
       1   2       
      / \       
     8   9   

         1
        / \
       4   3     
        \ / \        
        8 2  9

Output: Not Same
Leaf traversals of two trees are different.
For first, it is 8 9 2 and for second it is
8 2 9
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
一个**简单的解决方案**是遍历第一棵树，将叶子从左到右存储在一个数组中。然后遍历其他树，将叶子存储在另一个数组中。最后比较两个数组。如果两个数组相同，则返回 true。
上述解决方案需要 O(m+n)个额外空间，其中 m 和 n 分别是第一棵树和第二棵树中的节点。
**如何用 O(h1 + h2)空间检查？**
思路是使用迭代遍历。同时遍历两棵树，在两棵树中寻找一个叶子节点，并比较找到的叶子。所有的叶子必须相配。

**算法:**

```
1. Create empty stacks stack1 and stack2 
   for iterative traversals of tree1 and tree2

2. insert (root of tree1) in stack1
   insert (root of tree2) in stack2

3. Stores current leaf nodes of tree1 and tree2
temp1 = (root of tree1) 
temp2 = (root of tree2)  

4. Traverse both trees using stacks
while (stack1 and stack2 parent empty) 
{
    // Means excess leaves in one tree
    if (if one of the stacks are empty)   
    return false

   // get next leaf node in tree1 
   temp1 = stack1.pop()
   while (temp1 is not leaf node) 
   {
        push right child to stack1     
    push left child to stack1
   }

   // get next leaf node in tree2     
   temp2 = stack2.pop()
   while (temp2 is not leaf node) 
   {
        push right child to stack2      
    push left child to stack2
   }

   // If leaves do not match return false
   if (temp1 != temp2)                  
       return false
}

5. If all leaves matched, return true
```

下面是上面算法的 Java 实现。

## C++

```
// C++ code to check if leaf traversals
// of two Binary Trees are same or not.
#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
};

// Returns new Node with data as
// input to below function.
Node* newNode(int d)
{
    Node* temp = new Node;
    temp->data = d;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// checks if a given node is leaf or not.
bool isLeaf(Node* root)
{
    if (root == NULL)
        return false;
    if (!root->left && !root->right)
        return true;
    return false;
}

// iterative function.
// returns true if leaf traversals
// are same, else false.
bool isSame(Node* root1, Node* root2)
{
    stack<Node*> s1;
    stack<Node*> s2;

    // push root1 to empty stack s1.
    s1.push(root1);

    // push root2 to empty stack s2.
    s2.push(root2);

    // loop until either of stacks are non-empty.
    while (!s1.empty() || !s2.empty())
    {
        // this means one of the stacks has
        // extra leaves, hence return false.
        if (s1.empty() || s2.empty())
            return false;

        Node* temp1 = s1.top();
        s1.pop();
        while (temp1 != NULL && !isLeaf(temp1))
        {
            // Push right child if exists
            if (temp1->right)
                s1.push(temp1->right);

            // Push left child if exists
            if (temp1->left)
                s1.push(temp1->left);

            // Note that right child(if exists)
            // is pushed before left child(if exists).
            temp1 = s1.top();
            s1.pop();
        }

        Node* temp2 = s2.top();
        s2.pop();
        while (temp2 != NULL && !isLeaf(temp2))
        {
            // Push right child if exists
            if (temp2->right)
                s2.push(temp2->right);

            // Push left child if exists
            if (temp2->left)
                s2.push(temp2->left);
            temp2 = s2.top();
            s2.pop();
        }

        if (!temp1 && temp2)
            return false;
        if (temp1 && !temp2)
            return false;
        if (temp1 && temp2) {
            return temp1->data == temp2->data;
        }
    }

    // all leaves are matched
    return true;
}

// Driver Code
int main()
{
    Node* root1 = newNode(1);
    root1->left = newNode(2);
    root1->right = newNode(3);
    root1->left->left = newNode(4);
    root1->right->left = newNode(6);
    root1->right->right = newNode(7);

    Node* root2 = newNode(0);
    root2->left = newNode(1);
    root2->right = newNode(5);
    root2->left->right = newNode(4);
    root2->right->left = newNode(6);
    root2->right->right = newNode(7);

    if (isSame(root1, root2))
        cout << "Same";
    else
        cout << "Not Same";
    return 0;
}

// This code is contributed
// by AASTHA VARMA
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two Leaf Traversal of
// Two Binary Trees is same or not
import java.util.*;
import java.lang.*;
import java.io.*;

// Binary Tree node
class Node
{
    int data;
    Node left, right;
    public Node(int x)
    {
        data = x;
        left = right = null;
    }
    public boolean isLeaf()
    {
        return (left == null && right == null);
    }
}

class LeafOrderTraversal
{
    // Returns true of leaf traversal of two trees is
    // same, else false
    public static boolean isSame(Node root1, Node root2)
    {
        // Create empty stacks.  These stacks are going
        // to be used for iterative traversals.
        Stack<Node> s1 = new Stack<Node>();
        Stack<Node> s2 = new Stack<Node>();

        s1.push(root1);
        s2.push(root2);

        // Loop until either of two stacks is not empty
        while (!s1.empty() || !s2.empty())
        {
            // If one of the stacks is empty means other
            // stack has extra leaves so return false
            if (s1.empty() || s2.empty())
                return false;

            Node temp1 = s1.pop();
            while (temp1 != null && !temp1.isLeaf())
            {
                // Push right and left children of temp1.
                // Note that right child is inserted
                // before left
                if (temp1.right != null)
                    s1.push(temp1.right);
                if (temp1.left != null)
                    s1.push(temp1.left);
                temp1 = s1.pop();
            }

            // same for tree2
            Node temp2 = s2.pop();
            while (temp2 != null && !temp2.isLeaf())
            {
                if (temp2.right != null)
                    s2.push(temp2.right);
                if (temp2.left != null)
                    s2.push(temp2.left);
                temp2 = s2.pop();
            }

            // If one is null and other is not, then
            // return false
            if (temp1 == null && temp2 != null)
                return false;
            if (temp1 != null && temp2 == null)
                return false;

            // If both are not null and data is not
            // same return false
            if (temp1 != null && temp2 != null)
            {
                if (temp1.data != temp2.data)
                    return false;
            }
        }

        // If control reaches this point, all leaves
        // are matched
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Let us create trees in above example 1
        Node root1 = new Node(1);
        root1.left = new Node(2);
        root1.right = new Node(3);
        root1.left.left = new Node(4);
        root1.right.left = new Node(6);
        root1.right.right = new Node(7);

        Node root2 = new Node(0);
        root2.left = new Node(1);
        root2.right = new Node(5);
        root2.left.right = new Node(4);
        root2.right.left = new Node(6);
        root2.right.right = new Node(7);

        if (isSame(root1, root2))
            System.out.println("Same");
        else
            System.out.println("Not Same");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if two Leaf
# Traversal of Two Binary Trees is same or not

# Binary Tree node

class Node:
    def __init__(self, x):
        self.data = x
        self.left = self.right = None

    def isLeaf(self):
        return (self.left == None and
                self.right == None)

# Returns true of leaf traversal of
# two trees is same, else false

def isSame(root1, root2):

    # Create empty stacks. These stacks are going
    # to be used for iterative traversals.
    s1 = []
    s2 = []

    s1.append(root1)
    s2.append(root2)

    # Loop until either of two stacks
    # is not empty
    while (len(s1) != 0 or len(s2) != 0):

        # If one of the stacks is empty means other
        # stack has extra leaves so return false
        if (len(s1) == 0 or len(s2) == 0):
            return False

        temp1 = s1.pop(-1)
        while (temp1 != None and not temp1.isLeaf()):

            # append right and left children of temp1.
            # Note that right child is inserted
            # before left
            if (temp1.right != None):
                s1.append(temp1\. right)
            if (temp1.left != None):
                s1.append(temp1.left)
                temp1 = s1.pop(-1)

        # same for tree2
        temp2 = s2.pop(-1)
        while (temp2 != None and not temp2.isLeaf()):
            if (temp2.right != None):
                s2.append(temp2.right)
            if (temp2.left != None):
                s2.append(temp2.left)
            temp2 = s2.pop(-1)

        # If one is None and other is not,
        # then return false
        if (temp1 == None and temp2 != None):
            return False
        if (temp1 != None and temp2 == None):
            return False

        # If both are not None and data is
        # not same return false
        if (temp1 != None and temp2 != None):
            if (temp1.data != temp2.data):
                return False

    # If control reaches this point,
    # all leaves are matched
    return True

# Driver Code
if __name__ == '__main__':

    # Let us create trees in above example 1
    root1 = Node(1)
    root1.left = Node(2)
    root1.right = Node(3)
    root1.left.left = Node(4)
    root1.right.left = Node(6)
    root1.right.right = Node(7)

    root2 = Node(0)
    root2.left = Node(1)
    root2.right = Node(5)
    root2.left.right = Node(4)
    root2.right.left = Node(6)
    root2.right.right = Node(7)

    if (isSame(root1, root2)):
        print("Same")
    else:
        print("Not Same")

# This code is contributed by pranchalK
```

## C#

```
// C# program to check if two Leaf Traversal
// of Two Binary Trees is same or not
using System;
using System.Collections.Generic;

// Binary Tree node
public class Node {
    public int data;
    public Node left, right;
    public Node(int x)
    {
        data = x;
        left = right = null;
    }
    public virtual bool Leaf
    {
        get {
          return (left == null && right == null);
        }
    }
}

class GFG {
    // Returns true of leaf traversal of
    // two trees is same, else false
    public static bool isSame(Node root1, Node root2)
    {
        // Create empty stacks. These stacks
        // are going to be used for iterative
        // traversals.
        Stack<Node> s1 = new Stack<Node>();
        Stack<Node> s2 = new Stack<Node>();

        s1.Push(root1);
        s2.Push(root2);

        // Loop until either of two stacks
        // is not empty
        while (s1.Count > 0 || s2.Count > 0)
        {
            // If one of the stacks is empty means other
            // stack has extra leaves so return false
            if (s1.Count == 0 || s2.Count == 0)
            {
                return false;
            }

            Node temp1 = s1.Pop();
            while (temp1 != null && !temp1.Leaf)
            {
                // Push right and left children of temp1.
                // Note that right child is inserted
                // before left
                if (temp1.right != null)
                {
                    s1.Push(temp1.right);
                }
                if (temp1.left != null)
                {
                    s1.Push(temp1.left);
                }
                temp1 = s1.Pop();
            }

            // same for tree2
            Node temp2 = s2.Pop();
            while (temp2 != null && !temp2.Leaf)
            {
                if (temp2.right != null)
                {
                    s2.Push(temp2.right);
                }
                if (temp2.left != null)
                {
                    s2.Push(temp2.left);
                }
                temp2 = s2.Pop();
            }

            // If one is null and other is not,
            // then return false
            if (temp1 == null && temp2 != null)
            {
                return false;
            }
            if (temp1 != null && temp2 == null)
            {
                return false;
            }

            // If both are not null and data
            // is not same return false
            if (temp1 != null && temp2 != null)
            {
                if (temp1.data != temp2.data)
                {
                    return false;
                }
            }
        }

        // If control reaches this point,
        // all leaves are matched
        return true;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // Let us create trees in above example 1
        Node root1 = new Node(1);
        root1.left = new Node(2);
        root1.right = new Node(3);
        root1.left.left = new Node(4);
        root1.right.left = new Node(6);
        root1.right.right = new Node(7);

        Node root2 = new Node(0);
        root2.left = new Node(1);
        root2.right = new Node(5);
        root2.left.right = new Node(4);
        root2.right.left = new Node(6);
        root2.right.right = new Node(7);

        if (isSame(root1, root2)) {
            Console.WriteLine("Same");
        }
        else {
            Console.WriteLine("Not Same");
        }
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript program to check if two Leaf Traversal of
    // Two Binary Trees is same or not

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Returns true of leaf traversal of two trees is
    // same, else false
    function isSame(root1, root2)
    {
        // Create empty stacks.  These stacks are going
        // to be used for iterative traversals.
        let s1 = [];
        let s2 = [];

        s1.push(root1);
        s2.push(root2);

        // Loop until either of two stacks is not empty
        while (s1.length > 0 || s2.length > 0)
        {
            // If one of the stacks is empty means other
            // stack has extra leaves so return false
            if (s1.length == 0 || s1.length == 0)
                return false;

            let temp1 = s1.pop();
            while (temp1 != null && !(temp1.left == null &&
            temp1.right == null))
            {
                // Push right and left children of temp1.
                // Note that right child is inserted
                // before left
                if (temp1.right != null)
                    s1.push(temp1.right);
                if (temp1.left != null)
                    s1.push(temp1.left);
                temp1 = s1.pop();
            }

            // same for tree2
            let temp2 = s2.pop();
            while (temp2 != null && !(temp2.left == null &&
            temp2.right == null))
            {
                if (temp2.right != null)
                    s2.push(temp2.right);
                if (temp2.left != null)
                    s2.push(temp2.left);
                temp2 = s2.pop();
            }

            // If one is null and other is not, then
            // return false
            if (temp1 == null && temp2 != null)
                return false;
            if (temp1 != null && temp2 == null)
                return false;

            // If both are not null and data is not
            // same return false
            if (temp1 != null && temp2 != null)
            {
                if (temp1.data != temp2.data)
                    return false;
            }
        }

        // If control reaches this point, all leaves
        // are matched
        return true;
    }

    // Let us create trees in above example 1
    let root1 = new Node(1);
    root1.left = new Node(2);
    root1.right = new Node(3);
    root1.left.left = new Node(4);
    root1.right.left = new Node(6);
    root1.right.right = new Node(7);

    let root2 = new Node(0);
    root2.left = new Node(1);
    root2.right = new Node(5);
    root2.left.right = new Node(4);
    root2.right.left = new Node(6);
    root2.right.right = new Node(7);

    if (isSame(root1, root2))
      document.write("Same");
    else
      document.write("Not Same");

</script>
```

**Output**

```
Same
```

本文由**库马尔·高拉夫**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息