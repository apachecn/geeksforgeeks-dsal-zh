# 检查给定的二叉树是否完整|集合 1(迭代解)

> 原文:[https://www . geeksforgeeks . org/check-if-a-给定-二叉树-complete-tree-or-not/](https://www.geeksforgeeks.org/check-if-a-given-binary-tree-is-complete-tree-or-not/)

给定一棵二叉树，写一个函数来检查给定的二叉树是否是完全二叉树。
一个[完整的二叉树](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)是一个二叉树，在这个二叉树中，除了可能的最后一级之外，每一级都被完全填充，所有的节点都尽可能的靠左。请参见以下示例。

```
The following trees are examples of Complete Binary Trees
    1
  /   \
 2     3

       1
    /    \
   2       3
  /
 4

       1
    /    \
   2      3
  /  \    /
 4    5  6
```

```
The following trees are examples of Non-Complete Binary Trees
    1
      \
       3

       1
    /    \
   2       3
    \     /  \   
     4   5    6

       1
    /    \
   2      3
         /  \
        4    5 
```

[级序遍历后](https://www.geeksforgeeks.org/level-order-tree-traversal/)的方法 2 可以很容易修改，检查一棵树是否完整。为了理解这种方法，让我们首先定义术语“完整节点”。如果左右子节点都不为空(或不为空)，则节点为“完整节点”。

方法是从根开始进行级别顺序遍历。在遍历中，一旦找到一个不是完整节点的节点，所有后面的节点都必须是叶节点。

另外，还需要检查一件事来处理下面的情况:如果一个节点有一个空的左子节点，那么右子节点必须是空的。

```
    1
  /   \
 2     3
  \
   4
```

感谢 Guddu Sharma 提出了这个简单高效的方法。

## C++

```
// C++ program to check if a given
// binary tree is complete or not
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* Given a binary tree, return
true if the tree is complete
else false */
bool isCompleteBT(node* root)
{
    // Base Case: An empty tree
    // is complete Binary Tree
    if (root == NULL)
        return true;

    // Create an empty queue
    //int rear, front;
    //node **queue = createQueue(&front, &rear);
    queue<node *> q;
    q.push(root);
    // Create a flag variable which will be set true
    // when a non full node is seen
    bool flag = false;

    // Do level order traversal using queue.
    //enQueue(queue, &rear, root);
    while(!q.empty())
    {
        node *temp =q.front();
        q.pop();

        /* Check if left child is present*/
        if(temp->left)
        {
        // If we have seen a non full node,
        // and we see a node with non-empty
        // left child, then the given tree is not
        // a complete Binary Tree
        if (flag == true)
            return false;

        q.push(temp->left);// Enqueue Left Child
        }
        else // If this a non-full node, set the flag as true
        flag = true;

        /* Check if right child is present*/
        if(temp->right)
        {
        // If we have seen a non full node,
        // and we see a node with non-empty
        // right child, then the given tree is not
        // a complete Binary Tree
        if(flag == true)
            return false;

        q.push(temp->right); // Enqueue Right Child
        }
        else // If this a non-full node, set the flag as true
        flag = true;
    }

    // If we reach here, then the
    // tree is complete Binary Tree
    return true;
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(
        sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

/* Driver code*/
int main()
{
    /* Let us construct the following Binary Tree which
        is not a complete Binary Tree
              1
            /  \
            2   3
           / \  /
          4   5 6
        */

    node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);

    if ( isCompleteBT(root) == true )
        cout << "Complete Binary Tree";
    else
        cout << "NOT Complete Binary Tree";

    return 0;
}

// This code is contributed by izuna_894
```

## C

```
// A program to check if a given binary tree is complete or not
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#define MAX_Q_SIZE 500

/* A binary tree node has data, a pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* function prototypes for functions needed for Queue data
   structure. A queue is needed for level order traversal */
struct node** createQueue(int *, int *);
void enQueue(struct node **, int *, struct node *);
struct node *deQueue(struct node **, int *);
bool isQueueEmpty(int *front, int *rear);

/* Given a binary tree, return true if the tree is complete
   else false */
bool isCompleteBT(struct node* root)
{
  // Base Case: An empty tree is complete Binary Tree
  if (root == NULL)
    return true;

  // Create an empty queue
  int rear, front;
  struct node **queue = createQueue(&front, &rear);

  // Create a flag variable which will be set true
  // when a non full node is seen
  bool flag = false;

  // Do level order traversal using queue.
  enQueue(queue, &rear, root);
  while(!isQueueEmpty(&front, &rear))
  {
    struct node *temp_node = deQueue(queue, &front);

    /* Check if left child is present*/
    if(temp_node->left)
    {
       // If we have seen a non full node, and we see a node
       // with non-empty left child, then the given tree is not
       // a complete Binary Tree
       if (flag == true)
         return false;

       enQueue(queue, &rear, temp_node->left);  // Enqueue Left Child
    }
    else // If this a non-full node, set the flag as true
       flag = true;

    /* Check if right child is present*/
    if(temp_node->right)
    {
       // If we have seen a non full node, and we see a node
       // with non-empty right child, then the given tree is not
       // a complete Binary Tree
       if(flag == true)
         return false;

       enQueue(queue, &rear, temp_node->right);  // Enqueue Right Child
    }
    else // If this a non-full node, set the flag as true
       flag = true;
  }

  // If we reach here, then the tree is complete Binary Tree
  return true;
}

/*UTILITY FUNCTIONS*/
struct node** createQueue(int *front, int *rear)
{
  struct node **queue =
   (struct node **)malloc(sizeof(struct node*)*MAX_Q_SIZE);

  *front = *rear = 0;
  return queue;
}

void enQueue(struct node **queue, int *rear, struct node *new_node)
{
  queue[*rear] = new_node;
  (*rear)++;
}

struct node *deQueue(struct node **queue, int *front)
{
  (*front)++;
  return queue[*front - 1];
}

bool isQueueEmpty(int *front, int *rear)
{
   return (*rear == *front);
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
  struct node* node = (struct node*)
                       malloc(sizeof(struct node));
  node->data = data;
  node->left = NULL;
  node->right = NULL;

  return(node);
}

/* Driver program to test above functions*/
int main()
{
   /* Let us construct the following Binary Tree which
      is not a complete Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    */

  struct node *root  = newNode(1);
  root->left         = newNode(2);
  root->right        = newNode(3);
  root->left->left   = newNode(4);
  root->left->right  = newNode(5);
  root->right->right = newNode(6);

  if ( isCompleteBT(root) == true )
      printf ("Complete Binary Tree");
  else
      printf ("NOT Complete Binary Tree");

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//A Java program to check if a given binary tree is complete or not

import java.util.LinkedList;
import java.util.Queue;

public class CompleteBTree
{
    /* A binary tree node has data, a pointer to left child
       and a pointer to right child */
    static class Node
    {
        int data;
        Node left;
        Node right;

        // Constructor
        Node(int d)
        {
            data = d;
            left = null;
            right = null;
        }
    }

    /* Given a binary tree, return true if the tree is complete
       else false */
    static boolean isCompleteBT(Node root)
    {
        // Base Case: An empty tree is complete Binary Tree
        if(root == null)
            return true;

        // Create an empty queue
        Queue<Node> queue =new LinkedList<>();

        // Create a flag variable which will be set true
        // when a non full node is seen
        boolean flag = false;

        // Do level order traversal using queue.
        queue.add(root);
        while(!queue.isEmpty())
        {
            Node temp_node = queue.remove();

            /* Check if left child is present*/
            if(temp_node.left != null)
            {
                 // If we have seen a non full node, and we see a node
                 // with non-empty left child, then the given tree is not
                 // a complete Binary Tree
                if(flag == true)
                    return false;

                 // Enqueue Left Child
                queue.add(temp_node.left);
            }
            // If this a non-full node, set the flag as true
            else
                flag = true;

            /* Check if right child is present*/
            if(temp_node.right != null)
            {
                // If we have seen a non full node, and we see a node
                // with non-empty right child, then the given tree is not
                // a complete Binary Tree
                if(flag == true)
                    return false;

                // Enqueue Right Child
                queue.add(temp_node.right);

            }
            // If this a non-full node, set the flag as true
            else
                flag = true;
        }
         // If we reach here, then the tree is complete Binary Tree
        return true;
    }

    /* Driver program to test above functions*/
    public static void main(String[] args)
    {

        /* Let us construct the following Binary Tree which
          is not a complete Binary Tree
                1
              /   \
             2     3
            / \     \
           4   5     6
        */

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(6);

        if(isCompleteBT(root) == true)
            System.out.println("Complete Binary Tree");
        else
            System.out.println("NOT Complete Binary Tree");
     }

}
//This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Check whether a binary tree is complete or not

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Given a binary tree, return true if the tree is complete
# else return false
def isCompleteBT(root):

    # Base Case: An empty tree is complete Binary tree
    if root is None:
        return True

    # Create an empty queue
    queue = []

    # Create a flag variable which will be set True
    # when a non-full node is seen
    flag = False

    # Do level order traversal using queue
    queue.append(root)
    while(len(queue) > 0):
        tempNode = queue.pop(0) # Dequeue

        # Check if left child is present
        if (tempNode.left):

            # If we have seen a non-full node, and we see
            # a node with non-empty left child, then the
            # given tree is not a complete binary tree
            if flag == True :
                return False

            # Enqueue left child
            queue.append(tempNode.left)

            # If this a non-full node, set the flag as true
        else:
            flag = True

        # Check if right child is present
        if(tempNode.right):

            # If we have seen a non full node, and we
            # see a node with non-empty right child, then
            # the given tree is not a compelete BT
            if flag == True:
                return False

            # Enqueue right child
            queue.append(tempNode.right)

        # If this is non-full node, set the flag as True
        else:
            flag = True

    # If we reach here, then the tree is complete BT
    return True

# Driver program to test above function

""" Let us construct the following Binary Tree which
      is not a complete Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    """
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.right = Node(6)

if (isCompleteBT(root)):
    print "Complete Binary Tree"
else:
    print "NOT Complete Binary Tree"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to check if a given
// binary tree is complete or not
using System;
using System.Collections.Generic;

public class CompleteBTree
{
    /* A binary tree node has data,
    pointer to left child and a
     pointer to right child */
    public class Node
    {
        public int data;
        public Node left;
        public Node right;

        // Constructor
        public Node(int d)
        {
            data = d;
            left = null;
            right = null;
        }
    }

    /* Given a binary tree, return
    true if the tree is complete
    else false */
    static bool isCompleteBT(Node root)
    {
        // Base Case: An empty tree
        // is complete Binary Tree
        if(root == null)
            return true;

        // Create an empty queue
        Queue<Node> queue = new Queue<Node>();

        // Create a flag variable which will be set true
        // when a non full node is seen
        bool flag = false;

        // Do level order traversal using queue.
        queue.Enqueue(root);
        while(queue.Count != 0)
        {
            Node temp_node = queue.Dequeue();

            /* Check if left child is present*/
            if(temp_node.left != null)
            {
                // If we have seen a non full node,
                // and we see a node with non-empty
                // left child, then the given tree is not
                // a complete Binary Tree
                if(flag == true)
                    return false;

                // Enqueue Left Child
                queue.Enqueue(temp_node.left);
            }

            // If this a non-full node, set the flag as true
            else
                flag = true;

            /* Check if right child is present*/
            if(temp_node.right != null)
            {
                // If we have seen a non full node,
                // and we see a node with non-empty
                // right child, then the given tree
                // is not a complete Binary Tree
                if(flag == true)
                    return false;

                // Enqueue Right Child
                queue.Enqueue(temp_node.right);

            }

            // If this a non-full node,
            // set the flag as true
            else
                flag = true;
        }

        // If we reach here, then the
        // tree is complete Binary Tree
        return true;
    }

    /* Driver code*/
    public static void Main()
    {

        /* Let us construct the following Binary Tree which
        is not a complete Binary Tree
                1
            / \
            2     3
            / \     \
        4 5     6
        */

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(6);

        if(isCompleteBT(root) == true)
            Console.WriteLine("Complete Binary Tree");
        else
            Console.WriteLine("NOT Complete Binary Tree");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to check if a given
// binary tree is complete or not

/* A binary tree node has data,
pointer to left child and a
 pointer to right child */
class Node
{
    // Constructor
    constructor(d)
    {
        this.data = d;
        this.left = null;
        this.right = null;
    }
}

/* Given a binary tree, return
true if the tree is complete
else false */
function isCompleteBT(root)
{
    // Base Case: An empty tree
    // is complete Binary Tree
    if(root == null)
        return true;

    // Create an empty queue
    var queue = [];

    // Create a flag variable which will be set true
    // when a non full node is seen
    var flag = false;

    // Do level order traversal using queue.
    queue.push(root);
    while(queue.length != 0)
    {
        var temp_node = queue.shift();

        /* Check if left child is present*/
        if(temp_node.left != null)
        {
            // If we have seen a non full node,
            // and we see a node with non-empty
            // left child, then the given tree is not
            // a complete Binary Tree
            if(flag == true)
                return false;

            // push Left Child
            queue.push(temp_node.left);
        }

        // If this a non-full node, set the flag as true
        else
            flag = true;

        /* Check if right child is present*/
        if(temp_node.right != null)
        {
            // If we have seen a non full node,
            // and we see a node with non-empty
            // right child, then the given tree
            // is not a complete Binary Tree
            if(flag == true)
                return false;

            // push Right Child
            queue.push(temp_node.right);

        }

        // If this a non-full node,
        // set the flag as true
        else
            flag = true;
    }

    // If we reach here, then the
    // tree is complete Binary Tree
    return true;
}

/* Driver code*/
/* Let us construct the following Binary Tree which
is not a complete Binary Tree
        1
    / \
    2     3
    / \     \
4 5     6
*/
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.right = new Node(6);

if(isCompleteBT(root) == true)
    document.write("Complete Binary Tree");
else
    document.write("NOT Complete Binary Tree");

</script>
```

**Output**

```
Complete Binary Tree
```

**时间复杂度:** O(n)其中 n 为给定二叉树中的节点数
T3】辅助空间: O(n)为队列。

**方法 2 :** 更简单的方法是检查遇到的空节点是否是二叉树的最后一个节点。如果在二叉树中遇到的空节点是最后一个节点，那么它就是一个完整的二叉树，如果即使在遇到空节点之后仍然存在一个有效的节点，那么这个树就不是一个完整的二叉树。

## C++

```
// C++ program to check if a given
// binary tree is complete or not
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* Given a binary tree, return
true if the tree is complete
else false */
bool isCompleteBT(node* root)
{
    // Base Case: An empty tree
    // is complete Binary Tree
    if (root == NULL)
        return true;

    // Create an empty queue
    queue<node *> q;
    q.push(root);
    // Create a flag variable which will be set true
    // when a non full node is seen
    bool flag = false;

    // Do level order traversal using queue.
    //enQueue(queue, &rear, root);
    while(!q.empty())
    {
        node *temp =q.front();
        q.pop();

        if(temp == NULL){
        // If we have seen a NULL node,
        // we set the flag to true
            flag = true ;
        }else{
            // If that NULL node
            // is not the last node
            // then return false
            if(flag == true){
                return false ;
            }
            // Push both nodes
            // even if there are null
            q.push(temp->left) ;           
            q.push(temp->right) ;
        }   
    }

    // If we reach here, then the
    // tree is complete Binary Tree
    return true;
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(
        sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

/* Driver code*/
int main()
{
    /* Let us construct the following Binary Tree which
        is not a complete Binary Tree
             1
            / \
            2   3
           / \  /
          4   5 6
        */

    struct node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);

    if ( isCompleteBT(root) == true )
        cout << "Complete Binary Tree";
    else
        cout << "NOT Complete Binary Tree";

    return 0;
}
```

**Output**

```
Complete Binary Tree
```

**时间复杂度** : O(n)，其中 n 是给定二叉树中的节点数

**辅助空间** : O(n)为队列。

如果您发现上述任何代码/算法不正确，请写下评论，或者找到其他方法来解决相同的问题。