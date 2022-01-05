# N 元树中的平均宽度

> 原文:[https://www . geesforgeks . org/average-width in a-n-ary-tree/](https://www.geeksforgeeks.org/average-width-in-a-n-ary-tree/)

给定一个由 **N** 个节点组成的[类属树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，任务是为给定树中的每个节点找到**平均宽度**。

> 每个节点的**平均宽度**可以通过该子树中的节点总数(包括节点本身)与该节点下的层次总数之比来计算。

**示例:**

> **输入:**
> **1
> /\
> 2 3
> /\/\ \
> 4 5 6 7 8
> **输出:** 1:2，2:1，3:2，4:1，5:1，6:1，7:1， 8:1
> **说明:**每个节点的平均宽度可以计算为
> 对于节点 1: 8/3 = 2
> 对于节点 2: 3/2 = 1
> 对于节点 3: 4/2 = 2
> 对于节点 4: 1/1 = 1
> 对于节点 5: 1/1 = 1
> 对于节点 6: 1/1 = 1
> 对于节点 7: 1/1 = 1
> 对于节点 8: 1/1**

****方法:**平均宽度可以通过求[N 元树](https://www.geeksforgeeks.org/calculate-number-nodes-subtrees-using-dfs/)中每个节点的子树大小和 N 元树中每个节点的级别或[高度来计算。两者都可以使用单次](https://www.geeksforgeeks.org/height-n-ary-tree-parent-array-given/) [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 遍历来计算。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
vector<vector<int> > ans;

// Node structure
struct Node {
    int val;
    vector<Node*> child;
};

// Utility function to create a new
// tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->val = key;
    return temp;
}

// Function to find levels and
// subtree sizes
vector<int> UtilityFun(Node* root, vector<vector<int> >& ans)
{
    if (root == nullptr)
        return { 0, 0 };

    // Num nodes and level with just
    // a single node
    int totalNodes = 1, totalLevels = 1;

    // Recur for all children
    for (int i = 0; i < root->child.size(); i++) {
        vector<int> info = UtilityFun(root->child[i], ans);
        totalNodes += info[0];
        totalLevels = max(totalLevels, 1 + info[1]);
    }

    // Finding the current Width
    int currentAverageWidth = totalNodes / totalLevels;

    // Storing in ans
    ans.push_back({ root->val, currentAverageWidth });

    return { totalNodes, totalLevels };
}

// Function to find the average width
// of all nodes
vector<vector<int> > findAvgWidth(Node* root)
{
    if (root == nullptr)
        return {};

    // Function Call
    UtilityFun(root, ans);
    return ans;
}

// Function to display the values
void display(vector<vector<int> > ans)
{
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i][0] << ":" << ans[i][1] << ", ";
    }
}

// Driver Code
int main()
{
    // Given Input
    Node* root = newNode(1);
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(3));
    (root->child[0]->child).push_back(newNode(4));
    (root->child[1]->child).push_back(newNode(5));
    (root->child[0]->child).push_back(newNode(6));
    (root->child[1])->child.push_back(newNode(7));
    (root->child[1]->child).push_back(newNode(8));

    // Function Call
    findAvgWidth(root);

    // Function Call
    display(ans);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
public class Main
{
    static Vector<Vector<Integer>> ans = new Vector<Vector<Integer>>();

    // Node structure
    static class Node {

        public int val;
        public Vector<Node> child;

        public Node(int key)
        {
            val = key;
            child = new Vector<Node>();
        }
    }

    // Utility function to create a new
    // tree node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    // Function to find levels and
    // subtree sizes
    static Vector<Integer> UtilityFun(Node root, Vector<Vector<Integer>> ans)
    {
        if (root == null)
        {
            Vector<Integer> temp = new Vector<Integer>();
            temp.add(0);
            temp.add(0);
            return temp;
        }

        // Num nodes and level with just
        // a single node
        int totalNodes = 1, totalLevels = 1;

        // Recur for all children
        for (int i = 0; i < root.child.size(); i++) {
            Vector<Integer> info = UtilityFun(root.child.get(i), ans);
            totalNodes += info.get(0);
            totalLevels = Math.max(totalLevels, 1 + info.get(1));
        }

        // Finding the current Width
        int currentAverageWidth = totalNodes / totalLevels;

        // Storing in ans
        Vector<Integer> temp = new Vector<Integer>();
        temp.add(root.val);
        temp.add(currentAverageWidth);
        ans.add(temp);

        temp = new Vector<Integer>();
        temp.add(totalNodes);
        temp.add(totalLevels);

        return temp;
    }

    // Function to find the average width
    // of all nodes
    static Vector<Vector<Integer>> findAvgWidth(Node root)
    {
        if (root == null)
            return new Vector<Vector<Integer>>();

        // Function Call
        UtilityFun(root, ans);
        return ans;
    }

    // Function to display the values
    static void display(Vector<Vector<Integer>> ans)
    {
        for (int i = 0; i < ans.size(); i++) {
            System.out.print(ans.get(i).get(0) + ":" + ans.get(i).get(1) + ", ");
        }
    }

    public static void main(String[] args)
    {
        // Given Input
        Node root = newNode(1);
        (root.child).add(newNode(2));
        (root.child).add(newNode(3));
        (root.child.get(0).child).add(newNode(4));
        (root.child.get(1).child).add(newNode(5));
        (root.child.get(0).child).add(newNode(6));
        (root.child.get(1)).child.add(newNode(7));
        (root.child.get(1).child).add(newNode(8));

        // Function Call
        findAvgWidth(root);

        // Function Call
        display(ans);
    }
}

// This code is contributed by suresh07.
```

## **蟒蛇 3**

```
# Python3 program for the above approach
ans = []

