# 迭代后序遍历|集合 2(使用一个堆栈)

> 原文:[https://www . geesforgeks . org/iterative-post-order-遍历-使用-stack/](https://www.geeksforgeeks.org/iterative-postorder-traversal-using-stack/)

在前一篇文章中，我们讨论了一个简单的[迭代后置遍历，使用了两个堆栈](https://www.geeksforgeeks.org/iterative-postorder-traversal/)。在这篇文章中，讨论了一种只有一个堆栈的方法。

想法是使用左指针向下移动到最左边的节点。向下移动时，将 root 和 root 的右子级推入堆栈。一旦我们到达最左边的节点，如果它没有合适的子节点，就打印它。如果它有一个正确的子对象，那么就要改变根对象，这样正确的子对象才会被处理。

下面是详细的算法。

```
1.1 Create an empty stack
2.1 Do following while root is not NULL
    a) Push root's right child and then root to stack.
    b) Set root as root's left child.
2.2 Pop an item from stack and set it as root.
    a) If the popped item has a right child and the right child 
       is at top of stack, then remove the right child from stack,
       push the root back and set root as root's right child.
    b) Else print root's data and set root as NULL.
2.3 Repeat steps 2.1 and 2.2 while stack is not empty.
```

让我们考虑下面的树

![](img/9a421706dfa118ae96184c178e32b4c9.png)

下面是使用一个堆栈打印上述树的后置遍历的步骤。

```
1\. Right child of 1 exists. 
   Push 3 to stack. Push 1 to stack. Move to left child.
        Stack: 3, 1

2\. Right child of 2 exists. 
   Push 5 to stack. Push 2 to stack. Move to left child.
        Stack: 3, 1, 5, 2

3\. Right child of 4 doesn't exist. '
   Push 4 to stack. Move to left child.
        Stack: 3, 1, 5, 2, 4

4\. Current node is NULL. 
   Pop 4 from stack. Right child of 4 doesn't exist. 
   Print 4\. Set current node to NULL.
        Stack: 3, 1, 5, 2

5\. Current node is NULL. 
    Pop 2 from stack. Since right child of 2 equals stack top element, 
    pop 5 from stack. Now push 2 to stack.     
    Move current node to right child of 2 i.e. 5
        Stack: 3, 1, 2

6\. Right child of 5 doesn't exist. Push 5 to stack. Move to left child.
        Stack: 3, 1, 2, 5

7\. Current node is NULL. Pop 5 from stack. Right child of 5 doesn't exist. 
   Print 5\. Set current node to NULL.
        Stack: 3, 1, 2

8\. Current node is NULL. Pop 2 from stack. 
   Right child of 2 is not equal to stack top element. 
   Print 2\. Set current node to NULL.
        Stack: 3, 1

9\. Current node is NULL. Pop 1 from stack. 
   Since right child of 1 equals stack top element, pop 3 from stack. 
   Now push 1 to stack. Move current node to right child of 1 i.e. 3
        Stack: 1

10\. Repeat the same as above steps and Print 6, 7 and 3\. 
    Pop 1 and Print 1.
```

## C

```
// C program for iterative postorder traversal using one stack
#include <stdio.h>
#include <stdlib.h>

// Maximum stack size
#define MAX_SIZE 100

// A tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Stack type
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
{ return stack->top - 1 == stack->size; }

int isEmpty(struct Stack* stack)
{ return stack->top == -1; }

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

// An iterative function to do postorder traversal of a given binary tree
void postOrderIterative(struct Node* root)
{
    // Check for empty tree
    if (root == NULL)
        return;

    struct Stack* stack = createStack(MAX_SIZE);
    do
    {
        // Move to leftmost node
        while (root)
        {
            // Push root's right child and then root to stack.
            if (root->right)
                push(stack, root->right);
            push(stack, root);

            // Set root as root's left child
            root = root->left;
        }

        // Pop an item from stack and set it as root    
        root = pop(stack);

        // If the popped item has a right child and the right child is not
        // processed yet, then make sure right child is processed before root
        if (root->right && peek(stack) == root->right)
        {
            pop(stack); // remove right child from stack
            push(stack, root); // push root back to stack
            root = root->right; // change root so that the right
                                // child is processed next
        }
        else // Else print root's data and set root as NULL
        {
            printf("%d ", root->data);
            root = NULL;
        }
    } while (!isEmpty(stack));
}

// Driver program to test above functions
int main()
{
    // Let us construct the tree shown in above figure
    struct Node* root = NULL;
    root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    printf("Post order traversal of binary tree is :\n");
    printf("[");
    postOrderIterative(root);
    printf("]");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A java program for iterative postorder traversal using stack

import java.util.ArrayList;
import java.util.Stack;

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right;
    }
}

class BinaryTree
{
    Node root;
    ArrayList<Integer> list = new ArrayList<Integer>();

    // An iterative function to do postorder traversal
    // of a given binary tree
    ArrayList<Integer> postOrderIterative(Node node)
    {
        Stack<Node> S = new Stack<Node>();

        // Check for empty tree
        if (node == null)
            return list;
        S.push(node);
        Node prev = null;
        while (!S.isEmpty())
        {
            Node current = S.peek();

            /* go down the tree in search of a leaf an if so process it
            and pop stack otherwise move down */
            if (prev == null || prev.left == current ||
                                        prev.right == current)
            {
                if (current.left != null)
                    S.push(current.left);
                else if (current.right != null)
                    S.push(current.right);
                else
                {
                    S.pop();
                    list.add(current.data);
                }

                /* go up the tree from left node, if the child is right
                push it onto stack otherwise process parent and pop
                stack */
            }
            else if (current.left == prev)
            {
                if (current.right != null)
                    S.push(current.right);
                else
                {
                    S.pop();
                    list.add(current.data);
                }

                /* go up the tree from right node and after coming back
                from right node process parent and pop stack */
            }
            else if (current.right == prev)
            {
                S.pop();
                list.add(current.data);
            }

            prev = current;
        }

        return list;
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
    BinaryTree tree = new BinaryTree();

        // Let us create trees shown in above diagram
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);

        ArrayList<Integer> mylist = tree.postOrderIterative(tree.root);

        System.out.println("Post order traversal of binary tree is :");
        System.out.println(mylist);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program for iterative postorder traversal
# using one stack

# Stores the answer
ans = []

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def peek(stack):
    if len(stack) > 0:
        return stack[-1]
    return None
# A iterative function to do postorder traversal of
# a given binary tree
def postOrderIterative(root):

    # Check for empty tree
    if root is None:
        return

    stack = []

    while(True):

        while (root):
            # Push root's right child and then root to stack
            if root.right is not None:
                stack.append(root.right)
            stack.append(root)

            # Set root as root's left child
            root = root.left

        # Pop an item from stack and set it as root
        root = stack.pop()

        # If the popped item has a right child and the
        # right child is not processed yet, then make sure
        # right child is processed before root
        if (root.right is not None and
            peek(stack) == root.right):
            stack.pop() # Remove right child from stack
            stack.append(root) # Push root back to stack
            root = root.right # change root so that the
                            # right childis processed next

        # Else print root's data and set root as None
        else:
            ans.append(root.data)
            root = None

        if (len(stack) <= 0):
                break

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)

print("Post Order traversal of binary tree is")
postOrderIterative(root)
print(ans)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// A C# program for iterative postorder traversal using stack
using System;
using System.Collections.Generic;

// A binary tree node
class Node
{
  public int data;
  public Node left, right;

  public Node(int item)
  {
    data = item;
    left = right;
  }
}

public class BinaryTree
{
  Node root;
  List<int> list = new List<int>();

  // An iterative function to do postorder traversal
  // of a given binary tree
  List<int> postOrderIterative(Node node)
  {
    Stack<Node> S = new Stack<Node>();

    // Check for empty tree
    if (node == null)
      return list;
    S.Push(node);
    Node prev = null;
    while (S.Count != 0)
    {
      Node current = S.Peek();

      /* go down the tree in search of a leaf an if so process it
            and pop stack otherwise move down */
      if (prev == null || prev.left == current ||
          prev.right == current)
      {
        if (current.left != null)
          S.Push(current.left);
        else if (current.right != null)
          S.Push(current.right);
        else
        {
          S.Pop();
          list.Add(current.data);
        }

        /* go up the tree from left node, if the child is right
                push it onto stack otherwise process parent and pop
                stack */
      }
      else if (current.left == prev)
      {
        if (current.right != null)
          S.Push(current.right);
        else
        {
          S.Pop();
          list.Add(current.data);
        }

        /* go up the tree from right node and after coming back
                from right node process parent and pop stack */
      }
      else if (current.right == prev)
      {
        S.Pop();
        list.Add(current.data);
      }

      prev = current;
    }

    return list;
  }

  // Driver code
  public static void Main(String []args)
  {
    BinaryTree tree = new BinaryTree();

    // Let us create trees shown in above diagram
    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);
    tree.root.left.left = new Node(4);
    tree.root.left.right = new Node(5);
    tree.root.right.left = new Node(6);
    tree.root.right.right = new Node(7);

    List<int> mylist = tree.postOrderIterative(tree.root);

    Console.WriteLine("Post order traversal of binary tree is :");
    foreach(int i in mylist)
      Console.Write(i+" ");
  }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// A javascript program for iterative postorder traversal using stack

// A binary tree node
    class Node
    {
        constructor(item)
        {
            this.data=item;
            this.left=null;
            this.right=null;
        }
    }

    let root;
    let list = [];

    // An iterative function to do postorder traversal
    // of a given binary tree
    function postOrderIterative(node)
    {
        let S = [];
        // Check for empty tree
        if (node == null)
            return list;
        S.push(node);
        let prev = null;
        while (S.length!=0)
        {
            let current = S[S.length-1];

            /* go down the tree in search of a leaf an if so process it
            and pop stack otherwise move down */
            if (prev == null || prev.left == current ||
                                        prev.right == current)
            {
                if (current.left != null)
                    S.push(current.left);
                else if (current.right != null)
                    S.push(current.right);
                else
                {
                    S.pop();
                    list.push(current.data);
                }

                /* go up the tree from left node, if the child is right
                push it onto stack otherwise process parent and pop
                stack */
            }
            else if (current.left == prev)
            {
                if (current.right != null)
                    S.push(current.right);
                else
                {
                    S.pop();
                    list.push(current.data);
                }

                /* go up the tree from right node and after coming back
                from right node process parent and pop stack */
            }
            else if (current.right == prev)
            {
                S.pop();
                list.push(current.data);
            }

            prev = current;
        }

        return list;
    }

    // Driver program to test above functions

    // Let us create trees shown in above diagram
    root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);

    let mylist = postOrderIterative(root);
    document.write("Post order traversal of binary tree is :<br>");
    for(let i = 0; i < mylist.length; i++)
    {
        document.write(mylist[i]+" ");
    }

    // This code is contributed by unknown2108
</script>
```

**Output**

```
Post order traversal of binary tree is :
[4 5 2 6 7 3 1 ]
```

**方法二:**
向左遍历的同时直接推根节点两次。当弹出时，如果你发现栈顶()与根相同，那么去找根- >右，否则打印根。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to print PostOrder Traversal(Iterative)
import java.util.Stack;

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right;
    }
}

