# 用括号表示的字符串构建二叉树|集合 2

> 原文:[https://www . geeksforgeeks . org/construct-a-二叉树-由带括号的字符串表示-set-2/](https://www.geeksforgeeks.org/construct-a-binary-tree-from-string-with-bracket-representation-set-2/)

给定一个由圆括号{ *'('和')'* }和整数组成的字符串 **s** ，任务是从中构建一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，并打印其[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。

**示例:**

> **输入:**S =【1(2)(3)】
> **输出:** 1 2 3
> **解释:**对应的二叉树如下:
> 1
> / \
> 2 3
> 
> **输入:**“4(2(3)(1))(6(5))”
> **输出:** 4 2 3 1 6 5
> **解释:**
> 对应的二叉树如下:
> 
> 4
> / \
> 2 6
> / \ /
> 3 1 5

[**递归**](https://www.geeksforgeeks.org/recursion/) **方法:**参考[前一篇](https://www.geeksforgeeks.org/construct-binary-tree-string-bracket-representation/)递归解决问题。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**方法:**这个问题可以使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)解决。按照以下步骤解决问题:

*   将位置 **0** 处的字符更新为[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/) 的**根**，并初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/) **stk** 。
*   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N-1】**中迭代
    *   如果遇到**(“**)，将**根**推到[栈](https://www.geeksforgeeks.org/stack-data-structure/) **stk** 。
    *   否则，如果遇到 **')'** ，更新**根**为[栈](https://www.geeksforgeeks.org/stack-data-structure/)的最顶层元素，弹出最顶层元素。
    *   否则，如果字符是数字，则分支到空部分(左或右)。
*   在上述步骤结束时，返回二叉树的**根**节点。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Build a tree node having left and
// right pointers set to null initially
struct Node {
    Node* left;
    Node* right;
    int data;

    // Constructor to set the data of
    // the newly created tree node
    Node(int element)
    {
        data = element;
        this->left = nullptr;
        this->right = nullptr;
    }
};

// Utility function to print
// preorder traversal of the tree
void preorder(Node* root)
{
    if (!root)
        return;

    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Function to construct a
// tree using bracket notation
Node* constructTree(string s)
{

    // First character is the root of the tree
    Node* root = new Node(s[0] - '0');

    // Stack used to store the
    // previous root elements
    stack<Node*> stk;

    // Iterate over remaining characters
    for (int i = 1; i < s.length(); i++) {

        // If current character is '('
        if (s[i] == '(') {

            // Push root into stack
            stk.push(root);
        }

        // If current character is ')'
        else if (s[i] == ')') {

            // Make root the top most
            // element in the stack
            root = stk.top();

            // Remove the top node
            stk.pop();
        }

        // If current character is a number
        else {

            // If left is null, then put the new
            // node to the left and move to the
            // left of the root
            if (root->left == nullptr) {

                Node* left = new Node(s[i] - '0');
                root->left = left;
                root = root->left;
            }

            // Otherwise, if right is null, then
            // put the new node to the right and
            // move to the right of the root
            else if (root->right == nullptr) {

                Node* right = new Node(s[i] - '0');
                root->right = right;
                root = root->right;
            }
        }
    }

    // Return the root
    return root;
}

// Driver code
int main()
{
    // Input
    string s = "4(2(3)(1))(6(5))";

    // Function calls
    Node* root = constructTree(s);
    preorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Class containing left and
    // right child of current
    // node and key value
    static class Node {

        public int data;
        public Node left, right;

        public Node(int element)
        {
            data = element;
            left = right = null;
        }
    }

    // Utility function to print
    // preorder traversal of the tree
    static void preorder(Node root)
    {
        if (root == null)
            return;

        System.out.print(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }

    // Function to construct a
    // tree using bracket notation
    static Node constructTree(String s)
    {

        // First character is the root of the tree
        Node root = new Node(s.charAt(0) - '0');

        // Stack used to store the
        // previous root elements
        Stack<Node> stk = new Stack<Node>();

        // Iterate over remaining characters
        for (int i = 1; i < s.length(); i++) {

            // If current character is '('
            if (s.charAt(i) == '(') {

                // Push root into stack
                stk.push(root);
            }

            // If current character is ')'
            else if (s.charAt(i) == ')') {

                // Make root the top most
                // element in the stack
                root = stk.peek();

                // Remove the top node
                stk.pop();
            }

            // If current character is a number
            else {

                // If left is null, then put the new
                // node to the left and move to the
                // left of the root
                if (root.left == null) {

                    Node left = new Node(s.charAt(i) - '0');
                    root.left = left;
                    root = root.left;
                }

                // Otherwise, if right is null, then
                // put the new node to the right and
                // move to the right of the root
                else if (root.right == null) {

                    Node right = new Node(s.charAt(i) - '0');
                    root.right = right;
                    root = root.right;
                }
            }
        }

        // Return the root
        return root;
    }

    public static void main(String[] args) {
        // Input
        String s = "4(2(3)(1))(6(5))";

        // Function calls
        Node root = constructTree(s);
        preorder(root);
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python program for the above approach

# Build a tree node having left and
# right pointers set to null initially
class Node:
    # Constructor to set the data of
    # the newly created tree node
    def __init__(self, element):
        self.data = element
        self.left = None
        self.right = None

# Utility function to print
# preorder traversal of the tree
def preorder(root):
    if (not root):
        return

    print(root.data, end = " ")
    preorder(root.left)
    preorder(root.right)

# Function to construct a
# tree using bracket notation
def constructTree(s):

    # First character is the root of the tree
    root = Node(ord(s[0]) - ord('0'))

    # Stack used to store the
    # previous root elements
    stk = []

    # Iterate over remaining characters
    for i in range(1,len(s)):
        # If current character is '('
        if (s[i] == '('):

            # Push root into stack
            stk.append(root)

        # If current character is ')'
        elif (s[i] == ')'):

            # Make root the top most
            # element in the stack
            root = stk[-1]

            # Remove the top node
            del stk[-1]
        # If current character is a number
        else:

            # If left is null, then put the new
            # node to the left and move to the
            # left of the root
            if (root.left == None):

                left = Node(ord(s[i]) - ord('0'))
                root.left = left
                root = root.left

            # Otherwise, if right is null, then
            # put the new node to the right and
            # move to the right of the root
            elif (root.right == None):

                right =  Node(ord(s[i]) - ord('0'))
                root.right = right
                root = root.right

    # Return the root
    return root

# Driver code
if __name__ == '__main__':
    # Input
    s = "4(2(3)(1))(6(5))"

    # Function calls
    root = constructTree(s)
    preorder(root)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG
{

    // Class containing left and
    // right child of current
    // node and key value
    class Node {

        public int data;
        public Node left, right;

        public Node(int element)
        {
            data = element;
            left = right = null;
        }
    }

    // Utility function to print
    // preorder traversal of the tree
    static void preorder(Node root)
    {
        if (root == null)
            return;

        Console.Write(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }

    // Function to construct a
    // tree using bracket notation
    static Node constructTree(string s)
    {

        // First character is the root of the tree
        Node root = new Node(s[0] - '0');

        // Stack used to store the
        // previous root elements
        Stack stk = new Stack();

        // Iterate over remaining characters
        for (int i = 1; i < s.Length; i++) {

            // If current character is '('
            if (s[i] == '(') {

                // Push root into stack
                stk.Push(root);
            }

            // If current character is ')'
            else if (s[i] == ')') {

                // Make root the top most
                // element in the stack
                root = (Node)(stk.Peek());

                // Remove the top node
                stk.Pop();
            }

            // If current character is a number
            else {

                // If left is null, then put the new
                // node to the left and move to the
                // left of the root
                if (root.left == null) {

                    Node left = new Node(s[i] - '0');
                    root.left = left;
                    root = root.left;
                }

                // Otherwise, if right is null, then
                // put the new node to the right and
                // move to the right of the root
                else if (root.right == null) {

                    Node right = new Node(s[i] - '0');
                    root.right = right;
                    root = root.right;
                }
            }
        }

        // Return the root
        return root;
    }

  // Driver code
  static void Main()
  {

    // Input
    string s = "4(2(3)(1))(6(5))";

    // Function calls
    Node root = constructTree(s);
    preorder(root);
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach  
    class Node
    {
        constructor(element) {
           this.left = null;
           this.right = null;
           this.data = element;
        }
    }

    // Utility function to print
    // preorder traversal of the tree
    function preorder(root)
    {
        if (root == null)
            return;

        document.write(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }

    // Function to construct a
    // tree using bracket notation
    function constructTree(s)
    {

        // First character is the root of the tree
        let root = new Node(s[0].charCodeAt() - '0'.charCodeAt());

        // Stack used to store the
        // previous root elements
        let stk = [];

        // Iterate over remaining characters
        for (let i = 1; i < s.length; i++) {

            // If current character is '('
            if (s[i] == '(') {

                // Push root into stack
                stk.push(root);
            }

            // If current character is ')'
            else if (s[i] == ')') {

                // Make root the top most
                // element in the stack
                root = stk[stk.length - 1];

                // Remove the top node
                stk.pop();
            }

            // If current character is a number
            else {

                // If left is null, then put the new
                // node to the left and move to the
                // left of the root
                if (root.left == null) {

                    let left = new Node(s[i].charCodeAt() - '0'.charCodeAt());
                    root.left = left;
                    root = root.left;
                }

                // Otherwise, if right is null, then
                // put the new node to the right and
                // move to the right of the root
                else if (root.right == null) {

                    let right = new Node(s[i].charCodeAt() - '0'.charCodeAt());
                    root.right = right;
                    root = root.right;
                }
            }
        }

        // Return the root
        return root;
    }

    // Input
    let s = "4(2(3)(1))(6(5))";

    // Function calls
    let root = constructTree(s);
    preorder(root);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
4 2 3 1 6 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)