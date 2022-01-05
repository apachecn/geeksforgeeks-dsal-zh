# 为所有节点填充有序后继节点

> 原文:[https://www . geeksforgeeks . org/populate-in order-后继者 for all-nodes/](https://www.geeksforgeeks.org/populate-inorder-successor-for-all-nodes/)

给定一个二叉树，其中每个节点具有以下结构，编写一个函数来填充所有节点的下一个指针。每个节点的下一个指针应该设置为指向下一个后继节点。

## C++

```
class node
{
    public:
    int data;
    node *left;
    node *right;
    node *next;
};

// This code is contributed
// by Shubham Singh
```

## C

```
struct node
{
  int data;
  struct node* left;
  struct node* right;
  struct node* next;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A binary tree node
class Node
{
    int data;
    Node left, right, next;

    Node(int item)
    {
        data = item;
        left = right = next = null;
    }
}

// This code is contributed by SUBHAMSINGH10.
```

## 蟒蛇 3

```
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.next = None

# This code is contributed by Shubham Singh
```

## C#

```
class Node
{
   public int data;
   public Node left, right, next;

  public Node(int item)
 {
      data = item;
      left = right = next = null;
  }
}
Node root;

// This code is contributed
// by Shubham Singh
```

最初，所有下一个指针都有空值。您的函数应该填充这些下一个指针，以便它们指向更高级的后继函数。

**解决方案(使用反向有序遍历)**
以反向有序遍历的方式遍历给定的树，并跟踪以前访问过的节点。当一个节点被访问时，分配一个先前访问过的节点作为下一个。

## C++

```
// C++ program to populate inorder
// traversal of all nodes
#include<bits/stdc++.h>
using namespace std;

class node
{
    public:
    int data;
    node *left;
    node *right;
    node *next;
};

/* Set next of p and all descendants of p
by traversing them in reverse Inorder */
void populateNext(node* p)
{
    // The first visited node will be the
    // rightmost node next of the rightmost
    // node will be NULL
    static node *next = NULL;

    if (p)
    {
        // First set the next pointer
        // in right subtree
        populateNext(p->right);

        // Set the next as previously visited
        // node in reverse Inorder
        p->next = next;

        // Change the prev for subsequent node
        next = p;

        // Finally, set the next pointer in
        // left subtree
        populateNext(p->left);
    }
}

/* UTILITY FUNCTIONS */
/* Helper function that allocates a new
node with the given data and NULL left
and right pointers. */
node* newnode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;
    Node->next = NULL;

    return(Node);
}

// Driver Code
int main()
{

    /* Constructed binary tree is
            10
            / \
        8 12
        /
    3
    */
    node *root = newnode(10);
    root->left = newnode(8);
    root->right = newnode(12);
    root->left->left = newnode(3);

    // Populates nextRight pointer in all nodes
    populateNext(root);

    // Let us see the populated values
    node *ptr = root->left->left;
    while(ptr)
    {
        // -1 is printed if there is no successor
        cout << "Next of " << ptr->data << " is "
             << (ptr->next? ptr->next->data: -1)
             << endl;
        ptr = ptr->next;
    }

    return 0;
}

// This code is contributed by rathbhupendra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to populate inorder traversal of all nodes

// A binary tree node
class Node
{
    int data;
    Node left, right, next;

    Node(int item)
    {
        data = item;
        left = right = next = null;
    }
}

class BinaryTree
{
    Node root;
    static Node next = null;

    /* Set next of p and all descendants of p by traversing them in
       reverse Inorder */
    void populateNext(Node node)
    {
        // The first visited node will be the rightmost node
        // next of the rightmost node will be NULL
        if (node != null)
        {
            // First set the next pointer in right subtree
            populateNext(node.right);

            // Set the next as previously visited node in reverse Inorder
            node.next = next;

            // Change the prev for subsequent node
            next = node;

            // Finally, set the next pointer in left subtree
            populateNext(node.left);
        }
    }

    /* Driver program to test above functions*/
    public static void main(String args[])
    {
        /* Constructed binary tree is
            10
           /   \
          8      12
         /
        3    */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(12);
        tree.root.left.left = new Node(3);

        // Populates nextRight pointer in all nodes
        tree.populateNext(tree.root);

        // Let us see the populated values
        Node ptr = tree.root.left.left;
        while (ptr != null)
        {
            // -1 is printed if there is no successor
            int print = ptr.next != null ? ptr.next.data : -1;
            System.out.println("Next of " + ptr.data + " is: " + print);
            ptr = ptr.next;
        }
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to populate
# inorder traversal of all nodes

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.next = None

# The first visited node will be
# the rightmost node next of the
# rightmost node will be None
next = None

# Set next of p and all descendants of p
# by traversing them in reverse Inorder
def populateNext(p):

    global next

    if (p != None):

        # First set the next pointer
        # in right subtree
        populateNext(p.right)

        # Set the next as previously visited node
        # in reverse Inorder
        p.next = next

        # Change the prev for subsequent node
        next = p

        # Finally, set the next pointer
        # in left subtree
        populateNext(p.left)

# UTILITY FUNCTIONS
# Helper function that allocates
# a new node with the given data
# and None left and right pointers.
def newnode(data):

    node = Node(0)
    node.data = data
    node.left = None
    node.right = None
    node.next = None

    return(node)

# Driver Code

# Constructed binary tree is
#         10
#     / \
#     8     12
# /
# 3
root = newnode(10)
root.left = newnode(8)
root.right = newnode(12)
root.left.left = newnode(3)

# Populates nextRight pointer
# in all nodes
p = populateNext(root)

# Let us see the populated values
ptr = root.left.left
while(ptr != None):

    out = 0
    if(ptr.next != None):
        out = ptr.next.data
    else:
        out = -1

    # -1 is printed if there is no successor
    print("Next of", ptr.data, "is", out)
    ptr = ptr.next

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to populate inorder traversal of all nodes
using System;

class BinaryTree
{
    // A binary tree node
    class Node
    {
       public int data;
       public Node left, right, next;

      public Node(int item)
     {
          data = item;
          left = right = next = null;
      }
    }
    Node root;
    static Node next = null;

    /* Set next of p and all descendants of p by traversing them in
       reverse Inorder */
    void populateNext(Node node)
    {
        // The first visited node will be the rightmost node
        // next of the rightmost node will be NULL
        if (node != null)
        {
            // First set the next pointer in right subtree
            populateNext(node.right);

            // Set the next as previously visited node in reverse Inorder
            node.next = next;

            // Change the prev for subsequent node
            next = node;

            // Finally, set the next pointer in left subtree
            populateNext(node.left);
        }
    }

    /* Driver program to test above functions*/
     static public void Main(String []args )
    {
        /* Constructed binary tree is
            10
           /   \
          8      12
         /
        3    */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(12);
        tree.root.left.left = new Node(3);

        // Populates nextRight pointer in all nodes
        tree.populateNext(tree.root);

        // Let us see the populated values
        Node ptr = tree.root.left.left;
        while (ptr != null)
        {
            // -1 is printed if there is no successor
            int print = ptr.next != null ? ptr.next.data : -1;
            Console.WriteLine("Next of " + ptr.data + " is: " + print);
            ptr = ptr.next;
        }
    }
}

// This code has been contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript program to populate inorder traversal of all nodes

    // A binary tree node
    class Node
    {

        constructor(x) {
            this.data = x;
            this.left = null;
            this.right = null;
          }
    }

    let root;
    let next = null;

    /* Set next of p and all descendants of p by traversing them in
       reverse Inorder */
    function populateNext(node)
    {
        // The first visited node will be the rightmost node
        // next of the rightmost node will be NULL
        if (node != null)
        {
            // First set the next pointer in right subtree
            populateNext(node.right);

            // Set the next as previously visited node in reverse Inorder
            node.next = next;

            // Change the prev for subsequent node
            next = node;

            // Finally, set the next pointer in left subtree
            populateNext(node.left);
        }
    }

    /* Driver program to test above functions*/

    /* Constructed binary tree is
            10
           /   \
          8      12
         /
        3    */
    root = new Node(10)
    root.left = new Node(8)
    root.right = new Node(12)
    root.left.left = new Node(3)

    // Populates nextRight pointer
    // in all nodes
    p = populateNext(root)

    // Let us see the populated values
    ptr = root.left.left

    while (ptr != null)
        {
            // -1 is printed if there is no successor
            let print = ptr.next != null ? ptr.next.data : -1;
            document.write("Next of " + ptr.data + " is: " + print+"<br>");
            ptr = ptr.next;
        }

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
Next of 3 is 8
Next of 8 is 10
Next of 10 is 12
Next of 12 is -1
```

我们可以通过将对 next 的引用作为参数传递来避免使用静态变量。

## C++

```
// An implementation that doesn't use static variable

// A wrapper over populateNextRecur
void populateNext(node *root)
{
    // The first visited node will be the rightmost node
    // next of the rightmost node will be NULL
    node *next = NULL;

    populateNextRecur(root, &next);
}

/* Set next of all descendants of p by
traversing them in reverse Inorder */
void populateNextRecur(node* p, node **next_ref)
{
    if (p)
    {
        // First set the next pointer in right subtree
        populateNextRecur(p->right, next_ref);

        // Set the next as previously visited
        // node in reverse Inorder
        p->next = *next_ref;

        // Change the prev for subsequent node
        *next_ref = p;

        // Finally, set the next pointer in right subtree
        populateNextRecur(p->left, next_ref);
    }
}

// This is code is contributed by rathbhupendra
```

## C

```
// An implementation that doesn't use static variable

// A wrapper over populateNextRecur
void populateNext(struct node *root)
{
    // The first visited node will be the rightmost node
    // next of the rightmost node will be NULL
    struct node *next = NULL;

    populateNextRecur(root, &next);
}

/* Set next of all descendants of p by traversing them in reverse Inorder */
void populateNextRecur(struct node* p, struct node **next_ref)
{
    if (p)
    {
        // First set the next pointer in right subtree
        populateNextRecur(p->right, next_ref);

        // Set the next as previously visited node in reverse Inorder
        p->next = *next_ref;

        // Change the prev for subsequent node
        *next_ref = p;

        // Finally, set the next pointer in right subtree
        populateNextRecur(p->left, next_ref);
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A wrapper over populateNextRecur
    void populateNext(Node node) {

        // The first visited node will be the rightmost node
        // next of the rightmost node will be NULL
        populateNextRecur(node, next);
    }

    /* Set next of all descendants of p by traversing them in reverse Inorder */
    void populateNextRecur(Node p, Node next_ref) {
        if (p != null) {

           // First set the next pointer in right subtree
            populateNextRecur(p.right, next_ref);

            // Set the next as previously visited node in reverse Inorder
            p.next = next_ref;

            // Change the prev for subsequent node
            next_ref = p;

            // Finally, set the next pointer in right subtree
            populateNextRecur(p.left, next_ref);
        }
    }
```

## 蟒蛇 3

```
# A wrapper over populateNextRecur
def populateNext(node):

    # The first visited node will be the rightmost node
    # next of the rightmost node will be NULL
    populateNextRecur(node, next)

# /* Set next of all descendants of p by
# traversing them in reverse Inorder */
def populateNextRecur(p, next_ref):

    if (p != None):

        # First set the next pointer in right subtree
        populateNextRecur(p.right, next_ref)

        # Set the next as previously visited node in reverse Inorder
        p.next = next_ref

        # Change the prev for subsequent node
        next_ref = p

        # Finally, set the next pointer in right subtree
        populateNextRecur(p.left, next_ref)

# This code is contributed by Mohit kumar 29
```

## C#

```
    // A wrapper over populateNextRecur
    void populateNext(Node node)
    {

        // The first visited node will be the rightmost node
        // next of the rightmost node will be NULL
        populateNextRecur(node, next);
    }

    /* Set next of all descendants of p by
    traversing them in reverse Inorder */
    void populateNextRecur(Node p, Node next_ref)
    {
        if (p != null)
        {

            // First set the next pointer in right subtree
            populateNextRecur(p.right, next_ref);

            // Set the next as previously visited node in reverse Inorder
            p.next = next_ref;

            // Change the prev for subsequent node
            next_ref = p;

            // Finally, set the next pointer in right subtree
            populateNextRecur(p.left, next_ref);
        }
    }

// This code is contributed by princiraj1992
```

## java 描述语言

```
<script>

// A wrapper over populateNextRecur
function populateNext(node)
{
    // The first visited node will be the rightmost node
    // next of the rightmost node will be NULL
    populateNextRecur(node, next);
}

/* Set next of all descendants of p by
traversing them in reverse Inorder */
function populateNextRecur(p, next_ref)
{
    if (p != null)
    {

        // First set the next pointer in right subtree
        populateNextRecur(p.right, next_ref);

        // Set the next as previously visited node in reverse Inorder
        p.next = next_ref;

        // Change the prev for subsequent node
        next_ref = p;

        // Finally, set the next pointer in right subtree
        populateNextRecur(p.left, next_ref);
    }
}

// This code is contributed by importantly.
</script>
```

**时间复杂度:** O(n)

**<u>进场:</u>**

**步骤:**

1.  创建数组或数组列表。
2.  将二叉树的有序遍历存储到数组列表中(存储节点)。
3.  现在遍历数组，并将节点的下一个指针替换为紧挨着右边的节点(数组中的下一个元素，它是所需的有序后继元素)。

```
    list.get(i).next = list.get(i+1)
```

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.ArrayList;

//class Node
class Node{
    int data;
    Node left,right,next;

    //constructor for initializing key value and all the
    //pointers
    Node(int data){
        this.data = data;
        left = right = next = null;
    }
}

public class Solution {
    Node root = null;

    //list to store inorder sequence
    ArrayList<Node> list = new ArrayList<>();

    //function for populating next pointer to inorder successor
    void populateNext() {

        //list = [3,8,10,12]

        //inorder successor of the present node is the immediate
        //right node
        //foe ex: inorder successor of 3 is 8
        for(int i=0;i<list.size();i++) {
            //check if it is the last node
            //point next of last node(right most) to null
            if(i != list.size()-1) {
                list.get(i).next = list.get(i+1);
            }
            else {
                list.get(i).next = null;
            }
        }

        // Let us see the populated values
        Node ptr = root.left.left;
        while (ptr != null)
        {
            // -1 is printed if there is no successor
            int print = ptr.next != null ? ptr.next.data : -1;
            System.out.println("Next of " + ptr.data + " is: " + print);
            ptr = ptr.next;
        }
    }

    //insert the inorder into a list to keep track
    //of the inorder successor
    void inorder(Node root) {
        if(root!=null) {
            inorder(root.left);
            list.add(root);
            inorder(root.right);
        }
    }

    //Driver function
    public static void main(String args[]) {
        Solution tree = new Solution();

        /*         10
               /   \
              8      12
             /
            3                */
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(12);
        tree.root.left.left = new Node(3);

        //function calls
        tree.inorder(tree.root);
        tree.populateNext();
    }
}
```

## C#

```
using System;
using System.Collections.Generic;

// class Node
public
 class Node {
    public

 int data;
    public

 Node left, right, next;

    // constructor for initializing key value and all the
    // pointers
    public

 Node(int data) {
        this.data = data;
        left = right = next = null;
    }
}

public class Solution {
    Node root = null;

    // list to store inorder sequence
    List<Node> list = new List<Node>();

    // function for populating next pointer to inorder successor
    void populateNext() {

        // list = [3,8,10,12]

        // inorder successor of the present node is the immediate
        // right node
        // foe ex: inorder successor of 3 is 8
        for (int i = 0; i < list.Count; i++) {
            // check if it is the last node
            // point next of last node(right most) to null
            if (i != list.Count - 1) {
                list[i].next = list[i + 1];
            } else {
                list[i].next = null;
            }
        }

        // Let us see the populated values
        Node ptr = root.left.left;
        while (ptr != null) {
            // -1 is printed if there is no successor
            int print = ptr.next != null ? ptr.next.data : -1;
            Console.WriteLine("Next of " + ptr.data + " is: " + print);
            ptr = ptr.next;
        }
    }

    // insert the inorder into a list to keep track
    // of the inorder successor
    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            list.Add(root);
            inorder(root.right);
        }
    }

    // Driver function
    public static void Main(String []args) {
        Solution tree = new Solution();

        /*
         * 10 / \ 8 12 / 3
         */
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(12);
        tree.root.left.left = new Node(3);

        // function calls
        tree.inorder(tree.root);
        tree.populateNext();
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// class Node
class Node
{
    // constructor for initializing key value and all the
    // pointers
    constructor(data)
    {
        this.data = data;
        this.left = this.right = this.next = null;
    }
}

let root = null;

// list to store inorder sequence
let list = [];

// function for populating next pointer to inorder successor
function populateNext()
{
    // list = [3,8,10,12]

        // inorder successor of the present node is the immediate
        // right node
        // foe ex: inorder successor of 3 is 8
        for(let i = 0; i < list.length; i++)
        {
            // check if it is the last node
            // point next of last node(right most) to null
            if(i != list.length - 1)
            {
                list[i].next = list[i + 1];
            }
            else {
                list[i].next = null;
            }
        }

        // Let us see the populated values
        let ptr = root.left.left;
        while (ptr != null)
        {

            // -1 is printed if there is no successor
            let print = ptr.next != null ? ptr.next.data : -1;
            document.write("Next of " + ptr.data + " is: " + print+"<br>");
            ptr = ptr.next;
        }
}

// insert the inorder into a list to keep track
// of the inorder successor
function inorder(root)
{
    if(root != null)
    {
            inorder(root.left);
            list.push(root);
            inorder(root.right);
        }
}

// Driver function

/*         10
               /   \
              8      12
             /
            3                */
root = new Node(10);
root.left = new Node(8);
root.right = new Node(12);
root.left.left = new Node(3);

// function calls
inorder(root);
populateNext();

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Next of 3 is: 8
Next of 8 is: 10
Next of 10 is: 12
Next of 12 is: -1
```