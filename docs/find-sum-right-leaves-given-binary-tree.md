# 求给定二叉树中所有右叶的和

> 原文:[https://www . geesforgeks . org/find-sum-right-leads-given-二叉树/](https://www.geeksforgeeks.org/find-sum-right-leaves-given-binary-tree/)

给定一棵二叉树，求其中所有正确叶子的和。
类似文章:[求给定二叉树中所有左叶的和](https://www.geeksforgeeks.org/find-sum-left-leaves-given-binary-tree/)
**例:**

```
Input : 
         1
        /  \
       2    3
     /  \     \
    4    5     8 
     \        /  \
      2       6   7

Output :
sum = 2 + 5 + 7 = 14
```

方法 1:递归方法

这个想法是从根开始遍历树，检查节点是否是叶节点。如果节点是右叶，则将右叶的数据添加到 sum 变量中。
以下是相同的实现。

## C++

```
// CPP program to find total sum
// of right leaf nodes
#include <bits/stdc++.h>
using namespace std;

// struct node of binary tree
struct Node{
    int data;
    Node *left, *right;
};

// return new node
Node *addNode(int data){
    Node *temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
}

// utility function to calculate sum
// of right leaf nodes
void rightLeafSum(Node *root, int *sum){
    if(!root)
        return;

    // check if the right child of root
    // is leaf node
    if(root->right)
        if(!root->right->left  && 
                     !root->right->right)
            *sum += root->right->data;

    rightLeafSum(root->left, sum);
    rightLeafSum(root->right, sum);
}

// driver program
int main(){

        //construct binary tree
    Node *root = addNode(1);
    root->left = addNode(2);
    root->left->left = addNode(4);
    root->left->right = addNode(5);
    root->left->left->right = addNode(2);
    root->right = addNode(3);
    root->right->right = addNode(8);
    root->right->right->left = addNode(6);
    root->right->right->right = addNode(7);

    // variable to store sum of right
       // leaves
    int sum = 0;
    rightLeafSum(root, &sum);
    cout << sum << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total
// sum of right leaf nodes
class GFG
{

    // sum
    static int sum = 0;

// node of binary tree
static class Node
{
    int data;
    Node left, right;
};

// return new node
static Node addNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// utility function to calculate
// sum of right leaf nodes
static void rightLeafSum(Node root)
{
    if(root == null)
        return;

    // check if the right child
    // of root is leaf node
    if(root.right != null)
        if(root.right.left == null &&
           root.right.right == null)
            sum += root.right.data;

    rightLeafSum(root.left);
    rightLeafSum(root.right);
}

// Driver Code
public static void main(String args[])
{

    //construct binary tree
    Node root = addNode(1);
    root.left = addNode(2);
    root.left.left = addNode(4);
    root.left.right = addNode(5);
    root.left.left.right = addNode(2);
    root.right = addNode(3);
    root.right.right = addNode(8);
    root.right.right.left = addNode(6);
    root.right.right.right = addNode(7);

    // variable to store sum
    // of right leaves
    sum = 0;
    rightLeafSum(root);
    System.out.println( sum );
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find total Sum
# of right leaf nodes

# return new node
class addNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# utility function to calculate Sum
# of right leaf nodes
def rightLeafSum(root, Sum):
    if(not root):
        return

    # check if the right child of root
    # is leaf node
    if(root.right):
        if(not root.right.left and
           not root.right.right):
            Sum[0] += root.right.data

    rightLeafSum(root.left, Sum)
    rightLeafSum(root.right, Sum)

# Driver Code
if __name__ == '__main__':

    # construct binary tree
    root = addNode(1)
    root.left = addNode(2)
    root.left.left = addNode(4)
    root.left.right = addNode(5)
    root.left.left.right = addNode(2)
    root.right = addNode(3)
    root.right.right = addNode(8)
    root.right.right.left = addNode(6)
    root.right.right.right = addNode(7)

    # variable to store Sum of right
    # leaves
    Sum = [0]
    rightLeafSum(root, Sum)
    print(Sum[0])

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to find total 
// sum of right leaf nodes 
public class GFG
{

    // sum
    public static int sum = 0;

// node of binary tree 
public class Node
{
    public int data;
    public Node left, right;
}

// return new node 
public static Node addNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// utility function to calculate 
// sum of right leaf nodes 
public static void rightLeafSum(Node root)
{
    if (root == null)
    {
        return;
    }

    // check if the right child
    // of root is leaf node 
    if (root.right != null)
    {
        if (root.right.left == null && root.right.right == null)
        {
            sum += root.right.data;
        }
    }

    rightLeafSum(root.left);
    rightLeafSum(root.right);
}

// Driver Code
public static void Main(string[] args)
{

    //construct binary tree 
    Node root = addNode(1);
    root.left = addNode(2);
    root.left.left = addNode(4);
    root.left.right = addNode(5);
    root.left.left.right = addNode(2);
    root.right = addNode(3);
    root.right.right = addNode(8);
    root.right.right.left = addNode(6);
    root.right.right.right = addNode(7);

    // variable to store sum 
    // of right leaves 
    sum = 0;
    rightLeafSum(root);
    Console.WriteLine(sum);
}
}

  //  This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to find total
    // sum of right leaf nodes

    // sum
    let sum = 0;

    // node of binary tree
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // return new node
    function addNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // utility function to calculate
    // sum of right leaf nodes
    function rightLeafSum(root)
    {
        if(root == null)
            return;

        // check if the right child
        // of root is leaf node
        if(root.right != null)
            if(root.right.left == null &&
               root.right.right == null)
                sum += root.right.data;

        rightLeafSum(root.left);
        rightLeafSum(root.right);
    }

    //construct binary tree
    let root = addNode(1);
    root.left = addNode(2);
    root.left.left = addNode(4);
    root.left.right = addNode(5);
    root.left.left.right = addNode(2);
    root.right = addNode(3);
    root.right.right = addNode(8);
    root.right.right.left = addNode(6);
    root.right.right.right = addNode(7);

    // variable to store sum
    // of right leaves
    sum = 0;
    rightLeafSum(root);
    document.write(sum );

    // This code is contributed by divyesh072019.
</script>
```

**Output**

```
14
```