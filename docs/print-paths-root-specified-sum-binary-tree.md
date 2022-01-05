# 打印从根开始的所有路径，在二叉树中指定一个和

> 原文:[https://www . geesforgeks . org/print-path-root-specified-sum-二叉树/](https://www.geeksforgeeks.org/print-paths-root-specified-sum-binary-tree/)

给定一棵二叉树和一个和 **S** ，打印所有路径，从根开始，求和到给定的和。
注意，这个问题与[根到叶路径](https://www.geeksforgeeks.org/root-to-leaf-path-sum-equal-to-a-given-number/)不同。这里的路径不需要在叶节点上结束。

**示例:**

```
Input : 
Input : sum = 8, 
        Root of tree
         1
       /   \
     20      3
           /    \
         4       15    
        /  \     /  \
       6    7   8    9           
Output :
Path: 1 3 4

Input : sum = 38,
        Root of tree
          10
       /     \
     28       13
           /     \
         14       15
        /   \     /  \
       21   22   23   24
Output : Path found: 10 28 
        Path found: 10 13 15
```

对于这个问题，前序遍历是最适合的，因为我们必须在到达那个节点时添加一个键值。
我们从根开始，通过前序遍历开始遍历，给 *sum_so_far* 加上键值，检查是否等于需要的和。
同样，由于树节点没有指向其父节点的指针，我们必须从我们移动的地方显式保存。我们使用向量*路径*来存储该路径。
该路径中的每个节点都有助于 sum_so_far。

## C++

```
// C++ program to print all paths begiinning with
// root and sum as given sum
#include<bits/stdc++.h>
using namespace std;

// A Tree node
struct Node
{
    int key;
    struct Node *left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

void printPathsUtil(Node* curr_node, int sum,
            int sum_so_far, vector<int> &path)
{
    if (curr_node == NULL)
        return;

    // add the current node's value
    sum_so_far += curr_node->key;

    // add the value to path
    path.push_back(curr_node->key);

    // print the required path
    if (sum_so_far == sum )
    {
        cout << "Path found: ";
        for (int i=0; i<path.size(); i++)
            cout << path[i] << " ";

        cout << endl;
    }

    // if left child exists
    if (curr_node->left != NULL)
        printPathsUtil(curr_node->left, sum, sum_so_far, path);

    // if right child exists
    if (curr_node->right != NULL)
        printPathsUtil(curr_node->right, sum, sum_so_far, path);

    // Remove last element from path
    // and move back to parent
    path.pop_back();
}

// Wrapper over printPathsUtil
void printPaths(Node *root, int sum)
{
    vector<int> path;
    printPathsUtil(root, sum, 0, path);
}

// Driver program
int main ()
{
    /* 10
    /     \
    28     13
        /     \
        14     15
        / \     / \
    21 22 23 24*/
    Node *root = newNode(10);
    root->left = newNode(28);
    root->right = newNode(13);

    root->right->left = newNode(14);
    root->right->right = newNode(15);

    root->right->left->left = newNode(21);
    root->right->left->right = newNode(22);
    root->right->right->left = newNode(23);
    root->right->right->right = newNode(24);

    int sum = 38;

    printPaths(root, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all paths beginning
// with root and sum as given sum
import java.util.ArrayList;

class Graph{

// A Tree node
static class Node
{
    int key;
    Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

static void printPathsUtil(Node curr_node, int sum,
                           int sum_so_far,
                           ArrayList<Integer> path)
{
    if (curr_node == null)
        return;

    // Add the current node's value
    sum_so_far += curr_node.key;

    // Add the value to path
    path.add(curr_node.key);

    // Print the required path
    if (sum_so_far == sum)
    {
        System.out.print("Path found: ");
        for(int i = 0; i < path.size(); i++)
            System.out.print(path.get(i) + " ");

        System.out.println();
    }

    // If left child exists
    if (curr_node.left != null)
        printPathsUtil(curr_node.left, sum,
                       sum_so_far, path);

    // If right child exists
    if (curr_node.right != null)
        printPathsUtil(curr_node.right, sum,
                       sum_so_far, path);

    // Remove last element from path
    // and move back to parent
    path.remove(path.size() - 1);
}

// Wrapper over printPathsUtil
static void printPaths(Node root, int sum)
{
    ArrayList<Integer> path = new ArrayList<>();
    printPathsUtil(root, sum, 0, path);
}

// Driver code
public static void main(String[] args)
{

    /*    10
       /     \
     28       13
           /     \
         14       15
        /   \     /  \
       21   22   23   24*/
    Node root = newNode(10);
    root.left = newNode(28);
    root.right = newNode(13);

    root.right.left = newNode(14);
    root.right.right = newNode(15);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(22);
    root.right.right.left = newNode(23);
    root.right.right.right = newNode(24);

    int sum = 38;

    printPaths(root, sum);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to Print all the
# paths from root, with a specified
# sum in Binary tree

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# This function prints all paths
# that have sum k
def printPathsUtil(curr_node, sum,
                sum_so_far, path):

    # empty node
    if (not curr_node) :
        return
    sum_so_far += curr_node.key

    # add current node to the path
    path.append(curr_node.key)

    # print the required path
    if (sum_so_far == sum ) :

        print("Path found:", end = " ")
        for i in range(len(path)):
            print(path[i], end = " ")

        print()

    # if left child exists
    if (curr_node.left != None) :
        printPathsUtil(curr_node.left, sum,
                    sum_so_far, path)

    # if right child exists
    if (curr_node.right != None) :
        printPathsUtil(curr_node.right, sum,
                    sum_so_far, path)

    # Remove the current element
    # from the path
    path.pop(-1)

# A wrapper over printKPathUtil()
def printPaths(root, sum):

    path = []
    printPathsUtil(root, sum, 0, path)

# Driver Code
if __name__ == '__main__':

    """ 10
    /     \
    28     13
        /     \
        14     15
        / \     / \
    21 22 23 24"""
    root = newNode(10)
    root.left = newNode(28)
    root.right = newNode(13)

    root.right.left = newNode(14)
    root.right.right = newNode(15)

    root.right.left.left = newNode(21)
    root.right.left.right = newNode(22)
    root.right.right.left = newNode(23)
    root.right.right.right = newNode(24)

    sum = 38

    printPaths(root, sum)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## java 描述语言

```
<script>

// JavaScript program to print all paths beginning
// with root and sum as given sum

// A Tree node
class Node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to create a new node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

function printPathsUtil(curr_node, sum, sum_so_far, path)
{
    if (curr_node == null)
        return;

    // Add the current node's value
    sum_so_far += curr_node.key;

    // Add the value to path
    path.push(curr_node.key);

    // Print the required path
    if (sum_so_far == sum)
    {
        document.write("Path found: ");
        for(var i = 0; i < path.length; i++)
            document.write(path[i] + " ");

        document.write("<br>");
    }

    // If left child exists
    if (curr_node.left != null)
        printPathsUtil(curr_node.left, sum,
                       sum_so_far, path);

    // If right child exists
    if (curr_node.right != null)
        printPathsUtil(curr_node.right, sum,
                       sum_so_far, path);

    // Remove last element from path
    // and move back to parent
    path.pop();
}

// Wrapper over printPathsUtil
function printPaths(root, sum)
{
    var path = [];
    printPathsUtil(root, sum, 0, path);
}

// Driver code

/*    10
   /     \
 28       13
       /     \
     14       15
    /   \     /  \
   21   22   23   24*/
var root = newNode(10);
root.left = newNode(28);
root.right = newNode(13);
root.right.left = newNode(14);
root.right.right = newNode(15);
root.right.left.left = newNode(21);
root.right.left.right = newNode(22);
root.right.right.left = newNode(23);
root.right.right.right = newNode(24);
var sum = 38;
printPaths(root, sum);

</script>
```

**输出:**

```
Path found: 10 28 
Path found: 10 13 15
```

本文由 [**舒巴姆·古普塔**](https://www.facebook.com/Shubh1307) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。