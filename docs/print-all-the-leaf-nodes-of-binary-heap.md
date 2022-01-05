# 打印二进制堆的所有叶节点

> 原文:[https://www . geesforgeks . org/print-all-the-leaf-nodes-of-binary-heap/](https://www.geeksforgeeks.org/print-all-the-leaf-nodes-of-binary-heap/)

给定一个表示二进制堆的[数组表示的 **N** 元素数组，任务是找到这个](https://www.geeksforgeeks.org/array-representation-of-binary-heap/)[二进制堆](https://www.geeksforgeeks.org/binary-heap/)的叶节点。

**示例:**

```
Input: 
arr[] = {1, 2, 3, 4, 5, 6, 7}
Output: 4 5 6 7
Explanation:
             1
           /   \
          2     3
         / \   / \
        4   5 6   7
Leaf nodes of the Binary Heap are:
4 5 6 7

Input: 
arr[] = {1, 2, 3, 4, 5,
         6, 7, 8, 9, 10}
Output: 6 7 8 9 10
Explanation:
                1
             /     \
            2       3
          /   \    / \
         4      5 6   7
       /   \   /
      8     9 10
Leaf Nodes of the Binary Heap are:
6 7 8 9 10

```

**方法:**问题中的关键观察是，如果 H 是二进制堆的高度，那么二进制堆的每个叶节点都将处于高度 **H** 或 **H -1，**处。因此，叶节点可以计算如下:

*   计算二进制堆的总[高度。](https://www.geeksforgeeks.org/height-complete-binary-tree-heap-n-nodes/)
*   以相反的顺序遍历数组，并将每个节点的高度与二进制堆的计算高度 **H** 进行比较。
*   如果当前节点的高度是 H，则将当前节点添加到叶节点。
*   否则，如果当前节点的高度为 H-1，并且没有子节点，那么也将该节点添加为叶节点。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// the leaf nodes of a Binary Heap

import java.lang.*;
import java.util.*;
class GFG {

    // Function to calculate height
    // of the Binary heap with given
    // the count of the nodes
    static int height(int N)
    {
        return (int)Math.ceil(
                   Math.log(N + 1)
                   / Math.log(2))
            - 1;
    }

    // Function to find the leaf
    // nodes of binary heap
    static void findLeafNodes(
        int arr[], int n)
    {
        // Calculate the height of
        // the complete binary tree
        int h = height(n);

        ArrayList<Integer> arrlist
            = new ArrayList<>();

        for (int i = n - 1; i >= 0; i--) {
            if (height(i + 1) == h) {
                arrlist.add(arr[i]);
            }
            else if (height(i + 1) == h - 1
                     && n <= ((2 * i) + 1)) {

                // if the height if h-1,
                // then there should not
                // be any child nodes
                arrlist.add(arr[i]);
            }
            else {
                break;
            }
        }
        printLeafNodes(arrlist);
    }

    // Function to print the leaf nodes
    static void printLeafNodes(
        ArrayList<Integer> arrlist)
    {
        for (int i = arrlist.size() - 1;
             i >= 0; i--) {
            System.out.print(
                arrlist.get(i) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5,
                      6, 7, 8, 9, 10 };
        findLeafNodes(arr, arr.length);
    }
}
```

## C#

```
// C# implementation to print
// the leaf nodes of a Binary Heap
using System;
using System.Collections.Generic;
class GFG{

// Function to calculate height
// of the Binary heap with given
// the count of the nodes
static int height(int N)
{
    return (int)Math.Ceiling(
                Math.Log(N + 1) /
                Math.Log(2)) - 1;
}

// Function to find the leaf
// nodes of binary heap
static void findLeafNodes(int []arr, 
                          int n)
{
    // Calculate the height of
    // the complete binary tree
    int h = height(n);

    List<int> arrlist = new List<int>();

    for (int i = n - 1; i >= 0; i--) 
    {
        if (height(i + 1) == h)
        {
            arrlist.Add(arr[i]);
        }
        else if (height(i + 1) == h - 1 && 
                 n <= ((2 * i) + 1)) 
        {

            // if the height if h-1,
            // then there should not
            // be any child nodes
            arrlist.Add(arr[i]);
        }
        else
        {
            break;
        }
    }
    printLeafNodes(arrlist);
}

// Function to print the leaf nodes
static void printLeafNodes(List<int> arrlist)
{
    for (int i = arrlist.Count - 1; i >= 0; i--) 
    {
        Console.Write(arrlist[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 };
    findLeafNodes(arr, arr.Length);
}
}

// This code is contributed by Princi Singh
```

**Output:**

```
6 7 8 9 10

```

**性能分析:**

*   **时间复杂度:** O(L)，其中 L 为叶节点数。
*   **辅助空间:** O(1)