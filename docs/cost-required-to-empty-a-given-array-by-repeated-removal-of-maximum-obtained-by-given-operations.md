# 通过重复移除给定操作获得的最大值来清空给定数组所需的成本

> 原文:[https://www . geesforgeks . org/通过重复移除给定操作获得的最大值来清空给定阵列所需的成本/](https://www.geeksforgeeks.org/cost-required-to-empty-a-given-array-by-repeated-removal-of-maximum-obtained-by-given-operations/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在按指定顺序执行下列操作任意多次后，找出移除所有数组元素的代价:

*   将给定数组中存在的[最大元素添加到成本中。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   从给定数组中移除最大元素。
*   将给定数组中的所有整数减少 **1** 。
*   移除减少到 0 的元素。

**示例:**

> **输入:** arr[] = {1，6，7，4，2，5，3}
> **输出:** 16
> **解释:**
> 第一步:当前最大元素= 7。移除 7 并将每个元素减少 1 会将数组修改为{0，5，3，1，4，2}。成本= 7。
> 第二步:当前最大元素= 5。移除 5 并将每个元素减少 1 会将数组修改为{2，0，3，1}。成本= 7 + 5 = 12。
> 第三步:电流最大值= 3。移除 3 并将每个元素减少 1 会将数组修改为{1，1}。成本= 12 + 3 = 15
> 第四步:获得的最终成本= 15 + 1 = 16
> 
> **输入:** arr[] = {6，4，6，1}
> **输出:** 13

**天真方法:**解决问题最简单的方法如下:

*   从给定数组中找到最大值
*   从阵列中移除后，将其添加到**成本**中。
*   移除最大元素后，将所有剩余的数组元素减少 1。移除所有减少到 0 的元素。
*   重复以上步骤，直到移除所有数组元素。
*   最后打印**成本**的值。

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为给定数组的大小。*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，我们的想法是观察数组中每个 i <sup>第</sup>个最大元素被添加**arr[I]–I**次到**成本**中，其中 I 是每个元素的索引 **arr[i]** 。按照以下步骤解决上述问题:

1.  [按降序排列给定的数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将每个数组元素的值**arr[I]–I**加到**成本**上，如果它大于 **0** 。
3.  完成以上步骤后，打印**成本**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the total cost
// of removing all array elements
int findCost(int* a, int n)
{
    // Sort the array in descending order
    sort(a, a + n, greater<int>());

    // Stores the total cost
    int count = 0;

    for (int j = 0; j < n; j++) {

        // Contribution of i-th
        // greatest element to the cost
        int p = a[j] - j;

        // Remove the element
        a[j] = 0;

        // If negative
        if (p < 0) {
            p = 0;
            continue;
        }

        // Add to the final cost
        count += p;
    }

    // Return the cost
    return count;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 6, 7, 4, 2, 5, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findCost(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the total cost
// of removing all array elements
static int findCost(Integer [] a, int n)
{
    // Sort the array in descending order
     Arrays.sort(a, Collections.reverseOrder());

    // Stores the total cost
    int count = 0;

    for (int j = 0; j < n; j++)
    {
        // Contribution of i-th
        // greatest element to the cost
        int p = a[j] - j;

        // Remove the element
        a[j] = 0;

        // If negative
        if (p < 0)
        {
            p = 0;
            continue;
        }

        // Add to the final cost
        count += p;
    }

    // Return the cost
    return count;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    Integer arr[] = {1, 6, 7,
                     4, 2, 5, 3};

    int N = arr.length;

    // Function Call
    System.out.print(findCost(arr, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the total cost
# of removing all array elements
def findCost(a, n):

    # Sort the array in descending order
    a.sort(reverse = True)

    # Stores the total cost
    count = 0

    for j in range(n):

        # Contribution of i-th
        # greatest element to the cost
        p = a[j] - j

        # Remove the element
        a[j] = 0

        # If negative
        if(p < 0):
            p = 0
            continue

        # Add to the final cost
        count += p

    # Return the cost
    return count

# Driver Code

# Given array arr[]
arr = [ 1, 6, 7, 4, 2, 5, 3 ]

N = len(arr)

# Function call
print(findCost(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the total cost
// of removing all array elements
static int findCost(int []a, int n)
{
    // Sort the array in descending order
    Array.Sort(a);
    Array.Reverse(a);

    // Stores the total cost
    int count = 0;

    for (int j = 0; j < n; j++)
    {
        // Contribution of i-th
        // greatest element to the cost
        int p = a[j] - j;

        // Remove the element
        a[j] = 0;

        // If negative
        if (p < 0)
        {
            p = 0;
            continue;
        }

        // Add to the readonly cost
        count += p;
    }

    // Return the cost
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []arr = {1, 6, 7,
                 4, 2, 5, 3};

    int N = arr.Length;

    // Function Call
    Console.Write(findCost(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find the total cost
      // of removing all array elements
      function findCost(a, n) {
        // Sort the array in descending order
        a.sort((x, y) => y - x);

        // Stores the total cost
        var count = 0;

        for (var j = 0; j < n; j++) {
          // Contribution of i-th
          // greatest element to the cost
          var p = a[j] - j;

          // Remove the element
          a[j] = 0;

          // If negative
          if (p < 0) {
            p = 0;
            continue;
          }
          // Add to the final cost
          count += p;
        }
        // Return the cost
        return count;
      }

      // Driver Code
      // Given array arr[]
      var arr = [1, 6, 7, 4, 2, 5, 3];
      var N = arr.length;
      // Function Call
      document.write(findCost(arr, N));
    </script>
```

**Output:** 

```
16
```

***时间复杂度:** O(NlogN)，其中 N 是给定数组的大小。*
***辅助空间:** O(1)*