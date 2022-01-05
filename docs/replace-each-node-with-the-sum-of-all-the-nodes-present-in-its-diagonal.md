# 将二叉树的每个节点替换为其对角线上所有节点的总和

> 原文:[https://www . geesforgeks . org/将每个节点替换为其对角线上所有节点的总和/](https://www.geeksforgeeks.org/replace-each-node-with-the-sum-of-all-the-nodes-present-in-its-diagonal/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是将树的每个节点的值替换为同一对角线上所有节点的和后，打印树的[级序遍历。](https://www.geeksforgeeks.org/level-order-tree-traversal/)

**示例:**

> **输入:**
> 
> ```
>              9
>             / \
>            6   10
>           / \   \
>          4   7   11
>         / \   \
>        3  5   8
> ```
> 
> **输出:**30 21 30 9 21 30 3 9 21
> T3】解释:T5】
> 
> ```
>              30
>             / \
>           21   30
>           / \   \
>          9   21  30
>         / \   \
>        3   9   21
> ```
> 
> 二叉树的对角遍历
> 9 10 11
> 6 7 8
> 4 5
> 3
> 
> **输入:**
> 
> ```
>              5
>             / \
>            6   3
>           / \   \
>          4   9   2
> ```
> 
> **输出:** 10 15 10 4 15 10
> **说明:**
> 
> ```
>              10
>             / \
>            15  10
>           / \   \
>          4   15  10
> ```

**方法:**思想是执行二叉树的[对角遍历，并将每个节点的和存储在同一对角线上。最后，遍历树并用对角线上的节点总和替换每个节点。按照以下步骤解决问题:](https://www.geeksforgeeks.org/diagonal-traversal-of-binary-tree/)

*   使用[树的对角线遍历](https://www.geeksforgeeks.org/diagonal-traversal-of-binary-tree/)并存储树的每条对角线上所有节点的总和，并将每条对角线的总和存储到一个地图中。
*   [使用](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)遍历树，并用该对角线上所有节点的总和替换树的每个节点。
*   最后，使用层级顺序遍历打印[树。](https://www.geeksforgeeks.org/level-order-tree-traversal/)

下面是上述方法的实现:

## C++

```
// CPP program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a tree node
struct TreeNode
{
  int val;
  struct TreeNode *left,*right;
  TreeNode(int x)
  {
    val = x;
    left = NULL;
    right = NULL;
  }
};

// Function to replace each node with
// the sum of nodes at the same diagonal
void  replaceDiag(TreeNode *root, int d,
                  unordered_map<int,int> &diagMap){

  // IF root is NULL
  if (!root)
    return;

  // Replace nodes
  root->val = diagMap[d];

  // Traverse the left subtree
  replaceDiag(root->left, d + 1, diagMap);

  // Traverse the right subtree
  replaceDiag(root->right, d, diagMap);
}

// Function to find the sum of all the nodes
// at each diagonal of the tree
void getDiagSum(TreeNode *root, int d,
                unordered_map<int,int> &diagMap)
{

  // If root is not NULL
  if (!root)
    return;

  // If update sum of nodes
  // at current diagonal
  if (diagMap[d] > 0)
    diagMap[d] += root->val;
  else
    diagMap[d] = root->val;

  // Traverse the left subtree
  getDiagSum(root->left, d + 1, diagMap);

  // Traverse the right subtree
  getDiagSum(root->right, d, diagMap);
}

// Function to print the nodes of the tree
// using level order traversal
void levelOrder(TreeNode *root)
{

  // Stores node at each level of the tree
  queue<TreeNode*> q;
  q.push(root);
  while (true)
  {

    // Stores count of nodes
    // at current level
    int length = q.size();
    if (!length)
      break;
    while (length)
    {

      // Stores front element
      // of the queue
      auto temp = q.front();
      q.pop();

      cout << temp->val << " ";

      // Insert left subtree
      if (temp->left)
        q.push(temp->left);

      // Insert right subtree
      if (temp->right)
        q.push(temp->right);

      // Update length
      length -= 1;
    }
  }
}

// Driver Code
int main()
{
  // Build tree
  TreeNode *root = new TreeNode(5);
  root->left = new TreeNode(6);
  root->right = new TreeNode(3);
  root->left->left =new TreeNode(4);
  root->left->right = new TreeNode(9);
  root->right->right = new TreeNode(2);

  // Store sum of nodes at each
  // diagonal of the tree
  unordered_map<int,int> diagMap;

  // Find sum of nodes at each
  // diagonal of the tree
  getDiagSum(root, 0, diagMap);

  // Replace nodes with the sum
  // of nodes at the same diagonal
  replaceDiag(root, 0, diagMap);

  // Print tree
  levelOrder(root);
  return 0;
}

// This code is contributed by mohit kumar 29
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Structure of a tree node
class TreeNode:
    def __init__(self, val = 0, left = None,
                            right = None):
        self.val = val
        self.left = left
        self.right = right

# Function to replace each node with 
# the sum of nodes at the same diagonal
def replaceDiag(root, d, diagMap):

    # IF root is NULL
    if not root:
        return

    # Replace nodes
    root.val = diagMap[d]

    # Traverse the left subtree
    replaceDiag(root.left, d + 1, diagMap)

    # Traverse the right subtree
    replaceDiag(root.right, d, diagMap)

# Function to find the sum of all the nodes
# at each diagonal of the tree
def getDiagSum(root, d, diagMap):

    # If root is not NULL
    if not root:
        return

    # If update sum of nodes
    # at current diagonal
    if d in diagMap:
        diagMap[d] += root.val
    else:
        diagMap[d] = root.val

    # Traverse the left subtree   
    getDiagSum(root.left, d + 1, diagMap)

    # Traverse the right subtree
    getDiagSum(root.right, d, diagMap)

# Function to print the nodes of the tree
# using level order traversal
def levelOrder(root):

    # Stores node at each level of the tree
    que = [root]
    while True:

        # Stores count of nodes
        # at current level
        length = len(que)     
        if not length:
            break
        while length:

            # Stores front element
            # of the queue
            temp = que.pop(0)
            print(temp.val, end =' ')

            # Insert left subtree
            if temp.left:
                que.append(temp.left)

            # Insert right subtree   
            if temp.right:
                que.append(temp.right)

            # Update length   
            length -= 1

# Driver code
if __name__ == '__main__':

    # Build tree
    root = TreeNode(5)
    root.left = TreeNode(6)
    root.right = TreeNode(3)
    root.left.left = TreeNode(4)
    root.left.right = TreeNode(9)
    root.right.right = TreeNode(2)

    # Store sum of nodes at each
    # diagonal of the tree
    diagMap = {}

    # Find sum of nodes at each
    # diagonal of the tree
    getDiagSum(root, 0, diagMap)

    # Replace nodes with the sum
    # of nodes at the same diagonal
    replaceDiag(root, 0, diagMap)

    # Print tree
    levelOrder(root)
```

## java 描述语言

```
<script>

    // Javascript program to implement the above approach

    // Structure of a tree node
    class TreeNode
    {
        constructor(x) {
           this.left = null;
           this.right = null;
           this.val = x;
        }
    }

    // Store sum of nodes at each
    // diagonal of the tree
    let diagMap = new Map();

    // Function to replace each node with
    // the sum of nodes at the same diagonal
    function replaceDiag(root, d){

      // IF root is NULL
      if (root == null)
        return;

      // Replace nodes
      if(diagMap.has(d))
      root.val = diagMap.get(d);

      // Traverse the left subtree
      replaceDiag(root.left, d + 1);

      // Traverse the right subtree
      replaceDiag(root.right, d);
    }

    // Function to find the sum of all the nodes
    // at each diagonal of the tree
    function getDiagSum(root, d)
    {

      // If root is not NULL
      if(root == null)
        return;

      // If update sum of nodes
      // at current diagonal
      if (diagMap.has(d))
        diagMap.set(d, diagMap.get(d) + root.val);
      else
        diagMap.set(d, root.val);

      // Traverse the left subtree
      getDiagSum(root.left, d + 1);

      // Traverse the right subtree
      getDiagSum(root.right, d);
    }

    // Function to print the nodes of the tree
    // using level order traversal
    function levelOrder(root)
    {

      // Stores node at each level of the tree
      let q = [];
      q.push(root);
      while (true)
      {

        // Stores count of nodes
        // at current level
        let length = q.length;
        if (!length)
          break;
        while (length)
        {

          // Stores front element
          // of the queue
          let temp = q[0];
          q.shift();

          document.write(temp.val + " ");

          // Insert left subtree
          if (temp.left != null)
            q.push(temp.left);

          // Insert right subtree
          if (temp.right != null)
            q.push(temp.right);

          // Update length
          length -= 1;
        }
      }
    }

    // Build tree
    let root = new TreeNode(5);
    root.left = new TreeNode(6);
    root.right = new TreeNode(3);
    root.left.left =new TreeNode(4);
    root.left.right = new TreeNode(9);
    root.right.right = new TreeNode(2);

    // Find sum of nodes at each
    // diagonal of the tree
    getDiagSum(root, 0);

    // Replace nodes with the sum
    // of nodes at the same diagonal
    replaceDiag(root, 0);

    // Print tree
    levelOrder(root);

</script>
```

**Output:** 

```
10 15 10 4 15 10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)