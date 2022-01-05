# 二叉树中每一级要相加的最小值，使所有级和相等

> 原文:[https://www . geeksforgeeks . org/二进制树中每一级要增加的最小值，使所有级别的总和相等/](https://www.geeksforgeeks.org/minimum-value-to-be-added-at-each-level-in-binary-tree-to-make-all-level-sum-equal/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到所有大于或等于零的**最小值**值，这些值应该在每一级相加，使每一级**的和等于**。

**示例:**

> **输入:**
> **1
> /\
> 2 3
> /\
> 4 5
> **输出:** 8 4 0
> **说明:**每一级的初和为{1，5，9}。为了使所有级别总和相等，要添加的最小值为{8，4，0}。所以每一级的最终和变成{ 1**+**+T17】8、5**+**+T21】4、9**+**+T25】0}即{9，9，9}。**
> 
> ****输入:**
> **8
> /\
> 3 10
> /\ \
> 1 6 14
> /\/
> 4 7 13
> /T12】输出: 16 11 3 0****

******方法:**给定的问题可以通过[求二叉树中的最大水平和来解决。](https://www.geeksforgeeks.org/find-level-maximum-sum-binary-tree/)通过[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)，在每一级应该相加的**最小值**必须等于二叉树中该级的[和](https://www.geeksforgeeks.org/sum-of-all-the-levels-in-a-binary-search-tree/)与二叉树中最大**级和之间的**差**。******

**下面是上述方法的实现:**

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

// Node class
class Node {
public:
    int data;
    Node *left, *right;
    Node(int item)
    {
        data = item;
        left = right = NULL;
    }
};

// Function to find sum of nodes
// present in a single level.
void Utilfun(Node* root, int level, vector<int>& ans)
{
    if (root == NULL) {
        return;
    }

    // Adding the data
    // of all the level
    if (ans.size() == level) {
        ans.push_back(root->data);
    }

    // If previous node data is already
    // then update ans
    else {
        int val = ans[level] + root->data;
        ans[level] = val;
    }

    // Basic dfs approach to traverse
    // on all the nodes with next level
    Utilfun(root->left, level + 1, ans);
    Utilfun(root->right, level + 1, ans);
}

// Function to find the minimum
// value added to make each level
// sum equal
vector<int>
levelOrderAP(Node* root)
{

    // Initialization of array
    vector<int> finalAns;

    // If root is null
    if (root == NULL) {
        return finalAns;
    }

    // Function Call
    Utilfun(root, 0, finalAns);
    int maxi = INT_MIN;

    // finding the maximum element
    for (int ele : finalAns) {
        maxi = max(maxi, ele);
    }
    // Subtracting all the elements
    // from maximum elements
    for (int i = 0; i < finalAns.size(); i++) {
        int val = maxi - finalAns[i];
        finalAns[i] = val;
    }
    return finalAns;
}

// Driver Code
int main()
{
    Node* root = new Node(8);
    root->left = new Node(3);
    root->right = new Node(10);
    root->left->left = new Node(1);
    root->left->right = new Node(6);
    root->right->right = new Node(14);
    root->left->right->left = new Node(4);
    root->left->right->right = new Node(7);
    root->right->right->left = new Node(13);

    vector<int> ans = levelOrderAP(root);
    for (auto i : ans) {
        cout << i << " ";
    }
    return 0;
}

// This code is contributed by maddler.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

// Node class
class Node {
    int data;
    Node left, right;
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// Binary tree class
class BinaryTree {
    Node root;
    public BinaryTree()
    {
        root = null;
    }

    // Function to find the minimum
    // value added to make each level
    // sum equal
    static ArrayList<Integer> levelOrderAP(Node root)
    {

        // Initialization of array
        ArrayList<Integer> finalAns = new ArrayList<>();

        // If root is null
        if (root == null) {
            return finalAns;
        }

        // Function Call
        Utilfun(root, 0, finalAns);
        int maxi = Integer.MIN_VALUE;

        // finding the maximum element
        for (int ele : finalAns) {
            maxi = Math.max(maxi, ele);
        }
        // Subtracting all the elements
        // from maximum elements
        for (int i = 0; i < finalAns.size(); i++) {
            int val = maxi - finalAns.get(i);
            finalAns.set(i, val);
        }
        return finalAns;
    }

    // Function to find sum of nodes
    // present in a single level.
    static void Utilfun(Node root,
                        int level,
                        ArrayList<Integer> ans)
    {
        if (root == null) {
            return;
        }

        // Adding the data
        // of all the level
        if (ans.size() == level) {
            ans.add(root.data);
        }

        // If previous node data is already
        // then update ans
        else {
            int val = ans.get(level)
                      + root.data;
            ans.set(level, val);
        }

        // Basic dfs approach to traverse
        // on all the nodes with next level
        Utilfun(root.left, level + 1, ans);
        Utilfun(root.right, level + 1, ans);
    }

    // Driver Code
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(8);
        tree.root.left = new Node(3);
        tree.root.right = new Node(10);
        tree.root.left.left = new Node(1);
        tree.root.left.right = new Node(6);
        tree.root.right.right = new Node(14);
        tree.root.left.right.left = new Node(4);
        tree.root.left.right.right = new Node(7);
        tree.root.right.right.left = new Node(13);

        ArrayList<Integer> ans
            = levelOrderAP(tree.root);
        System.out.println(ans);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach
import sys

# Structure of Node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def newNode(data):
    temp = Node(data)
    return temp

# Function to find the minimum
# value added to make each level
# sum equal
def levelOrderAP(root):
    # Initialization of array
    finalAns = []

    # If root is null
    if (root == None):
        return finalAns

    # Function Call
    Utilfun(root, 0, finalAns)
    maxi = -sys.maxsize

    # finding the maximum element
    for ele in range(len(finalAns)):
        maxi = max(maxi, finalAns[ele])
    # Subtracting all the elements
    # from maximum elements
    for i in range(len(finalAns)):
        val = maxi - finalAns[i]
        finalAns[i] = val
    return finalAns

# Function to find sum of nodes
# present in a single level.
def Utilfun(root, level, ans):
    if (root == None):
        return

    # Adding the data
    # of all the level
    if (len(ans) == level):
        ans.append(root.data)

    # If previous node data is already
    # then update ans
    else:
        val = ans[level] + root.data
        ans[level] = val

    # Basic dfs approach to traverse
    # on all the nodes with next level
    Utilfun(root.left, level + 1, ans)
    Utilfun(root.right, level + 1, ans)

root = newNode(8)
root.left = newNode(3)
root.right = newNode(10)
root.left.left = newNode(1)
root.left.right = newNode(6)
root.right.right = newNode(14)
root.left.right.left = newNode(4)
root.left.right.right = newNode(7)
root.right.right.left = newNode(13)

ans = levelOrderAP(root)
print("[", end="")
for i in range(len(ans) - 1):
    print(ans[i], ", ", sep = "", end = "")
print(ans[-1], "]", sep = "")

# This code is contributed by rameshtravel07.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

public class Node
{
    public int data;
    public Node left, right;
};

static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

   // Function to find the minimum
    // value added to make each level
    // sum equal
    static List<int> levelOrderAP(Node root)
    {

        // Initialization of array
        List<int> finalAns = new List<int>();

        // If root is null
        if (root == null) {
            return finalAns;
        }

        // Function Call
        Utilfun(root, 0, finalAns);
        int maxi = Int32.MinValue;

        // finding the maximum element
        foreach (int ele in finalAns) {
            maxi = Math.Max(maxi, ele);
        }
        // Subtracting all the elements
        // from maximum elements
        for (int i = 0; i < finalAns.Count; i++) {
            int val = maxi - finalAns[i];
            finalAns[i] = val;
        }
        return finalAns;
    }

    // Function to find sum of nodes
    // present in a single level.
    static void Utilfun(Node root,
                        int level,
                        List<int> ans)
    {
        if (root == null) {
            return;
        }

        // Adding the data
        // of all the level
        if (ans.Count == level) {
            ans.Add(root.data);
        }

        // If previous node data is already
        // then update ans
        else {
            int val = ans[level]
                      + root.data;
            ans[level] = val;
        }

        // Basic dfs approach to traverse
        // on all the nodes with next level
        Utilfun(root.left, level + 1, ans);
        Utilfun(root.right, level + 1, ans);
    }

    // Driver Code
    public static void Main()
    {
        Node root = newNode(8);
        root.left = newNode(3);
        root.right = newNode(10);
        root.left.left = newNode(1);
        root.left.right = newNode(6);
        root.right.right = newNode(14);
        root.left.right.left = newNode(4);
        root.left.right.right = newNode(7);
        root.right.right.left = newNode(13);

        List<int> ans = levelOrderAP(root);
        foreach(int i in ans)
          Console.Write(i+ " ");
    }
}

// This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>
    // Javascript program for the above approach

    class Node
    {
        constructor(data) {
           this.data = data;
           this.left = null;
           this.right = null;
        }
    }

    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

   // Function to find the minimum
    // value added to make each level
    // sum equal
    function levelOrderAP(root)
    {

        // Initialization of array
        let finalAns = [];

        // If root is null
        if (root == null) {
            return finalAns;
        }

        // Function Call
        Utilfun(root, 0, finalAns);
        let maxi = Number.MIN_VALUE;

        // finding the maximum element
        for(let ele = 0; ele < finalAns.length; ele++) {
            maxi = Math.max(maxi, finalAns[ele]);
        }
        // Subtracting all the elements
        // from maximum elements
        for (let i = 0; i < finalAns.length; i++) {
            let val = maxi - finalAns[i];
            finalAns[i] = val;
        }
        return finalAns;
    }

    // Function to find sum of nodes
    // present in a single level.
    function Utilfun(root, level, ans)
    {
        if (root == null) {
            return;
        }

        // Adding the data
        // of all the level
        if (ans.length == level) {
            ans.push(root.data);
        }

        // If previous node data is already
        // then update ans
        else {
            let val = ans[level] + root.data;
            ans[level] = val;
        }

        // Basic dfs approach to traverse
        // on all the nodes with next level
        Utilfun(root.left, level + 1, ans);
        Utilfun(root.right, level + 1, ans);
    }

    let root = newNode(8);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.right.right = newNode(14);
    root.left.right.left = newNode(4);
    root.left.right.right = newNode(7);
    root.right.right.left = newNode(13);

    let ans = levelOrderAP(root);
    document.write("[");
    for(let i = 0; i < ans.length - 1; i++)
    {
        document.write(ans[i] + ", ");
    }
    document.write(ans[ans.length - 1] + "]");

// This code is contributed by decode2207.
</script>
```

****Output**

```
[16, 11, 3, 0]
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**