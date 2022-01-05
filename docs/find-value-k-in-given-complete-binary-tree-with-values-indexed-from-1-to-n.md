# 在给定的完整二叉树中找到值 K，其值从 1 到 N 进行索引

> 原文:[https://www . geesforgeks . org/find-value-k-in-给定-complete-二叉树-带值-索引-从-1 到-n/](https://www.geeksforgeeks.org/find-value-k-in-given-complete-binary-tree-with-values-indexed-from-1-to-n/)

给定一个完整的二叉树(T1)和一个键(T2)和一个键(T3)。任务是检查树中是否存在一个键。如果密钥存在，则打印“真”，否则打印“假”。

> 完整的二叉树:如果除了可能的最后一级之外所有的级都被完全填充，并且最后一级尽可能剩下所有的键
> ，那么二叉树就是完整的二叉树

**例:**

> **输入:** K = 2
> 
> ```
>          1
>        /   \  
>      2      3  
>     /  \   / \
>    4    5 6   7
>  /  \   /
> 8    9 10
> ```
> 
> **输出:**真
> 
> **输入:** K = 11
> 
> ```
>          1
>        /   \  
>      2      3  
>     /  \   / \
>    4    5 6   7
>  /  \   /
> 8    9 10
> ```
> 
> **输出:**假

**天真方法:**最简单的方法是简单地遍历整个树，检查树中是否存在密钥。

***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**高效方法:**该方法基于这样的思想，即树是一个完整的二叉树，节点从顶部开始从 1 到 N 进行索引。所以我们可以**追踪**从根到关键的路径，如果关键存在的话。以下是步骤:

1.  对于给定节点 **i** 的完整二叉树，其子节点将是 **2*i** 和 **2*i + 1** 。因此，给定节点 **i** ，其父节点将为 **i/2** 。
2.  迭代找出键的父节点，直到找到树的根节点，将步骤存储在数组中 **steps[]** 为-1 为左，1 为右(left 表示当前节点是其父节点的左子节点，right 表示当前节点是其父节点的右子节点)。
3.  现在按照数组**步骤【】**中存储的招式横树。如果整个数组被成功遍历，这意味着键存在于树中，所以打印“真”，否则打印“假”。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

// Class containing left
// and right child of current node
// and key value
class Node {
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = null;
        right = null;
    }
}

class Solution {

    // Function to store the
    // list of the directions
    public static ArrayList<Integer>
    findSteps(Node root, int data)
    {
        ArrayList<Integer> steps
            = new ArrayList<Integer>();

        // While the root is not found
        while (data != 1) {
            // If it is the right
            // child of its parent
            if (data / 2.0 > data / 2) {

                // Add right step (1)
                steps.add(1);
            }
            else {

                // Add left step (-1)
                steps.add(-1);
            }

            int parent = data / 2;

            // Repeat the same
            // for its parent
            data = parent;
        }

        // Reverse the steps list
        Collections.reverse(steps);

        // Return the steps
        return steps;
    }

    // Function to find
    // if the key is present or not
    public static boolean
    findKey(Node root, int data)
    {
        // Get the steps to be followed
        ArrayList<Integer> steps
            = findSteps(root, data);

        // Taking one step at a time
        for (Integer cur_step : steps) {

            // Go left
            if (cur_step == -1) {

                // If left child does
                // not exist return false
                if (root.left == null)
                    return false;

                root = root.left;
            }

            // Go right
            else {

                // If right child does
                // not exist return false
                if (root.right == null)
                    return false;

                root = root.right;
            }
        }

        // If the entire array of steps
        // has been successfully
        // traversed
        return true;
    }

    public static void main(String[] args)
    {
        /* Consider the following complete binary tree
                 1
                / \ 
               2   3 
              / \ / \
             4  5 6  7
            / \ /
           8  9 10 
        */
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.left.left = new Node(8);
        root.left.left.right = new Node(9);
        root.left.right.left = new Node(10);

        // Function Call
        System.out.println(findKey(root, 7));
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// Class containing left
// and right child of current node
// and key value
class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class Solution {

    // Function to store the
    // list of the directions
    public static List<int>
    findSteps(Node root, int data)
    {
        List<int> steps
            = new List<int>();

        // While the root is not found
        while (data != 1) {
            // If it is the right
            // child of its parent
            if (data / 2.0 > data / 2) {

                // Add right step (1)
                steps.Add(1);
            }
            else {

                // Add left step (-1)
                steps.Add(-1);
            }

            int parent = data / 2;

            // Repeat the same
            // for its parent
            data = parent;
        }

        // Reverse the steps list
        steps.Reverse();

        // Return the steps
        return steps;
    }

    // Function to find
    // if the key is present or not
    public static bool
    findKey(Node root, int data)
    {
        // Get the steps to be followed
        List<int> steps
            = findSteps(root, data);

        // Taking one step at a time
        foreach (int cur_step in steps) {

            // Go left
            if (cur_step == -1) {

                // If left child does
                // not exist return false
                if (root.left == null)
                    return false;

                root = root.left;
            }

            // Go right
            else {

                // If right child does
                // not exist return false
                if (root.right == null)
                    return false;

                root = root.right;
            }
        }

        // If the entire array of steps
        // has been successfully
        // traversed
        return true;
    }

    public static void Main()
    {
        /* Consider the following complete binary tree
                 1
                / \ 
               2   3 
              / \ / \
             4  5 6  7
            / \ /
           8  9 10 
        */
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.left.left = new Node(8);
        root.left.left.right = new Node(9);
        root.left.right.left = new Node(10);

        // Function Call
        Console.Write(findKey(root, 7));
    }
}
```

**Output:** 

```
true
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*