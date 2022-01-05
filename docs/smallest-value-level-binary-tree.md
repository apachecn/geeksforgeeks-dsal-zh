# 二叉树各级中的最小值

> 原文:[https://www . geesforgeks . org/最小值级二叉树/](https://www.geeksforgeeks.org/smallest-value-level-binary-tree/)

给定一个包含 n 个节点的二叉树，任务是打印二叉树每一级中的最小元素。
**例:**

```
Input : 
            7
         /    \
        6       5
       / \     / \
      4  3     2  1  

Output : 
Every level minimum is
level 0 min is = 7
level 1 min is = 5
level 2 min is = 1

Input :  
            7
          /    \
        16       1
       / \      
      4   13    

Output :
Every level minimum is
level 0 min is = 7
level 1 min is = 1
level 2 min is = 4
```

**方法 1:使用有序遍历**
**方法:-** 其思想是以有序的方式递归遍历树。根被认为是零级的。首先，找到树的高度并将其存储到 res. res 数组中存储二叉树每一级中的每个最小元素。
下面是在二叉树的每一级寻找最小值的实现。

## C++

```
// CPP program to print smallest element
// in each level of binary tree.
#include <bits/stdc++.h>
#define INT_MAX 10e6
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// return height of tree
int heightoftree(Node* root)
{

    if (root == NULL)
        return 0;

    int left = heightoftree(root->left);
    int right = heightoftree(root->right);

    return ((left > right ? left : right) + 1);
}

// Inorder Traversal
// Search minimum element in each level and
// store it into vector array.
void printPerLevelMinimum(Node* root,
                  vector<int>& res, int level)
{

    if (root != NULL) {

        printPerLevelMinimum(root->left,
                              res, level + 1);

        if (root->data < res[level])
            res[level] = root->data;

        printPerLevelMinimum(root->right,
                              res, level + 1);
    }
}

void perLevelMinimumUtility(Node* root)
{

    // height of tree for the size of
    // vector array
    int n = heightoftree(root), i;

    // vector for store all minimum of
    // every level
    vector<int> res(n, INT_MAX);

    // save every level minimum using
    // inorder traversal
    printPerLevelMinimum(root, res, 0);

    // print every level minimum
    cout << "Every level minimum is\n";
    for (i = 0; i < n; i++) {
        cout << "level " << i <<" min is = "
                            << res[i] << "\n";
    }
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Driver program to test above functions
int main()
{

    // Let us create binary tree shown
    // in above diagram
    Node* root = newNode(7);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->left = newNode(2);
    root->right->right = newNode(1);

    /*       7
         /  \
        6     5
       / \     / \
      4   3 2   1         */
    perLevelMinimumUtility(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print smallest element
// in each level of binary tree.
import java.util.Arrays;
class GFG
{
static int INT_MAX = (int) 10e6;

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// return height of tree
static int heightoftree(Node root)
{
    if (root == null)
        return 0;

    int left = heightoftree(root.left);
    int right = heightoftree(root.right);

    return ((left > right ? left : right) + 1);
}

// Inorder Traversal
// Search minimum element in each level and
// store it into vector array.
static void printPerLevelMinimum(Node root,
                      int []res, int level)
{
    if (root != null)
    {
        printPerLevelMinimum(root.left,
                             res, level + 1);

        if (root.data < res[level])
            res[level] = root.data;

        printPerLevelMinimum(root.right,
                             res, level + 1);
    }
}

static void perLevelMinimumUtility(Node root)
{

    // height of tree for the size of
    // vector array
    int n = heightoftree(root), i;

    // vector for store all minimum of
    // every level
    int []res = new int[n];
    Arrays.fill(res, INT_MAX);

    // save every level minimum using
    // inorder traversal
    printPerLevelMinimum(root, res, 0);

    // print every level minimum
    System.out.print("Every level minimum is\n");
    for (i = 0; i < n; i++)
    {
        System.out.print("level " + i +
                         " min is = " +
                        res[i] + "\n");
    }
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// Driver Code
public static void main(String[] args)
{

    // Let us create binary tree shown
    // in above diagram
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /*     7
        / \
        6     5
    / \     / \
    4 3 2 1         */
    perLevelMinimumUtility(root);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to print
# smallest element in each
# level of binary tree.
INT_MAX = 1000006

# A Binary Tree Node
class Node:

    def __init__(self,
                 data):

        self.data = data
        self.left = None
        self.right = None   

# return height of tree
def heightoftree(root):

    if (root == None):
        return 0;

    left = heightoftree(root.left);
    right = heightoftree(root.right);

    return ((left if left > right
                  else right) + 1);

# Inorder Traversal
# Search minimum element in
# each level and store it
# into vector array.
def printPerLevelMinimum(root,
                         res, level):

    if (root != None):
        res = printPerLevelMinimum(root.left,
                                   res, level + 1);
        if (root.data < res[level]):
            res[level] = root.data;

        res = printPerLevelMinimum(root.right,
                                   res, level + 1);
    return res

def perLevelMinimumUtility(root):

    # height of tree for the
    # size of vector array
    n = heightoftree(root)
    i = 0

    # vector for store all
    # minimum of every level
    res = [INT_MAX for i in range(n)]

    # save every level minimum
    # using inorder traversal
    res = printPerLevelMinimum(root,
                               res, 0);

    # print every level minimum
    print("Every level minimum is")

    for i in range(n):
        print('level ' + str(i) +
              ' min is = ' + str(res[i]))       

# Utility function to create
# a new tree node
def newNode(data):

    temp = Node(data)
    return temp;

# Driver code
if __name__ == "__main__":

    # Let us create binary
    # tree shown in below
    # diagram
    root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    '''    7
         /  \
        6     5
       / \     / \
      4   3 2   1         '''

    perLevelMinimumUtility(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# program to print smallest element
// in each level of binary tree.
using System;

class GFG
{
static int INT_MAX = (int) 10e6;

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
};

// return height of tree
static int heightoftree(Node root)
{
    if (root == null)
        return 0;

    int left = heightoftree(root.left);
    int right = heightoftree(root.right);

    return ((left > right ? left : right) + 1);
}

// Inorder Traversal
// Search minimum element in each level and
// store it into vector array.
static void printPerLevelMinimum(Node root,
                                 int []res,
                                 int level)
{
    if (root != null)
    {
        printPerLevelMinimum(root.left,
                             res, level + 1);

        if (root.data < res[level])
            res[level] = root.data;

        printPerLevelMinimum(root.right,
                             res, level + 1);
    }
}

static void perLevelMinimumUtility(Node root)
{

    // height of tree for the size of
    // vector array
    int n = heightoftree(root), i;

    // vector for store all minimum of
    // every level
    int []res = new int[n];
    for (i = 0; i < n; i++)
        res[i] = INT_MAX;

    // save every level minimum using
    // inorder traversal
    printPerLevelMinimum(root, res, 0);

    // print every level minimum
    Console.Write("Every level minimum is\n");
    for (i = 0; i < n; i++)
    {
        Console.Write("level " + i +
                      " min is = " +
                     res[i] + "\n");
    }
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// Driver Code
public static void Main(String[] args)
{

    // Let us create binary tree shown
    // in above diagram
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /*     7
        / \
        6     5
    / \     / \
    4 3 2 1         */
    perLevelMinimumUtility(root);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to print smallest element
    // in each level of binary tree.

    let INT_MAX = 10e6;

    // A Binary Tree Node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // return height of tree
    function heightoftree(root)
    {
        if (root == null)
            return 0;

        let left = heightoftree(root.left);
        let right = heightoftree(root.right);

        return ((left > right ? left : right) + 1);
    }

    // Inorder Traversal
    // Search minimum element in each level and
    // store it into vector array.
    function printPerLevelMinimum(root, res, level)
    {
        if (root != null)
        {
            printPerLevelMinimum(root.left, res, level + 1);

            if (root.data < res[level])
                res[level] = root.data;

            printPerLevelMinimum(root.right, res, level + 1);
        }
    }

    function perLevelMinimumUtility(root)
    {

        // height of tree for the size of
        // vector array
        let n = heightoftree(root), i;

        // vector for store all minimum of
        // every level
        let res = new Array(n);
        res.fill(INT_MAX);

        // save every level minimum using
        // inorder traversal
        printPerLevelMinimum(root, res, 0);

        // print every level minimum
        document.write("Every level minimum is" + "</br>");
        for (i = 0; i < n; i++)
        {
            document.write("level " + i +
                             " min is = " +
                            res[i] + "</br>");
        }
    }

    // Utility function to create a new tree node
    function newNode(data)
    {
        let temp = new Node(data);
        temp.data = data;
        temp.left = temp.right = null;

        return temp;
    }

    // Let us create binary tree shown
    // in above diagram
    let root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /*     7
        / \
        6     5
    / \     / \
    4 3 2 1         */
    perLevelMinimumUtility(root);

</script>
```

**输出:**

```
Every level minimum is
level 0 min is = 7
level 1 min is = 5
level 2 min is = 1
```

**方法 2:使用层级顺序遍历**
**方法:-** 想法是使用队列执行二叉树的迭代层级顺序遍历。遍历 keep min 变量时，该变量存储正在处理的树的当前级别的最小元素。当液位完全通过时，打印该最小值。

## C++

```
// CPP program to print minimum element
// in each level of binary tree.
#include <iostream>
#include <queue>
#include <vector>
#define INT_MAX 10e6
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// return height of tree
int heightoftree(Node* root)
{

    if (root == NULL)
        return 0;

    int left = heightoftree(root->left);
    int right = heightoftree(root->right);

    return ((left > right ? left : right) + 1);
}

// Iterative method to find every level
// minimum element of Binary Tree
void printPerLevelMinimum(Node* root)
{

    // Base Case
    if (root == NULL)
        return ;

    // Create an empty queue for
    // level order traversal
    queue<Node*> q;

    // push the root for Change the level
    q.push(root);

    // for go level by level
    q.push(NULL);

    int min = INT_MAX;
    // for check the level
    int level = 0;

    while (q.empty() == false) {

        // Get top of queue
        Node* node = q.front();
        q.pop();

        // if node == NULL (Means this is
        // boundary between two levels)
        if (node == NULL) {

            cout << "level " << level <<
             " min is = " << min << "\n";

            // here queue is empty represent
            // no element in the actual
            // queue
            if (q.empty())
                break;

            q.push(NULL);

            // increment level
            level++;

            // Reset min for next level
            // minimum value
            min = INT_MAX;

            continue;
        }

        // get Minimum in every level
        if (min > node->data)
            min = node->data;

        /* Enqueue left child */
        if (node->left != NULL) {
            q.push(node->left);
        }

        /*Enqueue right child */
        if (node->right != NULL) {
            q.push(node->right);
        }
    }
}

// Utility function to create a
// new tree node
Node* newNode(int data)
{

    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Driver program to test above functions
int main()
{

    // Let us create binary tree shown
    // in above diagram
    Node* root = newNode(7);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->left = newNode(2);
    root->right->right = newNode(1);

    /*      7
        /  \
       6    5
      / \  / \
     4  3 2   1         */

    cout << "Every Level minimum is"
        << "\n";

    printPerLevelMinimum(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to print minimum element
// in each level of binary tree.
import java.util.*;

class GFG
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// return height of tree
static int heightoftree(Node root)
{

    if (root == null)
        return 0;

    int left = heightoftree(root.left);
    int right = heightoftree(root.right);

    return ((left > right ? left : right) + 1);
}

// Iterative method to find every level
// minimum element of Binary Tree
static void printPerLevelMinimum(Node root)
{

    // Base Case
    if (root == null)
        return ;

    // Create an empty queue for
    // level order traversal
    Queue<Node> q = new LinkedList<Node>();

    // push the root for Change the level
    q.add(root);

    // for go level by level
    q.add(null);

    int min = Integer.MAX_VALUE;
    // for check the level
    int level = 0;

    while (q.isEmpty() == false)
    {

        // Get top of queue
        Node node = q.peek();
        q.remove();

        // if node == null (Means this is
        // boundary between two levels)
        if (node == null)
        {

            System.out.print("level " + level +
            " min is = " + min+ "\n");

            // here queue is empty represent
            // no element in the actual
            // queue
            if (q.isEmpty())
                break;

            q.add(null);

            // increment level
            level++;

            // Reset min for next level
            // minimum value
            min = Integer.MAX_VALUE;

            continue;
        }

        // get Minimum in every level
        if (min > node.data)
            min = node.data;

        /* Enqueue left child */
        if (node.left != null)
        {
            q.add(node.left);
        }

        /*Enqueue right child */
        if (node.right != null)
        {
            q.add(node.right);
        }
    }
}

// Utility function to create a
// new tree node
static Node newNode(int data)
{

    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// Driver code
public static void main(String[] args)
{

    // Let us create binary tree shown
    // in above diagram
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /*     7
        / \
    6 5
    / \ / \
    4 3 2 1         */

    System.out.print("Every Level minimum is"
    + "\n");

    printPerLevelMinimum(root);

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to prminimum element
# in each level of binary tree.

# Importing Queue
from queue import Queue

# Utility class to create a
# new tree node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# return height of tree p
def heightoftree(root):

    if (root == None):
        return 0

    left = heightoftree(root.left)
    right = heightoftree(root.right)
    if left > right:
        return left + 1
    else:
        return right + 1

# Iterative method to find every level
# minimum element of Binary Tree
def printPerLevelMinimum(root):

    # Base Case
    if (root == None):
        return

    # Create an empty queue for
    # level order traversal
    q = Queue()

    # put the root for Change the level
    q.put(root)

    # for go level by level
    q.put(None)

    Min = 9999999999999

    # for check the level
    level = 0

    while (q.empty() == False):

        # Get get of queue
        node = q.queue[0]
        q.get()

        # if node == None (Means this is
        # boundary between two levels)
        if (node == None):

            print("level", level, "min is =", Min)

            # here queue is empty represent
            # no element in the actual
            # queue
            if (q.empty()):
                break

            q.put(None)

            # increment level
            level += 1

            # Reset min for next level
            # minimum value
            Min = 999999999999

            continue

        # get Minimum in every level
        if (Min > node.data):
            Min = node.data

        # Enqueue left child
        if (node.left != None):
            q.put(node.left)

        #Enqueue right child
        if (node.right != None):
            q.put(node.right)

# Driver Code
if __name__ == '__main__':

    # Let us create binary tree shown
    # in above diagram
    root = newNode(7)
    root.left = newNode(6)
    root.right = newNode(5)
    root.left.left = newNode(4)
    root.left.right = newNode(3)
    root.right.left = newNode(2)
    root.right.right = newNode(1)

    #     7
    # / \
    # 6 5
    # / \ / \
    # 4 3 2 1        
    print("Every Level minimum is")

    printPerLevelMinimum(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to print minimum element
// in each level of binary tree.
using System;
using System.Collections.Generic;

class GFG
{

// A Binary Tree Node
class Node
{
    public int data;
    public Node left, right;
};

// return height of tree
static int heightoftree(Node root)
{

    if (root == null)
        return 0;

    int left = heightoftree(root.left);
    int right = heightoftree(root.right);

    return ((left > right ? left : right) + 1);
}

// Iterative method to find every level
// minimum element of Binary Tree
static void printPerLevelMinimum(Node root)
{

    // Base Case
    if (root == null)
        return;

    // Create an empty queue for
    // level order traversal
    Queue<Node> q = new Queue<Node>();

    // push the root for Change the level
    q.Enqueue(root);

    // for go level by level
    q.Enqueue(null);

    int min = int.MaxValue;
    // for check the level
    int level = 0;

    while (q.Count != 0)
    {

        // Get top of queue
        Node node = q.Peek();
        q.Dequeue();

        // if node == null (Means this is
        // boundary between two levels)
        if (node == null)
        {

            Console.Write("level " + level +
                          " min is = " + min + "\n");

            // here queue is empty represent
            // no element in the actual
            // queue
            if (q.Count == 0)
                break;

            q.Enqueue(null);

            // increment level
            level++;

            // Reset min for next level
            // minimum value
            min = int.MaxValue;

            continue;
        }

        // get Minimum in every level
        if (min > node.data)
            min = node.data;

        /* Enqueue left child */
        if (node.left != null)
        {
            q.Enqueue(node.left);
        }

        /*Enqueue right child */
        if (node.right != null)
        {
            q.Enqueue(node.right);
        }
    }
}

// Utility function to create a
// new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// Driver code
public static void Main(String[] args)
{

    // Let us create binary tree shown
    // in above diagram
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /* 7
        / \
    6 5
    / \ / \
    4 3 2 1     */

    Console.Write("Every Level minimum is" + "\n");

    printPerLevelMinimum(root);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to print minimum element
    // in each level of binary tree.

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // return height of tree
    function heightoftree(root)
    {

        if (root == null)
            return 0;

        let left = heightoftree(root.left);
        let right = heightoftree(root.right);

        return ((left > right ? left : right) + 1);
    }

    // Iterative method to find every level
    // minimum element of Binary Tree
    function printPerLevelMinimum(root)
    {

        // Base Case
        if (root == null)
            return ;

        // Create an empty queue for
        // level order traversal
        let q = [];

        // push the root for Change the level
        q.push(root);

        // for go level by level
        q.push(null);

        let min = Number.MAX_VALUE;
        // for check the level
        let level = 0;

        while (q.length > 0)
        {

            // Get top of queue
            let node = q[0];
            q.shift();

            // if node == null (Means this is
            // boundary between two levels)
            if (node == null)
            {

                document.write("level " + level +
                " min is = " + min+ "</br>");

                // here queue is empty represent
                // no element in the actual
                // queue
                if (q.length == 0)
                    break;

                q.push(null);

                // increment level
                level++;

                // Reset min for next level
                // minimum value
                min = Number.MAX_VALUE;

                continue;
            }

            // get Minimum in every level
            if (min > node.data)
                min = node.data;

            /* Enqueue left child */
            if (node.left != null)
            {
                q.push(node.left);
            }

            /*Enqueue right child */
            if (node.right != null)
            {
                q.push(node.right);
            }
        }
    }

    // Utility function to create a
    // new tree node
    function newNode(data)
    {

        let temp = new Node(data);
        return temp;
    }

    // Let us create binary tree shown
    // in above diagram
    let root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    /*     7
        / \
    6 5
    / \ / \
    4 3 2 1         */

    document.write("Every level minimum is"
    + "</br>");

    printPerLevelMinimum(root);

// This code is contributed by decode2207.
</script>
```

**输出:**

```
Every level minimum is
level 0 min is = 7
level 1 min is = 5
level 2 min is = 1
```