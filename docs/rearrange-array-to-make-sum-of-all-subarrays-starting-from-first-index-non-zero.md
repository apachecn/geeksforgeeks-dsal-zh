# 重新排列数组，使从第一个索引开始的所有子数组之和不为零

> 原文:[https://www . geesforgeks . org/rearray-数组到所有子数组的和-从第一个索引开始-非零/](https://www.geeksforgeeks.org/rearrange-array-to-make-sum-of-all-subarrays-starting-from-first-index-non-zero/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是重新排列数组，使得从数组的第一个索引开始的所有子数组的[和为**非零**。如果无法生成这样的排列，则打印**-1”**。](https://www.geeksforgeeks.org/sum-of-all-subarrays/)

**示例:**

> **输入:** arr[] = {-1，1，-2，3}
> **输出:** {-1，-2，1，3}
> **解释:**可能的重排之一是{-1，-2，1，3}。
> 从索引 0 开始的子阵分别为{-1}、{-1、-2}、{-1、-2、1}和{-1、-2、1、3}。上面的子阵列都没有 sum 0。
> 
> **输入:** arr[] = {0，0，0，0}
> **输出:** -1

**方法:**如果给定阵列处于以下两种配置中的任何一种，则可以从给定阵列中获得所需阵列:

*   如果[给定数组按升序排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)，则可以通过将子数组的最后一个元素替换为大于它的元素来处理求和为零的第一个子数组。
*   类似地，在按降序排序的[数组中](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)，通过用一个小于它的元素替换求和零的子数组的第一个元素，以确保其后的和为负。

按照以下步骤解决问题:

1.  **数组按升序排序时:**
    *   [对数组 **arr[]** 进行升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)求数组前 I 个元素的和(0 ≤ i ≤ N)。
    *   遇到零和时，用数组中最大的元素替换使前缀和无效的元素(即第<sup>个</sup>元素):
        *   如果数组的[最大元素等于导致无效的整数，则移动到第二个配置。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
        *   如果最大的元素大于有问题的元素，这种替换将确保正和而不是零。
2.  **数组按降序排序时:**
    *   [对数组 **arr[]** 进行降序排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)开始寻找数组最后 I 个元素的和(0 ≤ i ≤ N)。
    *   遇到零和时，用数组的最小元素替换使前缀和无效的元素(即第<sup>个</sup>元素):
        *   如果数组的[最小元素等于导致无效的整数，则不可能重新排列数组 arr[]。](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)
        *   如果最小的元素小于有问题的元素，这种替换将确保负和而不是零。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array such
// that sum of all elements of subarrays
// from the 1st index is non-zero
void rearrangeArray(int a[], int N)
{
    // Initialize sum of subarrays
    int sum = 0;

    // Sum of all elements of array
    for (int i = 0; i < N; i++) {

        sum += a[i];
    }

    // If sum is 0, the required
    // array could never be formed
    if (sum == 0) {
        cout << "-1";
        return;
    }

    // If sum is non zero, array
    // might be formed
    sum = 0;

    int b = 0;

    // Sort array in ascending order
    sort(a, a + N);

    for (int i = 0; i < N; i++) {
        sum += a[i];

        // When current subarray sum
        // becomes 0 replace it with
        // the largest element
        if (sum == 0) {

            if (a[i] != a[N - 1]) {

                sum -= a[i];

                // Swap Operation
                swap(a[i], a[N - 1]);
                sum += a[i];
            }

            // If largest element is same
            // as element to be replaced,
            // then rearrangement impossible
            else {
                b = 1;
                break;
            }
        }
    }

    // If b = 1, then rearrangement
    // is not possible. Hence check
    // with reverse configuration
    if (b == 1) {

        b = 0;
        sum = 0;

        // Sort array in descending order
        sort(a, a + N, greater<int>());

        // When current subarray sum
        // becomes 0 replace it with
        // the smallest element
        for (int i = N - 1; i >= 0; i--) {

            sum += a[i];
            if (sum == 0) {
                if (a[i] != a[0]) {
                    sum -= a[i];

                    // Swap Operation
                    swap(a[i], a[0]);
                    sum += a[i];
                }

                // If smallest element is same
                // as element to be replaced,
                // then rearrangement impossible
                else {
                    b = 1;
                    break;
                }
            }
        }
    }

    // If neither of the configurations
    // worked then print "-1"
    if (b == 1) {
        cout << "-1";
        return;
    }

    // Otherwise, print the formed
    // rearrangement
    for (int i = 0; i < N; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, -1, 2, 4, 0 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    rearrangeArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.util.Arrays;
import java.util.Collections;

class GFG{

// Function to rearrange the array such
// that sum of all elements of subarrays
// from the 1st index is non-zero
static void rearrangeArray(int a[], int N)
{

    // Initialize sum of subarrays
    int sum = 0;

    // Sum of all elements of array
    for(int i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // If sum is 0, the required
    // array could never be formed
    if (sum == 0)
    {
        System.out.print("-1");
        return;
    }

    // If sum is non zero, array
    // might be formed
    sum = 0;

    int b = 0;

    // Sort array in ascending order
    Arrays.sort(a);

    for(int i = 0; i < N; i++)
    {
        sum += a[i];

        // When current subarray sum
        // becomes 0 replace it with
        // the largest element
        if (sum == 0)
        {
            if (a[i] != a[N - 1])
            {
                sum -= a[i];

                // Swap Operation
                int temp = a[i];
                a[i] = a[N - 1];
                a[N - 1] = temp;
                sum += a[i];
            }

            // If largest element is same
            // as element to be replaced,
            // then rearrangement impossible
            else
            {
                b = 1;
                break;
            }
        }
    }

    // If b = 1, then rearrangement
    // is not possible. Hence check
    // with reverse configuration
    if (b == 1)
    {
        b = 0;
        sum = 0;

        // Sort array in descending order
        Arrays.sort(a);

        // When current subarray sum
        // becomes 0 replace it with
        // the smallest element
        for(int i = N - 1; i >= 0; i--)
        {
            sum += a[i];
            if (sum == 0)
            {
                if (a[i] != a[0])
                {
                    sum -= a[i];

                    // Swap Operation
                    int temp = a[i];
                    a[i] = a[0];
                    a[0] = temp;
                    sum += a[i];
                }

                // If smallest element is same
                // as element to be replaced,
                // then rearrangement impossible
                else
                {
                    b = 1;
                    break;
                }
            }
        }
    }

    // If neither of the configurations
    // worked then print "-1"
    if (b == 1)
    {
        System.out.print("-1" + " ");
        return;
    }

    // Otherwise, print the formed
    // rearrangement
    for(int i = 0; i < N; i++)
    {
        System.out.print(a[i] + " ");
    }
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int arr[] = { 1, -1, 2, 4, 0 };

    // Size of array
    int N = arr.length;

    // Function Call
    rearrangeArray(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rearrange the array such
# that sum of all elements of subarrays
# from the 1st index is non-zero
def rearrangeArray(a, N):

    # Initialize sum of subarrays
    sum = 0

    # Sum of all elements of array
    for i in range(N):
        sum += a[i]

    # If sum is 0, the required
    # array could never be formed
    if (sum == 0):
        print("-1")
        return

    # If sum is non zero, array
    # might be formed
    sum = 0

    b = 0

    # Sort array in ascending order
    a = sorted(a)

    for i in range(N):
        sum += a[i]

        # When current subarray sum
        # becomes 0 replace it with
        # the largest element
        if (sum == 0):
            if (a[i] != a[N - 1]):
                sum -= a[i]

                # Swap Operation
                a[i], a[N - 1] = a[N - 1], a[i]
                sum += a[i]

            # If largest element is same
            # as element to be replaced,
            # then rearrangement impossible
            else:
                b = 1
                break

    # If b = 1, then rearrangement
    # is not possible. Hence check
    # with reverse configuration
    if (b == 1):
        b = 0
        sum = 0

        # Sort array in descending order
        a = sorted(a)
        a = a[::-1]

        # When current subarray sum
        # becomes 0 replace it with
        # the smallest element
        for i in range(N - 1, -1, -1):
            sum += a[i]

            if (sum == 0):
                if (a[i] != a[0]):
                    sum -= a[i]

                    # Swap Operation
                    a[i], a[0] = a[0], a[i]
                    sum += a[i]

                # If smallest element is same
                # as element to be replaced,
                # then rearrangement impossible
                else:
                    b = 1
                    break

    # If neither of the configurations
    # worked then pr"-1"
    if (b == 1):
        print("-1")
        return

    # Otherwise, print the formed
    # rearrangement
    for i in range(N):
        print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, -1, 2, 4, 0 ]

    # Size of array
    N = len(arr)

    # Function Call
    rearrangeArray(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to rearrange the array such
// that sum of all elements of subarrays
// from the 1st index is non-zero
static void rearrangeArray(int [] a, int N)
{

    // Initialize sum of subarrays
    int sum = 0;

    // Sum of all elements of array
    for(int i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // If sum is 0, the required
    // array could never be formed
    if (sum == 0)
    {
        Console.Write("-1");
        return;
    }

    // If sum is non zero, array
    // might be formed
    sum = 0;

    int b = 0;

    // Sort array in ascending order
    Array.Sort(a);

    for(int i = 0; i < N; i++)
    {
        sum += a[i];

        // When current subarray sum
        // becomes 0 replace it with
        // the largest element
        if (sum == 0)
        {
            if (a[i] != a[N - 1])
            {
                sum -= a[i];

                // Swap Operation
                int temp = a[i];
                a[i] = a[N - 1];
                a[N - 1] = temp;
                sum += a[i];
            }

            // If largest element is same
            // as element to be replaced,
            // then rearrangement impossible
            else
            {
                b = 1;
                break;
            }
        }
    }

    // If b = 1, then rearrangement
    // is not possible. Hence check
    // with reverse configuration
    if (b == 1)
    {
        b = 0;
        sum = 0;

        // Sort array in descending order
        Array.Sort(a);

        // When current subarray sum
        // becomes 0 replace it with
        // the smallest element
        for(int i = N - 1; i >= 0; i--)
        {
            sum += a[i];
            if (sum == 0)
            {
                if (a[i] != a[0])
                {
                    sum -= a[i];

                    // Swap Operation
                    int temp = a[i];
                    a[i] = a[0];
                    a[0] = temp;
                    sum += a[i];
                }

                // If smallest element is same
                // as element to be replaced,
                // then rearrangement impossible
                else
                {
                    b = 1;
                    break;
                }
            }
        }
    }

    // If neither of the configurations
    // worked then print "-1"
    if (b == 1)
    {
        Console.Write("-1" + " ");
        return;
    }

    // Otherwise, print the formed
    // rearrangement
    for(int i = 0; i < N; i++)
    {
        Console.Write(a[i] + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given array
    int[] arr = { 1, -1, 2, 4, 0 };

    // Size of array
    int N = arr.Length;

    // Function Call
    rearrangeArray(arr, N);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to rearrange the array such
// that sum of all elements of subarrays
// from the 1st index is non-zero
function rearrangeArray(a, N)
{

    // Initialize sum of subarrays
    let sum = 0;

    // Sum of all elements of array
    for(let i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // If sum is 0, the required
    // array could never be formed
    if (sum == 0)
    {
        document.write("-1");
        return;
    }

    // If sum is non zero, array
    // might be formed
    sum = 0;

    let b = 0;

    // Sort array in ascending order
    a.sort();

    for(let i = 0; i < N; i++)
    {
        sum += a[i];

        // When current subarray sum
        // becomes 0 replace it with
        // the largest element
        if (sum == 0)
        {
            if (a[i] != a[N - 1])
            {
                sum -= a[i];

                // Swap Operation
                let temp = a[i];
                a[i] = a[N - 1];
                a[N - 1] = temp;
                sum += a[i];
            }

            // If largest element is same
            // as element to be replaced,
            // then rearrangement impossible
            else
            {
                b = 1;
                break;
            }
        }
    }

    // If b = 1, then rearrangement
    // is not possible. Hence check
    // with reverse configuration
    if (b == 1)
    {
        b = 0;
        sum = 0;

        // Sort array in descending order
        a.sort();

        // When current subarray sum
        // becomes 0 replace it with
        // the smallest element
        for(let i = N - 1; i >= 0; i--)
        {
            sum += a[i];
            if (sum == 0)
            {
                if (a[i] != a[0])
                {
                    sum -= a[i];

                    // Swap Operation
                    let temp = a[i];
                    a[i] = a[0];
                    a[0] = temp;
                    sum += a[i];
                }

                // If smallest element is same
                // as element to be replaced,
                // then rearrangement impossible
                else
                {
                    b = 1;
                    break;
                }
            }
        }
    }

    // If neither of the configurations
    // worked then print "-1"
    if (b == 1)
    {
        document.write("-1" + " ");
        return;
    }

    // Otherwise, print the formed
    // rearrangement
    for(let i = 0; i < N; i++)
    {
        document.write(a[i] + " ");
    }
}

// Driver Code

    // Given array
    let arr = [ 1, -1, 2, 4, 0 ];

    // Size of array
    let N = arr.length;

    // Function Call
    rearrangeArray(arr, N);

</script>
```

**Output:** 

```
-1 0 4 2 1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*