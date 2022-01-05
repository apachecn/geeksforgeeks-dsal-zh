# 打印距根 k 距离的节点|迭代

> 原文:[https://www . geesforgeks . org/print-nodes-k-distance-root-iterative/](https://www.geeksforgeeks.org/print-nodes-k-distance-root-iterative/)

给定一个树根和一个整数 k。打印离树根 k 距离的所有节点。
**例:**

```
Input :
                20
              /   \
            10    30
           / \    / \
          5  15  25  40
             /
            12

and k = 3
Root is at level 1.

Output :
5 15 25 40
```

这个问题的递归方法在这里讨论
下面是迭代方法。
解决方法类似于[获取二叉树](https://www.geeksforgeeks.org/get-level-node-binary-tree-iterative-approach/)
中节点的级别

## C++

```
// CPP program to print all nodes of level k
// iterative approach
/* binary tree
root is at level 1

                20
              /   \
            10    30
           / \    / \
          5  15  25  40
             /
            12  */
#include <bits/stdc++.h>
using namespace std;

// Node of binary tree
struct Node {
    int data;
    Node* left, * right;
};

// Function to add a new node
Node* newNode(int data)
{
    Node* newnode = new Node();
    newnode->data = data;
    newnode->left = newnode->right = NULL;
}

// Function to print nodes of given level
bool printKDistant(Node* root, int klevel)
{
    queue<Node*> q;
    int level = 1;
    bool flag = false;
    q.push(root);

    // extra NULL is pushed to keep track
    // of all the nodes to be pushed before
    // level is incremented by 1
    q.push(NULL);
    while (!q.empty()) {
        Node* temp = q.front();

        // print when level is equal to k
        if (level == klevel && temp != NULL) {
            flag = true;
            cout << temp->data << " ";
        }
        q.pop();
        if (temp == NULL) {
            if (q.front())
                q.push(NULL);
            level += 1;

            // break the loop if level exceeds
            // the given level number
            if (level > klevel)
                break;
        } else {
            if (temp->left)
                q.push(temp->left);

            if (temp->right)
                q.push(temp->right);
        }
    }
    cout << endl;

    return flag;
}

// Driver code
int main()
{
    // create a binary tree
    Node* root = newNode(20);
    root->left = newNode(10);
    root->right = newNode(30);
    root->left->left = newNode(5);
    root->left->right = newNode(15);
    root->left->right->left = newNode(12);
    root->right->left = newNode(25);
    root->right->right = newNode(40);

    cout << "data at level 1 : ";
    int ret = printKDistant(root, 1);
    if (ret == false)
        cout << "Number exceeds total number of levels\n";

    cout << "data at level 2 : ";
    ret = printKDistant(root, 2);
    if (ret == false)
        cout << "Number exceeds total number of levels\n";

    cout << "data at level 3 : ";
    ret = printKDistant(root, 3);
    if (ret == false)
        cout << "Number exceeds total number of levels\n";

    cout << "data at level 6 : ";
    ret = printKDistant(root, 6);
    if (ret == false)
        cout << "Number exceeds total number of levels\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all nodes of level k
// iterative approach
/* binary tree
root is at level 1

                20
            / \
            10 30
        / \ / \
        5 15 25 40
            /
            12 */

import java.util.*;
class GFG
{

// Node of binary tree
static class Node
{
    int data;
    Node left, right;
}

// Function to add a new node
static Node newNode(int data)
{
    Node newnode = new Node();
    newnode.data = data;
    newnode.left = newnode.right = null;
    return newnode;
}

// Function to print nodes of given level
static boolean printKDistant(Node root, int klevel)
{
    Queue<Node> q = new LinkedList<>();
    int level = 1;
    boolean flag = false;
    q.add(root);

    // extra null is added to keep track
    // of all the nodes to be added before
    // level is incremented by 1
    q.add(null);
    while (q.size() > 0)
    {
        Node temp = q.peek();

        // print when level is equal to k
        if (level == klevel && temp != null)
        {
            flag = true;
            System.out.print( temp.data + " ");
        }
        q.remove();
        if (temp == null)
        {
            if (q.peek() != null)
                q.add(null);
            level += 1;

            // break the loop if level exceeds
            // the given level number
            if (level > klevel)
                break;
        }
        else
        {
            if (temp.left != null)
                q.add(temp.left);

            if (temp.right != null)
                q.add(temp.right);
        }
    }
    System.out.println();
    return flag;
}

// Driver code
public static void main(String srga[])
{
    // create a binary tree
    Node root = newNode(20);
    root.left = newNode(10);
    root.right = newNode(30);
    root.left.left = newNode(5);
    root.left.right = newNode(15);
    root.left.right.left = newNode(12);
    root.right.left = newNode(25);
    root.right.right = newNode(40);

    System.out.print( "data at level 1 : ");
    boolean ret = printKDistant(root, 1);
    if (ret == false)
        System.out.print( "Number exceeds total " +
                            "number of levels\n");

    System.out.print("data at level 2 : ");
    ret = printKDistant(root, 2);
    if (ret == false)
        System.out.print("Number exceeds total " +
                            "number of levels\n");

    System.out.print( "data at level 3 : ");
    ret = printKDistant(root, 3);
    if (ret == false)
        System.out.print("Number exceeds total " +
                        "number of levels\n");

    System.out.print( "data at level 6 : ");
    ret = printKDistant(root, 6);
    if (ret == false)
        System.out.print( "Number exceeds total" +
                            "number of levels\n");

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print all nodes of level k
# iterative approach
""" binary tree
root is at level 1

                20
            / \
            10 30
        / \ / \
        5 15 25 40
            /
            12 """

# Node of binary tree
# Function to add a new node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Function to prnodes of given level
def printKDistant( root, klevel):

    q = []
    level = 1
    flag = False
    q.append(root)

    # extra None is appended to keep track
    # of all the nodes to be appended
    # before level is incremented by 1
    q.append(None)
    while (len(q)):
        temp = q[0]

        # prwhen level is equal to k
        if (level == klevel and temp != None):
            flag = True
            print(temp.data, end = " ")

        q.pop(0)
        if (temp == None) :
            if (len(q)):
                q.append(None)
            level += 1

            # break the loop if level exceeds
            # the given level number
            if (level > klevel) :
                break
        else:
            if (temp.left) :
                q.append(temp.left)

            if (temp.right) :
                q.append(temp.right)
    print()

    return flag

# Driver Code
if __name__ == '__main__':
    root = newNode(20)
    root.left = newNode(10)
    root.right = newNode(30)
    root.left.left = newNode(5)
    root.left.right = newNode(15)
    root.left.right.left = newNode(12)
    root.right.left = newNode(25)
    root.right.right = newNode(40)

    print("data at level 1 : ", end = "")
    ret = printKDistant(root, 1)
    if (ret == False):
        print("Number exceeds total",
                  "number of levels")

    print("data at level 2 : ", end = "")
    ret = printKDistant(root, 2)
    if (ret == False) :
        print("Number exceeds total",
                  "number of levels")

    print("data at level 3 : ", end = "")
    ret = printKDistant(root, 3)
    if (ret == False) :
        print("Number exceeds total",
                  "number of levels")

    print("data at level 6 : ", end = "")
    ret = printKDistant(root, 6)
    if (ret == False):
        print("Number exceeds total number of levels")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to print all nodes of level k
// iterative approach
/* binary tree
root is at level 1

                20
            / \
            10 30
        / \ / \
        5 15 25 40
            /
            12 */

using System;
using System.Collections.Generic;

class GFG
{

// Node of binary tree
public class Node
{
    public int data;
    public Node left, right;
}

// Function to add a new node
static Node newNode(int data)
{
    Node newnode = new Node();
    newnode.data = data;
    newnode.left = newnode.right = null;
    return newnode;
}

// Function to print nodes of given level
static Boolean printKDistant(Node root, int klevel)
{
    Queue<Node> q = new Queue<Node>();
    int level = 1;
    Boolean flag = false;
    q.Enqueue(root);

    // extra null is added to keep track
    // of all the nodes to be added before
    // level is incremented by 1
    q.Enqueue(null);
    while (q.Count > 0)
    {
        Node temp = q.Peek();

        // print when level is equal to k
        if (level == klevel && temp != null)
        {
            flag = true;
            Console.Write( temp.data + " ");
        }
        q.Dequeue();
        if (temp == null)
        {
            if (q.Count > 0&&q.Peek() != null)
                q.Enqueue(null);
            level += 1;

            // break the loop if level exceeds
            // the given level number
            if (level > klevel)
                break;
        }
        else
        {
            if (temp.left != null)
                q.Enqueue(temp.left);

            if (temp.right != null)
                q.Enqueue(temp.right);
        }
    }
    Console.Write("\n");
    return flag;
}

// Driver code
public static void Main(String []srga)
{
    // create a binary tree
    Node root = newNode(20);
    root.left = newNode(10);
    root.right = newNode(30);
    root.left.left = newNode(5);
    root.left.right = newNode(15);
    root.left.right.left = newNode(12);
    root.right.left = newNode(25);
    root.right.right = newNode(40);

    Console.Write( "data at level 1 : ");
    Boolean ret = printKDistant(root, 1);
    if (ret == false)
        Console.Write( "Number exceeds total " +
                            "number of levels\n");

    Console.Write("data at level 2 : ");
    ret = printKDistant(root, 2);
    if (ret == false)
        Console.Write("Number exceeds total " +
                            "number of levels\n");

    Console.Write( "data at level 3 : ");
    ret = printKDistant(root, 3);
    if (ret == false)
        Console.Write("Number exceeds total " +
                        "number of levels\n");

    Console.Write( "data at level 6 : ");
    ret = printKDistant(root, 6);
    if (ret == false)
        Console.Write( "Number exceeds total" +
                            "number of levels\n");

}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program to print all nodes of level k
    // iterative approach
    /* binary tree
    root is at level 1

                    20
                / \
                10 30
            / \ / \
            5 15 25 40
                /
                12 */

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to add a new node
    function newNode(data)
    {
        let newnode = new Node(data);
        return newnode;
    }

    // Function to print nodes of given level
    function printKDistant(root, klevel)
    {
        let q = [];
        let level = 1;
        let flag = false;
        q.push(root);

        // extra null is added to keep track
        // of all the nodes to be added before
        // level is incremented by 1
        q.push(null);
        while (q.length > 0)
        {
            let temp = q[0];

            // print when level is equal to k
            if (level == klevel && temp != null)
            {
                flag = true;
                document.write( temp.data + " ");
            }
            q.shift();
            if (temp == null)
            {
                if (q[0] != null)
                    q.push(null);
                level += 1;

                // break the loop if level exceeds
                // the given level number
                if (level > klevel)
                    break;
            }
            else
            {
                if (temp.left != null)
                    q.push(temp.left);

                if (temp.right != null)
                    q.push(temp.right);
            }
        }
        document.write("</br>");
        return flag;
    }

    // create a binary tree
    let root = newNode(20);
    root.left = newNode(10);
    root.right = newNode(30);
    root.left.left = newNode(5);
    root.left.right = newNode(15);
    root.left.right.left = newNode(12);
    root.right.left = newNode(25);
    root.right.right = newNode(40);

    document.write( "data at level 1 : ");
    let ret = printKDistant(root, 1);
    if (ret == false)
        document.write( "Number exceeds total " +
                            "number of levels" + "</br>");

    document.write("data at level 2 : ");
    ret = printKDistant(root, 2);
    if (ret == false)
        document.write("Number exceeds total " +
                            "number of levels" + "</br>");

    document.write( "data at level 3 : ");
    ret = printKDistant(root, 3);
    if (ret == false)
        document.write("Number exceeds total " +
                        "number of levels" + "</br>");

    document.write( "data at level 6 : ");
    ret = printKDistant(root, 6);
    if (ret == false)
        document.write( "Number exceeds total" +
                            "number of levels" + "</br>");

// This code is contributed by suresh07.           
</script>
```

**输出:**

```
data at level 1 : 20 
data at level 2 : 10 30 
data at level 3 : 5 15 25 40 
data at level 6 : 
Number exceeds total number of levels
```

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由[T2【曼德普·辛格 T4【投稿】撰写。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](https://github.com/msdeep14)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。