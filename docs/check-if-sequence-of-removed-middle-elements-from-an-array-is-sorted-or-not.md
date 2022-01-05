# 检查从数组中移除的中间元素的顺序是否排序

> 原文:[https://www . geesforgeks . org/check-if-sequence-of-removed-in-elements-from-a-array-sorted-or-not/](https://www.geeksforgeeks.org/check-if-sequence-of-removed-middle-elements-from-an-array-is-sorted-or-not/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查从给定数组 **arr[]** 中重复删除中间元素形成的数字序列是否排序。如果有两个[中间元件](https://www.geeksforgeeks.org/start-end-start2-preferrable-method-calculating-middle-array-start-end2/)，则移除其中任何一个。

**示例:**

> **输入:** arr[] = {4，3，1，2，5}
> **输出:**是
> **说明:**
> 元素移除顺序为:
> 数组中间元素= arr[2]。移除 arr[2]会将数组修改为{4，3，2，5}。
> 数组的中间元素是 arr[1]和 arr[2]。移除 arr[2]会将数组修改为{4，3，5}。
> 数组的中间元素是 arr[1]。移除 arr[1]会将数组修改为{4，5}。
> 同样，arr[0]和 arr[1]从数组中移除。
> 最后去掉数组元素的顺序是{1，2，3，4，5}，排序。
> 
> **输入:** arr[] = {5，4，1，2，3}
> 输出:否

**天真方法:**解决给定问题的最简单方法是使用[递归](https://www.geeksforgeeks.org/recursion/)来生成数组元素移除的每个可能组合。对于有两个中间元素的实例，需要进行两次递归调用，一次考虑 **N / 2 <sup>第</sup>元素**，另一次考虑 **(N / 2 + 1) <sup>第</sup>元素**。完成递归后，检查任何递归调用形成的数组是否排序。如果发现属实，则打印“**是**”。否则，打印**“否”**。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于这样的观察进行优化，即数组末尾的元素需要大于所有数组元素，才能得到排序越来越多的数组。
按照以下步骤解决问题:

*   初始化一个变量，用**“是”**表示**和**，检查所需的序列是否可以排序。
*   初始化[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)，说 **L** 为**0****R**为**(N–1)**，存储数组的开始和结束索引。
*   重复直到 **L** 小于 **R** ，并执行以下步骤:
    *   如果 **arr[L]** 的值大于或等于 **arr[L + 1]** 和**arr[R–1]**的最大值，且 **arr[R]** 的值大于或等于 **arr[L + 1]** 和**arr[R–1]**的最小值，则将 **L** 的值增加 **1** 和
    *   否则，将 **ans** 的值更新为**“否”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if sequence of
// removed middle elements from an
// array is sorted or not
bool isSortedArray(int arr[], int n)
{
    // Points to the ends
    // of the array
    int l = 0, r = (n - 1);

    // Iterate l + 1 < r
    while ((l + 1) < r) {

        // If the element at index L and
        // R is greater than (L + 1)-th
        // and (R - 1)-th elements
        if (arr[l] >= max(arr[l + 1],
                          arr[r - 1])
            && arr[r] >= max(arr[r - 1],
                             arr[l + 1])) {

            // If true, then decrement R
            // by 1 and increment L by 1
            l++;
            r--;
        }

        // Otherwise, return false
        else {
            return false;
        }
    }

    // If an increasing sequence is
    // formed, then return true
    return true;
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 1, 2, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    if (isSortedArray(arr, N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if sequence of
// removed middle elements from an
// array is sorted or not
static boolean isSortedArray(int []arr, int n)
{

    // Points to the ends
    // of the array
    int l = 0, r = (n - 1);

    // Iterate l + 1 < r
    while ((l + 1) < r)
    {

        // If the element at index L and
        // R is greater than (L + 1)-th
        // and (R - 1)-th elements
        if (arr[l] >= Math.max(arr[l + 1],
                               arr[r - 1]) &&
            arr[r] >= Math.max(arr[r - 1],
                               arr[l + 1]))
        {

            // If true, then decrement R
            // by 1 and increment L by 1
            l++;
            r--;
        }

        // Otherwise, return false
        else
        {
            return false;
        }
    }

    // If an increasing sequence is
    // formed, then return true
    return true;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 4, 3, 1, 2, 5 };
    int N = arr.length;

    if (isSortedArray(arr, N))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if sequence of
# removed middle elements from an
# array is sorted or not
def isSortedArray(arr, n):

    # Points toa the ends
    # of the array
    l = 0
    r = (n - 1)

    # Iterate l + 1 < r
    while ((l + 1) < r):

        # If the element at index L and
        # R is greater than (L + 1)-th
        # and (R - 1)-th elements
        if (arr[l] >= max(arr[l + 1],
                          arr[r - 1])
            and arr[r] >= max(arr[r - 1],
                              arr[l + 1])):

            # If true, then decrement R
            # by 1 and increment L by 1
            l += 1
            r -= 1

        # Otherwise, return false
        else:
            return False

    # If an increasing sequence is
    # formed, then return true
    return True

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 3, 1, 2, 5 ]
    N = len(arr)

    if (isSortedArray(arr, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if sequence of removed
// middle elements from an array is sorted or not
static bool isSortedArray(int []arr, int n)
{

    // Points to the ends
    // of the array
    int l = 0, r = (n - 1);

    // Iterate l + 1 < r
    while ((l + 1) < r)
    {

        // If the element at index L and
        // R is greater than (L + 1)-th
        // and (R - 1)-th elements
        if (arr[l] >= Math.Max(arr[l + 1],
                               arr[r - 1]) &&
            arr[r] >= Math.Max(arr[r - 1],
                               arr[l + 1]))
        {

            // If true, then decrement R
            // by 1 and increment L by 1
            l++;
            r--;
        }

        // Otherwise, return false
        else
        {
            return false;
        }
    }

    // If an increasing sequence is
    // formed, then return true
    return true;
}

// Driver Code
public static void Main(string[] args)
{
    int []arr = { 4, 3, 1, 2, 5 };
    int N = arr.Length;

    if (isSortedArray(arr, N))
       Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
// JavaScript program for the above approach

// Function to check if sequence of
// removed middle elements from an
// array is sorted or not
function isSortedArray(arr, n){

    // Points toa the ends
    // of the array
    var l = 0
    var r = (n - 1)

    // Iterate l + 1 < r
    while ((l + 1) < r) {

        // If the element at index L and
        // R is greater than (L + 1)-th
        // and (R - 1)-th elements
        if (arr[l] >= Math.max(arr[l + 1],
                          arr[r - 1])
            && arr[r] >= Math.max(arr[r - 1],
            arr[l + 1])){

            // If true, then decrement R
            // by 1 and increment L by 1
            l += 1
            r -= 1
    }

        // Otherwise, return false
        else
            return false
    }

    // If an increasing sequence is
    // formed, then return true
    return true
}

// Driver Code

var arr = [ 4, 3, 1, 2, 5 ]
var N = arr.length

if (isSortedArray(arr, N))
      console.log("Yes")
else
      console.log("No")

// This code is contributed by AnkThon
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)