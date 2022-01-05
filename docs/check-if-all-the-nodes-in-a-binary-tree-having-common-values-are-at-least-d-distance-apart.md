# 检查二叉树中所有具有公共值的节点之间的距离是否至少为 D

> 原文:[https://www . geeksforgeeks . org/check-如果具有公共值的二叉树中的所有节点相距至少 d 距离/](https://www.geeksforgeeks.org/check-if-all-the-nodes-in-a-binary-tree-having-common-values-are-at-least-d-distance-apart/)

给定一个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) 和一个整数 **D** ，任务是检查树中所有相同节点值对之间的距离是否为？ **D** 与否。如果发现是真的，那么打印**是**。否则，打印**否**。

**示例:**

> **输入:** D = 7
> 
> ```
>                 1
>               /   \ 
>              2     3
>             / \   /  \ 
>            4   3  4   4
> ```
> 
> **输出:**是
> T3】说明:T5】节点重复值为 3 和 4。
> 值为 3 的两个节点之间的距离为 3。
> 任意一对值为 4 的节点之间的最大距离为 4。
> 因此，这些距离没有一个超过 7
> 
> **输入:** D = 1
> 
> ```
>           3
>          / \
>         3   3
>              \
>               3
> ```
> 
> **输出:**否

**方法:**
思路是观察问题类似于[求一棵树的两个节点之间的距离](https://www.geeksforgeeks.org/find-distance-between-two-nodes-of-a-binary-tree/)。但是可以有多对节点，我们必须找到它们的距离。请遵循以下步骤:

1.  对给定的树执行[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，找出重复的节点对之间的距离。
2.  使用[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)找到树中重复的节点。
3.  对于特定值的每个重复节点，找出任意对之间的最大可能距离。
4.  如果该距离为> **D** ，则打印“否”。
5.  如果没有发现这样的节点值具有包含该值的对，超过 **D、**，则打印“是”。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to count the frequency of
// node value present in the tree
void frequencyCounts(unordered_map<int, int>& map,
                     Node* root)
{
    if (root == NULL)
        return;
    map[root->key]++;

    frequencyCounts(map, root->left);
    frequencyCounts(map, root->right);
}

// Function that returns the max distance
// between the nodes that have the same key
int computeDistance(Node* root, int value)
{
    if (root == NULL) {
        return -1;
    }

    int left
        = computeDistance(root->left, value);

    int right
        = computeDistance(root->right, value);

    // If right and left subtree did not
    // have node whose key is value
    if (left == -1 && right == -1) {

        // Check if the current node
        // is equal to value
        if (root->key == value) {
            return 1;
        }
        else
            return -1;
    }

    // If the left subtree has no node
    // whose key is equal to value
    if (left == -1) {
        return right + 1;
    }

    // If the right subtree has no node
    // whose key is equal to value
    if (right == -1) {
        return left + 1;
    }
    else {
        return 1 + max(left, right);
    }
    return -1;
}

// Function that finds if the distance
// between any same nodes is at most K
void solve(Node* root, int dist)
{

    // Create the map to look
    // for same value of nodes
    unordered_map<int, int> map;

    // Counting the frequency of nodes
    frequencyCounts(map, root);
    int flag = 0;

    for (auto it = map.begin();
         it != map.end(); it++) {

        if (it->second > 1) {

            // If the returned value of
            // distance is exceeds dist
            int result
                = computeDistance(root, it->first);

            if (result > dist || result == -1) {
                flag = 1;
                break;
            }
        }
    }

    // Print the result
    flag == 0 ? cout << "Yes\n" : cout << "No\n";
}

// Driver Code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->right = newNode(4);
    root->right->left = newNode(4);

    int dist = 7;

    solve(root, dist);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure of a Tree node
static class Node
{
    int key;
    Node left, right;
};

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to count the frequency of
// node value present in the tree
static void frequencyCounts(HashMap<Integer,
                                    Integer> map,
                            Node root)
{
    if (root == null)
        return;

    if(map.containsKey(root.key))
        map.put(root.key, map.get(root.key) + 1);
    else
        map.put(root.key, 1);

    frequencyCounts(map, root.left);
    frequencyCounts(map, root.right);
}

// Function that returns the max distance
// between the nodes that have the same key
static int computeDistance(Node root, int value)
{
    if (root == null)
    {
        return -1;
    }

    int left = computeDistance(root.left, value);
    int right = computeDistance(root.right, value);

    // If right and left subtree did not
    // have node whose key is value
    if (left == -1 && right == -1)
    {

        // Check if the current node
        // is equal to value
        if (root.key == value)
        {
            return 1;
        }
        else
            return -1;
    }

    // If the left subtree has no node
    // whose key is equal to value
    if (left == -1)
    {
        return right + 1;
    }

    // If the right subtree has no node
    // whose key is equal to value
    if (right == -1)
    {
        return left + 1;
    }
    else
    {
        return 1 + Math.max(left, right);
    }
}

// Function that finds if the distance
// between any same nodes is at most K
static void solve(Node root, int dist)
{

    // Create the map to look
    // for same value of nodes
    HashMap<Integer,
            Integer> map = new HashMap<Integer,
                                       Integer>();

    // Counting the frequency of nodes
    frequencyCounts(map, root);
    int flag = 0;

    for(Map.Entry<Integer,
                  Integer> it : map.entrySet())
    {
        if (it.getValue() > 1)
        {

            // If the returned value of
            // distance is exceeds dist
            int result = computeDistance(
                         root, it.getKey());

            if (result > dist || result == -1)
            {
                flag = 1;
                break;
            }
        }
    }

    // Print the result
    if(flag == 0)
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}

// Driver Code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.right = newNode(4);
    root.right.left = newNode(4);

    int dist = 7;

    solve(root, dist);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of a Tree node
# Function to create a new node
mp = {}

class newNode:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to count the frequency
# of node value present in the tree
def frequencyCounts(root):

    global mp

    if (root == None):
        return

    mp[root.key] = mp.get(root.key, 0) + 1
    frequencyCounts(root.left)
    frequencyCounts(root.right)

# Function that returns the max
# distance between the nodes that
# have the same key
def computeDistance(root, value):

    if (root == None):
        return -1

    left = computeDistance(root.left,
                           value)
    right = computeDistance(root.right,
                            value)

    # If right and left subtree
    # did not have node whose
    # key is value
    if (left == -1 and
        right == -1):

        # Check if the current node
        # is equal to value
        if (root.key == value):
            return 1
        else:
            return -1

    # If the left subtree has
    # no node whose key is equal
    # to value
    if (left == -1):
        return right + 1

    # If the right subtree has
    # no node whose key is equal
    # to value
    if (right == -1):
        return left + 1
    else:
        return 1 + max(left, right)
    return -1

# Function that finds if the
# distance between any same
# nodes is at most K
def solve(root, dist):

    # Create the mp to look
    # for same value of nodes
    global mp

    # Counting the frequency
    # of nodes
    frequencyCounts(root)
    flag = 0

    for key,value in mp.items():
        if(value > 1):

            # If the returned value of
            # distance is exceeds dist
            result = computeDistance(root,
                                     key)

            if (result > dist or
                result == -1):
                flag = 1
                break

    # Print the result
    if flag == 0:
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(3)
    root.right.right = newNode(4)
    root.right.left = newNode(4)
    dist = 7
    solve(root, dist)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Structure of a Tree node
public

 class Node
{
    public

 int key;
    public

 Node left, right;
};

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to count the frequency of
// node value present in the tree
static void frequencyCounts(Dictionary<int, int> map,
                            Node root)
{
    if (root == null)
        return;

    if(map.ContainsKey(root.key))
        map[root.key] = map[root.key]+1;
    else
        map[root.key] = 1;

    frequencyCounts(map, root.left);
    frequencyCounts(map, root.right);
}

// Function that returns the max distance
// between the nodes that have the same key
static int computeDistance(Node root, int value)
{
    if (root == null)
    {
        return -1;
    }

    int left = computeDistance(root.left, value);
    int right = computeDistance(root.right, value);

    // If right and left subtree did not
    // have node whose key is value
    if (left == -1 && right == -1)
    {

        // Check if the current node
        // is equal to value
        if (root.key == value)
        {
            return 1;
        }
        else
            return -1;
    }

    // If the left subtree has no node
    // whose key is equal to value
    if (left == -1)
    {
        return right + 1;
    }

    // If the right subtree has no node
    // whose key is equal to value
    if (right == -1)
    {
        return left + 1;
    }
    else
    {
        return 1 + Math.Max(left, right);
    }
}

// Function that finds if the distance
// between any same nodes is at most K
static void solve(Node root, int dist)
{

    // Create the map to look
    // for same value of nodes
    Dictionary<int,
            int> map = new Dictionary<int, int>();

    // Counting the frequency of nodes
    frequencyCounts(map, root);
    int flag = 0;

    foreach(KeyValuePair<int, int> it in map)
    {
        if (it.Value > 1)
        {

            // If the returned value of
            // distance is exceeds dist
            int result = computeDistance(
                         root, it.Key);

            if (result > dist || result == -1)
            {
                flag = 1;
                break;
            }
        }
    }

    // Print the result
    if(flag == 0)
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}

// Driver Code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.right = newNode(4);
    root.right.left = newNode(4);

    int dist = 7;

    solve(root, dist);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
    // Javascript Program to implement the above approach

    // Structure of a Tree node
    class Node
    {
        constructor(key) {
           this.key = key;
           this.left = this.right = null;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    // Function to count the frequency of
    // node value present in the tree
    function frequencyCounts(map, root)
    {
        if (root == null)
            return;

        if(map.has(root.key))
            map.set(root.key, map.get(root.key) + 1);
        else
            map.set(root.key, 1);

        frequencyCounts(map, root.left);
        frequencyCounts(map, root.right);
    }

    // Function that returns the max distance
    // between the nodes that have the same key
    function computeDistance(root, value)
    {
        if (root == null)
        {
            return -1;
        }

        let left = computeDistance(root.left, value);
        let right = computeDistance(root.right, value);

        // If right and left subtree did not
        // have node whose key is value
        if (left == -1 && right == -1)
        {

            // Check if the current node
            // is equal to value
            if (root.key == value)
            {
                return 1;
            }
            else
                return -1;
        }

        // If the left subtree has no node
        // whose key is equal to value
        if (left == -1)
        {
            return right + 1;
        }

        // If the right subtree has no node
        // whose key is equal to value
        if (right == -1)
        {
            return left + 1;
        }
        else
        {
            return 1 + Math.max(left, right);
        }
    }

    // Function that finds if the distance
    // between any same nodes is at most K
    function solve(root, dist)
    {

        // Create the map to look
        // for same value of nodes
        let map = new Map();

        // Counting the frequency of nodes
        frequencyCounts(map, root);
        let flag = 0;

        map.forEach((values,keys)=>{
            if (values > 1)
            {

                // If the returned value of
                // distance is exceeds dist
                let result = computeDistance(root, keys);

                if (result > dist || result == -1)
                {
                    flag = 1;
                    map.clear();
                }
            }
        })

        // Print the result
        if(flag == 0)
            document.write("Yes");
        else
            document.write("No");
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.right = newNode(4);
    root.right.left = newNode(4);

    let dist = 7;

    solve(root, dist);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*