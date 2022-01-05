# 打印出现 N / K 次以上的所有数组元素

> 原文:[https://www . geeksforgeeks . org/print-all-array-elements-being-more-n-k-times/](https://www.geeksforgeeks.org/print-all-array-elements-appearing-more-than-n-k-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找出出现次数超过 **(N / K)** 次的所有数组元素。

**示例:**

> **输入:** arr[] = { 1，2，6，6，6，6，6，10 }，K = 4
> **输出:** 6
> **说明:**
> 数组中 6 的频率大于 N / K(= 2)。因此，所需的输出为 6。
> 
> **输入:** arr[] = { 3，4，4，5，5，5，5 }，K = 4
> **输出:** 4 5
> **说明:**
> 数组中 4 的频率大于 N / K(= 1)。
> 数组中 5 的频率大于 N / K(= 1)。
> 因此，要求的输出是 4 5。

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个不同的数组元素，统计其频率，检查是否超过 **N / K** 。如果发现为真，则打印数组元素。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

[**排序**](https://www.geeksforgeeks.org/sorting-algorithms/)**基于方法的思路是[排序数组](https://www.geeksforgeeks.org/sort-c-stl/)，然后[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，通过检查相邻元素是否相等来计算每个不同数组元素的频率。如果发现数组元素的频率大于 **N / K** ，则打印数组元素。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print all array elements
// whose frequency is greater than N / K
void NDivKWithFreq(int arr[], int N, int K)
{
    // Sort the array, arr[]
    sort(arr, arr + N);

    // Traverse the array
    for (int i = 0; i < N;) {

        // Stores frequency of arr[i]
        int cnt = 1;

        // Traverse array elements which
        // is equal to arr[i]
        while ((i + 1) < N
               && arr[i] == arr[i + 1]) {

            // Update cnt
            cnt++;

            // Update i
            i++;
        }

        // If frequency of arr[i] is
        // greater than (N / K)
        if (cnt > (N / K)) {

            cout << arr[i] << " ";
        }
        i++;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 6, 6, 6, 6, 7, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;

    NDivKWithFreq(arr, N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print all array elements
// whose frequency is greater than N / K
static void NDivKWithFreq(int arr[], int N, int K)
{
    // Sort the array, arr[]
    Arrays.sort(arr);

    // Traverse the array
    for (int i = 0; i < N;) {

        // Stores frequency of arr[i]
        int cnt = 1;

        // Traverse array elements which
        // is equal to arr[i]
        while ((i + 1) < N
               && arr[i] == arr[i + 1]) {

            // Update cnt
            cnt++;

            // Update i
            i++;
        }

        // If frequency of arr[i] is
        // greater than (N / K)
        if (cnt > (N / K)) {

            System.out.print(arr[i]+ " ");
        }
        i++;
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 6, 6, 6, 6, 7, 10 };
    int N = arr.length;
    int K = 4;

    NDivKWithFreq(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to prall array elements
# whose frequency is greater than N / K
def NDivKWithFreq(arr, N, K):

    # Sort the array, arr[]
    arr = sorted(arr)

    # Traverse the array
    i = 0

    while i < N:

        # Stores frequency of arr[i]
        cnt = 1

        # Traverse array elements which
        # is equal to arr[i]
        while ((i + 1) < N and
               arr[i] == arr[i + 1]):

            # Update cnt
            cnt += 1

            # Update i
            i += 1

        # If frequency of arr[i] is
        # greater than (N / K)
        if (cnt > (N // K)):
            print(arr[i], end = " ")

        i += 1

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 2, 6, 6, 6, 6, 7, 10 ]
    N = len(arr)
    K = 4

    NDivKWithFreq(arr, N, K)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to print all array elements
// whose frequency is greater than N / K
static void NDivKWithFreq(int[] arr, int N,
                          int K)
{

    // Sort the array, arr[]
    Array.Sort(arr);

    // Traverse the array
    for(int i = 0; i < N;)
    {

        // Stores frequency of arr[i]
        int cnt = 1;

        // Traverse array elements which
        // is equal to arr[i]
        while ((i + 1) < N &&
               arr[i] == arr[i + 1])
        {

            // Update cnt
            cnt++;

            // Update i
            i++;
        }

        // If frequency of arr[i] is
        // greater than (N / K)
        if (cnt > (N / K))
        {
            Console.Write(arr[i] + " ");
        }
        i++;
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 2, 6, 6, 6, 6, 7, 10 };
    int N = arr.Length;
    int K = 4;

    NDivKWithFreq(arr, N, K);
}
}

// This code is contributed by code_hunt
```

## **java 描述语言**

```
<script>

// JavaScript program for above approach

// Function to print all array elements
// whose frequency is greater than N / K
function NDivKWithFreq(arr, N, K)
{
    // Sort the array, arr[]
    arr.sort();

    // Traverse the array
    for (let i = 0; i < N;) {

        // Stores frequency of arr[i]
        let cnt = 1;

        // Traverse array elements which
        // is equal to arr[i]
        while ((i + 1) < N
               && arr[i] == arr[i + 1]) {

            // Update cnt
            cnt++;

            // Update i
            i++;
        }

        // If frequency of arr[i] is
        // greater than (N / K)
        if (cnt > (N / K)) {

            document.write(arr[i]+ " ");
        }
        i++;
    }
}

// Driver Code

    let arr = [1, 2, 2, 6, 6, 6, 6, 7, 10 ];
    let N = arr.length;
    let K = 4;

    NDivKWithFreq(arr, N, K);

</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:**O(N * log<sub>2</sub>N)*
***辅助空间:** O(1)***

**[**【二分搜索法】**](https://www.geeksforgeeks.org/binary-search/)**-基于方法:**使用[二分搜索法手法](https://www.geeksforgeeks.org/binary-search/)可以解决问题。其思想是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，通过计算数组元素的[上限](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/)来统计每个不同数组元素的频率。最后检查阵元频率是否大于 **N / K** 。如果发现为真，则打印数组元素。按照以下步骤解决问题:**

*   **[排序数组](https://www.geeksforgeeks.org/sort-c-stl/)， **arr[]** 。**
*   **[使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，找到**arr【I】**的[上界](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/)，说 **X** ，检查**(X–I)**是否大于 **N / K** 。如果发现为真，则打印 **arr[i]** 。**
*   **最后更新 **i = X** 。**

## **C++**

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to+ find the upper_bound of
// an array element
int upperBound(int arr[], int N, int K)
{

    // Stores minimum index
    // in which K lies
    int l = 0;

    // Stores maximum index
    // in which K lies
    int r = N;

    // Calculate the upper
    // bound of K
    while (l < r) {

        // Stores mid element
        // of l and r
        int mid = (l + r) / 2;

        // If arr[mid] is less
        // than or equal to K
        if (arr[mid] <= K) {

            // Right subarray
            l = mid + 1;
        }

        else {

            // Left subarray
            r = mid;
        }
    }
    return l;
}

// Function to print all array elements
// whose frequency is greater than N / K
void NDivKWithFreq(int arr[], int N, int K)
{

    // Sort the array arr[]
    sort(arr, arr + N);

    // Stores index of
    // an array element
    int i = 0;

    // Traverse the array
    while (i < N) {

        // Stores upper bound of arr[i]
        int X = upperBound(arr, N, arr[i]);

        // If frequency of arr[i] is
        // greater than N / 4
        if ((X - i) > N / 4) {

            cout << arr[i] << " ";
        }

        // Update i
        i = X;
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 2, 6, 6, 6, 6, 7, 10 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 4;

    // Function Call
    NDivKWithFreq(arr, N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to+ find the upper_bound of
// an array element
static int upperBound(int arr[], int N, int K)
{

    // Stores minimum index
    // in which K lies
    int l = 0;

    // Stores maximum index
    // in which K lies
    int r = N;

    // Calculate the upper
    // bound of K
    while (l < r)
    {

        // Stores mid element
        // of l and r
        int mid = (l + r) / 2;

        // If arr[mid] is less
        // than or equal to K
        if (arr[mid] <= K)
        {

            // Right subarray
            l = mid + 1;
        }

        else
        {

            // Left subarray
            r = mid;
        }
    }
    return l;
}

// Function to print all array elements
// whose frequency is greater than N / K
static void NDivKWithFreq(int arr[], int N, int K)
{

    // Sort the array arr[]
    Arrays.sort(arr);

    // Stores index of
    // an array element
    int i = 0;

    // Traverse the array
    while (i < N)
    {

        // Stores upper bound of arr[i]
        int X = upperBound(arr, N, arr[i]);

        // If frequency of arr[i] is
        // greater than N / 4
        if ((X - i) > N / 4)
        {

            System.out.print(arr[i] + " ");
        }

        // Update i
        i = X;
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 1, 2, 2, 6, 6, 6, 6, 7, 10 };

    // Size of array
    int N = arr.length;
    int K = 4;

    // Function Call
    NDivKWithFreq(arr, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# Python program to implement
# the above approach

# Function to+ find the upper_bound of
# an array element
def upperBound(arr, N, K):

  # Stores minimum index
    # in which K lies
    l = 0;

    # Stores maximum index
    # in which K lies
    r = N;

    # Calculate the upper
    # bound of K
    while (l < r):

        # Stores mid element
        # of l and r
        mid = (l + r) // 2;

        # If arr[mid] is less
        # than or equal to K
        if (arr[mid] <= K):

            # Right subarray
            l = mid + 1;
        else:

            # Left subarray
            r = mid;
    return l;

# Function to prall array elements
# whose frequency is greater than N / K
def NDivKWithFreq(arr, N, K):

  # Sort the array arr
    arr.sort();

    # Stores index of
    # an array element
    i = 0;

    # Traverse the array
    while (i < N):

        # Stores upper bound of arr[i]
        X = upperBound(arr, N, arr[i]);

        # If frequency of arr[i] is
        # greater than N / 4
        if ((X - i) > N // 4):
            print(arr[i], end="");

        # Update i
        i = X;

# Driver Code
if __name__ == '__main__':

    # Given array arr
    arr = [1, 2, 2, 6, 6, 6, 6, 7, 10];

    # Size of array
    N = len(arr);
    K = 4;

    # Function Call
    NDivKWithFreq(arr, N, K);

    # This code is contributed by 29AjayKumar
```

## **C#**

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to+ find the upper_bound of
  // an array element
  static int upperBound(int []arr, int N, int K)
  {

    // Stores minimum index
    // in which K lies
    int l = 0;

    // Stores maximum index
    // in which K lies
    int r = N;

    // Calculate the upper
    // bound of K
    while (l < r)
    {

      // Stores mid element
      // of l and r
      int mid = (l + r) / 2;

      // If arr[mid] is less
      // than or equal to K
      if (arr[mid] <= K)
      {

        // Right subarray
        l = mid + 1;
      }

      else
      {

        // Left subarray
        r = mid;
      }
    }
    return l;
  }

  // Function to print all array elements
  // whose frequency is greater than N / K
  static void NDivKWithFreq(int []arr, int N, int K)
  {

    // Sort the array arr[]
    Array.Sort(arr);

    // Stores index of
    // an array element
    int i = 0;

    // Traverse the array
    while (i < N)
    {

      // Stores upper bound of arr[i]
      int X = upperBound(arr, N, arr[i]);

      // If frequency of arr[i] is
      // greater than N / 4
      if ((X - i) > N / 4)
      {

        Console.Write(arr[i] + " ");
      }

      // Update i
      i = X;
    }
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given array arr[]
    int []arr = { 1, 2, 2, 6, 6, 6, 6, 7, 10 };

    // Size of array
    int N = arr.Length;
    int K = 4;

    // Function Call
    NDivKWithFreq(arr, N, K);
  }
}

// This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
// Javascript program to implement
// the above approach

//function to sort the array
function sortt(number)
{
var n= number.length;
    for (i = 0; i < n; ++i)
        {
             for (j = i + 1; j < n; ++j)
            {
                 if (number[i] > number[j])
                {
                     a =  number[i];
                    number[i] = number[j];
                    number[j] = a;
                 }
             }
         }
}

// Function to find the upper_bound of
// an array element
function upperBound( arr, N, K)
{

    // Stores minimum index
    // in which K lies
    var l = 0;

    // Stores maximum index
    // in which K lies
    var r = N;

    // Calculate the upper
    // bound of K
    while (l < r) {

        // Stores mid element
        // of l and r
        var mid = parseInt((l + r) / 2);

        // If arr[mid] is less
        // than or equal to K
        if (arr[mid] <= K) {

            // Right subarray
            l = mid + 1;
        }

        else {

            // Left subarray
            r = mid;
        }
    }
    return l;
}

// Function to print all array elements
// whose frequency is greater than N / K
function NDivKWithFreq(arr, N, K)
{

    // Sort the array arr[]
    sortt(arr);

    // Stores index of
    // an array element
    var i = 0;

    // Traverse the array
    while (i < N) {

        // Stores upper bound of arr[i]
        var X = upperBound(arr, N, arr[i]);

        // If frequency of arr[i] is
        // greater than N / 4
        if ((X - i) > parseInt(N / 4)) {

            document.write( arr[i] + " ");
        }

        // Update i
        i = X;
    }
}

    // Given array arr[]
    var arr = [ 1, 2, 2, 6, 6, 6, 6, 7, 10 ];

    // Size of array
    var N = arr.length;

    var K = 4;

    // Function Call
    NDivKWithFreq(arr, N, K);

//This code in contributed by SoumikMondal
</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:**O(N * log<sub>2</sub>N)*
***辅助空间:** O(1)***

#### **另一种方法:使用内置的 Python 函数:**

*   **使用 [**【计数器()**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能计算每个元素的频率。**
*   **遍历频率数组，打印 n/k 次以上出现的所有元素。**

**下面是实现:**

## **蟒蛇 3**

```
# Python3 implementation
from collections import Counter

# Function to find the number of array
# elements with frequency more than n/k times
def printElements(arr, n, k):

    # Calculating n/k
    x = n//k

    # Counting frequency of every
    # element using Counter
    mp = Counter(arr)

    # Traverse the map and print all
    # the elements with occurrence atleast n/k times
    for it in mp:
        if mp[it] > x:
            print(it)

# Driver code
arr = [1, 2, 2, 6, 6, 6, 6, 7, 10]

# Size of array
n = len(arr)
k = 4

printElements(arr, n, k)

# This code is contributed by vikkycirus
```

****输出:****

```
6
```

****时间复杂度:** O(N)**

****辅助空间:** O(N)**

****高效方法:**为了优化上述方法，想法是将每个不同数组元素的频率存储到[图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)中。最后，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，检查其频率是否大于 **(N / K)** 。如果发现为真，则打印数组元素。关于该方法的讨论，请参考本文。**

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**