# 二叉树中最大的 BST |集合 2

> 原文:[https://www . geesforgeks . org/maximum-BST-二叉树-set-2/](https://www.geeksforgeeks.org/largest-bst-binary-tree-set-2/)

给定一棵二叉树，写一个函数，返回最大的子树的大小，它也是一个二叉查找树树。如果完整的二叉树是 BST，那么返回整个树的大小。
**例:**

```
Input: 
      5
    /  \
   2    4
 /  \
1    3

Output: 3 
The following subtree is the 
maximum size BST subtree 
   2  
 /  \
1    3

Input: 
       50
     /    \
  30       60
 /  \     /  \ 
5   20   45    70
              /  \
            65    80
Output: 5
The following subtree is the
maximum size BST subtree 
      60
     /  \ 
   45    70
        /  \
      65    80
```

## [推荐:请先在“ ***<u>【练习】</u>*** ”上解，再继续解。](https://practice.geeksforgeeks.org/problems/largest-bst/1)

我们在下面的帖子中讨论了两种方法。
[求给定二叉树中最大的 BST 子树|集合 1](https://www.geeksforgeeks.org/find-the-largest-subtree-in-a-tree-that-is-also-a-bst/)
在这篇文章中，讨论了一个不同的 O(n)解。这个解决方案比上面讨论的解决方案更简单，并且在 O(n)时间内有效。
这个想法是基于[的方法 3，检查一个二叉树是否是 BST 文章](https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)。
如果每个节点 x 都符合以下条件，则树为 BST。

1.  (x 的)左子树中的最大值小于 x 的值。
2.  (x 的)右子树中的最小值大于 x 的值。

我们以自下而上的方式遍历树。对于每个遍历的节点，我们返回以它为根的子树中的最大值和最小值。如果任何节点遵循上述
的属性和大小

## C++

```
// C++ program to find largest BST in a
// Binary Tree.
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new
node with the given data and NULL left
and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;

    return(node);
}

// Information to be returned by every
// node in bottom up traversal.
struct Info
{
    int sz; // Size of subtree
    int max; // Min value in subtree
    int min; // Max value in subtree
    int ans; // Size of largest BST which
    // is subtree of current node
    bool isBST; // If subtree is BST
};

// Returns Information about subtree. The
// Information also includes size of largest
// subtree which is a BST.
Info largestBSTBT(Node* root)
{
    // Base cases : When tree is empty or it has
    // one child.
    if (root == NULL)
        return {0, INT_MIN, INT_MAX, 0, true};
    if (root->left == NULL && root->right == NULL)
        return {1, root->data, root->data, 1, true};

    // Recur for left subtree and right subtrees
    Info l = largestBSTBT(root->left);
    Info r = largestBSTBT(root->right);

    // Create a return variable and initialize its
    // size.
    Info ret;
    ret.sz = (1 + l.sz + r.sz);

    // If whole tree rooted under current root is
    // BST.
    if (l.isBST && r.isBST && l.max < root->data &&
            r.min > root->data)
    {
        ret.min = min(l.min, min(r.min, root->data));
        ret.max = max(r.max, max(l.max, root->data));

        // Update answer for tree rooted under
        // current 'root'
        ret.ans = ret.sz;
        ret.isBST = true;

        return ret;
    }

    // If whole tree is not BST, return maximum
    // of left and right subtrees
    ret.ans = max(l.ans, r.ans);
    ret.isBST = false;

    return ret;
}

/* Driver program to test above functions*/
int main()
{
    /* Let us construct the following Tree
        60
       /  \
      65  70
     /
    50 */

    struct Node *root = newNode(60);
    root->left = newNode(65);
    root->right = newNode(70);
    root->left->left = newNode(50);
    printf(" Size of the largest BST is %d\n",
           largestBSTBT(root).ans);
    return 0;
}

// This code is contributed by Vivek Garg in a
// comment on below set 1.
// www.geeksforgeeks.org/find-the-largest-subtree-in-a-tree-that-is-also-a-bst/
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest BST in a Binary Tree.

/* A binary tree node has data, pointer to left child and a pointer to right child */
class Node {
  int data;
  Node left, right;

  public Node(final int d) {
    data = d;
  }
}

class GFG {

  public static void main(String[] args) {

       /* Let us construct the following Tree
        60
       /  \
      65  70
     /
    50 */

    final Node node1 = new Node(60);
    node1.left = new Node(65);
    node1.right = new Node(70);
    node1.left.left = new Node(50);

    System.out.print("Size of the largest BST is " + Solution.largestBst(node1) + "\n");

  }
}

class Solution {
  static int MAX = Integer.MAX_VALUE;
  static int MIN = Integer.MIN_VALUE;

  static class nodeInfo {
    int size; // Size of subtree
    int max; // Min value in subtree
    int min; // Max value in subtree
    boolean isBST; // If subtree is BST

    nodeInfo() {
    }

    nodeInfo(int size, int max, int min, boolean isBST) {
      this.size = size;
      this.max = max;
      this.min = min;
      this.isBST = isBST;
    }
  }

  static nodeInfo largestBST(Node root) {

    // Base cases : When tree is empty or it has one child.
    if (root == null) {
      return new nodeInfo(0, MIN, MAX, true);
    }
    if (root.left == null && root.right == null) {
      return new nodeInfo(1, root.data, root.data, true);
    }

    // Recur for left subtree and right subtrees
    nodeInfo left = largestBST(root.left);
    nodeInfo right = largestBST(root.right);

    // Create a return variable and initialize its size.
    nodeInfo returnInfo = new nodeInfo();

    // If whole tree rooted under current root is BST.
    if (left.isBST && right.isBST && left.max < root.data && right.min > root.data) {
      returnInfo.min = Math.min(Math.min(left.min, right.min), root.data);
      returnInfo.max = Math.max(Math.max(left.max, right.max), root.data);

      // Update answer for tree rooted under current 'root'
      returnInfo.size = left.size + 1 + right.size;
      returnInfo.isBST = true;
      return returnInfo;
    }

    // If whole tree is not BST, return maximum of left and right subtrees
    returnInfo.size = Math.max(left.size, right.size);
    returnInfo.isBST = false;
    return returnInfo;
  }

  // Return the size of the largest sub-tree which is also a BST
  static int largestBst(Node root) {
    return largestBST(root).size;
  }
}
// This code is contributed by Andrei Sljusar
```

## 蟒蛇 3

```
# Python program to find largest
# BST in a Binary Tree.

INT_MIN = -2147483648
INT_MAX = 2147483647

# Helper function that allocates a new
# node with the given data and None left
# and right pointers.
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Returns Information about subtree. The
# Information also includes size of largest
# subtree which is a BST
def largestBSTBT(root):

# Base cases : When tree is empty or it has
    # one child.
    if (root == None):
        return 0, INT_MIN, INT_MAX, 0, True
    if (root.left == None and root.right == None) :
        return 1, root.data, root.data, 1, True

    # Recur for left subtree and right subtrees
    l = largestBSTBT(root.left)
    r = largestBSTBT(root.right)

    # Create a return variable and initialize its
    # size.
    ret = [0, 0, 0, 0, 0]
    ret[0] = (1 + l[0] + r[0])

    # If whole tree rooted under current root is
    # BST.
    if (l[4] and r[4] and l[1] <
        root.data and r[2] > root.data) :

        ret[2] = min(l[2], min(r[2], root.data))
        ret[1] = max(r[1], max(l[1], root.data))

        # Update answer for tree rooted under
        # current 'root'
        ret[3] = ret[0]
        ret[4] = True

        return ret

    # If whole tree is not BST, return maximum
    # of left and right subtrees
    ret[3] = max(l[3], r[3])
    ret[4] = False

    return ret

# Driver Code
if __name__ == '__main__':

    """Let us construct the following Tree
        60
        / \
        65 70
    /
    50 """
    root = newNode(60)
    root.left = newNode(65)
    root.right = newNode(70)
    root.left.left = newNode(50)
    print("Size of the largest BST is",
                    largestBSTBT(root)[3])

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

**Output**

```
 Size of the largest BST is 2
```

**时间复杂度:** O(n)
本文由**舒巴姆·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。