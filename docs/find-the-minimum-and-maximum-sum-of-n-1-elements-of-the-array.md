# 求数组 N-1 个元素的最小和最大和

> 原文:[https://www . geeksforgeeks . org/find-n-1 个数组元素的最小和最大和/](https://www.geeksforgeeks.org/find-the-minimum-and-maximum-sum-of-n-1-elements-of-the-array/)

给定一个大小为 **N** 的未排序数组 **A** ，任务是通过精确添加 **N-1** 元素来找到可以计算的最小值和最大值。

**示例:**

> **输入:** a[] = {13，5，11，9，7}
> **输出:** 32 40
> **说明:**最小和为 5 + 7 + 9 + 11 = 32，最大和为 7 + 9 + 11 + 13 = 40。
> **输入:** a[] = {13，11，45，32，89，21}
> **输出:** 122 200
> **说明:**最小和为 11 + 13 + 21 + 32 + 45 = 122，最大和为 13 + 21 + 32 + 45 + 89 = 200。
> **输入:** a[] = {6，3，15，27，9}
> **输出:** 33 57
> **说明:**最小和为 3 + 6 + 9 + 15 = 33，最大和为 6 + 9 + 15 + 27 = 57。

**简单方法:**

1.  按升序对数组进行排序。
2.  数组中前 N-1 个元素的和给出了最小可能的和。
3.  数组中最后 N-1 个元素的和给出了最大可能的和。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the above approach
import java.util.*;

class GFG {

    static void minMax(int[] arr)
    {
        // Initialize the min_value
        // and max_value to 0
        long min_value = 0;
        long max_value = 0;
        int n = arr.length;

        // Sort array before calculating
        // min and max value
        Arrays.sort(arr);

        for (int i = 0, j = n - 1;
             i < n - 1; i++, j--)
        {
            // All elements except
            // rightmost will be added
            min_value += arr[i];

            // All elements except
            // leftmost will be added
            max_value += arr[j];
        }

        // Output: min_value and max_value
        System.out.println(
            min_value + " "
            + max_value);
    }

    // Driver Code
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);

        // Initialize your array elements here
        int[] arr = { 10, 9, 8, 7, 6, 5 };
        int[] arr1 = { 100, 200, 300, 400, 500 };
        minMax(arr);
        minMax(arr1);
    }
}
```

## 蟒蛇 3

```
# Python Implementation of the above approach
def minMax(arr):

    # Initialize the min_value
    # and max_value to 0
    min_value = 0
    max_value = 0
    n=len(arr)

    # Sort array before calculating
    # min and max value
    arr.sort()
    j=n-1
    for i in range(n-1):

        # All elements except
        # rightmost will be added
        min_value += arr[i]

        # All elements except
        # leftmost will be added
        max_value += arr[j]
        j-=1

    # Output: min_value and max_value
    print(min_value," ",max_value)

#  Driver Code
arr=[10, 9, 8, 7, 6, 5]
arr1=[100, 200, 300, 400, 500]

minMax(arr)
minMax(arr1)

#  This code is contributed by ab2127.
```

## C#

```
using System;

public class GFG{

    static void minMax(int[] arr)
    {
        // Initialize the min_value
        // and max_value to 0
        long min_value = 0;
        long max_value = 0;
        int n = arr.Length;

        // Sort array before calculating
        // min and max value
        Array.Sort(arr);
        int j = n - 1;                  
        for (int i = 0 ;i < n - 1; i++)
        {
            // All elements except
            // rightmost will be added
            min_value += arr[i];

            // All elements except
            // leftmost will be added
            max_value += arr[j];
            j--;
        }

        // Output: min_value and max_value
        Console.WriteLine(
            min_value + " "
            + max_value);
    }

    // Driver Code

    static public void Main (){

        // Initialize your array elements here
        int[] arr = { 10, 9, 8, 7, 6, 5 };
        int[] arr1 = { 100, 200, 300, 400, 500 };
        minMax(arr);
        minMax(arr1);
    }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript Implementation of the above approach

