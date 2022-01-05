# 使用二叉树按出现顺序打印字符及其频率

> 原文:[https://www . geesforgeks . org/print-characters-and-frequency-in-order-of-occurrence-using-二叉树/](https://www.geeksforgeeks.org/print-characters-and-their-frequencies-in-order-of-occurrence-using-binary-tree/)

给定一个只包含小写字符的字符串**字符串**。问题是使用二叉树
**打印字符及其出现频率。示例:**

> **输入:**str = " aaaaabannccccz "
> **输出:**【a4b2n2 c4z】
> **解释:**
> 
> **输入:**输出: g2e4k2s2for

**进场:**

1.  从字符串中的第一个字符开始。
2.  在二叉树中执行字符的级别顺序插入
3.  选择下一个字符:
    *   如果已经看到该字符，并且我们在级别顺序插入期间遇到它，则增加节点的计数。
    *   如果到目前为止还没有看到该角色，请转到第 2 步。
4.  对字符串的所有字符重复该过程。
5.  打印应该输出所需输出的树的层次顺序遍历。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Node in the tree where
// data holds the character
// of the string and cnt
// holds the frequency
struct node {
    char data;
    int cnt;
    node *left, *right;
};

// Function to add a new
// node to the Binary Tree
node* add(char data)
{

    // Create a new node and
    // populate its data part,
    // set cnt as 1 and left
    // and right children as NULL
    node* newnode = new node;
    newnode->data = data;
    newnode->cnt = 1;
    newnode->left = newnode->right = NULL;

    return newnode;
}

// Function to add a node
// to the Binary Tree in
// level order
node* addinlvlorder(node* root, char data)
{

    if (root == NULL) {
        return add(data);
    }
    // Use the queue data structure
    // for level order insertion
    // and push the root of tree to Queue
    queue<node*> Q;
    Q.push(root);

    while (!Q.empty()) {

        node* temp = Q.front();
        Q.pop();

        // If the character to be
        // inserted is present,
        // update the cnt
        if (temp->data == data) {
            temp->cnt++;
            break;
        }
        // If the left child is
        // empty add a new node
        // as the left child
        if (temp->left == NULL) {
            temp->left = add(data);
            break;
        }
        else {
            // If the character is present
            // as a left child, update the
            // cnt and exit the loop
            if (temp->left->data == data) {
                temp->left->cnt++;
                break;
            }
            // Add the left child to
            // the queue for further
            // processing
            Q.push(temp->left);
        }
        // If the right child is empty,
        // add a new node to the right
        if (temp->right == NULL) {
            temp->right = add(data);
            break;
        }
        else {
            // If the character is present
            // as a right child, update the
            // cnt and exit the loop
            if (temp->right->data == data) {
                temp->right->cnt++;
                break;
            }
            // Add the right child to
            // the queue for further
            // processing
            Q.push(temp->right);
        }
    }

    return root;
}

// Function to print the
// level order traversal of
// the Binary Tree
void printlvlorder(node* root)
{

    // Add the root to the queue
    queue<node*> Q;
    Q.push(root);

    while (!Q.empty()) {
        node* temp = Q.front();
        // If the cnt of the character
        // is more then one, display cnt
        if (temp->cnt > 1) {
            cout << temp->data << temp->cnt;
        }
        // If the cnt of character
        // is one, display character only
        else {
            cout << temp->data;
        }
        Q.pop();
        // Add the left child to
        // the queue for further
        // processing
        if (temp->left != NULL) {
            Q.push(temp->left);
        }
        // Add the right child to
        // the queue for further
        // processing
        if (temp->right != NULL) {
            Q.push(temp->right);
        }
    }
}

// Driver code
int main()
{

    string s = "geeksforgeeks";
    node* root = NULL;

    // Add individual characters
    // to the string one by one
    // in level order
    for (int i = 0; i < s.size(); i++) {
        root = addinlvlorder(root, s[i]);
    }

    // Print the level order
    // of the constructed
    // binary tree
    printlvlorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG
{

// Node in the tree where
// data holds the character
// of the String and cnt
// holds the frequency
static class node
{
    char data;
    int cnt;
    node left, right;
};

// Function to add a new
// node to the Binary Tree
static node add(char data)
{

    // Create a new node and
    // populate its data part,
    // set cnt as 1 and left
    // and right children as null
    node newnode = new node();
    newnode.data = data;
    newnode.cnt = 1;
    newnode.left = newnode.right = null;

    return newnode;
}

// Function to add a node
// to the Binary Tree in
// level order
static node addinlvlorder(node root, char data)
{

    if (root == null)
    {
        return add(data);
    }

    // Use the queue data structure
    // for level order insertion
    // and push the root of tree to Queue
    Queue<node> Q = new LinkedList<node>();
    Q.add(root);

    while (!Q.isEmpty())
    {

        node temp = Q.peek();
        Q.remove();

        // If the character to be
        // inserted is present,
        // update the cnt
        if (temp.data == data)
        {
            temp.cnt++;
            break;
        }

        // If the left child is
        // empty add a new node
        // as the left child
        if (temp.left == null)
        {
            temp.left = add(data);
            break;
        }
        else
        {
            // If the character is present
            // as a left child, update the
            // cnt and exit the loop
            if (temp.left.data == data)
            {
                temp.left.cnt++;
                break;
            }

            // Add the left child to
            // the queue for further
            // processing
            Q.add(temp.left);
        }

        // If the right child is empty,
        // add a new node to the right
        if (temp.right == null)
        {
            temp.right = add(data);
            break;
        }
        else
        {
            // If the character is present
            // as a right child, update the
            // cnt and exit the loop
            if (temp.right.data == data)
            {
                temp.right.cnt++;
                break;
            }

            // Add the right child to
            // the queue for further
            // processing
            Q.add(temp.right);
        }
    }

    return root;
}

// Function to print the
// level order traversal of
// the Binary Tree
static void printlvlorder(node root)
{

    // Add the root to the queue
    Queue<node> Q = new LinkedList<node>();
    Q.add(root);

    while (!Q.isEmpty())
    {
        node temp = Q.peek();

        // If the cnt of the character
        // is more then one, display cnt
        if (temp.cnt > 1)
        {
            System.out.print((temp.data +""+ temp.cnt));
        }

        // If the cnt of character
        // is one, display character only
        else
        {
            System.out.print((char)temp.data);
        }
        Q.remove();

        // Add the left child to
        // the queue for further
        // processing
        if (temp.left != null)
        {
            Q.add(temp.left);
        }

        // Add the right child to
        // the queue for further
        // processing
        if (temp.right != null)
        {
            Q.add(temp.right);
        }
    }
}

// Driver code
public static void main(String[] args)
{

    String s = "geeksforgeeks";
    node root = null;

    // Add individual characters
    // to the String one by one
    // in level order
    for (int i = 0; i < s.length(); i++)
    {
        root = addinlvlorder(root, s.charAt(i));
    }

    // Print the level order
    // of the constructed
    // binary tree
    printlvlorder(root);

}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Node in the tree where
// data holds the character
// of the String and cnt
// holds the frequency
public class node
{
    public char data;
    public int cnt;
    public node left, right;
};

// Function to add a new
// node to the Binary Tree
static node add(char data)
{

    // Create a new node and
    // populate its data part,
    // set cnt as 1 and left
    // and right children as null
    node newnode = new node();
    newnode.data = data;
    newnode.cnt = 1;
    newnode.left = newnode.right = null;

    return newnode;
}

// Function to add a node
// to the Binary Tree in
// level order
static node addinlvlorder(node root, char data)
{

    if (root == null)
    {
        return add(data);
    }

    // Use the queue data structure
    // for level order insertion
    // and push the root of tree to Queue
    List<node> Q = new List<node>();
    Q.Add(root);

    while (Q.Count != 0)
    {

        node temp = Q[0];
        Q.RemoveAt(0);

        // If the character to be
        // inserted is present,
        // update the cnt
        if (temp.data == data)
        {
            temp.cnt++;
            break;
        }

        // If the left child is
        // empty add a new node
        // as the left child
        if (temp.left == null)
        {
            temp.left = add(data);
            break;
        }
        else
        {
            // If the character is present
            // as a left child, update the
            // cnt and exit the loop
            if (temp.left.data == data)
            {
                temp.left.cnt++;
                break;
            }

            // Add the left child to
            // the queue for further
            // processing
            Q.Add(temp.left);
        }

        // If the right child is empty,
        // add a new node to the right
        if (temp.right == null)
        {
            temp.right = add(data);
            break;
        }
        else
        {
            // If the character is present
            // as a right child, update the
            // cnt and exit the loop
            if (temp.right.data == data)
            {
                temp.right.cnt++;
                break;
            }

            // Add the right child to
            // the queue for further
            // processing
            Q.Add(temp.right);
        }
    }

    return root;
}

// Function to print the
// level order traversal of
// the Binary Tree
static void printlvlorder(node root)
{

    // Add the root to the queue
    List<node> Q = new List<node>();
    Q.Add(root);

    while (Q.Count != 0)
    {
        node temp = Q[0];

        // If the cnt of the character
        // is more then one, display cnt
        if (temp.cnt > 1)
        {
            Console.Write((temp.data +""+ temp.cnt));
        }

        // If the cnt of character
        // is one, display character only
        else
        {
            Console.Write((char)temp.data);
        }
        Q.RemoveAt(0);

        // Add the left child to
        // the queue for further
        // processing
        if (temp.left != null)
        {
            Q.Add(temp.left);
        }

        // Add the right child to
        // the queue for further
        // processing
        if (temp.right != null)
        {
            Q.Add(temp.right);
        }
    }
}

// Driver code
public static void Main(String[] args)
{

    String s = "geeksforgeeks";
    node root = null;

    // Add individual characters
    // to the String one by one
    // in level order
    for (int i = 0; i < s.Length; i++)
    {
        root = addinlvlorder(root, s[i]);
    }

    // Print the level order
    // of the constructed
    // binary tree
    printlvlorder(root);

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

// Node in the tree where
// data holds the character
// of the String and cnt
// holds the frequency
class node
{
    constructor()
    {
        this.data = '';
        this.cnt = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to add a new
// node to the Binary Tree
function add(data)
{

    // Create a new node and
    // populate its data part,
    // set cnt as 1 and left
    // and right children as null
    var newnode = new node();
    newnode.data = data;
    newnode.cnt = 1;
    newnode.left = newnode.right = null;

    return newnode;
}

// Function to add a node
// to the Binary Tree in
// level order
function addinlvlorder(root, data)
{

    if (root == null)
    {
        return add(data);
    }

    // Use the queue data structure
    // for level order insertion
    // and push the root of tree to Queue
    var Q = [];
    Q.push(root);

    while (Q.length != 0)
    {

        var temp = Q[0];
        Q.shift();

        // If the character to be
        // inserted is present,
        // update the cnt
        if (temp.data == data)
        {
            temp.cnt++;
            break;
        }

        // If the left child is
        // empty add a new node
        // as the left child
        if (temp.left == null)
        {
            temp.left = add(data);
            break;
        }
        else
        {
            // If the character is present
            // as a left child, update the
            // cnt and exit the loop
            if (temp.left.data == data)
            {
                temp.left.cnt++;
                break;
            }

            // push the left child to
            // the queue for further
            // processing
            Q.push(temp.left);
        }

        // If the right child is empty,
        // add a new node to the right
        if (temp.right == null)
        {
            temp.right = add(data);
            break;
        }
        else
        {
            // If the character is present
            // as a right child, update the
            // cnt and exit the loop
            if (temp.right.data == data)
            {
                temp.right.cnt++;
                break;
            }

            // push the right child to
            // the queue for further
            // processing
            Q.push(temp.right);
        }
    }

    return root;
}

// Function to print the
// level order traversal of
// the Binary Tree
function printlvlorder(root)
{

    // push the root to the queue
    var Q = [];
    Q.push(root);

    while (Q.length != 0)
    {
        var temp = Q[0];

        // If the cnt of the character
        // is more then one, display cnt
        if (temp.cnt > 1)
        {
            document.write((temp.data +""+ temp.cnt));
        }

        // If the cnt of character
        // is one, display character only
        else
        {
            document.write(temp.data);
        }
        Q.shift();

        // push the left child to
        // the queue for further
        // processing
        if (temp.left != null)
        {
            Q.push(temp.left);
        }

        // push the right child to
        // the queue for further
        // processing
        if (temp.right != null)
        {
            Q.push(temp.right);
        }
    }
}

// Driver code
var s = "geeksforgeeks";
var root = null;
// push individual characters
// to the String one by one
// in level order
for(var i = 0; i < s.length; i++)
{
    root = addinlvlorder(root, s[i]);
}
// Print the level order
// of the constructed
// binary tree
printlvlorder(root);

</script>
```

**Output:** 

```
g2e4k2s2for
```