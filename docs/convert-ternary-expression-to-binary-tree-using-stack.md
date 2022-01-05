# 使用栈

将三元表达式转换为二叉树

> 原文:[https://www . geesforgeks . org/convert-三元-表达式-二叉树-使用-堆栈/](https://www.geeksforgeeks.org/convert-ternary-expression-to-binary-tree-using-stack/)

给定一个字符串**字符串**，它包含一个可以嵌套的三元表达式。任务是将给定的三元表达式转换成二叉树并返回根。
**例:**

```
Input: str = "a?b:c"
Output: a b c
  a
 / \
b   c
The preorder traversal of the above tree is a b c.

Input: str = "a?b?c:d:e"
Output: a b c d e
    a
   / \
  b   e
 / \
c   d
```

**方法:**这是针对给定问题的基于堆栈的方法。由于三元运算符具有从右到左的关联性，因此可以从右到左遍历字符串。把字母一个接一个地跳过字母？和“:”因为这些字母用于决定当前字母(alphabet [a 到 z])是进入堆栈，还是用于从堆栈顶部弹出前 2 个元素，使它们成为当前字母的子元素，然后将当前字母本身推入堆栈。这以自下而上的方式形成树，并且在处理完整个字符串之后，堆栈中的最后一个剩余元素是树的根。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node structure
struct Node {
    char data;
    Node *left, *right;
};

// Function to create a new node
Node* createNewNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = NULL, node->right = NULL;
    return node;
}

