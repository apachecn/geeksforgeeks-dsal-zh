# 打印完整二叉树中从根到所有节点的路径

> 原文:[https://www . geesforgeks . org/print-path-从根到完整二叉树中的所有节点/](https://www.geeksforgeeks.org/print-path-from-root-to-all-nodes-in-a-complete-binary-tree/)

给定一个数字 **N** ，这是一个完整的二叉树中节点的总数，其中节点从 1 到 N 依次逐级排列。任务是编写一个程序来打印从根到完整二叉树中所有节点的路径。
N = 3 时，树为:

```
     1
  /     \
2        3 
```

对于 N = 7，树将是:

```
       1
    /     \
   2        3 
 /   \    /  \ 
4    5    6   7
```

**例:**

```
Input : 7  
Output : 
1 
1 2 
1 2 4 
1 2 5 
1 3 
1 3 6 
1 3 7 

Input : 4 
Output :
1 
1 2 
1 2 4 
1 3 
```

**解释** :-因为，给定的树是一个完整的二叉树。对于每个节点![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")，我们可以将其左子节点计算为 **2*i** ，右子节点计算为 **2*i + 1** 。
想法是使用回溯方法打印所有路径。维护一个向量来存储路径，最初将根节点 1 推给它，在推左和右子节点之前，打印存储在其中的当前路径，然后也为左和右子节点调用函数。
以下是上述方法的完整实现:

## C++

```
// C++ program to print path from root to all
// nodes in a complete binary tree.

#include <iostream>
#include <vector>
using namespace std;

// Function to print path of all the nodes
// nth node represent as given node
// kth node represents as left and right node
void printPath(vector<int> res, int nThNode, int kThNode)
{
    // base condition
    // if kth node value is greater
    // then nth node then its means
    // kth node is not valid so
    // we not store it into the res
    // simply we just return
    if (kThNode > nThNode)
        return;

    // Storing node into res
    res.push_back(kThNode);

    // Print the path from root to node
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
    cout << "\n";

    // store left path of a tree
    // So for left we will go node(kThNode*2)
    printPath(res, nThNode, kThNode * 2);

    // right path of a tree
    // and for right we will go node(kThNode*2+1)
    printPath(res, nThNode, kThNode * 2 + 1);
}

// Function to print path from root to all of the nodes
void printPathToCoverAllNodeUtil(int nThNode)
{
    // res is for store the path
    // from root to particulate node
    vector<int> res;

    // Print path from root to all node.
    // third argument 1 because of we have
    // to consider root node is 1
    printPath(res, nThNode, 1);
}

// Driver Code
int main()
{
    // Given Node
    int nThNode = 7;

    // Print path from root to all node.
    printPathToCoverAllNodeUtil(nThNode);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print path from root to all
// nodes in a complete binary tree.
import java.util.*;

class GFG
{

// Function to print path of all the nodes
// nth node represent as given node
// kth node represents as left and right node
static void printPath(Vector<Integer> res,
                    int nThNode, int kThNode)
{
    // base condition
    // if kth node value is greater
    // then nth node then its means
    // kth node is not valid so
    // we not store it into the res
    // simply we just return
    if (kThNode > nThNode)
        return;

    // Storing node into res
    res.add(kThNode);

    // Print the path from root to node
    for (int i = 0; i < res.size(); i++)
        System.out.print( res.get(i) + " ");
    System.out.print( "\n");

    // store left path of a tree
    // So for left we will go node(kThNode*2)
    printPath(res, nThNode, kThNode * 2);

    // right path of a tree
    // and for right we will go node(kThNode*2+1)
    printPath(res, nThNode, kThNode * 2 + 1);

    res.remove(res.size()-1);
}

// Function to print path from root to all of the nodes
static void printPathToCoverAllNodeUtil(int nThNode)
{
    // res is for store the path
    // from root to particulate node
    Vector<Integer> res=new Vector<Integer>();

    // Print path from root to all node.
    // third argument 1 because of we have
    // to consider root node is 1
    printPath(res, nThNode, 1);
}

// Driver Code
public static void main(String args[])
{
    // Given Node
    int nThNode = 7;

    // Print path from root to all node.
    printPathToCoverAllNodeUtil(nThNode);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print path from root
# to all nodes in a complete binary tree.

# Function to print path of all the nodes
# nth node represent as given node kth
# node represents as left and right node
def printPath(res, nThNode, kThNode):

    # base condition
    # if kth node value is greater
    # then nth node then its means
    # kth node is not valid so
    # we not store it into the res
    # simply we just return
    if kThNode > nThNode:
        return

    # Storing node into res
    res.append(kThNode)

    # Print the path from root to node
    for i in range(0, len(res)):
        print(res[i], end = " ")
    print()

    # store left path of a tree
    # So for left we will go node(kThNode*2)
    printPath(res[:], nThNode, kThNode * 2)

    # right path of a tree
    # and for right we will go node(kThNode*2+1)
    printPath(res[:], nThNode, kThNode * 2 + 1)

# Function to print path from root
# to all of the nodes
def printPathToCoverAllNodeUtil(nThNode):

    # res is for store the path
    # from root to particulate node
    res = []

    # Print path from root to all node.
    # third argument 1 because of we have
    # to consider root node is 1
    printPath(res, nThNode, 1)

# Driver Code
if __name__ == "__main__":

    # Given Node
    nThNode = 7

    # Print path from root to all node.
    printPathToCoverAllNodeUtil(nThNode)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print path from root to all
// nodes in a complete binary tree.
using System;
using System.Collections.Generic;

class GFG
{

// Function to print path of all the nodes
// nth node represent as given node
// kth node represents as left and right node
static void printPath(List<int> res,
                    int nThNode, int kThNode)
{
    // base condition
    // if kth node value is greater
    // then nth node then its means
    // kth node is not valid so
    // we not store it into the res
    // simply we just return
    if (kThNode > nThNode)
        return;

    // Storing node into res
    res.Add(kThNode);

    // Print the path from root to node
    for (int i = 0; i < res.Count; i++)
        Console.Write( res[i] + " ");
    Console.Write( "\n");

    // store left path of a tree
    // So for left we will go node(kThNode*2)
    printPath(res, nThNode, kThNode * 2);

    // right path of a tree
    // and for right we will go node(kThNode*2+1)
    printPath(res, nThNode, kThNode * 2 + 1);

    res.RemoveAt(res.Count-1);
}

// Function to print path from root to all of the nodes
static void printPathToCoverAllNodeUtil(int nThNode)
{
    // res is for store the path
    // from root to particulate node
    List<int> res=new List<int>();

    // Print path from root to all node.
    // third argument 1 because of we have
    // to consider root node is 1
    printPath(res, nThNode, 1);
}

// Driver Code
public static void Main(String []args)
{
    // Given Node
    int nThNode = 7;

    // Print path from root to all node.
    printPathToCoverAllNodeUtil(nThNode);
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print path from root to all
// nodes in a complete binary tree.

// Function to print path of all the nodes
// nth node represent as given node
// kth node represents as left and right node
function printPath($res, $nThNode, $kThNode)
{
    // base condition
    // if kth node value is greater
    // then nth node then its means
    // kth node is not valid so
    // we not store it into the res
    // simply we just return
    if ($kThNode > $nThNode)
        return;

    // Storing node into res
    array_push($res, $kThNode);

    // Print the path from root to node
    for ($i = 0; $i < count($res); $i++)
        echo $res[$i] . " ";
    echo "\n";

    // store left path of a tree
    // So for left we will go node(kThNode*2)
    printPath($res, $nThNode, $kThNode * 2);

    // right path of a tree
    // and for right we will go node(kThNode*2+1)
    printPath($res, $nThNode, $kThNode * 2 + 1);
}

// Function to print path
// from root to all of the nodes
function printPathToCoverAllNodeUtil($nThNode)
{
    // res is for store the path
    // from root to particulate node
    $res = array();

    // Print path from root to all node.
    // third argument 1 because of we have
    // to consider root node is 1
    printPath($res, $nThNode, 1);
}

// Driver Code

// Given Node
$nThNode = 7;

// Print path from root to all node.
printPathToCoverAllNodeUtil($nThNode);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to print path from root to all
// nodes in a complete binary tree.

// Function to print path of all the nodes
// nth node represent as given node
// kth node represents as left and right node
function printPath(res, nThNode, kThNode)
{
    // base condition
    // if kth node value is greater
    // then nth node then its means
    // kth node is not valid so
    // we not store it into the res
    // simply we just return
    if (kThNode > nThNode)
        return;

    // Storing node into res
    res.push(kThNode);

    // Print the path from root to node
    for (var i = 0; i < res.length; i++)
        document.write( res[i] + " ");
    document.write( "<br>");

    // store left path of a tree
    // So for left we will go node(kThNode*2)
    printPath(res, nThNode, kThNode * 2);

    // right path of a tree
    // and for right we will go node(kThNode*2+1)
    printPath(res, nThNode, kThNode * 2 + 1);

    res.pop()
}

// Function to print path from root to all of the nodes
function printPathToCoverAllNodeUtil( nThNode)
{
    // res is for store the path
    // from root to particulate node
    var res = [];

    // Print path from root to all node.
    // third argument 1 because of we have
    // to consider root node is 1
    printPath(res, nThNode, 1);
}

// Driver Code

// Given Node
var nThNode = 7;

// Print path from root to all node.
printPathToCoverAllNodeUtil(nThNode);

</script>
```

**Output:** 

```
1 
1 2 
1 2 4 
1 2 5 
1 3 
1 3 6 
1 3 7
```