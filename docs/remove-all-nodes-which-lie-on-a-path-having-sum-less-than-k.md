# 用和> = k

移除所有不在任何路径中的节点

> 原文:[https://www . geesforgeks . org/remove-all-nodes-on-a-path-sum-小于-k/](https://www.geeksforgeeks.org/remove-all-nodes-which-lie-on-a-path-having-sum-less-than-k/)

给定一棵二叉树，完整的路径被定义为从根到叶的路径。该路径上所有节点的总和被定义为该路径的总和。给定一个数字 K，你必须移除(修剪树)所有不在任何路径上的节点，并且总和> =k

注意:一个节点可以是多个路径的一部分。所以只有当它的所有路径的和小于 k 时，我们才必须删除它。

```
Consider the following Binary Tree
          1 
      /      \
     2        3
   /   \     /  \
  4     5   6    7
 / \    /       /
8   9  12      10
   / \           \
  13  14         11
      / 
     15 

For input k = 20, the tree should be changed to following
(Nodes with values 6 and 8 are deleted)
          1 
      /      \
     2        3
   /   \        \
  4     5        7
   \    /       /
    9  12      10
   / \           \
  13  14         11
      / 
     15 

For input k = 45, the tree should be changed to following.
      1 
    / 
   2   
  / 
 4  
  \   
   9    
    \   
     14 
     /
    15 
```

其思想是遍历树并以自下而上的方式删除节点。遍历树时，递归计算每个路径从根节点到叶节点的节点总数。对于每个受访节点，对照给定的总和“k”检查总计算总和。如果总和小于 k，则释放(删除)该节点(叶节点)，并将总和返回到前一个节点。由于路径是从根到叶，并且节点是以自下而上的方式删除的，因此只有当节点的所有后代都被删除时，节点才会被删除。因此，当删除一个节点时，它必须是当前二叉树中的一片叶子。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// A utility function to get maximum of two integers
int max(int l, int r) { return (l > r ? l : r); }

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary Tree node with given data
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// print the tree in LVR (Inorder traversal) way.
void print(struct Node *root)
{
    if (root != NULL)
    {
        print(root->left);
        cout <<" "<< root->data;
        print(root->right);
    }
}

/* Main function which truncates the binary tree. */
struct Node *pruneUtil(struct Node *root, int k, int *sum)
{
    // Base Case
    if (root == NULL)  return NULL;

    // Initialize left and right sums as sum from root to
    // this node (including this node)
    int lsum = *sum + (root->data);
    int rsum = lsum;

    // Recursively prune left and right subtrees
    root->left = pruneUtil(root->left, k, &lsum);
    root->right = pruneUtil(root->right, k, &rsum);

    // Get the maximum of left and right sums
    *sum = max(lsum, rsum);

    // If maximum is smaller than k, then this node
    // must be deleted
    if (*sum < k)
    {
        free(root);
        root = NULL;
    }

    return root;
}

// A wrapper over pruneUtil()
struct Node *prune(struct Node *root, int k)
{
    int sum = 0;
    return pruneUtil(root, k, &sum);
}

// Driver program to test above function
int main()
{
    int k = 45;
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);
    root->left->right->left = newNode(12);
    root->right->right->left = newNode(10);
    root->right->right->left->right = newNode(11);
    root->left->left->right->left = newNode(13);
    root->left->left->right->right = newNode(14);
    root->left->left->right->right->left = newNode(15);

    cout <<"Tree before truncation\n";
    print(root);

    root = prune(root, k); // k is 45

    cout <<"\n\nTree after truncation\n";
    print(root);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
#include <stdio.h>
#include <stdlib.h>

// A utility function to get maximum of two integers
int max(int l, int r) { return (l > r ? l : r); }

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary Tree node with given data
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// print the tree in LVR (Inorder traversal) way.
void print(struct Node *root)
{
    if (root != NULL)
    {
        print(root->left);
        printf("%d ",root->data);
        print(root->right);
    }
}

/* Main function which truncates the binary tree. */
struct Node *pruneUtil(struct Node *root, int k, int *sum)
{
    // Base Case
    if (root == NULL)  return NULL;

    // Initialize left and right sums as sum from root to
    // this node (including this node)
    int lsum = *sum + (root->data);
    int rsum = lsum;

    // Recursively prune left and right subtrees
    root->left = pruneUtil(root->left, k, &lsum);
    root->right = pruneUtil(root->right, k, &rsum);

    // Get the maximum of left and right sums
    *sum = max(lsum, rsum);

    // If maximum is smaller than k, then this node
    // must be deleted
    if (*sum < k)
    {
        free(root);
        root = NULL;
    }

    return root;
}

// A wrapper over pruneUtil()
struct Node *prune(struct Node *root, int k)
{
    int sum = 0;
    return pruneUtil(root, k, &sum);
}

// Driver program to test above function
int main()
{
    int k = 45;
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);
    root->left->right->left = newNode(12);
    root->right->right->left = newNode(10);
    root->right->right->left->right = newNode(11);
    root->left->left->right->left = newNode(13);
    root->left->left->right->right = newNode(14);
    root->left->left->right->right->left = newNode(15);

    printf("Tree before truncation\n");
    print(root);

    root = prune(root, k); // k is 45

    printf("\n\nTree after truncation\n");
    print(root);

    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*; 
class GFG
{

// A utility function to get
// maximum of two integers 
static int max(int l, int r) 
{ 
    return (l > r ? l : r);
} 

// A Binary Tree Node 
static class Node 
{ 
    int data; 
    Node left, right; 
}; 

static class INT
{
    int v;
INT(int a)
{
    v = a;
}
}

// A utility function to create 
// a new Binary Tree node with
// given data 
static Node newNode(int data) 
{ 
    Node node = new Node(); 
    node.data = data; 
    node.left = node.right = null; 
    return node; 
} 

// print the tree in LVR 
// (Inorder traversal) way. 
static void print(Node root) 
{ 
    if (root != null) 
    { 
        print(root.left); 
        System.out.print(root.data + " "); 
        print(root.right); 
    } 
} 

// Main function which
// truncates the binary tree. 
static Node pruneUtil(Node root, int k, 
                      INT sum) 
{ 
    // Base Case 
    if (root == null) return null; 

    // Initialize left and right 
    // sums as sum from root to 
    // this node (including this node) 
    INT lsum = new INT(sum.v + (root.data)); 
    INT rsum = new INT(lsum.v); 

    // Recursively prune left 
    // and right subtrees 
    root.left = pruneUtil(root.left, k, lsum); 
    root.right = pruneUtil(root.right, k, rsum); 

    // Get the maximum of
    // left and right sums 
    sum.v = max(lsum.v, rsum.v); 

    // If maximum is smaller 
    // than k, then this node 
    // must be deleted 
    if (sum.v < k) 
    { 

        root = null; 
    } 

    return root; 
} 

// A wrapper over pruneUtil() 
static Node prune(Node root, int k) 
{ 
    INT sum = new INT(0); 
    return pruneUtil(root, k, sum); 
} 

// Driver Code
public static void main(String args[])
{ 
    int k = 45; 
    Node root = newNode(1); 
    root.left = newNode(2); 
    root.right = newNode(3); 
    root.left.left = newNode(4); 
    root.left.right = newNode(5); 
    root.right.left = newNode(6); 
    root.right.right = newNode(7); 
    root.left.left.left = newNode(8); 
    root.left.left.right = newNode(9); 
    root.left.right.left = newNode(12); 
    root.right.right.left = newNode(10); 
    root.right.right.left.right = newNode(11); 
    root.left.left.right.left = newNode(13); 
    root.left.left.right.right = newNode(14); 
    root.left.left.right.right.left = newNode(15); 

    System.out.println("Tree before truncation\n"); 
    print(root); 

    root = prune(root, k); // k is 45 

    System.out.println("\n\nTree after truncation\n"); 
    print(root); 
} 
}

// This code is contributed by Arnab Kundu

```

## 蟒蛇 3

```
# A class to create a new Binary Tree
# node with given data 
class newNode:
    def __init__(self, data): 
        self.data = data 
        self.left = self.right = None

# print the tree in LVR (Inorder traversal) way. 
def Print(root):
    if (root != None):
        Print(root.left) 
        print(root.data, end = " ") 
        Print(root.right)

# Main function which truncates
# the binary tree. 
def pruneUtil(root, k, Sum):

    # Base Case 
    if (root == None):
        return None

    # Initialize left and right Sums as 
    # Sum from root to this node 
    # (including this node) 
    lSum = [Sum[0] + (root.data)] 
    rSum = [lSum[0]] 

    # Recursively prune left and right 
    # subtrees 
    root.left = pruneUtil(root.left, k, lSum) 
    root.right = pruneUtil(root.right, k, rSum) 

    # Get the maximum of left and right Sums 
    Sum[0] = max(lSum[0], rSum[0]) 

    # If maximum is smaller than k, 
    # then this node must be deleted 
    if (Sum[0] < k[0]):
        root = None
    return root

# A wrapper over pruneUtil() 
def prune(root, k):
    Sum = [0] 
    return pruneUtil(root, k, Sum)

# Driver Code
if __name__ == '__main__':
    k = [45]
    root = newNode(1) 
    root.left = newNode(2) 
    root.right = newNode(3) 
    root.left.left = newNode(4) 
    root.left.right = newNode(5) 
    root.right.left = newNode(6) 
    root.right.right = newNode(7) 
    root.left.left.left = newNode(8) 
    root.left.left.right = newNode(9) 
    root.left.right.left = newNode(12) 
    root.right.right.left = newNode(10) 
    root.right.right.left.right = newNode(11) 
    root.left.left.right.left = newNode(13) 
    root.left.left.right.right = newNode(14) 
    root.left.left.right.right.left = newNode(15) 

    print("Tree before truncation")
    Print(root) 
    print()
    root = prune(root, k) # k is 45 

    print("Tree after truncation")
    Print(root)

# This code is contributed by PranchalK

```

## C#

```

using System;

// C# program to implement 
// the above approach 
public class GFG
{

// A utility function to get 
// maximum of two integers  
public static int max(int l, int r)
{
    return (l > r ? l : r);
}

// A Binary Tree Node  
public class Node
{
    public int data;
    public Node left, right;
}

public class INT
{
    public int v;
public INT(int a)
{
    v = a;
}
}

// A utility function to create  
// a new Binary Tree node with 
// given data  
public static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// print the tree in LVR  
// (Inorder traversal) way.  
public static void print(Node root)
{
    if (root != null)
    {
        print(root.left);
        Console.Write(root.data + " ");
        print(root.right);
    }
}

// Main function which 
// truncates the binary tree.  
public static Node pruneUtil(Node root, int k, INT sum)
{
    // Base Case  
    if (root == null)
    {
        return null;
    }

    // Initialize left and right  
    // sums as sum from root to  
    // this node (including this node)  
    INT lsum = new INT(sum.v + (root.data));
    INT rsum = new INT(lsum.v);

    // Recursively prune left  
    // and right subtrees  
    root.left = pruneUtil(root.left, k, lsum);
    root.right = pruneUtil(root.right, k, rsum);

    // Get the maximum of 
    // left and right sums  
    sum.v = max(lsum.v, rsum.v);

    // If maximum is smaller  
    // than k, then this node  
    // must be deleted  
    if (sum.v < k)
    {

        root = null;
    }

    return root;
}

// A wrapper over pruneUtil()  
public static Node prune(Node root, int k)
{
    INT sum = new INT(0);
    return pruneUtil(root, k, sum);
}

// Driver Code 
public static void Main(string[] args)
{
    int k = 45;
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(9);
    root.left.right.left = newNode(12);
    root.right.right.left = newNode(10);
    root.right.right.left.right = newNode(11);
    root.left.left.right.left = newNode(13);
    root.left.left.right.right = newNode(14);
    root.left.left.right.right.left = newNode(15);

    Console.WriteLine("Tree before truncation\n");
    print(root);

    root = prune(root, k); // k is 45

    Console.WriteLine("\n\nTree after truncation\n");
    print(root);
}
}

  // This code is contributed by Shrikant13

```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// A utility function to get
// maximum of two integers 
function max(l, r) 
{ 
    return (l > r ? l : r);
} 

class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

class INT
{
    constructor(a) 
    {
        this.v = a;
    }
}

// A utility function to create 
// a new Binary Tree node with
// given data 
function newNode(data) 
{ 
    let node = new Node(data); 
    return node; 
} 

// print the tree in LVR 
// (Inorder traversal) way. 
function print(root) 
{ 
    if (root != null) 
    { 
        print(root.left); 
        document.write(root.data + " "); 
        print(root.right); 
    } 
} 

// Main function which
// truncates the binary tree. 
function pruneUtil(root, k, sum) 
{ 

    // Base Case 
    if (root == null) 
        return null; 

    // Initialize left and right 
    // sums as sum from root to 
    // this node (including this node) 
    let lsum = new INT(sum.v + (root.data)); 
    let rsum = new INT(lsum.v); 

    // Recursively prune left 
    // and right subtrees 
    root.left = pruneUtil(root.left, k, lsum); 
    root.right = pruneUtil(root.right, k, rsum); 

    // Get the maximum of
    // left and right sums 
    sum.v = max(lsum.v, rsum.v); 

    // If maximum is smaller 
    // than k, then this node 
    // must be deleted 
    if (sum.v < k) 
    { 
        root = null; 
    } 
    return root; 
} 

// A wrapper over pruneUtil() 
function prune(root, k) 
{ 
    let sum = new INT(0); 
    return pruneUtil(root, k, sum);
} 

// Driver code
let k = 45; 
let root = newNode(1); 
root.left = newNode(2); 
root.right = newNode(3); 
root.left.left = newNode(4); 
root.left.right = newNode(5); 
root.right.left = newNode(6); 
root.right.right = newNode(7); 
root.left.left.left = newNode(8); 
root.left.left.right = newNode(9); 
root.left.right.left = newNode(12); 
root.right.right.left = newNode(10); 
root.right.right.left.right = newNode(11); 
root.left.left.right.left = newNode(13); 
root.left.left.right.right = newNode(14); 
root.left.left.right.right.left = newNode(15); 

document.write("Tree before truncation" + "</br>"); 
print(root); 

root = prune(root, k); // k is 45 

document.write("</br></br>" + 
               "Tree after truncation" + "</br>"); 
print(root); 

// This code is contributed by decode2207

</script>
```

**输出:**

```
Tree before truncation
8 4 13 9 15 14 2 12 5 1 6 3 10 11 7

Tree after truncation
4 9 15 14 2 1
```

**时间复杂度:** O(n)，解对给定的二叉树做单次遍历。

**一个更简单的解决方案:**
上面的代码可以用节点自下而上删除的方式来简化。这个想法是在向下遍历时不断减少总和。当我们到达一片叶子并且总和大于叶子的数据时，我们就删除叶子。请注意，删除节点可能会将非叶节点转换为叶节点，如果转换后的叶节点的数据小于当前总和，则转换后的叶节点也应被删除。
感谢维姬在下方评论中提出这个解决方案。

## C++

```

#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary
// Tree node with given data
struct Node* newNode(int data)
{
    struct Node* node =
    (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// print the tree in LVR (Inorder traversal) way.
void print(struct Node *root)
{
    if (root != NULL)
    {
        print(root->left);
        cout << root->data << " ";
        print(root->right);
    }
}

/* Main function which truncates the binary tree. */
struct Node *prune(struct Node *root, int sum)
{
    // Base Case
    if (root == NULL) return NULL;

    // Recur for left and right subtrees
    root->left = prune(root->left, sum - root->data);
    root->right = prune(root->right, sum - root->data);

    // If we reach leaf whose data is smaller than sum,
    // we delete the leaf. An important thing to note
    // is a non-leaf node can become leaf when its
    // children are deleted.
    if (root->left==NULL && root->right==NULL)
    {
        if (root->data < sum)
        {
            free(root);
            return NULL;
        }
    }

    return root;
}

// Driver program to test above function
int main()
{
    int k = 45;
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);
    root->left->right->left = newNode(12);
    root->right->right->left = newNode(10);
    root->right->right->left->right = newNode(11);
    root->left->left->right->left = newNode(13);
    root->left->left->right->right = newNode(14);
    root->left->left->right->right->left = newNode(15);

    cout << "Tree before truncation\n";
    print(root);

    root = prune(root, k); // k is 45

    cout << "\n\nTree after truncation\n";
    print(root);

    return 0;
}

// This code is contributed
// by Akanksha Rai

```

## C

```
#include <stdio.h>
#include <stdlib.h>

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary
// Tree node with given data
struct Node* newNode(int data)
{
    struct Node* node =
       (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// print the tree in LVR (Inorder traversal) way.
void print(struct Node *root)
{
    if (root != NULL)
    {
        print(root->left);
        printf("%d ",root->data);
        print(root->right);
    }
}

/* Main function which truncates the binary tree. */
struct Node *prune(struct Node *root, int sum)
{
    // Base Case
    if (root == NULL) return NULL;

    // Recur for left and right subtrees
    root->left = prune(root->left, sum - root->data);
    root->right = prune(root->right, sum - root->data);

    // If we reach leaf whose data is smaller than sum,
    // we delete the leaf.  An important thing to note
    // is a non-leaf node can become leaf when its
    // children are deleted.
    if (root->left==NULL && root->right==NULL)
    {
        if (root->data < sum)
        {
            free(root);
            return NULL;
        }
    }

    return root;
}

// Driver program to test above function
int main()
{
    int k = 45;
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);
    root->left->right->left = newNode(12);
    root->right->right->left = newNode(10);
    root->right->right->left->right = newNode(11);
    root->left->left->right->left = newNode(13);
    root->left->left->right->right = newNode(14);
    root->left->left->right->right->left = newNode(15);

    printf("Tree before truncation\n");
    print(root);

    root = prune(root, k); // k is 45

    printf("\n\nTree after truncation\n");
    print(root);

    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove all nodes which donot 
// lie on path having sum>= k

// Class representing binary tree node
class Node {
    int data;
    Node left;
    Node right;

    // Constructor to create a new node
    public Node(int data) {
        this.data = data;
        left = null;
        right = null;
    }
}

// class to truncate binary tree
class BinaryTree {
    Node root;

    // recursive method to truncate binary tree
    public Node prune(Node root, int sum) {

        // base case
        if (root == null)
            return null;

        // recur for left and right subtree
        root.left = prune(root.left, sum - root.data);
        root.right = prune(root.right, sum - root.data);

        // if node is a leaf node whose data is smaller
        // than the sum we delete the leaf.An important
        // thing to note is a non-leaf node can become
        // leaf when its children are deleted.
        if (isLeaf(root)) {
            if (sum > root.data)
                root = null;
        }

        return root;
    } 

    // utility method to check if node is leaf
    public boolean isLeaf(Node root) {
        if (root == null)
            return false;
        if (root.left == null && root.right == null)
            return true;
        return false;
    }

    // for print traversal
    public void print(Node root) {

        // base case
        if (root == null)
            return;

        print(root.left);
        System.out.print(root.data + " ");
        print(root.right);
    }
}

// Driver class to test above function
public class GFG {
    public static void main(String args[]) {

        BinaryTree tree = new BinaryTree();

        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.left.left.left = new Node(8);
        tree.root.left.left.right = new Node(9);
        tree.root.left.right.left = new Node(12);
        tree.root.right.right.left = new Node(10);
        tree.root.right.right.left.right = new Node(11);
        tree.root.left.left.right.left = new Node(13);
        tree.root.left.left.right.right = new Node(14);
        tree.root.left.left.right.right.left = new Node(15);

        System.out.println("Tree before truncation");
        tree.print(tree.root);

        tree.prune(tree.root, 45);

        System.out.println("\nTree after truncation");
        tree.print(tree.root);
    }
}

// This code is contributed by Shweta Singh

```

## 蟒蛇 3

```
"""
Python program to remove all nodes which don’t
lie in any path with sum>= k
"""

# binary tree node contains data field , left
# and right pointer
class Node:

    # constructor to create tree node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to remove all nodes which do not
# lie in th sum path
def prune(root, sum):

    # Base case
    if root is None:
        return None

    # Recur for left and right subtree
    root.left = prune(root.left, sum - root.data)
    root.right = prune(root.right, sum - root.data)

    # if node is leaf and sum is found greater
    # than data than remove node An important 
    # thing to remember is that a non-leaf node 
    # can become a leaf when its children are 
    # removed
    if root.left is None and root.right is None:
        if sum > root.data:
            return None

    return root

# inorder traversal
def inorder(root):
    if root is None:
        return
    inorder(root.left)
    print(root.data, "", end="")
    inorder(root.right)

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)
root.left.left.left = Node(8)
root.left.left.right = Node(9)
root.left.right.left = Node(12)
root.right.right.left = Node(10)
root.right.right.left.right = Node(11)
root.left.left.right.left = Node(13)
root.left.left.right.right = Node(14)
root.left.left.right.right.left = Node(15)

print("Tree before truncation")
inorder(root)
prune(root, 45)
print("\nTree after truncation")
inorder(root)

# This code is contributed by Shweta Singh

```

## C#

```

using System;

// C# program to remove all nodes which donot  
// lie on path having sum>= k 

// Class representing binary tree node 
public class Node
{
    public int data;
    public Node left;
    public Node right;

    // Constructor to create a new node 
    public Node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
}

// class to truncate binary tree 
public class BinaryTree
{
    public Node root;

    // recursive method to truncate binary tree 
    public virtual Node prune(Node root, int sum)
    {

        // base case 
        if (root == null)
        {
            return null;
        }

        // recur for left and right subtree 
        root.left = prune(root.left, sum - root.data);
        root.right = prune(root.right, sum - root.data);

        // if node is a leaf node whose data is smaller 
        // than the sum we delete the leaf.An important 
        // thing to note is a non-leaf node can become 
        // leaf when its children are deleted. 
        if (isLeaf(root))
        {
            if (sum > root.data)
            {
                root = null;
            }
        }

        return root;
    }

    // utility method to check if node is leaf 
    public virtual bool isLeaf(Node root)
    {
        if (root == null)
        {
            return false;
        }
        if (root.left == null && root.right == null)
        {
            return true;
        }
        return false;
    }

    // for print traversal 
    public virtual void print(Node root)
    {

        // base case 
        if (root == null)
        {
            return;
        }

        print(root.left);
        Console.Write(root.data + " ");
        print(root.right);
    }
}

// Driver class to test above function 
public class GFG
{
    public static void Main(string[] args)
    {

        BinaryTree tree = new BinaryTree();

        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.left.left.left = new Node(8);
        tree.root.left.left.right = new Node(9);
        tree.root.left.right.left = new Node(12);
        tree.root.right.right.left = new Node(10);
        tree.root.right.right.left.right = new Node(11);
        tree.root.left.left.right.left = new Node(13);
        tree.root.left.left.right.right = new Node(14);
        tree.root.left.left.right.right.left = new Node(15);

        Console.WriteLine("Tree before truncation");
        tree.print(tree.root);

        tree.prune(tree.root, 45);

        Console.WriteLine("\nTree after truncation");
        tree.print(tree.root);
    }
}

  // This code is contributed by Shrikant13

```

## java 描述语言

```
<script>

      // JavaScript program to remove all nodes which donot
      // lie on path having sum>= k

      // Class representing binary tree node
      class Node {
        // Constructor to create a new node
        constructor(data) {
          this.data = data;
          this.left = null;
          this.right = null;
        }
      }

      // class to truncate binary tree
      class BinaryTree {
        constructor() {
          this.root = null;
        }

        // recursive method to truncate binary tree
        prune(root, sum) {
          // base case
          if (root == null) {
            return null;
          }

          // recur for left and right subtree
          root.left = this.prune(root.left, sum - root.data);
          root.right = this.prune(root.right, sum - root.data);

          // if node is a leaf node whose data is smaller
          // than the sum we delete the leaf.An important
          // thing to note is a non-leaf node can become
          // leaf when its children are deleted.
          if (this.isLeaf(root)) {
            if (sum > root.data) {
              root = null;
            }
          }

          return root;
        }

        // utility method to check if node is leaf
        isLeaf(root) {
          if (root == null) {
            return false;
          }
          if (root.left == null && root.right == null) {
            return true;
          }
          return false;
        }

        // for print traversal
        print(root) {
          // base case
          if (root == null) {
            return;
          }

          this.print(root.left);
          document.write(root.data + " ");
          this.print(root.right);
        }
      }

      // Driver class to test above function
      var tree = new BinaryTree();

      tree.root = new Node(1);
      tree.root.left = new Node(2);
      tree.root.right = new Node(3);
      tree.root.left.left = new Node(4);
      tree.root.left.right = new Node(5);
      tree.root.right.left = new Node(6);
      tree.root.right.right = new Node(7);
      tree.root.left.left.left = new Node(8);
      tree.root.left.left.right = new Node(9);
      tree.root.left.right.left = new Node(12);
      tree.root.right.right.left = new Node(10);
      tree.root.right.right.left.right = new Node(11);
      tree.root.left.left.right.left = new Node(13);
      tree.root.left.left.right.right = new Node(14);
      tree.root.left.left.right.right.left = new Node(15);

      document.write("Tree before truncation <br>");
      tree.print(tree.root);

      tree.prune(tree.root, 45);

      document.write("<br><br>Tree after truncation<br>");
      tree.print(tree.root);

</script>
```

**输出:**

```
Tree before truncation
8 4 13 9 15 14 2 12 5 1 6 3 10 11 7

Tree after truncation
4 9 15 14 2 1

```

本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643?fref=ts) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。