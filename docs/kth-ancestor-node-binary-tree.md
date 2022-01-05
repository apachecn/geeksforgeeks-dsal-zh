# 二叉树中节点的第 K 个祖先

> 原文:[https://www . geesforgeks . org/kth-祖先-节点-二叉树/](https://www.geeksforgeeks.org/kth-ancestor-node-binary-tree/)

给定一棵二叉树，其中节点的编号从 1 到 n。给定一个节点和一个正整数 K。我们必须打印二叉树中给定节点的第 K 个祖先。如果不存在任何这样的祖先，那么打印-1。
例如，在下面给出的二叉树中，节点 4 和 5 的第二个祖先是 1。节点 4 的第三个祖先将是-1。

![](img/7f3dedd212126dc478d65c331a09b2a9.png)

这样做的想法是首先遍历二叉树，并将每个节点的祖先存储在一个大小为 n 的数组中。例如，假设该数组是一个控制器[n]。然后在索引 I 处，祖先[i]将存储第 I 个节点的祖先。所以，ith node 的第二个祖先将是祖先[祖先[i]]等等。我们将使用这个想法来计算给定节点的第 k 个祖先。我们可以使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)来填充这个祖先数组。

以下是上述想法的实现。

## C++

```
/* C++ program to calculate Kth ancestor of given node */
#include <iostream>
#include <queue>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// function to generate array of ancestors
void generateArray(Node *root, int ancestors[])
{
    // There will be no ancestor of root node
    ancestors[root->data] = -1;

    // level order traversal to
    // generate 1st ancestor
    queue<Node*> q;
    q.push(root);

    while(!q.empty())
    {
        Node* temp  = q.front();
        q.pop();

        if (temp->left)
        {
            ancestors[temp->left->data] = temp->data;
            q.push(temp->left);
        }

        if (temp->right)
        {
            ancestors[temp->right->data] = temp->data;
            q.push(temp->right);
        }
    }
}

// function to calculate Kth ancestor
int kthAncestor(Node *root, int n, int k, int node)
{
    // create array to store 1st ancestors
    int ancestors[n+1] = {0};

    // generate first ancestor array
    generateArray(root,ancestors);

    // variable to track record of number of
    // ancestors visited
    int count = 0;

    while (node!=-1)
    {  
        node = ancestors[node];
        count++;

        if(count==k)
            break;
    }

    // print Kth ancestor
    return node;
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree shown in above diagram
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    int k = 2;
    int node = 5;

    // print kth ancestor of given node
    cout<<kthAncestor(root,5,k,node);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to calculate Kth ancestor of given node */
import java.util.*;
class GfG {
// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
}

// function to generate array of ancestors
static void generateArray(Node root, int ancestors[])
{
    // There will be no ancestor of root node
    ancestors[root.data] = -1;

    // level order traversal to
    // generate 1st ancestor
    Queue<Node> q = new LinkedList<Node> ();
    q.add(root);

    while(!q.isEmpty())
    {
        Node temp = q.peek();
        q.remove();

        if (temp.left != null)
        {
            ancestors[temp.left.data] = temp.data;
            q.add(temp.left);
        }

        if (temp.right != null)
        {
            ancestors[temp.right.data] = temp.data;
            q.add(temp.right);
        }
    }
}

// function to calculate Kth ancestor
static int kthAncestor(Node root, int n, int k, int node)
{
    // create array to store 1st ancestors
    int ancestors[] = new int[n + 1];

    // generate first ancestor array
    generateArray(root,ancestors);

    // variable to track record of number of
    // ancestors visited
    int count = 0;

    while (node!=-1)
    {
        node = ancestors[node];
        count++;

        if(count==k)
            break;
    }

    // print Kth ancestor
    return node;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver program to test above functions
public static void main(String[] args)
{
    // Let us create binary tree shown in above diagram
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    int k = 2;
    int node = 5;

    // print kth ancestor of given node
    System.out.println(kthAncestor(root,5,k,node));
}
}
```

## 蟒蛇 3

