# 检查数组是否包含允许重复的连续整数

> 原文:[https://www . geesforgeks . org/check-if-array-contains-contact-integer-with-duplicates-allowed/](https://www.geeksforgeeks.org/check-if-array-contains-contiguous-integers-with-duplicates-allowed/)

给定一个由 **N** 个整数组成的数组 **Arr** (允许重复)。如果是一组连续的整数，则打印“是”，否则打印“否”。
**例:**

> **输入:** Arr = { 5，2，3，6，4，4，6，6 }
> **输出:** Yes
> 数组的元素组成一个连续的整数集合，该集合为{2，3，4，5，6 }，因此输出为 Yes。
> **输入:** Arr = { 10，14，10，12，12，13，15 }
> **输出:**否

**进场:**

1.  这里讨论了类似的方法。建议在继续阅读本文之前仔细阅读。
2.  从数组中找出最大和最小元素。
3.  用数组中最大元素的差值更新数组。
4.  遍历数组并执行以下操作
    *   如果**0<= ABS(arr[I])-1)<n**和**arr[ABS(arr[I])-1]>0**表示元素为正(第一次访问)，则通过执行**arr[ABS(arr[I])-1]=-arr[ABS(arr[I])-1]**将其设为负。
    *   否则继续循环意味着该值已被访问或超出数组范围
5.  再次遍历循环，检查是否有任何元素是正的，这意味着元素的差值大于 1
    断开循环并打印“否”
6.  如果没有发现阳性元素，打印“是”

下面是实现代码:

## C++

