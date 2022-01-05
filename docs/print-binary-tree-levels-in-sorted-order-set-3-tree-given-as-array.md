# 按排序顺序打印二叉树级别|集合 3(作为数组给出的树)

> 原文:[https://www . geesforgeks . org/print-二叉树-级别-按排序-集合-3-树-给定为数组/](https://www.geeksforgeeks.org/print-binary-tree-levels-in-sorted-order-set-3-tree-given-as-array/)

给定一个[完整二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)作为数组，任务是按排序顺序打印它的所有级别。
**例:**

```
Input: arr[] = {7, 6, 5, 4, 3, 2, 1}
The given tree looks like
            7
          /   \
        6      5
       / \    / \
      4  3   2   1
Output:
7
5 6
1 2 3 4

Input: arr[] = {5, 6, 4, 9, 2, 1}
The given tree looks like 
            5
          /   \
        6      4
       / \    /    
      9   2  1
Output: 
5
4 6
1 2 9
```

**方法:**这里讨论了一个类似的问题
因为给定的树是一个[完全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/) :

```
No. of nodes at a level l will be 2l where l ≥ 0
```

1.  开始遍历级别初始化为 0 的数组。
2.  [对属于当前级别的元素进行排序](https://www.geeksforgeeks.org/sort-c-stl/)并打印元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the levels
// of the given tree in sorted order
void printSortedLevels(int arr[], int n)
{

    // Initialize level with 0
    int level = 0;
    for (int i = 0; i < n; level++) {

        // Number of nodes at current level
        int cnt = (int)pow(2, level);

        // Indexing of array starts from 0
        // so subtract no. of nodes by 1
        cnt -= 1;

        // Index of the last node in the current level
        int j = min(i + cnt, n - 1);

        // Sort the nodes of the current level
        sort(arr + i, arr + j + 1);

        // Print the sorted nodes
        while (i <= j) {
            cout << arr[i] << " ";
            i++;
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 4, 9, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printSortedLevels(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function to print all the levels
// of the given tree in sorted order
static void printSortedLevels(int arr[], int n)
{

    // Initialize level with 0
    int level = 0;
    for (int i = 0; i < n; level++)
    {

        // Number of nodes at current level
        int cnt = (int)Math.pow(2, level);

        // Indexing of array starts from 0
        // so subtract no. of nodes by 1
        cnt -= 1;

        // Index of the last node in the current level
        int j = Math.min(i + cnt, n - 1);

        // Sort the nodes of the current level
        Arrays.sort(arr, i, j+1);

        // Print the sorted nodes
        while (i <= j)
        {
            System.out.print(arr[i] + " ");
            i++;
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 4, 9, 2, 1 };
    int n = arr.length;
    printSortedLevels(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import pow

# Function to print all the levels
# of the given tree in sorted order
def printSortedLevels(arr, n):

    # Initialize level with 0
    level = 0
    i = 0
    while(i < n):

        # Number of nodes at current level
        cnt = int(pow(2, level))

        # Indexing of array starts from 0
        # so subtract no. of nodes by 1
        cnt -= 1

        # Index of the last node in the current level
        j = min(i + cnt, n - 1)

        # Sort the nodes of the current level
        arr = arr[:i] + sorted(arr[i:j + 1]) + \
                               arr[j + 1:]

        # Print the sorted nodes
        while (i <= j):
            print(arr[i], end = " ")
            i += 1
        print()
        level += 1

# Driver code
arr = [ 5, 6, 4, 9, 2, 1]
n = len(arr)
printSortedLevels(arr, n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;                

class GFG
{

// Function to print all the levels
// of the given tree in sorted order
static void printSortedLevels(int []arr, int n)
{

    // Initialize level with 0
    int level = 0;
    for (int i = 0; i < n; level++)
    {

        // Number of nodes at current level
        int cnt = (int)Math.Pow(2, level);

        // Indexing of array starts from 0
        // so subtract no. of nodes by 1
        cnt -= 1;

        // Index of the last node in the current level
        int j = Math.Min(i + cnt, n - 1);

        // Sort the nodes of the current level
        Array.Sort(arr, i, j + 1 - i);

        // Print the sorted nodes
        while (i <= j)
        {
            Console.Write(arr[i] + " ");
            i++;
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 6, 4, 9, 2, 1 };
    int n = arr.Length;
    printSortedLevels(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to sort the elements of the array
    // from index a to index b
    function partSort(arr, N, a, b)
    {
        // Variables to store start and end of the index range
        let l = Math.min(a, b);
        let r = Math.max(a, b);

        // Temporary array
        let temp = new Array(r - l + 1);
        temp.fill(0);
        let j = 0;
        for (let i = l; i <= r; i++) {
            temp[j] = arr[i];
            j++;
        }

        // Sort the temporary array
        temp.sort(function(a, b){return a - b});

        // Modifying original array with temporary array elements
        j = 0;
        for (let i = l; i <= r; i++) {
            arr[i] = temp[j];
            j++;
        }
    }

    // Function to print all the levels
    // of the given tree in sorted order
    function printSortedLevels(arr, n)
    {

        // Initialize level with 0
        let level = 0;
        for (let i = 0; i < n; level++)
        {

            // Number of nodes at current level
            let cnt = Math.pow(2, level);

            // Indexing of array starts from 0
            // so subtract no. of nodes by 1
            cnt -= 1;

            // Index of the last node in the current level
            let j = Math.min(i + cnt, n - 1);

            // Sort the nodes of the current level
            partSort(arr, n, i, j + 1);

            // Print the sorted nodes
            while (i <= j)
            {
                document.write(arr[i] + " ");
                i++;
            }
            document.write("</br>");
        }
    }

    let arr = [ 5, 6, 4, 9, 2, 1 ];
    let n = arr.length;
    printSortedLevels(arr, n);

</script>
```

**Output:** 

```
5 
4 6 
1 2 9
```