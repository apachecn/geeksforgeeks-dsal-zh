# 在连续数字的排序数组中查找缺失的元素

> 原文:[https://www . geeksforgeeks . org/find-连续数字排序数组中缺少元素/](https://www.geeksforgeeks.org/find-missing-element-in-a-sorted-array-of-consecutive-numbers/)

给定一个由 **n** 个不同整数组成的数组 **arr[]** 。元素按升序排列，缺少一个元素。任务是找到丢失的元素。
**例:**

> **输入:** arr[] = {1，2，4，5，6，7，8，9}
> **输出:** 3
> **输入:** arr[] = {-4，-3，-1，0，1，2}
> **输出:** -2
> **输入:** arr[] = {1，2，3，4}
> **输出:** -1
> No

**原则:**

> *   **Looking for inconsistency:** Ideally, the difference between any element and its index must be **arr [0]** of each element.
>     **Examples** ,
>     A [] = {1,2,3,4,5}-> Consistent
>     B [] = {101,102,103,104}-> Consistent
>     = C[0] means 4–2! = 1
>     
> *   Discovering inconsistencies helps to scan only half of the array in O(logN) at a time.

**算法**

> 1.  Find the middle element and check whether it is consistent.
> 2.  If the middle element is consistent, check whether the difference between the middle element and its next element is greater than 1, that is, check **arr [mid+1]–arr [mid] > 1**
>     *   If so, arr[mid]+1 is a missing element.
>     *   If not, then we have to scan the right half array from the middle element and skip to step -1.
> 3.  If the middle elements are inconsistent, check whether the difference between the middle element and its previous element is greater than 1, that is, check **arr [mid]–arr [mid–1] > 1**
>     *   If so, then arr [mid]–1 is the missing element.
>     *   If not, then we will scan the left half array from the middle element and skip to step -1.

以下是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the missing element
int findMissing(int arr[], int n)
{

    int l = 0, h = n - 1;
    int mid;

    while (h > l)
    {

        mid = l + (h - l) / 2;

        // Check if middle element is consistent
        if (arr[mid] - mid == arr[0])
        {

            // No inconsistency till middle elements
            // When missing element is just after
            // the middle element
            if (arr[mid + 1] - arr[mid] > 1)
                return arr[mid] + 1;
            else
            {
                // Move right
                l = mid + 1;
            }
        }
        else
        {

            // Inconsistency found
            // When missing element is just before
            // the middle element
            if (arr[mid] - arr[mid - 1] > 1)
                return arr[mid] - 1;
            else
            {
                // Move left
                h = mid - 1;
            }
        }
    }

    // No missing element found
    return -1;
}

// Driver code
int main()
{
    int arr[] = { -9, -8, -7, -5, -4, -3, -2, -1, 0 };
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << (findMissing(arr, n));
}

// This code iscontributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the missing element
    public static int findMissing(int arr[], int n)
    {

        int l = 0, h = n - 1;
        int mid;

        while (h > l) {

            mid = l + (h - l) / 2;

            // Check if middle element is consistent
            if (arr[mid] - mid == arr[0]) {

                // No inconsistency till middle elements
                // When missing element is just after
                // the middle element
                if (arr[mid + 1] - arr[mid] > 1)
                    return arr[mid] + 1;
                else {

                    // Move right
                    l = mid + 1;
                }
            }
            else {

                // Inconsistency found
                // When missing element is just before
                // the middle element
                if (arr[mid] - arr[mid - 1] > 1)
                    return arr[mid] - 1;
                else {

                    // Move left
                    h = mid - 1;
                }
            }
        }

        // No missing element found
        return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { -9, -8, -7, -5, -4, -3, -2, -1, 0 };
        int n = arr.length;

        System.out.print(findMissing(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the missing element
def findMissing(arr, n):

    l, h = 0, n - 1
    mid = 0

    while (h > l):

        mid = l + (h - l) // 2

        # Check if middle element is consistent
        if (arr[mid] - mid == arr[0]):

            # No inconsistency till middle elements
            # When missing element is just after
            # the middle element
            if (arr[mid + 1] - arr[mid] > 1):
                return arr[mid] + 1
            else:

                # Move right
                l = mid + 1

        else:

            # Inconsistency found
            # When missing element is just before
            # the middle element
            if (arr[mid] - arr[mid - 1] > 1):
                return arr[mid] - 1
            else:

                # Move left
                h = mid - 1

    # No missing element found
    return -1

# Driver code
arr = [-9, -8, -7, -5, -4, -3, -2, -1, 0 ]
n = len(arr)

print(findMissing(arr, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the missing element
    public static int findMissing(int[] arr, int n)
    {

        int l = 0, h = n - 1;
        int mid;

        while (h > l)
        {

            mid = l + (h - l) / 2;

            // Check if middle element is consistent
            if (arr[mid] - mid == arr[0])
            {

                // No inconsistency till middle elements
                // When missing element is just after
                // the middle element
                if (arr[mid + 1] - arr[mid] > 1)
                    return arr[mid] + 1;
                else
                {

                    // Move right
                    l = mid + 1;
                }
            }
            else
            {

                // Inconsistency found
                // When missing element is just before
                // the middle element
                if (arr[mid] - arr[mid - 1] > 1)
                    return arr[mid] - 1;
                else
                {

                    // Move left
                    h = mid - 1;
                }
            }
        }

        // No missing element found
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { -9, -8, -7, -5, -4, -3, -2, -1, 0 };
        int n = arr.Length;

        Console.WriteLine(findMissing(arr, n));
    }
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the missing element
function findMissing($arr, $n)
{
    $l = 0; $h = $n - 1;

    while ($h > $l)
    {

        $mid = floor($l + ($h - $l) / 2);

        // Check if middle element is consistent
        if ($arr[$mid] - $mid == $arr[0])
        {

            // No inconsistency till middle elements
            // When missing element is just after
            // the middle element
            if ($arr[$mid + 1] - $arr[$mid] > 1)
                return $arr[$mid] + 1;
            else
            {

                // Move right
                $l = $mid + 1;
            }
        }
        else
        {

            // Inconsistency found
            // When missing element is just before
            // the middle element
            if ($arr[$mid] - $arr[$mid - 1] > 1)
                return $arr[$mid] - 1;
            else
            {

                // Move left
                $h = $mid - 1;
            }
        }
    }

    // No missing element found
    return -1;
}

// Driver code
$arr = array( -9, -8, -7, -5, -
               4, -3, -2, -1, 0 );
$n = count($arr);

echo findMissing($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to return the missing element
function findMissing(arr, n)
{

    let l = 0, h = n - 1;
    let mid;

    while (h > l)
    {

        mid = l + Math.floor((h - l) / 2);

        // Check if middle element is consistent
        if (arr[mid] - mid == arr[0])
        {

            // No inconsistency till middle elements
            // When missing element is just after
            // the middle element
            if (arr[mid + 1] - arr[mid] > 1)
                return arr[mid] + 1;
            else
            {
                // Move right
                l = mid + 1;
            }
        }
        else
        {

            // Inconsistency found
            // When missing element is just before
            // the middle element
            if (arr[mid] - arr[mid - 1] > 1)
                return arr[mid] - 1;
            else
            {
                // Move left
                h = mid - 1;
            }
        }
    }

    // No missing element found
    return -1;
}

// Driver code
    let arr = [ -9, -8, -7, -5, -4, -3, -2, -1, 0 ];
    let n = arr.length;

    document.write(findMissing(arr, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
-6
```

**时间复杂度:** O(log(N) )
**辅助空间:** O(1)