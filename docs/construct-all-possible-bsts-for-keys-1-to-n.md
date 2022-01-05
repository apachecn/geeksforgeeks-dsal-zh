# 为键 1 至 N 构建所有可能的 BSTs】

> 原文:[https://www . geesforgeks . org/construct-all-可能性-bsts-for-key-1-to-n/](https://www.geeksforgeeks.org/construct-all-possible-bsts-for-keys-1-to-n/)

本文首先讨论了可能的二分搜索法树的计数，然后讨论了所有可能的树的构造。

**从 1 开始的键有多少个结构上唯一的 BST..n？**

```
For example, for N = 2, there are 2 unique BSTs
     1               2  
      \            /
       2         1 

For N = 3, there are 5 possible BSTs
  1              3        3         2      1
    \           /        /        /  \      \
     3        2         1        1    3      2
    /       /            \                    \
   2      1               2                    3
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
我们知道左子树中所有节点都比根小，右子树中的所有节点都比根大，所以如果我们以 1 为根，从 1 到 i-1 的所有数字都将在左子树中，i+1 到 N 将在右子树中。如果 1 到 i-1 可以形成 x 个不同的树，i+1 到 N 可以形成 y 个不同的树，那么当 I 是根时，我们将有 x*y 个总树，我们也有 N 个根的选择，所以我们可以简单地从 1 到 N 迭代根，另一个循环是左右子树。如果我们仔细观察，我们可以注意到计数基本上是[第 n 个加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)。我们已经讨论了不同的方法来找到第 n 个加泰罗尼亚数字[这里](https://www.geeksforgeeks.org/program-nth-catalan-number/)。

**如何为按键 1 构造所有 BST..n？**
想法是维护所有 BST 的根列表。递归构造所有可能的左右子树。为每对左右子树创建一棵树，并将树添加到列表中。下面是详细的算法。

```
1) Initialize list of BSTs as empty.  
2) For every number i where i varies from 1 to N, do following
......a)  Create a new node with key as 'i', let this node be 'node'
......b)  Recursively construct list of all left subtrees.
......c)  Recursively construct list of all right subtrees.
3) Iterate for all left subtrees
   a) For current leftsubtree, iterate for all right subtrees
        Add current left and right subtrees to 'node' and add
        'node' to list.
```

以下是上述想法的实现。

## C++

```
// A C++ prgroam to contrcut all unique BSTs for keys from 1 to n
#include <bits/stdc++.h>
using namespace std;

