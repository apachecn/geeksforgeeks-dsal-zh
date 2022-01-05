# 二叉树中给定和的子树

> 原文:[https://www . geesforgeks . org/subtree-given-sum-二叉树/](https://www.geeksforgeeks.org/subtree-given-sum-binary-tree/)

给你一棵二叉树和一个给定的和。任务是检查是否存在所有节点的总和等于给定总和的子树。

![](img/3fe68e1f4fb92b42bda15ee46d1b9ba1.png)

**例:**

```
// For above tree
Input : sum = 17
Output: "Yes"
// sum of all nodes of subtree {3, 5, 9} = 17

Input : sum = 11
Output: "No"
// no subtree with given sum exist
```

这个想法是以后序方式遍历树，因为这里我们必须自下而上地思考。首先计算左子树的和，然后计算右子树的和，检查**sum _ left+sum _ right+cur _ node = sum**是否满足任意给定和的子树存在的条件。下面是算法的递归实现。

## C++

```
// C++ program to find if there is a subtree with
// given sum
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct Node
{
    int data;
    struct Node* left, *right;
};

/* utility that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* newnode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right  = NULL;
    return (node);
}

// function to check if there exist any subtree with given sum
// cur_sum  --> sum of current subtree from ptr as root
// sum_left --> sum of left subtree from ptr as root
// sum_right --> sum of right subtree from ptr as root
bool sumSubtreeUtil(struct Node *ptr, int *cur_sum, int sum)
{
    // base condition
    if (ptr == NULL)
    {
        *cur_sum = 0;
        return false;
    }

    // Here first we go to left sub-tree, then right subtree
    // then first we calculate sum of all nodes of subtree
    // having ptr as root and assign it as cur_sum
    // cur_sum = sum_left + sum_right + ptr->data
    // after that we check if cur_sum == sum
    int sum_left = 0, sum_right = 0;
    return ( sumSubtreeUtil(ptr->left, &sum_left, sum) ||
             sumSubtreeUtil(ptr->right, &sum_right, sum) ||
        ((*cur_sum = sum_left + sum_right + ptr->data) == sum));
}

// Wrapper over sumSubtreeUtil()
bool sumSubtree(struct Node *root, int sum)
{
    // Initialize sum of subtree with root
    int cur_sum = 0;

    return sumSubtreeUtil(root, &cur_sum, sum);
}

// driver program to run the case
int main()
{
    struct Node *root = newnode(8);
    root->left    = newnode(5);
    root->right   = newnode(4);
    root->left->left = newnode(9);
    root->left->right = newnode(7);
    root->left->right->left = newnode(1);
    root->left->right->right = newnode(12);
    root->left->right->right->right = newnode(2);
    root->right->right = newnode(11);
    root->right->right->left = newnode(3);
    int sum = 22;

    if (sumSubtree(root, sum))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there
// is a subtree with given sum
import java.util.*;
class GFG
{

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
static class Node
{
    int data;
    Node left, right;
}

static class INT
{
    int v;
    INT(int a)
    {
        v = a;
    }
}

/* utility that allocates a new
 node with the given data and
 null left and right pointers. */
static Node newnode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// function to check if there exist
// any subtree with given sum
// cur_sum -. sum of current subtree
//            from ptr as root
// sum_left -. sum of left subtree
//             from ptr as root
// sum_right -. sum of right subtree
//              from ptr as root
static boolean sumSubtreeUtil(Node ptr,
                              INT cur_sum,
                              int sum)
{
    // base condition
    if (ptr == null)
    {
        cur_sum = new INT(0);
        return false;
    }

    // Here first we go to left
    // sub-tree, then right subtree
    // then first we calculate sum
    // of all nodes of subtree having
    // ptr as root and assign it as
    // cur_sum. (cur_sum = sum_left +
    // sum_right + ptr.data) after that
    // we check if cur_sum == sum
    INT sum_left = new INT(0),
        sum_right = new INT(0);
    return (sumSubtreeUtil(ptr.left, sum_left, sum) ||
            sumSubtreeUtil(ptr.right, sum_right, sum) ||
        ((cur_sum.v = sum_left.v +
                      sum_right.v + ptr.data) == sum));
}

// Wrapper over sumSubtreeUtil()
static boolean sumSubtree(Node root, int sum)
{
    // Initialize sum of
    // subtree with root
    INT cur_sum = new INT( 0);

    return sumSubtreeUtil(root, cur_sum, sum);
}

// Driver Code
public static void main(String args[])
{
    Node root = newnode(8);
    root.left = newnode(5);
    root.right = newnode(4);
    root.left.left = newnode(9);
    root.left.right = newnode(7);
    root.left.right.left = newnode(1);
    root.left.right.right = newnode(12);
    root.left.right.right.right = newnode(2);
    root.right.right = newnode(11);
    root.right.right.left = newnode(3);
    int sum = 22;

    if (sumSubtree(root, sum))
        System.out.println( "Yes");
    else
        System.out.println( "No");
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find if there is a
# subtree with given sum

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class newnode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# function to check if there exist any
# subtree with given sum
# cur_sum -. sum of current subtree
#            from ptr as root
# sum_left -. sum of left subtree from
#             ptr as root
# sum_right -. sum of right subtree
#              from ptr as root
def sumSubtreeUtil(ptr,cur_sum,sum):

    # base condition
    if (ptr == None):
        cur_sum[0] = 0
        return False

    # Here first we go to left sub-tree,
    # then right subtree then first we
    # calculate sum of all nodes of subtree
    # having ptr as root and assign it as cur_sum
    # cur_sum = sum_left + sum_right + ptr.data
    # after that we check if cur_sum == sum
    sum_left, sum_right = [0], [0]
    x=sumSubtreeUtil(ptr.left, sum_left, sum)
    y=sumSubtreeUtil(ptr.right, sum_right, sum)
    cur_sum[0] = (sum_left[0] +
                  sum_right[0] + ptr.data)
    return ((x or y)or (cur_sum[0] == sum))

# Wrapper over sumSubtreeUtil()
def sumSubtree(root, sum):

    # Initialize sum of subtree with root
    cur_sum = [0]

    return sumSubtreeUtil(root, cur_sum, sum)

# Driver Code
if __name__ == '__main__':

    root = newnode(8)
    root.left = newnode(5)
    root.right = newnode(4)
    root.left.left = newnode(9)
    root.left.right = newnode(7)
    root.left.right.left = newnode(1)
    root.left.right.right = newnode(12)
    root.left.right.right.right = newnode(2)
    root.right.right = newnode(11)
    root.right.right.left = newnode(3)
    sum = 22

    if (sumSubtree(root, sum)) :
        print("Yes" )
    else:
        print("No")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
using System;

// C# program to find if there
// is a subtree with given sum
public class GFG
{

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
public class Node
{
    public int data;
    public Node left, right;
}

public class INT
{
    public int v;
    public INT(int a)
    {
        v = a;
    }
}

/* utility that allocates a new
node with the given data and
null left and right pointers. */
public static Node newnode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// function to check if there exist
// any subtree with given sum
// cur_sum -. sum of current subtree
//         from ptr as root
// sum_left -. sum of left subtree
//             from ptr as root
// sum_right -. sum of right subtree
//             from ptr as root
public static bool sumSubtreeUtil(Node ptr, INT cur_sum, int sum)
{
    // base condition
    if (ptr == null)
    {
        cur_sum = new INT(0);
        return false;
    }

    // Here first we go to left
    // sub-tree, then right subtree
    // then first we calculate sum
    // of all nodes of subtree having
    // ptr as root and assign it as
    // cur_sum. (cur_sum = sum_left +
    // sum_right + ptr.data) after that
    // we check if cur_sum == sum
    INT sum_left = new INT(0), sum_right = new INT(0);
    return (sumSubtreeUtil(ptr.left, sum_left, sum)
            || sumSubtreeUtil(ptr.right, sum_right, sum)
            || ((cur_sum.v = sum_left.v + sum_right.v + ptr.data) == sum));
}

// Wrapper over sumSubtreeUtil()
public static bool sumSubtree(Node root, int sum)
{
    // Initialize sum of
    // subtree with root
    INT cur_sum = new INT(0);

    return sumSubtreeUtil(root, cur_sum, sum);
}

// Driver Code
public static void Main(string[] args)
{
    Node root = newnode(8);
    root.left = newnode(5);
    root.right = newnode(4);
    root.left.left = newnode(9);
    root.left.right = newnode(7);
    root.left.right.left = newnode(1);
    root.left.right.right = newnode(12);
    root.left.right.right.right = newnode(2);
    root.right.right = newnode(11);
    root.right.right.left = newnode(3);
    int sum = 22;

    if (sumSubtree(root, sum))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to find if there
// is a subtree with given sum

    /*
     * A binary tree node has data, pointer to left child and a pointer to right
     * child
     */
     class Node {
        constructor(){
        this.data = 0;
        this.left = null;
        this.right = null;
        }
    }

     class INT {

        constructor(a) {
            this.v = a;
        }
    }

    /*
     * utility that allocates a new node with the given data and null left and right
     * pointers.
     */
    function newnode(data) {
        var node = new Node();
        node.data = data;
        node.left = node.right = null;
        return (node);
    }

    // function to check if there exist
    // any subtree with given sum
    // cur_sum -. sum of current subtree
    // from ptr as root
    // sum_left -. sum of left subtree
    // from ptr as root
    // sum_right -. sum of right subtree
    // from ptr as root
    function sumSubtreeUtil( ptr,  cur_sum , sum)
    {

        // base condition
        if (ptr == null)
        {
            cur_sum = new INT(0);
            return false;
        }

        // Here first we go to left
        // sub-tree, then right subtree
        // then first we calculate sum
        // of all nodes of subtree having
        // ptr as root and assign it as
        // cur_sum. (cur_sum = sum_left +
        // sum_right + ptr.data) after that
        // we check if cur_sum == sum
        var sum_left = new INT(0), sum_right = new INT(0);
        return (sumSubtreeUtil(ptr.left, sum_left, sum) || sumSubtreeUtil(ptr.right, sum_right, sum)
                || ((cur_sum.v = sum_left.v + sum_right.v + ptr.data) == sum));
    }

    // Wrapper over sumSubtreeUtil()
    function sumSubtree( root, sum)
    {

        // Initialize sum of
        // subtree with root
        var cur_sum = new INT(0);

        return sumSubtreeUtil(root, cur_sum, sum);
    }

    // Driver Code

        var root = newnode(8);
        root.left = newnode(5);
        root.right = newnode(4);
        root.left.left = newnode(9);
        root.left.right = newnode(7);
        root.left.right.left = newnode(1);
        root.left.right.right = newnode(12);
        root.left.right.right.right = newnode(2);
        root.right.right = newnode(11);
        root.right.right.left = newnode(3);
        var sum = 22;

        if (sumSubtree(root, sum))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
Yes
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。