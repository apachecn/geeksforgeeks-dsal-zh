# 检查数组是否可以通过重新排列奇数和偶数索引元素来排序

> 原文:[https://www . geeksforgeeks . org/check-如果一个数组可以通过重新排列奇数和偶数索引元素进行排序，或者不进行排序/](https://www.geeksforgeeks.org/check-if-an-array-can-be-sorted-by-rearranging-odd-and-even-indexed-elements-or-not/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查是否可以使用以下操作对数组进行[排序:](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)

*   **交换(arr[i]，arr[j])** ，如果 **i & 1 = 1** 和 **j & 1 = 1** 。
*   **交换(arr[i]，arr[j])** ，如果 **i & 1 = 0** 和 **j & 1 = 0** 。

**示例:**

> **输入:** arr[] = {3，5，1，2，6}
> **输出:**是
> **解释:**
> 交换(3，1)–>{ 1，5，3，2，6}
> 交换(5，2)–>{ 1，2，3，5，6}
> 
> **输入:** arr[] = {3，1，5，2，6}
> 输出:否

**天真法:**思想是为偶数索引或奇数索引寻找最小元素，如果当前元素的索引分别为偶数或奇数，则从当前元素中交换。

*   [遍历阵列](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**并执行以下操作:
    *   如果当前指数为偶数，遍历剩余的偶数指数。
    *   找到偶数索引元素中的最小元素。
    *   用当前数组元素交换最小值。
*   对所有奇数索引元素也重复上述步骤。
*   完成上述操作后，如果对数组进行排序，则可以对数组进行排序。
*   否则，无法对数组进行排序。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check if array
// can be sorted or not
bool isSorted(int arr[], int n)
{
    for(int i = 0; i < n - 1; i++)
    {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Function to check if given
// array can be sorted or not
bool sortPoss(int arr[], int n)
{

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int idx = -1;
        int minVar = arr[i];

        // Traverse remaining elements
        // at indices separated by 2
        int j = i;

        while (j < n)
        {

            // If current element
            // is the minimum
            if (arr[j] < minVar)
            {
                minVar = arr[j];
                idx = j;
            }
            j = j + 2;
        }

        // If any smaller minimum exists
        if (idx != -1)
        {

            // Swap with current element
            swap(arr[i], arr[idx]);
        }
    }

    // If array is sorted
    if (isSorted(arr, n))
        return true;

    // Otherwise
    else
        return false;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 3, 5, 1, 2, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (sortPoss(arr, n))
        cout << "True";
      else
        cout << "False";

    return 0;
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// Function to check if array
// can be sorted or not
public static boolean isSorted(int arr[], int n)
{
    for(int i = 0; i < n - 1; i++)
    {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Function to check if given
// array can be sorted or not
public static boolean sortPoss(int arr[], int n)
{

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int idx = -1;
        int minVar = arr[i];

        // Traverse remaining elements
        // at indices separated by 2
        int j = i;

        while (j < n)
        {

            // If current element
            // is the minimum
            if (arr[j] < minVar)
            {
                minVar = arr[j];
                idx = j;
            }
            j = j + 2;
        }

        // If any smaller minimum exists
        if (idx != -1)
        {

            // Swap with current element
            int t;
            t = arr[i];
            arr[i] = arr[idx];
            arr[idx] = t;
        }
    }

    // If array is sorted
    if (isSorted(arr, n))
        return true;

    // Otherwise
    else
        return false;
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int arr[] = { 3, 5, 1, 2, 6 };
    int n = arr.length;

    if (sortPoss(arr, n))
        System.out.println("True");
      else
        System.out.println("False");
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Function to check if array
# can be sorted or not
def isSorted(arr):
  for i in range(len(arr)-1):
    if arr[i]>arr[i + 1]:
      return False
  return True

# Function to check if given
# array can be sorted or not
def sortPoss(arr):

  # Traverse the array
  for i in range(len(arr)):

    idx = -1
    minVar = arr[i]

    # Traverse remaining elements
    # at indices separated by 2
    for j in range(i, len(arr), 2):

      # If current element
      # is the minimum
      if arr[j]<minVar:

        minVar = arr[j]
        idx = j

    # If any smaller minimum exists
    if idx != -1:

      # Swap with current element
      arr[i], arr[idx] = arr[idx], arr[i]

  # If array is sorted
  if isSorted(arr):
    return True

  # Otherwise
  else:
    return False

# Driver Code

# Given array
arr = [ 3, 5, 1, 2, 6 ]

print(sortPoss(arr))
```

## C#

```
using System;

class GFG{

// Function to check if array
// can be sorted or not
public static bool isSorted(int[] arr, int n)
{
    for(int i = 0; i < n - 1; i++)
    {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Function to check if given
// array can be sorted or not
public static bool sortPoss(int[] arr, int n)
{

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int idx = -1;
        int minVar = arr[i];

        // Traverse remaining elements
        // at indices separated by 2
        int j = i;

        while (j < n)
        {

            // If current element
            // is the minimum
            if (arr[j] < minVar)
            {
                minVar = arr[j];
                idx = j;
            }
            j = j + 2;
        }

        // If any smaller minimum exists
        if (idx != -1)
        {

            // Swap with current element
            int t;
            t = arr[i];
            arr[i] = arr[idx];
            arr[idx] = t;
        }
    }

    // If array is sorted
    if (isSorted(arr, n))
        return true;

    // Otherwise
    else
        return false;
}

// Driver code
static public void Main()
{

    // Given array
    int[] arr = { 3, 5, 1, 2, 6 };
    int n = arr.Length;

    if (sortPoss(arr, n))
        Console.WriteLine("True");
    else
        Console.WriteLine("False");
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

    // Function to check if array
    // can be sorted or not
    function isSorted(arr , n) {
        for (i = 0; i < n - 1; i++) {
            if (arr[i] > arr[i + 1])
                return false;
        }
        return true;
    }

    // Function to check if given
    // array can be sorted or not
    function sortPoss(arr , n) {

        // Traverse the array
        for (i = 0; i < n; i++) {
            var idx = -1;
            var minVar = arr[i];

            // Traverse remaining elements
            // at indices separated by 2
            var j = i;

            while (j < n) {

                // If current element
                // is the minimum
                if (arr[j] < minVar) {
                    minVar = arr[j];
                    idx = j;
                }
                j = j + 2;
            }

            // If any smaller minimum exists
            if (idx != -1) {

                // Swap with current element
                var t;
                t = arr[i];
                arr[i] = arr[idx];
                arr[idx] = t;
            }
        }

        // If array is sorted
        if (isSorted(arr, n))
            return true;

        // Otherwise
        else
            return false;
    }

    // Driver Code

        // Given array
        var arr = [ 3, 5, 1, 2, 6 ];
        var n = arr.length;

        if (sortPoss(arr, n))
            document.write("True");
        else
            document.write("False");

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
True
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**这个想法是检查是否利用了这样一个事实，即我们可以按照我们想要使用交换操作的方式排列所有的偶数索引和奇数索引元素。

*   初始化一个数组，比如 **dupArr[]** ，来存储给定数组的内容。
*   对数组**和**进行排序。
*   检查原始数组中的所有偶数索引元素是否与**dupArr【】**中的偶数索引元素相同。
*   如果发现是真的，那么排序是可能的。否则，排序是不可能的。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to check if array can
# be sorted by given operations
def sortPoss(arr):

  # Copy contents
  # of the array
  dupArr = list(arr)

  # Sort the duplicate array
  dupArr.sort()

  evenOrg = []
  evenSort = []

  # Traverse the array
  for i in range(0, len(arr), 2):

    # Append even-indexed elements
    # of the original array
    evenOrg.append(arr[i])

    # Append even-indexed elements
    # of the duplicate array
    evenSort.append(dupArr[i])

  # Sort the even-indexed elements
  evenOrg.sort()
  evenSort.sort()

  # Return true if even-indexed
  # elements are identical
  return evenOrg == evenSort

# Driver Code

# Given array
arr = [3, 5, 1, 2, 6]

print(sortPoss(arr))
```

**Output:** 

```
True
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*