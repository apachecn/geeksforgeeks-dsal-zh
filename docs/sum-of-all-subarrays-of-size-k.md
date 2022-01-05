# 大小为 K 的所有子阵列之和

> 原文:[https://www . geeksforgeeks . org/大小为 k 的所有子阵列之和/](https://www.geeksforgeeks.org/sum-of-all-subarrays-of-size-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是计算大小为 K 的所有子数组的和

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，K = 3
> **输出:** 6 9 12 15
> **解释:**
> 大小为 K 的所有子阵列及其和:
> 子阵列 1: {1，2，3} = 1 + 2 + 3 = 6
> 子阵列 2: {2，3，4} = 2 + 3 + 4 = 9
> 子阵列 3: {3，4，5} =
> 
> **输入:** arr[] = {1，-2，3，-4，5，6}，K = 2
> **输出:** -1，1，-1，1，11
> **解释:**
> 大小为 K 的所有子阵列及其和:
> 子阵列 1: {1，-2 } = 1–2 =-1
> 子阵列 2: {-2，3} = -2 + 3 = -1
> 子阵列 3: {3，4} =

**天真方法:**天真方法将是[生成所有大小为 **K** 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并使用迭代找到每个子阵列的和。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the sum
// of all subarrays of size K

#include <iostream>
using namespace std;

// Function to find the sum of
// all subarrays of size K
int calcSum(int arr[], int n, int k)
{

    // Loop to consider every
    // subarray of size K
    for (int i = 0; i <= n - k; i++) {

        // Initialize sum = 0
        int sum = 0;

        // Calculate sum of all elements
        // of current subarray
        for (int j = i; j < k + i; j++)
            sum += arr[j];

        // Print sum of each subarray
        cout << sum << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    // Function Call
    calcSum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum
// of all subarrays of size K
class GFG{

// Function to find the sum of
// all subarrays of size K
static void calcSum(int arr[], int n, int k)
{

    // Loop to consider every
    // subarray of size K
    for (int i = 0; i <= n - k; i++) {

        // Initialize sum = 0
        int sum = 0;

        // Calculate sum of all elements
        // of current subarray
        for (int j = i; j < k + i; j++)
            sum += arr[j];

        // Print sum of each subarray
        System.out.print(sum+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = arr.length;
    int k = 3;

    // Function Call
    calcSum(arr, n, k);
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to find the sum
// of all subarrays of size K
using System;

class GFG 
{

    // Function to find the sum of
    // all subarrays of size K
    static  void calcSum(int[] arr, int n, int k)
    {

        // Loop to consider every
        // subarray of size K
        for (int i = 0; i <= n - k; i++) {

            // Initialize sum = 0
            int sum = 0;

            // Calculate sum of all elements
            // of current subarray
            for (int j = i; j < k + i; j++)
                sum += arr[j];

            // Print sum of each subarray
            Console.Write(sum + " ");
        }
    }

    // Driver Code
    static void Main()
    {
        int[] arr = new int[] { 1, 2, 3, 4, 5, 6 };
        int n = arr.Length;
        int k = 3;

        // Function Call
        calcSum(arr, n, k);

    }
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 implementation to find the sum
# of all subarrays of size K

# Function to find the sum of
# all subarrays of size K
def calcSum(arr, n, k):

    # Loop to consider every
    # subarray of size K
    for i in range(n - k + 1):

        # Initialize sum = 0
        sum = 0

        # Calculate sum of all elements
        # of current subarray
        for j in range(i, k + i):
            sum += arr[j]

        # Prsum of each subarray
        print(sum, end=" ")

# Driver Code
arr=[1, 2, 3, 4, 5, 6]
n = len(arr)
k = 3

# Function Call
calcSum(arr, n, k)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript implementation to find the sum
// of all subarrays of size K

// Function to find the sum of
// all subarrays of size K
function calcSum(arr, n, k)
{

    // Loop to consider every
    // subarray of size K
    for (var i = 0; i <= n - k; i++) {

        // Initialize sum = 0
        var sum = 0;

        // Calculate sum of all elements
        // of current subarray
        for (var j = i; j < k + i; j++)
            sum += arr[j];

        // Print sum of each subarray
        document.write(sum + " ");
    }
}

// Driver Code
var arr = [ 1, 2, 3, 4, 5, 6 ];
var n = arr.length;
var k = 3;

// Function Call
calcSum(arr, n, k);

</script>
```

**Output:** 

```
6 9 12 15
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，有两个循环，第一个循环运行(N–K)次，第二个循环运行 K 次。因此时间复杂性将是 **O(N*K)** 。
*   **辅助空间复杂度:**同上。没有使用额外的空间。因此辅助空间的复杂性将是 **O(1)** 。

**<u>高效方法:使用滑动窗口</u>** 想法是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)方法来寻找阵列中所有可能子阵列的和。

*   对于[0，K]范围内的每个大小，找到大小为 K 的第一个窗口的总和，并将其存储在数组中。
*   然后，对于[K，N]范围内的每个大小，添加下一个有助于滑动窗口的元素，并减去从窗口弹出的元素。

```
// Adding the element which
// adds into the new window
sum = sum + arr[j]

// Subtracting the element which
// pops out from the window
sum = sum - arr[j-k]

where sum is the variable to store the result
      arr is the given array
      j is the loop variable in range [K, N]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the sum
// of all subarrays of size K

#include <iostream>
using namespace std;

// Function to find the sum of
// all subarrays of size K
int calcSum(int arr[], int n, int k)
{
    // Initialize sum = 0
    int sum = 0;

    // Consider first subarray of size k
    // Store the sum of elements
    for (int i = 0; i < k; i++)
        sum += arr[i];

    // Print the current sum
    cout << sum << " ";

    // Consider every subarray of size k
    // Remove first element and add current
    // element to the window
    for (int i = k; i < n; i++) {

        // Add the element which enters
        // into the window and subtract
        // the element which pops out from
        // the window of the size K
        sum = (sum - arr[i - k]) + arr[i];

        // Print the sum of subarray
        cout << sum << " ";
    }
}

// Drivers Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    // Function Call
    calcSum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum
// of all subarrays of size K
class GFG{

// Function to find the sum of
// all subarrays of size K
static void calcSum(int arr[], int n, int k)
{
    // Initialize sum = 0
    int sum = 0;

    // Consider first subarray of size k
    // Store the sum of elements
    for (int i = 0; i < k; i++)
        sum += arr[i];

    // Print the current sum
    System.out.print(sum+ " ");

    // Consider every subarray of size k
    // Remove first element and add current
    // element to the window
    for (int i = k; i < n; i++) {

        // Add the element which enters
        // into the window and subtract
        // the element which pops out from
        // the window of the size K
        sum = (sum - arr[i - k]) + arr[i];

        // Print the sum of subarray
        System.out.print(sum+ " ");
    }
}

// Drivers Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = arr.length;
    int k = 3;

    // Function Call
    calcSum(arr, n, k);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the sum
# of all subarrays of size K

# Function to find the sum of
# all subarrays of size K
def calcSum(arr, n, k):

    # Initialize sum = 0
    sum = 0

    # Consider first subarray of size k
    # Store the sum of elements
    for i in range( k):
        sum += arr[i]

    # Print the current sum
    print( sum ,end= " ")

    # Consider every subarray of size k
    # Remove first element and add current
    # element to the window
    for i in range(k,n):

        # Add the element which enters
        # into the window and subtract
        # the element which pops out from
        # the window of the size K
        sum = (sum - arr[i - k]) + arr[i]

        # Print the sum of subarray
        print( sum ,end=" ")

# Drivers Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5, 6 ]
    n = len(arr)
    k = 3

    # Function Call
    calcSum(arr, n, k)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the sum
// of all subarrays of size K
using System;

class GFG{

// Function to find the sum of
// all subarrays of size K
static void calcSum(int []arr, int n, int k)
{
    // Initialize sum = 0
    int sum = 0;

    // Consider first subarray of size k
    // Store the sum of elements
    for (int i = 0; i < k; i++)
        sum += arr[i];

    // Print the current sum
    Console.Write(sum+ " ");

    // Consider every subarray of size k
    // Remove first element and add current
    // element to the window
    for (int i = k; i < n; i++) {

        // Add the element which enters
        // into the window and subtract
        // the element which pops out from
        // the window of the size K
        sum = (sum - arr[i - k]) + arr[i];

        // Print the sum of subarray
        Console.Write(sum + " ");
    }
}

// Drivers Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6 };
    int n = arr.Length;
    int k = 3;

    // Function Call
    calcSum(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find the sum
// of all subarrays of size K

// Function to find the sum of
// all subarrays of size K
function calcSum(arr, n, k)
{

    // Initialize sum = 0
    var sum = 0;

    // Consider first subarray of size k
    // Store the sum of elements
    for (var i = 0; i < k; i++)
        sum += arr[i];

    // Print the current sum
    document.write( sum + " ");

    // Consider every subarray of size k
    // Remove first element and add current
    // element to the window
    for (var i = k; i < n; i++) {

        // Add the element which enters
        // into the window and subtract
        // the element which pops out from
        // the window of the size K
        sum = (sum - arr[i - k]) + arr[i];

        // Print the sum of subarray
        document.write( sum + " ");
    }
}

// Drivers Code
var arr = [ 1, 2, 3, 4, 5, 6 ];
var n = arr.length;
var k = 3;

// Function Call
calcSum(arr, n, k);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
6 9 12 15
```

**性能分析:**

*   **时间复杂度:**同上。有一个循环需要 0(N)时间。因此时间复杂性将是 **O(N)** 。
*   **辅助空间复杂度:**同上。没有使用额外的空间。因此辅助空间的复杂性将是 **O(1)** 。