```
"""Python3 program to calculate Kth ancestor
   of given node """

# A Binary Tree Node
# Utility function to create a new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to generate array of ancestors
def generateArray(root, ancestors):

    # There will be no ancestor of root node
    ancestors[root.data] = -1

    # level order traversal to
    # generate 1st ancestor
    q = []
    q.append(root)

    while(len(q)):
        temp = q[0]
        q.pop(0)

        if (temp.left):
            ancestors[temp.left.data] = temp.data
            q.append(temp.left)

        if (temp.right):
            ancestors[temp.right.data] = temp.data
            q.append(temp.right)

# function to calculate Kth ancestor
def kthAncestor(root, n, k, node):

    # create array to store 1st ancestors
    ancestors = [0] * (n + 1)

    # generate first ancestor array
    generateArray(root,ancestors)

    # variable to track record of number
    # of ancestors visited
    count = 0

    while (node != -1) :
        node = ancestors[node]
        count += 1
        if(count == k):
            break

    # prKth ancestor
    return node

# Driver Code
if __name__ == '__main__':

    # Let us create binary tree shown
    # in above diagram
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)

    k = 2
    node = 5

    # prkth ancestor of given node
    print(kthAncestor(root, 5, k, node))

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
/* C# program to calculate Kth ancestor of given node */
using System;
using System.Collections.Generic;

class GfG
{

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
}

// function to generate array of ancestors
static void generateArray(Node root, int []ancestors)
{
    // There will be no ancestor of root node
    ancestors[root.data] = -1;

    // level order traversal to
    // generate 1st ancestor
    LinkedList<Node> q = new LinkedList<Node> ();
    q.AddLast(root);

    while(q.Count != 0)
    {
        Node temp = q.First.Value;
        q.RemoveFirst();

        if (temp.left != null)
        {
            ancestors[temp.left.data] = temp.data;
            q.AddLast(temp.left);
        }

        if (temp.right != null)
        {
            ancestors[temp.right.data] = temp.data;
            q.AddLast(temp.right);
        }
    }
}

// function to calculate Kth ancestor
static int kthAncestor(Node root, int n, int k, int node)
{
    // create array to store 1st ancestors
    int []ancestors = new int[n + 1];

    // generate first ancestor array
    generateArray(root,ancestors);

    // variable to track record of number of
    // ancestors visited
    int count = 0;

    while (node != -1)
    {
        node = ancestors[node];
        count++;

        if(count == k)
            break;
    }

    // print Kth ancestor
    return node;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver program to test above functions
public static void Main(String[] args)
{
    // Let us create binary tree shown in above diagram
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    int k = 2;
    int node = 5;

    // print kth ancestor of given node
    Console.WriteLine(kthAncestor(root,5,k,node));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

/* JavaScript program to calculate
Kth ancestor of given node */

// A Binary Tree Node
class Node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
}

// function to generate array of ancestors
function generateArray(root, ancestors)
{
    // There will be no ancestor of root node
    ancestors[root.data] = -1;

    // level order traversal to
    // generate 1st ancestor
    var q = [];
    q.push(root);

    while(q.length != 0)
    {
        var temp = q[0];
        q.shift();

        if (temp.left != null)
        {
            ancestors[temp.left.data] = temp.data;
            q.push(temp.left);
        }

        if (temp.right != null)
        {
            ancestors[temp.right.data] = temp.data;
            q.push(temp.right);
        }
    }
}

// function to calculate Kth ancestor
function kthAncestor(root, n, k, node)
{
    // create array to store 1st ancestors
    var ancestors = Array(n+1).fill(0);

    // generate first ancestor array
    generateArray(root,ancestors);

    // variable to track record of number of
    // ancestors visited
    var count = 0;

    while (node != -1)
    {
        node = ancestors[node];
        count++;

        if(count == k)
            break;
    }

    // print Kth ancestor
    return node;
}

// Utility function to create a new tree node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver program to test above functions
// Let us create binary tree shown in above diagram
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
var k = 2;
var node = 5;
// print kth ancestor of given node
document.write(kthAncestor(root,5,k,node));

</script>
```

**输出:**

```
1
```

**时间复杂度**:O(n)
T3】辅助空间 : O( n)

**方法 2:** 在这个方法中，首先我们将得到一个必须搜索其祖先的元素，从那个节点开始，我们将逐个递减计数，直到到达那个祖先节点。
例如–

