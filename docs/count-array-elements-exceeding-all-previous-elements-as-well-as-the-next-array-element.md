# 计数超过所有先前元素的数组元素以及下一个数组元素

> 原文:[https://www . geeksforgeeks . org/count-array-elements-exclusive-all-previous-elements-as-next-array-element/](https://www.geeksforgeeks.org/count-array-elements-exceeding-all-previous-elements-as-well-as-the-next-array-element/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出满足以下条件的数组元素的个数:

*   数组元素应该严格大于所有先前出现的数组元素。
*   要么是最后一个数组元素，要么整数应该严格大于下一个数组元素。

***注:**也可以考虑数组的第一个整数。*

**示例:**

> **输入:** arr[] = {1，2，0，7，2，0，2，0}
> **输出:** 2
> **说明:** arr[1] (= 2)和 arr[3] ( = 7)是满足给定条件的数组元素。
> 
> **输入:** arr[] = {4，8，15，16，23，42}
> **输出:** 1

**方法:**思路是线性[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查每个数组元素是否满足给定条件。按照以下步骤解决此问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   从数组的第一个元素开始，跟踪到目前为止遇到的最大数组元素。
*   如果最大数组元素大于之前遇到的最大数组元素，请更新它。
*   更新当前最大值后，检查下一个数组元素是否大于当前数组元素。如果发现为真，则增加计数。
*   重复这个过程，直到遍历完最后一个数组元素。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count array elements
// satisfying the given condition
int numberOfIntegers(int arr[], int N)
{
    int cur_max = 0, count = 0;

    // If there is only one
    // array element
    if (N == 1) {
        count = 1;
    }
    else {

        // Traverse the array
        for (int i = 0; i < N - 1; i++) {

            // Update the maximum element
            // encountered so far
            if (arr[i] > cur_max) {
                cur_max = arr[i];

                // Count the number of array elements
                // strictly greater than all previous
                // and immediately next elements
                if (arr[i] > arr[i + 1]) {

                    count++;
                }
            }
        }
        if (arr[N - 1] > cur_max)
            count++;
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 0, 7, 2, 0, 2, 0 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    numberOfIntegers(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to count array elements
    // satisfying the given condition
    static void numberOfIntegers(int[] arr, int N)
    {
        int cur_max = 0, count = 0;

        // If there is only one
        // array element
        if (N == 1) {
            count = 1;
        }
        else
        {

            // Traverse the array
            for (int i = 0; i < N - 1; i++)
            {

                // Update the maximum element
                // encountered so far
                if (arr[i] > cur_max)
                {
                    cur_max = arr[i];

                    // Count the number of array elements
                    // strictly greater than all previous
                    // and immediately next elements
                    if (arr[i] > arr[i + 1])
                    {
                        count++;
                    }
                }
            }
            if (arr[N - 1] > cur_max)
                count++;
        }

        // Print the count
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int[] arr = new int[] { 1, 2, 0, 7, 2, 0, 2, 0 };

        // Size of the array
        int N = arr.length;
        numberOfIntegers(arr, N);
    }
}

// This code is contributed by dharanendralv23
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count array elements
# satisfying the given condition
def numberOfIntegers(arr, N) :  
    cur_max = 0
    count = 0

    # If there is only one
    # array element
    if (N == 1) :
        count = 1   
    else :

        # Traverse the array
        for i in range(N - 1):

            # Update the maximum element
            # encountered so far
            if (arr[i] > cur_max) :
                cur_max = arr[i]

                # Count the number of array elements
                # strictly greater than all previous
                # and immediately next elements
                if (arr[i] > arr[i + 1]) :
                    count += 1                  
        if (arr[N - 1] > cur_max) :
            count += 1

    # Print the count
    print(count)

# Driver Code

# Given array
arr = [ 1, 2, 0, 7, 2, 0, 2, 0 ]

# Size of the array
N = len(arr)
numberOfIntegers(arr, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to count array elements
    // satisfying the given condition
    static void numberOfIntegers(int[] arr, int N)
    {
        int cur_max = 0, count = 0;

        // If there is only one
        // array element
        if (N == 1) {
            count = 1;
        }
        else {

            // Traverse the array
            for (int i = 0; i < N - 1; i++) {

                // Update the maximum element
                // encountered so far
                if (arr[i] > cur_max) {
                    cur_max = arr[i];

                    // Count the number of array elements
                    // strictly greater than all previous
                    // and immediately next elements
                    if (arr[i] > arr[i + 1]) {

                        count++;
                    }
                }
            }
            if (arr[N - 1] > cur_max)
                count++;
        }

        // Print the count
        Console.WriteLine(count);
    }

    // Driver Code
    static public void Main()
    {

        // Given array
        int[] arr = new int[] { 1, 2, 0, 7, 2, 0, 2, 0 };

        // Size of the array
        int N = arr.Length;

        numberOfIntegers(arr, N);
    }
}

// This code is contributed by dharavendralv23
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

    // Function to count array elements
    // satisfying the given condition
    function numberOfIntegers(arr, N)
    {
        let cur_max = 0, count = 0;

        // If there is only one
        // array element
        if (N == 1) {
            count = 1;
        }
        else
        {

            // Traverse the array
            for (let i = 0; i < N - 1; i++)
            {

                // Update the maximum element
                // encountered so far
                if (arr[i] > cur_max)
                {
                    cur_max = arr[i];

                    // Count the number of array elements
                    // strictly greater than all previous
                    // and immediately next elements
                    if (arr[i] > arr[i + 1])
                    {
                        count++;
                    }
                }
            }
            if (arr[N - 1] > cur_max)
                count++;
        }

        // Print the count
        document.write(count);
    } 

// Driver code

        // Given array
        let arr = [ 1, 2, 0, 7, 2, 0, 2, 0 ];

        // Size of the array
        let N = arr.length;
        numberOfIntegers(arr, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)