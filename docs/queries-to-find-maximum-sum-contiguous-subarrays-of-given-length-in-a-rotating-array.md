# 在旋转阵列中查找给定长度的最大和连续子阵列的查询

> 原文:[https://www . geeksforgeeks . org/查询查找旋转数组中给定长度的最大和连续子数组/](https://www.geeksforgeeks.org/queries-to-find-maximum-sum-contiguous-subarrays-of-given-length-in-a-rotating-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和以下两种类型的表单 **{X，Y}** 的 **Q** 个查询:

*   如果 **X = 1** ，将给定阵列向左旋转 **Y** 位置。
*   如果 **X = 2** ，打印当前阵列状态下长度 **Y** 的[最大和子阵列](https://www.geeksforgeeks.org/maximum-subarray-sum-using-divide-and-conquer-algorithm/)。

**示例:**

> **输入:** N = 5，arr[] = {1，2，3，4，5}，Q = 2，Query[][] = {{1，2}，{2，3}}
> **输出:**
> 查询 1: 3 4 5 1 2
> 查询 2: 12
> **解释:**
> 查询 1:向左移动数组 2 次:{1，2，3，4，5} - > {2，3，4，5
> 
> **输入:** N = 5，arr[] = {3，4，5，1，2}，Q = 3，Query[][] = {{1，3}，{1，1}，{2，4}}
> **输出:**
> 查询 1:1 2 3 4
> 查询 2: 2 3 4 5 1
> 查询 3: 14
> **解释:**
> 查询 1:向左移位数组 3 次:{3，4，5 4} - > {1，2，3，4，5}
> 查询 2:向左移动数组 1 次:{1，2，3，4，5} - > {2，3，4，5，1}
> 查询 3:长度为 4 的子数组的最大和为{2，3，4，5}，和为 14

**简单方法:**最简单的方法是[旋转数组](https://www.geeksforgeeks.org/array-rotation/)通过将元素一个接一个地移动到距离 **Y** 进行查询是**类型 1** 和[生成长度为 Y](https://www.geeksforgeeks.org/sum-of-all-subarrays-of-size-k/) 的所有子数组的和，如果查询是**类型 2** 则打印最大和。
***时间复杂度:**O(Q * N * Y)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，思路是使用[杂耍算法](https://www.geeksforgeeks.org/array-rotation/)进行阵列旋转，并使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)寻找长度的最大和子阵列 **Y** 。按照以下步骤解决问题:

1.  如果 **X = 1** ，使用[杂耍算法](https://www.geeksforgeeks.org/array-rotation/)将阵列旋转 **Y** 。
2.  否则，如果 **X = 2** ，[使用滑动窗口技术找到长度为 Y](https://www.geeksforgeeks.org/window-sliding-technique/) 的最大和子阵。
3.  如果查询 **X** 为 **1** ，则打印数组。
4.  否则，打印尺寸 **Y** 的最大和子阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the maximum
// sum of length k
int MaxSum(vector<int> arr, int n,
           int k)
{
    int i, max_sum = 0, sum = 0;

    // Calculating the max sum for
    // the first k elements
    for (i = 0; i < k; i++) {
        sum += arr[i];
    }
    max_sum = sum;

    // Find subarray with maximum sum
    while (i < n) {

        // Update the sum
        sum = sum - arr[i - k] + arr[i];
        if (max_sum < sum) {
            max_sum = sum;
        }
        i++;
    }

    // Return maximum sum
    return max_sum;
}

// Function to calculate gcd of the
// two numbers n1 and n2
int gcd(int n1, int n2)
{
    // Base Case
    if (n2 == 0) {
        return n1;
    }

    // Recursively find the GCD
    else {
        return gcd(n2, n1 % n2);
    }
}

// Function to rotate the array by Y
vector<int> RotateArr(vector<int> arr,
                      int n, int d)
{
    // For handling k >= N
    int i = 0, j = 0;
    d = d % n;

    // Dividing the array into
    // number of sets
    int no_of_sets = gcd(d, n);

    for (i = 0; i < no_of_sets; i++) {

        int temp = arr[i];
        j = i;

        // Rotate the array by Y
        while (true) {

            int k = j + d;

            if (k >= n)
                k = k - n;

            if (k == i)
                break;

            arr[j] = arr[k];
            j = k;
        }

        // Update arr[j]
        arr[j] = temp;
    }

    // Return the rotated array
    return arr;
}

// Function that performs the queries
// on the given array
void performQuery(vector<int>& arr,
                  int Q[][2], int q)
{

    int N = (int)arr.size();

    // Traverse each query
    for (int i = 0; i < q; i++) {

        // If query of type X = 1
        if (Q[i][0] == 1) {

            arr = RotateArr(arr, N,
                            Q[i][1]);

            // Print the array
            for (auto t : arr) {
                cout << t << " ";
            }
            cout << "\n";
        }

        // If query of type X = 2
        else {
            cout << MaxSum(arr, N, Q[i][1])
                 << "\n";
        }
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 1, 2, 3, 4, 5 };

    int q = 5;

    // Given Queries
    int Q[][2] = { { 1, 2 }, { 2, 3 },
                   { 1, 3 }, { 1, 1 },
                   { 2, 4 }
    };

    // Function Call
    performQuery(arr, Q, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Function to calculate the maximum
// sum of length k
static int MaxSum(int []arr,
                  int n, int k)
{
  int i, max_sum = 0, sum = 0;

  // Calculating the max sum for
  // the first k elements
  for (i = 0; i < k; i++)
  {
    sum += arr[i];
  }
  max_sum = sum;

  // Find subarray with maximum sum
  while (i < n)
  {
    // Update the sum
    sum = sum - arr[i - k] +
                arr[i];
    if (max_sum < sum)
    {
      max_sum = sum;
    }
    i++;
  }

  // Return maximum sum
  return max_sum;
}

// Function to calculate gcd
//  of the two numbers n1 and n2
static int gcd(int n1, int n2)
{
  // Base Case
  if (n2 == 0)
  {
    return n1;
  }

  // Recursively find the GCD
  else
  {
    return gcd(n2, n1 % n2);
  }
}

// Function to rotate the array by Y
static int []RotateArr(int []arr,
                       int n, int d)
{
  // For handling k >= N
  int i = 0, j = 0;
  d = d % n;

  // Dividing the array into
  // number of sets
  int no_of_sets = gcd(d, n);

  for (i = 0; i < no_of_sets; i++)
  {
    int temp = arr[i];
    j = i;

    // Rotate the array by Y
    while (true)
    {
      int k = j + d;

      if (k >= n)
        k = k - n;

      if (k == i)
        break;

      arr[j] = arr[k];
      j = k;
    }

    // Update arr[j]
    arr[j] = temp;
  }

  // Return the rotated array
  return arr;
}

// Function that performs the queries
// on the given array
static void performQuery(int []arr,
                         int Q[][], int q)
{
  int N = arr.length;

  // Traverse each query
  for (int i = 0; i < q; i++)
  {
    // If query of type X = 1
    if (Q[i][0] == 1)
    {
      arr = RotateArr(arr, N,
                      Q[i][1]);

      // Print the array
      for (int t : arr)
      {
        System.out.print(t + " ");
      }
      System.out.print("\n");
    }

    // If query of type X = 2
    else
    {
      System.out.print(MaxSum(arr, N,
                              Q[i][1]) + "\n");
    }
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int []arr = {1, 2, 3, 4, 5};

  int q = 5;

  // Given Queries
  int Q[][] = {{1, 2}, {2, 3},
               {1, 3}, {1, 1},
               {2, 4}};

  // Function Call
  performQuery(arr, Q, q);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the maximum
# sum of length k
def MaxSum(arr, n, k):

    i, max_sum = 0, 0
    sum = 0

    # Calculating the max sum for
    # the first k elements
    while i < k:
        sum += arr[i]
        i += 1

    max_sum = sum

    # Find subarray with maximum sum
    while (i < n):

        # Update the sum
        sum = sum - arr[i - k] + arr[i]

        if (max_sum < sum):
            max_sum = sum

        i += 1

    # Return maximum sum
    return max_sum

# Function to calculate gcd of the
# two numbers n1 and n2
def gcd(n1, n2):

    # Base Case
    if (n2 == 0):
        return n1

    # Recursively find the GCD
    else:
        return gcd(n2, n1 % n2)

# Function to rotate the array by Y
def RotateArr(arr, n, d):

    # For handling k >= N
    i = 0
    j = 0
    d = d % n

    # Dividing the array into
    # number of sets
    no_of_sets = gcd(d, n)

    for i in range(no_of_sets):
        temp = arr[i]
        j = i

        # Rotate the array by Y
        while (True):
            k = j + d

            if (k >= n):
                k = k - n
            if (k == i):
                break

            arr[j] = arr[k]
            j = k

        # Update arr[j]
        arr[j] = temp

    # Return the rotated array
    return arr

# Function that performs the queries
# on the given array
def performQuery(arr, Q, q):

    N = len(arr)

    # Traverse each query
    for i in range(q):

        # If query of type X = 1
        if (Q[i][0] == 1):
            arr = RotateArr(arr, N, Q[i][1])

            # Print the array
            for t in arr:
                print(t, end = " ")

            print()

        # If query of type X = 2
        else:
            print(MaxSum(arr, N, Q[i][1]))

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3, 4, 5 ]

    q = 5

    # Given Queries
    Q = [ [ 1, 2 ], [ 2, 3 ],
          [ 1, 3 ], [ 1, 1 ],
          [ 2, 4 ] ]

    # Function call
    performQuery(arr, Q, q)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to calculate the maximum
// sum of length k
static int MaxSum(int[] arr, int n,
                             int k)
{
    int i, max_sum = 0, sum = 0;

    // Calculating the max sum for
    // the first k elements
    for(i = 0; i < k; i++)
    {
        sum += arr[i];
    }
    max_sum = sum;

    // Find subarray with maximum sum
    while (i < n)
    {

        // Update the sum
        sum = sum - arr[i - k] +
                    arr[i];

        if (max_sum < sum)
        {
            max_sum = sum;
        }
        i++;
    }

    // Return maximum sum
    return max_sum;
}

// Function to calculate gcd
//  of the two numbers n1 and n2
static int gcd(int n1, int n2)
{

    // Base Case
    if (n2 == 0)
    {
        return n1;
    }

    // Recursively find the GCD
    else
    {
        return gcd(n2, n1 % n2);
    }
}

// Function to rotate the array by Y
static int []RotateArr(int []arr, int n,
                                  int d)
{

    // For handling k >= N
    int i = 0, j = 0;
    d = d % n;

    // Dividing the array into
    // number of sets
    int no_of_sets = gcd(d, n);

    for(i = 0; i < no_of_sets; i++)
    {
        int temp = arr[i];
        j = i;

        // Rotate the array by Y
        while (true)
        {
            int k = j + d;

            if (k >= n)
                k = k - n;

            if (k == i)
                break;

            arr[j] = arr[k];
            j = k;
        }

        // Update arr[j]
        arr[j] = temp;
    }

    // Return the rotated array
    return arr;
}

// Function that performs the queries
// on the given array
static void performQuery(int[] arr,
                         int[,] Q, int q)
{
    int N = arr.Length;

    // Traverse each query
    for(int i = 0; i < q; i++)
    {

        // If query of type X = 1
        if (Q[i, 0] == 1)
        {
            arr = RotateArr(arr, N,
                            Q[i, 1]);

            // Print the array
            for(int t = 0; t < arr.Length; t++)
            {
                Console.Write(arr[t] + " ");
            }
            Console.WriteLine();
        }

        // If query of type X = 2
        else
        {
            Console.WriteLine(MaxSum(arr, N,
                                     Q[i, 1]));
        }
    }
}

// Driver code
static void Main()
{

    // Given array arr[]
    int[] arr = { 1, 2, 3, 4, 5 };

    int q = 5;

    // Given Queries
    int[,] Q = { { 1, 2 }, { 2, 3 },
                 { 1, 3 }, { 1, 1 },
                 { 2, 4 } };

    // Function call
    performQuery(arr, Q, q);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// javascript program for
// the above approach   
// Function to calculate the maximum
    // sum of length k
    function MaxSum(arr , n , k) {
        var i, max_sum = 0, sum = 0;

        // Calculating the max sum for
        // the first k elements
        for (i = 0; i < k; i++) {
            sum += arr[i];
        }
        max_sum = sum;

        // Find subarray with maximum sum
        while (i < n) {
            // Update the sum
            sum = sum - arr[i - k] + arr[i];
            if (max_sum < sum) {
                max_sum = sum;
            }
            i++;
        }

        // Return maximum sum
        return max_sum;
    }

    // Function to calculate gcd
    // of the two numbers n1 and n2
    function gcd(n1 , n2) {
        // Base Case
        if (n2 == 0) {
            return n1;
        }

        // Recursively find the GCD
        else {
            return gcd(n2, n1 % n2);
        }
    }

    // Function to rotate the array by Y
    function RotateArr(arr , n , d) {
        // For handling k >= N
        var i = 0, j = 0;
        d = d % n;

        // Dividing the array into
        // number of sets
        var no_of_sets = gcd(d, n);

        for (i = 0; i < no_of_sets; i++) {
            var temp = arr[i];
            j = i;

            // Rotate the array by Y
            while (true) {
                var k = j + d;

                if (k >= n)
                    k = k - n;

                if (k == i)
                    break;

                arr[j] = arr[k];
                j = k;
            }

            // Update arr[j]
            arr[j] = temp;
        }

        // Return the rotated array
        return arr;
    }

    // Function that performs the queries
    // on the given array
    function performQuery(arr , Q , q) {
        var N = arr.length;

        // Traverse each query
        for (i = 0; i < q; i++) {
            // If query of type X = 1
            if (Q[i][0] == 1) {
                arr = RotateArr(arr, N, Q[i][1]);

                // Print var the array
                for (var t =0 ;t< arr.length;t++) {
                    document.write(arr[t] + " ");
                }
                document.write("<br/>");
            }

            // If query of type X = 2
            else {
                document.write(MaxSum(arr, N, Q[i][1]) + "<br/>");
            }
        }
    }

    // Driver Code

        // Given array arr
        var arr = [ 1, 2, 3, 4, 5 ];

        var q = 5;

        // Given Queries
        var Q = [ [ 1, 2 ], [ 2, 3 ], [ 1, 3 ], [ 1, 1 ], [ 2, 4 ] ];

        // Function Call
        performQuery(arr, Q, q);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
3 4 5 1 2 
12
1 2 3 4 5 
2 3 4 5 1 
14
```

***时间复杂度:** O(Q*N)，其中 Q 是查询数量*，*N 是给定数组的大小。*
***辅助空间:** O(N)*