考虑下面给出的树:-

         (1)

/ \

      (4)   (2)

/ \ \

   (3)  (7)    (6)

\

              (8)

然后检查 k 是否=0，如果是，则返回该元素作为祖先，否则向上爬一级并减少 k (k = k-1)。
**最初 k = 2**
首先我们搜索 8，然后，
在 8 = >检查是否(k == 0)但是 k = 2 所以 k = k-1 = > k = 2-1 = 1 并且向上爬一级，即在 7
在 7 = >检查是否(k == 0)但是 k = 1 所以 k = k-1 = > k = 1-1 = 0 并且向上爬一级，即在 4
在

## C++14

```
// C++ program for finding
// kth ancestor of a particular node
#include<bits/stdc++.h>
using namespace std;

// Structure for a node
struct node{
  int data;
  struct node *left, *right;
  node(int x)
  {
    data = x;
    left = right = NULL;
  }
};

// Program to find kth ancestor
bool ancestor(struct node* root, int item, int &k)
{
  if(root == NULL)
    return false;

  // Element whose ancestor is to be searched
  if(root->data == item)
  {
    //reduce count by 1
    k = k-1;
    return true;
  }
  else
  {

    // Checking in left side
    bool flag = ancestor(root->left,item,k);
    if(flag)
    {
      if(k == 0)
      {

        // If count = 0 i.e. element is found
        cout<<"["<<root->data<<"] ";
        return false;
      }

      // if count !=0 i.e. this is not the
      // ancestor we are searching for
      // so decrement count
      k = k-1;
      return true;
    }

    // Similarly Checking in right side
    bool flag2 = ancestor(root->right,item,k);
    if(flag2)
    {
      if(k == 0)
      {
        cout<<"["<<root->data<<"] ";
        return false;
      }
      k = k-1;
      return true;
    }
  }
}

// Driver Code
int main()
{
  struct node* root = new node(1);
  root->left = new node(4);
  root->left->right = new node(7);
  root->left->left = new node(3);
  root->left->right->left = new node(8);
  root->right = new node(2);
  root->right->right = new node(6);

  int item,k;
  item = 3;
  k = 1;
  int loc = k;
  bool flag =  ancestor(root,item,k);
  if(flag)
       cout<<"Ancestor doesn't exist\n";
  else
    cout<<"is the "<<loc<<"th ancestor of ["<<
                                   item<<"]"<<endl;
  return 0;
}

// This code is contributed by Sanjeev Yadav.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding
// kth ancestor of a particular node
import java.io.*;

class Node
{
    int data;
    Node left, right;

    Node(int x)
    {
        this.data = x;
        this.left = this.right = null;
    }
}

class GFG{

static int k = 1;

static boolean ancestor(Node root, int item)
{
    if (root == null)
        return false;

    // Element whose ancestor is to be searched
    if (root.data == item)
    {

        // Reduce count by 1
        k = k-1;
        return true;
    }
    else
    {

        // Checking in left side
        boolean flag = ancestor(root.left, item);
        if (flag)
        {
            if (k == 0)
            {

                // If count = 0 i.e. element is found
                System.out.print("[" + root.data + "] ");
                return false;
            }

            // If count !=0 i.e. this is not the
            // ancestor we are searching for
            // so decrement count
            k = k - 1;
            return true;
        }

        // Similarly Checking in right side
        boolean flag2 = ancestor(root.right, item);
        if (flag2)
        {
            if (k == 0)
            {
                System.out.print("[" + root.data + "] ");
                return false;
            }
            k = k - 1;
            return true;
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(4);
    root.left.right = new Node(7);
    root.left.left = new Node(3);
    root.left.right.left = new Node(8);
    root.right = new Node(2);
    root.right.right = new Node(6);

    int item = 3;
    int loc = k;
    boolean flag = ancestor(root, item);

    if (flag)
        System.out.println("Ancestor doesn't exist");
    else
        System.out.println("is the " + (loc) +
                           "th ancestor of [" +
                           (item) + "]");
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for finding
# kth ancestor of a particular node

# Structure for a node
class node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.data = data

# Program to find kth ancestor
def ancestor(root, item):

    global k

    if (root == None):
        return False

    # Element whose ancestor is
    # to be searched
    if (root.data == item):

        # Reduce count by 1
        k = k - 1
        return True

    else:

        # Checking in left side
        flag = ancestor(root.left, item);

        if (flag):
            if (k == 0):

                # If count = 0 i.e. element is found
                print("[" + str(root.data) + "]", end = ' ')
                return False

            # If count !=0 i.e. this is not the
            # ancestor we are searching for
            # so decrement count
            k = k - 1
            return True

        # Similarly Checking in right side
        flag2 = ancestor(root.right, item)

        if (flag2):
            if (k == 0):
                print("[" + str(root.data) + "]")
                return False

            k = k - 1
            return True

# Driver code
if __name__=="__main__":

    root = node(1)
    root.left = node(4)
    root.left.right = node(7)
    root.left.left = node(3)
    root.left.right.left = node(8)
    root.right = node(2)
    root.right.right = node(6)

    item = 3
    k = 1
    loc = k
    flag = ancestor(root, item)

    if (flag):
        print("Ancestor doesn't exist")
    else:
        print("is the " + str(loc) +
              "th ancestor of [" + str(item) + "]")

# This code is contributed by rutvik_56
```

