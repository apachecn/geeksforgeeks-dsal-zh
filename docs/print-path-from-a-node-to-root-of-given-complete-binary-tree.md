# 打印从一个节点到给定完整二叉树根的路径

> 原文:[https://www . geesforgeks . org/print-path-从节点到给定完整二叉树的根/](https://www.geeksforgeeks.org/print-path-from-a-node-to-root-of-given-complete-binary-tree/)

给定一个整数 **N** ，任务是找到从**N**T4 节点到以下形式的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)根的路径:

> *   Binary tree is a [complete binary tree](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/) up to [T2】 N T7 node level.
> *   The node numbers are **1** to **n** , and **1** from the root.
> *   The structure of the tree is as follows:
>     
> 
> ```
>                1
>            /       \
>           2         3
>        /    \    /   \
>       4     5    6    7
>       ................
>    /    \ ............
>  N - 1  N ............
> ```

**示例:**

> **输入:** N = 7
> **输出:** 7 3 1
> **解释:**从节点 7 到根的路径是 7 - > 3 - > 1。
> 
> **输入:** N = 11
> **输出:** 11 5 2 1
> **说明:**从节点 11 到根的路径是 11 - > 5 - > 2 - > 1。

**天真方法:**解决问题最简单的方法是从给定节点执行 [**DFS**](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 直到遇到根节点并打印路径。

***时间复杂度:*** O(N)
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于给定二叉树的结构进行优化。可以观察到，每个 **N** 的父节点都是 **N / 2** 。因此，重复打印 **N** 的当前值，并将 **N** 更新为 **N / 2** ，直到 **N** 等于 **1** ，即到达根节点。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to print the path
// from node to root
void path_to_root(int node)
{
    // Iterate until root is reached
    while (node >= 1) {

        // Print the value of
        // the current node
        cout << node << ' ';

        // Move to parent of
        // the current node
        node /= 2;
    }
}

// Driver Code
int main()
{
    int N = 7;
    path_to_root(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the path
// from node to root
static void path_to_root(int node)
{

    // Iterate until root is reached
    while (node >= 1)
    {

        // Print the value of
        // the current node
        System.out.print(node + " ");

        // Move to parent of
        // the current node
        node /= 2;
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 7;

    path_to_root(N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the path
# from node to root
def path_to_root(node):

    # Iterate until root is reached
    while (node >= 1):

        # Print the value of
        # the current node
        print(node, end = " ")

        # Move to parent of
        # the current node
        node //= 2

# Driver Code
if __name__ == '__main__':

    N = 7

    path_to_root(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to print the path
// from node to root
static void path_to_root(int node)
{

    // Iterate until root is reached
    while (node >= 1)
    {

        // Print the value of
        // the current node
        Console.Write(node + " ");

        // Move to parent of
        // the current node
        node /= 2;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 7;   
    path_to_root(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the path
// from node to root
function path_to_root(node)
{

    // Iterate until root is reached
    while (node >= 1)
    {

        // Print the value of
        // the current node
        document.write(node + " ");

        // Move to parent of
        // the current node
        node = parseInt(node / 2, 10);
    }
}

// Driver code
let N = 7;

path_to_root(N);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
7 3 1
```

***时间复杂度:**O(log<sub>2</sub>(N))*
***辅助空间:** O(1)*