# 排除最大元素后和最大的子阵

> 原文:[https://www . geeksforgeeks . org/subarray-不包括其最大元素后的最大值/](https://www.geeksforgeeks.org/subarray-with-largest-sum-after-excluding-its-maximum-element/)

给定一个数组 **arr[]** ，任务是在排除其最大元素后，找到和最大的子数组的开始和结束索引。
**例:**

> **输入:** arr[] = {5，-2，10，-1，4}
> **输出:** 1 5
> **解释:**
> 子阵[1:5] = {5，-2，10，-1，4}
> 不含最大元素的子阵之和= 5 + (-2) + (-1) + 4 = 6
> **输入:** arr[] = {5，2，5，3，-30，-30

**方法:**思路是用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来解决这个问题。

1.  在这个问题中，我们必须选择一个子阵中最大的元素。
2.  因此，我们可以从数组中选择所有的正元素，每次我们都可以将大于那个元素的元素设为 INT_MIN，这样它就不包含在数组中了。
3.  最后[应用卡丹算法求最大和子阵](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。
4.  如果数组中没有正元素，那么我们可以从数组中选择任意一个元素，得到最大和为 0。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum sum subarray such by
// excluding the maximum element
// from the subarray

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// subarray by excluding the maximum
// element from the array
void maximumSumSubarray(int arr[], int n)
{
    unordered_map<int, int> mp;

    // Loop to store all the positive
    // elements in the map
    for (int i = 0; i < n; i++) {

        if (arr[i] >= 0
            && mp.find(arr[i])
                == mp.end())

            mp[arr[i]] = 1;
    }

    int first = 0;
    int last = 0;
    int ans = 0;
    int INF = 1e6;

    // Loop to iterating over the map
    // and considering as the maximum
    // element of the current including
    // subarray
    for (auto i : mp) {

        // Make the current
        // element maximum
        int mx = i.first;

        int curr = 0;
        int curr_start;

        // Iterate through array and
        // apply kadane's algorithm
        for (int j = 0; j < n; j++) {
            if (curr == 0)
                curr_start = j;

            // Condition if current element is
            // greater than mx then make
            // the element -infinity
            int val = arr[j] > mx
                        ? -INF
                        : arr[j];

            curr += val;

            if (curr < 0)
                curr = 0;

            if (curr > ans) {
                ans = curr;

                // Store the indices
                // in some variable
                first = curr_start;
                last = j;
            }
        }
    }

    cout << first + 1
        << " " << last + 1;
}

// Driver Code
int main()
{
    int arr[] = { 5, -2, 10, -1, 4 };

    int size = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumSumSubarray(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum subarray such by
// excluding the maximum element
// from the subarray
import java.util.*;

class GFG{

// Function to find the maximum sum
// subarray by excluding the maximum
// element from the array
static void maximumSumSubarray(int arr[], int n)
{
    Map<Integer, Integer> mp = new HashMap<>();

    // Loop to store all the positive
    // elements in the map
    for(int i = 0; i < n; i++)
    {
        if (arr[i] >= 0)
            mp.put(arr[i], 1);
    }

    int first = 0;
    int last = 0;
    int ans = 0;
    int INF = (int)1e6;

    // Loop to iterating over the map
    // and considering as the maximum
    // element of the current including
    // subarray
    for (Map.Entry<Integer,
                   Integer> i : mp.entrySet())
    {

        // Make the current
        // element maximum
        int mx = i.getKey();
        int curr = 0;
        int curr_start = -1;

        // Iterate through array and
        // apply kadane's algorithm
        for(int j = 0; j < n; j++)
        {
            if (curr == 0)
                curr_start = j;

            // Condition if current element is
            // greater than mx then make
            // the element -infinity
            int val = arr[j] > mx ? -INF : arr[j];
            curr += val;

            if (curr < 0)
                curr = 0;

            if (curr > ans)
            {
                ans = curr;

                // Store the indices
                // in some variable
                first = curr_start;
                last = j;
            }
        }
    }
    System.out.print((first + 1) + " " +
                      (last + 1));
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, -2, 10, -1, 4 };
    int size = arr.length;

    // Function call
    maximumSumSubarray(arr, size);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find
# the maximum sum subarray such
# by excluding the maximum
# element from the subarray

# Function to find the maximum sum
# subarray by excluding the maximum
# element from the array
def maximumSumSubarray(arr, n):
    mp = {}

    # Loop to store all the positive
    # elements in the map
    for i in range(n):

        if (arr[i] >= 0 and
            arr[i] not in mp):
            mp[arr[i]] = 1

    first = 0
    last = 0
    ans = 0
    INF = 1e6

    # Loop to iterating over the map
    # and considering as the maximum
    # element of the current including
    # subarray
    for i in mp:

        # Make the current
        # element maximum
        mx = i

        curr = 0

        # Iterate through array and
        # apply kadane's algorithm
        for j in range(n):
            if (curr == 0):
                curr_start = j

            # Condition if current element
            # is greater than mx then make
            # the element -infinity
            if arr[j] > mx:
                val =- INF
            else:
                val= arr[j];

            curr += val

            if (curr < 0):
                curr = 0

            if (curr > ans):
                ans = curr

                # Store the indices
                # in some variable
                first = curr_start
                last = j

    print(first + 1, last + 1)

# Driver Code
if __name__ == "__main__":

    arr = [ 5, -2, 10, -1, 4 ]
    size = len(arr)

    # Function Call
    maximumSumSubarray(arr, size)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the
// maximum sum subarray such by
// excluding the maximum element
// from the subarray
using System;
using System.Collections.Generic;
class GFG{

// Function to find the maximum sum
// subarray by excluding the maximum
// element from the array
static void maximumSumSubarray(int []arr,
                               int n)
{
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();

  // Loop to store all the positive
  // elements in the map
  for(int i = 0; i < n; i++)
  {
    if (arr[i] >= 0)
      mp.Add(arr[i], 1);
  }

  int first = 0;
  int last = 0;
  int ans = 0;
  int INF = (int)1e6;

  // Loop to iterating over the map
  // and considering as the maximum
  // element of the current including
  // subarray
  foreach (KeyValuePair<int,
                        int> i in mp)
  {
    // Make the current
    // element maximum
    int mx = i.Key;
    int curr = 0;
    int curr_start = -1;

    // Iterate through array and
    // apply kadane's algorithm
    for(int j = 0; j < n; j++)
    {
      if (curr == 0)
        curr_start = j;

      // Condition if current element is
      // greater than mx then make
      // the element -infinity
      int val = arr[j] > mx ?
                -INF : arr[j];
      curr += val;

      if (curr < 0)
        curr = 0;

      if (curr > ans)
      {
        ans = curr;

        // Store the indices
        // in some variable
        first = curr_start;
        last = j;
      }
    }
  }
  Console.Write((first + 1) + " " +
                (last + 1));
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {5, -2, 10, -1, 4};
  int size = arr.Length;

  // Function call
  maximumSumSubarray(arr, size);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// maximum sum subarray such by
// excluding the maximum element
// from the subarray

// Function to find the maximum sum
// subarray by excluding the maximum
// element from the array
function maximumSumSubarray(arr, n)
{
    var mp = new Map();

    // Loop to store all the positive
    // elements in the map
    for (var i = 0; i < n; i++) {

        if (arr[i] >= 0
            && !mp.has(arr[i]))
            mp.set(arr[i] , 1);
    }

    var first = 0;
    var last = 0;
    var ans = 0;
    var INF = 1000000;

    // Loop to iterating over the map
    // and considering as the maximum
    // element of the current including
    // subarray
    mp.forEach((value, key) => {

        // Make the current
        // element maximum
        var mx = key;

        var curr = 0;
        var curr_start;

        // Iterate through array and
        // apply kadane's algorithm
        for (var j = 0; j < n; j++) {
            if (curr == 0)
                curr_start = j;

            // Condition if current element is
            // greater than mx then make
            // the element -infinity
            var val = arr[j] > mx
                        ? -INF
                        : arr[j];

            curr += val;

            if (curr < 0)
                curr = 0;

            if (curr > ans) {
                ans = curr;

                // Store the indices
                // in some variable
                first = curr_start;
                last = j;
            }
        }
    });

    document.write( first + 1
        + " " + (last + 1));
}

// Driver Code

var arr = [5, -2, 10, -1, 4];
var size = arr.length;

// Function Call
maximumSumSubarray(arr, size);

</script>
```

**Output:** 

```
1 5
```