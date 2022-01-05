# 从存储在二叉树中的字符串中删除元音

> 原文:[https://www . geesforgeks . org/从二进制树中存储的字符串中移除元音/](https://www.geeksforgeeks.org/remove-vowels-from-a-string-stored-in-a-binary-tree/)

给定一棵二叉树，使得二叉树的水平顺序遍历产生一个字符串。任务是从二叉树中删除所有元音，并打印剩余树的水平顺序遍历。
**例:**

```
Input: 
     G
   /   \
  E     E
 / \ 
K   S

Output:
     G
   /   \
  K     S

Input:
     G
   /   \
  O     A
 /  
L   

Output:
     G 
   / 
  L    
```

**进场:**

1.  执行字符串中字符的级别顺序插入。
2.  声明一个新的二叉树，其根设置为空。
3.  执行二叉树的水平顺序遍历。
4.  如果遇到元音，不要将其添加到新的二叉树中。
5.  否则，将该字符添加到新的二叉树中。
6.  执行新树的级别顺序遍历。

以下是上述方法的实现:

## C++

```
// C++ program
// for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure Representing
// the Node in the Binary tree
struct Node {
    char data;
    Node *left, *right;
    Node(char _val)
    {
        data = _val;
        left = right = NULL;
    }
};

// Function to perform a level
// order insertion of a new Node
// in the Binary tree
Node* addinBT(Node* root, char data)
{
    // If the root is empty,
    // make it point to the new Node
    if (root == NULL) {
        root = new Node(data);
    }
    else {

        // In case there are elements
        // in the Binary tree, perform
        // a level order traversal
        // using a Queue
        queue<Node*> Q;
        Q.push(root);

        while (!Q.empty()) {
            Node* temp = Q.front();
            Q.pop();
            // If the left child does
            // not exist, insert the
            // new Node as the left child
            if (temp->left == NULL) {
                temp->left = new Node(data);
                break;
            }
            else
                Q.push(temp->left);
            // In case the right child
            // does not exist, insert
            // the new Node as the right child
            if (temp->right == NULL) {
                temp->right = new Node(data);
                break;
            }
            else
                Q.push(temp->right);
        }
    }
    return root;
}

// Function to print the level
// order traversal of the Binary tree
void print(Node* root)
{

    queue<Node*> Q;
    Q.push(root);

    while (Q.size()) {
        Node* temp = Q.front();
        Q.pop();
        cout << temp->data;
        if (temp->left)
            Q.push(temp->left);
        if (temp->right)
            Q.push(temp->right);
    }
}

// Function to check if the
// character is a vowel or not.
bool checkvowel(char ch)
{
    ch = tolower(ch);
    if (ch == 'a' || ch == 'e' || ch == 'i'
                  || ch == 'o' || ch == 'u') {
        return true;
    }
    else {
        return false;
    }
}

// Function to remove the
// vowels in the new Binary tree
Node* removevowels(Node* root)
{
    queue<Node*> Q;
    Q.push(root);
    // Declaring the root of
    // the new tree
    Node* root1 = NULL;

    while (!Q.empty()) {
        Node* temp = Q.front();
        Q.pop();
        // If the given character
        // is not a vowel, add it
        // to the new Binary tree
        if (!checkvowel(temp->data)) {
            root1 = addinBT(root1, temp->data);
        }
        if (temp->left) {
            Q.push(temp->left);
        }
        if (temp->right) {
            Q.push(temp->right);
        }
    }
    return root1;
}

// Driver code
int main()
{

    string s = "geeks";
    Node* root = NULL;

    for (int i = 0; i < s.size(); i++) {
        root = addinBT(root, s[i]);
    }

    root = removevowels(root);
    print(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

    // Structure Representing
    // the Node in the Binary tree
    static class Node
    {
        char data;
        Node left, right;

        Node(char _val)
        {
            data = _val;
            left = right = null;
        }
    };

    // Function to perform a level
    // order insertion of a new Node
    // in the Binary tree
    static Node addinBT(Node root,
                        char data)
    {
        // If the root is empty,
        // make it point to the new Node
        if (root == null)
        {
            root = new Node(data);
        }
        else
        {

            // In case there are elements
            // in the Binary tree, perform
            // a level order traversal
            // using a Queue
            Queue<Node> Q = new LinkedList<Node>();
            Q.add(root);

            while (!Q.isEmpty())
            {
                Node temp = Q.peek();
                Q.remove();

                // If the left child does
                // not exist, insert the
                // new Node as the left child
                if (temp.left == null)
                {
                    temp.left = new Node(data);
                    break;
                }
                else
                    Q.add(temp.left);

                // In case the right child
                // does not exist, insert
                // the new Node as the right child
                if (temp.right == null)
                {
                    temp.right = new Node(data);
                    break;
                }
                else
                    Q.add(temp.right);
            }
        }
        return root;
    }

    // Function to print the level
    // order traversal of the Binary tree
    static void print(Node root)
    {
        Queue<Node> Q = new LinkedList<Node>();
        Q.add(root);

        while (Q.size() > 0)
        {
            Node temp = Q.peek();
            Q.remove();
            System.out.print(temp.data);
            if (temp.left != null)
                Q.add(temp.left);
            if (temp.right != null)
                Q.add(temp.right);
        }
    }

    // Function to check if the
    // character is a vowel or not.
    static boolean checkvowel(char ch)
    {
        ch = Character.toLowerCase(ch);
        if (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u')
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Function to remove the
    // vowels in the new Binary tree
    static Node removevowels(Node root)
    {
        Queue<Node> Q = new LinkedList<Node>();
        Q.add(root);

        // Declaring the root of
        // the new tree
        Node root1 = null;

        while (!Q.isEmpty())
        {
            Node temp = Q.peek();
            Q.remove();

            // If the given character
            // is not a vowel, add it
            // to the new Binary tree
            if (!checkvowel(temp.data))
            {
                root1 = addinBT(root1, temp.data);
            }
            if (temp.left != null)
            {
                Q.add(temp.left);
            }
            if (temp.right != null)
            {
                Q.add(temp.right);
            }
        }
        return root1;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeks";
        Node root = null;

        for (int i = 0; i < s.length(); i++)
        {
            root = addinBT(root, s.charAt(i));
        }

        root = removevowels(root);
        print(root);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program
# for the above approach

# Structure Representing
# the Node in the Binary tree
class Node:
    def __init__( self,_val):
        self.data = _val
        self.left = self.right = None

# Function to perform a level
# order insertion of a Node
# in the Binary tree
def addinBT(root, data):

    # If the root is empty,
    # make it point to the Node
    if (root == None) :
        root = Node(data)

    else :

        # In case there are elements
        # in the Binary tree, perform
        # a level order traversal
        # using a Queue
        Q = []
        Q.append(root)

        while (len(Q) > 0):
            temp = Q[-1]
            Q.pop()

            # If the left child does
            # not exist, insert the
            # Node as the left child
            if (temp.left == None) :
                temp.left = Node(data)
                break

            else:
                Q.append(temp.left)

            # In case the right child
            # does not exist, insert
            # the Node as the right child
            if (temp.right == None):
                temp.right = Node(data)
                break

            else:
                Q.append(temp.right)

    return root

# Function to print the level
# order traversal of the Binary tree
def print_(root):

    Q = []
    Q.append(root)

    while (len(Q) > 0) :
        temp = Q[-1]
        Q.pop()
        print(temp.data,end = " ")
        if (temp.left != None):
            Q.append(temp.left)
        if (temp.right != None):
            Q.append(temp.right)

# Function to check if the
# character is a vowel or not.
def checkvowel( ch):

    ch = ch.lower()
    if (ch == 'a' or ch == 'e' or ch == 'i'
                or ch == 'o' or ch == 'u'):
        return True

    else:
        return False

# Function to remove the
# vowels in the Binary tree
def removevowels(root):

    Q = []
    Q.append(root)

    # Declaring the root of
    # the tree
    root1 = None

    while (len(Q) > 0):
        temp = Q[-1]
        Q.pop()

        # If the given character
        # is not a vowel, add it
        # to the Binary tree
        if (not checkvowel(temp.data)) :
            root1 = addinBT(root1, temp.data)

        if (temp.left != None):
            Q.append(temp.left)

        if (temp.right != None):
            Q.append(temp.right)

    return root1

# Driver code
s = "geeks"
root = None

for i in range( len(s) ) :
    root = addinBT(root, s[i])

root = removevowels(root)
print_(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Structure Representing
    // the Node in the Binary tree
    class Node
    {
        public char data;
        public Node left, right;

        public Node(char _val)
        {
            data = _val;
            left = right = null;
        }
    };

    // Function to perform a level
    // order insertion of a new Node
    // in the Binary tree
    static Node addinBT(Node root,
                        char data)
    {
        // If the root is empty,
        // make it point to the new Node
        if (root == null)
        {
            root = new Node(data);
        }
        else
        {

            // In case there are elements
            // in the Binary tree, perform
            // a level order traversal
            // using a Queue
            List<Node> Q = new List<Node>();
            Q.Add(root);

            while (Q.Count != 0)
            {
                Node temp = Q[0];
                Q.RemoveAt(0);

                // If the left child does
                // not exist, insert the
                // new Node as the left child
                if (temp.left == null)
                {
                    temp.left = new Node(data);
                    break;
                }
                else
                    Q.Add(temp.left);

                // In case the right child
                // does not exist, insert
                // the new Node as the right child
                if (temp.right == null)
                {
                    temp.right = new Node(data);
                    break;
                }
                else
                    Q.Add(temp.right);
            }
        }
        return root;
    }

    // Function to print the level
    // order traversal of the Binary tree
    static void print(Node root)
    {
        List<Node> Q = new List<Node>();
        Q.Add(root);

        while (Q.Count > 0)
        {
            Node temp = Q[0];
            Q.RemoveAt(0);
            Console.Write(temp.data);
            if (temp.left != null)
                Q.Add(temp.left);
            if (temp.right != null)
                Q.Add(temp.right);
        }
    }

    // Function to check if the
    // character is a vowel or not.
    static bool checkvowel(char ch)
    {
        ch = char.ToLower(ch);
        if (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u')
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Function to remove the
    // vowels in the new Binary tree
    static Node removevowels(Node root)
    {
        List<Node> Q = new List<Node>();
        Q.Add(root);

        // Declaring the root of
        // the new tree
        Node root1 = null;

        while (Q.Count != 0)
        {
            Node temp = Q[0];
            Q.RemoveAt(0);

            // If the given character
            // is not a vowel, add it
            // to the new Binary tree
            if (!checkvowel(temp.data))
            {
                root1 = addinBT(root1, temp.data);
            }
            if (temp.left != null)
            {
                Q.Add(temp.left);
            }
            if (temp.right != null)
            {
                Q.Add(temp.right);
            }
        }
        return root1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeks";
        Node root = null;

        for (int i = 0; i < s.Length; i++)
        {
            root = addinBT(root, s[i]);
        }

        root = removevowels(root);
        print(root);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Structure Representing
// the Node in the Binary tree
class Node
{
    constructor(_val)
    {
        this.data = _val;
        this.left = null;
        this.right = null;
    }
};
// Function to perform a level
// order insertion of a new Node
// in the Binary tree
function addinBT(root, data)
{
    // If the root is empty,
    // make it point to the new Node
    if (root == null)
    {
        root = new Node(data);
    }
    else
    {
        // In case there are elements
        // in the Binary tree, perform
        // a level order traversal
        // using a Queue
        var Q = [];
        Q.push(root);
        while (Q.length != 0)
        {
            var temp = Q[0];
            Q.shift();

            // If the left child does
            // not exist, insert the
            // new Node as the left child
            if (temp.left == null)
            {
                temp.left = new Node(data);
                break;
            }
            else
                Q.push(temp.left);

            // In case the right child
            // does not exist, insert
            // the new Node as the right child
            if (temp.right == null)
            {
                temp.right = new Node(data);
                break;
            }
            else
                Q.push(temp.right);
        }
    }
    return root;
}
// Function to print the level
// order traversal of the Binary tree
function print(root)
{
    var Q = []
    Q.push(root);
    while (Q.length > 0)
    {
        var temp = Q[0];
        Q.shift();
        document.write(temp.data);
        if (temp.left != null)
            Q.push(temp.left);
        if (temp.right != null)
            Q.push(temp.right);
    }
}
// Function to check if the
// character is a vowel or not.
function checkvowel(ch)
{
    ch = ch.toLowerCase();
    if (ch == "a" || ch == "e" ||
        ch == "i" || ch == "o" ||
        ch == "u")
    {
        return true;
    }
    else
    {
        return false;
    }
}
// Function to remove the
// vowels in the new Binary tree
function removevowels(root)
{
    var Q = []
    Q.push(root);

    // Declaring the root of
    // the new tree
    var root1 = null;
    while (Q.length != 0)
    {
        var temp = Q[0];
        Q.shift();

        // If the given character
        // is not a vowel, push it
        // to the new Binary tree
        if (!checkvowel(temp.data))
        {
            root1 = addinBT(root1, temp.data);
        }
        if (temp.left != null)
        {
            Q.push(temp.left);
        }
        if (temp.right != null)
        {
            Q.push(temp.right);
        }
    }
    return root1;
}
// Driver code
var s = "geeks";
var root = null;
for (var i = 0; i < s.length; i++)
{
    root = addinBT(root, s[i]);
}
root = removevowels(root);
print(root);

</script>
```

**Output:** 

```
gks
```