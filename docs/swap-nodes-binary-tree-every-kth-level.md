# 每第 k 级交换二叉树中的节点

> 原文:[https://www . geesforgeks . org/swap-nodes-binary-tree-ever-kth-level/](https://www.geeksforgeeks.org/swap-nodes-binary-tree-every-kth-level/)

给定一个二叉树和整数值 k，任务是交换每第 k 层的兄弟节点，其中 k >= 1。
示例:

```
Input :  k = 2  and Root of below tree                     
      1             Level 1 
    /   \ 
   2     3          Level 2
 /     /   \
4     7     8       Level 3

Output : Root of the following modified tree
      1
    /   \
   3     2
 /  \   /  
7    8  4
Explanation : We need to swap left and right sibling 
              every second level. There is only one 
              even level with nodes to be swapped are
              2 and 3.

Input : k = 1 and Root of following tree

       1          Level 1
     /   \ 
    2     3       Level 2
  /  \ 
 4    5           Level 3
Output : Root of the following modified tree
       1
     /   \
    3     2
         /  \
        5    4
Since k is 1, we need to swap sibling nodes of
all levels.
```

这个问题的一个**简单的解决方案**是，对于每一个都是为 k 的每一个倍数找到兄弟节点并交换它们。
一个**有效的解决方案**是跟踪递归调用中的级别号。对于每个被访问的节点，检查其子节点的层级数是否为 k 的倍数。如果是，则交换该节点的两个子节点。否则，对左右儿童重复出现。
以下是以上思路的实现

## C++

```
// c++ program swap nodes
#include<bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// swap two Node
void Swap( Node **a , Node **b)
{
    Node * temp = *a;
    *a = *b;
    *b = temp;
}

// A utility function swap left- node & right node of tree
// of every k'th level
void swapEveryKLevelUtil( Node *root, int level, int k)
{
    // base case
    if (root== NULL ||
            (root->left==NULL && root->right==NULL) )
        return ;

    //if current level + 1  is present in swap vector
    //then we swap left & right node
    if ( (level + 1) % k == 0)
        Swap(&root->left, &root->right);

    // Recur for left and right subtrees
    swapEveryKLevelUtil(root->left, level+1, k);
    swapEveryKLevelUtil(root->right, level+1, k);
}

// This function mainly calls recursive function
// swapEveryKLevelUtil()
void swapEveryKLevel(Node *root, int k)
{
    // call swapEveryKLevelUtil function with
    // initial level as 1.
    swapEveryKLevelUtil(root, 1, k);
}

// Utility method for inorder tree traversal
void inorder(Node *root)
{
    if (root == NULL)
        return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Driver Code
int main()
{
    /*    1
        /   \
       2     3
     /      /  \
    4      7    8   */
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->right = newNode(8);
    root->right->left = newNode(7);

    int k = 2;
    cout << "Before swap node :"<<endl;
    inorder(root);

    swapEveryKLevel(root, k);

    cout << "\nAfter swap Node :" << endl;
    inorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program swap nodes
class GFG
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// A utility function swap left- node & right node of tree
// of every k'th level
static void swapEveryKLevelUtil( Node root, int level, int k)
{
    // base case
    if (root== null ||
            (root.left==null && root.right==null) )
        return ;

    //if current level + 1 is present in swap vector
    //then we swap left & right node
    if ( (level + 1) % k == 0)
        {
            Node temp=root.left;
            root.left=root.right;
            root.right=temp;
        }

    // Recur for left and right subtrees
    swapEveryKLevelUtil(root.left, level+1, k);
    swapEveryKLevelUtil(root.right, level+1, k);
}

// This function mainly calls recursive function
// swapEveryKLevelUtil()
static void swapEveryKLevel(Node root, int k)
{
    // call swapEveryKLevelUtil function with
    // initial level as 1.
    swapEveryKLevelUtil(root, 1, k);
}

// Utility method for inorder tree traversal
static void inorder(Node root)
{
    if (root == null)
        return;
    inorder(root.left);
    System.out.print(root.data + " ");
    inorder(root.right);
}

// Driver Code
public static void main(String args[])
{
    /* 1
        / \
    2 3
    / / \
    4 7 8 */
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.right = newNode(8);
    root.right.left = newNode(7);

    int k = 2;
    System.out.println("Before swap node :");
    inorder(root);

    swapEveryKLevel(root, k);

    System.out.println("\nAfter swap Node :" );
    inorder(root);
}
}

// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python program to swap nodes

# A binary tree node
class Node:

    # constructor to create a new node 
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A utility function swap left node and right node of tree
# of every k'th level
def swapEveryKLevelUtil(root, level, k):

    # Base Case
    if (root is None or (root.left is None and
                        root.right is None ) ):
        return

    # If current level+1 is present in swap vector
    # then we swap left and right node
    if (level+1)%k == 0:
        root.left, root.right = root.right, root.left

    # Recur for left and right subtree
    swapEveryKLevelUtil(root.left, level+1, k)
    swapEveryKLevelUtil(root.right, level+1, k)

# This function mainly calls recursive function
# swapEveryKLevelUtil
def swapEveryKLevel(root, k):

    # Call swapEveryKLevelUtil function with
    # initial level as 1
    swapEveryKLevelUtil(root, 1, k)

# Method to find the inorder tree traversal
def inorder(root):

    # Base Case
    if root is None:
        return
    inorder(root.left)
    print root.data,
    inorder(root.right)

# Driver code
"""
          1
        /   \
       2     3
     /      /  \
    4      7    8
"""
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.right.right = Node(8)
root.right.left = Node(7)

k = 2
print "Before swap node :"
inorder(root)

swapEveryKLevel(root, k)

print "\nAfter swap Node : "
inorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program swap nodes
using System;

class GFG
{

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
};

// function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// A utility function swap left- node & right node of tree
// of every k'th level
static void swapEveryKLevelUtil( Node root, int level, int k)
{
    // base case
    if (root == null ||
            (root.left == null && root.right==null) )
        return ;

    //if current level + 1 is present in swap vector
    //then we swap left & right node
    if ( (level + 1) % k == 0)
        {
            Node temp=root.left;
            root.left=root.right;
            root.right=temp;
        }

    // Recur for left and right subtrees
    swapEveryKLevelUtil(root.left, level+1, k);
    swapEveryKLevelUtil(root.right, level+1, k);
}

// This function mainly calls recursive function
// swapEveryKLevelUtil()
static void swapEveryKLevel(Node root, int k)
{
    // call swapEveryKLevelUtil function with
    // initial level as 1.
    swapEveryKLevelUtil(root, 1, k);
}

// Utility method for inorder tree traversal
static void inorder(Node root)
{
    if (root == null)
        return;
    inorder(root.left);
    Console.Write(root.data + " ");
    inorder(root.right);
}

// Driver Code
public static void Main(String []args)
{
    /* 1
        / \
    2 3
    / / \
    4 7 8 */
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.right = newNode(8);
    root.right.left = newNode(7);

    int k = 2;
    Console.WriteLine("Before swap node :");
    inorder(root);

    swapEveryKLevel(root, k);

    Console.WriteLine("\nAfter swap Node :" );
    inorder(root);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program swap nodes

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to create a new tree node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // A utility function swap left- node & right node of tree
    // of every k'th level
    function swapEveryKLevelUtil(root, level, k)
    {
        // base case
        if (root== null ||
                (root.left==null && root.right==null) )
            return ;

        //if current level + 1 is present in swap vector
        //then we swap left & right node
        if ( (level + 1) % k == 0)
            {
                let temp=root.left;
                root.left=root.right;
                root.right=temp;
            }

        // Recur for left and right subtrees
        swapEveryKLevelUtil(root.left, level+1, k);
        swapEveryKLevelUtil(root.right, level+1, k);
    }

    // This function mainly calls recursive function
    // swapEveryKLevelUtil()
    function swapEveryKLevel(root, k)
    {
        // call swapEveryKLevelUtil function with
        // initial level as 1.
        swapEveryKLevelUtil(root, 1, k);
    }

    // Utility method for inorder tree traversal
    function inorder(root)
    {
        if (root == null)
            return;
        inorder(root.left);
        document.write(root.data + " ");
        inorder(root.right);
    }

    /* 1
        / \
    2 3
    / / \
    4 7 8 */
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.right = newNode(8);
    root.right.left = newNode(7);

    let k = 2;
    document.write("Before swap node :" + "</br>");
    inorder(root);

    swapEveryKLevel(root, k);

    document.write("</br>" + "After swap Node :" + "</br>");
    inorder(root);

</script>
```

**输出:**

```
Before swap node :
4 2 1 7 3 8 
After swap Node :
7 3 8 1 4 2 
```

本文由 **Nishant_singh(pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。