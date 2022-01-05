# 二叉树最大深度的节点之和

> 原文:[https://www . geesforgeks . org/sum-nodes-最大深度-二叉树/](https://www.geeksforgeeks.org/sum-nodes-maximum-depth-binary-tree/)

给定一棵树的根节点，求距根节点最大深度的所有叶节点的和。

**例:**

```
      1
    /   \
   2     3
  / \   / \
 4   5 6   7

Input : root(of above tree)
Output : 22

Explanation:
Nodes at maximum depth are: 4, 5, 6, 7\. 
So, sum of these nodes = 22
```

遍历节点时，将节点的级别与 max_level(直到当前节点的最大级别)进行比较。如果当前级别超过最大级别，则将 max_level 更新为当前级别。如果最大级别和当前级别相同，则将根数据添加到当前总和中。如果级别低于 max_level，则不执行任何操作。

## c++

```
// Code to find the sum of the nodes
// which are present at the maximum depth.
#include <bits/stdc++.h>

using namespace std;

int sum = 0, max_level = INT_MIN;

struct Node
{
    int d;
    Node *l;
    Node *r;
};

// Function to return a new node
Node* createNode(int d)
{
    Node *node;
    node = new Node;
    node->d = d;
    node->l = NULL;
    node->r = NULL;
    return node;
}

// Function to find the sum of the node
// which are present at the maximum depth.
// While traversing the nodes compare the level
// of the node with max_level
// (Maximum level till the current node).
// If the current level exceeds the maximum level,
// update the max_level as current level.
// If the max level and current level are same,
// add the root data to current sum.
void sumOfNodesAtMaxDepth(Node *ro,int level)
{
    if(ro == NULL)
    return;
    if(level > max_level)
    {
        sum = ro -> d;
        max_level = level;
    }
    else if(level == max_level)
    {
        sum = sum + ro -> d;
    }
    sumOfNodesAtMaxDepth(ro -> l, level + 1);
    sumOfNodesAtMaxDepth(ro -> r, level + 1);
}

// Driver Code
int main()
{
    Node *root;
    root = createNode(1);
    root->l = createNode(2);
    root->r = createNode(3);
    root->l->l = createNode(4);
    root->l->r = createNode(5);
    root->r->l = createNode(6);
    root->r->r = createNode(7);
    sumOfNodesAtMaxDepth(root, 0);
    cout << sum;
    return 0;
}
```

## Java

```
// Java code to find the sum of the nodes
// which are present at the maximum depth.
class GFG
{

static int sum = 0, max_level = Integer.MIN_VALUE;

static class Node
{
    int d;
    Node l;
    Node r;
};

// Function to return a new node
static Node createNode(int d)
{
    Node node;
    node = new Node();
    node.d = d;
    node.l = null;
    node.r = null;
    return node;
}

// Function to find the sum of the node
// which are present at the maximum depth.
// While traversing the nodes compare the level
// of the node with max_level
// (Maximum level till the current node).
// If the current level exceeds the maximum level,
// update the max_level as current level.
// If the max level and current level are same,
// add the root data to current sum.
static void sumOfNodesAtMaxDepth(Node ro,int level)
{
    if(ro == null)
    return;
    if(level > max_level)
    {
        sum = ro . d;
        max_level = level;
    }
    else if(level == max_level)
    {
        sum = sum + ro . d;
    }
    sumOfNodesAtMaxDepth(ro . l, level + 1);
    sumOfNodesAtMaxDepth(ro . r, level + 1);
}

// Driver Code
public static void main(String[] args)
{
    Node root;
    root = createNode(1);
    root.l = createNode(2);
    root.r = createNode(3);
    root.l.l = createNode(4);
    root.l.r = createNode(5);
    root.r.l = createNode(6);
    root.r.r = createNode(7);
    sumOfNodesAtMaxDepth(root, 0);
    System.out.println(sum);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## python 3

T2T18】c#T20

```
// C# code to find the sum of the nodes
// which are present at the maximum depth.
using System;

class GFG
{

static int sum = 0, max_level = int.MinValue;

public class Node
{
    public int d;
    public Node l;
    public Node r;
};

// Function to return a new node
static Node createNode(int d)
{
    Node node;
    node = new Node();
    node.d = d;
    node.l = null;
    node.r = null;
    return node;
}

// Function to find the sum of the node
// which are present at the maximum depth.
// While traversing the nodes compare the level
// of the node with max_level
// (Maximum level till the current node).
// If the current level exceeds the maximum level,
// update the max_level as current level.
// If the max level and current level are same,
// add the root data to current sum.
static void sumOfNodesAtMaxDepth(Node ro,int level)
{
    if(ro == null)
    return;
    if(level > max_level)
    {
        sum = ro . d;
        max_level = level;
    }
    else if(level == max_level)
    {
        sum = sum + ro . d;
    }
    sumOfNodesAtMaxDepth(ro . l, level + 1);
    sumOfNodesAtMaxDepth(ro . r, level + 1);
}

// Driver Code
public static void Main(String[] args)
{
    Node root;
    root = createNode(1);
    root.l = createNode(2);
    root.r = createNode(3);
    root.l.l = createNode(4);
    root.l.r = createNode(5);
    root.r.l = createNode(6);
    root.r.r = createNode(7);
    sumOfNodesAtMaxDepth(root, 0);
    Console.WriteLine(sum);
}
}

// This code is contributed by Princi Singh
```

T21

## Javascript

T4T26】

**输出:**

```
22
```

本文由 Ashwin Loganathan 供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

**方法:**计算给定树的最大深度。现在，开始遍历树，就像在最大深度计算期间遍历树一样。但是，这一次多了一个参数(即 maxdepth)，并且对于每个左或右调用，以深度递减 1 的方式递归遍历。max == 1 时，表示到达最大深度的节点。所以把它的数据值加起来。最后，返回 sum。

下面是上述方法的实现:

## c++

```
// C++ code for sum of nodes
// at maximum depth
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    Node* left, *right;

    // Constructor
    Node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

    // function to find the sum of nodes at
    // maximum depth arguments are node and
    // max, where max is to match the depth
    // of node at every call to node, if
    // max will be equal to 1, means
    // we are at deepest node.
    int sumMaxLevelRec(Node* node, int max)
    {
        // base case
        if (node == NULL)
            return 0;    

        // max == 1 to track the node
        // at deepest level
        if (max == 1)
            return node->data;

        // recursive call to left and right nodes
        return sumMaxLevelRec(node->left, max - 1) +
            sumMaxLevelRec(node->right, max - 1);
    }

    // maxDepth function to find the
    // max depth of the tree
    int maxDepth(Node* node)
    {
        // base case
        if (node == NULL)
            return 0;    

        // either leftDepth of rightDepth is
        // greater add 1 to include height
        // of node at which call is
        return 1 + max(maxDepth(node->left),
                        maxDepth(node->right));    
    }

    int sumMaxLevel(Node* root)
    {

        // call to function to calculate
        // max depth
        int MaxDepth = maxDepth(root);

        return sumMaxLevelRec(root, MaxDepth);
    }

    // Driver code
    int main()
    {

        /*     1
            / \
            2 3
            / \ / \
            4 5 6 7     */

        // Constructing tree
        Node* root = new Node(1);
        root->left = new Node(2);
        root->right = new Node(3);
        root->left->left = new Node(4);
        root->left->right = new Node(5);
        root->right->left = new Node(6);
        root->right->right = new Node(7);

        // call to calculate required sum
        cout<<(sumMaxLevel(root))<<endl;
    }

// This code is contributed by Arnab Kundu
```

## Java

```
// Java code for sum of nodes
// at maximum depth
import java.util.*;

class Node {
    int data;
    Node left, right;

    // Constructor
    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

class GfG {

    // function to find the sum of nodes at
    // maximum depth arguments are node and
    // max, where max is to match the depth
    // of node at every call to node, if
    // max will be equal to 1, means
    // we are at deepest node.
    public static int sumMaxLevelRec(Node node,
                     int max)
    {
        // base case
        if (node == null)
            return 0;    

        // max == 1 to track the node
        // at deepest level
        if (max == 1)
            return node.data;   

        // recursive call to left and right nodes
        return sumMaxLevelRec(node.left, max - 1) +
               sumMaxLevelRec(node.right, max - 1);
    }

    public static int sumMaxLevel(Node root) {

        // call to function to calculate
        // max depth
        int MaxDepth = maxDepth(root);

        return sumMaxLevelRec(root, MaxDepth);
    }

    // maxDepth function to find the
    // max depth of the tree
    public static int maxDepth(Node node)
    {
        // base case
        if (node == null)
            return 0;    

        // either leftDepth of rightDepth is
        // greater add 1 to include height
        // of node at which call is
        return 1 + Math.max(maxDepth(node.left),
                           maxDepth(node.right));    
    }

    // Driver code
    public static void main(String[] args)
    {

        /*      1
              / \
              2   3
            / \ / \
            4 5 6 7     */

        // Constructing tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);

        // call to calculate required sum
        System.out.println(sumMaxLevel(root));
    }
}
```

## python 3

```
# Python3 code for sum of nodes at maximum depth
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find the sum of nodes at maximum depth
# arguments are node and max, where Max is to match
# the depth of node at every call to node, if Max
# will be equal to 1, means we are at deepest node.
def sumMaxLevelRec(node, Max):

    # base case
    if node == None:
        return 0   

    # Max == 1 to track the node at deepest level
    if Max == 1:
        return node.data    

    # recursive call to left and right nodes
    return (sumMaxLevelRec(node.left, Max - 1) +
            sumMaxLevelRec(node.right, Max - 1))

def sumMaxLevel(root):

    # call to function to calculate max depth
    MaxDepth = maxDepth(root)
    return sumMaxLevelRec(root, MaxDepth)

# maxDepth function to find
# the max depth of the tree
def maxDepth(node):

    # base case
    if node == None:
        return 0   

    # Either leftDepth of rightDepth is
    # greater add 1 to include height
    # of node at which call is
    return 1 + max(maxDepth(node.left),
                    maxDepth(node.right))

# Driver code
if __name__ == "__main__":

    # Constructing tree
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)

    # call to calculate required sum
    print(sumMaxLevel(root))

# This code is contributed by Rituraj Jain
```

## c#

```
using System;

// C# code for sum of nodes
// at maximum depth

public class Node
{
    public int data;
    public Node left, right;

    // Constructor
    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

public class GfG
{

    // function to find the sum of nodes at
    // maximum depth arguments are node and
    // max, where max is to match the depth
    // of node at every call to node, if
    // max will be equal to 1, means
    // we are at deepest node.
    public static int sumMaxLevelRec(Node node, int max)
    {
        // base case
        if (node == null)
        {
            return 0;
        }

        // max == 1 to track the node
        // at deepest level
        if (max == 1)
        {
            return node.data;
        }

        // recursive call to left and right nodes
        return sumMaxLevelRec(node.left, max - 1)
                + sumMaxLevelRec(node.right, max - 1);
    }

    public static int sumMaxLevel(Node root)
    {

        // call to function to calculate
        // max depth
        int MaxDepth = maxDepth(root);

        return sumMaxLevelRec(root, MaxDepth);
    }

    // maxDepth function to find the
    // max depth of the tree
    public static int maxDepth(Node node)
    {
        // base case
        if (node == null)
        {
            return 0;
        }

        // either leftDepth of rightDepth is
        // greater add 1 to include height
        // of node at which call is
        return 1 + Math.Max(maxDepth(node.left),
                            maxDepth(node.right));
    }

    // Driver code
    public static void Main(string[] args)
    {

        /*     1
            / \
            2 3
            / \ / \
            4 5 6 7     */

        // Constructing tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);

        // call to calculate required sum
        Console.WriteLine(sumMaxLevel(root));
    }
}

// This code is contributed by Shrikant13
```

## Javascript

```
<script>
    // Javascript code for sum of nodes at maximum depth

    // Structure of a tree node.
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to find the sum of nodes at
    // maximum depth arguments are node and
    // max, where max is to match the depth
    // of node at every call to node, if
    // max will be equal to 1, means
    // we are at deepest node.
    function sumMaxLevelRec(node, max)
    {

        // base case
        if (node == null)
            return 0;   

        // max == 1 to track the node
        // at deepest level
        if (max == 1)
            return node.data;  

        // recursive call to left and right nodes
        return sumMaxLevelRec(node.left, max - 1) +
               sumMaxLevelRec(node.right, max - 1);
    }

    function sumMaxLevel(root) {

        // call to function to calculate
        // max depth
        let MaxDepth = maxDepth(root);

        return sumMaxLevelRec(root, MaxDepth);
    }

    // maxDepth function to find the
    // max depth of the tree
    function maxDepth(node)
    {
        // base case
        if (node == null)
            return 0;   

        // either leftDepth of rightDepth is
        // greater add 1 to include height
        // of node at which call is
        return 1 + Math.max(maxDepth(node.left),
                           maxDepth(node.right));   
    }

        /*      1
                / \
                2   3
              / \ / \
              4 5 6 7     */

    // Constructing tree
    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);

    // call to calculate required sum
    document.write(sumMaxLevel(root));

// This code is contributed by divyesh072019.
</script>
```

**输出:**

```
22
```

**时间复杂度:** O(N)，其中 N 为树中节点数。

**方法 3** :-使用队列

**方法:**在这种方法中，思想是按级别顺序遍历树，并为每个级别计算该级别中所有节点的总和。对于每个级别，我们将树的所有节点推入队列，并计算节点的总和。所以，当我们到达树的末端叶子时，总和就是二叉树中所有叶子的总和。

下面是上述方法的实现:

T5】c++T7

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
};

// Function to return a new node
TreeNode *createNode(int d)
{
    TreeNode *node;
    node = new TreeNode();
    node->val = d;
    node->left = NULL;
    node->right = NULL;
    return node;
}

// Iterative function to find the sum of the deepest
// nodes.
int deepestLeavesSum(TreeNode *root)
{

    // if the root is NULL then return 0
    if (root == NULL)
    {
        return 0;
    }

    // Initialize an empty queue.
    queue<TreeNode *> qu;

    // push the root of the tree into the queue
    qu.push(root);

    // initialize sum of current level to 0
    int sumOfCurrLevel = 0;

    // loop until the queue is not empty
    while (!qu.empty())
    {
        int size = qu.size();
        sumOfCurrLevel = 0;
        while (size-- > 0)
        {
            TreeNode *head = qu.front();
            qu.pop();
            sumOfCurrLevel += head->val;
            // if the left child of the head is not NULL
            if (head->left != NULL)
            {
                //push the child into the queue
                qu.push(head->left);
            }

            // if the right child is not NULL
            if (head->right != NULL)
            {

                // push the child into the queue
                qu.push(head->right);
            }
        }
    }
    return sumOfCurrLevel;
}

// Driver code
int main()
{

    TreeNode *root;
    root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);
    cout << (deepestLeavesSum(root));
    return 0;
}

// This code is contributed by Potta Lokesh
```

T8

## Java

T11

```
// Java code to print the sum of leaves present at maximum
// depth of a binary tree
import java.util.*;

class GFG {

    static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
    };

    // Function to return a new node
    static TreeNode createNode(int d)
    {
        TreeNode node;
        node = new TreeNode();
        node.val = d;
        node.left = null;
        node.right = null;
        return node;
    }
    // Iterative function to find the sum of the deepest
    // nodes.
    public static int deepestLeavesSum(TreeNode root)
    {
          // if the root is null then return 0
        if (root== null) {
            return 0;
        }
          // Initialize an empty queue.
        Queue<TreeNode> qu= new LinkedList<>();
        // push the root of the tree into the queue
        qu.offer(root);
        // initialize sum of current level to 0
        int sumOfCurrLevel= 0;
          // loop until the queue is not empty
        while (!qu.isEmpty()) {
            int size = qu.size();
            sumOfCurrLevel = 0;
            while (size-- > 0) {
                TreeNode head = qu.poll();
                sumOfCurrLevel += head.val;
                // if the left child of the head is not null
                if (head.left!= null) {
                    //push the child into the queue
                    qu.offer(head.left);
                }
                // if the right child is not null
                if (head.right!= null) {
                   // push the child into the queue
                    qu.offer(head.right);
                }
            }
        }
        return sumOfCurrLevel;
    }
    public static void main(String[] args)
    {

        TreeNode root;
        root = createNode(1);
        root.left = createNode(2);
        root.right = createNode(3);
        root.left.left = createNode(4);
        root.left.right = createNode(5);
        root.right.left = createNode(6);
        root.right.right = createNode(7);
        System.out.println(deepestLeavesSum(root));
    }
}
// this code is contributed by Rohan Raj
```

T12

## Javascript

T15

```
<script>

// JavaScript code to print the sum
// of leaves present at maximum
// depth of a binary tree

class TreeNode
{
    constructor()
    {
        this.val=0;
        this.left=this.right=null;
    }
}

function createNode(d)
{
    let node;
        node = new TreeNode();
        node.val = d;
        node.left = null;
        node.right = null;
        return node;
}

// Iterative function to find the sum of the deepest
    // nodes.
function deepestLeavesSum(root)
{
    // if the root is null then return 0
        if (root== null) {
            return 0;
        }
          // Initialize an empty queue.
        let qu= [];
        // push the root of the tree into the queue
        qu.push(root);
        // initialize sum of current level to 0
        let sumOfCurrLevel= 0;
          // loop until the queue is not empty
        while (qu.length!=0) {
            let size = qu.length;
            sumOfCurrLevel = 0;
            while (size-- > 0) {
                let head = qu.shift();
                sumOfCurrLevel += head.val;
                // if the left child of the head is not null
                if (head.left!= null) {
                    //push the child into the queue
                    qu.push(head.left);
                }
                // if the right child is not null
                if (head.right!= null) {
                   // push the child into the queue
                    qu.push(head.right);
                }
            }
        }
        return sumOfCurrLevel;
}

let root = createNode(1);
root.left = createNode(2);
root.right = createNode(3);
root.left.left = createNode(4);
root.left.right = createNode(5);
root.right.left = createNode(6);
root.right.right = createNode(7);
document.write(deepestLeavesSum(root));

// This code is contributed by avanitrachhadiya2155

</script>
```

T16T18**输出**T3

**时间复杂度:** O(N)，其中 N 是树中的节点数。**T3】**