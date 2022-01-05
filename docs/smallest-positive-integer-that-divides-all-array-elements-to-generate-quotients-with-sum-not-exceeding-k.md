# 将所有数组元素相除生成和不超过 K 的商的最小正整数

> 原文:[https://www . geeksforgeeks . org/最小正整数除以所有数组元素生成商和不超过-k/](https://www.geeksforgeeks.org/smallest-positive-integer-that-divides-all-array-elements-to-generate-quotients-with-sum-not-exceeding-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是找到最小正整数，使得通过将所有数组元素除以该最小正整数得到的剩余数组元素的[和不超过 **K** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**注意:**将数组元素除以最小正整数必须是[Cell](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)类型。

**示例:**

> **输入:** arr[] = {1，2，5，9}，K = 6
> **输出:** 5
> **解释:**
> 将所有数组元素除以 5 将 arr[]修改为{1，1，1，2}。
> 由于数组元素之和等于 5 ( < K)，所以需要的输出为 5。
> 
> **输入:** arr[]= {2，3，5，7，11}，K = 11
> T3】输出: 3

**天真法:**解决这个问题最简单的方法就是[找到数组](https://www.geeksforgeeks.org/how-to-find-the-maximum-element-of-an-array-using-stl-in-c/)中最大的元素，说出 **Max** ，使用变量 **i** 迭代范围**【1，Max】**，检查所有数组元素除以 **i** 后剩余数组元素的[和是否小于等于 **K** 。如果发现是真的，那么打印 **i** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

***时间复杂度:** O(N * Max)，其中 **Max** 是数组中最大的元素。*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用[二分搜索法手法](https://www.geeksforgeeks.org/binary-search/)。按照以下步骤解决问题:

*   初始化一个变量，比如 **Max** ，来存储数组中最大的[元素。](https://www.geeksforgeeks.org/how-to-find-the-maximum-element-of-an-array-using-stl-in-c/)
*   将所有数组元素相除得到剩余数组元素之和小于或等于 **K** 的最小正整数的值必须在范围**【1，最大】**内。因此，在**【1，最大值】**范围内应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。
*   初始化两个变量，比如**左= 1** 和**右=最大**，以存储所需输出值所在的范围。
*   检查是否有可能通过将数组元素除以**(左+右)/ 2** 得到小于或等于 **K** 的数组元素之和。如果发现属实，则更新**右=(左+右)/ 2** 。
*   否则，更新**左=(左+右)/2** 。
*   最后，打印**左侧**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest positive integer
// that divides array elements to get the sum <= K
int findSmallestInteger(int arr[], int N, int K)
{

    // Stores minimum possible of the smallest
    // positive integer satisfying the condition
    int left = 1;

    // Stores maximum possible of the smallest
    // positive integer satisfying the condition
    int right = *max_element(arr, arr + N);

    // Apply binary search over
    // the range [left, right]
    while (left < right) {

        // Stores middle element
        // of left and right
        int mid = (left + right) / 2;

        // Stores sum of
        // array elements
        int sum = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update sum
            sum += (arr[i] + mid - 1) / mid;
        }

        // If sum is greater than K
        if (sum > K) {

            // Update left
            left = mid + 1;
        }
        else {

            // Update right
            right = mid;
        }
    }
    return left;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    ;
    int K = 6;
    cout << findSmallestInteger(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the smallest positive integer
// that divides array elements to get the sum <= K
static int findSmallestInteger(int arr[],
                               int N, int K)
{

    // Stores minimum possible of the smallest
    // positive integer satisfying the condition
    int left = 1;

    // Stores maximum possible of the smallest
    // positive integer satisfying the condition
    int right = Arrays.stream(arr).max().getAsInt();

    // Apply binary search over
    // the range [left, right]
    while (left < right)
    {

        // Stores middle element
        // of left and right
        int mid = (left + right) / 2;

        // Stores sum of
        // array elements
        int sum = 0;

        // Traverse the array
        for(int i = 0; i < N; i++)
        {

            // Update sum
            sum += (arr[i] + mid - 1) / mid;
        }

        // If sum is greater than K
        if (sum > K)
        {

            // Update left
            left = mid + 1;
        }
        else
        {

            // Update right
            right = mid;
        }
    }
    return left;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 5, 9 };
    int N = arr.length;
    int K = 6;

    System.out.println(findSmallestInteger(arr, N, K));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the smallest positive integer
# that divides array elements to get the sum <= K
def findSmallestInteger(arr, N, K):

    # Stores minimum possible of the smallest
    # positive integer satisfying the condition
    left = 1

    # Stores maximum possible of the smallest
    # positive integer satisfying the condition
    right = max(arr)

    # Apply binary search over
    # the range [left, right]
    while (left < right):

        # Stores middle element
        # of left and right
        mid = (left + right) // 2

        # Stores sum of
        # array elements
        sum = 0

        # Traverse the array
        for i in range(N):

            # Update sum
            sum += (arr[i] + mid - 1) // mid

        # If sum is greater than K
        if (sum > K):

            # Update left
            left = mid + 1

        else:

            # Update right
            right = mid

    return left

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 5, 9]
    N = len(arr)

    K = 6
    print(findSmallestInteger(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
using System.Linq; 

class GFG{

// Function to find the smallest positive integer
// that divides array elements to get the sum <= K
static int findSmallestInteger(int[] arr,
                               int N, int K)
{

    // Stores minimum possible of the smallest
    // positive integer satisfying the condition
    int left = 1;

    // Stores maximum possible of the smallest
    // positive integer satisfying the condition
    int right = arr.Max();

    // Apply binary search over
    // the range [left, right]
    while (left < right)
    {

        // Stores middle element
        // of left and right
        int mid = (left + right) / 2;

        // Stores sum of
        // array elements
        int sum = 0;

        // Traverse the array
        for(int i = 0; i < N; i++)
        {

            // Update sum
            sum += (arr[i] + mid - 1) / mid;
        }

        // If sum is greater than K
        if (sum > K)
        {

            // Update left
            left = mid + 1;
        }
        else
        {

            // Update right
            right = mid;
        }
    }
    return left;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 5, 9 };
    int N = arr.Length;
    int K = 6;

    Console.Write(findSmallestInteger(arr, N, K));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the smallest positive integer
// that divides array elements to get the sum <= K
function findSmallestInteger(arr, N, K)
{

    // Stores minimum possible of the smallest
    // positive integer satisfying the condition
    var left = 1;

    // Stores maximum possible of the smallest
    // positive integer satisfying the condition
    var right = arr.reduce((a, b) => Math.max(a, b));

    // Apply binary search over
    // the range [left, right]
    while (left < right)
    {

        // Stores middle element
        // of left and right
        var mid = (left + right) / 2;

        // Stores sum of
        // array elements
        var sum = 0;

        // Traverse the array
        for(var i = 0; i < N; i++)
        {

            // Update sum
            sum += parseInt((arr[i] + mid - 1) / mid);
        }

        // If sum is greater than K
        if (sum > K)
        {

            // Update left
            left = mid + 1;
        }
        else
        {

            // Update right
            right = mid;
        }
    }
    return left;
}

// Driver Code
var arr = [ 1, 2, 5, 9 ];
var N = arr.length;
var K = 6;

document.write(findSmallestInteger(arr, N, K));

// This code is contributed by importantly

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N * log(Max))，其中 **Max** 是数组中最大的元素。*
***辅助空间:** O(1)*