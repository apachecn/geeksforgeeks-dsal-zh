# 将一个数组分解成最大数量的子数组，使它们的平均值相同

> 原文:[https://www . geesforgeks . org/break-array-max-number-sub-array-average/](https://www.geeksforgeeks.org/break-array-maximum-number-sub-arrays-averages/)

给定一个整数数组，任务是将数组分成最大数量的子数组，使得所有子数组的平均值相同。如果无法分割，则打印“不可能”。

**示例:**

```
Input : arr[] = {1, 5, 7, 2, 0};
Output : (0  1) 
         (2  4) 
Subarrays arr[0..1] and arr[2..4] 
have same average.

Input  : arr[] = {4, 6, 2, 4, 8, 0, 6, 2};    
Output : (0, 0)
         (1, 2)
         (3, 3)
         (4, 5)
         (6, 7)

Input : arr[] = {3, 3, 3};
Output : (0, 0)
         (1, 1)
         (2, 2)

Input  : arr[] = {4, 3, 5, 9, 11};
Output : Not possible
```

这个想法是基于这样一个事实，如果一个阵列可以分成相同平均值的子阵列，那么所有这些子阵列的平均值必须与总平均值相同。
1)求整个数组的平均值。
2)再次遍历数组，跟踪当前子数组的平均值。一旦平均值与总平均值相同，打印当前子阵列并开始新的子阵列。

这个解决方案划分为最大数量的子阵列，因为一旦我们发现平均值与总平均值相同，我们就开始一个新的子阵列。

## C++

