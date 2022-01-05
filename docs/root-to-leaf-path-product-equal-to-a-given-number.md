# 根到叶路径积等于给定的数

> 原文:[https://www . geesforgeks . org/根到叶路径-产品-等于给定号码/](https://www.geeksforgeeks.org/root-to-leaf-path-product-equal-to-a-given-number/)

给定一棵二叉树和一个数，如果树有一个从根到叶的路径，使得沿着该路径的所有值的乘积等于给定的数，则返回真。如果找不到这样的路径，返回为假。

![](img/86196bd25135ca339730eb82b1b7cea1.png)

例如，在上面的树中，存在三个根到叶的路径，具有以下产品。

*   240 –> 10 – 8 – 3
*   400 –> 10 – 8 – 5
*   40 –> 10 – 2 – 2

**方法:**思路是开始递归遍历树，向下递归时如果能整除，则从乘积中除当前节点的值，到达树当前路径的叶节点时检查乘积是否为 1。

下面是上述方法的实现:

## C++

```
// C++ program to check if there exists
// a root to leaf path product with
// given product

#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// Function to check if there exists a path
// with given product

// Strategy: divide the node value from the product
// if it is divisible when recurring down, and check
// to see if the product is 1 when you reach leaf
// node of the current path out of tree.
bool hasPathProduct(struct node* node, int prod)
{
    // return true if we run out
    // of tree and prod==1
    if (node == NULL) {
        return (prod == 1);
    }
    else {
        bool ans = 1;

        // Check if product is divisible by
        // current node, if not we are on wrong path
        if (prod % (node->data))
            return false;

        // otherwise check both subtrees
        int subProduct = prod / node->data;

        // If we reach a leaf node and prod
        // becomes 1 then return true
        if (subProduct == 1 && node->left == NULL
            && node->right == NULL)
            return 1;

        if (node->left)
            ans = hasPathProduct(node->left, subProduct);
        if (node->right)
            ans = hasPathProduct(node->right, subProduct);

        return ans;
    }
}

/* UTILITY FUNCTIONS */
// Helper function that allocates
// a new node with the given data
// and NULL left and right pointers
struct node* newnode(int data)
{
    struct node* newNode = new node();
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;

    return (newNode);
}

// Driver Code
int main()
{
    int prod = 400;

    /* Constructed binary tree is 
            10 
            / \ 
           8   2 
          / \ / 
         3    5 2 
    */

    struct node* root = newnode(10);
    root->left = newnode(8);
    root->right = newnode(2);
    root->left->left = newnode(3);
    root->left->right = newnode(5);
    root->right->left = newnode(2);

    if (hasPathProduct(root, prod))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there exists 
// a root to leaf path product with 
// given product 
class GFG
{

    // Binary Tree Node 
    static class node 
    {

        int data;
        node left;
        node right;
    };

    // Function to check if there exists a path 
    // with given product 
    // Strategy: divide the node value from the product 
    // if it is divisible when recurring down, and check 
    // to see if the product is 1 when you reach leaf 
    // node of the current path out of tree. 
    static boolean hasPathProduct(node node, int prod)
    {
        // return true if we run out 
        // of tree and prod==1 
        if (node == null)
        {
            return (prod == 1);
        } 
        else 
        {
            boolean ans = true;

            // Check if product is divisible by 
            // current node, if not we are on wrong path 
            if (prod % (node.data) == 1)
            {
                return false;
            }

            // otherwise check both subtrees 
            int subProduct = prod / node.data;

            // If we reach a leaf node and prod 
            // becomes 1 then return true 
            if (subProduct == 1 && node.left == null
                    && node.right == null) 
            {
                return true;
            }

            if (node.left != null) 
            {
                ans = hasPathProduct(node.left, subProduct);
            }
            if (node.right != null)
            {
                ans = hasPathProduct(node.right, subProduct);
            }

            return ans;
        }
    }

    /* UTILITY FUNCTIONS */
    // Helper function that allocates 
    // a new node with the given data 
    // and null left and right pointers 
    static node newnode(int data)
    {
        node node = new node();
        node.data = data;
        node.left = null;
        node.right = null;

        return (node);
    }

    // Driver Code 
    public static void main(String[] args)
    {
        int prod = 400;

        /* Constructed binary tree is 
            10 
            / \ 
        8 2 
        / \ / 
        3 5 2 
        */
        node root = newnode(10);
        root.left = newnode(8);
        root.right = newnode(2);
        root.left.left = newnode(3);
        root.left.right = newnode(5);
        root.right.left = newnode(2);

        if (hasPathProduct(root, prod))
        {
            System.out.println("Yes");
        }
        else 
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to check if there exists 
# a root to leaf path product with 
# given product 

""" UTILITY FUNCTIONS """
# Helper function that allocates 
# a new node with the given data 
# and None left and right pointers 
class newnode: 
    def __init__(self, data): 
        self.data = data 
        self.left = self.right = None

# Function to check if there exists 
# a path with given product 

# Strategy: divide the node value from 
# the product if it is divisible when 
# recurring down, and check to see if 
# the product is 1 when you reach leaf 
# node of the current path out of tree. 
def hasPathProduct(node, prod) :

    # return true if we run out 
    # of tree and prod==1 
    if (node == None) :
        return (prod == 1) 

    else :

        ans = 1

        # Check if product is divisible by 
        # current node, if not we are on wrong path 
        if (prod % (node.data)) :
            return False

        # otherwise check both subtrees 
        subProduct = prod // node.data 

        # If we reach a leaf node and prod 
        # becomes 1 then return true 
        if (subProduct == 1 and 
            node.left == None and 
            node.right == None) :
            return 1

        if (node.left) :
            ans = hasPathProduct(node.left, 
                                 subProduct) 
        if (node.right) :
            ans = hasPathProduct(node.right, 
                                 subProduct) 

        return ans 

# Driver Code 
if __name__ == '__main__':
    prod = 400

    """ Constructed binary tree is 
            10 
            / \ 
        8 2 
        / \ / 
        3 5 2 
    """
    root = newnode(10) 
    root.left = newnode(8) 
    root.right = newnode(2) 
    root.left.left = newnode(3) 
    root.left.right = newnode(5) 
    root.right.left = newnode(2) 

    if (hasPathProduct(root, prod)) :
        print("YES" )
    else:
        print("NO")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to check if there exists 
// a root to leaf path product with 
// given product
using System;

class GFG
{

    // Binary Tree Node 
    public class node 
    {

        public int data;
        public node left;
        public node right;
    };

    // Function to check if there exists a path 
    // with given product 
    // Strategy: divide the node value from the product 
    // if it is divisible when recurring down, and check 
    // to see if the product is 1 when you reach leaf 
    // node of the current path out of tree. 
    static bool hasPathProduct(node node, int prod)
    {
        // return true if we run out 
        // of tree and prod==1 
        if (node == null)
        {
            return (prod == 1);
        } 
        else
        {
            bool ans = true;

            // Check if product is divisible by 
            // current node, if not we are on wrong path 
            if (prod % (node.data) == 1)
            {
                return false;
            }

            // otherwise check both subtrees 
            int subProduct = prod / node.data;

            // If we reach a leaf node and prod 
            // becomes 1 then return true 
            if (subProduct == 1 && node.left == null
                    && node.right == null) 
            {
                return true;
            }

            if (node.left != null) 
            {
                ans = hasPathProduct(node.left, subProduct);
            }
            if (node.right != null)
            {
                ans = hasPathProduct(node.right, subProduct);
            }

            return ans;
        }
    }

    /* UTILITY FUNCTIONS */
    // Helper function that allocates 
    // a new node with the given data 
    // and null left and right pointers 
    static node newnode(int data)
    {
        node node = new node();
        node.data = data;
        node.left = null;
        node.right = null;

        return (node);
    }

    // Driver Code 
    public static void Main(String[] args)
    {
        int prod = 400;

        /* Constructed binary tree is 
            10 
            / \ 
        8 2 
        / \ / 
        3 5 2 
        */
        node root = newnode(10);
        root.left = newnode(8);
        root.right = newnode(2);
        root.left.left = newnode(3);
        root.left.right = newnode(5);
        root.right.left = newnode(2);

        if (hasPathProduct(root, prod))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript program to check if there exists 
// a root to leaf path product with 
// given product    // Binary Tree Node 
    class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }

    // Function to check if there exists a path 
    // with given product 
    // Strategy: divide the node value from the product 
    // if it is divisible when recurring down, and check 
    // to see if the product is 1 when you reach leaf 
    // node of the current path out of tree. 
    function hasPathProduct( node , prod)
    {
        // return true if we run out 
        // of tree and prod==1 
        if (node == null)
        {
            return (prod == 1);
        } 
        else 
        {
            var ans = true;

            // Check if product is divisible by 
            // current node, if not we are on wrong path 
            if (prod % (node.data) == 1)
            {
                return false;
            }

            // otherwise check both subtrees 
            var subProduct = prod / node.data;

            // If we reach a leaf node and prod 
            // becomes 1 then return true 
            if (subProduct == 1 && node.left == null
                    && node.right == null) 
            {
                return true;
            }

            if (node.left != null) 
            {
                ans = hasPathProduct(node.left, subProduct);
            }
            if (node.right != null)
            {
                ans = hasPathProduct(node.right, subProduct);
            }

            return ans;
        }
    }

    /* UTILITY FUNCTIONS */
    // Helper function that allocates 
    // a new node with the given data 
    // and null left and right pointers 
     function newnode(data)
    {
        var node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;

        return (node);
    }

    // Driver Code 

        var prod = 400;

        /* Constructed binary tree is 
            10 
            / \ 
        8 2 
        / \ / 
        3 5 2 
        */
        var root = newnode(10);
        root.left = newnode(8);
        root.right = newnode(2);
        root.left.left = newnode(3);
        root.left.right = newnode(5);
        root.right.left = newnode(2);

        if (hasPathProduct(root, prod))
        {
            document.write("Yes");
        }
        else 
        {
            document.write("No");
        }

// This code contributed by Rajput-Ji
</script>
```

**输出**:

```
YES
```

**时间复杂度:** O(n)
***辅助空间** : O(n)*