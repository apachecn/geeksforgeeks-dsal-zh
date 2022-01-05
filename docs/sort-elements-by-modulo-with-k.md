# 以 K 为模对元素进行排序

> 原文:[https://www . geeksforgeeks . org/按 k 模对元素进行排序/](https://www.geeksforgeeks.org/sort-elements-by-modulo-with-k/)

给定一个整数数组 **arr[]** 和一个整数 **K** 。任务是按照以 **K** 为模的递增顺序对给定数组的元素进行排序。如果两个数有相同的余数，那么较小的数应该排在第一位。

**示例**:

> **输入:** arr[] = {10，3，2，6，12}，K = 4
> **输出:** 12 2 6 10 3
> {12，2，6，10，3}是所需的排序顺序，因为 K = 4 的这些元素的模
> 是{0，2，2，2，3}。
> 
> **输入:** arr[] = {3，4，5，10，11，1}，K = 3
> **输出:** 3 1 4 10 5 11

**进场:**

*   创建 **K** 空[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。
*   从左到右遍历数组并更新向量，使得 **i <sup>th</sup>** 向量包含当除以 **K** 时给出 **i** 作为余数的元素。
*   [单独排序](https://www.geeksforgeeks.org/merge-sort/)所有向量，因为所有与 **K** 取模值相同的元素必须按升序排序。
*   现在，从第一个向量开始到最后一个向量，在向量中从左到右将给出所需排序顺序的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to sort the array elements
// based on their modulo with K
void sortWithRemainder(int arr[], int n, int k)
{

    // Create K empty vectors
    vector<int> v[k];

    // Update the vectors such that v[i]
    // will contain all the elements
    // that give remainder as i
    // when divided by k
    for (int i = 0; i < n; i++) {
        v[arr[i] % k].push_back(arr[i]);
    }

    // Sorting all the vectors separately
    for (int i = 0; i < k; i++)
        sort(v[i].begin(), v[i].end());

    // Replacing the elements in arr[] with
    // the required modulo sorted elements
    int j = 0;
    for (int i = 0; i < k; i++) {

        // Add all the elements of the
        // current vector to the array
        for (vector<int>::iterator it = v[i].begin();
            it != v[i].end(); it++) {

            arr[j] = *it;
            j++;
        }
    }

    // Print the sorted array
    printArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 10, 7, 2, 6, 12, 3, 33, 46 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    sortWithRemainder(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Utility function to print the
// contents of an array
static void printArr(int[] arr, int n)
{
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to sort the array elements
// based on their modulo with K
static void sortWithRemainder(int[] arr,
                              int n, int k)
{

    // Create K empty vectors
    ArrayList<
    ArrayList<Integer>> v = new ArrayList<
                                ArrayList<Integer>>(k);

    for(int i = 0; i < k; i++)
        v.add(new ArrayList<Integer>());

    // Update the vectors such that v[i]
    // will contain all the elements
    // that give remainder as i
    // when divided by k
    for(int i = 0; i < n; i++)
    {
        int t = arr[i] % k;
        v.get(t).add(arr[i]);
    }

    // Sorting all the vectors separately
    for(int i = 0; i < k; i++)
    {
        Collections.sort(v.get(i));
    }

    // Replacing the elements in
    // arr[] with the required
    // modulo sorted elements
    int j = 0;

    for(int i = 0; i < k; i++)
    {

        // Add all the elements of the
        // current vector to the array
        for(int x : v.get(i))
        {
            arr[j] = x;
            j++;
        }
    }

    // Print the sorted array
    printArr(arr, n);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 10, 7, 2, 6,
                  12, 3, 33, 46 };
    int n = arr.length;
    int k = 4;

    sortWithRemainder(arr, n, k);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# contents of an array
def printArr(arr, n):

    for i in range(n):
        print(arr[i], end = ' ')

# Function to sort the array elements
# based on their modulo with K
def sortWithRemainder(arr, n, k):

    # Create K empty vectors
    v = [[] for i in range(k)]

    # Update the vectors such that v[i]
    # will contain all the elements
    # that give remainder as i
    # when divided by k
    for i in range(n):
        v[arr[i] % k].append(arr[i])

    # Sorting all the vectors separately
    for i in range(k):
        v[i].sort()

    # Replacing the elements in arr[] with
    # the required modulo sorted elements
    j = 0

    for i in range(k):

        # Add all the elements of the
        # current vector to the array
        for it in v[i]:
            arr[j] = it
            j += 1

    # Print the sorted array
    printArr(arr, n)

# Driver code
if __name__=='__main__':

    arr = [ 10, 7, 2, 6, 12, 3, 33, 46 ]
    n = len(arr)
    k = 4

    sortWithRemainder(arr, n, k)

# This code is contributed by pratham76
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections;
class GFG{

// Utility function to print the
// contents of an array
static void printArr(int []arr,
                     int n)
{
  for (int i = 0; i < n; i++)
    Console.Write(arr[i] + " ");
}

// Function to sort the array elements
// based on their modulo with K
static void sortWithRemainder(int []arr,
                              int n, int k)
{
  // Create K empty vectors
  ArrayList []v = new ArrayList[k];

  for(int i = 0; i < k; i++)
  {
    v[i] = new ArrayList();
  }

  // Update the vectors such that v[i]
  // will contain all the elements
  // that give remainder as i
  // when divided by k
  for (int i = 0; i < n; i++)
  {
    v[arr[i] % k].Add(arr[i]);
  }

  // Sorting all the vectors separately
  for (int i = 0; i < k; i++)
  {
    v[i].Sort();
  }

  // Replacing the elements in
  // arr[] with the required
  // modulo sorted elements
  int j = 0;
  for (int i = 0; i < k; i++)
  {
    // Add all the elements of the
    // current vector to the array
    foreach(int x in v[i])
    {
      arr[j] = x;
      j++;
    }
  }

  // Print the sorted array
  printArr(arr, n);
}

// Driver Code
public static void Main(string[] args)
{
  int []arr = {10, 7, 2, 6,
               12, 3, 33, 46};
  int n = arr.Length;
  int k = 4;
  sortWithRemainder(arr, n, k);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to print the
// contents of an array
function printArr(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to sort the array elements
// based on their modulo with K
function sortWithRemainder(arr, n, k)
{

    // Create K empty vectors
    let v = new Array();

    for (let i = 0; i < k; i++)
    {
        v.push([])
    }

    // Update the vectors such that v[i]
    // will contain all the elements
    // that give remainder as i
    // when divided by k
    for (let i = 0; i < n; i++) {
        v[arr[i] % k].push(arr[i]);
    }

    // Sorting all the vectors separately
    for (let i = 0; i < k; i++)
        v[i].sort((a, b) => a - b);

        console.log(v)

    // Replacing the elements in arr[] with
    // the required modulo sorted elements
    let j = 0;
    for (let i = 0; i < k; i++) {

        // Add all the elements of the
        // current vector to the array
        for (let it of v[i]) {

            arr[j] = it;
            j++;
        }
    }

    // Print the sorted array
    printArr(arr, n);
}

// Driver code

let arr = [10, 7, 2, 6, 12, 3, 33, 46];
let n = arr.length;
let k = 4;

sortWithRemainder(arr, n, k);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
12 33 2 6 10 46 3 7
```

**时间复杂度:** O(nlogn)