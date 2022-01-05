# 在 BST

中找到给定和的一对

> 原文:[https://www.geeksforgeeks.org/find-pair-given-sum-bst/](https://www.geeksforgeeks.org/find-pair-given-sum-bst/)

给定一个 [BST](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) 和一个和，找出是否有一对和给定的和。

**示例:**

```
Input : sum = 28
        Root of below tree
```

![](img/54ee2e767d7f4727213b46109e4d6d57.png)

```
Output : Pair is found (16, 12)
```

### [推荐:请先在“PRACTICE”上解决，再进行解决](https://practice.geeksforgeeks.org/problems/find-a-pair-with-given-target-in-bst/1)

我们在下面的帖子中讨论了不同的方法来找到一对给定和的。[在一个平衡的 BST](https://www.geeksforgeeks.org/find-a-pair-with-given-sum-in-bst/)
中找到一个给定和的配对在这篇文章中，讨论了基于散列的解决方案。我们按顺序遍历二叉查找树，并将节点的值插入一个集合中。还要检查任意节点，给定和与集合中节点值之间的差异，如果找到，则配对存在，否则不存在。

## C++

```
// CPP program to find a pair with
// given sum using hashing
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node *left, *right;
};

Node* NewNode(int data)
{
    Node* temp = (Node*)malloc(sizeof(Node));
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

Node* insert(Node* root, int key)
{
    if (root == NULL)
        return NewNode(key);
    if (key < root->data)
        root->left = insert(root->left, key);
    else
        root->right = insert(root->right, key);
    return root;
}

bool findpairUtil(Node* root, int sum,
                  unordered_set<int>& set)
{
    if (root == NULL)
        return false;

    if (findpairUtil(root->left, sum, set))
        return true;

    if (set.find(sum - root->data) != set.end()) {
        cout << "Pair is found (" << sum - root->data
             << ", " << root->data << ")" << endl;
        return true;
    }
    else
        set.insert(root->data);

    return findpairUtil(root->right, sum, set);
}

void findPair(Node* root, int sum)
{
    unordered_set<int> set;
    if (!findpairUtil(root, sum, set))
        cout << "Pairs do not exit" << endl;
}

// Driver code
int main()
{
    Node* root = NULL;
    root = insert(root, 15);
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 12);
    root = insert(root, 16);
    root = insert(root, 25);
    root = insert(root, 10);

    int sum = 33;
    findPair(root, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find a pair with
// given sum using hashing

import java.util.*;

class GFG {

    static class Node {
        int data;
        Node left, right;
    };

    static Node NewNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    static Node insert(Node root, int key)
    {
        if (root == null)
            return NewNode(key);
        if (key < root.data)
            root.left = insert(root.left, key);
        else
            root.right = insert(root.right, key);
        return root;
    }

    static boolean findpairUtil(Node root, int sum,
                                HashSet<Integer> set)
    {
        if (root == null)
            return false;

        if (findpairUtil(root.left, sum, set))
            return true;

        if (set.contains(sum - root.data)) {
            System.out.println("Pair is found ("
                               + (sum - root.data) + ", "
                               + root.data + ")");
            return true;
        }
        else
            set.add(root.data);

        return findpairUtil(root.right, sum, set);
    }

    static void findPair(Node root, int sum)
    {
        HashSet<Integer> set = new HashSet<Integer>();
        if (!findpairUtil(root, sum, set))
            System.out.print("Pairs do not exit"
                             + "\n");
    }

    // Driver code
    public static void main(String[] args)
    {
        Node root = null;
        root = insert(root, 15);
        root = insert(root, 10);
        root = insert(root, 20);
        root = insert(root, 8);
        root = insert(root, 12);
        root = insert(root, 16);
        root = insert(root, 25);
        root = insert(root, 10);

        int sum = 33;
        findPair(root, sum);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find a pair with
# given sum using hashing
import sys
import math

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def insert(root, data):
    if root is None:
        return Node(data)
    if(data < root.data):
        root.left = insert(root.left, data)
    if(data > root.data):
        root.right = insert(root.right, data)
    return root

def findPairUtil(root, summ, unsorted_set):
    if root is None:
        return False
    if findPairUtil(root.left, summ, unsorted_set):
        return True
    if unsorted_set and (summ-root.data) in unsorted_set:
        print("Pair is Found ({},{})".format(summ-root.data, root.data))
        return True
    else:
        unsorted_set.add(root.data)

    return findPairUtil(root.right, summ, unsorted_set)

def findPair(root, summ):
    unsorted_set = set()
    if(not findPairUtil(root, summ, unsorted_set)):
        print("Pair do not exist!")

# Driver code
if __name__ == '__main__':
    root = None
    root = insert(root, 15)
    root = insert(root, 10)
    root = insert(root, 20)
    root = insert(root, 8)
    root = insert(root, 12)
    root = insert(root, 16)
    root = insert(root, 25)
    root = insert(root, 10)
    summ = 33
    findPair(root, summ)

# This code is contributed by Vikash Kumar 37
```

## C#

```
// C# program to find a pair with
// given sum using hashing
using System;
using System.Collections.Generic;

class GFG {

    class Node {
        public int data;
        public Node left, right;
    };

    static Node NewNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    static Node insert(Node root, int key)
    {
        if (root == null)
            return NewNode(key);
        if (key < root.data)
            root.left = insert(root.left, key);
        else
            root.right = insert(root.right, key);
        return root;
    }

    static bool findpairUtil(Node root, int sum,
                             HashSet<int> set)
    {
        if (root == null)
            return false;

        if (findpairUtil(root.left, sum, set))
            return true;

        if (set.Contains(sum - root.data)) {
            Console.WriteLine("Pair is found ("
                              + (sum - root.data) + ", "
                              + root.data + ")");
            return true;
        }
        else
            set.Add(root.data);

        return findpairUtil(root.right, sum, set);
    }

    static void findPair(Node root, int sum)
    {
        HashSet<int> set = new HashSet<int>();
        if (!findpairUtil(root, sum, set))
            Console.Write("Pairs do not exit"
                          + "\n");
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = null;
        root = insert(root, 15);
        root = insert(root, 10);
        root = insert(root, 20);
        root = insert(root, 8);
        root = insert(root, 12);
        root = insert(root, 16);
        root = insert(root, 25);
        root = insert(root, 10);

        int sum = 33;
        findPair(root, sum);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find a pair with
// given sum using hashing
class Node {
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};
function NewNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}
function insert(root, key)
{
    if (root == null)
        return NewNode(key);
    if (key < root.data)
        root.left = insert(root.left, key);
    else
        root.right = insert(root.right, key);
    return root;
}
function findpairUtil(root, sum, set)
{
    if (root == null)
        return false;
    if (findpairUtil(root.left, sum, set))
        return true;
    if (set.has(sum - root.data)) {
        document.write("Pair is found ("
                          + (sum - root.data) + ", "
                          + root.data + ")<br>");
        return true;
    }
    else
        set.add(root.data);
    return findpairUtil(root.right, sum, set);
}
function findPair(root, sum)
{
    var set = new Set();
    if (!findpairUtil(root, sum, set))
        document.write("Pairs do not exit"
                      + "\n");
}
// Driver code
var root = null;
root = insert(root, 15);
root = insert(root, 10);
root = insert(root, 20);
root = insert(root, 8);
root = insert(root, 12);
root = insert(root, 16);
root = insert(root, 25);
root = insert(root, 10);
var sum = 33;
findPair(root, sum);

</script>
```

**输出:**

```
Pair is found (8, 25)
```

***时间复杂度:*** O(n)。