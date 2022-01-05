# 重新排列数组，使前缀和数组的乘积不为零

> 原文:[https://www . geeksforgeeks . org/rearray-array-make-积-前缀-和-array-非零/](https://www.geeksforgeeks.org/rearrange-array-to-make-product-of-prefix-sum-array-non-zero/)

给定一个大小为 **N** 的数组 **arr[ ]** ，任务是重新排列给定的数组，使其[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的所有元素的乘积不等于 **0** 。如果无法重新排列满足给定条件的数组，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，-1，-2，3}
> **输出:** 3 1 -1 -2
> **解释:**
> 将给定数组重新排列后的前缀和为{3，1，-1，-2}是{3，4，3，1}并乘积其前缀和数组的所有元素= (3 * 4 * 3 * 1) = 36。
> 因此，需要的数组是{3，1，-1，-2}
> 
> **输入:** arr = {1，1，-1，-1}
> **输出:** -1

**方法:**思路是[按照升序或降序对给定数组](https://www.geeksforgeeks.org/sort-in-python/)排序，使其前缀和的任何元素不等于 **0** 。按照以下步骤解决问题:

*   [计算给定数组的元素之和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)，比如**合计**。
*   如果**总计= 0** ，则打印 **-1** 。
*   如果 **totalSum > 0** 则按降序打印给定数组，使其前缀和的任何元素不等于 0。
*   如果 **totalSum < 0** 则按升序打印给定数组，使其前缀和的任何元素不等于 0。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print array elements
void printArr(int arr[], int N)
{
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Function to rearrange array
// that satisfies the given condition
void rearrangeArr(int arr[], int N)
{
    // Stores sum of elements
    // of the given array
    int totalSum = 0;

    // Calculate totalSum
    for (int i = 0; i < N; i++) {
        totalSum += arr[i];
    }

    // If the totalSum is equal to 0
    if (totalSum == 0) {

        // No possible way to
        // rearrange array
        cout << "-1" << endl;
    }

    // If totalSum exceeds 0
    else if (totalSum > 0) {

        // Rearrange the array
        // in descending order
        sort(arr, arr + N,
             greater<int>());
        printArr(arr, N);
    }

    // Otherwise
    else {

        // Rearrange the array
        // in ascending order
        sort(arr, arr + N);
        printArr(arr, N);
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, -1, -2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    rearrangeArr(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print array elements
static void printArr(int arr[], int N)
{
    for(int i = 0; i < N; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Function to rearrange array
// that satisfies the given condition
static void rearrangeArr(int arr[], int N)
{

    // Stores sum of elements
    // of the given array
    int totalSum = 0;

    // Calculate totalSum
    for(int i = 0; i < N; i++)
    {
        totalSum += arr[i];
    }

    // If the totalSum is equal to 0
    if (totalSum == 0)
    {

        // No possible way to
        // rearrange array
        System.out.print("-1" + "\n");
    }

    // If totalSum exceeds 0
    else if (totalSum > 0)
    {

        // Rearrange the array
        // in descending order
        Arrays.sort(arr);
        arr = reverse(arr);
        printArr(arr, N);
    }

    // Otherwise
    else
    {

        // Rearrange the array
        // in ascending order
        Arrays.sort(arr);
        printArr(arr, N);
    }
}

static int[] reverse(int a[])
{
    int i, n = a.length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, -1, -2, 3 };
    int N = arr.length;

    rearrangeArr(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to rearrange array
# that satisfies the given condition
def rearrangeArr(arr, N):

    # Stores sum of elements
    # of the given array
    totalSum = 0

    # Calculate totalSum
    for i in range(N):
        totalSum += arr[i]

    # If the totalSum is equal to 0
    if (totalSum == 0):

        # No possible way to
        # rearrange array
        print(-1)

    # If totalSum exceeds 0
    elif (totalSum > 0):

        # Rearrange the array
        # in descending order
        arr.sort(reverse = True)
        print(*arr, sep = ' ')

    # Otherwise
    else:

        # Rearrange the array
        # in ascending order
        arr.sort()
        print(*arr, sep = ' ')

# Driver Code
arr = [ 1, -1, -2, 3 ]
N = len(arr)

rearrangeArr(arr, N);

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print array elements
static void printArr(int []arr, int N)
{
    for(int i = 0; i < N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to rearrange array
// that satisfies the given condition
static void rearrangeArr(int []arr, int N)
{

    // Stores sum of elements
    // of the given array
    int totalSum = 0;

    // Calculate totalSum
    for(int i = 0; i < N; i++)
    {
        totalSum += arr[i];
    }

    // If the totalSum is equal to 0
    if (totalSum == 0)
    {

        // No possible way to
        // rearrange array
        Console.Write("-1" + "\n");
    }

    // If totalSum exceeds 0
    else if (totalSum > 0)
    {

        // Rearrange the array
        // in descending order
        Array.Sort(arr);
        arr = reverse(arr);
        printArr(arr, N);
    }

    // Otherwise
    else
    {

        // Rearrange the array
        // in ascending order
        Array.Sort(arr);
        printArr(arr, N);
    }
}

static int[] reverse(int []a)
{
    int i, n = a.Length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, -1, -2, 3 };
    int N = arr.Length;

    rearrangeArr(arr, N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to print array elements

function printArr(arr,  N)
{
    for(var i = 0; i < N; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Function to rearrange array
// that satisfies the given condition

  function rearrangeArr(arr, N)
{

    // Stores sum of elements
    // of the given array
    var totalSum = 0;

    // Calculate totalSum
    for(var i = 0; i < N; i++)
    {
        totalSum += arr[i];
    }

    // If the totalSum is equal to 0
    if (totalSum == 0)
    {

        // No possible way to
        // rearrange array
        document.write("-1" + "<br>");
    }

    // If totalSum exceeds 0
    else if (totalSum > 0)
    {

        // Rearrange the array
        // in descending order

        arr.sort(compare);
        arr = reverse(arr);
        printArr(arr, N);
    }

    // Otherwise
    else
    {

        // Rearrange the array
        // in ascending order
        arr.sort(compare);
        printArr(arr, N);
    }
}

function compare(a, b) {
    if (a < b) {
        return -1;
    } else if (a > b) {
        return 1;
    } else {
        return 0;
    }
}

  function reverse(a)
{
    var i, n = a.length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code

    var arr = [ 1, -1, -2, 3 ] ;
    var N = arr.length;

    rearrangeArr(arr, N);

</script>
```

**Output:** 

```
3 1 -1 -2
```

***时间复杂度:** O(N logN)*
***空间复杂度:** O(1)*