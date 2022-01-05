# 检查等面积的 N 个矩形是否可以由(4 * N)个整数构成

> 原文:[https://www . geeksforgeeks . org/check-if-n-等面积矩形可由-4-n-整数构成/](https://www.geeksforgeeks.org/check-if-n-rectangles-of-equal-area-can-be-formed-from-4-n-integers/)

给定一个整数 **N** 和一个大小为 **4 * N** 的数组**arr【】**，任务是检查如果每个元素只能使用一次，是否可以由这个数组形成面积相等的 **N** 矩形。

**示例:**

> **输入:** arr[] = {1，8，2，1，2，4，4，8}，N = 2
> **输出:**是
> 可以形成边长为(1，8，1，8)和(2，4，2，4)的两个矩形。
> 这两个矩形面积相同。
> 
> **输入:** arr[] = {1，3，3，5，5，7，1，6}，N = 2
> **输出:**否

**进场:**

*   形成一个矩形需要四条边。
*   给定 **4 * N** 个整数，最多 **N** 个矩形只能用数字组成一次。
*   任务是检查所有矩形的面积是否相同。为了检查这一点，首先对数组进行排序。
*   边被认为是前两个元素和后两个元素。
*   如果面积与最初计算的面积相同，则计算并检查面积。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether we can make n
// rectangles of equal area
bool checkRectangles(int* arr, int n)
{
    bool ans = true;

    // Sort the array
    sort(arr, arr + 4 * n);

    // Find the area of any one rectangle
    int area = arr[0] * arr[4 * n - 1];

    // Check whether we have two equal sides
    // for each rectangle and that area of
    // each rectangle formed is the same
    for (int i = 0; i < 2 * n; i = i + 2) {
        if (arr[i] != arr[i + 1]
            || arr[4 * n - i - 1] != arr[4 * n - i - 2]
            || arr[i] * arr[4 * n - i - 1] != area) {

            // Update the answer to false
            // if any condition fails
            ans = false;
            break;
        }
    }

    // If possible
    if (ans)
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 8, 2, 1, 2, 4, 4, 8 };
    int n = 2;

    if (checkRectangles(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to check whether we can make n
// rectangles of equal area
static boolean checkRectangles(int[] arr, int n)
{
    boolean ans = true;

    // Sort the array
    Arrays.sort(arr);

    // Find the area of any one rectangle
    int area = arr[0] * arr[4 * n - 1];

    // Check whether we have two equal sides
    // for each rectangle and that area of
    // each rectangle formed is the same
    for (int i = 0; i < 2 * n; i = i + 2)
    {
        if (arr[i] != arr[i + 1] ||
            arr[4 * n - i - 1] != arr[4 * n - i - 2] ||
            arr[i] * arr[4 * n - i - 1] != area)
        {

            // Update the answer to false
            // if any condition fails
            ans = false;
            break;
        }
    }

    // If possible
    if (ans)
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 8, 2, 1, 2, 4, 4, 8 };
    int n = 2;

    if (checkRectangles(arr, n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to check whether we can make n
# rectangles of equal area
def checkRectangles(arr, n):
    ans = True

    # Sort the array
    arr.sort()

    # Find the area of any one rectangle
    area = arr[0] * arr[4 * n - 1]

    # Check whether we have two equal sides
    # for each rectangle and that area of
    # each rectangle formed is the same
    for i in range(0, 2 * n, 2):
        if (arr[i] != arr[i + 1]
            or arr[4 * n - i - 1] != arr[4 * n - i - 2]
            or arr[i] * arr[4 * n - i - 1] != area):

            # Update the answer to false
            # if any condition fails
            ans = False
            break

    # If possible
    if (ans):
        return True

    return False

# Driver code
arr = [ 1, 8, 2, 1, 2, 4, 4, 8 ]
n = 2

if (checkRectangles(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to check whether we can make n
// rectangles of equal area
static bool checkRectangles(int[] arr, int n)
{
    bool ans = true;

    // Sort the array
    Array.Sort(arr);

    // Find the area of any one rectangle
    int area = arr[0] * arr[4 * n - 1];

    // Check whether we have two equal sides
    // for each rectangle and that area of
    // each rectangle formed is the same
    for (int i = 0; i < 2 * n; i = i + 2)
    {
        if (arr[i] != arr[i + 1] ||
            arr[4 * n - i - 1] != arr[4 * n - i - 2] ||
            arr[i] * arr[4 * n - i - 1] != area)
        {

            // Update the answer to false
            // if any condition fails
            ans = false;
            break;
        }
    }

    // If possible
    if (ans)
        return true;

    return false;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 8, 2, 1, 2, 4, 4, 8 };
    int n = 2;

    if (checkRectangles(arr, n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check whether we can make n
// rectangles of equal area
function checkRectangles(arr, n)
{
    let ans = true;

    // Sort the array
    arr.sort();

    // Find the area of any one rectangle
    var area = arr[0] * arr[4 * n - 1];

    // Check whether we have two equal sides
    // for each rectangle and that area of
    // each rectangle formed is the same
    for(let i = 0; i < 2 * n; i = i + 2)
    {
        if (arr[i] != arr[i + 1] ||
            arr[4 * n - i - 1] !=
            arr[4 * n - i - 2] ||
            arr[i] * arr[4 * n - i - 1] != area)
        {

            // Update the answer to false
            // if any condition fails
            ans = false;
            break;
        }
    }

    // If possible
    if (ans)
        return true;

    return false;
}

// Driver code
var arr = [ 1, 8, 2, 1, 2, 4, 4, 8 ];
var n = 2;

if (checkRectangles(arr, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```