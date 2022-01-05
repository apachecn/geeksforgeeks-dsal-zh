# 根据给定条件搜索数组中的元素并修改数组的查询

> 原文:[https://www . geesforgeks . org/query-to-search-for-in-a-element-in-array-and-modify-the-array-based-on-conditions/](https://www.geeksforgeeks.org/queries-to-search-for-an-element-in-an-array-and-modify-the-array-based-on-given-conditions/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在执行由数组**操作[]** 表示的 **X** 个查询后打印该数组。每个查询的任务如下:

*   如果数组包含整数**运算【I】**，则从找到**运算【I】**的索引开始，将子数组反转到数组的末尾。
*   否则，将**操作【I】**插入到数组的末尾。

**示例:**

> **输入:** arr[] = {1，2，3，4}，X = 3，运算[] = {12，2，13 }
> T3】输出:1 12 4 3 2
> T6】解释:
> **查询 1:** arr[]，不包含 12。因此，将其附加到最后。因此，arr[] = {1，2，3，4，12}。
> **查询 2:** arr[]在索引 1 处包含 2。因此，反转子阵列 **{arr[1]，arr[4]}** 。因此，arr[] = {1，12，4，3，2}。
> **查询 3:** arr[]不包含 13。因此，将其附加到最后。因此，arr[] = {1，12，4，3，2，13}。
> 
> **输入:** arr[] = {1，1，12，6}，X = 2，运算[] = {1，13 }
> T3】输出: 1 12 4 3 2

**方法:**最简单的方法是，对于每个查询，搜索整个数组来检查相关的整数是否存在。如果出现在索引 **i** 处，并且阵列的当前大小为 **N** ，则[反转子阵列 **{arr[i]，…arr[N–1]}**](https://www.geeksforgeeks.org/reverse-an-array-upto-a-given-position/)。否则，在数组末尾插入搜索到的元素。按照以下步骤解决问题:

1.  创建函数[线性搜索数组中元素](https://www.geeksforgeeks.org/linear-search/)的索引。
2.  现在，对于每个查询，如果给定的元素不在给定的数组中，则将该元素追加到数组的末尾。
3.  否则，如果它出现在任何索引 **i** ，[从索引 **i** 到结尾](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)反转子阵列。
4.  完成上述步骤后，打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to reverse the subarray
// over the range [i, r]
void rev(vector<int> &arr, int l, int r)
{

    // Iterate over the range [l, r]
    while (l < r)
    {
        int tmp = arr[l];
        arr[l] = arr[r];
        arr[r] = tmp;
        l++;
        r--;
    }
}

// Function that perform the given
// queries for the given array
void doOperation(vector<int> &arr, int o)
{

    // Search for the element o
    int ind = -1;

    // Current size of the array
    int n = arr.size();

    for(int i = 0; i < n; i++)
    {

        // If found, break out of loop
        if (arr[i] == o)
        {
            ind = i;
            break;
        }
    }

    // If not found, append o
    if (ind == -1)
        arr.push_back(o);

    // Otherwise, reverse the
    // subarray arr[ind] to arr[n - 1]
    else
        rev(arr, ind, n - 1);
}

// Function to print the elements
// in the vector arr[]
void print(vector<int> &arr)
{

    // Traverse the array arr[]
    for(int x : arr)
    {

        // Print element
        cout << x << " ";
    }
}

// Function to perform operations
void operations(vector<int> &queries,
                vector<int> &arr)
{
    for(auto x : queries)
        doOperation(arr, x);
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };
    int x = 3;

    // Given queries
    vector<int> queries({ 12, 2, 13 });

    // Add elements to the vector
    vector<int> arr1;

    for(int z : arr)
        arr1.push_back(z);

    // Perform queries
    operations(queries, arr1);

    // Print the resultant array
    print(arr1);
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function that perform the given
    // queries for the given array
    static void doOperation(
        ArrayList<Integer> arr, int o)
    {

        // Search for the element o
        int ind = -1;

        // Current size of the array
        int n = arr.size();

        for (int i = 0; i < n; i++) {

            // If found, break out of loop
            if (arr.get(i) == o) {
                ind = i;
                break;
            }
        }

        // If not found, append o
        if (ind == -1)
            arr.add(o);

        // Otherwise, reverse the
        // subarray arr[ind] to arr[n - 1]
        else
            reverse(arr, ind, n - 1);
    }

    // Function to reverse the subarray
    // over the range [i, r]
    static void reverse(
        ArrayList<Integer> arr, int l,
        int r)
    {
        // Iterate over the range [l, r]
        while (l < r) {
            int tmp = arr.get(l);
            arr.set(l, arr.get(r));
            arr.set(r, tmp);
            l++;
            r--;
        }
    }

    // Function to print the elements
    // in the ArrayList arr[]
    static void print(ArrayList<Integer> arr)
    {
        // Traverse the array arr[]
        for (int x : arr) {

            // Print element
            System.out.print(x + " ");
        }
    }

    // Function to perform operations
    static void operations(
        int queries[],
        ArrayList<Integer> arr)
    {
        for (int x : queries)
            doOperation(arr, x);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 1, 2, 3, 4 };
        int x = 3;

        // Given queries
        int queries[] = { 12, 2, 13 };

        // Add elements to the arraylist
        ArrayList<Integer> arr1
            = new ArrayList<>();

        for (int z : arr)
            arr1.add(z);

        // Perform queries
        operations(queries, arr1);

        // Print the resultant array
        print(arr1);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to reverse the
# subarray over the range
# [i, r]
def rev(arr, l, r):

    # Iterate over the
    # range [l, r]
    while (l < r):
        arr[l], arr[r] = (arr[r],
                          arr[l])
        l += 1
        r -= 1

# Function that perform the given
# queries for the given array
def doOperation(arr, o):

    # Search for the
    # element o
    ind = -1

    # Current size of
    # the array
    n = len(arr)

    for i in range(n):

        # If found, break out
        # of loop
        if (arr[i] == o):

            ind = i
            break

    # If not found, append o
    if (ind == -1):
        arr.append(o)

    # Otherwise, reverse the
    # subarray arr[ind] to
    # arr[n - 1]
    else:
        rev(arr,
            ind, n - 1)

# Function to print the
# elements in the vector
# arr[]
def print_array(arr):

    # Traverse the
    # array arr[]
    for x in arr:

        # Print element
        print(x, end = " ")

# Function to perform
# operations
def operations(queries, arr):

    for x in queries:
        doOperation(arr, x)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 2, 3, 4]
    x = 3

    # Given queries
    queries = [12, 2, 13]

    # Add elements to the vector
    arr1 = []

    for z in arr:
        arr1.append(z)

    # Perform queries
    operations(queries, arr1)

    # Print the resultant array
    print_array(arr1)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that perform the given
// queries for the given array
static void doOperation(List<int> arr, int o)
{

    // Search for the element o
    int ind = -1;

    // Current size of the array
    int n = arr.Count;

    for(int i = 0; i < n; i++)
    {

        // If found, break out of loop
        if (arr[i] == o)
        {
            ind = i;
            break;
        }
    }

    // If not found, append o
    if (ind == -1)
        arr.Add(o);

    // Otherwise, reverse the
    // subarray arr[ind] to arr[n - 1]
    else
        reverse(arr, ind, n - 1);
}

// Function to reverse the subarray
// over the range [i, r]
static void reverse(List<int> arr, int l,
                                   int r)
{

    // Iterate over the range [l, r]
    while (l < r)
    {
        int tmp = arr[l];
        arr[l] = arr[r];
        arr[r] =  tmp;
        l++;
        r--;
    }
}

// Function to print the elements
// in the List []arr
static void print(List<int> arr)
{

    // Traverse the array []arr
    foreach(int x in arr)
    {

        // Print element
        Console.Write(x + " ");
    }
}

// Function to perform operations
static void operations(int []queries,
                       List<int> arr)
{
    foreach(int x in queries)
        doOperation(arr, x);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 2, 3, 4 };
    //int x = 3;

    // Given queries
    int []queries = { 12, 2, 13 };

    // Add elements to the arraylist
    List<int> arr1 = new List<int>();

    foreach (int z in arr)
        arr1.Add(z);

    // Perform queries
    operations(queries, arr1);

    // Print the resultant array
    print(arr1);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that perform the given
// queries for the given array
function doOperation(arr, o)
{

    // Search for the element o
    let ind = -1;

    // Current size of the array
    let n = arr.length;

    for(let i = 0; i < n; i++)
    {

        // If found, break out of loop
        if (arr[i] == o)
        {
            ind = i;
            break;
        }
    }

    // If not found, append o
    if (ind == -1)
        arr.push(o);

    // Otherwise, reverse the
    // subarray arr[ind] to arr[n - 1]
    else
        reverse(arr, ind, n - 1);
}

// Function to reverse the subarray
// over the range [i, r]
function reverse(arr, l, r)
{

    // Iterate over the range [l, r]
    while (l < r)
    {
        let tmp = arr[l];
        arr[l] = arr[r];
        arr[r] = tmp;
        l++;
        r--;
    }
}

// Function to print the elements
// in the ArrayList arr[]
function print(arr)
{
    document.write(arr.join(" "));
}

// Function to perform operations   
function operations(queries, arr)
{
    for(let x = 0; x < queries.length; x++)
        doOperation(arr, queries[x]);
}

// Driver Code
let arr = [ 1, 2, 3, 4 ];
let x = 3;

// Given queries
let queries = [ 12, 2, 13 ];

// Perform queries
operations(queries, arr);

// Print the resultant array
print(arr);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
1 12 4 3 2 13 
```

***时间复杂度:** O(N*X)，其中 N 是给定数组的大小，X 是查询的数量。*
***辅助空间:** O(N)*