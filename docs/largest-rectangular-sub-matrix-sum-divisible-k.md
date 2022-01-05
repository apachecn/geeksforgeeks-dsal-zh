# 总和可被 k 整除的最大矩形子矩阵

> 原文:[https://www . geesforgeks . org/maximum-矩形-子矩阵-和-整除-k/](https://www.geeksforgeeks.org/largest-rectangular-sub-matrix-sum-divisible-k/)

给定一个**n×n**整数矩阵。问题是找到和能被给定值 **k** 整除的面积最大的矩形子矩阵。

**示例:**

```
Input : mat[][] = { {1, 2, -1, -4},
                    {-8, -3, 4, 2},
                    {3, 8, 10, 1},
                    {-4, -1, 1, 7} }

        k = 5

Output : Area = 12
(Top, Left): (0, 0)
(Bottom, Right): (2, 3)
The sub-matrix is:
| 1, 2, -1, -4 |
| -8, -3, 4, 2 |
| 3, 8, 10, 1  |
```

**天真方法:**检查给定 2D 数组中每个可能的矩形，其和可被“k”整除，并打印最大的一个。该解决方案需要 4 个嵌套循环，并且该解决方案的时间复杂度是 O(n^4).

**有效的方法:** [对于一维阵列，具有可被 k 整除的和的最长子阵列](https://www.geeksforgeeks.org/longest-subarray-sum-divisible-k/)可以用于降低 O(n^3).的时间复杂度其思想是逐个固定左列和右列，并为每个左列和右列对的连续行找到总和可被“k”整除的最长子阵列。我们基本上为每个固定的左右列对找到顶部和底部的行号(它们是最大子矩阵的一部分)。要查找上下行号，请从左到右计算每行中元素的总和，并将这些总和存储在一个数组中，比如 temp[]。所以 temp[i]表示第 I 行从左到右的元素之和，现在，对 temp[]应用[最长和可被 k 整除的子阵列](https://www.geeksforgeeks.org/longest-subarray-sum-divisible-k/) 1D 算法，得到 temp[]最长和可被‘k’整除的子阵列。这个长度将是以左和右作为边界列的最大可能长度。为左右列对设置“顶部”和“底部”行索引，并计算面积。以类似的方式，获取具有可被“k”整除的和的其他子矩阵的顶部、底部、左侧和右侧索引，并打印具有最大面积的子矩阵。

## C++

```
// C++ implementation to find largest rectangular
// sub-matrix having sum divisible by k
#include <bits/stdc++.h>
using namespace std;

#define SIZE 10

// function to find the longest subarray with sum divisible
// by k. The function stores starting and ending indexes of
// the subarray at addresses pointed by start and finish
// pointers respectively.
void longSubarrWthSumDivByK(int arr[], int n, int k,
                            int& start, int& finish)
{
    // unordered map 'um' implemented as
    // hash table
    unordered_map<int, int> um;

    // 'mod_arr[i]' stores (sum[0..i] % k)
    int mod_arr[n];
    int curr_sum = 0, max = 0;

    // traverse arr[] and build up the
    // array 'mod_arr[]'
    for (int i = 0; i < n; i++) {
        curr_sum += arr[i];

        // as the sum can be negative, taking modulo twice
        mod_arr[i] = ((curr_sum % k) + k) % k;
    }

    for (int i = 0; i < n; i++) {

        // if true then sum(0..i) is divisible
        // by k
        if (mod_arr[i] == 0) {

            // update variables
            max = i + 1;
            start = 0;
            finish = i;
        }

        // if value 'mod_arr[i]' not present in 'um'
        // then store it in 'um' with index of its
        // first occurrence
        else if (um.find(mod_arr[i]) == um.end())
            um[mod_arr[i]] = i;

        else
            // if true, then update variables
            if (max < (i - um[mod_arr[i]])) {
            max = i - um[mod_arr[i]];
            start = um[mod_arr[i]] + 1;
            finish = i;
        }
    }
}

// function to find largest rectangular sub-matrix
// having sum divisible by k
void findLargestSubmatrix(int mat[SIZE][SIZE], int n, int k)
{
    // Variables to store the final output
    int finalLeft, finalRight, finalTop, finalBottom;

    int left, right, i, maxArea = 0;
    int temp[n], start, finish;

    // Set the left column
    for (left = 0; left < n; left++) {

        // Initialize all elements of temp as 0
        memset(temp, 0, sizeof(temp));

        // Set the right column for the left column
        // set by outer loop
        for (right = left; right < n; right++) {

            // Calculate sum between current left and
            // right for every row 'i'
            for (i = 0; i < n; ++i)
                temp[i] += mat[i][right];

            // The longSubarrWthSumDivByK() function sets
            // the values of 'start' and 'finish'. So
            // submatrix having sum divisible by 'k' between
            // (start, left) and (finish, right) which is
            // the largest submatrix with boundary columns
            // strictly as left and right.
            longSubarrWthSumDivByK(temp, n, k, start, finish);

            // Calculate current area and compare it with
            // maximum area so far. If maxArea is less, then
            // update maxArea and other output values
            if (maxArea < ((right - left + 1) *
                          (finish - start + 1))) {
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
                maxArea = (right - left + 1) * (finish - start + 1);
            }
        }
    }

    // Print final values
    cout << "(Top, Left): (" << finalTop << ", "
         << finalLeft << ")\n";
    cout << "(Bottom, Right): (" << finalBottom << ", "
         << finalRight << ")\n";
    cout << "Area: " << maxArea;
}

// Driver program to test above functions
int main()
{
    int mat[SIZE][SIZE] = { { 1, 2, -1, -4 },
                            { -8, -3, 4, 2 },
                            { 3, 8, 10, 1 },
                            { -4, -1, 1, 7 } };

    int n = 4, k = 5;
    findLargestSubmatrix(mat, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find largest
// rectangular sub-matrix having sum
// divisible by k
import java.util.*;

class GFG{

static final int SIZE = 10;
static int start, finish;

// Function to find the longest subarray
// with sum divisible by k. The function
// stores starting and ending indexes of
// the subarray at addresses pointed by
// start and finish pointers respectively
static void longSubarrWthSumDivByK(int arr[],
                                   int n, int k)
{

    // unordered map 'um' implemented as
    // hash table
    HashMap<Integer, Integer> um = new HashMap<>();

    // 'mod_arr[i]' stores (sum[0..i] % k)
    int []mod_arr = new int[n];
    int curr_sum = 0, max = 0;

    // Traverse arr[] and build up the
    // array 'mod_arr[]'
    for(int i = 0; i < n; i++)
    {
        curr_sum += arr[i];

        // As the sum can be negative,
        // taking modulo twice
        mod_arr[i] = ((curr_sum % k) + k) % k;
    }

    for(int i = 0; i < n; i++)
    {

        // If true then sum(0..i) is
        // divisible by k
        if (mod_arr[i] == 0)
        {

            // Update variables
            max = i + 1;
            start = 0;
            finish = i;
        }

        // If value 'mod_arr[i]' not present
        // in 'um' then store it in 'um' with
        // index of its first occurrence
        else if (!um.containsKey(mod_arr[i]))
            um.put(mod_arr[i], i);

        else

            // If true, then update variables
            if (max < (i - um.get(mod_arr[i])))
            {
                max = i - um.get(mod_arr[i]);
                start = um.get(mod_arr[i]) + 1;
                finish = i;
            }
    }
}

// Function to find largest rectangular
// sub-matrix having sum divisible by k
static void findLargestSubmatrix(int mat[][],
                                 int n, int k)
{

    // Variables to store the final output
    int finalLeft = 0, finalRight = 0,
        finalTop = 0, finalBottom = 0;

    int left, right, i, maxArea = 0;
    int []temp = new int[n];

    // Set the left column
    for(left = 0; left < n; left++)
    {

        // Initialize all elements of temp as 0
        Arrays.fill(temp, 0);

        // Set the right column for the left
        // column set by outer loop
        for(right = left; right < n; right++)
        {

            // Calculate sum between current
            // left and right for every row 'i'
            for(i = 0; i < n; ++i)
                temp[i] += mat[i][right];

            // The longSubarrWthSumDivByK() function
            // sets the values of 'start' and 'finish'.
            // So submatrix having sum divisible by 'k'
            // between (start, left) and (finish, right)
            // which is the largest submatrix with
            // boundary columns strictly as left and right.
            longSubarrWthSumDivByK(temp, n, k);

            // Calculate current area and compare it
            // with maximum area so far. If maxArea
            // is less, then update maxArea and other
            // output values
            if (maxArea < ((right - left + 1) *
                          (finish - start + 1)))
            {
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
                maxArea = (right - left + 1) *
                        (finish - start + 1);
            }
        }
    }

    // Print final values
    System.out.print("(Top, Left): (" +
                     finalTop + ", " +
                     finalLeft + ")\n");
    System.out.print("(Bottom, Right): (" +
                     finalBottom + ", " +
                     finalRight + ")\n");
    System.out.print("Area: " + maxArea);
}

// Driver code
public static void main(String[] args)
{
    int [][]mat = { { 1, 2, -1, -4 },
                    { -8, -3, 4, 2 },
                    { 3, 8, 10, 1 },
                    { -4, -1, 1, 7 } };

    int n = 4, k = 5;

    findLargestSubmatrix(mat, n, k);
}
}

// This code is contributed by Amit Katiyar
```

## C#

```
// C# implementation to find largest
// rectangular sub-matrix having sum
// divisible by k
using System;
using System.Collections.Generic;

class GFG{

//static readonly int SIZE = 10;
static int start, finish;

// Function to find the longest subarray
// with sum divisible by k. The function
// stores starting and ending indexes of
// the subarray at addresses pointed by
// start and finish pointers respectively
static void longSubarrWthSumDivByK(int []arr,
                                   int n, int k)
{

    // unordered map 'um' implemented as
    // hash table
    Dictionary<int,
               int> um = new Dictionary<int,
                                        int>();

    // 'mod_arr[i]' stores (sum[0..i] % k)
    int []mod_arr = new int[n];
    int curr_sum = 0, max = 0;

    // Traverse []arr and build up the
    // array 'mod_arr[]'
    for(int i = 0; i < n; i++)
    {
        curr_sum += arr[i];

        // As the sum can be negative,
        // taking modulo twice
        mod_arr[i] = ((curr_sum % k) + k) % k;
    }

    for(int i = 0; i < n; i++)
    {

        // If true then sum(0..i) is
        // divisible by k
        if (mod_arr[i] == 0)
        {

            // Update variables
            max = i + 1;
            start = 0;
            finish = i;
        }

        // If value 'mod_arr[i]' not present
        // in 'um' then store it in 'um' with
        // index of its first occurrence
        else if (!um.ContainsKey(mod_arr[i]))
            um.Add(mod_arr[i], i);

        else

            // If true, then update variables
            if (max < (i - um[mod_arr[i]]))
            {
                max = i - um[mod_arr[i]];
                start = um[mod_arr[i]] + 1;
                finish = i;
            }
    }
}

// Function to find largest rectangular
// sub-matrix having sum divisible by k
static void findLargestSubmatrix(int [,]mat,
                                 int n, int k)
{

    // Variables to store the readonly output
    int finalLeft = 0, finalRight = 0,
        finalTop = 0, finalBottom = 0;

    int left, right, i, maxArea = 0;
    int []temp;

    // Set the left column
    for(left = 0; left < n; left++)
    {

        // Initialize all elements of temp as 0
        temp = new int[n];

        // Set the right column for the left
        // column set by outer loop
        for(right = left; right < n; right++)
        {

            // Calculate sum between current
            // left and right for every row 'i'
            for(i = 0; i < n; ++i)
                temp[i] += mat[i,right];

            // The longSubarrWthSumDivByK() function
            // sets the values of 'start' and 'finish'.
            // So submatrix having sum divisible by 'k'
            // between (start, left) and (finish, right)
            // which is the largest submatrix with
            // boundary columns strictly as left and right.
            longSubarrWthSumDivByK(temp, n, k);

            // Calculate current area and compare it
            // with maximum area so far. If maxArea
            // is less, then update maxArea and other
            // output values
            if (maxArea < ((right - left + 1) *
                          (finish - start + 1)))
            {
                finalLeft = left;
                finalRight = right;
                finalTop = start;
                finalBottom = finish;
                maxArea = (right - left + 1) *
                        (finish - start + 1);
            }
        }
    }

    // Print readonly values
    Console.Write("(Top, Left): (" +
                   finalTop + ", " +
                  finalLeft + ")\n");
    Console.Write("(Bottom, Right): (" +
                    finalBottom + ", " +
                     finalRight + ")\n");
    Console.Write("Area: " + maxArea);
}

// Driver code
public static void Main(String[] args)
{
    int [,]mat = { { 1, 2, -1, -4 },
                   { -8, -3, 4, 2 },
                   { 3, 8, 10, 1 },
                   { -4, -1, 1, 7 } };

    int n = 4, k = 5;

    findLargestSubmatrix(mat, n, k);
}
}

// This code is contributed by Princi Singh
```

**输出:**

```
(Top, Left): (0, 0)
(Bottom, Right): (2, 3)
Area: 12
```

**时间复杂度:** O(n^3).
**辅助空间:** O(n)。