```
// C++ program to check if
// array contains contiguous
// integers with duplicates
// allowed in O(1) space
#include <bits/stdc++.h>
using namespace std;

// Function to return true or
// false
bool check(int arr[], int n)
{

    int k = INT_MIN;
    int r = INT_MAX;

    // To find the max and min
    // in the array
    for (int i = 0; i < n; i++) {
        k = max(k, arr[i]);
        r = min(r, arr[i]);
    }

    k += 1;

    // Update the array with
    // the difference from
    // the max element
    for (int i = 0; i < n; i++)
        arr[i] = k - arr[i];

    for (int i = 0; i < n; i++) {

        // if the element is positive
        // and less than the size of
        // array(in range), make it negative
        if (abs(arr[i]) - 1 < n
            && arr[abs(arr[i]) - 1] > 0) {
            arr[abs(arr[i]) - 1]
                = -arr[abs(arr[i]) - 1];
        }
    }

    int flag = 0;

    // Loop from 0 to end of the array
    for (int i = 0; i <= k - r - 1; i++) {

        // Found positive, out of range
        if (arr[i] > 0) {
            flag = 1;
            break;
        }
    }

    return flag == 0;
}

// Driver function
int main()
{

    // Given array
    int arr[] = { 5, 2, 3, 6, 4, 4, 6, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Calling
    if (check(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if array contains 
// contiguous integers with duplicates
// allowed in O(1) space
import java.util.*;

class GFG
{

// Function to return true or
// false
static boolean check(int arr[], int n)
{

    int k = Integer.MIN_VALUE;
    int r = Integer.MAX_VALUE;

    // To find the max and min
    // in the array
    for (int i = 0; i < n; i++)
    {
        k = Math.max(k, arr[i]);
        r = Math.min(r, arr[i]);
    }

    k += 1;

    // Update the array with
    // the difference from
    // the max element
    for (int i = 0; i < n; i++)
        arr[i] = k - arr[i];

    for (int i = 0; i < n; i++)
    {

        // if the element is positive
        // and less than the size of
        // array(in range), make it negative
        int abs_value = Math.abs(arr[i]);
        if (abs_value - 1 < n && 
        arr[abs_value - 1] > 0) 
        {
            arr[abs_value - 1] = -arr[abs_value - 1];
        }
    }

    int flag = 0;

    // Loop from 0 to end of the array
    for (int i = 0; i <= k - r - 1; i++)
    {

        // Found positive, out of range
        if (arr[i] > 0)
        {
            flag = 1;
            break;
        }
    }
    return flag == 0;
}

// Driver function
public static void main(String []args)
{

    // Given array
    int arr[] = { 5, 2, 3, 6, 4, 4, 6, 6 };
    int n = arr.length;

    // Function Calling
    if (check(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to check if array contains 
# contiguous integers with duplicates allowed 
# in O(1) space

# Function to return true or false
def check(arr, n):

    k = -10**9
    r = 10**9

    # To find the max and min in the array
    for i in range(n):
        k = max(k, arr[i])
        r = min(r, arr[i])

    k += 1

    # Update the array with the difference 
    # from the max element
    for i in range(n):
        arr[i] = k - arr[i]

    for i in range(n):

        # if the element is positive
        # and less than the size of
        # array(in range), make it negative
        if (abs(arr[i]) - 1 < n and 
                arr[abs(arr[i]) - 1] > 0):
            arr[abs(arr[i]) - 1]= -arr[abs(arr[i]) - 1]

    flag = 0

    # Loop from 0 to end of the array
    for i in range(k - r):

        # Found positive, out of range
        if (arr[i] > 0):
            flag = 1
            break

    return flag == 0

# Driver Code

# Given array
arr = [5, 2, 3, 6, 4, 4, 6, 6]
n = len(arr)

# Function Calling
if (check(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to check if array contains 
// contiguous integers with duplicates
// allowed in O(1) space
using System;

class GFG
{

// Function to return true or
// false
static bool check(int []arr, int n)
{
    int k = int.MinValue;
    int r = int.MaxValue;

    // To find the max and min
    // in the array
    for (int i = 0; i < n; i++)
    {
        k = Math.Max(k, arr[i]);
        r = Math.Min(r, arr[i]);
    }

    k += 1;

    // Update the array with
    // the difference from
    // the max element
    for (int i = 0; i < n; i++)
        arr[i] = k - arr[i];

    for (int i = 0; i < n; i++)
    {

        // if the element is positive
        // and less than the size of
        // array(in range), make it negative
        if (Math.Abs(arr[i]) - 1 < n && 
        arr[Math.Abs(arr[i]) - 1] > 0) 
        {
            arr[Math.Abs(arr[i]) - 1] = -
                         arr[Math.Abs(arr[i]) - 1];
        }
    }

    int flag = 0;

    // Loop from 0 to end of the array
    for (int i = 0; i <= k - r - 1; i++)
    {

        // Found positive, out of range
        if (arr[i] > 0)
        {
            flag = 1;
            break;
        }
    }
    return flag == 0;
}

// Driver Code
static public void Main ()
{

    // Given array
    int []arr = { 5, 2, 3, 6, 4, 4, 6, 6 };
    int n = arr.Length;

    // Function Calling
    if (check(arr, n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// Javascript program to check if
// array contains contiguous
// integers with duplicates
// allowed in O(1) space

// Function to return true or
// false
function check(arr, n)
{

    let k = Number.MIN_VALUE;
    let r = Number.MAX_VALUE;

    // To find the max and min
    // in the array
    for (let i = 0; i < n; i++) {
        k = Math.max(k, arr[i]);
        r = Math.min(r, arr[i]);
    }

    k += 1;

    // Update the array with
    // the difference from
    // the max element
    for (let i = 0; i < n; i++)
        arr[i] = k - arr[i];

    for (let i = 0; i < n; i++) {

        // if the element is positive
        // and less than the size of
        // array(in range), make it negative
        let abs_value = Math.abs(arr[i]);
        if (abs_value - 1 < n
            && arr[abs_value - 1] > 0) {
            arr[abs_value - 1]
                = -arr[abs_value - 1];
        }
    }

    let flag = 0;

    // Loop from 0 to end of the array
    for (let i = 0; i <= k - r - 1; i++) {

        // Found positive, out of range
        if (arr[i] > 0) {
            flag = 1;
            break;
        }
    }

    return flag == 0;
}

// Driver function

    // Given array
    let arr = [ 5, 2, 3, 6, 4, 4, 6, 6 ];
    let n = arr.length;

    // Function Calling
    if (check(arr, n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** ![O(N)   ](img/23f09f991be3459af525bfd21659fc83.png "Rendered by QuickLaTeX.com")
**空间复杂度:** ![O(1)   ](img/1bb3477242026f06b91f6eb1261c7ee9.png "Rendered by QuickLaTeX.com")额外空间