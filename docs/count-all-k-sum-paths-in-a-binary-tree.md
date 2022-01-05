# 计算二叉树中所有 k-和路径

> 原文:[https://www . geesforgeks . org/count-all-k-sum-path-in-a-a-binary-tree/](https://www.geeksforgeeks.org/count-all-k-sum-paths-in-a-binary-tree/)

给定一棵二叉树和一个整数 **k** 。任务是计算树中节点总和等于 **k** 的路径数。
路径可以从任意节点开始，在任意节点结束，并且必须只向下，即它们不需要是根节点和叶节点，树中也可以有负数。

**示例:**

```
Input : k = 5  
        Root of below binary tree:
           1
        /     \
      3        -1
    /   \     /   \
   2     1   4     5                        
        /   / \     \                    
       1   1   2     6    

Output : No of paths with sum equals to 5 are: 8
3 2 
3 1 1 
1 3 1 
4 1 
1 -1 4 1 
-1 4 2 
5 
1 -1 5 

Input : k = 3
           1
        /     \
      2       -1
    /   \     /   
   1     2   3                             
            / \                         
           2   5        
Output : No of paths with sum equals to 3 are : 4
```

**方法:**
路径和等于 k 的打印路径的实现已经在[这篇](https://www.geeksforgeeks.org/print-k-sum-paths-binary-tree/)使用向量的帖子中讨论过了。然而，如果我们只想存储这种路径的计数
的话，矢量存储和递归移动会增加空间和时间复杂度。上述问题的有效实现可以通过使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)和[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)来实现。

**步骤:**

*   我们将使用一个无序的地图，其中将充满各种路径和。
*   对于每个节点，我们将检查当前和与根的值是否等于 k。如果总和等于 k，则将所需答案增加 1。
*   然后我们将把地图中所有不同于当前**和+根- >数据**值的路径和加一个常数 k
*   然后我们将在地图中插入**当前总和+根- >数据**值。
*   我们将递归检查当前根的**左**和**右子树**
*   在右子树也被遍历之后，我们将从地图中移除**当前总和+根- >数据**值，以便在除当前根之外的其他节点的进一步遍历中不考虑它

下面是上述方法的实现:

## C++

```
// C++ program to count the number
// of paths with sum equals to k
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    int data;
    Node *left, *right;
    Node(int x)
    {
        data = x;
        left = right = NULL;
    }
};

// Function to backtrack the tree path and
// add each path sum in the unordered map
void k_paths(Node* root, int k, unordered_map<int, int>& p,
                                         int sum, int &res)
{
    // If root is not null
    if (root)
    {
        // If root value and previous sum equal
        // to k then increase the count 
        if (sum + root->data == k)
            res++;

        // Add those values also which differes
        // by the current sum and root data by k
        res += p[sum + root->data - k];

        // Insert the sum + root value in the map
        p[sum + root->data]++;

        // Move to left and right trees
        k_paths(root->left, k, p, sum + root->data, res);
        k_paths(root->right, k, p, sum + root->data, res);

        // remove the sum + root->data value from the
        // map if they are n not required further or
        // they do no sum up to k in any way
        p[sum + root->data]--;
    }
}

// Function to print the count
// of paths with sum equals to k
int printCount(Node* root, int k)
{
    // To store the required answer
    int res = 0;

    // To store the sum
    unordered_map<int, int> p;

    // Function call
    k_paths(root, k, p, 0, res);

    // Return the required answer
    return res;
}

// Driver code
int main()
{
    Node* root = new Node(1);
    root->left = new Node(2);
    root->left->left = new Node(1);
    root->left->right = new Node(2);
    root->right = new Node(-1);
    root->right->left = new Node(3);
    root->right->left->left = new Node(2);
    root->right->left->right = new Node(5);

    int k = 3;
    cout << "No of paths with sum equals to " <<  k
         << " are : "  << printCount(root, k) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all root to leaf
// paths with there relative position
import java.util.ArrayList;
import java.util.HashMap;

class Graph{

static int res;

// tree structure
static class Node
{
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        this.left = this.right = null;
    }
};

// Function to backtrack the tree path and
// add each path sum in the unordered map
static void k_paths(Node root, int k,
  HashMap<Integer, Integer> p, int sum)
{

    // If root is not null
    if (root != null)
    {

        // If root value and previous sum equal
        // to k then increase the count
        if (sum + root.data == k)
            res++;

        // Add those values also which differes
        // by the current sum and root data by k
        res += p.get(sum + root.data - k) == null ?
           0 : p.get(sum + root.data - k);

        // Insert the sum + root value in the map
        if (!p.containsKey(sum + root.data))
        {
            p.put(sum + root.data, 0);
        }
        p.put(sum + root.data,
        p.get(sum + root.data) + 1);

        // Move to left and right trees
        k_paths(root.left, k, p,
                sum + root.data);
        k_paths(root.right, k, p,
                sum + root.data);

        // Remove the sum + root.data value
        // from the map if they are n not
        // required further or they do no
        // sum up to k in any way
        p.put(sum + root.data,
        p.get(sum + root.data) - 1);
    }
}

// Function to print the count
// of paths with sum equals to k
static int printCount(Node root, int k)
{

    // To store the sum
    HashMap<Integer, Integer> p = new HashMap<>();

    // Function call
    k_paths(root, k, p, 0);

    // Return the required answer
    return res;
}

// Driver code
public static void main(String[] args)
{
    res = 0;
    Node root = new Node(1);
    root.left = new Node(2);
    root.left.left = new Node(1);
    root.left.right = new Node(2);
    root.right = new Node(-1);
    root.right.left = new Node(3);
    root.right.left.left = new Node(2);
    root.right.left.right = new Node(5);

    int k = 3;
    System.out.printf("No of paths with sum " +
                      "equals to %d are: %d\n", k,
                      printCount(root, k));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python program to count the number
# of paths with sum equals to k

# Binary tree node
from typing import Dict
class Node:
    def __init__(self, x: int) -> None:
        self.data = x
        self.left = None
        self.right = None
res = 0

# Function to backtrack the tree path and
# add each path sum in the unordered map
def k_paths(root: Node, k: int, p: Dict, sum: int) -> None:
    global res

    # If root is not null
    if (root):

        # If root value and previous sum equal
        # to k then increase the count
        if (sum + root.data == k):
            res += 1

        # Add those values also which differes
        # by the current sum and root data by k
        val = sum + root.data - k
        if val in p:
            res += p[val]
        else:
            res += 0

        # Insert the sum + root value in the map
        if (sum + root.data) not in p:
            p[sum + root.data] = 0
        p[sum + root.data] += 1

        # Move to left and right trees
        k_paths(root.left, k, p, sum + root.data)
        k_paths(root.right, k, p, sum + root.data)

        # remove the sum + root.data value from the
        # map if they are n not required further or
        # they do no sum up to k in any way
        p[sum + root.data] -= 1

# Function to print the count
# of paths with sum equals to k
def printCount(root: Node, k: int) -> int:

    # To store the required answer
    global res

    # To store the sum
    p = dict()

    # Function call
    k_paths(root, k, p, 0)

    # return res

# Driver code
if __name__ == "__main__":
    root = Node(1)
    root.left = Node(2)
    root.left.left = Node(1)
    root.left.right = Node(2)
    root.right = Node(-1)
    root.right.left = Node(3)
    root.right.left.left = Node(2)
    root.right.left.right = Node(5)

    k = 3
    printCount(root, k)
    print("No of paths with sum equals to {} are : {}".format(k, res))

# This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>

// Javascript program to print all root to leaf
// paths with there relative position
let res;

// Tree structure
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Function to backtrack the tree path and
// add each path sum in the unordered map
function k_paths(root, k, p, sum)
{

    // If root is not null
    if (root != null)
    {

        // If root value and previous sum equal
        // to k then increase the count
        if (sum + root.data == k)
            res++;

        // Add those values also which differes
        // by the current sum and root data by k
        res += p.get(sum + root.data - k) == null ?
           0 : p.get(sum + root.data - k);

        // Insert the sum + root value in the map
        if (!p.has(sum + root.data))
        {
            p.set(sum + root.data, 0);
        }
        p.set(sum + root.data,
        p.get(sum + root.data) + 1);

        // Move to left and right trees
        k_paths(root.left, k, p,
                sum + root.data);
        k_paths(root.right, k, p,
                sum + root.data);

        // Remove the sum + root.data value
        // from the map if they are n not
        // required further or they do no
        // sum up to k in any way
        p.set(sum + root.data,
        p.get(sum + root.data) - 1);
    }
}

// Function to print the count
// of paths with sum equals to k
function printCount(root, k)
{

    // To store the sum
    let p = new Map();

    // Function call
    k_paths(root, k, p, 0);

    // Return the required answer
    return res;
}

// Driver code
res = 0;
let root = new Node(1);
root.left = new Node(2);
root.left.left = new Node(1);
root.left.right = new Node(2);
root.right = new Node(-1);
root.right.left = new Node(3);
root.right.left.left = new Node(2);
root.right.left.right = new Node(5);

let k = 3;
document.write("No of paths with sum " +
               "equals to " + k + " are: " +
               printCount(root, k));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
No of paths with sum equals to 3 are : 4
```