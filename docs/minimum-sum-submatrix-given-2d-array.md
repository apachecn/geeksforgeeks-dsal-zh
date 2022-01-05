# 给定 2D 阵列中的最小和子矩阵

> 原文:[https://www . geesforgeks . org/minimum-sum-submatrix-given-2d-array/](https://www.geeksforgeeks.org/minimum-sum-submatrix-given-2d-array/)

给定一个 2D 数组，求其中的最小和子矩阵。

示例:

```
Input : M[][] = {{1, 2, -1, -4, -20},
                 {-8, -3, 4, 2, 1},
                 {3, 8, 10, 1, 3},
                 {-4, -1, 1, 7, -6}}
Output : -26
Submatrix starting from (Top, Left): (0, 0)
and ending at (Bottom, Right): (1, 4) indexes.
The elements are of the submtrix are:
{ {1, 2, -1, -4, -20},
  {-8, -3, 4, 2, 1}  } having sum = -26
```

**方法 1(天真方法):**检查给定 2D 阵列中的每个可能的子矩阵。该解决方案需要 4 个嵌套循环，并且该解决方案的时间复杂度是 O(n^4).

**方法 2(有效方法):** **卡丹的算法**对于 1D 阵列可以用来降低 O(n^3).的时间复杂度其思想是逐个固定左列和右列，并为每个左列和右列对找到最小和的连续行。我们基本上为每个固定的左右列对找到顶部和底部的行号(它们有最小和)。要查找上下行号，请从左到右计算每行中元素的总和，并将这些总和存储在一个数组中，比如 temp[]。所以 temp[i]表示第 I 行从左到右的元素之和，如果我们在 temp[]上应用 Kadane 的 1D 算法，得到 temp 的最小和子阵，这个最小和就是以左右为边界列的最小可能和。为了得到总的最小和，我们将这个和与目前为止的最小和进行比较。

## C++

```
// C++ implementation to find minimum sum
// submatrix in a given 2D array
#include <bits/stdc++.h>
using namespace std;

#define ROW 4
#define COL 5

// Implementation of Kadane's algorithm for
// 1D array. The function returns the minimum
// sum and stores starting and ending indexes
// of the minimum sum subarray at addresses
// pointed by start and finish pointers
// respectively.
int kadane(int* arr, int* start, int* finish,
                                       int n)
{
    // initialize sum, maxSum and
    int sum = 0, minSum = INT_MAX, i;

    // Just some initial value to check for
    // all negative values case
    *finish = -1;

    // local variable
    int local_start = 0;

    for (i = 0; i < n; ++i) {
        sum += arr[i];
        if (sum > 0) {
            sum = 0;
            local_start = i + 1;
        } else if (sum < minSum) {
            minSum = sum;
            *start = local_start;
            *finish = i;
        }
    }

    // There is at-least one non-negative number
    if (*finish != -1)
        return minSum;

    // Special Case: When all numbers in arr[]
    // are positive
    minSum = arr[0];
    *start = *finish = 0;

    // Find the minimum element in array
    for (i = 1; i < n; i++) {
        if (arr[i] < minSum) {
            minSum = arr[i];
            *start = *finish = i;
        }
    }
    return minSum;
}

// function to find minimum sum submatrix
// in a given 2D array
void findMinSumSubmatrix(int M[][COL])
{
    // Variables to store the final output
    int minSum = INT_MAX, finalLeft, finalRight,
                          finalTop, finalBottom;

    int left, right, i;
    int temp[ROW], sum, start, finish;

    // Set the left column
    for (left = 0; left < COL; ++left) {

        // Initialize all elements of temp as 0
        memset(temp, 0, sizeof(temp));

        // Set the right column for the left
        // column set by outer loop
        for (right = left; right < COL; ++right) {

            // Calculate sum between current left
            // and right for every row 'i'
            for (i = 0; i < ROW; ++i)
                temp[i] += M[i][right];

            // Find the minimum sum subarray in temp[].
            // The kadane() function also sets values
            // of start and finish.  So 'sum' is sum of
            // rectangle between (start, left) and
            // (finish, right) which is the minimum sum
            // with boundary columns strictly as
            // left and right.
            sum = kadane(temp, &start, &finish, ROW);

            // Compare sum with maximum sum so far. If
            // sum is more, then update maxSum and other
            // output values
            if (sum < minSum) {
                minSum = sum;
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
            }
        }
    }

    // Print final values
    cout << "(Top, Left): (" << finalTop << ", "
            << finalLeft << ")\n";
    cout << "(Bottom, Right): (" << finalBottom << ", "
         << finalRight << ")\n";
    cout << "Minimum sum: " << minSum;
}

// Driver program to test above
int main()
{
    int M[ROW][COL] = { { 1, 2, -1, -4, -20 },
                        { -8, -3, 4, 2, 1 },
                        { 3, 8, 10, 1, 3 },
                        { -4, -1, 1, 7, -6 } };
    findMinSumSubmatrix(M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.*;

class GFG
{
    static int ROW = 4;
    static int COL = 5;
    static int start;
    static int finish;

    static int kadane(int[] arr, int n)
    {

        // initialize sum, maxSum and
        int sum = 0, minSum = Integer.MAX_VALUE, i;

        // Just some initial value to check for
        // all negative values case
        finish = -1;

        // local variable
        int local_start = 0;

        for (i = 0; i < n; ++i)
        {
            sum += arr[i];
            if (sum > 0)
            {
                sum = 0;
                local_start = i + 1;
            }
          else if (sum < minSum)
          {
                minSum = sum;
                start = local_start;
                finish = i;
            }
        }

        // There is at-least one non-negative number
        if (finish != -1)
            return minSum;

        // Special Case: When all numbers in arr[]
        // are positive
        minSum = arr[0];
        start = finish = 0;

        // Find the minimum element in array
        for (i = 1; i < n; i++)
        {
            if (arr[i] < minSum)
            {
                minSum = arr[i];
                start = finish = i;
            }
        }
        return minSum;

    }

    // function to find minimum sum submatrix
    // in a given 2D array
    static void findMinSumSubmatrix(int[][] M)
    {

        // Variables to store the final output
        int minSum = Integer.MAX_VALUE;
        int finalLeft = 0 , finalRight = 0, finalTop = 0, finalBottom = 0;
        int left, right, i;
        int []temp= new int[ROW];
        int sum;

        // Set the left column
        for (left = 0; left < COL; ++left)
        {

            // Initialize all elements of temp as 0
            Arrays.fill(temp, 0);

            // Set the right column for the left
            // column set by outer loop
            for (right = left; right < COL; ++right)
            {

                // Calculate sum between current left
                // and right for every row 'i'
                for (i = 0; i < ROW; ++i)
                    temp[i] += M[i][right];

                // Find the minimum sum subarray in temp[].
                // The kadane() function also sets values
                // of start and finish.  So 'sum' is sum of
                // rectangle between (start, left) and
                // (finish, right) which is the minimum sum
                // with boundary columns strictly as
                // left and right.
                sum = kadane(temp, ROW);

                // Compare sum with maximum sum so far. If
                // sum is more, then update maxSum and other
                // output values
                if (sum < minSum)
                {
                    minSum = sum;
                    finalLeft = left;
                    finalRight = right;
                    finalTop = start;
                    finalBottom = finish;
                }
            }

        }

        // Print final values
        System.out.println("(Top, Left): (" +
                           finalTop + ", " +
                           finalLeft + ")");
        System.out.println("(Bottom, Right): (" +
                           finalBottom + ", " +
                           finalRight + ")");
        System.out.println("Minimum sum: "+ minSum);

    }

    // Driver program to test above
    public static void main (String[] args)
    {
        int[][] M ={{ 1, 2, -1, -4, -20 },
                    { -8, -3, 4, 2, 1 },
                    { 3, 8, 10, 1, 3 },
                    { -4, -1, 1, 7, -6 }};
        findMinSumSubmatrix(M);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation to find minimum
# sum submatrix in a given 2D array
import sys

# Implementation of Kadane's algorithm for
# 1D array. The function returns the minimum
# sum and stores starting and ending indexes
# of the minimum sum subarray at addresses
# pointed by start and finish pointers
# respectively.
def kadane(arr, start, finish, n):

    # Initialize sum, maxSum and
    sum, minSum = 0, sys.maxsize

    # Just some initial value to check
    # for all negative values case
    finish = -1

    # Local variable
    local_start = 0

    for i in range(n):
        sum += arr[i]

        if (sum > 0):
            sum = 0
            local_start = i + 1

        elif (sum < minSum):
            minSum = sum
            start = local_start
            finish = i

    # There is at-least one non-negative number
    if (finish != -1):
        return minSum, start, finish

    # Special Case: When all numbers in arr[]
    # are positive
    minSum = arr[0]
    start, finish = 0, 0

    # Find the minimum element in array
    for i in range(1, n):
        if (arr[i] < minSum):
            minSum = arr[i]
            start = finish = i

    return minSum, start, finish

# Function to find minimum sum submatrix
# in a given 2D array
def findMinSumSubmatrix(M):

    # Variables to store the final output
    minSum = sys.maxsize
    finalLeft = 0
    finalRight = 0
    finalTop = 0
    finalBottom = 0

    #left, right, i = 0, 0, 0
    sum, start, finish = 0, 0, 0

    # Set the left column
    for left in range(5):

        # Initialize all elements of temp as 0
        temp = [0 for i in range(5)]

        # Set the right column for the left
        # column set by outer loop
        for right in range(left, 5):

            # Calculate sum between current left
            # and right for every row 'i'
            for i in range(4):
                temp[i] += M[i][right]

            # Find the minimum sum subarray in temp[].
            # The kadane() function also sets values
            # of start and finish. So 'sum' is sum of
            # rectangle between (start, left) and
            # (finish, right) which is the minimum sum
            # with boundary columns strictly as
            # left and right.
            sum, start, finish = kadane(temp, start,
                                        finish, 4)

            # Compare sum with maximum sum so far. If
            # sum is more, then update maxSum and other
            # output values
            if (sum < minSum):
                minSum = sum
                finalLeft = left
                finalRight = right
                finalTop = start
                finalBottom = finish

    # Print final values
    print("(Top, Left): (", finalTop,
          ",", finalLeft, ")")
    print("(Bottom, Right): (", finalBottom,
          ",", finalRight, ")")
    print("Minimum sum:", minSum)

# Driver code
if __name__ == '__main__':

    M = [ [ 1, 2, -1, -4, -20 ],
          [ -8, -3, 4, 2, 1 ],
          [ 3, 8, 10, 1, 3 ],
          [ -4, -1, 1, 7, -6 ] ]

    findMinSumSubmatrix(M)

# This code is contributed by mohit kumar 29
```

## C#

```
using System;
public class GFG
{
    static int ROW = 4;
    static int COL = 5;
    static int start;
    static int finish;
    static int kadane(int[] arr, int n)
    {

        // initialize sum, maxSum and
        int sum = 0, minSum = Int32.MaxValue, i;

        // Just some initial value to check for
        // all negative values case
        finish = -1;

        // local variable
        int local_start = 0;

        for (i = 0; i < n; ++i)
        {
            sum += arr[i];
            if (sum > 0)
            {
                sum = 0;
                local_start = i + 1;
            }
          else if (sum < minSum)
          {
                minSum = sum;
                start = local_start;
                finish = i;
            }
        }

        // There is at-least one non-negative number
        if (finish != -1)
            return minSum;

        // Special Case: When all numbers in arr[]
        // are positive
        minSum = arr[0];
        start = finish = 0;

        // Find the minimum element in array
        for (i = 1; i < n; i++)
        {
            if (arr[i] < minSum)
            {
                minSum = arr[i];
                start = finish = i;
            }
        }
        return minSum;
    }

    // function to find minimum sum submatrix
    // in a given 2D array
    static void findMinSumSubmatrix(int[,] M)
    {

        // Variables to store the final output
        int minSum = Int32.MaxValue;
        int finalLeft = 0 , finalRight = 0, finalTop = 0, finalBottom = 0;
        int left, right, i;
        int []temp= new int[ROW];
        int sum;

        // Set the left column
        for (left = 0; left < COL; ++left)
        {

            // Initialize all elements of temp as 0
            Array.Fill(temp, 0);

            // Set the right column for the left
            // column set by outer loop
            for (right = left; right < COL; ++right)
            {

                // Calculate sum between current left
                // and right for every row 'i'
                for (i = 0; i < ROW; ++i)
                    temp[i] += M[i, right];

                // Find the minimum sum subarray in temp[].
                // The kadane() function also sets values
                // of start and finish.  So 'sum' is sum of
                // rectangle between (start, left) and
                // (finish, right) which is the minimum sum
                // with boundary columns strictly as
                // left and right.
                sum = kadane(temp, ROW);

                // Compare sum with maximum sum so far. If
                // sum is more, then update maxSum and other
                // output values
                if (sum < minSum)
                {
                    minSum = sum;
                    finalLeft = left;
                    finalRight = right;
                    finalTop = start;
                    finalBottom = finish;
                }
            }

        }
        Console.WriteLine("(Top, Left): (" +
                          finalTop + ", " +
                          finalLeft + ")");
        Console.WriteLine("(Bottom, Right): (" +
                          finalBottom + ", " +
                          finalRight + ")");
        Console.WriteLine("Minimum sum: "+ minSum);
    }

    // Driver program to test above
    static public void Main ()
    {
        int[,] M ={{ 1, 2, -1, -4, -20 },
                   { -8, -3, 4, 2, 1 },
                   { 3, 8, 10, 1, 3 },
                   { -4, -1, 1, 7, -6 }};
        findMinSumSubmatrix(M);
    }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

/*package whatever //do not write
package name here */

    var ROW = 4;
    var COL = 5;
    var start;
    var finish;

    function kadane(arr , n) {

        // initialize sum, maxSum and
        var sum = 0, minSum = Number.MAX_VALUE, i;

        // Just some initial value to check for
        // all negative values case
        finish = -1;

        // local variable
        var local_start = 0;

        for (i = 0; i < n; ++i) {
            sum += arr[i];
            if (sum > 0) {
                sum = 0;
                local_start = i + 1;
            } else if (sum < minSum) {
                minSum = sum;
                start = local_start;
                finish = i;
            }
        }

        // There is at-least one non-negative number
        if (finish != -1)
            return minSum;

        // Special Case: When all numbers in arr
        // are positive
        minSum = arr[0];
        start = finish = 0;

        // Find the minimum element in array
        for (i = 1; i < n; i++) {
            if (arr[i] < minSum) {
                minSum = arr[i];
                start = finish = i;
            }
        }
        return minSum;

    }

    // function to find minimum sum submatrix
    // in a given 2D array
    function findMinSumSubmatrix(M)
    {

        // Variables to store the final output
        var minSum = Number.MAX_VALUE;
        var finalLeft = 0, finalRight = 0, finalTop = 0,
        finalBottom = 0;
        var left, right, i;
        var temp = Array(ROW).fill(0);
        var sum;

        // Set the left column
        for (left = 0; left < COL; ++left) {

            // Initialize all elements of temp as 0
            temp.fill(0);

            // Set the right column for the left
            // column set by outer loop
            for (right = left; right < COL; ++right)
            {

                // Calculate sum between current left
                // and right for every row 'i'
                for (i = 0; i < ROW; ++i)
                    temp[i] += M[i][right];

                // Find the minimum sum subarray in temp.
                // The kadane() function also sets values
                // of start and finish. So 'sum' is sum of
                // rectangle between (start, left) and
                // (finish, right) which is the minimum sum
                // with boundary columns strictly as
                // left and right.
                sum = kadane(temp, ROW);

                // Compare sum with maximum sum so far. If
                // sum is more, then update maxSum and other
                // output values
                if (sum < minSum) {
                    minSum = sum;
                    finalLeft = left;
                    finalRight = right;
                    finalTop = start;
                    finalBottom = finish;
                }
            }

        }

        // Print final values
        document.write("(Top, Left): (" + finalTop + ", "
        + finalLeft + ")<br/>");
        document.write("(Bottom, Right): (" + finalBottom + ", "
        + finalRight + ")<br/>");
        document.write("Minimum sum: " + minSum);

    }

    // Driver program to test above

        var M = [ [ 1, 2, -1, -4, -20 ],
                [ -8, -3, 4, 2, 1 ],
                [ 3, 8, 10, 1, 3 ],
                [ -4, -1, 1, 7, -6 ] ];
        findMinSumSubmatrix(M);

// This code contributed by umadevi9616

</script>
```

**输出:**

```
(Top, Left): (0, 0)
(Bottom, Right): (1, 4)
Minimum sum: -26
```

时间复杂性:O(n^3)

本文由 [**阿育什·乔哈里**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。