//  node structure
struct node
{
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node *newNode(int item)
{
    struct node *temp =  new node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do preorder traversal of BST
void preorder(struct node *root)
{
    if (root != NULL)
    {
        cout << root->key << " ";
        preorder(root->left);
        preorder(root->right);
    }
}

//  function for constructing trees
vector<struct node *> constructTrees(int start, int end)
{
    vector<struct node *> list;

    /*  if start > end   then subtree will be empty so returning NULL
        in the list */
    if (start > end)
    {
        list.push_back(NULL);
        return list;
    }

    /*  iterating through all values from start to end  for constructing\
        left and right subtree recursively  */
    for (int i = start; i <= end; i++)
    {
        /*  constructing left subtree   */
        vector<struct node *> leftSubtree  = constructTrees(start, i - 1);

        /*  constructing right subtree  */
        vector<struct node *> rightSubtree = constructTrees(i + 1, end);

        /*  now looping through all left and right subtrees and connecting
            them to ith root  below  */
        for (int j = 0; j < leftSubtree.size(); j++)
        {
            struct node* left = leftSubtree[j];
            for (int k = 0; k < rightSubtree.size(); k++)
            {
                struct node * right = rightSubtree[k];
                struct node * node = newNode(i);// making value i as root
                node->left = left;              // connect left subtree
                node->right = right;            // connect right subtree
                list.push_back(node);           // add this tree to list
            }
        }
    }
    return list;
}

// Driver Program to test above functions
int main()
{
    // Construct all possible BSTs
    vector<struct node *> totalTreesFrom1toN = constructTrees(1, 3);

    /*  Printing preorder traversal of all constructed BSTs   */
    cout << "Preorder traversals of all constructed BSTs are \n";
    for (int i = 0; i < totalTreesFrom1toN.size(); i++)
    {
        preorder(totalTreesFrom1toN[i]);
        cout << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java prgroam to contrcut all unique BSTs for keys from 1 to n
import java.util.ArrayList;
public class Main {

    //  function for constructing trees
    static ArrayList<Node> constructTrees(int start, int end)
    {
        ArrayList<Node> list=new ArrayList<>();
        /*  if start > end   then subtree will be empty so returning NULL
            in the list */
        if (start > end)
        {
            list.add(null);
            return list;
        }

        /*  iterating through all values from start to end  for constructing\
            left and right subtree recursively  */
        for (int i = start; i <= end; i++)
        {
            /*  constructing left subtree   */
            ArrayList<Node> leftSubtree  = constructTrees(start, i - 1);

            /*  constructing right subtree  */
            ArrayList<Node> rightSubtree = constructTrees(i + 1, end);

            /*  now looping through all left and right subtrees and connecting
                them to ith root  below  */
            for (int j = 0; j < leftSubtree.size(); j++)
            {
                Node left = leftSubtree.get(j);
                for (int k = 0; k < rightSubtree.size(); k++)
                {
                    Node right = rightSubtree.get(k);
                    Node node = new Node(i);        // making value i as root
                    node.left = left;              // connect left subtree
                    node.right = right;            // connect right subtree
                    list.add(node);                // add this tree to list
                }
            }
        }
        return list;
    }

    // A utility function to do preorder traversal of BST
    static void preorder(Node root)
    {
        if (root != null)
        {
            System.out.print(root.key+" ") ;
            preorder(root.left);
            preorder(root.right);
        }
    }

    public static void main(String args[])
    {
        ArrayList<Node> totalTreesFrom1toN = constructTrees(1, 3);
        /*  Printing preorder traversal of all constructed BSTs   */
        System.out.println("Preorder traversals of all constructed BSTs are ");
        for (int i = 0; i < totalTreesFrom1toN.size(); i++)
        {
            preorder(totalTreesFrom1toN.get(i));
            System.out.println();
        }
    }
}

//  node structure
class Node
{
    int key;
    Node left, right;
    Node(int data)
    {
        this.key=data;
        left=right=null;
    }
};
//This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
# Python3 prgroam to contrcut all unique
# BSTs for keys from 1 to n

# Binary Tree Node
""" A utility function to create a
new BST node """
class newNode:

    # Construct to create a newNode
    def __init__(self, item):
        self.key=item
        self.left = None
        self.right = None

# A utility function to do preorder
# traversal of BST
def preorder(root) :

    if (root != None) :

        print(root.key, end = " " )
        preorder(root.left)
        preorder(root.right)

# function for constructing trees
def constructTrees(start, end):

    list = []

    """ if start > end then subtree will be
        empty so returning None in the list """
    if (start > end) :

        list.append(None)
        return list

    """ iterating through all values from
        start to end for constructing
        left and right subtree recursively """
    for i in range(start, end + 1):

        """ constructing left subtree """
        leftSubtree = constructTrees(start, i - 1)

        """ constructing right subtree """
        rightSubtree = constructTrees(i + 1, end)

        """ now looping through all left and
            right subtrees and connecting
            them to ith root below """
        for j in range(len(leftSubtree)) :
            left = leftSubtree[j]
            for k in range(len(rightSubtree)):
                right = rightSubtree[k]
                node = newNode(i)   # making value i as root
                node.left = left    # connect left subtree
                node.right = right    # connect right subtree
                list.append(node)    # add this tree to list
    return list

# Driver Code
if __name__ == '__main__':

    # Construct all possible BSTs
    totalTreesFrom1toN = constructTrees(1, 3)

    """ Printing preorder traversal of
        all constructed BSTs """
    print("Preorder traversals of all",
                "constructed BSTs are")
    for i in range(len(totalTreesFrom1toN)):
        preorder(totalTreesFrom1toN[i])
        print()

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# prgroam to contrcut all
// unique BSTs for keys from 1 to n
using System.Collections;
using System;

class GFG
{

    // function for constructing trees
    static ArrayList constructTrees(int start, int end)
    {
        ArrayList list = new ArrayList();

        /* if start > end then subtree will
        be empty so returning NULL
        in the list */
        if (start > end)
        {
            list.Add(null);
            return list;
        }

        /* iterating through all values from
        start to end for constructing\
        left and right subtree recursively */
        for (int i = start; i <= end; i++)
        {
            /* constructing left subtree */
            ArrayList leftSubtree = constructTrees(start, i - 1);

            /* constructing right subtree */
            ArrayList rightSubtree = constructTrees(i + 1, end);

            /* now looping through all left and
            right subtrees and connecting
            them to ith root below */
            for (int j = 0; j < leftSubtree.Count; j++)
            {
                Node left = (Node)leftSubtree[j];
                for (int k = 0; k < rightSubtree.Count; k++)
                {
                    Node right = (Node)rightSubtree[k];

                    // making value i as root
                    Node node = new Node(i);

                    // connect left subtree
                    node.left = left;

                    // connect right subtree
                    node.right = right;    

                    // Add this tree to list
                    list.Add(node);        
                }
            }
        }
        return list;
    }

    // A utility function to do
    // preorder traversal of BST
    static void preorder(Node root)
    {
        if (root != null)
        {
            Console.Write(root.key+" ") ;
            preorder(root.left);
            preorder(root.right);
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        ArrayList totalTreesFrom1toN = constructTrees(1, 3);

        /* Printing preorder traversal
        of all constructed BSTs */
        Console.WriteLine("Preorder traversals of all" +
                                "constructed BSTs are ");
        for (int i = 0; i < totalTreesFrom1toN.Count; i++)
        {
            preorder((Node)totalTreesFrom1toN[i]);
            Console.WriteLine();
        }
    }

// node structure
public class Node
{
    public int key;
    public Node left, right;
    public Node(int data)
    {
        this.key=data;
        left=right=null;
    }
};
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// node structure
class Node
{
    constructor(data)
    {
        this.key = data;
        this.left = null;
        this.right = null;
    }
};

// Javascript prgroam to contrcut all
// unique BSTs for keys from 1 to n
// function for constructing trees
function constructTrees(start, end)
{
    var list = [];

    /* if start > end then subtree will
    be empty so returning NULL
    in the list */
    if (start > end)
    {
        list.push(null);
        return list;
    }

    /* iterating through all values from
    start to end for constructing\
    left and right subtree recursively */
    for (var i = start; i <= end; i++)
    {
        /* constructing left subtree */
        var leftSubtree = constructTrees(start, i - 1);

        /* constructing right subtree */
        var rightSubtree = constructTrees(i + 1, end);

        /* now looping through all left and
        right subtrees and connecting
        them to ith root below */
        for (var j = 0; j < leftSubtree.length; j++)
        {
            var left = leftSubtree[j];
            for (var k = 0; k < rightSubtree.length; k++)
            {
                var right = rightSubtree[k];

                // making value i as root
                var node = new Node(i);

                // connect left subtree
                node.left = left;

                // connect right subtree
                node.right = right;    

                // push this tree to list
                list.push(node);        
            }
        }
    }
    return list;
}

// A utility function to do
// preorder traversal of BST
function preorder(root)
{
    if (root != null)
    {
        document.write(root.key+" ") ;
        preorder(root.left);
        preorder(root.right);
    }
}
// Driver code
var totalTreesFrom1toN = constructTrees(1, 3);

/* Printing preorder traversal
of all constructed BSTs */
document.write("Preorder traversals of all" +
                        "constructed BSTs are<br>");
for (var i = 0; i < totalTreesFrom1toN.length; i++)
{
    preorder(totalTreesFrom1toN[i]);
    document.write("<br>");
}

</script>
```

**输出:**

```
Preorder traversals of all constructed BSTs are
1 2 3
1 3 2
2 1 3
3 1 2
3 2 1
```

本文由 [**乌卡什·特里维迪**](https://www.linkedin.com/pub/utkarsh-trivedi/a7/69/253) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息