// create a postorder class
class PostOrder
{
    Node root;

    // An iterative function to do postorder traversal
    // of a given binary tree
    private void postOrderIterative(Node root) {
        Stack<Node> stack = new Stack<>();
        while(true) {
            while(root != null) {
                stack.push(root);
                stack.push(root);
                root = root.left;
            }

            // Check for empty stack
            if(stack.empty()) return;
            root = stack.pop();

            if(!stack.empty() && stack.peek() == root) root = root.right;

            else {

                System.out.print(root.data + " "); root = null;
            }
        }
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
    PostOrder tree = new PostOrder();

        // Let us create trees shown in above diagram
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        System.out.println("Post order traversal of binary tree is :");
        tree.postOrderIterative(tree.root);
    }
}
```

## 蟒蛇 3

```
# Simple Python3 program to print
# PostOrder Traversal(Iterative)

# A binary tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.right = None
        self.left = None

# Create a postorder class

# An iterative function to do postorder
# traversal of a given binary tree
def postOrderIterative(root):

    stack = []

    while(True):
        while(root != None):
            stack.append(root)
            stack.append(root)
            root = root.left

        # Check for empty stack
        if (len(stack) == 0):
            return

        root = stack.pop()

        if (len(stack) > 0 and stack[-1] == root):
            root = root.right
        else:
            print(root.data, end = " ")
            root = None

