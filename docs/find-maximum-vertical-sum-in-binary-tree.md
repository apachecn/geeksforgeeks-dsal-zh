# 求二叉树中最大垂直和

> 原文:[https://www . geesforgeks . org/find-maximum-vertical-sum-in-二叉树/](https://www.geeksforgeeks.org/find-maximum-vertical-sum-in-binary-tree/)

给定一棵二叉树，求二叉树中最大垂直水平和。

**示例:**

```
Input : 
                3
              /  \
             4    6
           /  \  /  \
         -1   -2 5   10
                  \
                   8  

Output : 14
Vertical level having nodes 6 and 8 has maximum
vertical sum 14\. 

Input :
                1
              /  \
             5    8
           /  \    \
          2   -6    3
           \       /
           -1     -4
             \
              9

Output : 4 
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

一个**简单的**解法是先求从最小垂直标高到最大垂直标高开始的各标高的垂直标高之和。求一个垂直水平的和需要 O(n)个时间。在最坏的情况下，这个解决方案的时间复杂度是 O(n^2).

一种**高效的**解决方案是对给定的二叉树进行级别顺序遍历，并在遍历的同时更新每一级的垂直级别和。在找到每个水平的垂直和之后，从这些值中找到最大垂直和。

下面是上述方法的实现:

## C++

```
// C++ program to find maximum vertical
// sum in binary tree.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new
// Binary Tree Node
struct Node* newNode(int item)
{
    struct Node* temp = (struct Node*)malloc(sizeof(struct Node));
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find maximum vertical sum
// in binary tree.
int maxVerticalSum(Node* root)
{
    if (root == NULL) {
        return 0;
    }

    // To store sum of each vertical level.
    unordered_map<int, int> verSum;

    // To store maximum vertical level sum.
    int maxSum = INT_MIN;

    // To store vertical level of current node.
    int currLev;

    // Queue to perform level order traversal.
    // Each element of queue is a pair of node
    // and its vertical level.
    queue<pair<Node*, int> > q;
    q.push({ root, 0 });

    while (!q.empty()) {

        // Extract node at front of queue
        // and its vertical level.
        root = q.front().first;
        currLev = q.front().second;
        q.pop();

        // Update vertical level sum of
        // vertical level to which
        // current node belongs to.
        verSum[currLev] += root->data;

        if (root->left)
            q.push({ root->left, currLev - 1 });

        if (root->right)
            q.push({ root->right, currLev + 1 });
    }

    // Find maximum vertical level sum.
    for (auto it : verSum)
        maxSum = max(maxSum, it.second);

    return maxSum;
}

// Driver Program to test above functions
int main()
{
    /*
                3
              /  \
             4    6
           /  \  /  \
         -1   -2 5   10
                  \
                   8 
    */

    struct Node* root = newNode(3);
    root->left = newNode(4);
    root->right = newNode(6);
    root->left->left = newNode(-1);
    root->left->right = newNode(-2);
    root->right->left = newNode(5);
    root->right->right = newNode(10);
    root->right->left->right = newNode(8);

    cout << maxVerticalSum(root);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find maximum
# vertical sum in binary tree.
from sys import maxsize
from collections import deque

INT_MIN = -maxsize

class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to find maximum vertical sum
# in binary tree.
def maxVerticalSum(root: Node) -> int:

    if (root is None):
        return 0

    # To store sum of each vertical level.
    verSum = dict()

    # To store maximum vertical level sum.
    maxSum = INT_MIN

    # To store vertical level of current node.
    currLev = 0

    # Queue to perform level order traversal.
    # Each element of queue is a pair of node
    # and its vertical level.
    q = deque()
    q.append([root, 0])

    while (q):

        # Extract node at front of queue
        # and its vertical level.
        root = q[0][0]
        currLev = q[0][1]
        q.popleft()

        # Update vertical level sum of
        # vertical level to which
        # current node belongs to.
        if currLev not in verSum:
            verSum[currLev] = 0

        verSum[currLev] += root.data

        if (root.left):
            q.append([root.left, currLev - 1])

        if (root.right):
            q.append([root.right, currLev + 1])

    # Find maximum vertical level sum.
    for it in verSum:
        maxSum = max([maxSum, verSum[it]])

    return maxSum

# Driver code
if __name__ == "__main__":

    '''
                3
              /  \
             4    6
           /  \  /  \
         -1   -2 5   10
                  \
                   8 
    '''

    root = Node(3)
    root.left = Node(4)
    root.right = Node(6)
    root.left.left = Node(-1)
    root.left.right = Node(-2)
    root.right.left = Node(5)
    root.right.right = Node(10)
    root.right.left.right = Node(8)

    print(maxVerticalSum(root))

# This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// vertical sum in binary tree.

// A Binary Tree Node
class Node
{
    constructor(item)
    {
        this.left = null;
        this.right = null;
        this.data = item;
    }
}

// A utility function to create a new
// Binary Tree Node
function newNode(item)
{
    let temp = new Node(item);
    return temp;
}

// Function to find maximum vertical sum
// in binary tree.
function maxVerticalSum(root)
{
    if (root == null)
    {
        return 0;
    }

    // To store sum of each vertical level.
    let verSum = new Map();

    // To store maximum vertical level sum.
    let maxSum = Number.MIN_VALUE;

    // To store vertical level of current node.
    let currLev;

    // Queue to perform level order traversal.
    // Each element of queue is a pair of node
    // and its vertical level.
    let q = [];
    q.push([ root, 0 ]);

    while (q.length > 0)
    {

        // Extract node at front of queue
        // and its vertical level.
        root = q[0][0];
        currLev = q[0][1];
        q.shift();

        // Update vertical level sum of
        // vertical level to which
        // current node belongs to.
        if (verSum.has(currLev))
        {
            verSum.set(currLev, verSum.get(currLev) +
                                root.data);
        }
        else
        {
            verSum.set(currLev, root.data);
        }

        if (root.left)
            q.push([root.left, currLev - 1]);

        if (root.right)
            q.push([root.right, currLev + 1]);
    }

    // Find maximum vertical level sum.
      verSum.forEach((values, keys)=>{
          maxSum = Math.max(maxSum, values);
    })
    return maxSum;
}

// Driver code
/*
            3
          /  \
         4    6
       /  \  /  \
     -1   -2 5   10
              \
               8
*/
let root = newNode(3);
root.left = newNode(4);
root.right = newNode(6);
root.left.left = newNode(-1);
root.left.right = newNode(-2);
root.right.left = newNode(5);
root.right.right = newNode(10);
root.right.left.right = newNode(8);

document.write(maxVerticalSum(root));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
14
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)