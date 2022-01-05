# 根据相邻元素的绝对差异对数组进行排序

> 原文:[https://www . geeksforgeeks . org/基于相邻元素绝对差的数组排序/](https://www.geeksforgeeks.org/sort-an-array-based-on-the-absolute-difference-of-adjacent-elements/)

给定一个包含 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是重新排列数组的所有元素，使得数组中连续元素之间的[绝对差按递增顺序排序。
**示例**](https://www.geeksforgeeks.org/absolute-difference-of-all-pairwise-consecutive-elements-in-an-array/) 

> **输入:** arr[] = { 5，-2，4，8，6，5 }
> **输出:** 5 5 6 4 8 -2
> **解释:**
> | 5–5 | = 0
> | 5–6 | = 1
> | 6–4 | = 2
> | 4–8 | = 4
> | 8 –(-2)| = 10
> 因此，相邻元素之间的差异被排序。
> **输入:** arr[] = { 8，1，4，2 }
> **输出:** 4 2 8 1
> **解释:**
> | 2–4 | = 2
> | 8–2 | = 6
> | 1–8 | = 7
> 因此，相邻元素之间的差异被排序。

**进场:**使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。我们知道[最大差异是在数组](https://www.geeksforgeeks.org/maximum-difference-between-two-elements-in-an-array/)的最小和最大元素之间。利用这个事实，如果我们在答案中包含一个最小元素，那么答案数组中包含的下一个元素将是最大元素，然后包含的第三个元素将是第二个最小元素，然后包含的第四个元素将是第二个最大元素，以此类推，将得到所需的数组。
以下是步骤:

1.  按递增顺序对给定数组 **arr[]** 进行排序。
2.  从排序后的数组中选择第一个最大值(比如说 **a** )和最小元素(比如说 **b** )并作为{a，b}插入到答案数组(比如说 **ans[]** )中。
3.  重复上述步骤，从排序的数组中选择第二、第三、第四…最大和最小元素，并将其插入到答案数组的前面。
4.  经过以上所有操作，答案数组得到了预期的结果。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that arrange the array such that
// all absolute difference between adjacent
// element are sorted
void sortedAdjacentDifferences(int arr[], int n)
{
    // To store the resultant array
    int ans[n];

    // Sorting the given array
    // in ascending order
    sort(arr + 0, arr + n);

    // Variable to represent left and right
    // ends of the given array
    int l = 0, r = n - 1;

    // Traversing the answer array in reverse
    // order and arrange the array elements from
    // arr[] in reverse order
    for (int i = n - 1; i >= 0; i--) {

        // Inserting elements in zig-zag manner
        if (i % 2) {
            ans[i] = arr[l];
            l++;
        }
        else {
            ans[i] = arr[r];
            r--;
        }
    }

    // Displaying the resultant array
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 5, -2, 4, 8, 6, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortedAdjacentDifferences(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function that arrange the array such that
// all absolute difference between adjacent
// element are sorted
static void sortedAdjacentDifferences(int arr[], int n)
{
    // To store the resultant array
    int []ans = new int[n];

    // Sorting the given array
    // in ascending order
    Arrays.sort(arr);

    // Variable to represent left and right
    // ends of the given array
    int l = 0, r = n - 1;

    // Traversing the answer array in reverse
    // order and arrange the array elements from
    // arr[] in reverse order
    for (int i = n - 1; i >= 0; i--) {

        // Inserting elements in zig-zag manner
        if (i % 2 == 1) {
            ans[i] = arr[l];
            l++;
        }
        else {
            ans[i] = arr[r];
            r--;
        }
    }

    // Displaying the resultant array
    for (int i = 0; i < n; i++) {
        System.out.print(ans[i]+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, -2, 4, 8, 6, 4, 5 };
    int n = arr.length;

    // Function Call
    sortedAdjacentDifferences(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that arrange the array such that
# all absolute difference between adjacent
# element are sorted
def sortedAdjacentDifferences(arr, n):

    # To store the resultant array
    ans = [0]*n

    # Sorting the given array
    # in ascending order
    arr = sorted(arr)

    # Variable to represent left and right
    # ends of the given array
    l = 0
    r = n - 1

    # Traversing the answer array in reverse
    # order and arrange the array elements from
    # arr[] in reverse order
    for i in range(n - 1, -1, -1):

        # Inserting elements in zig-zag manner
        if (i % 2):
            ans[i] = arr[l]
            l += 1
        else:
            ans[i] = arr[r]
            r -= 1

    # Displaying the resultant array
    for i in range(n):
        print(ans[i], end=" ")

# Driver Code
if __name__ == '__main__':
    arr=[5, -2, 4, 8, 6, 4, 5]
    n = len(arr)

    # Function Call
    sortedAdjacentDifferences(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function that arrange the array such that
    // all absolute difference between adjacent
    // element are sorted
    static void sortedAdjacentDifferences(int[] arr, int n)
    {
        // To store the resultant array
        int[] ans = new int[n];

        // Sorting the given array
        // in ascending order
        Array.Sort(arr);

        // Variable to represent left and right
        // ends of the given array
        int l = 0, r = n - 1;

        // Traversing the answer array in reverse
        // order and arrange the array elements from
        // arr[] in reverse order
        for (int i = n - 1; i >= 0; i--) {

            // Inserting elements in zig-zag manner
            if (i % 2 != 0) {
                ans[i] = arr[l];
                l++;
            }
            else {
                ans[i] = arr[r];
                r--;
            }
        }

        // Displaying the resultant array
        for (int i = 0; i < n; i++) {
            Console.Write(ans[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 5, -2, 4, 8, 6, 4, 5 };
        int n = arr.Length;

        // Function Call
        sortedAdjacentDifferences(arr, n);
    }
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function that arrange the array such that
// all absolute difference between adjacent
// element are sorted
function sortedAdjacentDifferences(arr, n)
{
    // To store the resultant array
    let ans = new Array(n);

    // Sorting the given array
    // in ascending order
    arr.sort();

    // Variable to represent left and right
    // ends of the given array
    let l = 0, r = n - 1;

    // Traversing the answer array in reverse
    // order and arrange the array elements from
    // arr[] in reverse order
    for (let i = n - 1; i >= 0; i--) {

        // Inserting elements in zig-zag manner
        if (i % 2) {
            ans[i] = arr[l];
            l++;
        }
        else {
            ans[i] = arr[r];
            r--;
        }
    }

    // Displaying the resultant array
    for (let i = 0; i < n; i++) {
        document.write(ans[i] + " ");
    }
}

// Driver Code
    let arr = [ 5, -2, 4, 8, 6, 4, 5 ];
    let n = arr.length;

    // Function Call
    sortedAdjacentDifferences(arr, n);

</script>
```

**Output:** 

```
5 4 5 4 6 -2 8
```

**时间复杂度:** O(N*log N)，其中 N 是给定数组中元素的个数。