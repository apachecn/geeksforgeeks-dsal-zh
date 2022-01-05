# 用数组右侧元素的和替换数组的每个元素

> 原文:[https://www . geeksforgeeks . org/将数组中的每个元素替换为右侧元素的总和/](https://www.geeksforgeeks.org/replace-every-element-of-array-with-sum-of-elements-on-its-right-side/)

给定一个数组 **arr[]** ，任务是用数组右侧元素的和替换数组的每个元素。
**例:**

> **输入:** arr[] = {1，2，5，2，2，5}
> **输出:** 16 14 9 7 5 0
> 
> **输入:** arr[] = {5，1，3，2，4}
> **输出:** 10 9 6 4 0

**天真法:**一个简单的方法是运行两个[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，外循环逐个固定每个元素，内循环计算固定元素右侧的元素之和。
**时间复杂度:** ![O(N^{2})    ](img/49dcd350a0d2b45cce363f14e678deb0.png "Rendered by QuickLaTeX.com")
**高效方法:**想法是计算数组的总和，然后将当前元素更新为![sum - arr[i]    ](img/adfea5e821b602d3cca68cc6f3b957e6.png "Rendered by QuickLaTeX.com")，并在每个步骤中将总和更新为当前元素。

```
for i in arr:
  arr[i] = sum - arr[i]
  sum = arr[i]
```

下面是上述方法的实现:

## C++

```
// C++ program to Replace every
// element of array with sum of
// elements on its right side
#include<bits/stdc++.h>
using namespace std;

// Function to replace every element
// of the array to the sum of elements
// on the right side of the array
void replaceElement(int arr[], int n)
{
    int sum = 0;

    // Calculate sum of all
    // elements of array
    for(int i = 0; i < n; i++)
       sum += arr[i];

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

       // Replace current element
       // of array with sum-arr[i]
       arr[i] = sum - arr[i];

       // Update sum with arr[i]
       sum = arr[i];
    }

    // Print modified array
    for(int i = 0; i < n; i++)
       cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 5, 2, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    replaceElement(arr, n);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Replace every
// element of array with sum of
// elements on its right side

import java.util.*;
class GFG {

    // Function to replace every element
    // of the array to the sum of elements
    // on the right side of the array
    static void replaceElement(int[] arr, int n)
    {
        int sum = 0;

        // Calculate sum of all
        // elements of array
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // Replace current element
            // of array with sum-arr[i]
            arr[i] = sum - arr[i];

            // Update sum with arr[i]
            sum = arr[i];
        }

        // Print modified array
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 5, 2, 2, 5 };
        int n = arr.length;
        replaceElement(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to replace every
# element of array with sum of
# elements on its right side

# Function to replace every element
# of the array to the sum of elements
# on the right side of the array
def replaceElement(arr, n):

    sum = 0;

    # Calculate sum of all
    # elements of array
    for i in range(0, n):
        sum += arr[i];

    # Traverse the array
    for i in range(0, n):

        # Replace current element
        # of array with sum-arr[i]
        arr[i] = sum - arr[i];

        # Update sum with arr[i]
        sum = arr[i];

    # Print modified array
    for i in range(0, n):
        print(arr[i], end = " ");

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 5, 2, 2, 5 ]
    n = len(arr)

    replaceElement(arr, n)

# This code is contributed by Ritik Bansal
```

## C#

```
// C# program to Replace every
// element of array with sum of
// elements on its right side
using System;
class GFG{

// Function to replace every element
// of the array to the sum of elements
// on the right side of the array
static void replaceElement(int[] arr, int n)
{
    int sum = 0;

    // Calculate sum of all
    // elements of array
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // Replace current element
        // of array with sum-arr[i]
        arr[i] = sum - arr[i];

        // Update sum with arr[i]
        sum = arr[i];
    }

    // Print modified array
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 5, 2, 2, 5 };
    int n = arr.Length;
    replaceElement(arr, n);
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// JavaScript program to Replace every
// element of array with sum of
// elements on its right side

// Function to replace every element
// of the array to the sum of elements
// on the right side of the array
function replaceElement(arr, n)
{
    let sum = 0;

    // Calculate sum of all
    // elements of array
    for(let i = 0; i < n; i++)
    sum += arr[i];

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

    // Replace current element
    // of array with sum-arr[i]
    arr[i] = sum - arr[i];

    // Update sum with arr[i]
    sum = arr[i];
    }

    // Print modified array
    for(let i = 0; i < n; i++)
    document.write(arr[i] + " ");
}

// Driver code

    let arr = [ 1, 2, 5, 2, 2, 5 ];
    let n = arr.length;

    replaceElement(arr, n);

//This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
16 14 9 7 5 0
```

**时间复杂度:** O(N)

**辅助空间:** O(1)