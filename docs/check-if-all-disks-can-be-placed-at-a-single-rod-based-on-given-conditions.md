# 根据给定条件

检查所有圆盘是否可以放在一根杆上

> 原文:[https://www . geesforgeks . org/check-if-all-disks-can-at-single-rod-based-on-conditions/](https://www.geeksforgeeks.org/check-if-all-disks-can-be-placed-at-a-single-rod-based-on-given-conditions/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，该数组由表示 **N** 个杆的 **N** 个整数组成，每个杆都有一个半径为**arr【I】**的圆盘，任务是检查是否有可能将所有圆盘移动到单个杆，条件是**I<sup>th</sup>T13】杆处的圆盘只有在以下情况下才能移动到**j<sup>th</sup>T17】杆:****

*   [**ABS**](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)**(I–j)= 1**和 **i <sup>th</sup>** 棒只有一个单盘。
*   第一根 杆的盘面半径小于第一根杆或第一根杆的顶盘面半径为空。

**示例:**

> **输入:** arr[] = {1，3，5，2}，N = 4
> **输出:** YES
> **解释:**
> 可能的方法之一是:
> 首先将杆 2 处半径为 3 的圆盘移动到杆 3 的顶部。
> 数组 arr[]修改为{1，0，(5，3)，2}。
> 将杆 4 处半径为 2 的圆盘移到杆 3 的顶部。数组 arr[]修改为{1，0，(5，3，2)，0}。
> 将杆 1 处半径为 1 的圆盘移动到杆 2 的顶部。数组 arr[]修改为{0，1，(5，3，2)，0}。
> 现在，将杆 2 处半径为 1 的圆盘移到杆 3 的顶部。数组 arr[]修改为{0，0，(5，3，2，1)，0}。
> 
> **输入:** arr[] = {4，1，2}，N = 3
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:

> *   It can be observed that if there is an index **I** that makes **arr [I] < arr [I–1] and arr [I] < arr [I+1],** it is impossible to move all the disks on a single rod.
> *   Therefore, the task is simplified to find out whether there is any index **I** , so that **arr [I] < arr [I–1] and arr [I] < arr [I+1].**

按照以下步骤解决问题:

*   初始化一个变量，比如说**标志=假**，来存储数组中是否存在这样的索引。
*   [在索引**【1，N–2】**上遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。对于每个 **i** <sup>th</sup> 索引，检查**arr[I]<arr[I–1]和 arr[i] < arr[i + 1]** ，然后设置**标志=真**和[断开。](https://www.geeksforgeeks.org/break-statement-cc/)
*   如果**旗**为**假**，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to move all disks to a single rod
bool check(int a[], int n)
{
    // Stores if it is possible to move
    // all disks to a single rod
    bool flag = 0;

    // Traverse the array
    for (int i = 1; i < n - 1; i++) {

        // If i-th element is smaller than
        // both its adjacent elements
        if (a[i + 1] > a[i]
            && a[i] < a[i - 1])
            flag = 1;
    }

    // If flag is true
    if (flag)
        return false;

    // Otherwise
    else
        return true;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    if (check(arr, N))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG
{

// Function to check if it is possible
// to move all disks to a single rod
static boolean check(int a[], int n)
{

    // Stores if it is possible to move
    // all disks to a single rod
    boolean flag = false;

    // Traverse the array
    for (int i = 1; i < n - 1; i++)
    {

        // If i-th element is smaller than
        // both its adjacent elements
        if (a[i + 1] > a[i]
            && a[i] < a[i - 1])
            flag = true;
    }

    // If flag is true
    if (flag)
        return false;

    // Otherwise
    else
        return true;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 5, 2 };
    int N = arr.length;

    if (check(arr, N))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if it is possible
# to move all disks to a single rod
def check(a, n) :

    # Stores if it is possible to move
    # all disks to a single rod
    flag = 0

    # Traverse the array
    for i in range(1, n - 1):

        # If i-th element is smaller than
        # both its adjacent elements
        if (a[i + 1] > a[i]
            and a[i] < a[i - 1]) :
            flag = 1

    # If flag is true
    if (flag != 0) :
        return False

    # Otherwise
    else :
        return True

# Driver Code
arr = [ 1, 3, 5, 2 ]
N = len(arr)

if (check(arr, N) != 0):
    print("YES")
else :
    print("NO")

    # This code is contributed by splevel62.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

// Function to check if it is possible
// to move all disks to a single rod
static bool check(int[] a, int n)
{

    // Stores if it is possible to move
    // all disks to a single rod
    bool flag = false;

    // Traverse the array
    for (int i = 1; i < n - 1; i++)
    {

        // If i-th element is smaller than
        // both its adjacent elements
        if (a[i + 1] > a[i]
            && a[i] < a[i - 1])
            flag = true;
    }

    // If flag is true
    if (flag)
        return false;

    // Otherwise
    else
        return true;
}
  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 1, 3, 5, 2 };
    int N = arr.Length;

    if (check(arr, N))
        Console.Write("YES");
    else
        Console.Write("NO");
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to check if it is possible
// to move all disks to a single rod
function check(a , n)
{

    // Stores if it is possible to move
    // all disks to a single rod
    flag = false;

    // Traverse the array
    for (i = 1; i < n - 1; i++)
    {

        // If i-th element is smaller than
        // both its adjacent elements
        if (a[i + 1] > a[i]
            && a[i] < a[i - 1])
            flag = true;
    }

    // If flag is true
    if (flag)
        return false;

    // Otherwise
    else
        return true;
}

// Driver Code

var arr = [ 1, 3, 5, 2 ];
var N = arr.length;

if (check(arr, N))
    document.write("YES");
else
    document.write("NO");

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)