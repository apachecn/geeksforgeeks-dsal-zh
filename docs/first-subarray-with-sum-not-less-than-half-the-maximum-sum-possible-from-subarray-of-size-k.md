# 第一子阵列，其总和至少为大小为 K 的任何子阵列的最大总和的一半

> 原文:[https://www . geeksforgeeks . org/sum 不小于 k 大小子阵列最大可能总和的一半的第一子阵列/](https://www.geeksforgeeks.org/first-subarray-with-sum-not-less-than-half-the-maximum-sum-possible-from-subarray-of-size-k/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是从任何大小的子阵列 **K** 中找到第一个[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其和大于或等于最大可能和的一半。

**示例:**

> **输入:** arr[] = {2，4，5，1，4，6，6，2，1，0}，K = 3
> **输出:**6 2 1
> T6】解释:
> 给定阵列在任何大小的子阵列中的最大可能和 **K** 是子阵列 **{4，6，6}** 的 16。
> 所以，需要的子阵和应该大于等于 8
> {6，2，1}是第一个 9 之和大于 8 的子阵。
> 
> **输入:** arr[] = {12，45，11，10，8，56，2}，K = 4
> **输出:** 45 11 10

**方法:**这个问题可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决，因为要考虑子阵列。按照以下步骤解决此问题:

1.  计算大小为 **K** 的所有子阵列的总和，并将其存储在一个数组中。
2.  现在，求所有和的最大值。
3.  迭代数组，找到大于或等于上面获得的最大子数组和的一半的和。
4.  打印满足上述条件的子阵列。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to print the subarray with sum
// greater or equal than the half of
// the maximum subarray sum of K size
void subArray(int arr[], int n, int k)
{
    int sum = 0;

    // Storing sum of first subarray
    for (int i = 0; i < k; i++) {
        sum += arr[i];
    }

    // Vector to store the
    // subarray sums
    vector<int> res;
    res.push_back(sum);

    // Sliding window technique to
    // Find sum of subarrays of size K
    for (int i = k; i < n; i++) {
        sum -= arr[i - k];
        sum += arr[i];
        res.push_back(sum);
    }

    // Maximum sub-array sum
    int max_sum = *max_element(res.begin(),
                               res.end());

    int half = max_sum / 2;

    // Create a copy vector
    vector<int> copy = res;

    // Sort the vector
    sort(copy.begin(),copy.end()); 

    int half_index, half_sum;

    // Check in a sorted array for
    // an element exceeding
    // half of the max_sum
    for (auto x : copy) {
        if (x >= half) {
            half_sum = x;
            break;
        }
    }

    // Calculate index of first
    // subarray having required sum
    for (int x = 0; x < res.size(); x++) {
        if (res[x] == half_sum) {
            half_index = x;
            break;
        }
    }

    // Print the subarray
    for (int i = 1; i <= k; i++) {
        cout << arr[half_index + i - 1]
             << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 4, 5, 1, 4, 6, 6, 2, 1, 0 };
    int k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    subArray(arr, n, k);

    return 0;
}
// This code is contributed by akshitdiwan05
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to print the subarray with sum
// greater or equal than the half of
// the maximum subarray sum of K size
static void subArray(int arr[],
                     int n, int k)
{
  int sum = 0;

  // Storing sum of first subarray
  for (int i = 0; i < k; i++)
  {
    sum += arr[i];
  }

  // Vector to store the
  // subarray sums
  Vector<Integer> res = new Vector<>();
  res.add(sum);

  // Sliding window technique to
  // Find sum of subarrays of size K
  for (int i = k; i < n; i++)
  {
    sum -= arr[i - k];
    sum += arr[i];
    res.add(sum);
  }

  // Maximum sub-array sum
  int max_sum = res.elementAt(0);
  for(int i =0; i < res.size(); i++)
  {
    if(max_sum < res.elementAt(i))
    {
      max_sum = res.elementAt(i);
    }
  }

  int half = max_sum / 2;

  // Create a copy vector
  Vector<Integer> copy =
                  new Vector<>(res);

  // Sort the vector
  Collections.sort(copy);
  int half_index = 0, half_sum = 0;

  // Check in a sorted array for
  // an element exceeding
  // half of the max_sum
  for (int x = 0; x < copy.size(); x++)
  {
    if (copy.elementAt(x) >= half)
    {
      half_sum = copy.elementAt(x);
      break;
    }
  }

  // Calculate index of first
  // subarray having required sum
  for (int x = 0; x < res.size(); x++)
  {
    if (res.elementAt(x) == half_sum)
    {
      half_index = x;
      break;
    }
  }

  // Print the subarray
  for (int i = 1; i <= k; i++)
  {
    System.out.print(
           arr[half_index + i - 1] + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int arr[] = {2, 4, 5, 1, 4,
               6, 6, 2, 1, 0};
  int k = 3;
  int n = arr.length;

  // Function Call
  subArray(arr, n, k);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python 3 implementation
# of the above approach

# Function to print the
# subarray with sum greater
# or equal than the half of
# the maximum subarray
# sum of K size
def subArray(arr, n, k):

    sum = 0

    # Storing sum of
    # first subarray
    for i in range (k):
        sum += arr[i]

    # Vector to store the
    # subarray sums
    res = []
    res.append(sum)

    # Sliding window technique
    # to find sum of subarrays
    # of size K
    for i in range (k, n):
        sum -= arr[i - k]
        sum += arr[i]
        res.append(sum)

    # Maximum sub-array sum
    max_sum = max(res)
    half = max_sum // 2

    # Create a copy vector
    copy = res.copy()

    # Sort the vector
    copy.sort()

    # Check in a sorted array for
    # an element exceeding
    # half of the max_sum
    for x in copy:
        if (x >= half):
            half_sum = x
            break

    # Calculate index of first
    # subarray having required sum
    for x in range (len(res)):
        if (res[x] == half_sum):
            half_index = x
            break

    # Print the subarray
    for i in range (1, k + 1):
        print (arr[half_index + i - 1] ,
               end = " ")

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [2, 4, 5, 1, 4,
           6, 6, 2, 1, 0]
    k = 3
    n = len(arr)

    # Function Call
    subArray(arr, n, k);

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the subarray with sum
// greater or equal than the half of
// the maximum subarray sum of K size
static void subArray(int []arr,
                     int n, int k)
{
    int sum = 0;

    // Storing sum of first subarray
    for(int i = 0; i < k; i++)
    {
        sum += arr[i];
    }

    // List to store the
    // subarray sums
    List<int> res = new List<int>();
    res.Add(sum);

    // Sliding window technique to
    // Find sum of subarrays of size K
    for(int i = k; i < n; i++)
    {
        sum -= arr[i - k];
        sum += arr[i];
        res.Add(sum);
    }

    // Maximum sub-array sum
    int max_sum = res[0];
    for(int i = 0; i < res.Count; i++)
    {
        if (max_sum < res[i])
        {
            max_sum = res[i];
        }
    }

    int half = max_sum / 2;

    // Create a copy vector
    List<int> copy = new List<int>(res);

    // Sort the vector
    copy.Sort();
    int half_index = 0, half_sum = 0;

    // Check in a sorted array for
    // an element exceeding
    // half of the max_sum
    for(int x = 0; x < copy.Count; x++)
    {
        if (copy[x] >= half)
        {
            half_sum = copy[x];
            break;
        }
    }

    // Calculate index of first
    // subarray having required sum
    for(int x = 0; x < res.Count; x++)
    {
        if (res[x] == half_sum)
        {
            half_index = x;
            break;
        }
    }

    // Print the subarray
    for(int i = 1; i <= k; i++)
    {
        Console.Write(
            arr[half_index + i - 1] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 4, 5, 1, 4,
                  6, 6, 2, 1, 0 };
    int k = 3;
    int n = arr.Length;

    // Function call
    subArray(arr, n, k);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript implementation of
// the above approach
// Creating the bblSort function
 function bblSort(arr){

 for(var i = 0; i < arr.length; i++){

   // Last i elements are already in place 
   for(var j = 0; j < ( arr.length - i -1 ); j++){

     // Checking if the item at present iteration
     // is greater than the next iteration
     if(arr[j] > arr[j+1]){

       // If the condition is true then swap them
       var temp = arr[j]
       arr[j] = arr[j + 1]
       arr[j+1] = temp
     }
   }
 }
 // Print the sorted array
 return arr;
}
    // Function to print the subarray with sum
    // greater or equal than the half of
    // the maximum subarray sum of K size
    function subArray(arr , n , k) {
        var sum = 0;

        // Storing sum of first subarray
        for (i = 0; i < k; i++) {
            sum += arr[i];
        }

        // Vector to store the
        // subarray sums
        var res =[];
        res.push(sum);

        // Sliding window technique to
        // Find sum of subarrays of size K
        for (i = k; i < n; i++) {
            sum -= arr[i - k];
            sum += arr[i];
            res.push(sum);
        }

        // Maximum sub-array sum
        var max_sum = res[0];
        for (i = 0; i < res.length; i++) {
            if (max_sum < res[i]) {
                max_sum = res[i];
            }
        }

        var half = max_sum / 2;

        // Create a copy vector
        var copy = Array(res.length).fill(0);
for (i = 0; i < res.length; i++)
copy[i] = res[i];
        // Sort the vector
        copy = bblSort(copy);
        var half_index = 0, half_sum = 0;

        // Check in a sorted array for
        // an element exceeding
        // half of the max_sum
        for (x = 0; x < copy.length; x++) {
            if (copy[x] >= half) {
                half_sum = copy[x];
                break;
            }
        }

        // Calculate index of first
        // subarray having required sum
        for (x = 0; x < res.length; x++) {
            if (res[x] == half_sum) {
                half_index = x;
                break;
            }
        }
        // Print the subarray
        for (i = 1; i <= k; i++) {
            document.write(arr[half_index + i - 1] + " ");
        }
    }

    // Driver Code

        // Given array
        var arr = [ 2, 4, 5, 1, 4, 6, 6, 2, 1, 0 ];
        var k = 3;
        var n = arr.length;

        // Function Call
        subArray(arr, n, k);

// This code is contributed by todaysgaurav

</script>
```

**Output**

```
6 2 1 
```

***时间复杂度:** O(NlogN)*
***空间复杂度:** O(N)*