// Function to print the preorder
// traversal of the tree
void preorder(Node* root)
{
    if (root == NULL)
        return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Function to convert the expression to a binary tree
Node* convertExpression(string str)
{
    stack<Node*> s;

    // If the letter is the last letter of
    // the string or is of the type :letter: or ?letter:
    // we push the node pointer containing
    // the letter to the stack
    for (int i = str.length() - 1; i >= 0;) {
        if ((i == str.length() - 1)
            || (i != 0 && ((str[i - 1] == ':'
                            && str[i + 1] == ':')
                           || (str[i - 1] == '?'
                               && str[i + 1] == ':')))) {
            s.push(createNewNode(str[i]));
        }

        // If we do not push the current letter node to stack,
        // it means the top 2 nodes in the stack currently are the
        // left and the right children of the current node
        // So pop these elements and assign them as the
        // children of the current letter node and then
        // push this node into the stack
        else {
            Node* lnode = s.top();
            s.pop();
            Node* rnode = s.top();
            s.pop();
            Node* node = createNewNode(str[i]);
            node->left = lnode;
            node->right = rnode;
            s.push(node);
        }
        i -= 2;
    }

    // Finally, there will be only 1 element
    // in the stack which will be the
    // root of the binary tree
    return s.top();
}

// Driver code
int main()
{
    string str = "a?b?c:d:e";

    // Convert expression
    Node* root = convertExpression(str);

    // Print the preorder traversal
    preorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class Main
{
    // Class containing left and
    // right child of current
    // node and key value
    static class Node {

        public char data;
        public Node left, right;

        public Node(char data)
        {
            this.data = data;
            left = right = null;
        }
    }

    // Function to create a new node
    static Node createNewNode(char data)
    {
        Node node = new Node(data);
        return node;
    }

    // Function to print the preorder
    // traversal of the tree
    static void preorder(Node root)
    {
        if (root == null)
            return;
        System.out.print(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }

    // Function to convert the expression to a binary tree
    static Node convertExpression(String str)
    {
        Stack<Node> s = new Stack<Node>();

        // If the letter is the last letter of
        // the string or is of the type :letter: or ?letter:
        // we push the node pointer containing
        // the letter to the stack
        for (int i = str.length() - 1; i >= 0😉 {
            if ((i == str.length() - 1)
                || (i != 0 && ((str.charAt(i - 1) == ':'
                                && str.charAt(i + 1) == ':')
                               || (str.charAt(i - 1) == '?'
                                   && str.charAt(i + 1) == ':')))) {
                s.push(createNewNode(str.charAt(i)));
            }

            // If we do not push the current
            // letter node to stack,
            // it means the top 2 nodes in
            // the stack currently are the
            // left and the right children of the current node
            // So pop these elements and assign them as the
            // children of the current letter node and then
            // push this node into the stack
            else {
                Node lnode = (Node)s.peek();
                s.pop();
                Node rnode = (Node)s.peek();
                s.pop();
                Node node = createNewNode(str.charAt(i));
                node.left = lnode;
                node.right = rnode;
                s.push(node);
            }
            i -= 2;
        }

        // Finally, there will be only 1 element
        // in the stack which will be the
        // root of the binary tree
        return (Node)s.peek();
    }

  // Driver code
    public static void main(String[] args)
    {
        String str = "a?b?c:d:e";

        // Convert expression
        Node root = convertExpression(str);

        // Print the preorder traversal
        preorder(root);
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Tree Structure
class Node:

    # Constructor to set the data of
    # the newly created tree node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to create a new node
def createNewNode(data):
    node = Node(data)
    return node

# Function to print the preorder
# traversal of the tree
def preorder(root):
    if (root == None):
        return
    print(root.data, end = " ")
    preorder(root.left)
    preorder(root.right)

# Function to convert the expression to a binary tree
def convertExpression(Str):
    s = []

    # If the letter is the last letter of
    # the string or is of the type :letter: or ?letter:
    # we push the node pointer containing
    # the letter to the stack
    i = len(Str) - 1
    while i >= 0:
        if ((i == len(Str) - 1) or (i != 0 and ((Str[i - 1] == ':' and Str[i + 1] == ':')
                           or (Str[i - 1] == '?' and Str[i + 1] == ':')))):
            s.append(createNewNode(Str[i]))

        # If we do not push the current
        # letter node to stack,
        # it means the top 2 nodes in
        # the stack currently are the
        # left and the right children of the current node
        # So pop these elements and assign them as the
        # children of the current letter node and then
        # push this node into the stack
        else:
            lnode = s[-1]
            s.pop()
            rnode = s[-1]
            s.pop()
            node = createNewNode(Str[i])
            node.left = lnode
            node.right = rnode
            s.append(node)
        i -= 2

    # Finally, there will be only 1 element
    # in the stack which will be the
    # root of the binary tree
    return s[-1]

Str = "a?b?c:d:e"

# Convert expression
root = convertExpression(Str)

# Print the preorder traversal
preorder(root)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
class GFG {

    // Class containing left and
    // right child of current
    // node and key value
    class Node {

        public char data;
        public Node left, right;

        public Node(char data)
        {
            this.data = data;
            left = right = null;
        }
    }

    // Function to create a new node
    static Node createNewNode(char data)
    {
        Node node = new Node(data);
        return node;
    }

    // Function to print the preorder
    // traversal of the tree
    static void preorder(Node root)
    {
        if (root == null)
            return;
        Console.Write(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }

    // Function to convert the expression to a binary tree
    static Node convertExpression(string str)
    {
        Stack s = new Stack();

        // If the letter is the last letter of
        // the string or is of the type :letter: or ?letter:
        // we push the node pointer containing
        // the letter to the stack
        for (int i = str.Length - 1; i >= 0;) {
            if ((i == str.Length - 1)
                || (i != 0 && ((str[i - 1] == ':'
                                && str[i + 1] == ':')
                               || (str[i - 1] == '?'
                                   && str[i + 1] == ':')))) {
                s.Push(createNewNode(str[i]));
            }

            // If we do not push the current
            // letter node to stack,
            // it means the top 2 nodes in
            // the stack currently are the
            // left and the right children of the current node
            // So pop these elements and assign them as the
            // children of the current letter node and then
            // push this node into the stack
            else {
                Node lnode = (Node)s.Peek();
                s.Pop();
                Node rnode = (Node)s.Peek();
                s.Pop();
                Node node = createNewNode(str[i]);
                node.left = lnode;
                node.right = rnode;
                s.Push(node);
            }
            i -= 2;
        }

        // Finally, there will be only 1 element
        // in the stack which will be the
        // root of the binary tree
        return (Node)s.Peek();
    }

  static void Main() {
    string str = "a?b?c:d:e";

    // Convert expression
    Node root = convertExpression(str);

    // Print the preorder traversal
    preorder(root);
  }
}

// This code is contributed by decode2207.
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

    // Function to create a new node
    function createNewNode(data)
    {
        let node = new Node(data);
        return node;
    }

    // Function to print the preorder
    // traversal of the tree
    function preorder(root)
    {
        if (root == null)
            return;
        document.write(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }

    // Function to convert the expression to a binary tree
    function convertExpression(str)
    {
        let s = [];

        // If the letter is the last letter of
        // the string or is of the type :letter: or ?letter:
        // we push the node pointer containing
        // the letter to the stack
        for (let i = str.length - 1; i >= 0;) {
            if ((i == str.length - 1)
                || (i != 0 && ((str[i - 1] == ':'
                                && str[i + 1] == ':')
                               || (str[i - 1] == '?'
                                   && str[i + 1] == ':')))) {
                s.push(createNewNode(str[i]));
            }

            // If we do not push the current
            // letter node to stack,
            // it means the top 2 nodes in
            // the stack currently are the
            // left and the right children of the current node
            // So pop these elements and assign them as the
            // children of the current letter node and then
            // push this node into the stack
            else {
                let lnode = s[s.length - 1];
                s.pop();
                let rnode = s[s.length - 1];
                s.pop();
                let node = createNewNode(str[i]);
                node.left = lnode;
                node.right = rnode;
                s.push(node);
            }
            i -= 2;
        }

        // Finally, there will be only 1 element
        // in the stack which will be the
        // root of the binary tree
        return s[s.length - 1];
    }

    let str = "a?b?c:d:e";

    // Convert expression
    let root = convertExpression(str);

    // Print the preorder traversal
    preorder(root);

</script>
```

**Output:** 

```
a b c d e
```

**时间复杂度:** O(n)