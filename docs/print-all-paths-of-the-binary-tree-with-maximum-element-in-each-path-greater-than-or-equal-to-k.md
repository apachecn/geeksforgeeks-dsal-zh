# 打印二叉树的所有路径，每个路径中最大元素大于或等于 K

> 原文:[https://www . geesforgeks . org/print-每条路径中包含最大元素的二叉树的所有路径大于或等于 k/](https://www.geeksforgeeks.org/print-all-paths-of-the-binary-tree-with-maximum-element-in-each-path-greater-than-or-equal-to-k/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和一个整数 **K** ，任务是打印从根到叶的路径，最大元素大于或等于 **K** 。如果没有这样的路径，打印-1。
**举例:**

```
Input: K = 25, 
                10
              /    \
             5      8
           /   \   /  \
          29    2 1    98
         /               \      
        20                50

Output: (10, 5, 29, 20), (10, 8, 98, 50)
Explanation:
The maximum value in the path 10
 -> 5 -> 29 -> 20 
is 29 which is greater than 25.
The maximum value in the path 10
 -> 8 -> 98 -> 50
is 98 which is greater than 25.

Input: K = 5
             2
           /   \
          1     4
         /
        0

Output: -1
Explanation: 
None of the paths from the root to a leaf 
has the value greater than 5.
```

**方法:**想法是检查节点是否包含大于或等于‘K’的值。如果是，则[该节点](https://www.geeksforgeeks.org/sub-tree-nodes-tree-using-dfs/)的所有子树都是有效路径。可以按照以下步骤计算答案:

*   对于每个节点，检查当前节点值是否大于“K”。
*   如果是，则将其插入到[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，并将标志变量设置为 1。这表示将打印通过该节点的所有路径。
*   使用[递归](https://www.geeksforgeeks.org/recursion/)重复上述步骤。对左右子树递归调用该函数。
*   最后，利用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)的概念，从向量中打印路径。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print paths with maximum
// element in the path greater than K

#include <bits/stdc++.h>
using namespace std;

// A Binary Tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new node
struct Node* newNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return (newNode);
}

// A recursive function to print the paths
// whose maximum element is greater than
// or equal to K.
void findPathUtil(Node* root, int k,
                  vector<int> path,
                  int flag, int& ans)
{
    if (root == NULL)
        return;

    // If the current node value is greater than
    // or equal to k, then all the subtrees
    // following that node will get printed,
    // flag = 1 indicates to print the required path
    if (root->data >= k)
        flag = 1;

    // If the leaf node is encountered, then the path is
    // printed if the size of the path vector is
    // greater than 0
    if (root->left == NULL && root->right == NULL) {
        if (flag == 1) {
            ans = 1;
            cout << "(";
            for (int i = 0; i < path.size(); i++) {
                cout << path[i] << ", ";
            }
            cout << root->data << "), ";
        }
        return;
    }

    // Append the node to the path vector
    path.push_back(root->data);

    // Recur left and right subtrees
    findPathUtil(root->left, k, path, flag, ans);
    findPathUtil(root->right, k, path, flag, ans);

    // Backtracking to return the vector
    // and print the path if the flag is 1
    path.pop_back();
}

// Function to initialize the variables
// and call the utility function to print
// the paths with maximum values greater than
// or equal to K
void findPath(Node* root, int k)
{
    // Initialize flag
    int flag = 0;

    // ans is used to check empty condition
    int ans = 0;

    vector<int> v;

    // Call function that print path
    findPathUtil(root, k, v, flag, ans);

    // If the path doesn't exist
    if (ans == 0)
        cout << "-1";
}

// Driver code
int main(void)
{
    int K = 25;

    /* Constructing the following tree:
                10
              /    \
             5      8
           /   \   /  \
          29    2 1    98
         /               \     
        20                50
   */

    struct Node* root = newNode(10);
    root->left = newNode(5);
    root->right = newNode(8);
    root->left->left = newNode(29);
    root->left->right = newNode(2);
    root->right->right = newNode(98);
    root->right->left = newNode(1);
    root->right->right->right = newNode(50);
    root->left->left->left = newNode(20);

    findPath(root, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print paths with maximum
// element in the path greater than K
import java.util.*;

class GFG
{

// A Binary Tree node
static class Node
{
    int data;
    Node left, right;
};
static int ans;

// A utility function to create a new node
static Node newNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}

// A recursive function to print the paths
// whose maximum element is greater than
// or equal to K.
static void findPathUtil(Node root, int k,
                Vector<Integer> path,
                int flag)
{
    if (root == null)
        return;

    // If the current node value is greater than
    // or equal to k, then all the subtrees
    // following that node will get printed,
    // flag = 1 indicates to print the required path
    if (root.data >= k)
        flag = 1;

    // If the leaf node is encountered, then the path is
    // printed if the size of the path vector is
    // greater than 0
    if (root.left == null && root.right == null)
    {
        if (flag == 1)
        {
            ans = 1;
            System.out.print("(");
            for (int i = 0; i < path.size(); i++)
            {
                System.out.print(path.get(i)+ ", ");
            }
            System.out.print(root.data+ "), ");
        }
        return;
    }

    // Append the node to the path vector
    path.add(root.data);

    // Recur left and right subtrees
    findPathUtil(root.left, k, path, flag);
    findPathUtil(root.right, k, path, flag);

    // Backtracking to return the vector
    // and print the path if the flag is 1
    path.remove(path.size()-1);
}

// Function to initialize the variables
// and call the utility function to print
// the paths with maximum values greater than
// or equal to K
static void findPath(Node root, int k)
{
    // Initialize flag
    int flag = 0;

    // ans is used to check empty condition
    ans = 0;

    Vector<Integer> v = new Vector<Integer>();

    // Call function that print path
    findPathUtil(root, k, v, flag);

    // If the path doesn't exist
    if (ans == 0)
        System.out.print("-1");
}

// Driver code
public static void main(String [] args)
{
    int K = 25;

    /* Constructing the following tree:
                10
            / \
            5     8
        / \ / \
        29 2 1 98
        /             \    
        20             50
*/

    Node root = newNode(10);
    root.left = newNode(5);
    root.right = newNode(8);
    root.left.left = newNode(29);
    root.left.right = newNode(2);
    root.right.right = newNode(98);
    root.right.left = newNode(1);
    root.right.right.right = newNode(50);
    root.left.left.left = newNode(20);

    findPath(root, K);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to construct string from binary tree

# A Binary Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A recursive function to print the paths
# whose maximum element is greater than
# or equal to K.
def findPathUtil(root: Node, k: int, path: list, flag: int):
    global ans

    if root is None:
        return

    # If the current node value is greater than
    # or equal to k, then all the subtrees
    # following that node will get printed,
    # flag = 1 indicates to print the required path
    if root.data >= k:
        flag = 1

    # If the leaf node is encountered, then the path is
    # printed if the size of the path vector is
    # greater than 0
    if root.left is None and root.right is None:
        if flag:
            ans = 1
            print("(", end = "")
            for i in range(len(path)):
                print(path[i], end = ", ")
            print(root.data, end = "), ")
        return

    # Append the node to the path vector
    path.append(root.data)

    # Recur left and right subtrees
    findPathUtil(root.left, k, path, flag)
    findPathUtil(root.right, k, path, flag)

    # Backtracking to return the vector
    # and print the path if the flag is 1
    path.pop()

# Function to initialize the variables
# and call the utility function to print
# the paths with maximum values greater than
# or equal to K
def findPath(root: Node, k: int):
    global ans

    # Initialize flag
    flag = 0

    # ans is used to check empty condition
    ans = 0

    v = []

    # Call function that print path
    findPathUtil(root, k, v, flag)

    # If the path doesn't exist
    if ans == 0:
        print(-1)

# Driver Code
if __name__ == "__main__":

    ans = 0
    k = 25

    # Constructing the following tree:
    #             10
    #         / \
    #         5     8
    #     / \ / \
    #     29 2 1 98
    #     /             \
    #     20             50

    root = Node(10)
    root.left = Node(5)
    root.right = Node(8)
    root.left.left = Node(29)
    root.left.right = Node(2)
    root.right.right = Node(98)
    root.right.left = Node(1)
    root.right.right.right = Node(50)
    root.left.left.left = Node(20)

    findPath(root, k)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print paths with maximum
// element in the path greater than K
using System;
using System.Collections.Generic;

class GFG
{

// A Binary Tree node
class Node
{
    public int data;
    public Node left, right;
};
static int ans;

// A utility function to create a new node
static Node newNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}

// A recursive function to print the paths
// whose maximum element is greater than
// or equal to K.
static void findPathUtil(Node root, int k,
                        List<int> path,
                        int flag)
{
    if (root == null)
        return;

    // If the current node value is greater than
    // or equal to k, then all the subtrees
    // following that node will get printed,
    // flag = 1 indicates to print the required path
    if (root.data >= k)
        flag = 1;

    // If the leaf node is encountered, then the path is
    // printed if the size of the path vector is
    // greater than 0
    if (root.left == null && root.right == null)
    {
        if (flag == 1)
        {
            ans = 1;
            Console.Write("(");
            for (int i = 0; i < path.Count; i++)
            {
                Console.Write(path[i] + ", ");
            }
            Console.Write(root.data + "), ");
        }
        return;
    }

    // Append the node to the path vector
    path.Add(root.data);

    // Recur left and right subtrees
    findPathUtil(root.left, k, path, flag);
    findPathUtil(root.right, k, path, flag);

    // Backtracking to return the vector
    // and print the path if the flag is 1
    path.RemoveAt(path.Count-1);
}

// Function to initialize the variables
// and call the utility function to print
// the paths with maximum values greater than
// or equal to K
static void findPath(Node root, int k)
{
    // Initialize flag
    int flag = 0;

    // ans is used to check empty condition
    ans = 0;

    List<int> v = new List<int>();

    // Call function that print path
    findPathUtil(root, k, v, flag);

    // If the path doesn't exist
    if (ans == 0)
        Console.Write("-1");
}

// Driver code
public static void Main(String [] args)
{
    int K = 25;

    /* Constructing the following tree:
                10
            / \
            5     8
        / \ / \
        29 2 1 98
        /             \    
        20             50
*/

    Node root = newNode(10);
    root.left = newNode(5);
    root.right = newNode(8);
    root.left.left = newNode(29);
    root.left.right = newNode(2);
    root.right.right = newNode(98);
    root.right.left = newNode(1);
    root.right.right.right = newNode(50);
    root.left.left.left = newNode(20);

    findPath(root, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to print paths with maximum
// element in the path greater than K

// A Binary Tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

var ans = 0;

// A utility function to create a new node
function newNode(data)
{
    var newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}

// A recursive function to print the paths
// whose maximum element is greater than
// or equal to K.
function findPathUtil(root, k, path, flag)
{
    if (root == null)
        return;

    // If the current node value is greater than
    // or equal to k, then all the subtrees
    // following that node will get printed,
    // flag = 1 indicates to print the required path
    if (root.data >= k)
        flag = 1;

    // If the leaf node is encountered, then the path is
    // printed if the size of the path vector is
    // greater than 0
    if (root.left == null && root.right == null)
    {
        if (flag == 1)
        {
            ans = 1;
            document.write("(");
            for (var i = 0; i < path.length; i++)
            {
                document.write(path[i] + ", ");
            }
            document.write(root.data + "), ");
        }
        return;
    }

    // Append the node to the path vector
    path.push(root.data);

    // Recur left and right subtrees
    findPathUtil(root.left, k, path, flag);
    findPathUtil(root.right, k, path, flag);

    // Backtracking to return the vector
    // and print the path if the flag is 1
    path.pop();
}

// Function to initialize the variables
// and call the utility function to print
// the paths with maximum values greater than
// or equal to K
function findPath(root, k)
{
    // Initialize flag
    var flag = 0;

    // ans is used to check empty condition
    ans = 0;

    var v = [];

    // Call function that print path
    findPathUtil(root, k, v, flag);

    // If the path doesn't exist
    if (ans == 0)
        document.write("-1");
}

// Driver code
var K = 25;
/* Constructing the following tree:
            10
        / \
        5     8
    / \ / \
    29 2 1 98
    /             \    
    20             50
  */
var root = newNode(10);
root.left = newNode(5);
root.right = newNode(8);
root.left.left = newNode(29);
root.left.right = newNode(2);
root.right.right = newNode(98);
root.right.left = newNode(1);
root.right.right.right = newNode(50);
root.left.left.left = newNode(20);
findPath(root, K);

</script>
```

**Output:** 

```
(10, 5, 29, 20), (10, 8, 98, 50),
```