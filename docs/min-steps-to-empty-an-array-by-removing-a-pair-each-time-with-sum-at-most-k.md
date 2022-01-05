# 每次移除一对数组清空数组的最小步骤，总和最多为 K

> 原文:[https://www . geeksforgeeks . org/min-每次移除最多 k 个和的对来清空阵列的步骤/](https://www.geeksforgeeks.org/min-steps-to-empty-an-array-by-removing-a-pair-each-time-with-sum-at-most-k/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个目标值 **K** 。任务是找到从数组中取出所有元素所需的**最小**步数。在每个步骤中，最多可以从数组中选择两个元素，使得它们的**和**不得超过目标值 **K** 。
**注:**数组的所有元素都小于或等于 **K** 。

> **输入:** arr[] = [5，1，5，4]，K = 8
> **输出:** 3
> **解释:**
> 我们可以分 3 步挑选{1，4}、{5}、{ 5}:
> 其他可能的排列可以是{1，5 }、{4}、{5}分三步。
> 所以，最少需要的步数是 3
> **输入:**【1，2，1，1，3】，n = 9
> **输出:** 3
> **解释:**
> 我们可以分三步挑选{1，1}、{2，3}和{1}。
> 其他可能的选择{1，3}、{1，2}、{1}或{1，1}、{1，3}、{2}
> 因此，所需的最小步骤数为 3

**进场:**以上问题可以使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)配合[二分技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决。想法是从数组中挑选最小的[和最大的元素，检查总和是否没有超过 **N** ，然后移除这些元素并计算这一步，否则移除最大的元素，然后重复上述步骤，直到所有元素都被移除。以下是步骤:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) 

1.  [排序](https://www.geeksforgeeks.org/sorting-algorithms/)给定数组 **arr[]** 。
2.  初始化两个索引 **i = 0** 和**j = N–1**。
3.  如果元素**arr【I】****arr【j】**之和不超过 **N** ，则递增 **i** 并递减 **j** 。
4.  否则减量 **j** 。
5.  重复以上步骤直到 **i < = j** 并计算每一步。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum steps
int countMinSteps(int arr[], int target,
                int n)
{

    // Function to sort the array
    sort(arr, arr + n);
    int minimumSteps = 0;
    int i = 0, j = n - 1;

    // Run while loop
    while (i <= j) {

        // Condition to check whether
        // sum exceed the target or not
        if (arr[i] + arr[j] <= target) {
            i++;
            j--;
        }
        else {
            j--;
        }

        // Increment the step
        // by 1
        minimumSteps++;
    }

    // Return minimum steps
    return minimumSteps;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 6, 2, 9, 6, 5, 8, 10 };

    // Given target value
    int target = 11;

    int size = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << countMinSteps(arr, target, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program implementation
// of the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to count minimum steps    
static int countMinSteps(int arr[],
                         int target,
                         int n)
{

    // Function to sort the array
    Arrays.sort(arr);

    int minimumSteps = 0;
    int i = 0;
    int j = n - 1;

    // Run while loop
    while (i <= j)
    {

        // Condition to check whether
        // sum exceed the target or not
        if (arr[i] + arr[j] <= target)
        {
            i += 1;
            j -= 1;
        }
        else
        {
            j -= 1;
        }

        // Increment the step by 1
        minimumSteps += 1;
    }

    // Return minimum steps
    return minimumSteps;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 2, 9, 6, 5, 8, 10 };

    // Given target value
    int target = 11;

    int size = arr.length;

    // Print the minimum flip
    System.out.print(countMinSteps(arr, target,
                                        size));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum steps
def countMinSteps(arr, target, n):

    # Function to sort the array
    arr.sort()

    minimumSteps = 0
    i, j = 0, n - 1

    # Run while loop
    while i <= j:

        # Condition to check whether
        # sum exceed the target or not
        if arr[i] + arr[j] <= target:
            i += 1
            j -= 1
        else:
            j -= 1

        # Increment the step
        # by 1
        minimumSteps += 1

    # Return minimum steps
    return minimumSteps

# Driver code

# Given array arr[]
arr = [ 4, 6, 2, 9, 6, 5, 8, 10 ]

# Given target value
target = 11

size = len(arr)

# Function call
print(countMinSteps(arr, target, size))

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program implementation
// of the above approach
using System;

class GFG{

// Function to count minimum steps    
static int countMinSteps(int[] arr,
                         int target,
                         int n)
{

    // Function to sort the array
    Array.Sort(arr);

    int minimumSteps = 0;
    int i = 0;
    int j = n - 1;

    // Run while loop
    while (i <= j)
    {

        // Condition to check whether
        // sum exceed the target or not
        if (arr[i] + arr[j] <= target)
        {
            i += 1;
            j -= 1;
        }
        else
        {
            j -= 1;
        }

        // Increment the step by 1
        minimumSteps += 1;
    }

    // Return minimum steps
    return minimumSteps;
}

// Driver code
public static void Main()
{
    int[] arr = new int[]{ 4, 6, 2, 9,
                           6, 5, 8, 10 };

    // Given target value
    int target = 11;

    int size = arr.Length;

    // Print the minimum flip
    Console.Write(countMinSteps(
                  arr, target, size));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to count minimum steps
function countMinSteps(arr, target, n)
{

    // Function to sort the array
    arr = arr.sort(function(a, b) {
  return a - b;
});
    var minimumSteps = 0;
    var i = 0, j = n - 1;

    // Run while loop
    while (i <= j) {

        // Condition to check whether
        // sum exceed the target or not
        if (arr[i] + arr[j] <= target) {
            i++;
            j--;
        }
        else {
            j--;
        }

        // Increment the step
        // by 1
        minimumSteps++;
    }

    // Return minimum steps
    return minimumSteps;
}

// Driver Code

    // Given array arr[]
    var arr = [4, 6, 2, 9, 6, 5, 8, 10];

    // Given target value
    var target = 11;

    var size = arr.length;

    // Function call
    document.write(countMinSteps(arr, target, size));

// This code is contributed by ipg2016107.
</script>
```

**输出:**

```
5
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*