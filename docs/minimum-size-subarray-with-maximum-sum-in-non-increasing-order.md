# 最小尺寸子阵列，最大和不递增

> 原文:[https://www . geesforgeks . org/最小尺寸子阵列最大非递增顺序/](https://www.geeksforgeeks.org/minimum-size-subarray-with-maximum-sum-in-non-increasing-order/)

给定一个数组 **arr** ，任务是找到数组元素的子数组，其和严格大于其余元素。子阵列的大小应该是最小的，总和应该是最大的，并且必须是不递增的。
**例:**

> **输入:** arr = [7，6，13，12，11]
> **输出:** 13 12
> **解释:**
> 子阵列[13，12]和[13，11]是极小的，使得它们的元素之和严格大于其余元素。然而，子阵列[13，12]具有其元素的最大总和，因此它以非递增顺序返回。
> **输入:**arr =【8】
> **输出:** 8

**进场:**

1.  首先，我们将对数组**进行排序**，并定义一个名为 **A** 的向量。现在我们先计算整个数组的**和**，然后在连续更新**温度**的同时，从后面迭代整个循环。循环运行直到**温度**变为零。

2.  实际上，当我们从后面迭代循环时，我们考虑的是最大值。因此，我们可以说，我们可以在更短的时间内达到目标条件，也通过采取更少的变量。

3.  现在，随着循环的运行，我们继续更新 temp 的值，只需将 **nums[i]** 添加到其中，并将 **nums[i]** 添加到**向量 A** 中。最后我们返回**向量 A** ，它代表我们想要的输出结果。

以下是上述方法的实现:

## C++

```
// C++ program to find the Minimum size Subarray
// with maximum sum in non-increasing order

#include <bits/stdc++.h>
using namespace std;

// Function to find the Minimum size Subarray
void minSet(vector<int>& nums)
{

    vector<int> A;

    // sort numbers in descending order
    sort(nums.begin(), nums.end());

    // get total sum of the given array.
    int sum = 0;
    for (int i = 0; i < nums.size(); i++)
        sum += nums[i];

    int temp = 0;

    // Loop until the sum of numbers
    // is greater than sum/2
    for (int i = nums.size() - 1;
         i >= 0 && temp <= sum / 2;
         i--) {

        A.push_back(nums[i]);
        temp += nums[i];
    }

    // Print the Minimum size Subarray
    for (int i = 0; i < A.size(); i++)
        cout << A[i] << " ";
}

// Driver code
int main()
{
    vector<int> vec
        = { 7, 6, 13, 13, 12, 11 };

    minSet(vec);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Minimum size Subarray
// with maximum sum in non-increasing order
import java.util.*;

class GFG {

  // Function to find the Minimum size Subarray
  static void minSet(ArrayList<Integer> nums) {

    ArrayList<Integer> A = new ArrayList<Integer> ();

    // sort numbers in descending order
    Collections.sort(nums);

    // get total sum of the given array.
    int sum = 0;
    for (int i = 0; i<nums.size(); i++)
      sum += nums.get(i);

    int temp = 0;

    // Loop until the sum of numbers
    // is greater than sum/2
    for (int i = nums.size() - 1; 
      i >= 0 && temp<= sum / 2;
      i--) {

      A.add(nums.get(i));
      temp += nums.get(i);
    }

    // Print the Minimum size Subarray
    for (int i = 0; i<A.size(); i++)
      System.out.print(A.get(i) + " ");
  }

  // Driver Code
  public static void main(String[] args) {
    ArrayList<Integer> gfg = new ArrayList<Integer> ();
    gfg.add(7);
    gfg.add(6);
    gfg.add(13);
    gfg.add(13);
    gfg.add(12);
    gfg.add(11);

    // Function calling
    minSet(gfg);
  }
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to find the Minimum size Subarray
# with maximum sum in non-increasing order

# Function to find the Minimum size Subarray
def minSet(nums) :

    A = []

    # sort numbers in descending order
    nums.sort()

    # get total sum of the given array.
    sum = 0
    for i in range(0,len(nums)):
        sum += nums[i]

    temp = 0

    # Loop until the sum of numbers
    # is greater than sum/2
    for i in range(len(nums)-1, -1, -1):
        if(temp > sum / 2):
            break
        A.append(nums[i])
        temp += nums[i]

    # Print the Minimum size Subarray
    for i in range(0, len(A)):
        print(A[i], end = ' ')

# Driver code
vec = [ 7, 6, 13, 13, 12, 11 ]

minSet(vec);

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find the Minimum size Subarray
// with maximum sum in non-increasing order
using System;
using System.Collections.Generic;

class GFG {

  // Function to find the Minimum size Subarray
  static void minSet(List<int> nums) {

    List<int> A = new List<int> ();

    // sort numbers in descending order
    nums.Sort();

    // get total sum of the given array.
    int sum = 0;
    for (int i = 0; i < nums.Count; i++)
      sum += nums[i];

    int temp = 0;

    // Loop until the sum of numbers
    // is greater than sum/2
    for (int i = nums.Count - 1; 
      i >= 0 && temp<= sum / 2;
      i--) {

      A.Add(nums[i]);
      temp += nums[i];
    }

    // Print the Minimum size Subarray
    for (int i = 0; i<A.Count; i++)
      Console.Write(A[i] + " ");
  }

  // Driver Code
  public static void Main(String[] args) {
    List<int> gfg = new List<int> ();
    gfg.Add(7);
    gfg.Add(6);
    gfg.Add(13);
    gfg.Add(13);
    gfg.Add(12);
    gfg.Add(11);

    // Function calling
    minSet(gfg);
  }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the Minimum size Subarray
// with maximum sum in non-increasing order

// Function to find the Minimum size Subarray
function minSet(nums)
{

    var A = [];

    // sort numbers in descending order
    nums.sort((a,b)=>a-b);

    // get total sum of the given array.
    var sum = 0;
    for (var i = 0; i < nums.length; i++)
        sum += nums[i];

    var temp = 0;

    // Loop until the sum of numbers
    // is greater than sum/2
    for (var i = nums.length - 1;
         i >= 0 && temp <= sum / 2;
         i--) {

        A.push(nums[i]);
        temp += nums[i];
    }

    // Print the Minimum size Subarray
    for (var i = 0; i < A.length; i++)
        document.write( A[i] + " ");
}

// Driver code
var vec
    = [7, 6, 13, 13, 12, 11];
minSet(vec);

</script>
```

**Output:** 

```
13 13 12
```

***时间复杂度:** O(N * log N)*
***辅助空间复杂度:** O(N)*