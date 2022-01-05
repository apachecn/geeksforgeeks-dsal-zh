# 计算给定二叉树中从根到给定节点的路径总和的查询

> 原文:[https://www . geeksforgeeks . org/查询-计算给定二叉树中从根到给定节点的路径总和/](https://www.geeksforgeeks.org/queries-to-calculate-sum-of-the-path-from-root-to-a-given-node-in-given-binary-tree/)

给定一个根在节点 **1** 的[无限完全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，其中每个**I**T6 节点有两个子节点，值为 **2 * i** 和 **2 * (i + 1)** 。给定另一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，每个数组元素 **arr[i]** 的任务是找出从根节点到节点 **arr[i]** 的路径中出现的节点值之和。

**示例:**

> **输入:** arr[] = {3，10}
> **输出:** 4 18
> **解释:**
> 节点 3:路径为 3 - > 1。因此，路径之和为 4。
> 节点 10:路径为 10 - > 5 - > 2 - > 1。因此，节点的总和是 18。
> 
> **输入:** arr[] = {1，4，20}
> **输出:** 1 7 38
> **解释:**
> 节点 1:路径为 1。因此，路径的总和为 1。
> 节点 4:路径为 4 - > 2 - > 1。因此，节点的总和为 7。
> 节点 20:路径为 20->10->5->2->1。因此，节点的总和是 38。

**天真方法:**最简单的方法是对每个数组元素**arr【I】**执行 [**DFS 遍历**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) ，以找到其从当前节点到根的路径，并打印该路径中节点值的总和。
***时间复杂度:** O(N * H)，其中 **H** 为树的最大高度。*
***辅助空间:** O(H)*

**高效方法:**上述方法也可以基于值为 **N** 的节点的父节点包含值 **N/2** 的观察进行优化。按照以下步骤解决问题:

*   初始化一个变量，比如 **sumOfNode** ，来存储路径中节点的总和。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【I】**并执行以下步骤:
    *   对于每个元素 **arr[i]** ，将 **sumOfNode** 的值更新为 **sumOfNode + X** ，将 **arr[i]** 更新为 **arr[i] / 2** 。
    *   当 **arr[i]** 大于 **0** 时，重复上述步骤。
    *   将 **sumOfNode** 的值打印为每个数组元素**arr【I】**的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <vector>
using namespace std;

// Function to find the sum of the
// path from root to the current node
void sumOfNodeInAPath(int node_value)
{
    // Sum of nodes in the path
    int sum_of_node = 0;

    // Iterate until root is reached
    while (node_value) {

        sum_of_node += node_value;

        // Update the node value
        node_value /= 2;
    }

    // Print the resultant sum
    cout << sum_of_node;

    return;
}

// Function to print the path
// sum for each query
void findSum(vector<int> Q)
{
    // Traverse the queries
    for (int i = 0; i < Q.size(); i++) {

        int node_value = Q[i];

        sumOfNodeInAPath(node_value);

        cout << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 5, 20, 100 };
    findSum(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.ArrayList;
class GFG {

  // Function to find the sum of the
  // path from root to the current node
  public static void sumOfNodeInAPath(int node_value)
  {
    // Sum of nodes in the path
    int sum_of_node = 0;

    // Iterate until root is reached
    while (node_value > 0) {

      sum_of_node += node_value;

      // Update the node value
      node_value /= 2;
    }

    // Print the resultant sum
    System.out.print(sum_of_node);
  }

  // Function to print the path
  // sum for each query
  public static void findSum(ArrayList<Integer> Q)
  {
    // Traverse the queries
    for (int i = 0; i < Q.size(); i++) {

      int node_value = Q.get(i);

      sumOfNodeInAPath(node_value);

      System.out.print(" ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    // arraylist to store integers
    ArrayList<Integer> arr = new ArrayList<>();
    arr.add(1);
    arr.add(5);
    arr.add(20);
    arr.add(100);
    findSum(arr);
  }
}

// This code is contributed by aditya7409.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the sum of the
# path from root to the current node
def sumOfNodeInAPath(node_value):

    # Sum of nodes in the path
    sum_of_node = 0

    # Iterate until root is reached
    while (node_value):

        sum_of_node += node_value

        # Update the node value
        node_value //= 2

    # Print the resultant sum
    print(sum_of_node, end = " ")

# Function to print the path
# sum for each query
def findSum(Q):

    # Traverse the queries
    for i in range(len(Q)):
        node_value = Q[i]
        sumOfNodeInAPath(node_value)
        print(end = "")

# Driver Code
arr = [1, 5, 20, 100]
findSum(arr)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to find the sum of the
  // path from root to the current node
  public static void sumOfNodeInAPath(int node_value)
  {

    // Sum of nodes in the path
    int sum_of_node = 0;

    // Iterate until root is reached
    while (node_value > 0) {

      sum_of_node += node_value;

      // Update the node value
      node_value /= 2;
    }

    // Print the resultant sum
    Console.Write(sum_of_node);
  }

  // Function to print the path
  // sum for each query
  public static void findSum(List<int> Q)
  {
    // Traverse the queries
    for (int i = 0; i < Q.Count ; i++) {

      int node_value = Q[i];
      sumOfNodeInAPath(node_value);
      Console.Write(" ");
    }
  }

// Driver Code
static public void Main()
{

    // arraylist to store integers
    List<int> arr = new List<int>();
    arr.Add(1);
    arr.Add(5);
    arr.Add(20);
    arr.Add(100);
    findSum(arr);
}
}
// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program to count frequencies of array items

// Function to find the sum of the
// path from root to the current node
function sumOfNodeInAPath(node_value)
{
    // Sum of nodes in the path
    let sum_of_node = 0;

    // Iterate until root is reached
    while (node_value) {

        sum_of_node += node_value;

        // Update the node value
        node_value = Math.floor(node_value / 2 );
    }

    // Print the resultant sum
    document.write(sum_of_node);

    return;
}

// Function to print the path
// sum for each query
function findSum( Q)
{
    // Traverse the queries
    for (let i = 0; i < Q.length; i++) {

        let node_value = Q[i];

        sumOfNodeInAPath(node_value);

        document.write(" ");
    }
}

// Driver Code

let arr = [ 1, 5, 20, 100 ];
findSum(arr);

</script>
```

**Output:** 

```
1 8 38 197
```

***时间复杂度:** O(N*log X)，其中 **X** 是* [*数组的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*