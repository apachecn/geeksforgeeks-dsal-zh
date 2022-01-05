# 检查移除不相邻元素的子序列是否会使数组排序

> 原文:[https://www . geeksforgeeks . org/check-if-移除非相邻元素的子序列-使数组排序/](https://www.geeksforgeeks.org/check-if-removal-of-a-subsequence-of-non-adjacent-elements-makes-the-array-sorted/)

给定大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查数组 **arr[]** 是否可以通过移除任何不相邻数组元素的子序列来排序。如果数组可以排序，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {1，0，1，0，1，0}
> **输出:**是
> **解释:**
> 移除索引{1，3，6}处的元素将给定的数组修改为{1，1，1，1}，并进行排序。因此，打印“是”。
> 
> **输入:** arr[] = {0，1，1，0，0}
> **输出:**否

**天真方法:**解决给定问题最简单的方法是[生成所有可能的非相邻元素的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，如果存在任何移除[对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序的子序列，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:当且仅当相邻索引 **i** 和 **i + 1** 处存在两个连续的 **1s** 并且相邻索引 **j** 和 **j + 1** 处存在两个连续的 **0s** 时，数组不能排序，使得 **(j > i)** 。按照以下步骤解决问题:

*   初始化一个变量，如果[在数组](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)中有两个连续的 **1s** ，就说 **idx** 为 **-1** 存储索引。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果数组中存在任意两个连续的 **1s** ，则将该索引存储在变量 **idx** 和[中，断开循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将所有 **1s** 从数组中移除，并对数组进行排序，打印**“是”**。
*   如果 **idx** 的值是**-1”**，那么像往常一样打印“是”，从数组中移除所有的 **1s** 使数组排序。
*   否则，从索引 **idx** 再次遍历数组，如果存在两个连续的 **0s** ，则打印并[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将所有 **0s** 从数组中移除，并对数组进行排序，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to sort the array or not
void isPossibleToSort(int arr[], int N)
{
    // Stores the index if there are two
    // consecutive 1's in the array
    int idx = -1;

    // Traverse the given array
    for (int i = 1; i < N; i++) {

        // Check adjacent same elements
        // having values 1s
        if (arr[i] == 1
            && arr[i - 1] == 1) {
            idx = i;
            break;
        }
    }

    // If there are no two consecutive
    // 1s, then always remove all the
    // 1s from array & make it sorted
    if (idx == -1) {
        cout << "YES";
        return;
    }

    for (int i = idx + 1; i < N; i++) {

        // If two consecutive 0's are
        // present after two consecutive
        // 1's then array can't be sorted
        if (arr[i] == 0 && arr[i - 1] == 0) {
            cout << "NO";
            return;
        }
    }

    // Otherwise, print Yes
    cout << "YES";
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 1, 0, 1, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    isPossibleToSort(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to check if it is possible
    // to sort the array or not
    static void isPossibleToSort(int arr[], int N)
    {
        // Stores the index if there are two
        // consecutive 1's in the array
        int idx = -1;

        // Traverse the given array
        for (int i = 1; i < N; i++) {

            // Check adjacent same elements
            // having values 1s
            if (arr[i] == 1 && arr[i - 1] == 1) {
                idx = i;
                break;
            }
        }

        // If there are no two consecutive
        // 1s, then always remove all the
        // 1s from array & make it sorted
        if (idx == -1) {
            System.out.println("YES");
            return;
        }

        for (int i = idx + 1; i < N; i++) {

            // If two consecutive 0's are
            // present after two consecutive
            // 1's then array can't be sorted
            if (arr[i] == 0 && arr[i - 1] == 0) {
                System.out.println("NO");
                return;
            }
        }

        // Otherwise, print Yes
        System.out.println("YES");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 0, 1, 0, 1, 1, 0 };
        int N = arr.length;
        isPossibleToSort(arr, N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to sort the array or not
def isPossibleToSort(arr, N):

    # Stores the index if there are two
    # consecutive 1's in the array
    idx = -1

    # Traverse the given array
    for i in range(1, N):

        # Check adjacent same elements
        # having values 1s
        if (arr[i] == 1 and arr[i - 1] == 1):
            idx = i
            break

    # If there are no two consecutive
    # 1s, then always remove all the
    # 1s from array & make it sorted
    if (idx == -1):
        print("YES")
        return

    for i in range(idx + 1, N, 1):

        # If two consecutive 0's are
        # present after two consecutive
        # 1's then array can't be sorted
        if (arr[i] == 0 and arr[i - 1] == 0):
            print("NO")
            return

    # Otherwise, print Yes
    print("YES")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 0, 1, 0, 1, 1, 0 ]
    N = len(arr)

    isPossibleToSort(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# for the above approach
using System.IO;
using System;

class GFG{

// Function to check if it is possible
// to sort the array or not
static void isPossibleToSort(int[] arr, int N)
{

    // Stores the index if there are two
    // consecutive 1's in the array
    int idx = -1;

    // Traverse the given array
    for(int i = 1; i < N; i++)
    {

        // Check adjacent same elements
        // having values 1s
        if (arr[i] == 1 && arr[i - 1] == 1)
        {
            idx = i;
            break;
        }
    }

    // If there are no two consecutive
    // 1s, then always remove all the
    // 1s from array & make it sorted
    if (idx == -1)
    {
        Console.WriteLine("YES");
        return;
    }

    for(int i = idx + 1; i < N; i++)
    {

        // If two consecutive 0's are
        // present after two consecutive
        // 1's then array can't be sorted
        if (arr[i] == 0 && arr[i - 1] == 0)
        {
            Console.WriteLine("NO");
            return;
        }
    }

    // Otherwise, print Yes
    Console.WriteLine("YES");
}

// Driver code
static void Main()
{
    int[] arr = { 1, 0, 1, 0, 1, 1, 0 };
    int N = arr.Length;

    isPossibleToSort(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if it is possible
// to sort the array or not
function isPossibleToSort(arr, N)
{
    // Stores the index if there are two
    // consecutive 1's in the array
    var idx = -1;

    var i;
    // Traverse the given array
    for (i = 1; i < N; i++) {

        // Check adjacent same elements
        // having values 1s
        if (arr[i] == 1
            && arr[i - 1] == 1) {
            idx = i;
            break;
        }
    }

    // If there are no two consecutive
    // 1s, then always remove all the
    // 1s from array & make it sorted
    if (idx == -1) {
        document.write("YES");
        return;
    }

    for (i = idx + 1; i < N; i++) {

        // If two consecutive 0's are
        // present after two consecutive
        // 1's then array can't be sorted
        if (arr[i] == 0 && arr[i - 1] == 0) {
            document.write("NO");
            return;
        }
    }

    // Otherwise, print Yes
    document.write("YES");
}

// Driver Code
    var arr = [1, 0, 1, 0, 1, 1, 0];
    var N = arr.length;
    isPossibleToSort(arr, N);

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)