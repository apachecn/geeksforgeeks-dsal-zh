# 打印 N 元树的所有根到叶路径

> 原文:[https://www . geeksforgeeks . org/print-n 元树的所有根到叶路径/](https://www.geeksforgeeks.org/print-all-root-to-leaf-paths-of-an-n-ary-tree/)

给定一个 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，任务是[打印给定 **N 元树**的所有根到叶路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)。

**示例:**

> **输入:**
> 1
> /\
> 2 3
> /\
> 4 5 6
> /\
> 7 8
> 
> **产量:**T2【1 2 4】T3【1 3 5】T4【1 3 6 7】T5【1 3 6 8】
> 
> **输入:**
> 1
> /| \
> 2 5 3
> /\ \
> 4 5 6
> **输出:**
> 1 2 4
> 1 2 5
> 1 5
> 1 3 6

**方法:**解决这个问题的思路是使用[深度优先搜索](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)开始[遍历 N 元树](https://www.geeksforgeeks.org/preorder-traversal-of-n-ary-tree-without-recursion/)，并保持[插入在**向量**T9】中遇到的每个节点，直到遇到](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) [**叶节点**](https://www.geeksforgeeks.org/write-a-c-program-to-get-count-of-leaf-nodes-in-a-binary-tree/) 。每当遇到叶节点时，打印存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中的元素，作为当前遍历的根到叶路径，删除最后添加的叶，并检查下一个组合。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of an N ary tree node
class Node {
public:
    int data;
    vector<Node*> child;

    // Parameterized Constructor
    Node(int x)
        : data(x)
    {
    }
};

// Function to print the root to leaf
// path of the given N-ary Tree
void printPath(vector<int> vec)
{
    // Print elements in the vector
    for (int ele : vec) {
        cout << ele << " ";
    }
    cout << endl;
}

// Utility function to print all
// root to leaf paths of an Nary Tree
void printAllRootToLeafPaths(
    Node* root, vector<int> vec)
{
    // If root is null
    if (!root)
        return;

    // Insert current node's
    // data into the vector
    vec.push_back(root->data);

    // If current node is a leaf node
    if (root->child.empty()) {

        // Print the path
        printPath(vec);

        // Pop the leaf node
        // and return
        vec.pop_back();
        return;
    }

    // Recur for all children of
    // the current node
    for (int i = 0;
        i < root->child.size(); i++)

        // Recursive Function Call
        printAllRootToLeafPaths(
            root->child[i], vec);
}

// Function to print root to leaf path
void printAllRootToLeafPaths(Node* root)
{
    // If root is null, return
    if (!root)
        return;

    // Stores the root to leaf path
    vector<int> vec;

    // Utility function call
    printAllRootToLeafPaths(root, vec);
}

// Driver Code
int main()
{
    // Given N-Ary tree
    Node* root = new Node(1);
    (root->child).push_back(new Node(2));
    (root->child).push_back(new Node(3));
    (root->child[0]->child).push_back(new Node(4));
    (root->child[1]->child).push_back(new Node(5));
    (root->child[1]->child).push_back(new Node(6));
    (root->child[1]->child[1]->child)
        .push_back(new Node(7));
    (root->child[1]->child[1]->child)
        .push_back(new Node(8));

    // Function Call
    printAllRootToLeafPaths(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
class GFG
{

    // Structure of an N ary tree node
    static class Node
    {
        int data;
        ArrayList<Node> child;

        // Parameterized Constructor
        public Node(int x)
        {
            this.data = x;
            this.child = new ArrayList<>();
        }
    };

    // Function to print the root to leaf
    // path of the given N-ary Tree
    static void printPath(ArrayList<Integer> vec)
    {

        // Print elements in the vector
        for (int ele : vec)
        {
            System.out.print(ele + " ");
        }
        System.out.println();
    }

    // Utility function to print all
    // root to leaf paths of an Nary Tree
    static void printAllRootToLeafPaths(Node root, ArrayList<Integer> vec)
    {

        // If root is null
        if (root == null)
            return;

        // Insert current node's
        // data into the vector
        vec.add(root.data);

        // If current node is a leaf node
        if (root.child.isEmpty())
        {

            // Print the path
            printPath(vec);

            // Pop the leaf node
            // and return
            vec.remove(vec.size() - 1);
            return;
        }

        // Recur for all children of
        // the current node
        for (int i = 0; i < root.child.size(); i++)

            // Recursive Function Call
            printAllRootToLeafPaths(root.child.get(i), vec);
        vec.remove(vec.size() - 1);
    }

    // Function to print root to leaf path
    static void printAllRootToLeafPaths(Node root)
    {

        // If root is null, return
        if (root == null)
            return;

        // Stores the root to leaf path
        ArrayList<Integer> vec = new ArrayList<>();

        // Utility function call
        printAllRootToLeafPaths(root, vec);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given N-Ary tree
        Node root = new Node(1);
        (root.child).add(new Node(2));
        (root.child).add(new Node(3));
        (root.child.get(0).child).add(new Node(4));
        (root.child.get(1).child).add(new Node(5));
        (root.child.get(1).child).add(new Node(6));
        (root.child.get(1).child.get(1).child).add(new Node(7));
        (root.child.get(1).child.get(1).child).add(new Node(8));

        // Function Call
        printAllRootToLeafPaths(root);
    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of an N ary tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.child = []

# Function to print the root to leaf
# path of the given N-ary Tree
def printPath(vec):

    # Print elements in the vector
    for ele in vec:
        print(ele, end = " ")

    print()

# Utility function to print all
# root to leaf paths of an Nary Tree
def printAllRootToLeafPaths(root):

    global vec

    # If root is null
    if (not root):
        return

    # Insert current node's
    # data into the vector
    vec.append(root.data)

    # If current node is a leaf node
    if (len(root.child) == 0):

        # Print the path
        printPath(vec)

        # Pop the leaf node
        # and return
        vec.pop()
        return

    # Recur for all children of
    # the current node
    for i in range(len(root.child)):

        # Recursive Function Call
        printAllRootToLeafPaths(root.child[i])

    vec.pop()   

# Function to print root to leaf path
def printRootToLeafPaths(root):

    global vec

    # If root is null, return
    if (not root):
        return

    # Utility function call
    printAllRootToLeafPaths(root)

# Driver Code
if __name__ == '__main__':

    # Given N-Ary tree
    vec = []
    root = Node(1)
    root.child.append(Node(2))
    root.child.append(Node(3))
    root.child[0].child.append(Node(4))
    root.child[1].child.append(Node(5))
    root.child[1].child.append(Node(6))
    root.child[1].child[1].child.append(Node(7))
    root.child[1].child[1].child.append(Node(8))

    # Function Call
    printRootToLeafPaths(root)

# This code is contributed by mohit kumar 29
```

## C#

```
using System;
using System.Collections.Generic;

// Structure of an N ary tree node
public class Node
{
    public int data;
    public List<Node> child;

    // Parameterized Constructor
    public Node(int x)
    {
        this.data = x;
        this.child = new List<Node>();
    }
}

public class GFG
{

    // Function to print the root to leaf
    // path of the given N-ary Tree
    static void printPath(List<int> vec)
    {

        // Print elements in the vector
        foreach (int ele in vec)
        {
            Console.Write(ele + " ");
        }
        Console.WriteLine();
    }

    // Utility function to print all
    // root to leaf paths of an Nary Tree
    static void printAllRootToLeafPaths(Node root, List<int> vec)
    {

        // If root is null
        if (root == null)
            return;

        // Insert current node's
        // data into the vector
        vec.Add(root.data);

        // If current node is a leaf node
        if (root.child.Count == 0)
        {

            // Print the path
            printPath(vec);

            // Pop the leaf node
            // and return
            vec.RemoveAt(vec.Count - 1);
            return;
        }

        // Recur for all children of
        // the current node
        for (int i = 0; i < root.child.Count; i++)
        {
            // Recursive Function Call
            printAllRootToLeafPaths(root.child[i], vec);
        }
        vec.RemoveAt(vec.Count - 1);
    }

    // Function to print root to leaf path
    static void printAllRootToLeafPaths(Node root)
    {

        // If root is null, return
        if (root == null)
            return;

        // Stores the root to leaf path
        List<int> vec = new List<int>();

        // Utility function call
        printAllRootToLeafPaths(root, vec);
    }

    // Driver Code
    static public void Main ()
    {

        // Given N-Ary tree
        Node root = new Node(1);
        (root.child).Add(new Node(2));
        (root.child).Add(new Node(3));
        (root.child[0].child).Add(new Node(4));
        (root.child[1].child).Add(new Node(5));
        (root.child[1].child).Add(new Node(6));
        (root.child[1].child[1].child).Add(new Node(7));
        (root.child[1].child[1].child).Add(new Node(8));

        // Function Call
        printAllRootToLeafPaths(root);
    }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Structure of an N ary tree node
class Node
{
    constructor(x)
    {
        this.data = x;
            this.child = [];
    }
}

// Function to print the root to leaf
    // path of the given N-ary Tree
function  printPath(vec)
{
    // Print elements in the vector
        for (let ele=0;ele< vec.length;ele++)
        {
            document.write(vec[ele] + " ");
        }
        document.write("<br>");
}

// Utility function to print all
    // root to leaf paths of an Nary Tree
function printAllRootToLeafPaths(root,vec)
{
    // If root is null
        if (root == null)
            return;

        // Insert current node's
        // data into the vector
        vec.push(root.data);

        // If current node is a leaf node
        if (root.child.length==0)
        {

            // Print the path
            printPath(vec);

            // Pop the leaf node
            // and return
            vec.pop();
            return;
        }

        // Recur for all children of
        // the current node
        for (let i = 0; i < root.child.length; i++)

            // Recursive Function Call
            printAllRootToLeafPaths(root.child[i], vec);
        vec.pop();
}

// Function to print root to leaf path
function printAllRootToLeaf_Paths(root)
{
    // If root is null, return
        if (root == null)
            return;

        // Stores the root to leaf path
        let vec = [];

        // Utility function call
        printAllRootToLeafPaths(root, vec);
}

// Driver Code
let root = new Node(1);
(root.child).push(new Node(2));
(root.child).push(new Node(3));
(root.child[0].child).push(new Node(4));
(root.child[1].child).push(new Node(5));
(root.child[1].child).push(new Node(6));
(root.child[1].child[1].child).push(new Node(7));
(root.child[1].child[1].child).push(new Node(8));

// Function Call
printAllRootToLeaf_Paths(root);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
1 2 4 
1 3 5 
1 3 6 7 
1 3 6 8
```

***时间复杂度:** O(N)*
***空间复杂度:** O(N)*