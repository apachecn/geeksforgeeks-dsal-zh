# 从最大值最小的数组中选择 K 个元素

> 原文:[https://www . geesforgeks . org/select-k-elements-from-a-array-其最大值被最小化/](https://www.geeksforgeeks.org/select-k-elements-from-an-array-whose-maximum-value-is-minimized/)

给定一个具有 **N** 个整数和一个整数 **K** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是从给定数组中选择 K 个元素，使得所有值的总和为正，并且 **K 个整数**中的最大值最小。

**示例:**

> **输入:** arr[] = {10，-8，5，-5，-2，4，-1，0，11}，k = 4
> **输出:** 4
> **解释:**
> 可能的数组是{0，4，-1，-2}最大元素是 4，这是最小的可能。
> **输入:** arr[] = {-8，-5，-2，-4，-1}，k = 2
> **输出:** -1
> **说明:**
> 选择 K 元素是不可能的。

**进场:**思路是使用 [**双指针手法**](https://www.geeksforgeeks.org/two-pointers-technique/) 。以下是步骤:

*   [给定数组排序](https://www.geeksforgeeks.org/sorting-algorithms/)。
*   使用 [C++](https://www.geeksforgeeks.org/c-plus-plus/) 中的[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)从上述数组中选择最小的非负值(比如在索引 **idx** 处)。
*   如果给定数组中不存在正值，则总和始终为负值，并且 **K 元素**都不满足给定条件。
*   如果存在正整数，那么可以选择总和为正的 **K 个元素**。
*   通过使用两个指针技术，我们可以找到其和为正的 K 个整数，如下所示:
    *   将左右两个指针分别初始化为**(ind–1)**和 **ind** 。
    *   如果 ***【当前总和+ arr【左侧】*** **大于 0** ，则在索引**左侧添加元素**(为负)，以最小化 K 个选定元素中的最大值，并向左递减。
    *   否则，在索引**右侧**添加一个元素，并更新最大值和增量右侧。
    *   对以上每个步骤递减 **K** 。
    *   重复以上步骤，直到 **K 变为零**，左边小于零，或者右边到达数组末尾。
*   如果以上任一项中 **K 变为零**，则打印存储的最大值。
*   否则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to  print the maximum from K
// selected elements of the array
pair<int, bool>
kthsmallestelement(vector<int> a,
                   int n, int k)
{
    // Sort the array
    sort(a.begin(), a.end());

    // Apply Binary search for
    // first positive element
    int ind = lower_bound(a.begin(),
                          a.end(), 0)
              - a.begin();

  // Check if no element is positive
    if (ind == n - 1 && a[n - 1] < 0)
        return make_pair(INT_MAX, false);

    // Initialize pointers
    int left = ind - 1, right = ind;
    int sum = 0;

    // Iterate to select exactly K elements
    while (k--) {

        // Check if left pointer
        // is greater than 0
        if (left >= 0 && sum + a[left] > 0) {

            // Update sum
            sum = sum + a[left];
            // Decrement left
            left--;
        }

        else if (right < n) {

            // Update sum
            sum = sum + a[right];

            // Increment right
            right++;
        }

        else
            return make_pair(INT_MAX, false);
    }

    // Return the answer
    return make_pair(a[right - 1], true);
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { -8, -5, -2, -4, -1 };

    int n = arr.size();
    int k = 2;

    // Function Call
    pair<int, bool> ans
        = kthsmallestelement(arr, n, k);

    if (ans.second == false)
        cout << "-1" << endl;

    else
        cout << ans.first << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the maximum from K
// selected elements of the array
static int[] kthsmallestelement(int[] a, int n,
                                int k)
{

    // Sort the array
    Arrays.sort(a);

    // Apply Binary search for
    // first positive element
    int ind = lowerBound(a, 0, a.length, 0);

    // Check if no element is positive
    if (ind == n - 1 && a[n - 1] < 0)
        return new int[] { Integer.MAX_VALUE, 0 };

    // Initialize pointers
    int left = ind - 1, right = ind;
    int sum = 0;

    // Iterate to select exactly K elements
    while (k-- > 0)
    {

        // Check if left pointer
        // is greater than 0
        if (left >= 0 && sum + a[left] > 0)
        {

            // Update sum
            sum = sum + a[left];
            // Decrement left
            left--;
        }

        else if (right < n)
        {

            // Update sum
            sum = sum + a[right];

            // Increment right
            right++;
        }
        else
            return new int[] { Integer.MAX_VALUE, 0 };
    }

    // Return the answer
    return new int[] { a[right - 1], 1 };
}

static int lowerBound(int[] numbers, int start,
                      int length, int searchnum)
{

    // If the number is not in the
    // list it will return -1
    int answer = -1;

    // Starting point of the list
    start = 0;

    // Ending point of the list
    int end = length - 1;

    while (start <= end)
    {

        // Finding the middle point of the list
        int middle = (start + end) / 2;

        if (numbers[middle] == searchnum)
        {
            answer = middle;
            end = middle - 1;
        } else if (numbers[middle] > searchnum)
            end = middle - 1;
        else
            start = middle + 1;
    }
    if (answer == -1)
        answer = length;

    return answer;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int[] arr = { -8, -5, -2, -4, -1 };

    int n = arr.length;
    int k = 2;

    // Function call
    int[] ans = kthsmallestelement(arr, n, k);

    if (ans[1] == 0)
        System.out.print("-1" + "\n");
    else
        System.out.print(ans[0] + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find lower_bound
def LowerBound(numbers, length, searchnum):

    # If the number is not in the
    # list it will return -1
    answer = -1

    # Starting point of the list
    start = 0

    # Ending point of the list
    end = length - 1

    while start <= end:

        # Finding the middle point of the list
        middle = (start + end) // 2

        if numbers[middle] == searchnum:
            answer = middle
            end = middle - 1
        elif numbers[middle] > searchnum:
            end = middle - 1
        else:
            start = middle + 1

    if(answer == -1):
        answer = length

    return answer

# Function to print the maximum from K
# selected elements of the array
def kthsmallestelement(a, n, k):

    # Sort the array
    a.sort()

    # Apply Binary search for
    # first positive element
    ind = LowerBound(a, len(a), 0)

    # Check if no element is positive
    if (ind == n - 1 and a[n - 1] < 0):
        return make_pair(INT_MAX, False)

    # Initialize pointers
    left = ind - 1
    right = ind
    sum = 0

    # Iterate to select exactly K elements
    while (k > 0):
        k -= 1

        # Check if left pointer
        # is greater than 0
        if (left >= 0 and sum + a[left] > 0):

            # Update sum
            sum = sum + a[left]

            # Decrement left
            left -= 1

        elif (right < n):

            # Update sum
            sum = sum + a[right]

            # Increment right
            right += 1
        else:
            return [sys.maxsize, False]

    print(sys.maxsize)

    # Return the answer
    return [a[right - 1], True]

# Driver Code

# Given array arr[]
arr = [ -8, -5, -2, -4, -1 ]

n = len(arr)
k = 2

# Function call
ans = kthsmallestelement(arr, n, k)

if (ans[1] == False):
    print(-1)
else:
    print(ans[0])

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print the maximum from K
// selected elements of the array
static int[] kthsmallestelement(int[] a, int n,
                                int k)
{

    // Sort the array
    Array.Sort(a);

    // Apply Binary search for
    // first positive element
    int ind = lowerBound(a, 0, a.Length, 0);

    // Check if no element is positive
    if (ind == n - 1 && a[n - 1] < 0)
        return new int[] { int.MaxValue, 0 };

    // Initialize pointers
    int left = ind - 1, right = ind;
    int sum = 0;

    // Iterate to select exactly K elements
    while (k-- > 0)
    {

        // Check if left pointer
        // is greater than 0
        if (left >= 0 && sum + a[left] > 0)
        {

            // Update sum
            sum = sum + a[left];

            // Decrement left
            left--;
        }

        else if (right < n)
        {

            // Update sum
            sum = sum + a[right];

            // Increment right
            right++;
        }
        else
            return new int[] { int.MaxValue, 0 };
    }

    // Return the answer
    return new int[] { a[right - 1], 1 };
}

static int lowerBound(int[] numbers, int start,
                      int length, int searchnum)
{

    // If the number is not in the
    // list it will return -1
    int answer = -1;

    // Starting point of the list
    start = 0;

    // Ending point of the list
    int end = length - 1;

    while (start <= end)
    {

        // Finding the middle point of the list
        int middle = (start + end) / 2;

        if (numbers[middle] == searchnum)
        {
            answer = middle;
            end = middle - 1;
        } else if (numbers[middle] > searchnum)
            end = middle - 1;
        else
            start = middle + 1;
    }
    if (answer == -1)
        answer = length;

    return answer;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int[] arr = { -8, -5, -2, -4, -1 };

    int n = arr.Length;
    int k = 2;

    // Function call
    int[] ans = kthsmallestelement(arr, n, k);

    if (ans[1] == 0)
        Console.Write("-1" + "\n");
    else
        Console.Write(ans[0] + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to print the maximum from K
// selected elements of the array
function kthsmallestelement(a, n, k)
{

    // Sort the array
    a.sort();

    // Apply Binary search for
    // first positive element
    let ind = lowerBound(a, 0, a.length, 0);

    // Check if no element is positive
    if (ind == n - 1 && a[n - 1] < 0)
        return [ Number.MAX_VALUE, 0 ];

    // Initialize pointers
    let left = ind - 1, right = ind;
    let sum = 0;

    // Iterate to select exactly K elements
    while (k-- > 0)
    {

        // Check if left pointer
        // is greater than 0
        if (left >= 0 && sum + a[left] > 0)
        {

            // Update sum
            sum = sum + a[left];
            // Decrement left
            left--;
        }

        else if (right < n)
        {

            // Update sum
            sum = sum + a[right];

            // Increment right
            right++;
        }
        else
            return [ Number.MAX_VALUE, 0 ];
    }

    // Return the answer
    return [ a[right - 1], 1 ];
}

function lowerBound( numbers, start,
                      length, searchnum)
{

    // If the number is not in the
    // list it will return -1
    let answer = -1;

    // Starting point of the list
    start = 0;

    // Ending point of the list
    let end = length - 1;

    while (start <= end)
    {

        // Finding the middle point of the list
        let middle = (start + end) / 2;

        if (numbers[middle] == searchnum)
        {
            answer = middle;
            end = middle - 1;
        } else if (numbers[middle] > searchnum)
            end = middle - 1;
        else
            start = middle + 1;
    }
    if (answer == -1)
        answer = length;

    return answer;
}

// Driver Code

    // Given array arr[]
    let arr = [ -8, -5, -2, -4, -1 ];

    let n = arr.length;
    let k = 2;

    // Function call
    let ans = kthsmallestelement(arr, n, k);

    if (ans[1] == 0)
        document.write("-1" + "\n");
    else
        document.write(ans[0] + "\n");

</script>
```

**Output:** 

```
-1
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*