# Driver code
if __name__ == '__main__':

    # Let us create trees shown
    # in above diagram
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)

    print("Post order traversal of binary tree is :")

    postOrderIterative(root)

# This code is contributed by mohit kumar 29
```

## C#

```
// Simple C# program to print PostOrder Traversal(Iterative)
using System;
using System.Collections.Generic;

// A binary tree node
public
  class Node
  {
    public
      int data;
    public
      Node left, right;
    public
      Node(int item)
    {
      data = item;
      left = right;
    }
  }

// create a postorder class
public class PostOrder
{
  Node root;

  // An iterative function to do postorder traversal
  // of a given binary tree
  private void postOrderIterative(Node root)
  {
    Stack<Node> stack = new Stack<Node>();
    while(true)
    {
      while(root != null)
      {
        stack.Push(root);
        stack.Push(root);
        root = root.left;
      }

      // Check for empty stack
      if(stack.Count == 0) return;
      root = stack.Pop();        
      if(stack.Count != 0 && stack.Peek() == root) root = root.right;           
      else
      {              
        Console.Write(root.data + " "); root = null;
      }
    }
  }

  // Driver program to test above functions
  public static void Main(String []args)
  {
    PostOrder tree = new PostOrder();

    // Let us create trees shown in above diagram
    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);
    tree.root.left.left = new Node(4);
    tree.root.left.right = new Node(5);
    tree.root.right.left = new Node(6);
    tree.root.right.right = new Node(7);
    Console.WriteLine("Post order traversal of binary tree is :");
    tree.postOrderIterative(tree.root);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // Simple JavaScript program to print
      // PostOrder Traversal(Iterative)

