# 从给定的后序

构建二叉查找树

> 原文:[https://www . geesforgeks . org/construct-a-binary-search-tree-from-给定-post-order/](https://www.geeksforgeeks.org/construct-a-binary-search-tree-from-given-postorder/)

给定二叉查找树的后序遍历，构造 BST。
例如，如果给定的遍历是{1，7，5，50，40，10}，那么应该构造下面的树，并返回树的根。

```
     10
   /   \
  5     40
 /  \      \
1    7      50
```

**方法 1 ( O(n^2)时间复杂度)**
后序遍历的最后一个元素总是根。我们首先构造根。然后我们找到小于根的最后一个元素的索引。让索引为“I”。0 和 I 之间的值是左子树的一部分，i+1 和 n-2 之间的值是右子树的一部分。在索引“I”处划分给定的帖子[]并对左右子树重复出现。
例如在{1，7，5，50，40，10}中，10 是最后一个元素，所以我们把它设为 root。现在我们寻找小于 10 的最后一个元素，我们找到 5。所以我们知道 BST 的结构如下。

```
             10
           /    \
          /      \
  {1, 7, 5}       {50, 40}
```

对于子阵列{1，7，5}和{40，50}，我们递归地遵循上述步骤，并获得完整的树。
**方法 2 ( O(n)时间复杂度)**
诀窍是设置一个范围{min..最大值)。将范围初始化为{INT_MIN..INT_MAX}。最后一个节点肯定在范围内，所以创建根节点。要构建左子树，请将范围设置为{INT_MIN …root- > data}。如果值在{ INT _ MIN 范围内..根- >数据}，值是左子树的一部分。要构建右子树，请将范围设置为{根- >数据..INT_MAX}。
下面的代码用于生成给定后序遍历的精确二叉查找树。

## C++

```
/* A O(n) program for construction of
BST from postorder traversal */
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
struct node
{
    int data;
    struct node *left, *right;
};

// A utility function to create a node
struct node* newNode (int data)
{
    struct node* temp =
(struct node *) malloc(sizeof(struct node));

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct
// BST from post[]. postIndex is used
// to keep track of index in post[].
struct node* constructTreeUtil(int post[], int* postIndex,
                               int key, int min, int max,
                               int size)
{
    // Base case
    if (*postIndex < 0)
        return NULL;

    struct node* root = NULL;

    // If current element of post[] is
    // in range, then only it is part
    // of current subtree
    if (key > min && key < max)
    {
        // Allocate memory for root of this
        // subtree and decrement *postIndex
        root = newNode(key);
        *postIndex = *postIndex - 1;

        if (*postIndex >= 0)
        {

        // All nodes which are in range {key..max}
        // will go in right subtree, and first such
        // node will be root of right subtree.
        root->right = constructTreeUtil(post, postIndex,
                                        post[*postIndex],
                                        key, max, size );

        // Construct the subtree under root
        // All nodes which are in range {min .. key}
        // will go in left subtree, and first such
        // node will be root of left subtree.
        root->left = constructTreeUtil(post, postIndex,
                                       post[*postIndex],
                                       min, key, size );
        }
    }
    return root;
}

// The main function to construct BST
// from given postorder traversal.
// This function mainly uses constructTreeUtil()
struct node *constructTree (int post[],
                            int size)
{
    int postIndex = size-1;
    return constructTreeUtil(post, &postIndex,
                             post[postIndex],
                             INT_MIN, INT_MAX, size);
}

// A utility function to print
// inorder traversal of a Binary Tree
void printInorder (struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout << node->data << " ";
    printInorder(node->right);
}

// Driver Code
int main ()
{
    int post[] = {1, 7, 5, 50, 40, 10};
    int size = sizeof(post) / sizeof(post[0]);

    struct node *root = constructTree(post, size);

    cout << "Inorder traversal of "
        << "the constructed tree: \n";
    printInorder(root);

    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
/* A O(n) program for construction of BST from
   postorder traversal */
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node *left, *right;
};

// A utility function to create a node
struct node* newNode (int data)
{
    struct node* temp =
        (struct node *) malloc( sizeof(struct node));

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct BST from post[].
// postIndex is used to keep track of index in post[].
struct node* constructTreeUtil(int post[], int* postIndex,
                         int key, int min, int max, int size)
{
    // Base case
    if (*postIndex < 0)
        return NULL;

    struct node* root = NULL;

    // If current element of post[] is in range, then
    // only it is part of current subtree
    if (key > min && key < max)
    {
        // Allocate memory for root of this subtree and decrement
        // *postIndex
        root = newNode(key);
        *postIndex = *postIndex - 1;

        if (*postIndex >= 0)
        {

          // All nodes which are in range {key..max} will go in right
          // subtree, and first such node will be root of right subtree.
          root->right = constructTreeUtil(post, postIndex, post[*postIndex],
                                          key, max, size );

          // Construct the subtree under root
          // All nodes which are in range {min .. key} will go in left
          // subtree, and first such node will be root of left subtree.
          root->left = constructTreeUtil(post, postIndex, post[*postIndex],
                                         min, key, size );
        }
    }
    return root;
}

// The main function to construct BST from given postorder
// traversal. This function mainly uses constructTreeUtil()
struct node *constructTree (int post[], int size)
{
    int postIndex = size-1;
    return constructTreeUtil(post, &postIndex, post[postIndex],
                             INT_MIN, INT_MAX, size);
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
    int post[] = {1, 7, 5, 50, 40, 10};
    int size = sizeof(post) / sizeof(post[0]);

    struct node *root = constructTree(post, size);

    printf("Inorder traversal of the constructed tree: \n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A O(n) program for construction of BST from
   postorder traversal */

 /* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right;

    Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class containing variable that keeps a track of overall
// calculated postindex
class Index
{
    int postindex = 0;
}

class BinaryTree
{
    // A recursive function to construct BST from post[].
    // postIndex is used to keep track of index in post[].
    Node constructTreeUtil(int post[], Index postIndex,
            int key, int min, int max, int size)
    {
        // Base case
        if (postIndex.postindex < 0)
            return null;

        Node root = null;

        // If current element of post[] is in range, then
        // only it is part of current subtree
        if (key > min && key < max)
        {
            // Allocate memory for root of this subtree and decrement
            // *postIndex
            root = new Node(key);
            postIndex.postindex = postIndex.postindex - 1;

            if (postIndex.postindex >= 0)
            {
                // All nodes which are in range {key..max} will go in
                // right subtree, and first such node will be root of right
                // subtree
                root.right = constructTreeUtil(post, postIndex,
                        post[postIndex.postindex],key, max, size);

                // Construct the subtree under root
                // All nodes which are in range {min .. key} will go in left
                // subtree, and first such node will be root of left subtree.
                root.left = constructTreeUtil(post, postIndex,
                        post[postIndex.postindex],min, key, size);
            }
        }
        return root;
    }

    // The main function to construct BST from given postorder
    // traversal. This function mainly uses constructTreeUtil()
    Node constructTree(int post[], int size)
    {
        Index index = new Index();
        index.postindex = size - 1;
        return constructTreeUtil(post, index, post[index.postindex],
                Integer.MIN_VALUE, Integer.MAX_VALUE, size);
    }

    // A utility function to print inorder traversal of a Binary Tree
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        int post[] = new int[]{1, 7, 5, 50, 40, 10};
        int size = post.length;

        Node root = tree.constructTree(post, size);

        System.out.println("Inorder traversal of the constructed tree:");
        tree.printInorder(root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# A O(n) program for construction of BST
# from postorder traversal
INT_MIN = -2**31
INT_MAX = 2**31

# A binary tree node has data, pointer to
# left child and a pointer to right child
# A utility function to create a node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# A recursive function to construct
# BST from post[]. postIndex is used
# to keep track of index in post[].
def constructTreeUtil(post, postIndex,
                      key, min, max, size):

    # Base case
    if (postIndex[0] < 0):
        return None

    root = None

    # If current element of post[] is
    # in range, then only it is part
    # of current subtree
    if (key > min and key < max) :

        # Allocate memory for root of this
        # subtree and decrement *postIndex
        root = newNode(key)
        postIndex[0] = postIndex[0] - 1

        if (postIndex[0] >= 0) :

            # All nodes which are in range key..
            # max will go in right subtree, and
            # first such node will be root of
            # right subtree.
            root.right = constructTreeUtil(post, postIndex,
                                           post[postIndex[0]],
                                           key, max, size )

            # Construct the subtree under root
            # All nodes which are in range min ..
            # key will go in left subtree, and
            # first such node will be root of
            # left subtree.
            root.left = constructTreeUtil(post, postIndex,
                                          post[postIndex[0]],
                                          min, key, size )

    return root

# The main function to construct BST
# from given postorder traversal. This
# function mainly uses constructTreeUtil()
def constructTree (post, size) :

    postIndex = [size-1]
    return constructTreeUtil(post, postIndex,
                             post[postIndex[0]],
                             INT_MIN, INT_MAX, size)

# A utility function to prinorder
# traversal of a Binary Tree
def printInorder (node) :

    if (node == None) :
        return
    printInorder(node.left)
    print(node.data, end = " ")
    printInorder(node.right)

# Driver Code
if __name__ == '__main__':
    post = [1, 7, 5, 50, 40, 10]
    size = len(post)

    root = constructTree(post, size)

    print("Inorder traversal of the",
                "constructed tree: ")
    printInorder(root)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
using System;
/* A O(n) program for
construction of BST from
postorder traversal */

/* A binary tree node has data,
pointer to left child and a
 pointer to right child */
class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class containing variable
// that keeps a track of overall
// calculated postindex
class Index
{
    public int postindex = 0;
}

public class BinaryTree
{
    // A recursive function to
    // construct BST from post[].
    // postIndex is used to
    // keep track of index in post[].
    Node constructTreeUtil(int []post, Index postIndex,
                    int key, int min, int max, int size)
    {
        // Base case
        if (postIndex.postindex < 0)
            return null;

        Node root = null;

        // If current element of post[] is in range, then
        // only it is part of current subtree
        if (key > min && key < max)
        {
            // Allocate memory for root of 
            // this subtree and decrement *postIndex
            root = new Node(key);
            postIndex.postindex = postIndex.postindex - 1;

            if (postIndex.postindex >= 0)
            {
                // All nodes which are in range
                // {key..max} will go in right subtree,
                // and first such node will be root of
                // right subtree
                root.right = constructTreeUtil(post, postIndex,
                        post[postIndex.postindex], key, max, size);

                // Construct the subtree under root
                // All nodes which are in range
                // {min .. key} will go in left
                // subtree, and first such node
                // will be root of left subtree.
                root.left = constructTreeUtil(post, postIndex,
                        post[postIndex.postindex],min, key, size);
            }
        }
        return root;
    }

    // The main function to construct
    // BST from given postorder traversal.
    // This function mainly uses constructTreeUtil()
    Node constructTree(int []post, int size)
    {
        Index index = new Index();
        index.postindex = size - 1;
        return constructTreeUtil(post, index,
                        post[index.postindex],
                        int.MinValue, int.MaxValue, size);
    }

    // A utility function to print
    // inorder traversal of a Binary Tree
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver code
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        int []post = new int[]{1, 7, 5, 50, 40, 10};
        int size = post.Length;

        Node root = tree.constructTree(post, size);

        Console.WriteLine("Inorder traversal of" +
                            "the constructed tree:");
        tree.printInorder(root);
    }
}

// This code has been contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

      /* A O(n) program for
construction of BST from
postorder traversal */

      /* A binary tree node has data,
pointer to left child and a
 pointer to right child */
      class Node {
        constructor(data) {
          this.data = data;
          this.left = null;
          this.right = null;
        }
      }

      // Class containing variable
      // that keeps a track of overall
      // calculated postindex
      class Index {
        constructor() {
          this.postindex = 0;
        }
      }

      class BinaryTree {
        // A recursive function to
        // construct BST from post[].
        // postIndex is used to
        // keep track of index in post[].
        constructTreeUtil(post, postIndex, key, min, max, size) {
          // Base case
          if (postIndex.postindex < 0) return null;

          var root = null;

          // If current element of post[] is in range, then
          // only it is part of current subtree
          if (key > min && key < max) {
            // Allocate memory for root of
            // this subtree and decrement *postIndex
            root = new Node(key);
            postIndex.postindex = postIndex.postindex - 1;

            if (postIndex.postindex >= 0) {
              // All nodes which are in range
              // {key..max} will go in right subtree,
              // and first such node will be root of
              // right subtree
              root.right = this.constructTreeUtil(
                post,
                postIndex,
                post[postIndex.postindex],
                key,
                max,
                size
              );

              // Construct the subtree under root
              // All nodes which are in range
              // {min .. key} will go in left
              // subtree, and first such node
              // will be root of left subtree.
              root.left = this.constructTreeUtil(
                post,
                postIndex,
                post[postIndex.postindex],
                min,
                key,
                size
              );
            }
          }
          return root;
        }

        // The main function to construct
        // BST from given postorder traversal.
        // This function mainly uses constructTreeUtil()
        constructTree(post, size) {
          var index = new Index();
          index.postindex = size - 1;
          return this.constructTreeUtil(
            post,
            index,
            post[index.postindex],
            -2147483648,
            2147483647,
            size
          );
        }

        // A utility function to print
        // inorder traversal of a Binary Tree
        printInorder(node) {
          if (node == null) return;
          this.printInorder(node.left);
          document.write(node.data + " ");
          this.printInorder(node.right);
        }
      }
      // Driver code
      var tree = new BinaryTree();
      var post = [1, 7, 5, 50, 40, 10];
      var size = post.length;

      var root = tree.constructTree(post, size);

      document.write("Inorder traversal of " +
      "the constructed tree: <br>");
      tree.printInorder(root);

</script>
```

**输出:**

```
Inorder traversal of the constructed tree: 
1 5 7 10 40 50 
```

*注意，当我们打印二叉查找树的有序遍历时，程序的输出将总是一个排序的序列。*

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息