# 用左边最小元素和右边最大元素的绝对差替换元素

> 原文:[https://www . geesforgeks . org/用左最小元素和右最大元素的绝对差值替换元素/](https://www.geeksforgeeks.org/replace-elements-with-absolute-difference-of-smallest-element-on-left-and-largest-element-on-right/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是用数组左边最小元素和右边最大元素的绝对差来替换数组的所有元素。
**例:**

> **输入:** arr[] = {1，5，2，4，3}
> **输出:**5 3 2 1
> 
> <figure class="table">
> 
> | 元素 | 左边最小的 | 最大的在右边 | 绝对差异 |
> | --- | --- | --- | --- |
> | one | 空 | five | five |
> | five | one | four | three |
> | Two | one | four | three |
> | four | one | three | Two |
> | three | one | 空 | one |
> 
> **输入:** arr[] = {4，3，6，2，1，20，9，10，15，6 }
> T3】输出: 20 16 17 17 18 14 14 14 5 1
> 
> </figure>

**天真的做法:**对于数组的每个元素**arr【I】**，找到子阵**arr【0…I-1】**中的最小元素，然后找到子阵**arr【I+1…n-1】**中的最大元素，打印两者的绝对差。这种方法的时间复杂度将是 **O(N <sup>2</sup> )** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// elements of an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to return the minimum element
// in the subarray arr[i...j]
int getMin(int arr[], int i, int j)
{

    // To store the minimum element
    int minVal = arr[i++];
    while (i <= j) {

        // Update the minimum element so far
        minVal = min(minVal, arr[i]);
        i++;
    }

    // Return the minimum element found
    return minVal;
}

// Function to return the maximum element
// in the subarray arr[i...j]
int getMax(int arr[], int i, int j)
{

    // To store the maximum element
    int maxVal = arr[i++];
    while (i <= j) {

        // Update the maximum element so far
        maxVal = max(maxVal, arr[i]);
        i++;
    }

    // Return the maximum element found
    return maxVal;
}

// Function to generate the array
// with the given operations
void generateArr(int arr[], int n)
{

    // Base cases
    if (n == 0)
        return;
    if (n == 1) {
        cout << arr[0];
        return;
    }

    // To store the new array elements
    int tmpArr[n];

    // The first element has no
    // element on its left
    tmpArr[0] = getMax(arr, 1, n - 1);

    // From the second element to the
    // second last element
    for (int i = 1; i < n - 1; i++) {

        // Absolute difference of the maximum
        // element to the right and the
        // minimum element to the left
        tmpArr[i] = abs(getMax(arr, i + 1, n - 1)
                        - getMin(arr, 0, i - 1));
    }

    // The last element has no
    // element on its right
    tmpArr[n - 1] = getMin(arr, 0, n - 2);

    // Print the generated array
    printArray(tmpArr, n);
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 2, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    generateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Utility function to print the
// elements of an array
static void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Function to return the minimum element
// in the subarray arr[i...j]
static int getMin(int arr[], int i, int j)
{

    // To store the minimum element
    int minVal = arr[i++];
    while (i <= j)
    {

        // Update the minimum element so far
        minVal = Math.min(minVal, arr[i]);
        i++;
    }

    // Return the minimum element found
    return minVal;
}

// Function to return the maximum element
// in the subarray arr[i...j]
static int getMax(int arr[], int i, int j)
{

    // To store the maximum element
    int maxVal = arr[i++];
    while (i <= j)
    {

        // Update the maximum element so far
        maxVal = Math.max(maxVal, arr[i]);
        i++;
    }

    // Return the maximum element found
    return maxVal;
}

// Function to generate the array
// with the given operations
static void generateArr(int arr[], int n)
{

    // Base cases
    if (n == 0)
        return;
    if (n == 1)
    {
        System.out.println(arr[0]);
        return;
    }

    // To store the new array elements
    int tmpArr[] = new int[n];

    // The first element has no
    // element on its left
    tmpArr[0] = getMax(arr, 1, n - 1);

    // From the second element to the
    // second last element
    for (int i = 1; i < n - 1; i++)
    {

        // Absolute difference of the maximum
        // element to the right and the
        // minimum element to the left
        tmpArr[i] = Math.abs(getMax(arr, i + 1, n - 1) -
                             getMin(arr, 0, i - 1));
    }

    // The last element has no
    // element on its right
    tmpArr[n - 1] = getMin(arr, 0, n - 2);

    // Print the generated array
    printArray(tmpArr, n);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 5, 2, 4, 3 };
    int n = arr.length;

    generateArr(arr, n);
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print the
# elements of an array
def printArray(arr, n):
    for i in range(n):
        print(arr[i], end = " ")

# Function to return the minimum element
# in the subarray arr[i...j]
def getMin(arr, i, j):

    # To store the minimum element
    minVal = arr[i]
    i += 1
    while (i <= j):

        # Update the minimum element so far
        minVal = min(minVal, arr[i])
        i += 1

    # Return the minimum element found
    return minVal

# Function to return the maximum element
# in the subarray arr[i...j]
def getMax(arr, i, j):

    # To store the maximum element
    maxVal = arr[i]
    i += 1
    while (i <= j):

        # Update the maximum element so far
        maxVal = max(maxVal, arr[i])
        i += 1

    # Return the maximum element found
    return maxVal

# Function to generate the array
# With the given operations
def generateArr(arr, n):

    # Base cases
    if (n == 0):
        return
    if (n == 1):
        print(arr[0], end = "")
        return

    # To store the new array elements
    tmpArr = [0 for i in range(n)]

    # The first element has no
    # element on its left
    tmpArr[0] = getMax(arr, 1, n - 1)

    # From the second element to the
    # second last element
    for i in range(1, n - 1):

        # Absolute difference of the maximum
        # element to the right and the
        # minimum element to the left
        tmpArr[i] = abs(getMax(arr, i + 1, n - 1) -
                        getMin(arr, 0, i - 1))

    # The last element has no
    # element on its right
    tmpArr[n - 1] = getMin(arr, 0, n - 2)

    # Print the generated array
    printArray(tmpArr, n)

# Driver code
arr = [1, 5, 2, 4, 3]
n = len(arr)

generateArr(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print the
// elements of an array
static void printArray(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to return the minimum element
// in the subarray arr[i...j]
static int getMin(int []arr, int i, int j)
{

    // To store the minimum element
    int minVal = arr[i++];
    while (i <= j)
    {

        // Update the minimum element so far
        minVal = Math.Min(minVal, arr[i]);
        i++;
    }

    // Return the minimum element found
    return minVal;
}

// Function to return the maximum element
// in the subarray arr[i...j]
static int getMax(int []arr, int i, int j)
{

    // To store the maximum element
    int maxVal = arr[i++];
    while (i <= j)
    {

        // Update the maximum element so far
        maxVal = Math.Max(maxVal, arr[i]);
        i++;
    }

    // Return the maximum element found
    return maxVal;
}

// Function to generate the array
// with the given operations
static void generateArr(int []arr, int n)
{

    // Base cases
    if (n == 0)
        return;
    if (n == 1)
    {
        Console.WriteLine(arr[0]);
        return;
    }

    // To store the new array elements
    int []tmpArr = new int[n];

    // The first element has no
    // element on its left
    tmpArr[0] = getMax(arr, 1, n - 1);

    // From the second element to the
    // second last element
    for (int i = 1; i < n - 1; i++)
    {

        // Absolute difference of the maximum
        // element to the right and the
        // minimum element to the left
        tmpArr[i] = Math.Abs(getMax(arr, i + 1, n - 1) -
                             getMin(arr, 0, i - 1));
    }

    // The last element has no
    // element on its right
    tmpArr[n - 1] = getMin(arr, 0, n - 2);

    // Print the generated array
    printArray(tmpArr, n);
}

// Driver code
static public void Main ()
{
    int []arr = { 1, 5, 2, 4, 3 };
    int n = arr.Length;

    generateArr(arr, n);
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Utility function to print the
    // elements of an array
    function printArray(arr, n)
    {
        for (let i = 0; i < n; i++)
        {
            document.write(arr[i] + " ");
        }
    }

    // Function to return the minimum element
    // in the subarray arr[i...j]
    function getMin(arr, i, j)
    {

        // To store the minimum element
        let minVal = arr[i++];
        while (i <= j)
        {

            // Update the minimum element so far
            minVal = Math.min(minVal, arr[i]);
            i++;
        }

        // Return the minimum element found
        return minVal;
    }

    // Function to return the maximum element
    // in the subarray arr[i...j]
    function getMax(arr, i, j)
    {

        // To store the maximum element
        let maxVal = arr[i++];
        while (i <= j)
        {

            // Update the maximum element so far
            maxVal = Math.max(maxVal, arr[i]);
            i++;
        }

        // Return the maximum element found
        return maxVal;
    }

    // Function to generate the array
    // with the given operations
    function generateArr(arr, n)
    {

        // Base cases
        if (n == 0)
            return;
        if (n == 1)
        {
            document.write(arr[0] + "</br>");
            return;
        }

        // To store the new array elements
        let tmpArr = new Array(n);
        tmpArr.fill(0);

        // The first element has no
        // element on its left
        tmpArr[0] = getMax(arr, 1, n - 1);

        // From the second element to the
        // second last element
        for (let i = 1; i < n - 1; i++)
        {

          // Absolute difference of the maximum
         // element to the right and the
        // minimum element to the left
           tmpArr[i] = Math.abs(getMax(arr, i + 1, n - 1) -
                                 getMin(arr, 0, i - 1));
        }

        // The last element has no
        // element on its right
        tmpArr[n - 1] = getMin(arr, 0, n - 2);

        // Print the generated array
        printArray(tmpArr, n);
    }

    let arr = [ 1, 5, 2, 4, 3 ];
    let n = arr.length;

    generateArr(arr, n);

// This code is contributed by suresh07.

</script>
```

**Output:** 

```
5 3 3 2 1
```

**有效方法:**创建一个数组**后缀 Max[]** 其中**后缀 Max[i]** 将存储子数组 **arr[i…N-1]** 中的最大元素。另外取一个变量 **minSoFar** ，它将存储从左到右遍历数组时的最小元素。现在，对于每个元素 **arr[i]** ，更新后的值将是 **abs(后缀 max[I+1]–minSoFar)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// elements of an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to generate the array
// with the given operations
void generateArr(int arr[], int n)
{

    // Base cases
    if (n == 0)
        return;
    if (n == 1) {
        cout << arr[0];
        return;
    }

    // To suffixMax[i] will store the maximum
    // element in the subarray arr[i...n-1]
    int suffixMax[n];
    suffixMax[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixMax[i] = max(arr[i], suffixMax[i + 1]);

    // To store the minimum element on the left
    int minSoFar = arr[0];

    // The first element has no
    // element on its left
    arr[0] = suffixMax[1];

    // From the second element to the
    // second last element
    for (int i = 1; i < n - 1; i++) {

        // Store a copy of the currene element
        int temp = arr[i];

        // Absolute difference of the maximum
        // element to the right and the
        // minimum element to the left
        arr[i] = abs(suffixMax[i + 1] - minSoFar);

        // Update the minimum element so far
        minSoFar = min(minSoFar, temp);
    }

    // The last element has no
    // element on its right
    arr[n - 1] = minSoFar;

    // Print the updated array
    printArray(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 2, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    generateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Utility function to print the
// elements of an array
static void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Function to generate the array
// with the given operations
static void generateArr(int arr[], int n)
{

    // Base cases
    if (n == 0)
        return;
    if (n == 1)
    {
        System.out.print(arr[0]);
        return;
    }

    // To suffixMax[i] will store the maximum
    // element in the subarray arr[i...n-1]
    int []suffixMax = new int[n];
    suffixMax[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixMax[i] = Math.max(arr[i],
                                suffixMax[i + 1]);

    // To store the minimum element on the left
    int minSoFar = arr[0];

    // The first element has no
    // element on its left
    arr[0] = suffixMax[1];

    // From the second element to the
    // second last element
    for (int i = 1; i < n - 1; i++)
    {

        // Store a copy of the currene element
        int temp = arr[i];

        // Absolute difference of the maximum
        // element to the right and the
        // minimum element to the left
        arr[i] = Math.abs(suffixMax[i + 1] -
                                 minSoFar);

        // Update the minimum element so far
        minSoFar = Math.min(minSoFar, temp);
    }

    // The last element has no
    // element on its right
    arr[n - 1] = minSoFar;

    // Print the updated array
    printArray(arr, n);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 5, 2, 4, 3 };
    int n = arr.length;

    generateArr(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Utility function to print the
# elements of an array
def printArray(arr, n):

    for i in range( n):
        print(arr[i],end= " ")

# Function to generate the array
# with the given operations
def generateArr(arr, n):

    # Base cases
    if (n == 0):
        return
    if (n == 1):
        print( arr[0])
        return

    # To suffixMax[i] will store the maximum
    # element in the subarray arr[i...n-1]
    suffixMax=[0]*n
    suffixMax[n - 1] = arr[n - 1]
    for i in range(n - 2, -1 ,-1):
        suffixMax[i] = max(arr[i], suffixMax[i + 1])

    # To store the minimum element on the left
    minSoFar = arr[0]

    # The first element has no
    # element on its left
    arr[0] = suffixMax[1]

    # From the second element to the
    # second last element
    for i in range( 1,n - 1):

        # Store a copy of the currene element
        temp = arr[i]

        # Absolute difference of the maximum
        # element to the right and the
        # minimum element to the left
        arr[i] = abs(suffixMax[i + 1] - minSoFar)

        # Update the minimum element so far
        minSoFar = min(minSoFar, temp)

    # The last element has no
    # element on its right
    arr[n - 1] = minSoFar

    # Print the updated array
    printArray(arr, n)

# Driver code
if __name__ == "__main__":
    arr = [ 1, 5, 2, 4, 3 ]
    n = len(arr)
    generateArr(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation for above approach
using System;

class GFG
{

// Utility function to print the
// elements of an array
static void printArray(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to generate the array
// with the given operations
static void generateArr(int []arr, int n)
{

    // Base cases
    if (n == 0)
        return;
    if (n == 1)
    {
        Console.Write(arr[0]);
        return;
    }

    // To suffixMax[i] will store the maximum
    // element in the subarray arr[i...n-1]
    int []suffixMax = new int[n];
    suffixMax[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixMax[i] = Math.Max(arr[i],
                                suffixMax[i + 1]);

    // To store the minimum element on the left
    int minSoFar = arr[0];

    // The first element has no
    // element on its left
    arr[0] = suffixMax[1];

    // From the second element to the
    // second last element
    for (int i = 1; i < n - 1; i++)
    {

        // Store a copy of the currene element
        int temp = arr[i];

        // Absolute difference of the maximum
        // element to the right and the
        // minimum element to the left
        arr[i] = Math.Abs(suffixMax[i + 1] -
                                 minSoFar);

        // Update the minimum element so far
        minSoFar = Math.Min(minSoFar, temp);
    }

    // The last element has no
    // element on its right
    arr[n - 1] = minSoFar;

    // Print the updated array
    printArray(arr, n);
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 1, 5, 2, 4, 3 };
    int n = arr.Length;

    generateArr(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation for above approach

    // Utility function to print the
    // elements of an array
    function printArray(arr, n)
    {
        for (let i = 0; i < n; i++)
        {
            document.write(arr[i] + " ");
        }
    }

    // Function to generate the array
    // with the given operations
    function generateArr(arr, n)
    {

        // Base cases
        if (n == 0)
            return;
        if (n == 1)
        {
            document.write(arr[0]);
            return;
        }

        // To suffixMax[i] will store the maximum
        // element in the subarray arr[i...n-1]
        let suffixMax = new Array(n);
        suffixMax.fill(0);
        suffixMax[n - 1] = arr[n - 1];
        for (let i = n - 2; i >= 0; i--)
            suffixMax[i] = Math.max(arr[i], suffixMax[i + 1]);

        // To store the minimum element on the left
        let minSoFar = arr[0];

        // The first element has no
        // element on its left
        arr[0] = suffixMax[1];

        // From the second element to the
        // second last element
        for (let i = 1; i < n - 1; i++)
        {

            // Store a copy of the currene element
            let temp = arr[i];

            // Absolute difference of the maximum
            // element to the right and the
            // minimum element to the left
            arr[i] = Math.abs(suffixMax[i + 1] -
                                     minSoFar);

            // Update the minimum element so far
            minSoFar = Math.min(minSoFar, temp);
        }

        // The last element has no
        // element on its right
        arr[n - 1] = minSoFar;

        // Print the updated array
        printArray(arr, n);
    }

    let arr = [ 1, 5, 2, 4, 3 ];
    let n = arr.length;

    generateArr(arr, n);

</script>
```

**Output:** 

```
5 3 3 2 1
```