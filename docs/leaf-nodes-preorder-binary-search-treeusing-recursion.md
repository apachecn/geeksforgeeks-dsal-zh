# 二叉查找树的叶节点(使用递归)

> 原文:[https://www . geesforgeks . org/leaf-nodes-preorder-binary-search-tree use-recursion/](https://www.geeksforgeeks.org/leaf-nodes-preorder-binary-search-treeusing-recursion/)

给定二叉查找树的预序遍历。然后任务是打印给定订单中二叉查找树的叶节点。

**例:**

```
Input : preorder[] = {890, 325, 290, 530, 965};
Output : 290 530 965

Tree represented is,
      890
     /   \
  325    965
  /  \
290   530

Input :  preorder[] = { 3, 2, 4 };
Output : 2 4
```

在这篇文章中，讨论了一个简单的递归解决方案。其思想是使用两个最小和最大变量，取 I(输入数组中的索引)，给定前序数组的索引，递归创建根节点，并相应地检查左和右是否存在。这个方法返回布尔变量，如果左边和右边都是假，那么它就意味着左边和右边都是空的，因此它必须是一个叶节点，所以把它打印在那里，并返回真，因为根在那个索引存在。

## c++

```
// Recursive C++ program  to find leaf
// nodes from given preorder traversal
#include<bits/stdc++.h>
using namespace std;

// Print the leaf node from
// the given preorder of BST.
bool isLeaf(int pre[], int &i, int n,
                        int min, int max)
{   
    if (i >= n)
        return false;

    if (pre[i] > min && pre[i] < max) {
        i++;

        bool left = isLeaf(pre, i, n, min, pre[i-1]);
        bool right = isLeaf(pre, i, n, pre[i-1], max);

        if (!left && !right)
            cout << pre[i-1] << " ";

        return true;
    }
    return false;
}

void printLeaves(int preorder[],  int n)
{
    int i = 0;   
    isLeaf(preorder, i, n, INT_MIN, INT_MAX);
}

// Driver code
int main()
{
    int preorder[] = { 890, 325, 290, 530, 965 };
    int n = sizeof(preorder)/sizeof(preorder[0]);
    printLeaves(preorder, n);   
    return 0;
}
```

## Java

```
// Recursive Java program to find leaf
// nodes from given preorder traversal
class GFG
{

    static int i = 0;

    // Print the leaf node from
    // the given preorder of BST.
    static boolean isLeaf(int pre[], int n,
            int min, int max)
    {
        if (i >= n)
        {
            return false;
        }

        if (pre[i] > min && pre[i] < max)
        {
            i++;

            boolean left = isLeaf(pre, n, min, pre[i - 1]);
            boolean right = isLeaf(pre, n, pre[i - 1], max);

            if (!left && !right)
            {
                System.out.print(pre[i - 1] + " ");
            }

            return true;
        }
        return false;
    }

    static void printLeaves(int preorder[], int n)
    {

        isLeaf(preorder, n, Integer.MIN_VALUE,
                            Integer.MAX_VALUE);
    }

    // Driver code
    public static void main(String[] args)
    {
        int preorder[] = {890, 325, 290, 530, 965};
        int n = preorder.length;
        printLeaves(preorder, n);
    }
}

// This code contributed by Rajput-Ji
```

## python 3

T2

## c#

T21

```
// Recursive C# program to find leaf
// nodes from given preorder traversal
using System;

class GFG
{

    static int i = 0;

    // Print the leaf node from
    // the given preorder of BST.
    static bool isLeaf(int []pre, int n,
                        int min, int max)
    {
        if (i >= n)
        {
            return false;
        }

        if (pre[i] > min && pre[i] < max)
        {
            i++;

            bool left = isLeaf(pre, n, min, pre[i - 1]);
            bool right = isLeaf(pre, n, pre[i - 1], max);

            if (!left && !right)
            {
                Console.Write(pre[i - 1] + " ");
            }

            return true;
        }
        return false;
    }

    static void printLeaves(int []preorder, int n)
    {

        isLeaf(preorder, n, int.MinValue, int.MaxValue);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []preorder = {890, 325, 290, 530, 965};
        int n = preorder.Length;
        printLeaves(preorder, n);
    }
}

// This code is contributed by princiraj1992
```

## PHP

```
<?php
// Recursive PHP program to
// find leaf nodes from given
// preorder traversal

// Print the leaf node from
// the given preorder of BST.

function isLeaf($pre, &$i, $n,
                $min, $max)
{
    if ($i >= $n)
        return false;

    if ($pre[$i] > $min &&
        $pre[$i] < $max)
    {
        $i++;

        $left = isLeaf($pre, $i, $n,
                       $min, $pre[$i - 1]);
        $right = isLeaf($pre, $i, $n,
                        $pre[$i - 1], $max);

        if (!$left && !$right)
            echo $pre[$i - 1] , " ";

        return true;
    }
    return false;
}

function printLeaves($preorder, $n)
{
    $i = 0;
    isLeaf($preorder, $i, $n,
           PHP_INT_MIN, PHP_INT_MAX);
}

// Driver code
$preorder = array (890, 325, 290,
                   530, 965 );
$n = sizeof($preorder);
printLeaves($preorder, $n);

// This code is contributed by ajit
?>
```

## Javascript

```
<script>

// Recursive Javascript program to find leaf
// nodes from given preorder traversal
let i = 0;

// Print the leaf node from
// the given preorder of BST.
function isLeaf(pre, n, min, max)
{
    if (i >= n)
    {
        return false;
    }

    if (pre[i] > min && pre[i] < max)
    {
        i++;

        let left = isLeaf(pre, n, min, pre[i - 1]);
        let right = isLeaf(pre, n, pre[i - 1], max);

        if (!left && !right)
        {
            document.write(pre[i - 1] + " ");
        }

        return true;
    }
    return false;
}

function printLeaves(preorder, n)
{
    isLeaf(preorder, n, Number.MIN_VALUE,
                        Number.MAX_VALUE);
}

// Driver code
let preorder = [ 890, 325, 290, 530, 965 ];
let n = preorder.length;

printLeaves(preorder, n);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
290 530 965 
```