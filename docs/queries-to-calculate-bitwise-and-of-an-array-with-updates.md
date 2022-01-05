# 通过更新计算数组位与的查询

> 原文:[https://www . geeksforgeeks . org/带有更新的按位计算数组查询/](https://www.geeksforgeeks.org/queries-to-calculate-bitwise-and-of-an-array-with-updates/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个由类型为 **{i，val}** 的查询组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**[]**，每个查询的任务是将**arr【I】**替换为 **val** ，并计算修改后数组的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，Q[][] = {{0，2}，{3，3}，{4，2}}
> **输出:** 0 0 2
> **解释:**
> **查询 1:** 将 A[0]更新为 2，然后数组修改为{2，2，3，4，5}。所有元素的按位“与”为 0。
> **查询 2:** 将 A[3]更新为 3，则数组修改为{2，2，3，3，5}。所有元素的按位“与”为 0。
> **查询 3:** 将 A[4]更新为 2，然后是修改后的数组，A[]={2，2，3，3，2}。所有元素的按位“与”是 2。
> 
> **输入:** arr[] = {1，2，3}，Q[][] = {{1，5}，{2，4 } }
> T3】输出: 1 0

**朴素方法:**解决给定问题最简单的方法是为每个查询更新数组元素，然后通过[遍历每个查询中的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)来找到所有数组元素的[位与。](https://www.geeksforgeeks.org/bitwise-and-of-all-the-elements-of-array/)

***时间复杂度:** O(N * Q)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用辅助数组来优化，比如大小为 **32 * N** 的**bit count【】【】**来存储位置 **i** 处的设置位之和，直到数组的第 **j <sup>个</sup>索引**。因此，**位计数[I][N–1]**代表使用所有数组元素的位置 **i** 处的设置位的总和。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **位计数【32】【N】**来存储数组元素的设置位。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，31】**，并执行以下步骤:
    *   如果 **A[0]** 的值设置在**I<sup>th</sup>T5】位置，则更新**位计数【I】【0】**至 **1** 。否则，更新为 **0** 。**
    *   使用变量 **j** 在范围**【1，N–1】**内遍历数组 **A[]** ，并执行以下步骤:
        *   如果 **A[j]** 的值设置在**I<sup>th</sup>T5】位置，则更新**位计数【I][j】**至 **1** 。**
        *   将**位计数[I][j–1]**的值加到**位计数[i][j]** 上。
*   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**Q[][]**，并执行以下步骤:
    *   初始化一个变量，将 **res** 设为 **0** ，以存储当前查询的结果。
    *   将当前值存储在**当前值**中的给定索引处，并将新值存储在**新值**中。
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，31】**
        *   如果**新值**设置在索引 **i** 处，而**当前值**未设置，那么将**前缀【I】【N–1】**增加 **1** 。
        *   否则，如果 **currentVal** 设置在索引 **i** 处，而 **newVal** 未设置，则以 **1** 递减**前缀【I】【N–1】**。
        *   如果**前缀【I】【N–1】**的值等于 **N** ，则在 **res** 中设置该位。
    *   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Store the number of set bits at
// each position
int prefixCount[32][10000];

// Function to precompute the prefix
// count array
void findPrefixCount(vector<int> arr,
                     int size)
{
    // Iterate over the range[0, 31]
    for (int i = 0; i < 32; i++) {

        // Set the bit at position i
        // if arr[0] is set at position i
        prefixCount[i][0]
            = ((arr[0] >> i) & 1);

        // Traverse the array and
        // take prefix sum
        for (int j = 1; j < size; j++) {

            // Update prefixCount[i][j]
            prefixCount[i][j]
                = ((arr[j] >> i) & 1);
            prefixCount[i][j]
                += prefixCount[i][j - 1];
        }
    }
}

// Function to find the Bitwise AND
// of all array elements
void arrayBitwiseAND(int size)
{
    // Stores the required result
    int result = 0;

    // Iterate over the range [0, 31]
    for (int i = 0; i < 32; i++) {

        // Stores the number of set
        // bits at position i
        int temp = prefixCount[i]
                              [size - 1];

        // If temp is N, then set ith
        // position in the result
        if (temp == size)
            result = (result | (1 << i));
    }

    // Print the result
    cout << result << " ";
}

// Function to update the prefix count
// array in each query
void applyQuery(int currentVal, int newVal,
                int size)
{
    // Iterate through all the bits
    // of the current number
    for (int i = 0; i < 32; i++) {

        // Store the bit at position
        // i in the current value and
        // the new value
        int bit1 = ((currentVal >> i) & 1);
        int bit2 = ((newVal >> i) & 1);

        // If bit2 is set and bit1 is
        // unset, then increase the
        // set bits at position i by 1
        if (bit2 > 0 && bit1 == 0)
            prefixCount[i][size - 1]++;

        // If bit1 is set and bit2 is
        // unset, then decrease the
        // set bits at position i by 1
        else if (bit1 > 0 && bit2 == 0)
            prefixCount[i][size - 1]--;
    }
}

// Function to find the bitwise AND
// of the array after each query
void findbitwiseAND(
    vector<vector<int> > queries,
    vector<int> arr, int N, int M)
{
    // Fill the prefix count array
    findPrefixCount(arr, N);

    // Traverse the queries
    for (int i = 0; i < M; i++) {

        // Store the index and
        // the new value
        int id = queries[i][0];
        int newVal = queries[i][1];

        // Store the current element
        // at the index
        int currentVal = arr[id];

        // Update the array element
        arr[id] = newVal;

        // Apply the changes to the
        // prefix count array
        applyQuery(currentVal, newVal, N);

        // Print the bitwise AND of
        // the modified array
        arrayBitwiseAND(N);
    }
}

// Driver Code
int main()
{
    vector<int> arr{ 1, 2, 3, 4, 5 };
    vector<vector<int> > queries{ { 0, 2 },
                                  { 3, 3 },
                                  { 4, 2 } };
    int N = arr.size();
    int M = queries.size();
    findbitwiseAND(queries, arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Store the number of set bits at
// each position
static int prefixCount[][];

// Function to precompute the prefix
// count array
static void findPrefixCount(int arr[], int size)
{

    // Iterate over the range[0, 31]
    for(int i = 0; i < 32; i++)
    {

        // Set the bit at position i
        // if arr[0] is set at position i
        prefixCount[i][0] = ((arr[0] >> i) & 1);

        // Traverse the array and
        // take prefix sum
        for(int j = 1; j < size; j++)
        {

            // Update prefixCount[i][j]
            prefixCount[i][j] = ((arr[j] >> i) & 1);
            prefixCount[i][j] += prefixCount[i][j - 1];
        }
    }
}

// Function to find the Bitwise AND
// of all array elements
static void arrayBitwiseAND(int size)
{

    // Stores the required result
    int result = 0;

    // Iterate over the range [0, 31]
    for(int i = 0; i < 32; i++)
    {

        // Stores the number of set
        // bits at position i
        int temp = prefixCount[i][size - 1];

        // If temp is N, then set ith
        // position in the result
        if (temp == size)
            result = (result | (1 << i));
    }

    // Print the result
    System.out.print(result + " ");
}

// Function to update the prefix count
// array in each query
static void applyQuery(int currentVal, int newVal,
                       int size)
{

    // Iterate through all the bits
    // of the current number
    for(int i = 0; i < 32; i++)
    {

        // Store the bit at position
        // i in the current value and
        // the new value
        int bit1 = ((currentVal >> i) & 1);
        int bit2 = ((newVal >> i) & 1);

        // If bit2 is set and bit1 is
        // unset, then increase the
        // set bits at position i by 1
        if (bit2 > 0 && bit1 == 0)
            prefixCount[i][size - 1]++;

        // If bit1 is set and bit2 is
        // unset, then decrease the
        // set bits at position i by 1
        else if (bit1 > 0 && bit2 == 0)
            prefixCount[i][size - 1]--;
    }
}

// Function to find the bitwise AND
// of the array after each query
static void findbitwiseAND(int queries[][], int arr[],
                           int N, int M)
{

    prefixCount = new int[32][10000];

    // Fill the prefix count array
    findPrefixCount(arr, N);

    // Traverse the queries
    for(int i = 0; i < M; i++)
    {

        // Store the index and
        // the new value
        int id = queries[i][0];
        int newVal = queries[i][1];

        // Store the current element
        // at the index
        int currentVal = arr[id];

        // Update the array element
        arr[id] = newVal;

        // Apply the changes to the
        // prefix count array
        applyQuery(currentVal, newVal, N);

        // Print the bitwise AND of
        // the modified array
        arrayBitwiseAND(N);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int queries[][] = { { 0, 2 }, { 3, 3 },
                        { 4, 2 } };
    int N = arr.length;
    int M = queries.length;

    findbitwiseAND(queries, arr, N, M);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Store the number of set bits at
# each position
prefixCount = [[0 for x in range(32)]
                  for y in range(10000)]

# Function to precompute the prefix
# count array
def findPrefixCount(arr, size):

    # Iterate over the range[0, 31]
    for i in range(32):

        # Set the bit at position i
        # if arr[0] is set at position i
        prefixCount[i][0] = ((arr[0] >> i) & 1)

        # Traverse the array and
        # take prefix sum
        for j in range(1, size):

            # Update prefixCount[i][j]
            prefixCount[i][j] = ((arr[j] >> i) & 1)
            prefixCount[i][j] += prefixCount[i][j - 1]

# Function to find the Bitwise AND
# of all array elements
def arrayBitwiseAND(size):

    # Stores the required result
    result = 0

    # Iterate over the range [0, 31]
    for i in range(32):

        # Stores the number of set
        # bits at position i
        temp = prefixCount[i][size - 1]

        # If temp is N, then set ith
        # position in the result
        if (temp == size):
            result = (result | (1 << i))

    # Print the result
    print(result, end = " ")

# Function to update the prefix count
# array in each query
def applyQuery(currentVal, newVal, size):

    # Iterate through all the bits
    # of the current number
    for i in range(32):

        # Store the bit at position
        # i in the current value and
        # the new value
        bit1 = ((currentVal >> i) & 1)
        bit2 = ((newVal >> i) & 1)

        # If bit2 is set and bit1 is
        # unset, then increase the
        # set bits at position i by 1
        if (bit2 > 0 and bit1 == 0):
            prefixCount[i][size - 1] += 1

        # If bit1 is set and bit2 is
        # unset, then decrease the
        # set bits at position i by 1
        elif (bit1 > 0 and bit2 == 0):
            prefixCount[i][size - 1] -= 1

# Function to find the bitwise AND
# of the array after each query
def findbitwiseAND(queries, arr, N,  M):

    # Fill the prefix count array
    findPrefixCount(arr, N)

    # Traverse the queries
    for i in range(M):

        # Store the index and
        # the new value
        id = queries[i][0]
        newVal = queries[i][1]

        # Store the current element
        # at the index
        currentVal = arr[id]

        # Update the array element
        arr[id] = newVal

        # Apply the changes to the
        # prefix count array
        applyQuery(currentVal, newVal, N)

        # Print the bitwise AND of
        # the modified array
        arrayBitwiseAND(N)

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5 ]
    queries = [ [ 0, 2 ],
                [ 3, 3 ],
                [ 4, 2 ] ]
    N = len(arr)
    M = len(queries)

    findbitwiseAND(queries, arr, N, M)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Store the number of set bits at
// each position
static int [,]prefixCount = new int[32, 10000];

// Function to precompute the prefix
// count array
static void findPrefixCount(List<int> arr,
                            int size)
{

    // Iterate over the range[0, 31]
    for(int i = 0; i < 32; i++)
    {

        // Set the bit at position i
        // if arr[0] is set at position i
        prefixCount[i, 0] = ((arr[0] >> i) & 1);

        // Traverse the array and
        // take prefix sum
        for(int j = 1; j < size; j++)
        {

            // Update prefixCount[i][j]
            prefixCount[i, j] = ((arr[j] >> i) & 1);
            prefixCount[i, j] += prefixCount[i, j - 1];
        }
    }
}

// Function to find the Bitwise AND
// of all array elements
static void arrayBitwiseAND(int size)
{

    // Stores the required result
    int result = 0;

    // Iterate over the range [0, 31]
    for(int i = 0; i < 32; i++)
    {

        // Stores the number of set
        // bits at position i
        int temp = prefixCount[i, size - 1];

        // If temp is N, then set ith
        // position in the result
        if (temp == size)
            result = (result | (1 << i));
    }

    // Print the result
    Console.Write(result + " ");
}

// Function to update the prefix count
// array in each query
static void applyQuery(int currentVal, int newVal,
                       int size)
{

    // Iterate through all the bits
    // of the current number
    for(int i = 0; i < 32; i++)
    {

        // Store the bit at position
        // i in the current value and
        // the new value
        int bit1 = ((currentVal >> i) & 1);
        int bit2 = ((newVal >> i) & 1);

        // If bit2 is set and bit1 is
        // unset, then increase the
        // set bits at position i by 1
        if (bit2 > 0 && bit1 == 0)
            prefixCount[i, size - 1]++;

        // If bit1 is set and bit2 is
        // unset, then decrease the
        // set bits at position i by 1
        else if (bit1 > 0 && bit2 == 0)
            prefixCount[i, size - 1]--;
    }
}

// Function to find the bitwise AND
// of the array after each query
static void findbitwiseAND(int [,]queries,
                      List<int> arr, int N, int M)
{

    // Fill the prefix count array
    findPrefixCount(arr, N);

    // Traverse the queries
    for(int i = 0; i < M; i++)
    {

        // Store the index and
        // the new value
        int id = queries[i,0];
        int newVal = queries[i,1];

        // Store the current element
        // at the index
        int currentVal = arr[id];

        // Update the array element
        arr[id] = newVal;

        // Apply the changes to the
        // prefix count array
        applyQuery(currentVal, newVal, N);

        // Print the bitwise AND of
        // the modified array
        arrayBitwiseAND(N);
    }
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 1, 2, 3, 4, 5 };
    int [,] queries = new int [3, 2]{ { 0, 2 },
                                      { 3, 3 },
                                      { 4, 2 } };

    int N = arr.Count;
    int M = 3;

    findbitwiseAND(queries, arr, N, M);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Store the number of set bits at
// each position
let prefixCount = [[]];

// Function to precompute the prefix
// count array
function findPrefixCount(arr, size)
{

    // Iterate over the range[0, 31]
    for(let i = 0; i < 32; i++)
    {

        // Set the bit at position i
        // if arr[0] is set at position i
        prefixCount[i][0] = ((arr[0] >> i) & 1);

        // Traverse the array and
        // take prefix sum
        for(let j = 1; j < size; j++)
        {

            // Update prefixCount[i][j]
            prefixCount[i][j] = ((arr[j] >> i) & 1);
            prefixCount[i][j] += prefixCount[i][j - 1];
        }
    }
}

// Function to find the Bitwise AND
// of all array elements
function arrayBitwiseAND(size)
{

    // Stores the required result
    let result = 0;

    // Iterate over the range [0, 31]
    for(let i = 0; i < 32; i++)
    {

        // Stores the number of set
        // bits at position i
        let temp = prefixCount[i][size - 1];

        // If temp is N, then set ith
        // position in the result
        if (temp == size)
            result = (result | (1 << i));
    }

    // Print the result
    document.write(result + " ");
}

// Function to update the prefix count
// array in each query
function applyQuery(currentVal, newVal,
                       size)
{

    // Iterate through all the bits
    // of the current number
    for(let i = 0; i < 32; i++)
    {

        // Store the bit at position
        // i in the current value and
        // the new value
        let bit1 = ((currentVal >> i) & 1);
        let bit2 = ((newVal >> i) & 1);

        // If bit2 is set and bit1 is
        // unset, then increase the
        // set bits at position i by 1
        if (bit2 > 0 && bit1 == 0)
            prefixCount[i][size - 1]++;

        // If bit1 is set and bit2 is
        // unset, then decrease the
        // set bits at position i by 1
        else if (bit1 > 0 && bit2 == 0)
            prefixCount[i][size - 1]--;
    }
}

// Function to find the bitwise AND
// of the array after each query
function findbitwiseAND(queries, arr,
                           N, M)
{

    prefixCount = new Array(32);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < prefixCount.length; i++) {
        prefixCount[i] = new Array(2);
    }

    // Fill the prefix count array
    findPrefixCount(arr, N);

    // Traverse the queries
    for(let i = 0; i < M; i++)
    {

        // Store the index and
        // the new value
        let id = queries[i][0];
        let newVal = queries[i][1];

        // Store the current element
        // at the index
        let currentVal = arr[id];

        // Update the array element
        arr[id] = newVal;

        // Apply the changes to the
        // prefix count array
        applyQuery(currentVal, newVal, N);

        // Print the bitwise AND of
        // the modified array
        arrayBitwiseAND(N);
    }
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5 ];
    let queries = [[ 0, 2 ], [ 3, 3 ],
                        [ 4, 2 ]];
    let N = arr.length;
    let M = queries.length;

    findbitwiseAND(queries, arr, N, M);

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
0 0 2
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*