## C#

```
// C# program for finding
// kth ancestor of a particular node
using System;

// Structure for a node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int x)
    {
        this.data = x;
        this.left = this.right = null;
    }
}

class GFG{

static int k = 1;

// Program to find kth ancestor
static bool ancestor(Node root, int item)
{
    if (root == null)
        return false;

    // Element whose ancestor is
    // to be searched
    if (root.data == item)
    {

        // Reduce count by 1
        k = k - 1;
        return true;
    }
    else
    {

        // Checking in left side
        bool flag = ancestor(root.left, item);
        if (flag)
        {
            if (k == 0)
            {

                // If count = 0 i.e. element is found
                Console.Write("[" + root.data + "] ");
                return false;
            }

            // If count !=0 i.e. this is not the
            // ancestor we are searching for
            // so decrement count
            k = k - 1;
            return true;
        }

        // Similarly Checking in right side
        bool flag2 = ancestor(root.right, item);
        if (flag2)
        {
            if (k == 0)
            {
                Console.Write("[" + root.data + "] ");
                return false;
            }
            k = k - 1;
            return true;
        }
    }
    return false;
}

// Driver code
static public void Main()
{
    Node root = new Node(1);
    root.left = new Node(4);
    root.left.right = new Node(7);
    root.left.left = new Node(3);
    root.left.right.left = new Node(8);
    root.right = new Node(2);
    root.right.right = new Node(6);

    int item = 3;
    int loc = k;
    bool flag = ancestor(root, item);

    if (flag)
        Console.WriteLine("Ancestor doesn't exist");
    else
        Console.WriteLine("is the " + (loc) +
                          "th ancestor of [" +
                          (item) + "]");
}
}

// This code is contributed by patel2127
```

## java 描述语言

```
<script>

class Node
{
    constructor(x)
    {
        this.data=x;
        this.left = this.right = null;
    }
}

function ancestor(root, item)
{
    if (root == null)
    {
        return false;
    }

    if (root.data == item)
    {
        k = k - 1;
        return true;
    }

    else
    {
        let flag = ancestor(root.left, item);
        if (flag)
        {
            if (k == 0)
            {
                document.write("[" + (root.data) + "] ");
                return false;
            }
            k = k - 1;
            return true;
        }
        let flag2 = ancestor(root.right, item);
        if (flag2)
        {
            if (k == 0)
            {
                document.write("[" + (root.data) + "] ");
                return false;
            }
            k = k - 1;
            return true;
        }

    }
}

let root = new Node(1)
root.left = new Node(4)
root.left.right = new Node(7)
root.left.left = new Node(3)
root.left.right.left = new Node(8)
root.right = new Node(2)
root.right.right = new Node(6)
let item = 3
    let k = 1
   let loc = k
   let flag = ancestor(root, item)

    if (flag)
        document.write("Ancestor doesn't exist")
    else
        document.write("is the " + (loc) +
              "th ancestor of [" + (item) + "]")

// This code is contributed by rag2127

</script>
```

**Output**

```
[4] is the 1th ancestor of [3]
```

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。