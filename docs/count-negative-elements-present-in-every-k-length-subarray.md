# 计数每个 K 长度子阵列中存在的负元素

> 原文:[https://www . geesforgeks . org/count-negative-elements-present-in-ever-k-length-subarray/](https://www.geeksforgeeks.org/count-negative-elements-present-in-every-k-length-subarray/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是计算所有**K**-长度[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中出现的负元素数量。

**示例:**

> **输入:** arr[] = {-1，2，-2，3，5，-7，-5}，K = 3
> **输出:** 2 1 1 1 2
> **解释:**
> 第一斯巴莱:{-1，2，-2}。负数计数= 2。
> 第二辆斯巴瑞:{2，-2，3}。负数计数= 1。
> 第三斯巴瑞:{-2，3，5}。负数计数= 1。
> 第四斯巴莱:{3，5，-7}。负数计数= 1。
> 第五斯巴莱:{5，-7，-5}。负数计数= 2。
> 
> **输入:** arr[] = {-1，2，4，4}，K = 2
> T3】输出: 1 0 0

**天真法:**最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，考虑每个大小为 **K** 、**T7】的窗口，找出每个窗口中负数的个数。**

***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*

**高效方法:**这个问题可以使用[窗口滑动技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。按照以下步骤解决问题:

*   初始化一个变量**计数**为 **0** ，在一个大小为 **K** 的窗口中存储负元素的计数。
*   将两个变量 **i** 和 **j** 初始化为 **0** ，分别存储窗口的第一个和最后一个索引。
*   [循环同时](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **j < N** 并执行以下步骤:
    *   如果**将【j】<设置为 0** ，则将**计数**增加 1。
    *   如果窗口的大小，即 **j-i+1** 等于 **K** ，打印**计数**、**T7】的值，检查**是否为【I】<0**，然后将**计数**减 1。另外，将 **i** 增加 1。**
    *   将 **j** 的值增加 1。

下面是上述方法的实现

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the number of
// negative elements in every window
// of size K
void countNegative(vector<int> arr, int k)
{

    // Initialize the window pointers
    int i = 0;
    int j = 0;

    // Store the count of negative numbers
    int count = 0;
    int n = arr.size();

    // Traverse the array, arr[]
    while (j < n)
    {

        // Increase the count
        // if element is less then 0
        if (arr[j] < 0)
        {
            count++;
        }

        // If size of the window equal to k
        if (j - i + 1 == k)
        {
            cout << count << " ";

            // If the first element of
            // the window is less than 0,
            // decrement count by 1
            if (arr[i] < 0)
            {
                count--;
            }
            i++;
        }
        j++;
    }
}

// Driver Code
int main()
{

    // Given Input
    vector<int> arr{ -1, 2, -2, 3, 5, -7, -5 };
    int k = 3;

    // Function Call
    countNegative(arr, k);
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to count the number of
    // negative elements in every window
    // of size K
    public static void countNegative(int[] arr, int k)
    {
        // Initialize the window pointers
        int i = 0;
        int j = 0;

        // Store the count of negative numbers
        int count = 0;
        int n = arr.length;

        // Traverse the array, arr[]
        while (j < n) {

            // Increase the count
            // if element is less then 0
            if (arr[j] < 0) {
                count++;
            }

            // If size of the window equal to k
            if (j - i + 1 == k) {
                System.out.print(count + " ");

                // If the first element of
                // the window is less than 0,
                // decrement count by 1
                if (arr[i] < 0) {
                    count--;
                }
                i++;
            }

            j++;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int[] arr = { -1, 2, -2, 3, 5, -7, -5 };
        int k = 3;

        // Function Call
        countNegative(arr, k);
    }
}
```

## 蟒蛇 3

```
# Function to count the number of
# negative elements in every window
# of size K
def countNegative(arr,k):

    # Initialize the window pointers
    i = 0
    j = 0

    # Store the count of negative numbers
    count = 0
    n = len(arr)

    while(j < n):

        # Increase the count
        # if element is less then 0

        if (arr[j] < 0):
            count = count + 1

        # If size of the window equal to k  
        if (j - i + 1 == k):
            print(count,end=" ")

            # If the first element of
            # the window is less than 0,
            # decrement count by 1

            if(arr[i] < 0):
                count = count - 1

            i = i+1
        j = j+1

# Driver Code

# Given Input
arr = [-1, 2, -2, 3, 5, -7, -5]
k = 3
countNegative(arr, k)

# This code is contributed by abhinavjain194.
```

## C#

```
// C#  program for the above approach
using System;

class GFG{

// Function to count the number of
// negative elements in every window
// of size K
public static void countNegative(int[] arr, int k)
{

    // Initialize the window pointers
    int i = 0;
    int j = 0;

    // Store the count of negative numbers
    int count = 0;
    int n = arr.Length;

    // Traverse the array, arr[]
    while (j < n)
    {

        // Increase the count
        // if element is less then 0
        if (arr[j] < 0)
        {
            count++;
        }

        // If size of the window equal to k
        if (j - i + 1 == k)
        {
            Console.Write(count + " ");

            // If the first element of
            // the window is less than 0,
            // decrement count by 1
            if (arr[i] < 0)
            {
                count--;
            }
            i++;
        }
        j++;
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given Input
    int[] arr = { -1, 2, -2, 3, 5, -7, -5 };
    int k = 3;

    // Function Call
    countNegative(arr, k);
}
}    

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number of
// negative elements in every window
// of size K
function countNegative(arr, k)
{

    // Initialize the window pointers
    var i = 0;
    var j = 0;

    // Store the count of negative numbers
    var count = 0;
    var n = arr.length;

    // Traverse the array, arr[]
    while (j < n)
    {

        // Increase the count
        // if element is less then 0
        if (arr[j] < 0)
        {
            count++;
        }

        // If size of the window equal to k
        if (j - i + 1 == k)
        {
            document.write( count + " ");

            // If the first element of
            // the window is less than 0,
            // decrement count by 1
            if (arr[i] < 0)
            {
                count--;
            }
            i++;
        }
        j++;
    }
}

var arr = [ -1, 2, -2, 3, 5, -7, -5 ];
var k = 3;

// Function Call
countNegative(arr, k);

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2 1 1 1 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)