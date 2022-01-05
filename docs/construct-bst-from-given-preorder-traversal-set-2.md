# 从给定的前序遍历|集合 2

构造 BST

> 原文:[https://www . geesforgeks . org/construct-BST-from-给定-preorder-遍历-set-2/](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversal-set-2/)

给定二叉查找树的前序遍历，构造 BST。
例如，如果给定的遍历是{10，5，1，7，40，50}，那么输出应该是跟随树的根。

```
     10
   /   \
  5     40
 /  \      \
1    7      50  
```

我们在之前的文章中讨论了 O(n^2)和 O(n)递归解。下面是一个基于堆栈的迭代解决方案，在 O(n)时间内有效。
T3】1。创建一个空堆栈。
**2。**将第一个值作为根。把它推到堆栈上。
**3。**当堆栈不为空且下一个值大于堆栈的顶值时，继续弹出。将此值作为最后一个弹出节点的右子节点。将新节点推入堆栈。
**4。**如果下一个值小于栈顶值，将该值作为栈顶节点的左子节点。将新节点推入堆栈。
**5。**重复步骤 2 和 3，直到 pre[]中还有项目。

## C++

```
// A O(n) iterative program for construction of BST from preorder traversal
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    public:
    int data;
    Node *left, *right;
} node;

// A Stack has array of Nodes, capacity, and top
class Stack
{
    public:
    int top;
    int capacity;
    Node** array;
} stack;

// A utility function to create a new tree node
Node* newNode( int data )
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to create a stack of given capacity
Stack* createStack( int capacity )
{
    Stack* stack = new Stack();
    stack->top = -1;
    stack->capacity = capacity;
    stack->array = new Node*[stack->capacity * sizeof( Node* )];
    return stack;
}

// A utility function to check if stack is full
int isFull( Stack* stack )
{
    return stack->top == stack->capacity - 1;
}

// A utility function to check if stack is empty
int isEmpty( Stack* stack )
{
    return stack->top == -1;
}

// A utility function to push an item to stack
void push( Stack* stack, Node* item )
{
    if( isFull( stack ) )
        return;
    stack->array[ ++stack->top ] = item;
}

// A utility function to remove an item from stack
Node* pop( Stack* stack )
{
    if( isEmpty( stack ) )
        return NULL;
    return stack->array[ stack->top-- ];
}

// A utility function to get top node of stack
Node* peek( Stack* stack )
{
    return stack->array[ stack->top ];
}

// The main function that constructs BST from pre[]
Node* constructTree ( int pre[], int size )
{
    // Create a stack of capacity equal to size
    Stack* stack = createStack( size );

    // The first element of pre[] is always root
    Node* root = newNode( pre[0] );

    // Push root
    push( stack, root );

    int i;
    Node* temp;

    // Iterate through rest of the size-1 items of given preorder array
    for ( i = 1; i < size; ++i )
    {
        temp = NULL;

        /* Keep on popping while the next value is greater than
        stack's top value. */
        while ( !isEmpty( stack ) && pre[i] > peek( stack )->data )
            temp = pop( stack );

        // Make this greater value as the right child
                // and push it to the stack
        if ( temp != NULL)
        {
            temp->right = newNode( pre[i] );
            push( stack, temp->right );
        }

        // If the next value is less than the stack's top
                // value, make this value as the left child of the
                // stack's top node. Push the new node to stack
        else
        {
            peek( stack )->left = newNode( pre[i] );
            push( stack, peek( stack )->left );
        }
    }

    return root;
}

// A utility function to print inorder traversal of a Binary Tree
void printInorder (Node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout<<node->data<<" ";
    printInorder(node->right);
}

// Driver program to test above functions
int main ()
{
    int pre[] = {10, 5, 1, 7, 40, 50};
    int size = sizeof( pre ) / sizeof( pre[0] );

    Node *root = constructTree(pre, size);

    cout<<"Inorder traversal of the constructed tree: \n";
    printInorder(root);

    return 0;
}

//This code is contributed by rathbhupendra
```

## C

```
// A O(n) iterative program for construction of BST from preorder traversal
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
typedef struct Node
{
    int data;
    struct Node *left, *right;
} Node;

// A Stack has array of Nodes, capacity, and top
typedef struct Stack
{
    int top;
    int capacity;
    Node* *array;
} Stack;

// A utility function to create a new tree node
Node* newNode( int data )
{
    Node* temp = (Node *)malloc( sizeof( Node ) );
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to create a stack of given capacity
Stack* createStack( int capacity )
{
    Stack* stack = (Stack *)malloc( sizeof( Stack ) );
    stack->top = -1;
    stack->capacity = capacity;
    stack->array = (Node **)malloc( stack->capacity * sizeof( Node* ) );
    return stack;
}

// A utility function to check if stack is full
int isFull( Stack* stack )
{
    return stack->top == stack->capacity - 1;
}

// A utility function to check if stack is empty
int isEmpty( Stack* stack )
{
    return stack->top == -1;
}

// A utility function to push an item to stack
void push( Stack* stack, Node* item )
{
    if( isFull( stack ) )
        return;
    stack->array[ ++stack->top ] = item;
}

// A utility function to remove an item from stack
Node* pop( Stack* stack )
{
    if( isEmpty( stack ) )
        return NULL;
    return stack->array[ stack->top-- ];
}

// A utility function to get top node of stack
Node* peek( Stack* stack )
{
    return stack->array[ stack->top ];
}

// The main function that constructs BST from pre[]
Node* constructTree ( int pre[], int size )
{
    // Create a stack of capacity equal to size
    Stack* stack = createStack( size );

    // The first element of pre[] is always root
    Node* root = newNode( pre[0] );

    // Push root
    push( stack, root );

    int i;
    Node* temp;

    // Iterate through rest of the size-1 items of given preorder array
    for ( i = 1; i < size; ++i )
    {
        temp = NULL;

        /* Keep on popping while the next value is greater than
           stack's top value. */
        while ( !isEmpty( stack ) && pre[i] > peek( stack )->data )
            temp = pop( stack );

        // Make this greater value as the right child
        // and push it to the stack
        if ( temp != NULL)
        {
            temp->right = newNode( pre[i] );
            push( stack, temp->right );
        }

        // If the next value is less than the stack's top
        // value, make this value as the left child of the
        // stack's top node. Push the new node to stack
        else
        {
            peek( stack )->left = newNode( pre[i] );
            push( stack, peek( stack )->left );
        }
    }

    return root;
}

// A utility function to print inorder traversal of a Binary Tree
void printInorder (Node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

// Driver program to test above functions
int main ()
{
    int pre[] = {10, 5, 1, 7, 40, 50};
    int size = sizeof( pre ) / sizeof( pre[0] );

    Node *root = constructTree(pre, size);

    printf("Inorder traversal of the constructed tree: \n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct BST from given preorder traversal

import java.util.*;

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d) {
        data = d;
        left = right = null;
    }
}

class BinaryTree {

    // The main function that constructs BST from pre[]
    Node constructTree(int pre[], int size) {

        // The first element of pre[] is always root
        Node root = new Node(pre[0]);

        Stack<Node> s = new Stack<Node>();

        // Push root
        s.push(root);

        // Iterate through rest of the size-1 items of given preorder array
        for (int i = 1; i < size; ++i) {
            Node temp = null;

            /* Keep on popping while the next value is greater than
             stack's top value. */
            while (!s.isEmpty() && pre[i] > s.peek().data) {
                temp = s.pop();
            }

            // Make this greater value as the right child
            // and push it to the stack
            if (temp != null) {
                temp.right = new Node(pre[i]);
                s.push(temp.right);
            }

            // If the next value is less than the stack's top
            // value, make this value as the left child of the
            // stack's top node. Push the new node to stack
            else {
                temp = s.peek();
                temp.left = new Node(pre[i]);
                s.push(temp.left);
            }
        }

        return root;
    }

    // A utility function to print inorder traversal of a Binary Tree
    void printInorder(Node node) {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test above functions
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int pre[] = new int[]{10, 5, 1, 7, 40, 50};
        int size = pre.length;
        Node root = tree.constructTree(pre, size);
        System.out.println("Inorder traversal of the constructed tree is ");
        tree.printInorder(root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to construct BST
# from given preorder traversal

# A binary tree node
class Node:

    def __init__(self, data = 0):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree :

    # The main function that constructs BST from pre[]
    def constructTree(self, pre, size):

        # The first element of pre[] is always root
        root = Node(pre[0])

        s = []

        # append root
        s.append(root)

        i = 1

        # Iterate through rest of the size-1
        # items of given preorder array
        while ( i < size):
            temp = None

            # Keep on popping while the next value
            # is greater than stack's top value.
            while (len(s) > 0 and pre[i] > s[-1].data):
                temp = s.pop()

            # Make this greater value as the right child
            # and append it to the stack
            if (temp != None):
                temp.right = Node(pre[i])
                s.append(temp.right)

            # If the next value is less than the stack's top
            # value, make this value as the left child of the
            # stack's top node. append the new node to stack
            else :
                temp = s[-1]
                temp.left = Node(pre[i])
                s.append(temp.left)
            i = i + 1

        return root

    # A utility function to print
    # inorder traversal of a Binary Tree
    def printInorder(self,node):
        if (node == None):
            return

        self.printInorder(node.left)
        print(node.data, end = " ")
        self.printInorder(node.right)

# Driver code
tree = BinaryTree()
pre = [10, 5, 1, 7, 40, 50]
size = len(pre)
root = tree.constructTree(pre, size)
print("Inorder traversal of the constructed tree is ")
tree.printInorder(root)

# This code is contributed by Arnab Kundu
```

## C#

```
using System;
using System.Collections.Generic;

// c# program to construct BST from given preorder traversal

// A binary tree node
public class Node
{

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinaryTree
{

    // The main function that constructs BST from pre[]
    public virtual Node constructTree(int[] pre, int size)
    {

        // The first element of pre[] is always root
        Node root = new Node(pre[0]);

        Stack<Node> s = new Stack<Node>();

        // Push root
        s.Push(root);

        // Iterate through rest of the size-1 items of given preorder array
        for (int i = 1; i < size; ++i)
        {
            Node temp = null;

            /* Keep on popping while the next value is greater than
             stack's top value. */
            while (s.Count > 0 && pre[i] > s.Peek().data)
            {
                temp = s.Pop();
            }

            // Make this greater value as the right child
            // and push it to the stack
            if (temp != null)
            {
                temp.right = new Node(pre[i]);
                s.Push(temp.right);
            }

            // If the next value is less than the stack's top
            // value, make this value as the left child of the
            // stack's top node. Push the new node to stack
            else
            {
                temp = s.Peek();
                temp.left = new Node(pre[i]);
                s.Push(temp.left);
            }
        }

        return root;
    }

    // A utility function to print inorder traversal of a Binary Tree
    public virtual void printInorder(Node node)
    {
        if (node == null)
        {
            return;
        }
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        int[] pre = new int[]{10, 5, 1, 7, 40, 50};
        int size = pre.Length;
        Node root = tree.constructTree(pre, size);
        Console.WriteLine("Inorder traversal of the constructed tree is ");
        tree.printInorder(root);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

      // JavaScript program to construct BST
      // from given preorder traversal

      // A binary tree node
      class Node {
        constructor(d) {
          this.data = d;
          this.left = null;
          this.right = null;
        }
      }

      class BinaryTree {
        // The main function that constructs BST from pre[]
        constructTree(pre, size) {
          // The first element of pre[] is always root
          var root = new Node(pre[0]);

          var s = [];

          // Push root
          s.push(root);

          // Iterate through rest of the size-1
          // items of given preorder array
          for (var i = 1; i < size; ++i) {
            var temp = null;

            /* Keep on popping while the next value is greater than
            stack's top value. */
            while (s.length > 0 && pre[i] > s[s.length - 1].data) {
              temp = s.pop();
            }

            // Make this greater value as the right child
            // and push it to the stack
            if (temp != null) {
              temp.right = new Node(pre[i]);
              s.push(temp.right);
            }

            // If the next value is less than the stack's top
            // value, make this value as the left child of the
            // stack's top node. Push the new node to stack
            else {
              temp = s[s.length - 1];
              temp.left = new Node(pre[i]);
              s.push(temp.left);
            }
          }

          return root;
        }

        // A utility function to print
        // inorder traversal of a Binary Tree
        printInorder(node) {
          if (node == null) {
            return;
          }
          this.printInorder(node.left);
          document.write(node.data + " ");
          this.printInorder(node.right);
        }
      }
      // Driver program to test above functions

      var tree = new BinaryTree();
      var pre = [10, 5, 1, 7, 40, 50];
      var size = pre.length;
      var root = tree.constructTree(pre, size);
      document.write(
      "Inorder traversal of the constructed tree is <br>");
      tree.printInorder(root);

</script>
```

**输出:**

```
Inorder traversal of the constructed tree is 
1 5 7 10 40 50  
```

**时间复杂度:** O(n)。从第一眼看，复杂程度更高。如果我们仔细观察，我们可以观察到每个项目只被推送和弹出一次。因此，在 constructTree()的主循环中最多执行 2n 次推/弹出操作。因此，时间复杂度为 O(n)。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。