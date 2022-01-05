# 包含 Q 查询的给定元素 X 的数组中的最大间隔

> 原文:[https://www . geeksforgeeks . org/包含给定元素 x 的最大数组间隔查询/](https://www.geeksforgeeks.org/largest-interval-in-an-array-that-contains-the-given-element-x-for-q-queries/)

给定一个由 **N** 元素和 **Q** 查询组成的**【X】**数组**arr[]**。对于每个查询，任务是找到数组的最大区间**【L，R】**，使得区间中最大的元素为**arr【X】**，使得 **1 ≤ L ≤ X ≤ R** 。
**注意:**数组有基于 1 的索引。

**示例:**

> **输入:** N = 5，arr[] = {2，1，2，3，2}，Q = 3，query[] = {1，2，4}
> **输出:**
> 【1，3】
> 【2，2】
> 【1，5】
> **说明:**
> 在第一次查询中，x = 1，所以 arr[x] = 2，答案为 L = 1，R = 3。在这里，我们可以看到 max(arr[1]，arr[2]，arr[3]) = arr[x]，这是最大间隔。
> 在第二个查询中，x = 2，所以 arr[x] = 1，由于它是数组中最小的元素，所以区间只包含一个元素，因此范围为[2，2]。
> 第三次查询，x = 4，所以 arr[x] = 4，这是 arr[]的最大元素，所以答案是全数组，L = 1，R = N。
> 
> **输入:** N = 4，arr[] = { 1，2，2，4}，Q = 2，query[] = {1，2}
> **输出:**
> 【1，1】
> 【1，3】
> **解释:**
> 在第一次查询中，x = 1，所以 arr[x] = 1 并且由于它是数组中最小的元素，所以区间只包含一个元素，因此范围为[1，1]。
> 第二次查询，x = 2，所以 arr[x] = 2，答案是 L = 1，R = 3。在这里，我们可以看到 max(arr[1]，arr[2]，arr[3]) = arr[x] = arr[2] = 2，这是最大间隔。

**方法:**思路是预计算**arr【】**中从 **1 到 N** 的每个值 **K** 的最大区间。以下是步骤:

1.  对于**arr【】**中的每个元素 **K** ，固定元素 **K** 的索引，然后找出我们可以将间隔扩展到它的左右多少。
2.  递减左迭代器直到 **arr【左】≤ K** ，类似地递增右迭代器直到 **arr【右】≤ K** 。
3.  左右的最终值代表区间的开始和结束索引，分别存储在 **arrL[]** 和 **arrR[]** 中。
4.  在我们预先计算了每个值的区间范围之后。然后，对于每个查询，我们需要打印 **arr[x]** 的间隔范围，即 **arrL[arr[x]]** 和 **arrR[arr[x]]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to precompute the interval
// for each query
void utilLargestInterval(int arr[],
                         int arrL[],
                         int arrR[],
                         int N)
{

    // For every values [1, N] find
    // the longest intervals
    for (int maxValue = 1;
         maxValue <= N; maxValue++) {

        int lastIndex = 0;

        // Iterate the array arr[]
        for (int i = 1; i <= N; i++) {

            if (lastIndex >= i
                || arr[i] != maxValue)
                continue;
            int left = i, right = i;

            // Shift the left pointers
            while (left > 0
                   && arr[left] <= maxValue)
                left--;

            // Shift the right pointers
            while (right <= N
                   && arr[right] <= maxValue)
                right++;

            left++, right--;
            lastIndex = right;

            // Store the range of interval
            // in arrL[] and arrR[].
            for (int j = left; j <= right; j++) {

                if (arr[j] == maxValue) {
                    arrL[j] = left;
                    arrR[j] = right;
                }
            }
        }
    }
}

// Function to find the largest interval
// for each query in Q[]
void largestInterval(
    int arr[], int query[], int N, int Q)
{

    // To store the L and R of X
    int arrL[N + 1], arrR[N + 1];

    // Function Call
    utilLargestInterval(arr, arrL,
                        arrR, N);

    // Iterate to find ranges for each query
    for (int i = 0; i < Q; i++) {

        cout << "[" << arrL[query[i]]
             << ", " << arrR[query[i]]
             << "]\n";
    }
}

// Driver Code
int main()
{
    int N = 5, Q = 3;

    // Given array arr[]
    int arr[N + 1] = { 0, 2, 1, 2, 3, 2 };

    // Given Queries
    int query[Q] = { 1, 2, 4 };

    // Function Call
    largestInterval(arr, query, N, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to precompute the interval
// for each query
static void utilLargestInterval(int arr[],
                                int arrL[],
                                int arrR[],
                                int N)
{

    // For every values [1, N] find
    // the longest intervals
    for(int maxValue = 1;
            maxValue <= N; maxValue++)
    {
       int lastIndex = 0;

       // Iterate the array arr[]
       for(int i = 1; i <= N; i++)
       {
          if (lastIndex >= i ||
                 arr[i] != maxValue)
              continue;
          int left = i, right = i;

          // Shift the left pointers
          while (left > 0 &&
                 arr[left] <= maxValue)
              left--;

          // Shift the right pointers
          while (right <= N &&
                 arr[right] <= maxValue)
              right++;

          left++;
          right--;
          lastIndex = right;

          // Store the range of interval
          // in arrL[] and arrR[].
          for(int j = left; j <= right; j++)
          {
             if (arr[j] == maxValue)
             {
                 arrL[j] = left;
                 arrR[j] = right;
             }
          }
       }
    }
}

// Function to find the largest interval
// for each query in Q[]
static void largestInterval(int arr[],
                            int query[],
                            int N, int Q)
{

    // To store the L and R of X
    int []arrL = new int[N + 1];
    int []arrR = new int[N + 1];

    // Function Call
    utilLargestInterval(arr, arrL,
                        arrR, N);

    // Iterate to find ranges for
    // each query
    for(int i = 0; i < Q; i++)
    {
       System.out.print("[" + arrL[query[i]] +
                       ", " + arrR[query[i]] + "]\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, Q = 3;

    // Given array arr[]
    int arr[] = { 0, 2, 1, 2, 3, 2 };

    // Given queries
    int query[] = { 1, 2, 4 };

    // Function call
    largestInterval(arr, query, N, Q);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to precompute the interval
# for each query
def utilLargestInterval(arr, arrL, arrR, N):

    # For every values [1, N] find
    # the longest intervals
    for maxValue in range(1, N + 1):
        lastIndex = 0

        # Iterate the array arr[]
        for i in range(N + 1):
            if (lastIndex >= i or
                   arr[i] != maxValue):
                continue

            left = i
            right = i

            # Shift the left pointers
            while (left > 0 and
               arr[left] <= maxValue):
                left -= 1

            # Shift the right pointers
            while (right <= N and
               arr[right] <= maxValue):
                right += 1

            left += 1
            right -= 1
            lastIndex = right

            # Store the range of interval
            # in arrL[] and arrR[].
            for j in range(left, right + 1):
                if (arr[j] == maxValue):
                    arrL[j] = left
                    arrR[j] = right

# Function to find the largest interval
# for each query in Q[]
def largestInterval(arr, query, N, Q):

    # To store the L and R of X
    arrL = [0 for i in range(N + 1)]
    arrR = [0 for i in range(N + 1)]

    # Function call
    utilLargestInterval(arr, arrL, arrR, N);

    # Iterate to find ranges for each query
    for i in range(Q):
        print('[' + str(arrL[query[i]]) +
             ', ' + str(arrR[query[i]]) + ']')

# Driver code
if __name__=="__main__":

    N = 5
    Q = 3

    # Given array arr[]
    arr = [ 0, 2, 1, 2, 3, 2 ]

    # Given Queries
    query = [ 1, 2, 4 ]

    # Function call
    largestInterval(arr, query, N, Q)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to precompute the interval
// for each query
static void utilLargestInterval(int []arr,
                                int []arrL,
                                int []arrR,
                                int N)
{

    // For every values [1, N] find
    // the longest intervals
    for(int maxValue = 1;
            maxValue <= N; maxValue++)
    {
       int lastIndex = 0;

       // Iterate the array []arr
       for(int i = 1; i <= N; i++)
       {
          if (lastIndex >= i ||
                 arr[i] != maxValue)
              continue;

          int left = i, right = i;

          // Shift the left pointers
          while (left > 0 &&
                 arr[left] <= maxValue)
              left--;

          // Shift the right pointers
          while (right <= N &&
                 arr[right] <= maxValue)
              right++;

          left++;
          right--;
          lastIndex = right;

          // Store the range of interval
          // in arrL[] and arrR[].
          for(int j = left; j <= right; j++)
          {
             if (arr[j] == maxValue)
             {
                 arrL[j] = left;
                 arrR[j] = right;
             }
          }
       }
    }
}

// Function to find the largest interval
// for each query in Q[]
static void largestInterval(int []arr,
                            int []query,
                            int N, int Q)
{

    // To store the L and R of X
    int []arrL = new int[N + 1];
    int []arrR = new int[N + 1];

    // Function Call
    utilLargestInterval(arr, arrL,
                        arrR, N);

    // Iterate to find ranges for
    // each query
    for(int i = 0; i < Q; i++)
    {
       Console.Write("[" + arrL[query[i]] +
                    ", " + arrR[query[i]] + "]\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5, Q = 3;

    // Given array []arr
    int []arr = { 0, 2, 1, 2, 3, 2 };

    // Given queries
    int []query = { 1, 2, 4 };

    // Function call
    largestInterval(arr, query, N, Q);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to precompute the interval
// for each query
function utilLargestInterval(arr, arrL, arrR, N)
{

    // For every values [1, N] find
    // the longest intervals
    for (var maxValue = 1;
         maxValue <= N; maxValue++) {

        var lastIndex = 0;

        // Iterate the array arr[]
        for (var i = 1; i <= N; i++) {

            if (lastIndex >= i
                || arr[i] != maxValue)
                continue;
            var left = i, right = i;

            // Shift the left pointers
            while (left > 0
                   && arr[left] <= maxValue)
                left--;

            // Shift the right pointers
            while (right <= N
                   && arr[right] <= maxValue)
                right++;

            left++, right--;
            lastIndex = right;

            // Store the range of interval
            // in arrL[] and arrR[].
            for (var j = left; j <= right; j++) {

                if (arr[j] == maxValue) {
                    arrL[j] = left;
                    arrR[j] = right;
                }
            }
        }
    }
}

// Function to find the largest interval
// for each query in Q[]
function largestInterval( arr, query, N, Q)
{

    // To store the L and R of X
    var arrL = Array(N+1).fill(0),arrR = Array(N+1).fill(0);

    // Function Call
    utilLargestInterval(arr, arrL,
                        arrR, N);

    // Iterate to find ranges for each query
    for (var i = 0; i < Q; i++) {

        document.write( "[" + arrL[query[i]]
             + ", " + arrR[query[i]]
             + "]<br>");
    }
}

// Driver Code
var N = 5, Q = 3;

// Given array arr[]
var arr = [0, 2, 1, 2, 3, 2];

// Given Queries
var query = [1, 2, 4];

// Function Call
largestInterval(arr, query, N, Q);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
[1, 3]
[2, 2]
[1, 5]
```

***时间复杂度:**O(Q+N<sup>2</sup>)*
***辅助空间:** O(N)*