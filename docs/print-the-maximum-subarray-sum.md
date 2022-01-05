# 打印最大子阵列总和

> 原文:[https://www . geesforgeks . org/print-the-max-subarray-sum/](https://www.geeksforgeeks.org/print-the-maximum-subarray-sum/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到具有最大和的相邻数字子数组的元素。

**示例:**

> **输入:** arr = [-2，-3，4，-1，-2，1，5，-3]
> **输出:**【4，-1，-2，1，5】
> **解释:**
> 在上述输入中，最大连续子阵列和为 7，子阵列的元素为【4，-1，-2，1，5】
> 
> **输入:** arr = [-2，-5，6，-2，-3，1，5，-6]
> **输出:**【6，-2，-3，1，5】
> **解释:**
> 在上述输入中，最大连续子阵列和为 7，子阵列的元素
> 为【6，-2，-3，1，5】

**天真方法:**天真方法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并打印具有最大和的那个子阵列。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**思路是利用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)找到最大子阵和，并存储具有最大和的子阵的起始和结束索引，打印从起始索引到结束索引的子阵。以下是步骤:

1.  将 3 个变量 **endIndex** 初始化为 0， **currMax** 和 **globalMax** 初始化为输入数组的第一个值。
2.  对于数组中从索引(比如 **i** ) 1 开始的每个元素，更新 **currMax** 到 **max(nums[i]，nums[i] + currMax)** 和 **globalMax** 和 **endIndex** 到 **i** 仅当 currMax > globalMax 时。
3.  要找到起始索引，从 endIndex 开始向左迭代，并不断递减 **globalMax** 的值，直到它变成 0。它变为 0 的点是开始索引。
4.  现在打印**【开始，结束】**之间的子阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the elements
// of Subarray with maximum sum
void SubarrayWithMaxSum(vector<int>& nums)
{
    // Initialize currMax and globalMax
    // with first value of nums
    int endIndex, currMax = nums[0];
    int globalMax = nums[0];

    // Iterate for all the elements
    // of the array
    for (int i = 1; i < nums.size(); ++i) {

        // Update currMax
        currMax = max(nums[i],
                      nums[i] + currMax);

        // Check if currMax is greater
        // than globalMax
        if (currMax > globalMax) {
            globalMax = currMax;
            endIndex = i;
        }
    }

    int startIndex = endIndex;

    // Traverse in left direction to
    // find start Index of subarray
    while (startIndex >= 0) {

        globalMax -= nums[startIndex];

        if (globalMax == 0)
            break;

        // Decrement the start index
        startIndex--;
    }

    // Printing the elements of
    // subarray with max sum
    for (int i = startIndex;
         i <= endIndex; ++i) {

        cout << nums[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr
        = { -2, -5, 6, -2,
            -3, 1, 5, -6 };

    // Function call
    SubarrayWithMaxSum(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to print the elements
  // of Subarray with maximum sum
  static void SubarrayWithMaxSum(Vector<Integer> nums)
  {
    // Initialize currMax and globalMax
    // with first value of nums
    int endIndex = 0, currMax = nums.get(0);
    int globalMax = nums.get(0);

    // Iterate for all the elements
    // of the array
    for (int i = 1; i < nums.size(); ++i)
    {

      // Update currMax
      currMax = Math.max(nums.get(i),
                         nums.get(i) + currMax);

      // Check if currMax is greater
      // than globalMax
      if (currMax > globalMax)
      {
        globalMax = currMax;
        endIndex = i;
      }
    }

    int startIndex = endIndex;

    // Traverse in left direction to
    // find start Index of subarray
    while (startIndex >= 0)
    {
      globalMax -= nums.get(startIndex);

      if (globalMax == 0)
        break;

      // Decrement the start index
      startIndex--;
    }

    // Printing the elements of
    // subarray with max sum
    for(int i = startIndex; i <= endIndex; ++i)
    {
      System.out.print(nums.get(i) + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given array arr[]
    Vector<Integer> arr = new Vector<Integer>();
    arr.add(-2);
    arr.add(-5);
    arr.add(6);
    arr.add(-2);
    arr.add(-3);
    arr.add(1);
    arr.add(5);
    arr.add(-6);

    // Function call
    SubarrayWithMaxSum(arr);
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the elements
# of Subarray with maximum sum
def SubarrayWithMaxSum(nums):

    # Initialize currMax and globalMax
    # with first value of nums
    currMax = nums[0]
    globalMax = nums[0]

    # Iterate for all the elements
    # of the array
    for i in range(1, len(nums)):

        # Update currMax
        currMax = max(nums[i],
                      nums[i] + currMax)

        # Check if currMax is greater
        # than globalMax
        if (currMax > globalMax):
            globalMax = currMax
            endIndex = i

    startIndex = endIndex

    # Traverse in left direction to
    # find start Index of subarray
    while (startIndex >= 0):
        globalMax -= nums[startIndex]

        if (globalMax == 0):
            break

        # Decrement the start index
        startIndex -= 1

    # Printing the elements of
    # subarray with max sum
    for i in range(startIndex, endIndex + 1):
        print(nums[i], end = " ")

# Driver Code

# Given array arr[]
arr = [ -2, -5, 6, -2,
        -3, 1, 5, -6 ]

# Function call
SubarrayWithMaxSum(arr)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

  // Function to print the elements
  // of Subarray with maximum sum
  static void SubarrayWithMaxSum(List<int> nums)
  {
    // Initialize currMax and globalMax
    // with first value of nums
    int endIndex = 0, currMax = nums[0];
    int globalMax = nums[0];

    // Iterate for all the elements
    // of the array
    for (int i = 1; i < nums.Count; ++i)
    {

      // Update currMax
      currMax = Math.Max(nums[i],
                         nums[i] + currMax);

      // Check if currMax is greater
      // than globalMax
      if (currMax > globalMax)
      {
        globalMax = currMax;
        endIndex = i;
      }
    }

    int startIndex = endIndex;

    // Traverse in left direction to
    // find start Index of subarray
    while (startIndex >= 0)
    {
      globalMax -= nums[startIndex];

      if (globalMax == 0)
        break;

      // Decrement the start index
      startIndex--;
    }

    // Printing the elements of
    // subarray with max sum
    for(int i = startIndex; i <= endIndex; ++i)
    {
      Console.Write(nums[i] + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    // Given array []arr
    List<int> arr = new List<int>();
    arr.Add(-2);
    arr.Add(-5);
    arr.Add(6);
    arr.Add(-2);
    arr.Add(-3);
    arr.Add(1);
    arr.Add(5);
    arr.Add(-6);

    // Function call
    SubarrayWithMaxSum(arr);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the elements
// of Subarray with maximum sum
function SubarrayWithMaxSum(nums)
{

    // Initialize currMax and globalMax
    // with first value of nums
    var endIndex, currMax = nums[0];
    var globalMax = nums[0];

    // Iterate for all the elements
    // of the array
    for(var i = 1; i < nums.length; ++i)
    {

        // Update currMax
        currMax = Math.max(nums[i],
                           nums[i] + currMax);

        // Check if currMax is greater
        // than globalMax
        if (currMax > globalMax)
        {
            globalMax = currMax;
            endIndex = i;
        }
    }

    var startIndex = endIndex;

    // Traverse in left direction to
    // find start Index of subarray
    while (startIndex >= 0)
    {
        globalMax -= nums[startIndex];

        if (globalMax == 0)
            break;

        // Decrement the start index
        startIndex--;
    }

    // Printing the elements of
    // subarray with max sum
    for(var i = startIndex;
            i <= endIndex; ++i)
    {
        document.write(nums[i] + " ");
    }
}

// Driver Code

// Given array arr[]
var arr = [ -2, -5, 6, -2,
            -3, 1, 5, -6 ];

// Function call
SubarrayWithMaxSum(arr);

// This code is contributed by rutvik_56

</script>
```

**Output**

```
6 -2 -3 1 5 
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**交替高效方法**:该方法消除了上述方法中向左递减 global_max 的内部 while 循环。因此这种方法减少了时间。

1.  将 currMax 和 globalMax 初始化为输入数组的第一个值。将 endIndex、startIndex、globalMaxStartIndex 初始化为 0。(endIndex，startIndex 存储以 I 结尾的最大和子数组的开始和结束索引。globalMaxStartIndex 存储 globalMax 的开始索引)
2.  对于数组中从 index(比如 i) 1 开始的每个元素，如果 nums[i] > nums[i] + currMax，则将 currMax 和 startIndex 更新为 I。否则只更新 currMax。
3.  如果当前最大值>全局最大值，则更新全局最大值。同时更新 globalMaxStartIndex。
4.  现在打印[开始索引，全局最开始索引]之间的子数组。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to print the elements
    // of Subarray with maximum sum
    static void SubarrayWithMaxSum(Vector<Integer> nums)
    {
        // Initialize currMax and globalMax
        // with first value of nums
        int currMax = nums.get(0), globalMax = nums.get(0);
        // Initialize endIndex startIndex,globalStartIndex
        int endIndex = 0;
        int startIndex = 0, globalMaxStartIndex = 0;

        // Iterate for all the elements of the array
        for (int i = 1; i < nums.size(); ++i) {

            // Update currMax and startIndex
            if (nums.get(i) > nums.get(i) + currMax) {
                currMax = nums.get(i);
                startIndex = i; // update the new startIndex
            }

            // Update currMax
            else if (nums.get(i) < nums.get(i) + currMax) {
                currMax = nums.get(i) + currMax;
            }

            // Update globalMax anf globalMaxStartIndex
            if (currMax > globalMax) {
                globalMax = currMax;
                endIndex = i;
                globalMaxStartIndex = startIndex;
            }
        }

        // Printing the elements of subarray with max sum
        for (int i = globalMaxStartIndex; i <= endIndex;
             ++i) {
            System.out.print(nums.get(i) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        Vector<Integer> arr = new Vector<Integer>();
        arr.add(-2);
        arr.add(-5);
        arr.add(6);
        arr.add(-2);
        arr.add(-3);
        arr.add(1);
        arr.add(5);
        arr.add(-6);
        // Function call
        SubarrayWithMaxSum(arr);
    }
}

// This code is contributed by Amritha Basavaraj Patil
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    // Function to print the elements
    // of Subarray with maximum sum
    static void SubarrayWithMaxSum(List<int> nums)
    {
        // Initialize currMax and globalMax
        // with first value of nums
        int currMax = nums[0], globalMax = nums[0];

        // Initialize endIndex startIndex,globalStartIndex
        int endIndex = 0;
        int startIndex = 0, globalMaxStartIndex = 0;

        // Iterate for all the elements of the array
        for (int i = 1; i < nums.Count; ++i) {

            // Update currMax and startIndex
            if (nums[i] > nums[i] + currMax) {
                currMax = nums[i];
                startIndex = i; // update the new startIndex
            }

            // Update currMax
            else if (nums[i] < nums[i] + currMax) {
                currMax = nums[i] + currMax;
            }

            // Update globalMax anf globalMaxStartIndex
            if (currMax > globalMax) {
                globalMax = currMax;
                endIndex = i;
                globalMaxStartIndex = startIndex;
            }
        }

        // Printing the elements of subarray with max sum
        for (int i = globalMaxStartIndex; i <= endIndex;
             ++i) {
            Console.Write(nums[i] + " ");
        }
    }

    // Driver Code
    static public void Main (){

        // Given array arr[]
        List<int> arr = new List<int>();
        arr.Add(-2);
        arr.Add(-5);
        arr.Add(6);
        arr.Add(-2);
        arr.Add(-3);
        arr.Add(1);
        arr.Add(5);
        arr.Add(-6);
        // Function call
        SubarrayWithMaxSum(arr);

    }
}

// This code is contributed by rag2127.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the elements
    // of Subarray with maximum sum
function SubarrayWithMaxSum(nums)
{
    // Initialize currMax and globalMax
        // with first value of nums
        let currMax = nums[0], globalMax = nums[0];
        // Initialize endIndex startIndex,globalStartIndex
        let endIndex = 0;
        let startIndex = 0, globalMaxStartIndex = 0;

        // Iterate for all the elements of the array
        for (let i = 1; i < nums.length; ++i) {

            // Update currMax and startIndex
            if (nums[i] > nums[i] + currMax) {
                currMax = nums[i];
                startIndex = i; // update the new startIndex
            }

            // Update currMax
            else if (nums[i] < nums[i] + currMax) {
                currMax = nums[i] + currMax;
            }

            // Update globalMax anf globalMaxStartIndex
            if (currMax > globalMax) {
                globalMax = currMax;
                endIndex = i;
                globalMaxStartIndex = startIndex;
            }
        }

        // Printing the elements of subarray with max sum
        for (let i = globalMaxStartIndex; i <= endIndex;
             ++i) {
            document.write(nums[i] + " ");
        }
}

// Driver Code

let arr = [];
arr.push(-2);
arr.push(-5);
arr.push(6);
arr.push(-2);
arr.push(-3);
arr.push(1);
arr.push(5);
arr.push(-6);
// Function call
SubarrayWithMaxSum(arr);

// This code is contributed by unknown2108

</script>
```

**Output**

```
6 -2 -3 1 5 
```

***时间复杂度:**O(N)**T5】
*T8】辅助空间: O(1)****