    function minMax(arr)
    {
        // Initialize the min_value
        // and max_value to 0
        let min_value = 0;
        let max_value = 0;
        let n = arr.length;

        // Sort array before calculating
        // min and max value
        arr.sort(function(a,b){return a-b;});

        for (let i = 0, j = n - 1;
             i < n - 1; i++, j--)
        {
            // All elements except
            // rightmost will be added
            min_value += arr[i];

            // All elements except
            // leftmost will be added
            max_value += arr[j];
        }

        // Output: min_value and max_value
        document.write(
            min_value + " "
            + max_value+"<br>");
    }

    // Driver Code
    let arr=[10, 9, 8, 7, 6, 5];
    let arr1=[100, 200, 300, 400, 500 ];
    minMax(arr);
    minMax(arr1);

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
35 40
1000 1400
```

**时间复杂度:** *O(NlogN)*

**有效方法:**

1.  找到数组的最小和最大元素。
2.  计算数组中所有元素的总和。
3.  从总和中排除最大元素给出最小可能总和。
4.  从总和中排除最小元素得到最大可能总和。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum and maximum
// sum from an array.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum and maximum sum
static void miniMaxSum(int arr[], int n)
{

    // Initialize the minElement, maxElement
    // and sum by 0.
    int minElement = 0, maxElement = 0, sum = 0;

    // Assigning maxElement, minElement
    // and sum as the first array element
    minElement = arr[0];
    maxElement = minElement;
    sum = minElement;

    // Traverse the entire array
    for(int i = 1; i < n; i++)
    {

        // Calculate the sum of
        // array elements
        sum += arr[i];

        // Keep updating the
        // minimum element
        if (arr[i] < minElement)
        {
            minElement = arr[i];
        }

        // Keep updating the
        // maximum element
        if (arr[i] > maxElement)
        {
            maxElement = arr[i];
        }
    }

    // print the minimum and maximum sum
    cout << (sum - maxElement) << " "
         << (sum - minElement) << endl;
}

// Driver Code
int main()
{

    // Test Case 1:
    int a1[] = { 13, 5, 11, 9, 7 };
    int n = sizeof(a1) / sizeof(a1[0]);

    // Call miniMaxSum()
    miniMaxSum(a1, n);

    // Test Case 2:
    int a2[] = { 13, 11, 45, 32, 89, 21 };
    n = sizeof(a2) / sizeof(a2[0]);
    miniMaxSum(a2, n);

    // Test Case 3:
    int a3[] = { 6, 3, 15, 27, 9 };
    n = sizeof(a3) / sizeof(a3[0]);
    miniMaxSum(a3, n);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum and maximum
// sum from an array.
class GFG {

    // Function to calculate minimum and maximum sum
    static void miniMaxSum(int[] arr)
    {

        // Initialize the minElement, maxElement
        // and sum by 0.
        int minElement = 0, maxElement = 0, sum = 0;

        // Assigning maxElement, minElement
        // and sum as the first array element
        minElement = arr[0];
        maxElement = minElement;
        sum = minElement;

        // Traverse the entire array
        for (int i = 1; i < arr.length; i++) {

            // calculate the sum of
            // array elements
            sum += arr[i];

            // Keep updating the
            // minimum element
            if (arr[i] < minElement) {
                minElement = arr[i];
            }

            // Keep updating the
            // maximum element
            if (arr[i] > maxElement) {
                maxElement = arr[i];
            }
        }

        // print the minimum and maximum sum
        System.out.println((sum - maxElement) + " "
                        + (sum - minElement));
    }

    // Driver Code
    public static void main(String args[])
    {

        // Test Case 1:
        int a1[] = { 13, 5, 11, 9, 7 };
        // Call miniMaxSum()
        miniMaxSum(a1);

        // Test Case 2:
        int a2[] = { 13, 11, 45, 32, 89, 21 };
        miniMaxSum(a2);

        // Test Case 3:
        int a3[] = { 6, 3, 15, 27, 9 };
        miniMaxSum(a3);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum and
# maximum sum from a list.

# Function to calculate minimum and maximum sum
def miniMaxSum(arr, n):

    # Initialize the minElement, maxElement
    # and sum by 0.
    minElement = 0
    maxElement = 0
    sum = 0

    # Assigning maxElement, minElement
    # and sum as the first list element
    minElement = arr[0]
    maxElement = minElement
    sum = minElement

    # Traverse the entire list
    for i in range(1, n):

        # Calculate the sum of
        # list elements
        sum += arr[i]

        # Keep updating the
        # minimum element
        if (arr[i] < minElement):
            minElement = arr[i]

        # Keep updating the
        # maximum element
        if (arr[i] > maxElement):
            maxElement = arr[i]

    # Print the minimum and maximum sum
    print(sum - maxElement,
          sum - minElement)

# Driver Code

# Test Case 1:
a1 = [ 13, 5, 11, 9, 7 ]
n = len(a1)

# Call miniMaxSum()
miniMaxSum(a1, n)

# Test Case 2:
a2 = [ 13, 11, 45, 32, 89, 21 ]
n = len(a2)
miniMaxSum(a2, n)

# Test Case 3:
a3 = [ 6, 3, 15, 27, 9 ]
n = len(a3)
miniMaxSum(a3, n)

# This code is contributed by vishu2908
```

## C#

```
// C# program to find the minimum and maximum
// sum from an array.
using System;

class GFG{

// Function to calculate minimum and maximum sum
static void miniMaxSum(int[] arr)
{

    // Initialize the minElement, maxElement
    // and sum by 0.
    int minElement = 0, maxElement = 0, sum = 0;

    // Assigning maxElement, minElement
    // and sum as the first array element
    minElement = arr[0];
    maxElement = minElement;
    sum = minElement;

    // Traverse the entire array
    for(int i = 1; i < arr.Length; i++)
    {

        // Calculate the sum of
        // array elements
        sum += arr[i];

        // Keep updating the
        // minimum element
        if (arr[i] < minElement)
        {
            minElement = arr[i];
        }

        // Keep updating the
        // maximum element
        if (arr[i] > maxElement)
        {
            maxElement = arr[i];
        }
    }

    // Print the minimum and maximum sum
    Console.WriteLine((sum - maxElement) + " " +
                      (sum - minElement));
}

// Driver Code
public static void Main()
{

    // Test Case 1:
    int[] a1 = new int[]{ 13, 5, 11, 9, 7 };

    // Call miniMaxSum()
    miniMaxSum(a1);

    // Test Case 2:
    int[] a2 = new int[]{ 13, 11, 45, 32, 89, 21 };
    miniMaxSum(a2);

    // Test Case 3:
    int[] a3 = new int[]{ 6, 3, 15, 27, 9 };
    miniMaxSum(a3);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Function to calculate minimum and maximum sum
function  miniMaxSum( arr, n)
{

    // Initialize the minElement, maxElement
    // and sum by 0.
    var minElement = 0, maxElement = 0, sum = 0;

    // Assigning maxElement, minElement
    // and sum as the first array element
    minElement = arr[0];
    maxElement = minElement;
    sum = minElement;

    // Traverse the entire array
    for(var i = 1; i < n; i++)
    {

        // Calculate the sum of
        // array elements
        sum += arr[i];

        // Keep updating the
        // minimum element
        if (arr[i] < minElement)
        {
            minElement = arr[i];
        }

        // Keep updating the
        // maximum element
        if (arr[i] > maxElement)
        {
            maxElement = arr[i];
        }
    }

    // print the minimum and maximum sum
    document.write((sum - maxElement)+ "  "+ (sum - minElement) + "<br>");
}

// Driver Code

var a1= [ 13, 5, 11, 9, 7 ];

    // Call miniMaxSum()
    miniMaxSum(a1, 5);

    // Test Case 2:
    var a2 = [13, 11, 45, 32, 89, 21 ];

    miniMaxSum(a2, 6);

    // Test Case 3:
    var a3 = [ 6, 3, 15, 27, 9 ];

    miniMaxSum(a3, 5);

</script>
```

**Output**

```
32 40
122 200
33 57
```

**时间复杂度:** *O(N)*