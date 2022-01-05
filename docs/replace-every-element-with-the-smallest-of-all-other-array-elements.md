# 用所有其他数组元素中最小的元素替换每个元素

> 原文:[https://www . geesforgeks . org/用所有其他数组元素中最小的元素替换每个元素/](https://www.geeksforgeeks.org/replace-every-element-with-the-smallest-of-all-other-array-elements/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是用数组中所有其他元素中最小的元素替换每个元素。

**示例:**

> **输入:** arr[] = {1，1，1，2}
> **输出:**1 1 1 1 1
> 
> **输入:** arr[] = {4，2，1，3}
> **输出:** 1 1 2 1

**天真方法:**
最简单的方法是借助嵌套循环为每个元素找到所有剩余元素中最小的一个。

***时间复杂度:** O(N <sup>2</sup> )*

**高效方法:**
想法是保持前缀和后缀最小数组。维护 ***leftMin[]*** 和 ***rightMin[]*** 阵列，该阵列存储每个阵列元素的左子阵列和右子阵列的最小值。一旦计算完成，通过存储最小的 **leftMin[i]** 和 **rightMin[i]** 来替换原始数组的每个 **i <sup>th</sup>** 索引。

下面是上述方法的实现:

## C++

```
// C++ program to replace every element
// with the smallest of all other
// array elements
#include<bits/stdc++.h>
using namespace std;

void ReplaceElements(int arr[], int n)
{

    // There should be atleast two elements
    if (n < 2)
    {
        cout << (" Invalid Input ");
        return;
    }

    // leftMin array stores minimum
    // element of left subarray
    int leftMin[n];
    leftMin[0] = INT_MAX;

    // rightMin array stores minimum
    // element of right subarray
    int rightMin[n];
    rightMin[n - 1] = INT_MAX;

    for(int i = 1; i < n; i++)
    {
       leftMin[i] = min(leftMin[i - 1], arr[i - 1]);
       rightMin[n - 1 - i] = min(rightMin[n - 1 - i + 1],
                                      arr[n - 1 - i + 1]);
    }

    // Update original array with minimum
    // of leftMin[i] and rightMin[i]
    for(int i = 0; i < n; i++)
    {
       arr[i] = min(leftMin[i], rightMin[i]);
    }

    // Print the modified array.
    for(int i = 0; i < n; ++i)
    {
       cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    ReplaceElements(arr, n);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace every element
// with the smallest of all other
// array elements
import java.util.*;

class GFG {

    static void ReplaceElements(int[] arr, int n)
    {

        /* There should be atleast two elements */
        if (n < 2) {
            System.out.println(" Invalid Input ");
            return;
        }

        // leftMin array stores minimum
        // element of left subarray
        int[] leftMin = new int[n];
        leftMin[0] = Integer.MAX_VALUE;

        // rightMin array stores minimum
        // element of right subarray
        int[] rightMin = new int[n];
        rightMin[n - 1] = Integer.MAX_VALUE;

        for (int i = 1; i < n; i++) {
            leftMin[i] = Math.min(leftMin[i - 1],
                                  arr[i - 1]);
            rightMin[n - 1 - i] = Math.min(
                rightMin[n - 1 - i + 1],
                arr[n - 1 - i + 1]);
        }

        // Update original array with minimum
        // of leftMin[i] and rightMin[i]
        for (int i = 0; i < n; i++) {
            arr[i] = Math.min(leftMin[i],
                              rightMin[i]);
        }

        // Print the modified array.
        for (int i = 0; i < n; ++i) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 2 };
        int n = arr.length;

        ReplaceElements(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to replace every
# element with the smallest of all
# other array elements
import sys

def ReplaceElements(arr, n):

    # There should be atleast two elements
    if (n < 2):
        print(" Invalid Input ")
        return

    # leftMin array stores minimum
    # element of left subarray
    leftMin = [0] * n
    leftMin[0] = sys.maxsize

    # rightMin array stores minimum
    # element of right subarray
    rightMin = [0] * n
    rightMin[n - 1] = sys.maxsize

    for i in range(1, n):
        leftMin[i] = min(leftMin[i - 1],
                             arr[i - 1])
        rightMin[n - 1 - i] = min(rightMin[n - 1 -
                                           i + 1],
                                       arr[n - 1 -
                                           i + 1])

    # Update original array with minimum
    # of leftMin[i] and rightMin[i]
    for i in range(n):
        arr[i] = min(leftMin[i],
                    rightMin[i])

    # Print the modified array.
    print(*arr, sep = " ")

# Driver code
arr = [ 1, 2, 3, 2 ]
n = len(arr)

ReplaceElements(arr, n)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to replace every element
// with the smallest of all other
// array elements
using System;
class GFG{

static void ReplaceElements(int[] arr, int n)
{

    // There should be atleast two elements
    if (n < 2)
    {
        Console.Write(" Invalid Input ");
        return;
    }

    // leftMin array stores minimum
    // element of left subarray
    int[] leftMin = new int[n];
    leftMin[0] = Int32.MaxValue;

    // rightMin array stores minimum
    // element of right subarray
    int[] rightMin = new int[n];
    rightMin[n - 1] = Int32.MaxValue;

    for(int i = 1; i < n; i++)
    {
       leftMin[i] = Math.Min(leftMin[i - 1],
                                 arr[i - 1]);
       rightMin[n - 1 - i] = Math.Min(
       rightMin[n - 1 - i + 1],
            arr[n - 1 - i + 1]);
    }

    // Update original array with minimum
    // of leftMin[i] and rightMin[i]
    for(int i = 0; i < n; i++)
    {
       arr[i] = Math.Min(leftMin[i],
                         rightMin[i]);
    }

    // Print the modified array.
    for(int i = 0; i < n; ++i)
    {
       Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main()
{
    int []arr = { 1, 2, 3, 2 };
    int n = arr.Length;

    ReplaceElements(arr, n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to replace every element
// with the smallest of all other
// array elements

function ReplaceElements(arr, n)
{

    // There should be atleast two elements
    if (n < 2)
    {
        document.write(" Invalid Input ");
        return;
    }

    // leftMin array stores minimum
    // element of left subarray
    var leftMin = Array(n);
    leftMin[0] = 1000000000;

    // rightMin array stores minimum
    // element of right subarray
    var rightMin = Array(n);
    rightMin[n - 1] = 10000000000;

    for(var i = 1; i < n; i++)
    {
       leftMin[i] = Math.min(leftMin[i - 1], arr[i - 1]);
       rightMin[n - 1 - i] = Math.min(rightMin[n - 1 - i + 1],
                                      arr[n - 1 - i + 1]);
    }

    // Update original array with minimum
    // of leftMin[i] and rightMin[i]
    for(var i = 0; i < n; i++)
    {
       arr[i] = Math.min(leftMin[i], rightMin[i]);
    }

    // Print the modified array.
    for(var i = 0; i < n; ++i)
    {
       document.write( arr[i] + " ");
    }
}

// Driver code
var arr = [1, 2, 3, 2];

var n = arr.length;
ReplaceElements(arr, n);

// This code is contributed by famously.
</script>
```

**Output:** 

```
2 1 1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**另一种有效的方法:**这个想法是通过遍历数组来找到数组中最小和第二小的元素。然后，再次遍历数组:

*   如果当前元素是最小元素，则用第二小元素替换它。
*   否则用最小的元素替换当前元素

下面是上述方法的实现:

## C++

```
// C++ program to replace every
// element with the smallest
// of all other array elements
#include <bits/stdc++.h>
using namespace std;

void ReplaceElements(int arr[], int n)
{

    // There should be
    // atleast two elements
    if (n < 2)
    {
        cout << " Invalid Input ";
        return;
    }

    // first stores minimum
    // element of the array
    int first = INT_MAX;

    // second stores second
    // minimum element of the array
    int second = INT_MAX;

    // Find the smallest and second
    // smallest elements of the array
    for(int i = 0; i < n; i++)
    {

       // If current element is smaller
       // than first then update both
       // first and second
       if (arr[i] < first)
       {
           second = first;
           first = arr[i];
       }

       // If arr[i] is in between
       // first and second
       // then update second
       else if (arr[i] < second &&
                arr[i] != first)
           second = arr[i];
    }

    // Update original array with
    // first and second
    for(int i = 0; i < n; i++)
    {
       arr[i] = (arr[i] == first) ?
                  second : first;
    }

    // Print the modified array.
    for(int i = 0; i < n; ++i)
    {
       cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    ReplaceElements(arr, n);
}

// This code is contributed by himanshu77
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace
// every element with the smallest
// of all other array elements

import java.util.*;

class GFG {

    static void ReplaceElements(int[] arr, int n)
    {

        // There should be
        // atleast two elements
        if (n < 2) {
            System.out.println(
                " Invalid Input ");
            return;
        }

        // first stores minimum
        // element of the array
        int first = Integer.MAX_VALUE;

        // second stores second
        // minimum element of the array
        int second = Integer.MAX_VALUE;

        // Find the smallest and second
        // smallest elements of the array
        for (int i = 0; i < n; i++) {

            // If current element
            // is smaller than first
            // then update both
            // first and second
            if (arr[i] < first) {
                second = first;
                first = arr[i];
            }

            // If arr[i] is in between
            // first and second
            // then update second
            else if (arr[i] < second
                     && arr[i] != first)
                second = arr[i];
        }

        // Update original array with
        // first and second
        for (int i = 0; i < n; i++) {

            arr[i] = (arr[i] == first)
                         ? second
                         : first;
        }

        // Print the modified array.
        for (int i = 0; i < n; ++i) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 2 };
        int n = arr.length;

        ReplaceElements(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to replace
# every element with the smallest
# of all other array elements
import sys

def ReplaceElements(arr, n):

    # There should be
    # atleast two elements
    if (n < 2):
        print(" Invalid Input ")
        return

    # first stores minimum
    # element of the array
    first = sys.maxsize

    # second stores second
    # minimum element of the array
    second = sys.maxsize

    # Find the smallest and second
    # smallest elements of the array
    for i in range(n):

        # If current element
        # is smaller than first
        # then update both
        # first and second
        if (arr[i] < first):
            second = first
            first = arr[i]

        # If arr[i] is in between
        # first and second
        # then update second
        elif (arr[i] < second and
              arr[i] != first):
            second = arr[i]

    # Update original array with
    # first and second
    for i in range(n):
        if (arr[i] == first):
            arr[i] = second
        else:
            arr[i] = first

    # Print the modified array.
    for i in range(n):
        print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 2 ]
    n = len(arr)

    ReplaceElements(arr, n)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to replace every
// element with the smallest
// of all other array elements
using System;

class GFG{

static void ReplaceElements(int[] arr, int n)
{

    // There should be
    // atleast two elements
    if (n < 2)
    {
        Console.WriteLine(" Invalid Input ");
        return;
    }

    // first stores minimum
    // element of the array
    int first = Int32.MaxValue;

    // second stores second
    // minimum element of the array
    int second = Int32.MaxValue;

    // Find the smallest and second
    // smallest elements of the array
    for(int i = 0; i < n; i++)
    {

        // If current element
        // is smaller than first
        // then update both
        // first and second
        if (arr[i] < first)
        {
            second = first;
            first = arr[i];
        }

        // If arr[i] is in between
        // first and second
        // then update second
        else if (arr[i] < second &&
                 arr[i] != first)
            second = arr[i];
    }

    // Update original array with
    // first and second
    for(int i = 0; i < n; i++)
    {
        arr[i] = (arr[i] == first) ?
                  second : first;
    }

    // Print the modified array.
    for(int i = 0; i < n; ++i)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver code
static void Main()
{
    int[] arr = { 1, 2, 3, 2 };
    int n = arr.Length;

    ReplaceElements(arr, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program to replace every
// element with the smallest
// of all other array elements

function ReplaceElements(arr,  n)
{

    // There should be
    // atleast two elements
    if (n < 2)
    {
        document.write( " Invalid Input ");
        return;
    }

    // first stores minimum
    // element of the array
    var first = Number.MAX_VALUE;

    // second stores second
    // minimum element of the array
    var second = Number.MAX_VALUE;

    // Find the smallest and second
    // smallest elements of the array
    for(var i = 0; i < n; i++)
    {

       // If current element is smaller
       // than first then update both
       // first and second
       if (arr[i] < first)
       {
           second = first;
           first = arr[i];
       }

       // If arr[i] is in between
       // first and second
       // then update second
       else if (arr[i] < second && arr[i] != first)
           second = arr[i];
    }

    // Update original array with
    // first and second
    for(var i = 0; i < n; i++)
    {
       arr[i] = (arr[i] == first) ? second : first;
    }

    // Print the modified array.
    for(var i = 0; i < n; ++i)
    {
       document.write( arr[i] + " ");
    }
}

var arr = [ 1, 2, 3, 2 ];
var n = arr.length;
ReplaceElements(arr, n);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2 1 1 1
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*