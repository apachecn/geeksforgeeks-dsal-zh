# 利用二叉树的前序遍历和镜像树的前序遍历来构造全二叉树

> 原文:[https://www . geesforgeks . org/construct-full-二叉树-use-preorder-遍历-preorder-遍历-镜像-tree/](https://www.geeksforgeeks.org/construct-full-binary-tree-using-preorder-traversal-preorder-traversal-mirror-tree/)

给定两个数组来表示完整二叉树及其镜像树的 Preorder 遍历，我们需要编写一个程序来使用这两个 Preorder 遍历来构造二叉树。
一个**完全二叉树**是一个二叉树，其中每个节点有 0 或 2 个子节点。

**注**:用这两个遍历不可能构造出一般的二叉树。但是我们可以使用上面的遍历创建一个完整的二叉树，没有任何歧义。更多详情请参考[这篇](https://www.geeksforgeeks.org/if-you-are-given-two-traversal-sequences-can-you-construct-the-binary-tree/)文章。

**示例:**

```
Input :  preOrder[] = {1,2,4,5,3,6,7}
         preOrderMirror[] = {1,3,7,6,2,5,4}

Output :          1
               /    \
              2      3
            /   \   /  \
           4     5 6    7
```

*   **方法 1** :我们把给定的两个数组看作 preOrder[] = {1，2，4，5，3，6，7}和 preOrderMirror[] = {1，3，7，6，2，5，4}。
    在 preOrder[]和 preOrderMirror[]中，最左边的元素都是树根。由于树已满且数组大小大于 1。preOrder[]中 1 旁边的值必须是根的左子级，preOrderMirror[]中 1 旁边的值必须是根的右子级。所以我们知道 1 是根，2 是左子，3 是右子。如何找到左子树中的所有节点？我们知道 2 是左子树中所有节点的根，3 是右子树中所有节点的根。preOrderMirror[]中来自和 2 的所有节点必须位于根节点 1 的左子树中，preOrderMirror[]中 3 之后和 2 之前的所有节点必须位于根节点 1 的右子树中。现在我们知道 1 是根，元素{2，5，4}在左子树，元素{3，7，6}在右子树。

```
           1
        /    \
       /      \
    {2,5,4}  {3,7,6}
```

*   我们将递归地遵循上面的方法，得到下面的树:

```
                  1
               /    \
              2      3
            /   \   /  \
           4     5 6    7
```

下面是上述方法的实现:

## C++

```
// C++ program to construct full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree

#include<bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to print inorder traversal
// of a Binary Tree
void printInorder(Node* node)
{
    if (node == NULL)
        return;

    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

// A recursive function to construct Full binary tree
//  from pre[] and preM[]. preIndex is used to keep
// track of index in pre[]. l is low index and h is high
//index for the current subarray in preM[]
Node* constructBinaryTreeUtil(int pre[], int preM[],
                    int &preIndex, int l,int h,int size)
{   
    // Base case
    if (preIndex >= size || l > h)
        return NULL;

    // The first node in preorder traversal is root.
    // So take the node at preIndex from preorder and
    // make it root, and increment preIndex
    Node* root = newNode(pre[preIndex]);
        ++(preIndex);

    // If the current subarray has only one element,
    // no need to recur
    if (l == h)
        return root;

    // Search the next element of pre[] in preM[]
    int i;
    for (i = l; i <= h; ++i)
        if (pre[preIndex] == preM[i])
            break;

    // construct left and right subtrees recursively   
    if (i <= h)
    {
        root->left = constructBinaryTreeUtil (pre, preM,
                                    preIndex, i, h, size);
        root->right = constructBinaryTreeUtil (pre, preM,
                                 preIndex, l+1, i-1, size);
    }

     // return root
    return root;   
}

// function to construct full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree
void constructBinaryTree(Node* root,int pre[],
                        int preMirror[], int size)
{
    int preIndex = 0;
    int preMIndex = 0;

    root =  constructBinaryTreeUtil(pre,preMirror,
                            preIndex,0,size-1,size);

    printInorder(root);
}

// Driver program to test above functions
int main()
{
    int preOrder[] = {1,2,4,5,3,6,7};
    int preOrderMirror[] = {1,3,7,6,2,5,4};

    int size = sizeof(preOrder)/sizeof(preOrder[0]);

    Node* root = new Node;

    constructBinaryTree(root,preOrder,preOrderMirror,size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree
class GFG
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};
static class INT
{
    int a;
    INT(int a){this.a=a;}
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to print inorder traversal
// of a Binary Tree
static void printInorder(Node node)
{
    if (node == null)
        return;

    printInorder(node.left);
    System.out.printf("%d ", node.data);
    printInorder(node.right);
}

// A recursive function to con Full binary tree
// from pre[] and preM[]. preIndex is used to keep
// track of index in pre[]. l is low index and h is high
//index for the current subarray in preM[]
static Node conBinaryTreeUtil(int pre[], int preM[],
                    INT preIndex, int l, int h, int size)
{
    // Base case
    if (preIndex.a >= size || l > h)
        return null;

    // The first node in preorder traversal is root.
    // So take the node at preIndex from preorder and
    // make it root, and increment preIndex
    Node root = newNode(pre[preIndex.a]);
        ++(preIndex.a);

    // If the current subarray has only one element,
    // no need to recur
    if (l == h)
        return root;

    // Search the next element of pre[] in preM[]
    int i;
    for (i = l; i <= h; ++i)
        if (pre[preIndex.a] == preM[i])
            break;

    // con left and right subtrees recursively
    if (i <= h)
    {
        root.left = conBinaryTreeUtil (pre, preM,
                                    preIndex, i, h, size);
        root.right = conBinaryTreeUtil (pre, preM,
                                preIndex, l + 1, i - 1, size);
    }

    // return root
    return root;    
}

// function to con full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree
static void conBinaryTree(Node root,int pre[],
                        int preMirror[], int size)
{
    INT preIndex = new INT(0);
    int preMIndex = 0;

    root = conBinaryTreeUtil(pre,preMirror,
                            preIndex, 0, size - 1, size);

    printInorder(root);
}

// Driver code
public static void main(String args[])
{
    int preOrder[] = {1,2,4,5,3,6,7};
    int preOrderMirror[] = {1,3,7,6,2,5,4};

    int size = preOrder.length;

    Node root = new Node();

    conBinaryTree(root,preOrder,preOrderMirror,size);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to construct full binary
# tree using its preorder traversal and
# preorder traversal of its mirror tree

# Utility function to create a new tree node
class newNode:
    def __init__(self,data):
        self.data = data
        self.left = self.right = None

# A utility function to print inorder
# traversal of a Binary Tree
def prInorder(node):
    if (node == None) :
        return
    prInorder(node.left)
    print(node.data, end = " ")
    prInorder(node.right)

# A recursive function to construct Full 
# binary tree from pre[] and preM[].
# preIndex is used to keep track of index
# in pre[]. l is low index and h is high
# index for the current subarray in preM[]
def constructBinaryTreeUtil(pre, preM, preIndex,
                                    l, h, size):
    # Base case
    if (preIndex >= size or l > h) :
        return None , preIndex

    # The first node in preorder traversal 
    # is root. So take the node at preIndex
    # from preorder and make it root, and
    # increment preIndex
    root = newNode(pre[preIndex])
    preIndex += 1

    # If the current subarray has only
    # one element, no need to recur
    if (l == h):
        return root, preIndex

    # Search the next element of
    # pre[] in preM[]
    i = 0
    for i in range(l, h + 1):
        if (pre[preIndex] == preM[i]):
                break

    # construct left and right subtrees
    # recursively
    if (i <= h):

        root.left, preIndex = constructBinaryTreeUtil(pre, preM, preIndex,
                                                               i, h, size)
        root.right, preIndex = constructBinaryTreeUtil(pre, preM, preIndex,
                                                       l + 1, i - 1, size)

    # return root
    return root, preIndex

# function to construct full binary tree
# using its preorder traversal and preorder
# traversal of its mirror tree
def constructBinaryTree(root, pre, preMirror, size):

    preIndex = 0
    preMIndex = 0

    root, x = constructBinaryTreeUtil(pre, preMirror, preIndex,
                                             0, size - 1, size)

    prInorder(root)

# Driver code
if __name__ =="__main__":

    preOrder = [1, 2, 4, 5, 3, 6, 7]
    preOrderMirror = [1, 3, 7, 6, 2, 5, 4]

    size = 7
    root = newNode(0)

    constructBinaryTree(root, preOrder,
                        preOrderMirror, size)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to construct full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree
using System;

class GFG
{

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
};
public class INT
{
    public int a;
    public INT(int a){this.a=a;}
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to print inorder traversal
// of a Binary Tree
static void printInorder(Node node)
{
    if (node == null)
        return;

    printInorder(node.left);
    Console.Write("{0} ", node.data);
    printInorder(node.right);
}

// A recursive function to con Full binary tree
// from pre[] and preM[]. preIndex is used to keep
// track of index in pre[]. l is low index and h is high
//index for the current subarray in preM[]
static Node conBinaryTreeUtil(int []pre, int []preM,
                    INT preIndex, int l, int h, int size)
{
    // Base case
    if (preIndex.a >= size || l > h)
        return null;

    // The first node in preorder traversal is root.
    // So take the node at preIndex from preorder and
    // make it root, and increment preIndex
    Node root = newNode(pre[preIndex.a]);
        ++(preIndex.a);

    // If the current subarray has only one element,
    // no need to recur
    if (l == h)
        return root;

    // Search the next element of pre[] in preM[]
    int i;
    for (i = l; i <= h; ++i)
        if (pre[preIndex.a] == preM[i])
            break;

    // con left and right subtrees recursively
    if (i <= h)
    {
        root.left = conBinaryTreeUtil (pre, preM,
                                    preIndex, i, h, size);
        root.right = conBinaryTreeUtil (pre, preM,
                                preIndex, l + 1, i - 1, size);
    }

    // return root
    return root;    
}

// function to con full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree
static void conBinaryTree(Node root,int []pre,
                        int []preMirror, int size)
{
    INT preIndex = new INT(0);
    int preMIndex = 0;

    root = conBinaryTreeUtil(pre,preMirror,
                            preIndex, 0, size - 1, size);

    printInorder(root);
}

// Driver code
public static void Main(String []args)
{
    int []preOrder = {1,2,4,5,3,6,7};
    int []preOrderMirror = {1,3,7,6,2,5,4};

    int size = preOrder.Length;

    Node root = new Node();

    conBinaryTree(root,preOrder,preOrderMirror,size);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to construct full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree

// A Binary Tree Node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

class INT
{
    constructor(a)
    {
        this.a = a;
    }
}

// Utility function to create a new tree node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to print inorder traversal
// of a Binary Tree
function printInorder(node)
{
    if (node == null)
        return;

    printInorder(node.left);
    document.write(node.data + " ");
    printInorder(node.right);
}

// A recursive function to con Full binary tree
// from pre[] and preM[]. preIndex is used to keep
// track of index in pre[]. l is low index and h is high
//index for the current subarray in preM[]
function conBinaryTreeUtil(pre, preM, preIndex, l, h, size)
{
    // Base case
    if (preIndex.a >= size || l > h)
        return null;

    // The first node in preorder traversal is root.
    // So take the node at preIndex from preorder and
    // make it root, and increment preIndex
    var root = newNode(pre[preIndex.a]);
        ++(preIndex.a);

    // If the current subarray has only one element,
    // no need to recur
    if (l == h)
        return root;

    // Search the next element of pre[] in preM[]
    var i;
    for (i = l; i <= h; ++i)
        if (pre[preIndex.a] == preM[i])
            break;

    // con left and right subtrees recursively
    if (i <= h)
    {
        root.left = conBinaryTreeUtil (pre, preM,
                                    preIndex, i, h, size);
        root.right = conBinaryTreeUtil (pre, preM,
                                preIndex, l + 1, i - 1, size);
    }

    // return root
    return root;    
}

// function to con full binary tree
// using its preorder traversal and preorder
// traversal of its mirror tree
function conBinaryTree(root,pre, preMirror, size)
{
    var preIndex = new INT(0);
    var preMIndex = 0;

    root = conBinaryTreeUtil(pre,preMirror,
                            preIndex, 0, size - 1, size);

    printInorder(root);
}

// Driver code
var preOrder = [1,2,4,5,3,6,7];
var preOrderMirror = [1,3,7,6,2,5,4];
var size = preOrder.length;
var root = new Node();
conBinaryTree(root,preOrder,preOrderMirror,size);

</script>
```

**输出:**

```
4 2 5 1 6 3 7 
```

*   **方法二**:如果我们仔细观察，那么镜像树的前序遍历的逆将是原树的后序遍历。我们可以用与上面类似的方式从给定的前序和后序遍历来构建树。你可以参考[这篇](https://www.geeksforgeeks.org/full-and-complete-binary-tree-from-given-preorder-and-postorder-traversals/)关于如何从给定的前序和后序遍历构造全二叉树的文章。

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。