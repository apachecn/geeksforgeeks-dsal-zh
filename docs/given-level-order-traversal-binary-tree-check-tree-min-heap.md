# 给定二叉树的级别顺序遍历，检查该树是否是最小堆

> 原文:[https://www . geesforgeks . org/给定级别-顺序-遍历-二叉树-检查-树-min-heap/](https://www.geeksforgeeks.org/given-level-order-traversal-binary-tree-check-tree-min-heap/)

给定一个[完全二叉树](https://www.geeksforgeeks.org/check-if-a-given-binary-tree-is-complete-tree-or-not/)的水平顺序遍历，确定该二叉树是否是有效的[最小堆](https://www.geeksforgeeks.org/binary-heap/)
T5】示例:

```
Input : level = [10, 15, 14, 25, 30]
Output : True
The tree of the given level order traversal is
                     10
                    /  \
                   15   14
                  /  \
                 25   30
We see that each parent has a value less than
its child, and hence satisfies the min-heap 
property

Input : level = [30, 56, 22, 49, 30, 51, 2, 67]
Output : False
The tree of the given level order traversal is
                         30
                      /      \
                    56         22
                 /      \     /   \
               49        30  51    2
              /
             67
We observe that at level 0, 30 > 22, and hence
min-heap property is not satisfied
```

我们需要检查每个非叶节点(父节点)是否满足[堆属性](https://www.geeksforgeeks.org/binary-heap/)。为此，我们检查每个父代(在索引 I 处)是否小于其子代(在索引 2*i+1 和 2*i+2 处，如果父代有两个子代)。如果只有一个孩子，我们只对照索引 2*i+1 检查父母。

## C++

```
// C++ program to check if a given tree is
// Binary Heap or not
#include <bits/stdc++.h>
using namespace std;

// Returns true if given level order traversal
// is Min Heap.
bool isMinHeap(int level[], int n)
{
    // First non leaf node is at index (n/2-1).
    // Check whether each parent is greater than child
    for (int i=(n/2-1) ; i>=0 ; i--)
    {
        // Left child will be at index 2*i+1
        // Right child will be at index 2*i+2
        if (level[i] > level[2 * i + 1])
            return false;

        if (2*i + 2 < n)
        {
            // If parent is greater than right child
            if (level[i] > level[2 * i + 2])
                return false;
        }
    }
    return true;
}

// Driver code
int main()
{
    int level[] = {10, 15, 14, 25, 30};
    int n = sizeof(level)/sizeof(level[0]);
    if  (isMinHeap(level, n))
        cout << "True";
    else
        cout << "False";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given tree is
// Binary Heap or not
import java.io.*;
import java.util.*;

public class detheap
{
    // Returns true if given level order traversal
    // is Min Heap.
    static boolean isMinHeap(int []level)
    {
        int n = level.length - 1;

        // First non leaf node is at index (n/2-1).
        // Check whether each parent is greater than child
        for (int i=(n/2-1) ; i>=0 ; i--)
        {
            // Left child will be at index 2*i+1
            // Right child will be at index 2*i+2
            if (level[i] > level[2 * i + 1])
                return false;

            if (2*i + 2 < n)
            {
                // If parent is greater than right child
                if (level[i] > level[2 * i + 2])
                   return false;
            }
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
                              throws IOException
    {
        // Level order traversal
        int[] level = new int[]{10, 15, 14, 25, 30};

        if  (isMinHeap(level))
            System.out.println("True");
        else
            System.out.println("False");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if a given
# tree is Binary Heap or not

# Returns true if given level order
# traversal is Min Heap.
def isMinHeap(level, n):

    # First non leaf node is at index
    # (n/2-1). Check whether each parent
    # is greater than child
    for i in range(int(n / 2) - 1, -1, -1):

        # Left child will be at index 2*i+1
        # Right child will be at index 2*i+2
        if level[i] > level[2 * i + 1]:
            return False

        if 2 * i + 2 < n:

            # If parent is greater than right child
            if level[i] > level[2 * i + 2]:
                return False
    return True

# Driver code
if __name__ == '__main__':
    level = [10, 15, 14, 25, 30]
    n = len(level)
    if isMinHeap(level, n):
        print("True")
    else:
        print("False")

# This code is contributed by PranchalK
```

## C#

```
// C# program to check if a given tree
// is Binary Heap or not
using System;

class GFG
{
// Returns true if given level
// order traversal is Min Heap.
public static bool isMinHeap(int[] level)
{
    int n = level.Length - 1;

    // First non leaf node is at
    // index (n/2-1). Check whether
    // each parent is greater than child
    for (int i = (n / 2 - 1) ; i >= 0 ; i--)
    {
        // Left child will be at index 2*i+1
        // Right child will be at index 2*i+2
        if (level[i] > level[2 * i + 1])
        {
            return false;
        }

        if (2 * i + 2 < n)
        {
            // If parent is greater than right child
            if (level[i] > level[2 * i + 2])
            {
            return false;
            }
        }
    }
    return true;
}

// Driver code
public static void Main(string[] args)
{
    // Level order traversal
    int[] level = new int[]{10, 15, 14, 25, 30};

    if (isMinHeap(level))
    {
        Console.WriteLine("True");
    }
    else
    {
        Console.WriteLine("False");
    }
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given tree
// is Binary Heap or not

// Returns true if given level order
// traversal is Min Heap.
function isMinHeap($level, $n)
{
    // First non leaf node is at index
    // (n/2-1). Check whether each parent
    // is greater than child
    for ($i = ($n / 2 - 1); $i >= 0; $i--)
    {
        // Left child will be at index 2*i+1
        // Right child will be at index 2*i+2
        if ($level[$i] > $level[2 * $i + 1])
            return false;

        if (2 * $i + 2 < $n)
        {
            // If parent is greater than right child
            if ($level[$i] > $level[2 * $i + 2])
                return false;
        }
    }
    return true;
}

// Driver code
$level = array(10, 15, 14, 25, 30);
$n = sizeof($level);
if (isMinHeap($level, $n))
    echo "True";
else
    echo "False";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript program to check if a given tree
// is Binary Heap or not

// Returns true if given level
// order traversal is Min Heap.
function isMinHeap(level)
{
    var n = level.length - 1;

    // First non leaf node is at
    // index (n/2-1). Check whether
    // each parent is greater than child
    for(var i = (n / 2 - 1) ; i >= 0 ; i--)
    {
        // Left child will be at index 2*i+1
        // Right child will be at index 2*i+2
        if (level[i] > level[2 * i + 1])
        {
            return false;
        }

        if (2 * i + 2 < n)
        {
            // If parent is greater than right child
            if (level[i] > level[2 * i + 2])
            {
            return false;
            }
        }
    }
    return true;
}

// Driver code
// Level order traversal
var level = [10, 15, 14, 25, 30];
if (isMinHeap(level))
{
    document.write("True");
}
else
{
    document.write("False");
}

</script>
```

**输出:**

```
True
```

这些算法在更糟糕的情况下运行 **O(n)** 复杂性
本文由 **Deepak Srivatsav** 提供。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。