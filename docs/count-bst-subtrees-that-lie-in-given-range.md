# 统计位于给定范围内的 BST 子树

> 原文:[https://www . geesforgeks . org/count-BST-subtrees-躺在给定范围内/](https://www.geeksforgeeks.org/count-bst-subtrees-that-lie-in-given-range/)

给定一个整数值的二叉查找树(BST)和一个范围[低，高]，返回该节点下的所有节点(或以该节点为根的子树)位于给定范围内的节点数。
**例:**

```
Input:
        10
      /    \
    5       50
   /       /  \
 1       40   100
Range: [5, 45]
Output:  1 
There is only 1 node whose subtree is in the given range.
The node is 40 

Input:
        10
      /    \
    5       50
   /       /  \
 1       40   100
Range: [1, 45]
Output:  3 
There are three nodes whose subtree is in the given range.
The nodes are 1, 5 and 40 
```

**我们强烈建议您最小化浏览器，先自己尝试一下。**
想法是以自下而上的方式遍历给定的二叉查找树(BST)。对于每个节点，对其子树重复出现，如果子树在范围内，并且节点也在范围内，则增加计数并返回 true(告诉父节点其状态)。计数作为指针传递，以便在所有函数调用中递增。
以下是上述思路的实现。

## C++

```
// C++ program to count subtrees that lie in a given range
#include <bits/stdc++.h>
using namespace std;

// A BST node
struct node {
    int data;
    struct node *left, *right;
};

// A utility function to check if data of root is
// in range from low to high
bool inRange(node* root, int low, int high)
{
    return root->data >= low && root->data <= high;
}

// A recursive function to get count of nodes whose subtree
// is in range from low to high.  This function returns true
// if nodes in subtree rooted under 'root' are in range.
bool getCountUtil(node* root, int low, int high, int* count)
{
    // Base case
    if (root == NULL)
        return true;

    // Recur for left and right subtrees
    bool l = getCountUtil(root->left, low, high, count);
    bool r = getCountUtil(root->right, low, high, count);

    // If both left and right subtrees are in range and current node
    // is also in range, then increment count and return true
    if (l && r && inRange(root, low, high)) {
        ++*count;
        return true;
    }

    return false;
}

// A wrapper over getCountUtil(). This function initializes count as 0
// and calls getCountUtil()
int getCount(node* root, int low, int high)
{
    int count = 0;
    getCountUtil(root, low, high, &count);
    return count;
}

// Utility function to create new node
node* newNode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return (temp);
}

// Driver program
int main()
{
    // Let us construct the BST shown in the above figure
    node* root = newNode(10);
    root->left = newNode(5);
    root->right = newNode(50);
    root->left->left = newNode(1);
    root->right->left = newNode(40);
    root->right->right = newNode(100);
    /* Let us constructed BST shown in above example
          10
        /    \
      5       50
     /       /  \
    1       40   100   */
    int l = 5;
    int h = 45;
    cout << "Count of subtrees in [" << l << ", "
         << h << "] is " << getCount(root, l, h);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subtrees
// that lie in a given range
class GfG {

    // A BST node
    static class node {
        int data;
        node left, right;
    };

    // int class
    static class INT {
        int a;
    }

    // A utility function to check if data of root is
    // in range from low to high
    static boolean inRange(node root, int low, int high)
    {
        return root.data >= low && root.data <= high;
    }

    // A recursive function to get count
    // of nodes whose subtree is in range
    // from low to high. This function returns
    // true if nodes in subtree rooted under
    // 'root' are in range.
    static boolean getCountUtil(node root, int low,
                                int high, INT count)
    {
        // Base case
        if (root == null)
            return true;

        // Recur for left and right subtrees
        boolean l = getCountUtil(root.left,
                                 low, high, count);
        boolean r = getCountUtil(root.right,
                                 low, high, count);

        // If both left and right subtrees are
        // in range and current node is also in
        // range, then increment count and return true
        if (l && r && inRange(root, low, high)) {
            ++count.a;
            return true;
        }

        return false;
    }

    // A wrapper over getCountUtil().
    // This function initializes count as 0
    // and calls getCountUtil()
    static INT getCount(node root, int low, int high)
    {
        INT count = new INT();
        count.a = 0;
        getCountUtil(root, low, high, count);
        return count;
    }

    // Utility function to create new node
    static node newNode(int data)
    {
        node temp = new node();
        temp.data = data;
        temp.left = temp.right = null;
        return (temp);
    }

    // Driver code
    public static void main(String args[])
    {
        // Let us construct  the BST shown in the above figure
        node root = newNode(10);
        root.left = newNode(5);
        root.right = newNode(50);
        root.left.left = newNode(1);
        root.right.left = newNode(40);
        root.right.right = newNode(100);
        /* Let us construct BST shown in above example
        10
        / \
    5 50
    / / \
    1 40 100 */
        int l = 5;
        int h = 45;
        System.out.println("Count of subtrees in [" + l + ", "
                           + h + "] is " + getCount(root, l, h).a);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to count subtrees that
# lie in a given range

# Utility function to create new node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A utility function to check if data of
# root is in range from low to high
def inRange(root, low, high):
    return root.data >= low and root.data <= high

# A recursive function to get count of nodes
# whose subtree is in range from low to high.
# This function returns true if nodes in subtree
# rooted under 'root' are in range.
def getCountUtil(root, low, high, count):

    # Base case
    if root == None:
        return True

    # Recur for left and right subtrees
    l = getCountUtil(root.left, low, high, count)
    r = getCountUtil(root.right, low, high, count)

    # If both left and right subtrees are in range
    # and current node is also in range, then
    # increment count and return true
    if l and r and inRange(root, low, high):
        count[0] += 1
        return True

    return False

# A wrapper over getCountUtil(). This function
# initializes count as 0 and calls getCountUtil()
def getCount(root, low, high):
    count = [0]
    getCountUtil(root, low, high, count)
    return count

# Driver Code
if __name__ == '__main__':

    # Let us construct the BST shown in
    # the above figure
    root = newNode(10)
    root.left = newNode(5)
    root.right = newNode(50)
    root.left.left = newNode(1)
    root.right.left = newNode(40)
    root.right.right = newNode(100)

    # Let us constructed BST shown in above example
    # 10
    # / \
    # 5     50
    # /     / \
    # 1     40 100
    l = 5
    h = 45
    print("Count of subtrees in [", l, ", ", h, "] is ",
                                   getCount(root, l, h))

# This code is contributed by PranchalK
```

## C#

```
// C# program to count subtrees
// that lie in a given range
using System;

class GfG {

    // A BST node
    public class node {
        public int data;
        public node left, right;
    };

    // int class
    public class INT {
        public int a;
    }

    // A utility function to check if data of root is
    // in range from low to high
    static bool inRange(node root, int low, int high)
    {
        return root.data >= low && root.data <= high;
    }

    // A recursive function to get count
    // of nodes whose subtree is in range
    // from low to high. This function returns
    // true if nodes in subtree rooted under
    // 'root' are in range.
    static bool getCountUtil(node root, int low,
                             int high, INT count)
    {
        // Base case
        if (root == null)
            return true;

        // Recur for left and right subtrees
        bool l = getCountUtil(root.left,
                              low, high, count);
        bool r = getCountUtil(root.right,
                              low, high, count);

        // If both left and right subtrees are
        // in range and current node is also in
        // range, then increment count and return true
        if (l && r && inRange(root, low, high)) {
            ++count.a;
            return true;
        }

        return false;
    }

    // A wrapper over getCountUtil().
    // This function initializes count as 0
    // and calls getCountUtil()
    static INT getCount(node root, int low, int high)
    {
        INT count = new INT();
        count.a = 0;
        getCountUtil(root, low, high, count);
        return count;
    }

    // Utility function to create new node
    static node newNode(int data)
    {
        node temp = new node();
        temp.data = data;
        temp.left = temp.right = null;
        return (temp);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Let us construct  the BST shown in the above figure
        node root = newNode(10);
        root.left = newNode(5);
        root.right = newNode(50);
        root.left.left = newNode(1);
        root.right.left = newNode(40);
        root.right.right = newNode(100);

        /* Let us construct BST shown in above example
        10
        / \
    5 50
    / / \
    1 40 100 */
        int l = 5;
        int h = 45;
        Console.WriteLine("Count of subtrees in [" + l + ", "
                          + h + "] is " + getCount(root, l, h).a);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to count subtrees
// that lie in a given range

    // A BST node

     class node {
            constructor(val) {
                this.data = val;
                this.left = null;
                this.right = null;
            }
        }

    // var class
     class INT {
         constructor(){
         this.a = 0;
         }
    }

    // A utility function to check if data of root is
    // in range from low to high
    function inRange( root , low , high)
    {
        return root.data >= low && root.data <= high;
    }

    // A recursive function to get count
    // of nodes whose subtree is in range
    // from low to high. This function returns
    // true if nodes in subtree rooted under
    // 'root' are in range.
    function getCountUtil( root , low,
                                 high,  count)
    {
        // Base case
        if (root == null)
            return true;

        // Recur for left and right subtrees
        var l = getCountUtil(root.left,
                                 low, high, count);
        var r = getCountUtil(root.right,
                                 low, high, count);

        // If both left and right subtrees are
        // in range and current node is also in
        // range, then increment count and return true
        if (l && r && inRange(root, low, high)) {
            ++count.a;
            return true;
        }

        return false;
    }

    // A wrapper over getCountUtil().
    // This function initializes count as 0
    // and calls getCountUtil()
     function getCount( root , low , high)
    {
        var count = new INT();
        count.a = 0;
        getCountUtil(root, low, high, count);
        return count;
    }

    // Utility function to create new node
     function newNode(data)
    {
        var temp = new node();
        temp.data = data;
        temp.left = temp.right = null;
        return (temp);
    }

    // Driver code

        // Let us construct  the BST shown in the above figure
        var root = newNode(10);
        root.left = newNode(5);
        root.right = newNode(50);
        root.left.left = newNode(1);
        root.right.left = newNode(40);
        root.right.right = newNode(100);
        /* Let us construct BST shown in above example
        10
        / \
    5 50
    / / \
    1 40 100 */
        var l = 5;
        var h = 45;
        document.write("Count of subtrees in [" + l + ", "
                    + h + "] is " + getCount(root, l, h).a);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Count of subtrees in [5, 45] is 1
```

本文由[高拉夫·阿赫瓦尔](https://www.facebook.com/COOL.DUDE.BORN.NUD3?fref=ts)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。