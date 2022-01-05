# 从给定的前序和后序遍历构建全二叉树

> 原文:[https://www . geesforgeks . org/full-and-complete-二叉树-从给定-前序-后序-traversals/](https://www.geeksforgeeks.org/full-and-complete-binary-tree-from-given-preorder-and-postorder-traversals/)

给定两个代表全二叉树的前序和后序遍历的数组，构造二叉树。
完全二叉树是一个二叉树，其中每个节点有 0 或 2 个子节点

以下是完整树的示例。

```
        1
      /   \
    2       3
  /  \     /  \
 4    5   6    7

       1
     /   \
   2      3
        /   \  
       4     5
           /   \  
          6    7

          1
        /   \
      2       3
    /  \     /  \
   4    5   6    7
 /  \  
8    9 
```

不可能由前序和后序遍历来构造一般的二叉树(见[本](https://www.geeksforgeeks.org/archives/657))。但是如果知道二叉树是满的，我们就可以毫不含糊地构造树。让我们借助下面的例子来理解这一点。

让我们将两个给定的数组视为 pre[] = {1，2，4，8，9，5，3，6，7}和 post[] = {8，9，4，5，2，6，7，3，1 }；
在 pre[]，最左边的元素是树根。由于树已满且数组大小大于 1。pre[]中 1 旁边的值必须是根的左子项。所以我们知道 1 是根，2 是左子。如何找到左子树中的所有节点？我们知道 2 是左子树中所有节点的根。post[]中 2 之前的所有节点必须在左子树中。现在我们知道 1 是根，元素{8，9，4，5，2}在左子树，元素{6，7，3}在右子树。

```
                  1
                /   \
               /      \
     {8, 9, 4, 5, 2}     {6, 7, 3}
```

我们递归地遵循上面的方法，得到下面的树。

```
          1
        /   \
      2       3
    /  \     /  \
   4    5   6    7
  / \  
 8   9 
```

## C++

```
/* program for construction of full binary tree */
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class node
{
    public:
    int data;
    node *left;
    node *right;
};

// A utility function to create a node
node* newNode (int data)
{
    node* temp = new node();

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct Full from pre[] and post[].
// preIndex is used to keep track of index in pre[].
// l is low index and h is high index for the current subarray in post[]
node* constructTreeUtil (int pre[], int post[], int* preIndex,
                                int l, int h, int size)
{
    // Base case
    if (*preIndex >= size || l > h)
        return NULL;

    // The first node in preorder traversal is root. So take the node at
    // preIndex from preorder and make it root, and increment preIndex
    node* root = newNode ( pre[*preIndex] );
    ++*preIndex;

    // If the current subarray has only one element, no need to recur
    if (l == h)
        return root;

    // Search the next element of pre[] in post[]
    int i;
    for (i = l; i <= h; ++i)
        if (pre[*preIndex] == post[i])
            break;

    // Use the index of element found in postorder to divide
        // postorder array in two parts. Left subtree and right subtree
    if (i <= h)
    {
        root->left = constructTreeUtil (pre, post, preIndex,
                                                l, i, size);
        root->right = constructTreeUtil (pre, post, preIndex,
                                                 i + 1, h-1, size);
    }

    return root;
}

// The main function to construct Full Binary Tree from given preorder and
// postorder traversals. This function mainly uses constructTreeUtil()
node *constructTree (int pre[], int post[], int size)
{
    int preIndex = 0;
    return constructTreeUtil (pre, post, &preIndex, 0, size - 1, size);
}

// A utility function to print inorder traversal of a Binary Tree
void printInorder (node* node)
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
    int pre[] = {1, 2, 4, 8, 9, 5, 3, 6, 7};
    int post[] = {8, 9, 4, 5, 2, 6, 7, 3, 1};
    int size = sizeof( pre ) / sizeof( pre[0] );

    node *root = constructTree(pre, post, size);

    cout<<"Inorder traversal of the constructed tree: \n";
    printInorder(root);

    return 0;
}

//This code is contributed by rathbhupendra
```

## C

```
/* program for construction of full binary tree */
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node *left;
    struct node *right;
};

// A utility function to create a node
struct node* newNode (int data)
{
    struct node* temp = (struct node *) malloc( sizeof(struct node) );

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct Full from pre[] and post[].
// preIndex is used to keep track of index in pre[].
// l is low index and h is high index for the current subarray in post[]
struct node* constructTreeUtil (int pre[], int post[], int* preIndex,
                                int l, int h, int size)
{
    // Base case
    if (*preIndex >= size || l > h)
        return NULL;

    // The first node in preorder traversal is root. So take the node at
    // preIndex from preorder and make it root, and increment preIndex
    struct node* root = newNode ( pre[*preIndex] );
    ++*preIndex;

    // If the current subarray has only one element, no need to recur
    if (l == h)
        return root;

    // Search the next element of pre[] in post[]
    int i;
    for (i = l; i <= h; ++i)
        if (pre[*preIndex] == post[i])
            break;

    // Use the index of element found in postorder to divide
    // postorder array in two parts. Left subtree and right subtree
    if (i <= h)
    {
        root->left = constructTreeUtil (pre, post, preIndex,
                                        l, i, size);
        root->right = constructTreeUtil (pre, post, preIndex,
                                         i + 1, h-1, size);
    }

    return root;
}

// The main function to construct Full Binary Tree from given preorder and
// postorder traversals. This function mainly uses constructTreeUtil()
struct node *constructTree (int pre[], int post[], int size)
{
    int preIndex = 0;
    return constructTreeUtil (pre, post, &preIndex, 0, size - 1, size);
}

// A utility function to print inorder traversal of a Binary Tree
void printInorder (struct node* node)
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
    int pre[] = {1, 2, 4, 8, 9, 5, 3, 6, 7};
    int post[] = {8, 9, 4, 5, 2, 6, 7, 3, 1};
    int size = sizeof( pre ) / sizeof( pre[0] );

    struct node *root = constructTree(pre, post, size);

    printf("Inorder traversal of the constructed tree: \n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for construction
// of full binary tree
public class fullbinarytreepostpre
{
    // variable to hold index in pre[] array
    static int preindex;

    static class node
    {
        int data;
        node left, right;

        public node(int data)
        {
            this.data = data;
        }
    }

    // A recursive function to construct Full
    // from pre[] and post[]. preIndex is used
    // to keep track of index in pre[]. l is
    // low index and h is high index for the
    // current subarray in post[]
    static node constructTreeUtil(int pre[], int post[], int l,
                                   int h, int size)
    {

        // Base case
        if (preindex >= size || l > h)
            return null;

        // The first node in preorder traversal is
        // root. So take the node at preIndex from
        // preorder and make it root, and increment
        // preIndex
        node root = new node(pre[preindex]);
        preindex++;

        // If the current subarray has only one
        // element, no need to recur or
        // preIndex > size after incrementing
        if (l == h || preindex >= size)
            return root;
        int i;

        // Search the next element of pre[] in post[]
        for (i = l; i <= h; i++)
        {
            if (post[i] == pre[preindex])
                break;
        }
        // Use the index of element found in
        // postorder to divide postorder array
        // in two parts. Left subtree and right subtree
        if (i <= h)
        {
            root.left = constructTreeUtil(pre, post, l, i, size);
            root.right = constructTreeUtil(pre, post, i + 1, h-1, size);
        }
        return root;
    }

    // The main function to construct Full
    // Binary Tree from given preorder and
    // postorder traversals. This function
    // mainly uses constructTreeUtil()
    static node constructTree(int pre[], int post[], int size)
    {
        preindex = 0;
        return constructTreeUtil(pre, post, 0, size - 1, size);
    }

    static void printInorder(node root)
    {
        if (root == null)
            return;
        printInorder(root.left);
        System.out.print(root.data + " ");
        printInorder(root.right);
    }

    public static void main(String[] args)
    {

        int pre[] = { 1, 2, 4, 8, 9, 5, 3, 6, 7 };
        int post[] = { 8, 9, 4, 5, 2, 6, 7, 3, 1 };

        int size = pre.length;
        node root = constructTree(pre, post, size);

        System.out.println("Inorder traversal of the constructed tree:");
        printInorder(root);
    }
}

// This code is contributed by Rishabh Mahrsee
```

## 蟒蛇 3

```
# Python3 program for construction of
# full binary tree

# A binary tree node has data, pointer
# to left child and a pointer to right child
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# A recursive function to construct
# Full from pre[] and post[].
# preIndex is used to keep track
# of index in pre[]. l is low index
# and h is high index for the
# current subarray in post[]
def constructTreeUtil(pre: list, post: list,
                        l: int, h: int,
                     size: int) -> Node:
    global preIndex

    # Base case
    if (preIndex >= size or l > h):
        return None

    # The first node in preorder traversal
    # is root. So take the node at preIndex
    # from preorder and make it root, and
    # increment preIndex
    root = Node(pre[preIndex])
    preIndex += 1

    # If the current subarray has only
    # one element, no need to recur
    if (l == h or preIndex >= size):
        return root

    # Search the next element
    # of pre[] in post[]
    i = l
    while i <= h:
        if (pre[preIndex] == post[i]):
            break

        i += 1

    # Use the index of element
    # found in postorder to divide
    # postorder array in two parts.
    # Left subtree and right subtree
    if (i <= h):
        root.left = constructTreeUtil(pre, post,
                                      l, i, size)
        root.right = constructTreeUtil(pre, post,
                                       i + 1, h-1,
                                       size)

    return root

# The main function to construct
# Full Binary Tree from given
# preorder and postorder traversals.
# This function mainly uses constructTreeUtil()
def constructTree(pre: list,
                 post: list,
                 size: int) -> Node:

    global preIndex

    return constructTreeUtil(pre, post, 0,
                             size - 1, size)

# A utility function to print
# inorder traversal of a Binary Tree
def printInorder(node: Node) -> None:

    if (node is None):
        return

    printInorder(node.left)
    print(node.data, end = " ")

    printInorder(node.right)

# Driver code
if __name__ == "__main__":

    pre = [ 1, 2, 4, 8, 9, 5, 3, 6, 7 ]
    post = [ 8, 9, 4, 5, 2, 6, 7, 3, 1 ]
    size = len(pre)

    preIndex = 0

    root = constructTree(pre, post, size)

    print("Inorder traversal of "
          "the constructed tree: ")

    printInorder(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program for construction
// of full binary tree
using System;

class GFG
{
// variable to hold index in pre[] array
public static int preindex;

public class node
{
    public int data;
    public node left, right;

    public node(int data)
    {
        this.data = data;
    }
}

// A recursive function to construct Full
// from pre[] and post[]. preIndex is used
// to keep track of index in pre[]. l is
// low index and h is high index for the
// current subarray in post[]
public static node constructTreeUtil(int[] pre, int[] post,
                                     int l, int h, int size)
{

    // Base case
    if (preindex >= size || l > h)
    {
        return null;
    }

    // The first node in preorder traversal is
    // root. So take the node at preIndex from
    // preorder and make it root, and increment
    // preIndex
    node root = new node(pre[preindex]);
    preindex++;

    // If the current subarray has only one
    // element, no need to recur or
    // preIndex > size after incrementing
    if (l == h || preindex >= size)
    {
        return root;
    }
    int i;

    // Search the next element
    // of pre[] in post[]
    for (i = l; i <= h; i++)
    {
        if (post[i] == pre[preindex])
        {
            break;
        }
    }

    // Use the index of element found
    // in postorder to divide postorder
    // array in two parts. Left subtree
    // and right subtree
    if (i <= h)
    {
        root.left = constructTreeUtil(pre, post,
                                      l, i, size);
        root.right = constructTreeUtil(pre, post,
                                       i + 1, h-1, size);
    }
    return root;
}

// The main function to construct Full
// Binary Tree from given preorder and
// postorder traversals. This function
// mainly uses constructTreeUtil()
public static node constructTree(int[] pre,
                                 int[] post, int size)
{
    preindex = 0;
    return constructTreeUtil(pre, post, 0, size - 1, size);
}

public static void printInorder(node root)
{
    if (root == null)
    {
        return;
    }
    printInorder(root.left);
    Console.Write(root.data + " ");
    printInorder(root.right);
}

// Driver Code
public static void Main(string[] args)
{
    int[] pre = new int[] {1, 2, 4, 8, 9, 5, 3, 6, 7};
    int[] post = new int[] {8, 9, 4, 5, 2, 6, 7, 3, 1};

    int size = pre.Length;
    node root = constructTree(pre, post, size);

    Console.WriteLine("Inorder traversal of " +
                      "the constructed tree:");
    printInorder(root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program for construction
// of full binary tree

// variable to hold index in pre[] array
var preindex = 0;

class node
{
    constructor(data)
    {
        this.data = data;
    }
}

// A recursive function to construct Full
// from pre[] and post[]. preIndex is used
// to keep track of index in pre[]. l is
// low index and h is high index for the
// current subarray in post[]
function constructTreeUtil(pre, post, l, h, size)
{

    // Base case
    if (preindex >= size || l > h)
    {
        return null;
    }

    // The first node in preorder traversal is
    // root. So take the node at preIndex from
    // preorder and make it root, and increment
    // preIndex
    var root = new node(pre[preindex]);
    preindex++;

    // If the current subarray has only one
    // element, no need to recur or
    // preIndex > size after incrementing
    if (l == h || preindex >= size)
    {
        return root;
    }
    var i;

    // Search the next element
    // of pre[] in post[]
    for (i = l; i <= h; i++)
    {
        if (post[i] == pre[preindex])
        {
            break;
        }
    }

    // Use the index of element found
    // in postorder to divide postorder
    // array in two parts. Left subtree
    // and right subtree
    if (i <= h)
    {
        root.left = constructTreeUtil(pre, post,
                                      l, i, size);
        root.right = constructTreeUtil(pre, post,
                                       i + 1, h-1, size);
    }
    return root;
}

// The main function to construct Full
// Binary Tree from given preorder and
// postorder traversals. This function
// mainly uses constructTreeUtil()
function constructTree(pre, post, size)
{
    preindex = 0;
    return constructTreeUtil(pre, post, 0, size - 1, size);
}

function printInorder(root)
{
    if (root == null)
    {
        return;
    }
    printInorder(root.left);
    document.write(root.data + " ");
    printInorder(root.right);
}

// Driver Code
var pre = [1, 2, 4, 8, 9, 5, 3, 6, 7];
var post = [8, 9, 4, 5, 2, 6, 7, 3, 1];
var size = pre.length;
var root = constructTree(pre, post, size);
document.write("Inorder traversal of " +
                  "the constructed tree:<br>");
printInorder(root);

</script>
```

**输出:**

```
Inorder traversal of the constructed tree:
8 4 9 2 5 1 6 3 7
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。