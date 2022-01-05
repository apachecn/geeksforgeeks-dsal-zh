# 按排序顺序打印二叉树级别|集合 2(使用集合)

> 原文:[https://www . geesforgeks . org/print-binary-tree-levels-sorted-order-2/](https://www.geeksforgeeks.org/print-binary-tree-levels-sorted-order-2/)

给定一棵树，按排序顺序打印级别顺序遍历。
**例:**

```
Input :     7
          /    \
        6       5
       / \     / \
      4  3    2   1
Output : 
7
5 6
1 2 3 4 

Input :     7
          /    \
        16       1
       / \      
      4   13    
Output :
7 
1 16
4 13
```

我们已经在下面的帖子中讨论了基于优先级队列的解决方案。
[按排序顺序打印二叉树级别|集合 1(使用优先级队列)](https://www.geeksforgeeks.org/print-binary-tree-levels-sorted-order/)
本文讨论了基于[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)(使用平衡二叉查找树实现)的解决方案。
**进场:**
1。开始树的层次顺序遍历。
2。将所有节点存储在一个集合(或任何其他类似的数据结构)中。
3。打印集合的元素。

## C++

```
// CPP code to print level order
// traversal in sorted order
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int dat = 0)
        : data(dat), left(nullptr),
          right(nullptr)
    {
    }
};

// Function to print sorted
// level order traversal
void sorted_level_order(Node* root)
{
    queue<Node*> q;
    set<int> s;

    q.push(root);
    q.push(nullptr);

    while (q.empty() == false) {
        Node* tmp = q.front();
        q.pop();

        if (tmp == nullptr) {
            if (s.empty() == true)
                break;
            for (set<int>::iterator it =
                 s.begin();it != s.end(); ++it)
                cout << *it << " ";
            q.push(nullptr);
            s.clear();
        }
        else {
            s.insert(tmp->data);

            if (tmp->left != nullptr)
                q.push(tmp->left);
            if (tmp->right != nullptr)
                q.push(tmp->right);
        }
    }
}

// Driver code
int main()
{
    Node* root = new Node(7);
    root->left = new Node(6);
    root->right = new Node(5);
    root->left->left = new Node(4);
    root->left->right = new Node(3);
    root->right->left = new Node(2);
    root->right->right = new Node(1);   
    sorted_level_order(root);   
    return 0;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print level order
// traversal in sorted order
import java.util.*;
import java.util.HashSet;

class GFG
{
static class Node
{
    int data;
    Node left, right;
};
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print sorted
// level order traversal
static void sorted_level_order(Node root)
{
    Queue<Node> q = new LinkedList<>();
    Set<Integer> s = new HashSet<Integer>();
    q.add(root);
    q.add(null);

    while (!q.isEmpty())
    {
        Node tmp = q.peek();
            q.remove();

        if (tmp == null)
        {
            if (s.isEmpty())
                break;
            Iterator value = s.iterator();
            while (value.hasNext())
            {
                System.out.print(value.next() + " ");
            }
            q.add(null);
            s.clear();
        }
        else
        {
            s.add(tmp.data);

            if (tmp.left != null)
                q.add(tmp.left);
            if (tmp.right != null)
                q.add(tmp.right);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);
    sorted_level_order(root);
}
}

// This code is contributed by SHUBHAMSINGH10
```

## 蟒蛇 3

```
# Python3 program to print level order
# traversal in sorted order

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                    
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to print sorted
# level order traversal
def sorted_level_order( root):

    q = []
    s = set()

    q.append(root)
    q.append(None)

    while (len(q)):
        tmp = q[0]
        q.pop(0)

        if (tmp == None):
            if (not len(s)):
                break
            for i in s:
                print(i, end = " ")
            q.append(None)
            s = set()

        else :
            s.add(tmp.data)

            if (tmp.left != None):
                q.append(tmp.left)
            if (tmp.right != None):
                q.append(tmp.right)

# Driver Code
if __name__ == '__main__':

    """
    Let us create Binary Tree shown
    in above example """
    root = newNode(7)
    root.left = newNode(6)
    root.right = newNode(5)
    root.left.left = newNode(4)
    root.left.right = newNode(3)
    root.right.left = newNode(2)
    root.right.right = newNode(1)
    sorted_level_order(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# code to print level order
// traversal in sorted order
using System;
using System.Collections.Generic;

class GFG
{
public class Node
{
    public int data;
    public Node left, right;
};

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print sorted
// level order traversal
static void sorted_level_order(Node root)
{
    Queue<Node> q = new Queue<Node>();
    SortedSet<int> s = new SortedSet<int>();
    q.Enqueue(root);
    q.Enqueue(null);

    while (q.Count != 0)
    {
        Node tmp = q.Peek();
            q.Dequeue();

        if (tmp == null)
        {
            if (s.Count == 0)
                break;
            foreach (int v in s)
            {
                Console.Write(v + " ");
            }
            q.Enqueue(null);
            s.Clear();
        }
        else
        {
            s.Add(tmp.data);

            if (tmp.left != null)
                q.Enqueue(tmp.left);
            if (tmp.right != null)
                q.Enqueue(tmp.right);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);
    sorted_level_order(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript code to print level order
// traversal in sorted order
var SortedSet = require("collections/sorted-set");

class Node
{
    constructor()
    {
        this.data=0;
        this.left=this.right=null;
    }
}

function newNode(data)
{
    let node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print sorted
// level order traversal
function sorted_level_order(root)
{
    let q = [];
    let s = new SortedSet();
    q.push(root);
    q.push(null);

    while (q.length!=0)
    {
        let tmp = q.shift();

        if (tmp == null)
        {
            if (s.size==0)
                break;
            for(let i of s.values())
            {
                document.write(i+" ");
            }
            q.push(null);
            s.clear();
        }
        else
        {
            s.add(tmp.data);

            if (tmp.left != null)
                q.push(tmp.left);
            if (tmp.right != null)
                q.push(tmp.right);
        }
    }
}

// Driver Code
let root = newNode(7);
root.left = newNode(6);
root.right = newNode(5);
root.left.left = newNode(4);
root.left.right = newNode(3);
root.right.left = newNode(2);
root.right.right = newNode(1);
sorted_level_order(root);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
7 5 6 1 2 3 4 
```