```
// C++ program to break given array into maximum
// number of subarrays with equal average.
#include<bits/stdc++.h>
using namespace std;

void findSubarrays(int arr[], int n)
{
    // To store all points where we can break
    // given array into equal average subarrays.
    vector<int> result;

    // Compute total array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    int curr_sum = 0;     // Current Sum
    int prev_index = -1;  // Index of previous subarray

    for (int i = 0; i < n ; i++)
    {
        curr_sum += arr[i];

        // If current point is a break point. Note that
        // we don't compare actual averages to avoid
        // floating point errors.
        if (sum * (i - prev_index) == curr_sum * n)
        {
            // Update current sum and previous index
            curr_sum = 0;
            prev_index = i;

            // Add current break point
            result.push_back(i);
        }
    }

    // If last break point was not end of array, we
    // cannot break the whole array.
    if (prev_index != n-1)
    {
        cout << "Not Possible";
        return;
    }

    // Printing the result in required format
    cout << "(0, " << result[0] << ")\n";
    for (int i=1; i<result.size(); i++)
        cout << "(" << result[i-1] + 1 << ", "
             << result[i] << ")\n";
}

// Main Entry function code
int main()
{
    int arr[] = {4, 6, 2, 4, 8, 0, 6, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    findSubarrays(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to break given array into maximum
// number of subarrays with equal average.
import java.util.Vector;
class GFG {

static void findSubarrays(int arr[], int n)
{
    // To store all points where we can break
    // given array into equal average subarrays.
    Vector<Integer> result = new Vector<>();

    // Compute total array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    int curr_sum = 0;     // Current Sum
    int prev_index = -1;  // Index of previous subarray

    for (int i = 0; i < n ; i++)
    {
        curr_sum += arr[i];

        // If current point is a break point. Note that
        // we don't compare actual averages to avoid
        // floating point errors.
        if (sum *(i - prev_index) == curr_sum*n)
        {
            // Update current sum and previous index
            curr_sum = 0;
            prev_index = i;

            // Add current break point
            result.add(i);
        }
    }

    // If last break point was not end of array, we
    // cannot break the whole array.
    if (prev_index != n-1)
    {
        System.out.println("Not Possible");
        return;
    }

    // Printing the result in required format
    System.out.print("(0, " + result.get(0) + ")\n");
    for (int i=1; i<result.size(); i++)
        System.out.print("(" + (result.get(i-1) + 1) + ", "
             + result.get(i) + ")\n");
}

// Main Entry function code
 public static void main(String[] args) {
       int arr[] = {4, 6, 2, 4, 8, 0, 6, 2};
    int n = arr.length;
    findSubarrays(arr, n);
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to break given array
# into maximum number of subarrays with
# equal average.

def findSubarrays(arr, n):

    # To store all points where we can break
    # given array into equal average subarrays.
    result = []

    # Compute total array sum
    sum = 0
    for i in range(0, n, 1):
        sum += arr[i]

    curr_sum = 0    # Current Sum
    prev_index = -1 # Index of previous subarray

    for i in range(0, n, 1):
        curr_sum += arr[i]

        # If current point is a break point.
        # Note that we don't compare actual
        # averages to avoid floating point errors.
        if (sum *(i - prev_index) == curr_sum * n):

            # Update current sum and
            # previous index
            curr_sum = 0
            prev_index = i

            # Add current break point
            result.append(i)

    # If last break point was not end of
    # array, we cannot break the whole array.
    if (prev_index != n - 1):
        print("Not Possible", end = " ")

    # Printing the result in required format
    print("( 0 ,", result[0], ")")
    for i in range(1, len(result), 1):
        print("(", result[i - 1] + 1, ",",
                            result[i],")")

# Driver Code
if __name__ == '__main__':
    arr = [4, 6, 2, 4, 8, 0, 6, 2]
    n = len(arr)
    findSubarrays(arr, n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to break given array into maximum
// number of subarrays with equal average.
using System;
using System.Collections.Generic;

class GFG
{

static void findSubarrays(int []arr, int n)
{
    // To store all points where we can break
    // given array into equal average subarrays.
    List<int> result = new List<int>();

    // Compute total array sum
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    int curr_sum = 0;     // Current Sum
    int prev_index = -1; // Index of previous subarray

    for (int i = 0; i < n ; i++)
    {
        curr_sum += arr[i];

        // If current point is a break point. Note that
        // we don't compare actual averages to avoid
        // floating point errors.
        if (sum *(i - prev_index) == curr_sum*n)
        {
            // Update current sum and previous index
            curr_sum = 0;
            prev_index = i;

            // Add current break point
            result.Add(i);
        }
    }

    // If last break point was not end of array, we
    // cannot break the whole array.
    if (prev_index != n-1)
    {
        Console.Write("Not Possible");
        return;
    }

    // Printing the result in required format
    Console.Write("(0, " + result[0] + ")\n");
    for (int i = 1; i < result.Count; i++)
        Console.Write("(" + (result[i-1] + 1) + ", "
            + result[i] + ")\n");
}

// Driver code
public static void Main()
{
    int []arr = {4, 6, 2, 4, 8, 0, 6, 2};
    int n = arr.Length;
    findSubarrays(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program to break given array into maximum
// number of subarrays with equal average.

    function findSubarrays(arr , n) {
        // To store all points where we can break
        // given array into equal average subarrays.
        var result = [];

        // Compute total array sum
        var sum = 0;
        for (i = 0; i < n; i++)
            sum += arr[i];

        var curr_sum = 0; // Current Sum
        var prev_index = -1; // Index of previous subarray

        for (i = 0; i < n; i++) {
            curr_sum += arr[i];

            // If current point is a break point. Note that
            // we don't compare actual averages to avoid
            // floating point errors.
            if (sum * (i - prev_index) == curr_sum * n) {
                // Update current sum and previous index
                curr_sum = 0;
                prev_index = i;

                // Add current break point
                result.push(i);
            }
        }

        // If last break point was not end of array, we
        // cannot break the whole array.
        if (prev_index != n - 1) {
            document.write("Not Possible");
            return;
        }

        // Printing the result in required format
        document.write("(0, " + result[0] + ")<br/>");
        for (i = 1; i < result.length; i++)
            document.write("(" + (result[i - 1] + 1) + ", " + result[i] + ")<br/>");
    }

    // Main Entry function code

        var arr = [ 4, 6, 2, 4, 8, 0, 6, 2 ];
        var n = arr.length;
        findSubarrays(arr, n);

// This code contributed by aashish1995
</script>
```

**输出:**

```
(0, 0)
(1, 2)
(3, 3)
(4, 5)
(6, 7)
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由**克里希纳库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。