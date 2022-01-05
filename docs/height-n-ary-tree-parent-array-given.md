# 给定父数组时 n 元树的高度

> 原文:[https://www . geesforgeks . org/height-n-ary-tree-parent-array-given/](https://www.geeksforgeeks.org/height-n-ary-tree-parent-array-given/)

给定一个父数组 P，其中 P[i]表示树中第 I 个节点的父节点(假设根节点 id 的父节点用-1 表示)。找到树的高度。

**示例:**

```
Input : array[] = [-1 0 1 6 6 0 0 2 7]
Output : height = 5
Tree formed is: 
                     0
                   / | \
                  5  1  6
                    /   | \
                   2    4  3
                  /
                 7
                /
               8   
```

1.从每个节点开始，一直到它的父节点，直到我们到达-1。
2。此外，跟踪所有节点之间的最大高度。

## C++

```
// C++ program to find the height of the generic
// tree(n-ary tree) if parent array is given
#include <bits/stdc++.h>
using namespace std;

// function to find the height of tree
int findHeight(int* parent, int n)
{
    int res = 0;

    // Traverse each node
    for (int i = 0; i < n; i++) {

        // traverse to parent until -1
        // is reached
        int p = i, current = 1;
        while (parent[p] != -1) {
            current++;
            p = parent[p];
        }

        res = max(res, current);
    }
    return res;
}

// Driver program
int main()
{
    int parent[] = { -1, 0, 1, 6, 6, 0, 0, 2, 7 };
    int n = sizeof(parent) / sizeof(parent[0]);
    int height = findHeight(parent, n);
    cout << "Height of the given tree is: "
         << height << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the height of
// the generic tree(n-ary tree) if
// parent array is given
import java.io.*;

public class GFG {

    // function to find the height of tree
    static int findHeight(int[] parent, int n)
    {
        int res = 0;

        // Traverse each node
        for (int i = 0; i < n; i++) {

            // traverse to parent until -1
            // is reached
            int p = i, current = 1;
            while (parent[p] != -1) {
                current++;
                p = parent[p];
            }

            res = Math.max(res, current);
        }
        return res;
    }

    // Driver program
    static public void main(String[] args)
    {
        int[] parent = { -1, 0, 1, 6, 6, 0,
                         0, 2, 7 };
        int n = parent.length;

        int height = findHeight(parent, n);

        System.out.println("Height of the "
                           + "given tree is: " + height);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to find the height of the generic
# tree(n-ary tree) if parent array is given

# function to find the height of tree
def findHeight(parent, n):

    res = 0

    # Traverse each node
    for i in range(n):            
        # traverse to parent until -1
        # is reached
        p = i
        current = 1
        while (parent[p] != -1):
            current+= 1
            p = parent[p]
        res = max(res, current)
    return res

# Driver code
if __name__ == '__main__':
    parent = [-1, 0, 1, 6, 6, 0, 0, 2, 7]
    n = len(parent)
    height = findHeight(parent, n)
    print("Height of the given tree is:", height)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find the height of
// the generic tree(n-ary tree) if
// parent array is given
using System;

public class GFG {

    // function to find the height of tree
    static int findHeight(int[] parent, int n)
    {
        int res = 0;

        // Traverse each node
        for (int i = 0; i < n; i++) {

            // traverse to parent until -1
            // is reached
            int p = i, current = 1;
            while (parent[p] != -1) {
                current++;
                p = parent[p];
            }

            res = Math.Max(res, current);
        }

        return res;
    }

    // Driver program
    static public void Main()
    {
        int[] parent = { -1, 0, 1, 6, 6, 0,
                         0, 2, 7 };
        int n = parent.Length;

        int height = findHeight(parent, n);

        Console.WriteLine("Height of the "
                          + "given tree is: " + height);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to find the height of
// the generic tree(n-ary tree) if
// parent array is given

    // function to find the height of tree
    function findHeight(parent,n)
    {
        let res = 0;

        // Traverse each node
        for (let i = 0; i < n; i++) {

            // traverse to parent until -1
            // is reached
            let p = i, current = 1;
            while (parent[p] != -1) {
                current++;
                p = parent[p];
            }

            res = Math.max(res, current);
        }
        return res;
    }

    // Driver program
    let parent=[-1, 0, 1, 6, 6, 0,
                         0, 2, 7];

    let n = parent.length;

    let height = findHeight(parent, n);

    document.write("Height of the "
                   + "given tree is: " + height);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Height of the given tree is: 5
```