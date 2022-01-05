# 弯曲次数最多的路径长度

> 原文:[https://www . geesforgeks . org/path-length-maximum-number-bends/](https://www.geeksforgeeks.org/path-length-maximum-number-bends/)

给定一棵二叉树，找出弯曲次数最多的路径长度。
**注意:**这里，弯曲表示在树中穿行时从左向右切换，反之亦然。
例如，考虑以下路径(L 表示向左移动，R 表示向右移动):
LLRRRR–1 弯
RLLLRR–2 弯
lrlrlrr–5 弯
**先决条件:** [在二叉树中找到最大路径长度](https://www.geeksforgeeks.org/longest-path-values-binary-tree/)
**示例:**

```
Input : 
            4
          /   \
        2      6
      /  \    / \
    1     3  5   7
                /
               9
              / \
             12 10
                  \
                  11
                  / \
                45  13
                      \
                      14

Output : 6
In the above example, the path 4-> 6-> 7-> 9-> 10-> 11-> 45
is having the maximum number of bends, i.e., 3\. 
The length of this path is 6\. 
```

**方法:**
思想是遍历树寻找根的左右子树。穿越时，跟踪运动方向(左或右)。无论何时，运动方向从左向右改变，反之亦然，将当前路径中的弯曲数量增加 1。
到达叶节点后，将当前路径中的弯曲数与根到叶路径中迄今为止看到的最大弯曲数(即最大弯曲数)进行比较。如果当前路径中的弯曲数大于最大弯曲数，则更新最大弯曲数等于当前路径中的弯曲数，并将最大路径长度(即 len)也更新为当前路径的长度。
**实施:**

## C++

```
// C++ program to find path length
// having maximum number of bends
#include <bits/stdc++.h>
using namespace std;

// structure node
struct Node {
    int key;
    struct Node* left;
    struct Node* right;
};

// Utility function to create a new node
struct Node* newNode(int key)
{
    struct Node* node = new Node();
    node->left = NULL;
    node->right = NULL;
    node->key = key;

    return node;
}

/* Recursive function to calculate the path
length having maximum number of bends.
The following are parameters for this function.

node --> pointer to the current node
dir --> determines whether the current node
is left or right child of it's parent node
bends --> number of bends so far in the
current path.
maxBends --> maximum number of bends in a
path from root to leaf
soFar --> length of the current path so
far traversed
len --> length of the path having maximum
number of bends
*/
void findMaxBendsUtil(struct Node* node,
                      char dir, int bends,
                      int* maxBends, int soFar,
                      int* len)
{
    // Base Case
    if (node == NULL)
        return;

    // Leaf node
    if (node->left == NULL && node->right == NULL) {
        if (bends > *maxBends) {
            *maxBends = bends;
            *len = soFar;
        }
    }
    // Recurring for both left and right child
    else {
        if (dir == 'l') {
            findMaxBendsUtil(node->left, dir,
                             bends, maxBends,
                             soFar + 1, len);
            findMaxBendsUtil(node->right, 'r',
                             bends + 1, maxBends,
                             soFar + 1, len);
        }
        else {
            findMaxBendsUtil(node->right, dir,
                             bends, maxBends,
                             soFar + 1, len);
            findMaxBendsUtil(node->left, 'l',
                             bends + 1, maxBends,
                             soFar + 1, len);
        }
    }
}

// Helper function to call findMaxBendsUtil()
int findMaxBends(struct Node* node)
{
    if (node == NULL)
        return 0;

    int len = 0, bends = 0, maxBends = -1;

    // Call for left subtree of the root
    if (node->left)
        findMaxBendsUtil(node->left, 'l',
                         bends, &maxBends, 1, &len);

    // Call for right subtree of the root
    if (node->right)
        findMaxBendsUtil(node->right, 'r', bends,
                         &maxBends, 1, &len);

    // Include the root node as well in the path length
    len++;

    return len;
}

// Driver code
int main()
{
    /* Constructed binary tree is
      10
      / \
     8    2
    / \  /
    3  5 2
          \
           1
          /
         9
    */

    struct Node* root = newNode(10);
    root->left = newNode(8);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->left = newNode(2);
    root->right->left->right = newNode(1);
    root->right->left->right->left = newNode(9);

    cout << findMaxBends(root) - 1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find path length
// having maximum number of bends
import java.util.*;
class GFG
{

  // structure node
  static class Node
  {
    int key;
    Node left;
    Node right;
  };

  // Utility function to create a new node
  static Node newNode(int key)
  {
    Node node = new Node();
    node.left = null;
    node.right = null;
    node.key = key;
    return node;
  }

  /* Recursive function to calculate the path
length having maximum number of bends.
The following are parameters for this function.

node -. pointer to the current node
dir -. determines whether the current node
is left or right child of it's parent node
bends -. number of bends so far in the
current path.
maxBends -. maximum number of bends in a
path from root to leaf
soFar -. length of the current path so
far traversed
len -. length of the path having maximum
number of bends
*/
  static int maxBends;
  static int len;
  static void findMaxBendsUtil(Node node,
                               char dir, int bends,
                               int soFar)
  {

    // Base Case
    if (node == null)
      return;

    // Leaf node
    if (node.left == null && node.right == null)
    {
      if (bends > maxBends)
      {
        maxBends = bends;
        len = soFar;
      }
    }

    // Recurring for both left and right child
    else
    {
      if (dir == 'l')
      {
        findMaxBendsUtil(node.left, dir,
                         bends,
                         soFar + 1);
        findMaxBendsUtil(node.right, 'r',
                         bends + 1,
                         soFar + 1);
      }
      else
      {
        findMaxBendsUtil(node.right, dir,
                         bends,
                         soFar + 1);
        findMaxBendsUtil(node.left, 'l',
                         bends + 1,
                         soFar + 1);
      }
    }
  }

  // Helper function to call findMaxBendsUtil()
  static int findMaxBends(Node node)
  {
    if (node == null)
      return 0;
    len = 0;
    maxBends = -1;
    int bends = 0;

    // Call for left subtree of the root
    if (node.left != null)
      findMaxBendsUtil(node.left, 'l',
                       bends, 1);

    // Call for right subtree of the root
    if (node.right != null)
      findMaxBendsUtil(node.right, 'r', bends,
                       1);

    // Include the root node as well in the path length
    len++;
    return len;
  }

  // Driver code
  public static void main(String[] args)
  {
    /* Constructed binary tree is
      10
      / \
     8    2
    / \  /
    3  5 2
          \
           1
          /
         9
    */

    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.left = newNode(2);
    root.right.left.right = newNode(1);
    root.right.left.right.left = newNode(9);

    System.out.print(findMaxBends(root) - 1);
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find path Length
# having maximum number of bends

# Utility function to create a new node
class newNode:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.key = key

# Recursive function to calculate the path
# Length having maximum number of bends.
# The following are parameters for this function.

# node -. pointer to the current node
# Dir -. determines whether the current node
# is left or right child of it's parent node
# bends -. number of bends so far in the
# current path.
# maxBends -. maximum number of bends in a
# path from root to leaf
# soFar -. Length of the current path so
# far traversed
# Len -. Length of the path having maximum
# number of bends

def findMaxBendsUtil(node, Dir, bends,
                     maxBends, soFar, Len):

    # Base Case
    if (node == None):
        return

    # Leaf node
    if (node.left == None and
        node.right == None):
        if (bends > maxBends[0]):
            maxBends[0] = bends
            Len[0] = soFar

    # Having both left and right child
    else:
        if (Dir == 'l'):
            findMaxBendsUtil(node.left, Dir, bends,
                             maxBends, soFar + 1, Len)
            findMaxBendsUtil(node.right, 'r', bends + 1,
                             maxBends, soFar + 1, Len)
        else:
            findMaxBendsUtil(node.right, Dir, bends,
                             maxBends, soFar + 1, Len)
            findMaxBendsUtil(node.left, 'l', bends + 1,
                             maxBends, soFar + 1, Len)

# Helper function to call findMaxBendsUtil()
def findMaxBends(node):
    if (node == None):
        return 0

    Len = [0]
    bends = 0
    maxBends = [-1]

    # Call for left subtree of the root
    if (node.left):
        findMaxBendsUtil(node.left, 'l', bends,
                         maxBends, 1, Len)

    # Call for right subtree of the root
    if (node.right):
        findMaxBendsUtil(node.right, 'r', bends,
                         maxBends, 1, Len)

    # Include the root node as well
    # in the path Length
    Len[0] += 1

    return Len[0]

# Driver code
if __name__ == '__main__':

    # Constructed binary tree is
    # 10
    # / \
    # 8 2
    # / \ /
    # 3 5 2
    #     \
    #     1
    #     /
    #     9
    root = newNode(10)
    root.left = newNode(8)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.left = newNode(2)
    root.right.left.right = newNode(1)
    root.right.left.right.left = newNode(9)

    print(findMaxBends(root) - 1)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find path length
// having maximum number of bends
using System;
public class GFG
{

  // structure node
  public
    class Node
    {
      public
        int key;
      public
        Node left;
      public
        Node right;
    };

  // Utility function to create a new node
  static Node newNode(int key)
  {
    Node node = new Node();
    node.left = null;
    node.right = null;
    node.key = key;
    return node;
  }

  /* Recursive function to calculate the path
length having maximum number of bends.
The following are parameters for this function.

node -. pointer to the current node
dir -. determines whether the current node
is left or right child of it's parent node
bends -. number of bends so far in the
current path.
maxBends -. maximum number of bends in a
path from root to leaf
soFar -. length of the current path so
far traversed
len -. length of the path having maximum
number of bends
*/
  static int maxBends;
  static int len;
  static void findMaxBendsUtil(Node node,
                               char dir, int bends,
                               int soFar)
  {

    // Base Case
    if (node == null)
      return;

    // Leaf node
    if (node.left == null && node.right == null)
    {
      if (bends > maxBends)
      {
        maxBends = bends;
        len = soFar;
      }
    }

    // Recurring for both left and right child
    else
    {
      if (dir == 'l')
      {
        findMaxBendsUtil(node.left, dir,
                         bends,
                         soFar + 1);
        findMaxBendsUtil(node.right, 'r',
                         bends + 1,
                         soFar + 1);
      }
      else
      {
        findMaxBendsUtil(node.right, dir,
                         bends,
                         soFar + 1);
        findMaxBendsUtil(node.left, 'l',
                         bends + 1,
                         soFar + 1);
      }
    }
  }

  // Helper function to call findMaxBendsUtil()
  static int findMaxBends(Node node)
  {
    if (node == null)
      return 0;
    len = 0;
    maxBends = -1;
    int bends = 0;

    // Call for left subtree of the root
    if (node.left != null)
      findMaxBendsUtil(node.left, 'l',
                       bends, 1);

    // Call for right subtree of the root
    if (node.right != null)
      findMaxBendsUtil(node.right, 'r', bends,
                       1);

    // Include the root node as well in the path length
    len++;
    return len;
  }

  // Driver code
  public static void Main(String[] args)
  {

    /* Constructed binary tree is
      10
      / \
     8    2
    / \  /
    3  5 2
          \
           1
          /
         9
    */

    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.left = newNode(2);
    root.right.left.right = newNode(1);
    root.right.left.right.left = newNode(9);

    Console.Write(findMaxBends(root) - 1);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to find path length
    // having maximum number of bends

    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Utility function to create a new node
    function newNode(key)
    {
      let node = new Node(key);
      return node;
    }

    /* Recursive function to calculate the path
      length having maximum number of bends.
      The following are parameters for this function.

      node -. pointer to the current node
      dir -. determines whether the current node
      is left or right child of it's parent node
      bends -. number of bends so far in the
      current path.
      maxBends -. maximum number of bends in a
      path from root to leaf
      soFar -. length of the current path so
      far traversed
      len -. length of the path having maximum
      number of bends
      */
    let maxBends;
    let len;
    function findMaxBendsUtil(node, dir, bends, soFar)
    {

      // Base Case
      if (node == null)
        return;

      // Leaf node
      if (node.left == null && node.right == null)
      {
        if (bends > maxBends)
        {
          maxBends = bends;
          len = soFar;
        }
      }

      // Recurring for both left and right child
      else
      {
        if (dir == 'l')
        {
          findMaxBendsUtil(node.left, dir,
                           bends,
                           soFar + 1);
          findMaxBendsUtil(node.right, 'r',
                           bends + 1,
                           soFar + 1);
        }
        else
        {
          findMaxBendsUtil(node.right, dir,
                           bends,
                           soFar + 1);
          findMaxBendsUtil(node.left, 'l',
                           bends + 1,
                           soFar + 1);
        }
      }
    }

    // Helper function to call findMaxBendsUtil()
    function findMaxBends(node)
    {
      if (node == null)
        return 0;
      len = 0;
      maxBends = -1;
      let bends = 0;

      // Call for left subtree of the root
      if (node.left != null)
        findMaxBendsUtil(node.left, 'l',
                         bends, 1);

      // Call for right subtree of the root
      if (node.right != null)
        findMaxBendsUtil(node.right, 'r', bends,
                         1);

      // Include the root node as well in the path length
      len++;
      return len;
    }

    /* Constructed binary tree is
      10
      / \
     8    2
    / \  /
    3  5 2
          \
           1
          /
         9
    */

    let root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.left = newNode(2);
    root.right.left.right = newNode(1);
    root.right.left.right.left = newNode(9);

    document.write(findMaxBends(root) - 1);

</script>
```

**输出:**

```
4
```