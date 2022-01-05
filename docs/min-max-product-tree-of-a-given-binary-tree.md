# 给定二叉树的最小-最大乘积树

> 原文:[https://www . geesforgeks . org/min-max-product-tree-of-a-给定二叉树/](https://www.geeksforgeeks.org/min-max-product-tree-of-a-given-binary-tree/)

给定一个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是将给定的二叉树转换成最小-最大乘积树，并打印修改后的树的[级序](https://www.geeksforgeeks.org/level-order-tree-traversal/)序列。
**最小-最大乘积树:**最小-最大乘积树包含其左右子树在每个节点的最小值和最大值的乘积。
**注意:**对于只有一个子节点的任何节点，该子节点的值将被视为最小值和最大值。
**示例:**

```
Input:  
                 1
                /  \ 
              12    11
             /     /   \ 
            3     4     13 
                   \    / 
                   15  5  
Output: 
45 9 60 3 225 25 15 5
Explanation:  
Min-Max Product Tree:
                 45 (3 * 15)
                /  \ 
       ( 3 * 3)9    60 (4 * 15)
             /     /   \ 
            3     225   25 (5* 5)
                   \    / 
                   15  5

Input:
                  5
                /  \ 
              21     77 
             /  \      \
            61   16     16 
                  \    / 
                   10  3    
                   /
                  23 
Output:
231 610 48 61 230 9 529 3 23
```

**方法:**
思路是使用[后序遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal/)递归遍历左右子树，提取最小值和最大值。在最小-最大乘积树中存储每个节点的最小和最大乘积。计算完成后，将当前节点值与当前最小值和最大值进行比较，并进行相应的修改。为更高级别的节点返回新的最小值和最大值。对所有节点重复此过程，最后，打印最小-最大产品树的层级顺序遍历。
以下是上述方法的实施:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// Utility function to create
// a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->data = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// A minMax Structure for storing
// minimum and maximum value
struct minMax {
    int min;
    int max;
};

// Function to return min value
int min(minMax* a, minMax* b)
{
    if (a != NULL
        && b != NULL) {

        return a->min < b->min
                   ? a->min
                   : b->min;
    }

    return a == NULL
               ? b->min
               : a->min;
}

// Function to return max value
int max(minMax* a, minMax* b)
{
    if (a != NULL
        && b != NULL) {

        return a->max > b->max
                   ? a->max
                   : b->max;
    }

    return a == NULL
               ? b->max
               : a->max;
}

// Function to return min value
int min(int x, int y)
{
    return x < y ? x : y;
}

// Function to return max value
int max(int x, int y)
{
    return x > y ? x : y;
}

// Utility function to create
// min-max product tree
minMax* minMaxTreeUtil(
    Node* root)
{

    // Base condition
    if (root == NULL) {
        return NULL;
    }

    minMax* var = new minMax;

    // Condition to check if
    // current node is leaf node
    if (root->left == NULL
        && root->right == NULL) {

        var->min = root->data;
        var->max = root->data;
        return var;
    }

    // Left recursive call
    minMax* left
        = minMaxTreeUtil(root->left);

    // Right recursive call
    minMax* right
        = minMaxTreeUtil(root->right);

    // Store Min
    var->min = min(left, right);

    // Store Max
    var->max = max(left, right);

    // Store current node data
    int currData = root->data;

    // Assign product of minimum
    // and maximum value
    root->data = var->min * var->max;

    // Again store min by considering
    // current node value
    var->min = min(var->min, currData);

    // Again store max by considering
    // current node value
    var->max = max(var->max, currData);
    return var;
}
void print(Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue for
    // level order traversal
    queue<Node*> q;

    // Enqueue Root and initialize
    // height
    q.push(root);

    while (q.empty() == false) {

        // nodeCount (queue size)
        // indicates number
        // of nodes at current level.
        int nodeCount = q.size();

        // Dequeue all nodes of current
        // level and Enqueue all nodes
        // of next level
        while (nodeCount > 0) {

            Node* node = q.front();
            cout << node->data << " ";
            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;
        }
    }
}

void minMaxProductTree(Node* root)
{
    // Utility Function call
    minMaxTreeUtil(root);

    // Print tree
    print(root);
}

// Driver Code
int main()
{

    /*     10
            / \
        48     3
                / \
            11     37
            / \ / \
            7 29 42 19
                    /
                    7
    */

    // Create Binary Tree as shown
    Node* root = newNode(10);
    root->left = newNode(48);
    root->right = newNode(3);

    root->right->left = newNode(11);
    root->right->right = newNode(37);
    root->right->left->left = newNode(7);
    root->right->left->right = newNode(29);
    root->right->right->left = newNode(42);
    root->right->right->right = newNode(19);
    root->right->right->right->left = newNode(7);

    // Create Min Max Product Tree
    minMaxProductTree(root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
from collections import deque

# A Tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# A minMax Structure for storing
# minimum and maximum value
class minMax:

    def __init__(self, x, y):

        self.min = x
        self.max = y

# Function to return min value
def minm(a, b):

    if (a != None and
        b != None):
        if a.min < b.min:
            return a.min
        return b.min

    if a == None:
        return b.min
    return a.min

# Function to return max value
def maxm(a, b):

    if a != None and b != None:
        if a.max > b.max:
            return a.max
        return b.max

    if a == None:
        return b.max
    return a.max

# Utility function to create
# min-max product tree
def minMaxTreeUtil(root):

    # Base condition
    if (root == None):
        return None

    var = minMax(10 ** 9,
                 -10 ** 9)

    # Condition to check if
    # current node is leaf node
    if (root.left == None and
        root.right == None):
        var.min = root.data
        var.max = root.data
        return var

    # Left recursive call
    left= minMaxTreeUtil(root.left)

    # Right recursive call
    right= minMaxTreeUtil(root.right)

    # Store Min
    var.min = minm(left, right)

    # Store Max
    var.max = maxm(left, right)

    # Store current node data
    currData = root.data

    # Assign product of minimum
    # and maximum value
    root.data = var.min * var.max

    # Again store min by considering
    # current node value
    var.min = min(var.min,
                  currData)

    # Again store max by considering
    # current node value
    var.max = max(var.max,
                  currData)
    return var

def printt(root):

    # Base Case
    if (root == None):
        return

    # Create an empty queue for
    # level order traversal
    q = deque()

    # Enqueue Root and initialize
    # height
    q.append(root)

    while (len(q) > 0):

        # nodeCount (queue size)
        # indicates number
        # of nodes at current level.
        nodeCount = len(q)

        # Dequeue all nodes of current
        # level and Enqueue all nodes
        # of next level
        while (nodeCount > 0):
            node = q.popleft()
            print(node.data,
                  end = " ")

            if (node.left != None):
                q.append(node.left)
            if (node.right != None):
                q.append(node.right)
            nodeCount -= 1

def minMaxProductTree(root):

    # Utility Function call
    minMaxTreeUtil(root)

    # Prtree
    printt(root)

# Driver Code
if __name__ == '__main__':

    # /*     10
    #         / \
    #     48     3
    #             / \
    #         11     37
    #         / \ / \
    #         7 29 42 19
    #                 /
    #                 7
    # */

    # Create Binary Tree as shown
    root = Node(10)
    root.left = Node(48)
    root.right = Node(3)

    root.right.left = Node(11)
    root.right.right = Node(37)
    root.right.left.left = Node(7)
    root.right.left.right = Node(29)
    root.right.right.left = Node(42)
    root.right.right.right = Node(19)
    root.right.right.right.left = Node(7)

    # Create Min Max Product Tree
    minMaxProductTree(root)

# This code is contributed by Mohit Kumar 29
```

**Output:** 

```
144 48 294 203 294 7 29 42 49 7
```

***时间复杂度:** O(N)，其中 N 表示二叉树中的节点数*
***辅助空间:** O(1)*