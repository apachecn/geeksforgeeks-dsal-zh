# 打印二叉树中的所有 k-sum 路径

> 原文:[https://www . geesforgeks . org/print-k-sum-path-二叉树/](https://www.geeksforgeeks.org/print-k-sum-paths-binary-tree/)

给出了二叉树和数 k。打印树中的每条路径，路径中节点的和为 k.
一条路径可以从任意节点开始，到任意节点结束，且必须只向下，即不必是根节点和叶节点；负数也可以出现在树中。
**例:**

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

Output :
3 2 
3 1 1 
1 3 1 
4 1 
1 -1 4 1 
-1 4 2 
5 
1 -1 5 
```

来源:[亚马逊面试体验集-323](https://www.geeksforgeeks.org/amazon-interview-experience-set-323-software-development-engineer-off-campus/)

请注意，这个问题与[寻找从根到叶的 k-sum 路径](https://www.geeksforgeeks.org/print-paths-root-specified-sum-binary-tree/)有很大的不同。在这里，每个节点都可以被视为根，因此路径可以在任何节点开始和结束。
解决这个问题的基本思路是对给定的树进行一次前序遍历。我们还需要一个容器(向量)来跟踪通向该节点的路径。在每个节点，我们检查是否有任何与 k 相加的路径，如果有，我们打印路径并递归地打印每个路径。
下面是同样的实现。

## C++

```
// C++ program to print all paths with sum k.
#include <bits/stdc++.h>
using namespace std;

// utility function to print contents of
// a vector from index i to it's end
void printVector(const vector<int>& v, int i)
{
    for (int j = i; j < v.size(); j++)
        cout << v[j] << " ";
    cout << endl;
}

// binary tree node
struct Node {
    int data;
    Node *left, *right;
    Node(int x)
    {
        data = x;
        left = right = NULL;
    }
};

// This function prints all paths that have sum k
void printKPathUtil(Node* root, vector<int>& path, int k)
{
    // empty node
    if (!root)
        return;

    // add current node to the path
    path.push_back(root->data);

    // check if there's any k sum path
    // in the left sub-tree.
    printKPathUtil(root->left, path, k);

    // check if there's any k sum path
    // in the right sub-tree.
    printKPathUtil(root->right, path, k);

    // check if there's any k sum path that
    // terminates at this node
    // Traverse the entire path as
    // there can be negative elements too
    int f = 0;
    for (int j = path.size() - 1; j >= 0; j--) {
        f += path[j];

        // If path sum is k, print the path
        if (f == k)
            printVector(path, j);
    }

    // Remove the current element from the path
    path.pop_back();
}

// A wrapper over printKPathUtil()
void printKPath(Node* root, int k)
{
    vector<int> path;
    printKPathUtil(root, path, k);
}

// Driver code
int main()
{
    Node* root = new Node(1);
    root->left = new Node(3);
    root->left->left = new Node(2);
    root->left->right = new Node(1);
    root->left->right->left = new Node(1);
    root->right = new Node(-1);
    root->right->left = new Node(4);
    root->right->left->left = new Node(1);
    root->right->left->right = new Node(2);
    root->right->right = new Node(5);
    root->right->right->right = new Node(2);

    int k = 5;
    printKPath(root, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all paths with sum k.
import java.util.*;

class GFG {

    // utility function to print contents of
    // a vector from index i to it's end
    static void printVector(Vector<Integer> v, int i)
    {
        for (int j = i; j < v.size(); j++)
            System.out.print(v.get(j) + " ");
        System.out.println();
    }

    // binary tree node
    static class Node {
        int data;
        Node left, right;
        Node(int x)
        {
            data = x;
            left = right = null;
        }
    };
    static Vector<Integer> path = new Vector<Integer>();

    // This function prints all paths that have sum k
    static void printKPathUtil(Node root, int k)
    {
        // empty node
        if (root == null)
            return;

        // add current node to the path
        path.add(root.data);

        // check if there's any k sum path
        // in the left sub-tree.
        printKPathUtil(root.left, k);

        // check if there's any k sum path
        // in the right sub-tree.
        printKPathUtil(root.right, k);

        // check if there's any k sum path that
        // terminates at this node
        // Traverse the entire path as
        // there can be negative elements too
        int f = 0;
        for (int j = path.size() - 1; j >= 0; j--) {
            f += path.get(j);

            // If path sum is k, print the path
            if (f == k)
                printVector(path, j);
        }

        // Remove the current element from the path
        path.remove(path.size() - 1);
    }

    // A wrapper over printKPathUtil()
    static void printKPath(Node root, int k)
    {
        path = new Vector<Integer>();
        printKPathUtil(root, k);
    }

    // Driver code
    public static void main(String args[])
    {
        Node root = new Node(1);
        root.left = new Node(3);
        root.left.left = new Node(2);
        root.left.right = new Node(1);
        root.left.right.left = new Node(1);
        root.right = new Node(-1);
        root.right.left = new Node(4);
        root.right.left.left = new Node(1);
        root.right.left.right = new Node(2);
        root.right.right = new Node(5);
        root.right.right.right = new Node(2);

        int k = 5;
        printKPath(root, k);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print all paths
# with sum k

# utility function to print contents of
# a vector from index i to it's end

def printVector(v, i):
    for j in range(i, len(v)):
        print(v[j], end=" ")
    print()

# Binary Tree Node
""" utility that allocates a newNode
with the given key """

class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# This function prints all paths
# that have sum k

def printKPathUtil(root, path, k):

    # empty node
    if (not root):
        return

    # add current node to the path
    path.append(root.data)

    # check if there's any k sum path
    # in the left sub-tree.
    printKPathUtil(root.left, path, k)

    # check if there's any k sum path
    # in the right sub-tree.
    printKPathUtil(root.right, path, k)

    # check if there's any k sum path that
    # terminates at this node
    # Traverse the entire path as
    # there can be negative elements too
    f = 0
    for j in range(len(path) - 1, -1, -1):
        f += path[j]

        # If path sum is k, print the path
        if (f == k):
            printVector(path, j)

    # Remove the current element
    # from the path
    path.pop(-1)

# A wrapper over printKPathUtil()

def printKPath(root, k):

    path = []
    printKPathUtil(root, path, k)

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(3)
    root.left.left = newNode(2)
    root.left.right = newNode(1)
    root.left.right.left = newNode(1)
    root.right = newNode(-1)
    root.right.left = newNode(4)
    root.right.left.left = newNode(1)
    root.right.left.right = newNode(2)
    root.right.right = newNode(5)
    root.right.right.right = newNode(2)

    k = 5
    printKPath(root, k)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to print all paths with sum k.
using System;
using System.Collections.Generic;

class GFG {

    // utility function to print contents of
    // a vector from index i to it's end
    static void printList(List<int> v, int i)
    {
        for (int j = i; j < v.Count; j++)
            Console.Write(v[j] + " ");
        Console.WriteLine();
    }

    // binary tree node
    public class Node {
        public int data;
        public Node left, right;
        public Node(int x)
        {
            data = x;
            left = right = null;
        }
    };
    static List<int> path = new List<int>();

    // This function prints all paths that have sum k
    static void printKPathUtil(Node root, int k)
    {
        // empty node
        if (root == null)
            return;

        // add current node to the path
        path.Add(root.data);

        // check if there's any k sum path
        // in the left sub-tree.
        printKPathUtil(root.left, k);

        // check if there's any k sum path
        // in the right sub-tree.
        printKPathUtil(root.right, k);

        // check if there's any k sum path that
        // terminates at this node
        // Traverse the entire path as
        // there can be negative elements too
        int f = 0;
        for (int j = path.Count - 1; j >= 0; j--) {
            f += path[j];

            // If path sum is k, print the path
            if (f == k)
                printList(path, j);
        }

        // Remove the current element from the path
        path.RemoveAt(path.Count - 1);
    }

    // A wrapper over printKPathUtil()
    static void printKPath(Node root, int k)
    {
        path = new List<int>();
        printKPathUtil(root, k);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = new Node(1);
        root.left = new Node(3);
        root.left.left = new Node(2);
        root.left.right = new Node(1);
        root.left.right.left = new Node(1);
        root.right = new Node(-1);
        root.right.left = new Node(4);
        root.right.left.left = new Node(1);
        root.right.left.right = new Node(2);
        root.right.right = new Node(5);
        root.right.right.right = new Node(2);

        int k = 5;
        printKPath(root, k);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
// Tree node class for Binary Tree
// representation
class Node {
    constructor(data) {
        this.data = data;
        this.left = this.right = null;
    }
}

function printPathUtil(node, k, path_arr, all_path_arr) {
    if (node == null) {
        return;
    }

    let p1 = node.data.toString();

    let p2 = '';

    if (path_arr.length > 0) {
        p2 = path_arr + ',' + p1;
    }
    else {
        p2 = p1;
    }

    if (node.data == k) {
        all_path_arr.add(p1);
    }

    let sum = 0;

    let p2_arr = p2.split(',');

    for (let i = 0; i < p2_arr.length; i++) {
        sum = sum + Number(p2_arr[i]);
    }

    if (sum == k) {
        all_path_arr.add(p2);
    }

    printPathUtil(node.left, k, p1, all_path_arr)
    printPathUtil(node.left, k, p2, all_path_arr)
    printPathUtil(node.right, k, p1, all_path_arr)
    printPathUtil(node.right, k, p2, all_path_arr)

}

function printKPath(root, k) {
    let all_path_arr = new Set();
    printPathUtil(root, k, '', all_path_arr);
    return all_path_arr;
}

function printPaths(paths) {
    for (let data of paths) {
        document.write(data.replaceAll(',', ' '));
        document.write('<br>');
    }
}

// Driver code
let root = new Node(1);
root.left = new Node(3);
root.left.left = new Node(2);
root.left.right = new Node(1);
root.left.right.left = new Node(1);
root.right = new Node(-1);
root.right.left = new Node(4);
root.right.left.left = new Node(1);
root.right.left.right = new Node(2);
root.right.right = new Node(5);
root.right.right.right = new Node(2);

let k = 5;

printPaths(printKPath(root, k));

// This code is contributed by gaurav2146
```

**输出:**

```
3 2 
3 1 1 
1 3 1 
4 1 
1 -1 4 1 
-1 4 2 
5 
1 -1 5 
```

**时间复杂度:O(n*h*h)** ，因为路径向量的最大大小可以是 h

**空间复杂度:O(h)**

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由 [**Ashutosh Kumar**](https://in.linkedin.com/in/ashutosh-kumar-9527a7105) 投稿如果你喜欢 GeeksforGeeks 并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。