      // A binary tree node
      class Node {
        constructor(item) {
          this.data = item;
          this.left = null;
          this.right = null;
        }
      }

      // create a postorder class
      class PostOrder {
        constructor() {
          this.root = null;
        }
        // An iterative function to do postorder traversal
        // of a given binary tree
        postOrderIterative(root) {
          var stack = [];
          while (true) {
            while (root != null) {
              stack.push(root);
              stack.push(root);
              root = root.left;
            }

            // Check for empty stack
            if (stack.length == 0) return;
            root = stack.pop();
            if (stack.length != 0 && stack[stack.length - 1] == root)
              root = root.right;
            else {
              document.write(root.data + " ");
              root = null;
            }
          }
        }
      }
      // Driver program to test above functions
      var tree = new PostOrder();

      // Let us create trees shown in above diagram
      tree.root = new Node(1);
      tree.root.left = new Node(2);
      tree.root.right = new Node(3);
      tree.root.left.left = new Node(4);
      tree.root.left.right = new Node(5);
      tree.root.right.left = new Node(6);
      tree.root.right.right = new Node(7);
      document.write("Post order traversal of binary tree is :<br>");
      tree.postOrderIterative(tree.root);

</script>
```

**Output**

```
Post order traversal of binary tree is :
4 5 2 6 7 3 1 
```

本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish?fref=ts)编辑。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息