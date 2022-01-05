# 检查数组是否被排序和旋转

> 原文:[https://www . geeksforgeeks . org/check-如果数组被排序和旋转/](https://www.geeksforgeeks.org/check-if-an-array-is-sorted-and-rotated/)

给定 N 个不同整数的数组。任务是编写一个程序来检查这个数组是否被排序和逆时针旋转。已排序的数组不被视为已排序和旋转的数组，即至少应该有一次旋转。
**例** :

```
Input : arr[] = { 3, 4, 5, 1, 2 }
Output : YES
The above array is sorted and rotated.
Sorted array: {1, 2, 3, 4, 5}. 
Rotating this sorted array clockwise 
by 3 positions, we get: { 3, 4, 5, 1, 2}

Input: arr[] = {7, 9, 11, 12, 5}
Output: YES

Input: arr[] = {1, 2, 3}
Output: NO

Input: arr[] = {3, 4, 6, 1, 2, 5}
Output: NO
```

**接近** :

*   找到数组中的最小元素。
*   现在，如果对数组进行排序，然后旋转最小元素之前的所有元素，最小元素之后的所有元素也将按递增顺序排列。
*   检查最小元素之前的所有元素是否按升序排列。
*   检查最小元素后的所有元素是否按递增顺序排列。
*   检查数组的最后一个元素是否小于起始元素。
*   如果以上三个条件都满足，则打印**是**否则打印**否**。

以下是上述思路的实现:

## C++

```
// CPP program to check if an array is
// sorted and rotated clockwise
#include <climits>
#include <iostream>

using namespace std;

// Function to check if an array is
// sorted and rotated clockwise
void checkIfSortRotated(int arr[], int n)
{
    int minEle = INT_MAX;
    int maxEle = INT_MIN;

    int minIndex = -1;

    // Find the minimum element
    // and it's index
    for (int i = 0; i < n; i++) {
        if (arr[i] < minEle) {
            minEle = arr[i];
            minIndex = i;
        }
    }

    int flag1 = 1;

    // Check if all elements before minIndex
    // are in increasing order
    for (int i = 1; i < minIndex; i++) {
        if (arr[i] < arr[i - 1]) {
            flag1 = 0;
            break;
        }
    }

    int flag2 = 1;

    // Check if all elements after minIndex
    // are in increasing order
    for (int i = minIndex + 1; i < n; i++) {
        if (arr[i] < arr[i - 1]) {
            flag2 = 0;
            break;
        }
    }

    // Check if last element of the array
    // is smaller than the element just
    // starting element of the array
    // for arrays like [3,4,6,1,2,5] - not circular array
    if (flag1 && flag2 && (arr[n - 1] < arr[0]))
        cout << "YES";
    else
        cout << "NO";
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 5, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    checkIfSortRotated(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if an
// array is sorted and rotated
// clockwise
import java.io.*;

class GFG {

    // Function to check if an array is
    // sorted and rotated clockwise
    static void checkIfSortRotated(int arr[], int n)
    {
        int minEle = Integer.MAX_VALUE;
        int maxEle = Integer.MIN_VALUE;

        int minIndex = -1;

        // Find the minimum element
        // and it's index
        for (int i = 0; i < n; i++) {
            if (arr[i] < minEle) {
                minEle = arr[i];
                minIndex = i;
            }
        }

        boolean flag1 = true;

        // Check if all elements before
        // minIndex are in increasing order
        for (int i = 1; i < minIndex; i++) {
            if (arr[i] < arr[i - 1]) {
                flag1 = false;
                break;
            }
        }

        boolean flag2 = true;

        // Check if all elements after
        // minIndex are in increasing order
        for (int i = minIndex + 1; i < n; i++) {
            if (arr[i] < arr[i - 1]) {
                flag2 = false;
                break;
            }
        }

        // check if the minIndex is 0, i.e the first element
        // is the smallest , which is the case when array is
        // sorted but not rotated.
        if (minIndex == 0) {
            System.out.print("NO");
            return;
        }
        // Check if last element of the array
        // is smaller than the element just
        // before the element at minIndex
        // starting element of the array
        // for arrays like [3,4,6,1,2,5] - not sorted
        // circular array
        if (flag1 && flag2 && (arr[n - 1] < arr[0]))
            System.out.println("YES");
        else
            System.out.print("NO");
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 4, 5, 1, 2 };

        int n = arr.length;

        // Function Call
        checkIfSortRotated(arr, n);
    }
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python3 program to check if an
# array is sorted and rotated clockwise
import sys

# Function to check if an array is
# sorted and rotated clockwise

def checkIfSortRotated(arr, n):
    minEle = sys.maxsize
    maxEle = -sys.maxsize - 1
    minIndex = -1

    # Find the minimum element
    # and it's index
    for i in range(n):
        if arr[i] < minEle:
            minEle = arr[i]
            minIndex = i
    flag1 = 1

    # Check if all elements before
    # minIndex are in increasing order
    for i in range(1, minIndex):
        if arr[i] < arr[i - 1]:
            flag1 = 0
            break
    flag2 = 2

    # Check if all elements after
    # minIndex are in increasing order
    for i in range(minIndex + 1, n):
        if arr[i] < arr[i - 1]:
            flag2 = 0
            break

    # Check if last element of the array
    # is smaller than the element just
    # before the element at minIndex
    # starting element of the array
    # for arrays like [3,4,6,1,2,5] - not sorted circular array
    if (flag1 and flag2 and
            arr[n - 1] < arr[0]):
        print("YES")
    else:
        print("NO")

# Driver code
arr = [3, 4, 5, 1, 2]
n = len(arr)

# Function Call
checkIfSortRotated(arr, n)

# This code is contributed
# by Shrikant13
```

## C#

```
// C# program to check if an
// array is sorted and rotated
// clockwise
using System;

class GFG {

    // Function to check if an array is
    // sorted and rotated clockwise
    static void checkIfSortRotated(int[] arr, int n)
    {
        int minEle = int.MaxValue;
        // int maxEle = int.MinValue;

        int minIndex = -1;

        // Find the minimum element
        // and it's index
        for (int i = 0; i < n; i++) {
            if (arr[i] < minEle) {
                minEle = arr[i];
                minIndex = i;
            }
        }

        bool flag1 = true;

        // Check if all elements before
        // minIndex are in increasing order
        for (int i = 1; i < minIndex; i++) {
            if (arr[i] < arr[i - 1]) {
                flag1 = false;
                break;
            }
        }

        bool flag2 = true;

        // Check if all elements after
        // minIndex are in increasing order
        for (int i = minIndex + 1; i < n; i++) {
            if (arr[i] < arr[i - 1]) {
                flag2 = false;
                break;
            }
        }

        // Check if last element of the array
        // is smaller than the element just
        // before the element at minIndex
        // starting element of the array
        // for arrays like [3,4,6,1,2,5] - not circular
        // array
        if (flag1 && flag2 && (arr[n - 1] < arr[0]))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 3, 4, 5, 1, 2 };

        int n = arr.Length;

          // Function Call
        checkIfSortRotated(arr, n);
    }
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if an
// array is sorted and rotated
// clockwise

// Function to check if an array
// is sorted and rotated clockwise
function checkIfSortRotated($arr, $n)
{
    $minEle = PHP_INT_MAX;
    $maxEle = PHP_INT_MIN;

    $minIndex = -1;

    // Find the minimum element
    // and it's index
    for ($i = 0; $i <$n; $i++)
    {
        if ($arr[$i] < $minEle)
        {
            $minEle = $arr[$i];
            $minIndex = $i;
        }
    }

    $flag1 = 1;

    // Check if all elements before
    // minIndex are in increasing order
    for ( $i = 1; $i <$minIndex; $i++)
    {
        if ($arr[$i] < $arr[$i - 1])
        {
            $flag1 = 0;
            break;
        }
    }

    $flag2 = 1;

    // Check if all elements after
    // minIndex are in increasing order
    for ($i = $minIndex + 1; $i <$n; $i++)
    {
        if ($arr[$i] < $arr[$i - 1])
        {
            $flag2 = 0;
            break;
        }
    }

    // Check if last element of the array
    // is smaller than the element just
    // starting element of the array
    // for arrays like [3,4,6,1,2,5] - not sorted circular array
    if ($flag1 && $flag2 &&
       ($arr[$n - 1] < $arr[$0]))
        echo( "YES");
    else
        echo( "NO");
}

// Driver code
$arr = array(3, 4, 5, 1, 2);

//Function Call
$n = count($arr);

checkIfSortRotated($arr, $n);

// This code is contributed
// by inder_verma.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if an
    // array is sorted and rotated
    // clockwise

    // Function to check if an array is
    // sorted and rotated clockwise
    function checkIfSortRotated(arr, n)
    {
        let minEle = Number.MAX_VALUE;
        // int maxEle = int.MinValue;

        let minIndex = -1;

        // Find the minimum element
        // and it's index
        for (let i = 0; i < n; i++) {
            if (arr[i] < minEle) {
                minEle = arr[i];
                minIndex = i;
            }
        }

        let flag1 = true;

        // Check if all elements before
        // minIndex are in increasing order
        for (let i = 1; i < minIndex; i++) {
            if (arr[i] < arr[i - 1]) {
                flag1 = false;
                break;
            }
        }

        let flag2 = true;

        // Check if all elements after
        // minIndex are in increasing order
        for (let i = minIndex + 1; i < n; i++) {
            if (arr[i] < arr[i - 1]) {
                flag2 = false;
                break;
            }
        }

        // Check if last element of the array
        // is smaller than the element just
        // before the element at minIndex
        // starting element of the array
        // for arrays like [3,4,6,1,2,5] - not circular
        // array
        if (flag1 && flag2 && (arr[n - 1] < arr[0]))
            document.write("YES");
        else
            document.write("NO");
    }

    let arr = [ 3, 4, 5, 1, 2 ];

    let n = arr.length;

    // Function Call
    checkIfSortRotated(arr, n);

// This code is contributed by mukesh07.
</script>
```

**Output**

```
YES
```