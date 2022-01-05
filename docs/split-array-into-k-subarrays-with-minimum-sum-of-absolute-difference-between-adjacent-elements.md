# 将阵列拆分为 K 个子阵列，相邻元素绝对差之和最小

> 原文:[https://www . geeksforgeeks . org/将数组拆分为 k 个子数组-相邻元素之间的绝对差之和最小/](https://www.geeksforgeeks.org/split-array-into-k-subarrays-with-minimum-sum-of-absolute-difference-between-adjacent-elements/)

给定一个大小为 **N** 的[阵列、](https://www.geeksforgeeks.org/array-data-structure/)T2【arr】和一个整数 **K** ，任务是将该阵列分割成 **K** [子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，最小化每个子阵列相邻元素之间的绝对差之和。

**示例:**

> **输入:** arr[] = {1，3，-2，5，-1}，K = 2
> **输出:** 13
> **解释:**将阵列拆分为以下 2 个子阵列:{1，3，-2}和{5，-1}。
> 
> **输入:** arr[] = {2，14，26，10，5，12}，K = 3
> **输出:** 24
> **解释:**将阵列拆分为以下 3 个子阵列:{2，14}，{26}，{10，5，12}。

**方法:**给定的问题可以基于以下观察来解决:

> 其思想是在给出相邻元素最大绝对差的第一个索引处对数组 **arr[]** 进行切片。从结果中减去它。在**K–1**处进行切片，将得到相邻元素绝对差之和最小的 **K** 子阵列。

按照以下步骤解决问题:

1.  初始化一个数组，比如说 **new_Arr[]** ，和一个整数变量，比如说 **ans** ，来存储总的绝对差和。
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
    *   存储相邻元素的绝对差，比如 **new_Arr[]** 数组中的 **arr[i+1]** 和 **arr[i]** 。
    *   将**和**增加 **arr[i]** 和 **arr[i + 1]** 的绝对差值
3.  [按降序排列**新 _Arr[]** 数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
4.  [从 **i = 0** 到 **i = K-1** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
    *   递减年由 **new_Arr[i]。**
5.  最后，打印 **ans。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to split an array into K subarrays
// with minimum sum of absolute difference
// of adjacent elements in each of K subarrays
void absoluteDifference(int arr[], int N, int K)
{

    // Stores the absolute differences
    // of adjacent elements
    int new_Arr[N - 1];

    // Stores the answer
    int ans = 0;

    // Stores absolute differences of
    // adjacent elements in new_Arr
    for (int i = 0; i < N - 1; i++) {
        new_Arr[i] = abs(arr[i] - arr[i + 1]);

        // Stores the sum of all absolute
        // differences of adjacent elements
        ans += new_Arr[i];
    }

    // Sorting the new_Arr
    // in decreasing order
    sort(new_Arr, new_Arr + N - 1,
         greater<int>());

    for (int i = 0; i < K - 1; i++) {

        // Removing K - 1 elements
        // with maximum sum
        ans -= new_Arr[i];
    }

    // Prints the answer
    cout << ans << endl;
}

// Driver code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 3, -2, 5, -1 };

    // Given K
    int K = 2;

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    absoluteDifference(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  java program for the above approach
import java.util.*;
import java.util.Arrays;
class GFG
{

 public static void reverse(int[] array)
 {

   // Length of the array
   int n = array.length;

   // Swaping the first half elements with last half
   // elements
   for (int i = 0; i < n / 2; i++)
   {

     // Storing the first half elements temporarily
     int temp = array[i];

     // Assigning the first half to the last half
     array[i] = array[n - i - 1];

     // Assigning the last half to the first half
     array[n - i - 1] = temp;
   }
 }

  // Function to split an array into K subarrays
  // with minimum sum of absolute difference
  // of adjacent elements in each of K subarrays
  public static void absoluteDifference(int arr[],
                                        int N, int K)
  {

    // Stores the absolute differences
    // of adjacent elements
    int new_Arr[] = new int[N - 1];

    // Stores the answer
    int ans = 0;

    // Stores absolute differences of
    // adjacent elements in new_Arr
    for (int i = 0; i < N - 1; i++)
    {
      new_Arr[i] = Math.abs(arr[i] - arr[i + 1]);

      // Stores the sum of all absolute
      // differences of adjacent elements
      ans += new_Arr[i];
    }

    // Sorting the new_Arr
    // in decreasing order
    Arrays.sort(new_Arr);
    reverse(new_Arr);

    for (int i = 0; i < K - 1; i++)
    {

      // Removing K - 1 elements
      // with maximum sum
      ans -= new_Arr[i];
    }

    // Prints the answer
    System.out.println(ans);
  }

  // Driver code
  public static void main (String[] args)
  {

    // Given array arr[]
    int arr[] = { 1, 3, -2, 5, -1 };

    // Given K
    int K = 2;

    // Size of array
    int N = arr.length;

    // Function Call
    absoluteDifference(arr, N, K);
   }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to split an array into K subarrays
# with minimum sum of absolute difference
# of adjacent elements in each of K subarrays
def absoluteDifference(arr, N, K):

    # Stores the absolute differences
    # of adjacent elements
    new_Arr = [0 for i in range(N - 1)]

    # Stores the answer
    ans = 0

    # Stores absolute differences of
    # adjacent elements in new_Arr
    for i in range(N - 1):
        new_Arr[i] = abs(arr[i] - arr[i + 1])

        # Stores the sum of all absolute
        # differences of adjacent elements
        ans += new_Arr[i]

    # Sorting the new_Arr
    # in decreasing order
    new_Arr = sorted(new_Arr)[::-1]

    for i in range(K - 1):

        # Removing K - 1 elements
        # with maximum sum
        ans -= new_Arr[i]

    # Prints the answer
    print (ans)

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 3, -2, 5, -1 ]

    # Given K
    K = 2

    # Size of array
    N = len(arr)

    # Function Call
    absoluteDifference(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

public static void reverse(int[] array)
{

    // Length of the array
    int n = array.Length;

    // Swaping the first half elements with
    // last half elements
    for(int i = 0; i < n / 2; i++)
    {

        // Storing the first half elements
        // temporarily
        int temp = array[i];

        // Assigning the first half to
        // the last half
        array[i] = array[n - i - 1];

        // Assigning the last half to
        // the first half
        array[n - i - 1] = temp;
    }
}

// Function to split an array into K subarrays
// with minimum sum of absolute difference
// of adjacent elements in each of K subarrays
public static void absoluteDifference(int[] arr,
                                      int N, int K)
{

    // Stores the absolute differences
    // of adjacent elements
    int[] new_Arr = new int[N - 1];

    // Stores the answer
    int ans = 0;

    // Stores absolute differences of
    // adjacent elements in new_Arr
    for(int i = 0; i < N - 1; i++)
    {
        new_Arr[i] = Math.Abs(arr[i] -
                              arr[i + 1]);

        // Stores the sum of all absolute
        // differences of adjacent elements
        ans += new_Arr[i];
    }

    // Sorting the new_Arr
    // in decreasing order
    Array.Sort(new_Arr);
    reverse(new_Arr);

    for(int i = 0; i < K - 1; i++)
    {

        // Removing K - 1 elements
        // with maximum sum
        ans -= new_Arr[i];
    }

    // Prints the answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main ()
{

    // Given array arr[]
    int[] arr = { 1, 3, -2, 5, -1 };

    // Given K
    int K = 2;

    // Size of array
    int N = arr.Length;

    // Function Call
    absoluteDifference(arr, N, K);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program for the above approach
function reverse(array)
{

    // Length of the array
    let n = array.length;

    // Swaping the first half elements
    // with last half elements
    for(let i = 0; i < n / 2; i++)
    {

        // Storing the first half
        // elements temporarily
        let temp = array[i];

        // Assigning the first half
        // to the last half
        array[i] = array[n - i - 1];

        // Assigning the last half
        // to the first half
        array[n - i - 1] = temp;
    }
}

// Function to split an array into K subarrays
// with minimum sum of absolute difference
// of adjacent elements in each of K subarrays
function absoluteDifference(arr, N, K)
{

    // Stores the absolute differences
    // of adjacent elements
    let new_Arr = new Array(N - 1).fill(0);

    // Stores the answer
    let ans = 0;

    // Stores absolute differences of
    // adjacent elements in new_Arr
    for(let i = 0; i < N - 1; i++)
    {
        new_Arr[i] = Math.abs(arr[i] - arr[i + 1]);

        // Stores the sum of all absolute
        // differences of adjacent elements
        ans += new_Arr[i];
    }

    // Sorting the new_Arr
    // in decreasing order
    new_Arr.sort();
    reverse(new_Arr);

    for(let i = 0; i < K - 1; i++)
    {

        // Removing K - 1 elements
        // with maximum sum
        ans -= new_Arr[i];
    }

    // Print the answer
    document.write(ans);
}

// Driver Code

// Given array arr[]
let arr = [ 1, 3, -2, 5, -1 ];

// Given K
let K = 2;

// Size of array
let N = arr.length;

// Function Call
absoluteDifference(arr, N, K);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N * Log(N))*
***辅助空间:** O(N)*