# Node structure
class Node:
    def __init__(self, key):
        self.val = key
        self.child = []

# Utility function to create a new
# tree node
def newNode(key):
    temp = Node(key)
    return temp

# Function to find levels and
# subtree sizes
def UtilityFun(root, ans):
    if (root == None):
        return [ 0, 0 ]

    # Num nodes and level with just
    # a single node
    totalNodes, totalLevels = 1, 1

    # Recur for all children
    for i in range(len(root.child)):
        info = UtilityFun(root.child[i], ans)
        totalNodes += info[0]
        totalLevels = max(totalLevels, 1 + info[1])

    # Finding the current Width
    currentAverageWidth = int(totalNodes / totalLevels)

    # Storing in ans
    ans.append([ root.val, currentAverageWidth ])

    return [ totalNodes, totalLevels ]

# Function to find the average width
# of all nodes
def findAvgWidth(root):
    if (root == None):
        return []

    # Function Call
    UtilityFun(root, ans)
    return ans

# Function to display the values
def display(ans):
    for i in range(len(ans)):
        print(ans[i][0], ":", ans[i][1], ", ", sep="",end="")

# Given Input
root = newNode(1)
(root.child).append(newNode(2))
(root.child).append(newNode(3))
(root.child[0].child).append(newNode(4))
(root.child[1].child).append(newNode(5))
(root.child[0].child).append(newNode(6))
(root.child[1]).child.append(newNode(7))
(root.child[1].child).append(newNode(8))

# Function Call
findAvgWidth(root)

# Function Call
display(ans)

# This code is contributed by divyesh072019.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    static List<List<int>> ans = new List<List<int>>();

    // Node structure
    class Node {

        public int val;
        public List<Node> child;

        public Node(int key)
        {
            val = key;
            child = new List<Node>();
        }
    }

    // Utility function to create a new
    // tree node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    // Function to find levels and
    // subtree sizes
    static List<int> UtilityFun(Node root, List<List<int>> ans)
    {
        if (root == null)
        {
            List<int> temp = new List<int>();
            temp.Add(0);
            temp.Add(0);
            return temp;
        }

        // Num nodes and level with just
        // a single node
        int totalNodes = 1, totalLevels = 1;

        // Recur for all children
        for (int i = 0; i < root.child.Count; i++) {
            List<int> info = UtilityFun(root.child[i], ans);
            totalNodes += info[0];
            totalLevels = Math.Max(totalLevels, 1 + info[1]);
        }

        // Finding the current Width
        int currentAverageWidth = totalNodes / totalLevels;

        // Storing in ans
        ans.Add(new List<int>{root.val, currentAverageWidth});

        return new List<int>{totalNodes, totalLevels};
    }

    // Function to find the average width
    // of all nodes
    static List<List<int>> findAvgWidth(Node root)
    {
        if (root == null)
            return new List<List<int>>();

        // Function Call
        UtilityFun(root, ans);
        return ans;
    }

    // Function to display the values
    static void display(List<List<int>> ans)
    {
        for (int i = 0; i < ans.Count; i++) {
            Console.Write(ans[i][0] + ":" + ans[i][1] + ", ");
        }
    }

  static void Main()
  {

    // Given Input
    Node root = newNode(1);
    (root.child).Add(newNode(2));
    (root.child).Add(newNode(3));
    (root.child[0].child).Add(newNode(4));
    (root.child[1].child).Add(newNode(5));
    (root.child[0].child).Add(newNode(6));
    (root.child[1]).child.Add(newNode(7));
    (root.child[1].child).Add(newNode(8));

    // Function Call
    findAvgWidth(root);

    // Function Call
    display(ans);
  }
}

// This code is contributed by mukesh07.
```

## **java 描述语言**

```
<script>
    // Javascript program for the above approach 

    let ans = []

    // Node structure
    class Node
    {
        constructor(key) {
           this.child = [];
           this.val = key;
        }
    }

    // Utility function to create a new
    // tree node
    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    // Function to find levels and
    // subtree sizes
    function UtilityFun(root, ans)
    {
        if (root == null)
            return [ 0, 0 ];

        // Num nodes and level with just
        // a single node
        let totalNodes = 1, totalLevels = 1;

        // Recur for all children
        for (let i = 0; i < root.child.length; i++) {
            let info = UtilityFun(root.child[i], ans);
            totalNodes += info[0];
            totalLevels = Math.max(totalLevels, 1 + info[1]);
        }

        // Finding the current Width
        let currentAverageWidth = parseInt(totalNodes / totalLevels, 10);

        // Storing in ans
        ans.push([ root.val, currentAverageWidth ]);

        return [ totalNodes, totalLevels ];
    }

    // Function to find the average width
    // of all nodes
    function findAvgWidth(root)
    {
        if (root == null)
            return [];

        // Function Call
        UtilityFun(root, ans);
        return ans;
    }

    // Function to display the values
    function display(ans)
    {
        for (let i = 0; i < ans.length; i++) {
            document.write(ans[i][0] + ":" + ans[i][1] + ", ");
        }
    }

    // Given Input
    let root = newNode(1);
    (root.child).push(newNode(2));
    (root.child).push(newNode(3));
    (root.child[0].child).push(newNode(4));
    (root.child[1].child).push(newNode(5));
    (root.child[0].child).push(newNode(6));
    (root.child[1]).child.push(newNode(7));
    (root.child[1].child).push(newNode(8));

    // Function Call
    findAvgWidth(root);

    // Function Call
    display(ans);

// Thi code is contributed by rameshtravel07.
</script>
```

****Output**

```
4:1, 6:1, 2:1, 5:1, 7:1, 8:1, 3:2, 1:2, 
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**