# 将三元表达式转换为二叉树

> 原文:[https://www . geesforgeks . org/convert-三元-表达式-二叉树/](https://www.geeksforgeeks.org/convert-ternary-expression-binary-tree/)

给定包含三元表达式的字符串。表达式可以是嵌套的，任务是将给定的三元表达式转换为二叉树。

**示例:**

```
Input :  string expression =   a?b:c 
Output :        a
              /  \
             b    c

Input : expression =  a?b?c:d:e
Output :     a
           /  \
          b    e
        /  \
       c    d
```

问于:**脸书访谈**

想法是我们遍历一个字符串，使第一个字符作为根，并递归执行以下步骤。
1。如果我们看到符号'？'
……..然后我们添加下一个字符作为 root 的左子字符。
2。如果我们看到符号:“
……”..然后我们将其添加为当前根的右子。
这样做，直到我们遍历“字符串”的所有元素。

以下是上述想法的实现

## C++

```
// C++ program to convert a ternary expression to
// a tree.
#include<bits/stdc++.h>
using namespace std;

// tree structure
struct Node
{
    char data;
    Node *left, *right;
};

// function create a new node
Node *newNode(char Data)
{
    Node *new_node = new Node;
    new_node->data = Data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

// Function to convert Ternary Expression to a Binary
// Tree. It return the root of tree
//Notice that we pass index i by reference because we want to skip the characters in the subtree
Node *convertExpression(string str, int & i)
{
    // store current character of expression_string
    // [ 'a' to 'z']
    Node * root =newNode(str[i]);

    //If it was last character return
    //Base Case
    if(i==str.length()-1) return root;

    // Move ahead in str
    i++;
    //If the next character is '?'.Then there will be subtree for the current node
    if(str[i]=='?')
    {
        //skip the '?'
        i++;

        //construct the left subtree
        //Notice after the below recursive call i will point to ':' just before the right child of current node since we pass i by reference
        root->left = convertExpression(str,i);

        //skip the ':' character
        i++;

        //construct the right subtree
        root->right = convertExpression(str,i);
        return root;
    }
    //If the next character is not '?' no subtree just return it
    else return root;
}

// function print tree
void printTree( Node *root)
{
    if (!root)
        return ;
    cout << root->data <<" ";
    printTree(root->left);
    printTree(root->right);
}

// Driver program to test above function
int main()
{
    string expression = "a?b?c:d:e";
    int i=0;
    Node *root = convertExpression(expression, i);
    printTree(root) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert a ternary
// expreesion to a tree.
import java.util.Queue;
import java.util.LinkedList;

// Class to represent Tree node
class Node
{
    char data;
    Node left, right;

    public Node(char item)
    {
        data = item;
        left = null;
        right = null;
    }
}

// Class to convert a ternary expression to a Tree
class BinaryTree
{
    // Function to convert Ternary Expression to a Binary
    // Tree. It return the root of tree
    Node convertExpression(char[] expression, int i)
    {
        // Base case
        if (i >= expression.length)
            return null;

        // store current character of expression_string
        // [ 'a' to 'z']
        Node root = new Node(expression[i]);

        // Move ahead in str
        ++i;

        // if current character of ternary expression is '?'
        // then we add next character as a left child of
        // current node
        if (i < expression.length && expression[i]=='?')
            root.left = convertExpression(expression, i+1);

        // else we have to add it as a right child of
        // current node expression.at(0) == ':'
        else if (i < expression.length)
            root.right = convertExpression(expression, i+1);

        return root;
    }

    // function print tree
    public void printTree( Node root)
    {
        if (root == null)
            return;

        System.out.print(root.data +" ");
        printTree(root.left);
        printTree(root.right);
    }

// Driver program to test above function
    public static void main(String args[])
    {
        String exp = "a?b?c:d:e";
        BinaryTree tree = new BinaryTree();
        char[] expression=exp.toCharArray();
        Node root = tree.convertExpression(expression, 0);
        tree.printTree(root) ;
    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Class to define a node
# structure of the tree
class Node:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to convert ternary
# expression to a Binary tree
# It returns the root node
# of the tree
def convert_expression(expression, i):
    if i >= len(expression):
        return None

    # Create a new node object
    # for the expression at
    # ith index
    root = Node(expression[i])

    i += 1

    # if current character of
    # ternary expression is '?'
    # then we add next character
    # as a left child of
    # current node
    if (i < len(expression) and
                expression[i] is "?"):
        root.left = convert_expression(expression, i + 1)

    # else we have to add it
    # as a right child of
    # current node expression[0] == ':'
    elif i < len(expression):
        root.right = convert_expression(expression, i + 1)
    return root

# Function to print the tree
# in a pre-order traversal pattern
def print_tree(root):
    if not root:
        return
    print(root.data, end=' ')
    print_tree(root.left)
    print_tree(root.right)

# Driver Code
if __name__ == "__main__":
    string_expression = "a?b?c:d:e"
    root_node = convert_expression(string_expression, 0)
    print_tree(root_node)

# This code is contributed
# by Kanav Malhotra
```

## C#

```
// C# program to convert a ternary
// expreesion to a tree.
using System;

// Class to represent Tree node
public class Node
{
    public char data;
    public Node left, right;

    public Node(char item)
    {
        data = item;
        left = null;
        right = null;
    }
}

// Class to convert a ternary
// expression to a Tree
public class BinaryTree
{
    // Function to convert Ternary Expression
    // to a Binary Tree. It return the root of tree
    public virtual Node convertExpression(char[] expression,
                                          int i)
    {
        // Base case
        if (i >= expression.Length)
        {
            return null;
        }

        // store current character of
        // expression_string [ 'a' to 'z']
        Node root = new Node(expression[i]);

        // Move ahead in str
        ++i;

        // if current character of ternary expression
        // is '?' then we add next character as a
        // left child of current node
        if (i < expression.Length && expression[i] == '?')
        {
            root.left = convertExpression(expression, i + 1);
        }

        // else we have to add it as a right child
        // of current node expression.at(0) == ':'
        else if (i < expression.Length)
        {
            root.right = convertExpression(expression, i + 1);
        }

        return root;
    }

    // function print tree
    public virtual void printTree(Node root)
    {
        if (root == null)
        {
            return;
        }

        Console.Write(root.data + " ");
        printTree(root.left);
        printTree(root.right);
    }

// Driver Code
public static void Main(string[] args)
{
    string exp = "a?b?c:d:e";
    BinaryTree tree = new BinaryTree();
    char[] expression = exp.ToCharArray();
    Node root = tree.convertExpression(expression, 0);
    tree.printTree(root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to convert a ternary
// expreesion to a tree.

// Class to represent Tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

// Function to convert Ternary Expression
// to a Binary Tree. It return the root of tree
function convertExpression(expression, i)
{

    // Base case
    if (i >= expression.length)
    {
        return null;
    }

    // Store current character of
    // expression_string [ 'a' to 'z']
    var root = new Node(expression[i]);

    // Move ahead in str
    ++i;

    // If current character of ternary expression
    // is '?' then we add next character as a
    // left child of current node
    if (i < expression.length && expression[i] == '?')
    {
        root.left = convertExpression(expression, i + 1);
    }

    // Else we have to add it as a right child
    // of current node expression.at(0) == ':'
    else if (i < expression.length)
    {
        root.right = convertExpression(expression, i + 1);
    }
    return root;
}

// Function print tree
function printTree(root)
{
    if (root == null)
    {
        return;
    }
    document.write(root.data + " ");
    printTree(root.left);
    printTree(root.right);
}

// Driver code
var exp = "a?b?c:d:e";
var expression = exp.split('');
var root = convertExpression(expression, 0);
printTree(root);

// This code is contributed by noob2000

</script>
```

**输出:**

```
a b c d e 
```

**时间复杂度:** O(n)【此处 **n** 为弦长】
本文由 [**尼尚辛格**](https://www.facebook.com/nishant.chaudhary.7334) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。