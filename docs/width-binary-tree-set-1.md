# 二叉树的垂直宽度|集合 1

> 原文:[https://www.geeksforgeeks.org/width-binary-tree-set-1/](https://www.geeksforgeeks.org/width-binary-tree-set-1/)

给定一棵二叉树，求二叉树的垂直宽度。二叉树的宽度是垂直路径的数量。

![](img/69d4b1471ee623d6782354a73dff8c8f.png)

在此图像中，树包含 6 条垂直线，这是树所需的宽度。

**示例:**

```
Input : 
             7
           /  \
          6    5
         / \  / \
        4   3 2  1 
Output :
5

Input :
           1
         /    \
        2       3
       / \     / \
      4   5   6   7
               \   \ 
                8   9 
Output :
6

```

**方法:**进行有序遍历，然后取一个临时变量，如果我们向左走，则温度值降低，如果向右走，则温度值升高。在这里声明一个条件，如果最小值大于温度，那么最小值=温度，如果最大值小于温度，那么最大值=温度。最后，打印最小+最大，即树的垂直宽度。

## C++

```
// CPP program to print vertical width
// of a tree
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// get vertical width
void lengthUtil(Node* root, int &maximum,
                int &minimum, int curr=0)
{
    if (root == NULL)
        return;

    // traverse left
    lengthUtil(root->left, maximum,
               minimum, curr - 1);

    // if curr is decrease then get
    // value in minimum
    if (minimum > curr)
        minimum = curr;

    // if curr is increase then get
    // value in maximum
    if (maximum < curr)
        maximum = curr;

    // traverse right
    lengthUtil(root->right, maximum,
               minimum,  curr + 1);

}

int getLength(Node* root)
{
    int maximum = 0, minimum = 0;
    lengthUtil(root, maximum, minimum, 0);

    // 1 is added to include root in the width
    return (abs(minimum) + maximum) + 1;
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* curr = new Node;
    curr->data = data;
    curr->left = curr->right = NULL;
    return curr;
}

// Driver program to test above functions
int main()
{

    Node* root = newNode(7);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->left = newNode(2);
    root->right->right = newNode(1);

    cout << getLength(root) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print vertical width
// of a tree
import java.util.*;

class GFG
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};
static int maximum = 0, minimum = 0;

// get vertical width
static void lengthUtil(Node root, int curr)
{
    if (root == null)
        return;

    // traverse left
    lengthUtil(root.left, curr - 1);

    // if curr is decrease then get
    // value in minimum
    if (minimum > curr)
        minimum = curr;

    // if curr is increase then get
    // value in maximum
    if (maximum < curr)
        maximum = curr;

    // traverse right
    lengthUtil(root.right, curr + 1);
}

static int getLength(Node root)
{
    maximum = 0; minimum = 0;
    lengthUtil(root, 0);

    // 1 is added to include root in the width
    return (Math.abs(minimum) + maximum) + 1;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node curr = new Node();
    curr.data = data;
    curr.left = curr.right = null;
    return curr;
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

    System.out.println(getLength(root));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to prvertical width 
# of a tree 

# class to create a new tree node 
class newNode:
    def __init__(self, data): 
        self.data = data 
        self.left = self.right = None

# get vertical width 
def lengthUtil(root, maximum, minimum, curr = 0):
    if (root == None):
        return

    # traverse left 
    lengthUtil(root.left, maximum, 
                minimum, curr - 1) 

    # if curr is decrease then get 
    # value in minimum 
    if (minimum[0] > curr):
        minimum[0] = curr 

    # if curr is increase then get 
    # value in maximum 
    if (maximum[0] < curr):
        maximum[0] = curr 

    # traverse right 
    lengthUtil(root.right, maximum, 
                 minimum, curr + 1)

def getLength(root):
    maximum = [0]
    minimum = [0] 
    lengthUtil(root, maximum, minimum, 0) 

    # 1 is added to include root in the width 
    return (abs(minimum[0]) + maximum[0]) + 1

# Driver Code
if __name__ == '__main__':

    root = newNode(7) 
    root.left = newNode(6) 
    root.right = newNode(5) 
    root.left.left = newNode(4) 
    root.left.right = newNode(3) 
    root.right.left = newNode(2) 
    root.right.right = newNode(1) 

    print(getLength(root))

# This code is contributed by PranchalK
```

## C#

```
// C# program to print vertical width
// of a tree
using System;

class GFG
{

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
};
static int maximum = 0, minimum = 0;

// get vertical width
static void lengthUtil(Node root,
                        int curr)
{
    if (root == null)
        return;

    // traverse left
    lengthUtil(root.left, curr - 1);

    // if curr is decrease then get
    // value in minimum
    if (minimum > curr)
        minimum = curr;

    // if curr is increase then get
    // value in maximum
    if (maximum < curr)
        maximum = curr;

    // traverse right
    lengthUtil(root.right, curr + 1);
}

static int getLength(Node root)
{
    maximum = 0; minimum = 0;
    lengthUtil(root, 0);

    // 1 is added to include root in the width
    return (Math.Abs(minimum) + maximum) + 1;
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node curr = new Node();
    curr.data = data;
    curr.left = curr.right = null;
    return curr;
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

    Console.WriteLine(getLength(root));
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
5

```

**时间复杂度:**O(n)
T3】辅助空间: O(h)其中 h 是二叉树的高度。递归调用需要这么多空间。