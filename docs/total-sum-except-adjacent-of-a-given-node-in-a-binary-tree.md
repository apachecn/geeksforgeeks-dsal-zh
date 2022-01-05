# 二叉树中给定节点除相邻节点外的总和

> 原文:[https://www . geeksforgeeks . org/二叉树中给定节点的除相邻之外的总和/](https://www.geeksforgeeks.org/total-sum-except-adjacent-of-a-given-node-in-a-binary-tree/)

给定一个 BT 和一个关键节点，求 BT 中的总和，除了那些与关键节点相邻的节点。
示例:

![](img/92943d3b348e96c04d22161e4a4f0614.png)

1.使用预先排序遍历树。
2。如果当前节点与关键字相邻，则不要将其添加到最终总和中。
3。如果当前节点是关键字，则不要将其子节点添加到最终总和中。
4。如果密钥不存在，则返回所有节点的总和。

## C++

```
// C++ program to find total sum except a given Node in BT
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node *left, *right;
};

// insertion of Node in Tree
Node* getNode(int n)
{
    struct Node* root = new Node;
    root->data = n;
    root->left = NULL;
    root->right = NULL;
    return root;
}

// sum of all element except those which are adjecent to key Node
void find_sum(Node* root, int key, int& sum, bool incl)
{
    if (root) {
        if (incl) {
            sum += root->data;

            if (root->left && root->left->data == key) {
                sum -= root->data;
            }
            else if (root->right && root->right->data == key) {
                sum -= root->data;
            }
        }

        incl = root->data == key ? false : true;
        find_sum(root->left, key, sum, incl);
        find_sum(root->right, key, sum, incl);
    }
}

// Driver code
int main()
{
    struct Node* root = getNode(15);
    root->left = getNode(13);
    root->left->left = getNode(12);
    root->left->left->left = getNode(11);
    root->left->right = getNode(14);
    root->right = getNode(20);
    root->right->left = getNode(18);
    root->right->right = getNode(24);
    root->right->right->left = getNode(23);
    root->right->right->right = getNode(25);
    int key = 20;
    int sum = 0;
    find_sum(root, key, sum, true);
    printf("%d ", sum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total sum except a given Node in BT
import java.util.*;
class Node
{
    int data;
    Node left, right;

    // insertion of Node in Tree
    Node(int key)
    {
        data = key;
        left = right = null;
    }
}
class GFG
{
    static class cal
   {
      int sum = 0;
    }

    // sum of all element except those which are adjecent to key Node
    public static void find_sum(Node root, int key, cal r, boolean incl)
    {
        if(root != null)
        {
            if(incl == true)
            {
                r.sum += root.data;
                if((root.left != null) && (root.left.data == key))
                        {
               r.sum -= root.data;
            }
                 else
                 if((root.right != null) && (root.right.data == key))
                       {
                   r.sum -= root.data;
            }

            }

            if(root.data == key)
                incl = false;
                else
                incl = true;

        find_sum(root.left, key, r, incl);
        find_sum(root.right, key, r, incl);
        }
    }

// Driver code
public static void main (String[] args)
{
        Node root = new Node(15);
        root.left = new Node(13);
        root.left.left = new Node(12);
        root.left.left.left = new Node(11);
        root.left.right = new Node(14);
        root.right = new Node(20);
        root.right.left = new Node(18);
        root.right.right = new Node(24);
        root.right.right.right = new Node(25);
        root.right.right.left = new Node(23);
        int key = 20;
         cal obj = new cal();
        find_sum(root, key, obj, true);
        System.out.print(obj.sum);
    }

}
```

## 计算机编程语言

```
# Python program to find total
# sum except a given Node in BT
class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.data = data

# Insertion of Node in Tree
def getNode(n):

    root = Node(n)
    return root

# sum of all element except
# those which are adjecent
# to key Node
def find_sum(root, key,
             sum, incl):

    if (root):       
        if(incl):           
            sum += root.data;

            if (root.left and
                root.left.data == key):
                sum -= root.data;

            elif (root.right and
                  root.right.data == key):
                sum -= root.data;

        if root.data == key:
            incl = False
        else:
            incl = True

        sum = find_sum(root.left, key,
                       sum, incl);
        sum = find_sum(root.right, key,
                       sum, incl);       
    return sum       

# Driver code       
if __name__ == "__main__":

    root = getNode(15);
    root.left = getNode(13);
    root.left.left = getNode(12);
    root.left.left.left = getNode(11);
    root.left.right = getNode(14);
    root.right = getNode(20);
    root.right.left = getNode(18);
    root.right.right = getNode(24);
    root.right.right.left = getNode(23);
    root.right.right.right = getNode(25);

    key = 20;
    sum = 0;
    sum = find_sum(root, key,
                   sum, True);
    print(sum)

# This code is contributed by Rutvik_56
```

## C#

```
// C# program to find total sum
// except a given Node in BT
using System;

public class Node
{
    public int data;
    public Node left, right;

    // insertion of Node in Tree
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}
public class GFG
{
public class cal
{
    public int sum = 0;
    }

    // sum of all element except those
    // which are adjecent to key Node
    public static void find_sum(Node root,
                    int key, cal r, bool incl)
    {
        if(root != null)
        {
            if(incl == true)
            {
                r.sum += root.data;
                if((root.left != null) &&
                    (root.left.data == key))
                {
                    r.sum -= root.data;
                }
                else
                if((root.right != null) &&
                    (root.right.data == key))
                {
                    r.sum -= root.data;
                }

            }

            if(root.data == key)
                incl = false;
            else
                incl = true;

        find_sum(root.left, key, r, incl);
        find_sum(root.right, key, r, incl);
        }
    }

// Driver code
public static void Main (String[] args)
{
        Node root = new Node(15);
        root.left = new Node(13);
        root.left.left = new Node(12);
        root.left.left.left = new Node(11);
        root.left.right = new Node(14);
        root.right = new Node(20);
        root.right.left = new Node(18);
        root.right.right = new Node(24);
        root.right.right.right = new Node(25);
        root.right.right.left = new Node(23);
        int key = 20;
        cal obj = new cal();
        find_sum(root, key, obj, true);
        Console.Write(obj.sum);
    }
}

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find total sum
// except a given Node in BT

class Node
{
  // insertion of Node in Tree
  constructor(key)
  {
    this.data = key;
    this.left = null;
    this.right = null;
  }
}

class cal
{
  constructor()
  {
    this.sum = 0;
  }
}

// sum of all element except those
// which are adjecent to key Node
function find_sum(root, key, r, incl)
{
    if(root != null)
    {
        if(incl == true)
        {
            r.sum += root.data;
            if((root.left != null) &&
                (root.left.data == key))
            {
                r.sum -= root.data;
            }
            else
            if((root.right != null) &&
                (root.right.data == key))
            {
                r.sum -= root.data;
            }

        }

        if(root.data == key)
            incl = false;
        else
            incl = true;

    find_sum(root.left, key, r, incl);
    find_sum(root.right, key, r, incl);
    }
}

var root = new Node(15);
root.left = new Node(13);
root.left.left = new Node(12);
root.left.left.left = new Node(11);
root.left.right = new Node(14);
root.right = new Node(20);
root.right.left = new Node(18);
root.right.right = new Node(24);
root.right.right.right = new Node(25);
root.right.right.left = new Node(23);
var key = 20;
var obj = new cal();
find_sum(root, key, obj, true);
document.write(obj.sum);

</script>
```

**Output:** 

```
118
```

**时间复杂度:** O(n)，其中 n 是 BT 中的节点数。