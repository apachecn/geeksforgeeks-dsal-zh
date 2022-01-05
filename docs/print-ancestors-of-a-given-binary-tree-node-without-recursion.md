# 不递归打印给定二叉树节点的祖先

> 原文:[https://www . geesforgeks . org/print-给定二叉树的祖先-无递归节点/](https://www.geeksforgeeks.org/print-ancestors-of-a-given-binary-tree-node-without-recursion/)

给定一棵二叉树和一个键，编写一个函数，打印给定二叉树中键的所有祖先。
例如，考虑下面的二叉树

```
            1
        /       \
       2         3
     /   \     /   \
    4     5    6    7 
   /       \       /
  8         9     10  
```

以下是上述树中不同的输入键及其祖先

```
Input Key    List of Ancestors 
-------------------------
 1            
 2            1
 3            1
 4            2 1
 5            2 1
 6            3 1
 7            3 1
 8            4 2 1
 9            5 2 1
10            7 3 1
```

这个问题的递归解在[这里](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)讨论。
很明显，我们需要使用基于堆栈的二叉树迭代遍历。其思想是当我们到达具有给定键的节点时，所有祖先都在堆栈中。一旦我们拿到钥匙，我们要做的就是打印堆栈的内容。
当我们到达给定节点时，如何获取堆栈中的所有祖先？我们可以以后序方式遍历所有节点。如果我们仔细观察递归后序遍历，我们可以很容易地观察到，当对一个节点调用递归函数时，递归调用栈包含该节点的祖先。因此，我们的想法是进行迭代后置遍历，并在到达所需节点时停止遍历。
以下是上述办法的实施情况。

## C

```
// C program to print all ancestors of a given key
#include <stdio.h>
#include <stdlib.h>

// Maximum stack size
#define MAX_SIZE 100

// Structure for a tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Structure for Stack
struct Stack
{
    int size;
    int top;
    struct Node* *array;
};

// A utility function to create a new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// A utility function to create a stack of given size
struct Stack* createStack(int size)
{
    struct Stack* stack = (struct Stack*) malloc(sizeof(struct Stack));
    stack->size = size;
    stack->top = -1;
    stack->array = (struct Node**) malloc(stack->size * sizeof(struct Node*));
    return stack;
}

// BASIC OPERATIONS OF STACK
int isFull(struct Stack* stack)
{
    return ((stack->top + 1) == stack->size);
}
int isEmpty(struct Stack* stack)
{
    return stack->top == -1;
}
void push(struct Stack* stack, struct Node* node)
{
    if (isFull(stack))
        return;
    stack->array[++stack->top] = node;
}
struct Node* pop(struct Stack* stack)
{
    if (isEmpty(stack))
        return NULL;
    return stack->array[stack->top--];
}
struct Node* peek(struct Stack* stack)
{
    if (isEmpty(stack))
        return NULL;
    return stack->array[stack->top];
}

// Iterative Function to print all ancestors of a given key
void printAncestors(struct Node *root, int key)
{
    if (root == NULL) return;

    // Create a stack to hold ancestors
    struct Stack* stack = createStack(MAX_SIZE);

    // Traverse the complete tree in postorder way till we find the key
    while (1)
    {
        // Traverse the left side. While traversing, push the nodes into
        // the stack so that their right subtrees can be traversed later
        while (root && root->data != key)
        {
            push(stack, root);   // push current node
            root = root->left;  // move to next node
        }

        // If the node whose ancestors are to be printed is found,
        // then break the while loop.
        if (root && root->data == key)
            break;

        // Check if right sub-tree exists for the node at top
        // If not then pop that node because we don't need this
        // node any more.
        if (peek(stack)->right == NULL)
        {
            root = pop(stack);

            // If the popped node is right child of top, then remove the top
            // as well. Left child of the top must have processed before.
            // Consider the following tree for example and key = 3.  If we
            // remove the following loop, the program will go in an
            // infinite loop after reaching 5.
            //          1
            //        /   \
            //       2     3
            //         \
            //           4
            //             \
            //              5
            while (!isEmpty(stack) && peek(stack)->right == root)
               root = pop(stack);
        }

        // if stack is not empty then simply set the root as right child
        // of top and start traversing right sub-tree.
        root = isEmpty(stack)? NULL: peek(stack)->right;
    }

    // If stack is not empty, print contents of stack
    // Here assumption is that the key is there in tree
    while (!isEmpty(stack))
        printf("%d ", pop(stack)->data);
}

// Driver program to test above functions
int main()
{
    // Let us construct a binary tree
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->right->right = newNode(9);
    root->right->right->left = newNode(10);

    printf("Following are all keys and their ancestors\n");
    for (int key = 1; key <= 10; key++)
    {
        printf("%d: ", key);
        printAncestors(root, key);
        printf("\n");
    }

    getchar();
    return 0;
}
```

## C++

```
// C++ program to print all ancestors of a given key
#include <bits/stdc++.h>
using namespace std;

// Structure for a tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Iterative Function to print all ancestors of a given key
void printAncestors(struct Node *root, int key)
{
    if (root == NULL) return;

    // Create a stack to hold ancestors
    stack<struct Node* > st;

    // Traverse the complete tree in postorder way till we find the key
    while (1)
    {
        // Traverse the left side. While traversing, push the nodes into
        // the stack so that their right subtrees can be traversed later
        while (root && root->data != key)
        {
            st.push(root);   // push current node
            root = root->left;  // move to next node
        }

        // If the node whose ancestors are to be printed is found,
        // then break the while loop.
        if (root && root->data == key)
            break;

        // Check if right sub-tree exists for the node at top
        // If not then pop that node because we don't need this
        // node any more.
        if (st.top()->right == NULL)
        {
            root = st.top();
            st.pop();

            // If the popped node is right child of top, then remove the top
            // as well. Left child of the top must have processed before.

            while (!st.empty() && st.top()->right == root)
               {root = st.top();
               st.pop();
               }
        }

        // if stack is not empty then simply set the root as right child
        // of top and start traversing right sub-tree.
        root = st.empty()? NULL: st.top()->right;
    }

    // If stack is not empty, print contents of stack
    // Here assumption is that the key is there in tree
    while (!st.empty())
    {
        cout<<st.top()->data<<" ";
        st.pop();
    }
}

// Driver program to test above functions
int main()
{
    // Let us construct a binary tree
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->right->right = newNode(9);
    root->right->right->left = newNode(10);

    cout<<"Following are all keys and their ancestors"<<endl;
    for (int key = 1; key <= 10; key++)
    {
        cout<<key<<":"<<" ";
        printAncestors(root, key);
        cout<<endl;
    }

    return 0;
}
// This code is contributed by Gautam Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all ancestors of a given key
import java.util.Stack;

public class GFG
{
    // Class for a tree node
    static class Node
    {
        int data;
        Node left,right;

        // constructor to create Node
        // left and right are by default null
        Node(int data)
        {
            this.data = data;
        }
    }

    // Iterative Function to print all ancestors of a given key
    static void printAncestors(Node root,int key)
    {
        if(root == null)
            return;

         // Create a stack to hold ancestors
        Stack<Node> st = new Stack<>();

        // Traverse the complete tree in postorder way till we find the key
        while(true)
        {

            // Traverse the left side. While traversing, push the nodes into
            // the stack so that their right subtrees can be traversed later
            while(root != null && root.data != key)
            {
                st.push(root);   // push current node
                root = root.left;   // move to next node
            }

            // If the node whose ancestors are to be printed is found,
            // then break the while loop.
            if(root != null && root.data == key)
                break;

            // Check if right sub-tree exists for the node at top
            // If not then pop that node because we don't need this
            // node any more.
            if(st.peek().right == null)
            {
                root =st.peek();
                st.pop();

                // If the popped node is right child of top, then remove the top
                // as well. Left child of the top must have processed before.
                while( st.empty() == false && st.peek().right == root)
                {
                    root = st.peek();
                    st.pop();
                }
            }

            // if stack is not empty then simply set the root as right child
            // of top and start traversing right sub-tree.
            root = st.empty() ? null : st.peek().right;
        }

        // If stack is not empty, print contents of stack
        // Here assumption is that the key is there in tree
        while( !st.empty() )
        {
            System.out.print(st.peek().data+" ");
            st.pop();
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
         // Let us construct a binary tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.left.left = new Node(8);
        root.left.right.right = new Node(9);
        root.right.right.left = new Node(10);

        System.out.println("Following are all keys and their ancestors");
        for(int key = 1;key <= 10;key++)
        {
            System.out.print(key+": ");
            printAncestors(root, key);
            System.out.println();
        }
    }

}
//This code is Contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to print all ancestors of a given key

# Class for a tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Iterative Function to print all ancestors of a given key
def printAncestors(root, key):
    if(root == None):
        return;

     # Create a stack to hold ancestors
    st = []

    # Traverse the complete tree in postorder way till we find the key
    while(True):

        # Traverse the left side. While traversing, append the nodes into
        # the stack so that their right subtrees can be traversed later
        while(root != None and root.data != key):

            st.append(root);   # append current node
            root = root.left;   # move to next node

        # If the node whose ancestors are to be printed is found,
        # then break the while loop.
        if(root != None and root.data == key):
            break;

        # Check if right sub-tree exists for the node at top
        # If not then pop that node because we don't need this
        # node any more.
        if(st[-1].right == None):
            root = st[-1];
            st.pop();

            # If the popped node is right child of top, then remove the top
            # as well. Left child of the top must have processed before.
            while(len(st) != 0 and st[-1].right == root):
                root = st[-1];
                st.pop();

        # if stack is not empty then simply set the root as right child
        # of top and start traversing right sub-tree.
        root = None if len(st) == 0 else st[-1].right;

    # If stack is not empty, print contents of stack
    # Here assumption is that the key is there in tree
    while(len(st) != 0):
        print(st[-1].data, end = " ")
        st.pop();

# Driver program to test above functions
if __name__=='__main__':

     # Let us construct a binary tree
    root = Node(1);
    root.left = Node(2);
    root.right = Node(3);
    root.left.left = Node(4);
    root.left.right = Node(5);
    root.right.left = Node(6);
    root.right.right = Node(7);
    root.left.left.left = Node(8);
    root.left.right.right = Node(9);
    root.right.right.left = Node(10);

    print("Following are all keys and their ancestors");
    for key in range(1, 11):

        print(key, end = ": ");
        printAncestors(root, key);
        print();

# This code is contributed by rutvik_56.
```

## C#

```
// C# program to print all ancestors
// of a given key
using System;
using System.Collections.Generic;

class GFG
{
// Class for a tree node
public class Node
{
    public int data;
    public Node left, right;

    // constructor to create Node
    // left and right are by default null
    public Node(int data)
    {
        this.data = data;
    }
}

// Iterative Function to print
// all ancestors of a given key
public static void printAncestors(Node root,
                                  int key)
{
    if (root == null)
    {
        return;
    }

    // Create a stack to hold ancestors
    Stack<Node> st = new Stack<Node>();

    // Traverse the complete tree in
    // postorder way till we find the key
    while (true)
    {

        // Traverse the left side. While
        // traversing, push the nodes into
        // the stack so that their right
        // subtrees can be traversed later
        while (root != null && root.data != key)
        {
            st.Push(root); // push current node
            root = root.left; // move to next node
        }

        // If the node whose ancestors
        // are to be printed is found,
        // then break the while loop.
        if (root != null && root.data == key)
        {
            break;
        }

        // Check if right sub-tree exists for
        // the node at top. If not then pop
        // that node because we don't need
        // this node any more.
        if (st.Peek().right == null)
        {
            root = st.Peek();
            st.Pop();

            // If the popped node is right child
            // of top, then remove the top as well.
            // Left child of the top must have
            // processed before.
            while (st.Count > 0 &&
                   st.Peek().right == root)
            {
                root = st.Peek();
                st.Pop();
            }
        }

        // if stack is not empty then simply
        // set the root as right child of top
        // and start traversing right sub-tree.
        root = st.Count == 0 ?
                        null : st.Peek().right;
    }

    // If stack is not empty, print contents
    // of stack. Here assumption is that the
    // key is there in tree
    while (st.Count > 0)
    {
        Console.Write(st.Peek().data + " ");
        st.Pop();
    }
}

// Driver Code
public static void Main(string[] args)
{
    // Let us construct a binary tree
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.left.left.left = new Node(8);
    root.left.right.right = new Node(9);
    root.right.right.left = new Node(10);

    Console.WriteLine("Following are all keys " +
                          "and their ancestors");
    for (int key = 1; key <= 10; key++)
    {
        Console.Write(key + ": ");
        printAncestors(root, key);
        Console.WriteLine();
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to print all ancestors of a given key

    // Class for a tree node
    class Node
    {
        // constructor to create Node
        // left and right are by default null
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Iterative Function to print
    // all ancestors of a given key
    function printAncestors(root, key)
    {
        if (root == null)
        {
            return;
        }

        // Create a stack to hold ancestors
        let st = [];

        // Traverse the complete tree in
        // postorder way till we find the key
        while (true)
        {

            // Traverse the left side. While
            // traversing, push the nodes into
            // the stack so that their right
            // subtrees can be traversed later
            while (root != null && root.data != key)
            {
                st.push(root); // push current node
                root = root.left; // move to next node
            }

            // If the node whose ancestors
            // are to be printed is found,
            // then break the while loop.
            if (root != null && root.data == key)
            {
                break;
            }

            // Check if right sub-tree exists for
            // the node at top. If not then pop
            // that node because we don't need
            // this node any more.
            if (st[st.length - 1].right == null)
            {
                root = st[st.length - 1];
                st.pop();

                // If the popped node is right child
                // of top, then remove the top as well.
                // Left child of the top must have
                // processed before.
                while (st.length > 0 &&
                       st[st.length - 1].right == root)
                {
                    root = st[st.length - 1];
                    st.pop();
                }
            }

            // if stack is not empty then simply
            // set the root as right child of top
            // and start traversing right sub-tree.
            root = st.length == 0 ?
                            null : st[st.length - 1].right;
        }

        // If stack is not empty, print contents
        // of stack. Here assumption is that the
        // key is there in tree
        while (st.length > 0)
        {
            document.write(st[st.length - 1].data + " ");
            st.pop();
        }
    }

    // Let us construct a binary tree
    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.left.left.left = new Node(8);
    root.left.right.right = new Node(9);
    root.right.right.left = new Node(10);

    document.write("Following are all keys " +
                          "and their ancestors" + "</br>");
    for (let key = 1; key <= 10; key++)
    {
        document.write(key + ": ");
        printAncestors(root, key);
        document.write("</br>");
    }

// This code is contributed by decode2207.
</script>
```

**输出:**

```
Following are all keys and their ancestors
1:
2: 1
3: 1
4: 2 1
5: 2 1
6: 3 1
7: 3 1
8: 4 2 1
9: 5 2 1
10: 7 3 1
```

**练习**
注意，上面的解决方案假设给定的键存在于给定的二叉树中。如果密钥不存在，它可能会进入无限循环。扩展上述解决方案，即使密钥不在树中也能工作。
本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643?fref=ts) 控制。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。