# 从给定数组

构建 MEX 数组

> 原文:[https://www . geeksforgeeks . org/construct-MEX-array-from-the-给定-array/](https://www.geeksforgeeks.org/construct-mex-array-from-the-given-array/)

给定一个具有 **N** 个不同正元素的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是生成另一个数组 **B[]** ，使得对于数组中的每个 **i** <sup>第</sup>个索引， **arr[]** ， **B[i]** 是从 **arr[]** 中缺失的最小正数，不包括 **arr[i]** 。

**示例:**

> **输入:** arr[] = {2，1，5，3}
> **输出:** B[] = {2，1，4，3}
> **说明:**排除 arr[0]后，数组为{1，5，3}，该数组中不存在的最小正数为 2。因此，B[0] = 2。类似地，在排除 arr[1]、arr[2]、arr[3]后，数组中不存在的最小正数分别为 1、4 和 3。因此，B[1] = 1，B[2] = 4，B[3] = 3。
> 
> **输入:** arr[] = {1，9，2，4}
> **输出:** B[] = {1，3，2，3}

**天真方法:**解决这个问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**对于每个索引 **i** ，初始化一个数组**hash【】**对于每个索引 **j** (其中**j**≦**I**，更新**hash【arr[j]】= 1**。现在从索引 **1** 遍历数组**hash【】**，找到 **hash[k] = 0** 的最小索引 **k** ，更新 **B[i] = k** 。最后，完成上述步骤后，打印数组 **B[]** 。

***时间复杂度:** O(N <sup>2</sup> )其中 N 是给定数组的长度。*
***辅助空间:** O(N)*

**高效途径:**对上述途径进行优化，思路是计算数组 **arr[]** 的 **MEX** ，遍历数组 **arr[]** 。如果 **arr[i]** 小于数组 **arr[]** 的 **MEX，那么排除该元素的 **MEX** 将是 **arr[i]** 本身，如果数组 **A[]** 的 **arr[i]** 大于数组 **MEX** ，那么排除后数组的 **MEX** 不会改变**

按照以下步骤解决问题:

1.  初始化一个数组，比如说 **hash[]** ，来存储数组 **arr[]** 中是否存在值 **i** 。如果存在**I****哈希[i] = 1** 否则**哈希[i] = 0。**
2.  初始化变量 **MexOfArr** 以存储数组**arr【】**的 **MEX** ，并从 **1** 遍历数组**hash【】**以找到最小索引 **j** ，对于该最小索引 **hash[j] = 0，**，这意味着数组**arr【】**中不存在值 **j** ，并存储 **MexOfArr【】**
3.  现在遍历数组， **arr[]** ，如果 **arr[i]** 小于 **MexOfArr，**则存储 **B[i] = arr[i]** 否则 **B[i] = MexOfArr** 。
4.  完成以上步骤后，打印数组 **B[]** 的元素作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAXN 100001

// Function to construct array B[] that
// stores MEX of array A[] excluding A[i]
void constructMEX(int arr[], int N)
{
    // Stores elements present in arr[]
    int hash[MAXN] = { 0 };

    // Mark all values 1, if present
    for (int i = 0; i < N; i++) {

        hash[arr[i]] = 1;
    }

    // Initialize variable to store MEX
    int MexOfArr;

    // Find MEX of arr[]
    for (int i = 1; i < MAXN; i++) {
        if (hash[i] == 0) {
            MexOfArr = i;
            break;
        }
    }

    // Stores MEX for all indices
    int B[N];

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Update MEX
        if (arr[i] < MexOfArr)
            B[i] = arr[i];

        // MEX default
        else
            B[i] = MexOfArr;
    }

    // Print the array B
    for (int i = 0; i < N; i++)
        cout << B[i] << ' ';
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 1, 5, 3 };

    // Given size
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    constructMEX(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

static int MAXN = 100001;

// Function to construct array
// B[] that stores MEX of array
// A[] excluding A[i]
static void constructMEX(int arr[],
                         int N)
{
  // Stores elements present
  // in arr[]
  int hash[] = new int[MAXN];
  for (int i = 0; i < N; i++)
  {
    hash[i] = 0;
  }

  // Mark all values 1, if
  // present
  for (int i = 0; i < N; i++)
  {
    hash[arr[i]] = 1;
  }

  // Initialize variable to
  // store MEX
  int MexOfArr = 0 ;

  // Find MEX of arr[]
  for (int i = 1; i < MAXN; i++)
  {
    if (hash[i] == 0)
    {
      MexOfArr = i;
      break;
    }
  }

  // Stores MEX for all
  // indices
  int B[] = new int[N];

  // Traverse the given array
  for (int i = 0; i < N; i++)
  {
    // Update MEX
    if (arr[i] < MexOfArr)
      B[i] = arr[i];

    // MEX default
    else
      B[i] = MexOfArr;
  }

  // Print the array B
  for (int i = 0; i < N; i++)
    System.out.print(B[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {2, 1, 5, 3};

  // Size of array
  int N = arr.length;

  // Function call
  constructMEX(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

MAXN = 100001

# Function to construct
# array B[] that stores
# MEX of array A[] excluding
# A[i]
def constructMEX(arr, N):

    # Stores elements present
    # in arr[]
    hash = [0] * MAXN

    # Mark all values 1,
    # if present
    for i in range(N):
        hash[arr[i]] = 1

    # Initialize variable to
    # store MEX
    MexOfArr = 0

    # Find MEX of arr[]
    for i in range(1, MAXN):
        if (hash[i] == 0):
            MexOfArr = i
            break

    # Stores MEX for all
    # indices
    B = [0] * N

    # Traverse the given array
    for i in range(N):

        # Update MEX
        if (arr[i] < MexOfArr):
            B[i] = arr[i]

        # MEX default
        else:
            B[i] = MexOfArr

    # Prthe array B
    for i in range(N):
        print(B[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [2, 1, 5, 3]

    # Given size
    N = len(arr)

    # Function call
    constructMEX(arr, N)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int MAXN = 100001;

// Function to construct array
// B[] that stores MEX of array
// A[] excluding A[i]
static void constructMEX(int[] arr,
                         int N)
{

  // Stores elements present
  // in arr[]
  int[] hash = new int[MAXN];
  for(int i = 0; i < N; i++)
  {
    hash[i] = 0;
  }

  // Mark all values 1, if
  // present
  for(int i = 0; i < N; i++)
  {
    hash[arr[i]] = 1;
  }

  // Initialize variable to
  // store MEX
  int MexOfArr = 0;

  // Find MEX of arr[]
  for(int i = 1; i < MAXN; i++)
  {
    if (hash[i] == 0)
    {
      MexOfArr = i;
      break;
    }
  }

  // Stores MEX for all
  // indices
  int[] B = new int[N];

  // Traverse the given array
  for(int i = 0; i < N; i++)
  {

    // Update MEX
    if (arr[i] < MexOfArr)
      B[i] = arr[i];

    // MEX default
    else
      B[i] = MexOfArr;
  }

  // Print the array B
  for(int i = 0; i < N; i++)
    Console.Write(B[i] + " ");
}

// Driver Code
public static void Main()
{

  // Given array arr[]
  int[] arr = { 2, 1, 5, 3 };

  // Size of array
  int N = arr.Length;

  // Function call
  constructMEX(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program for the above approach

var MAXN = 100001;

// Function to construct array B[] that
// stores MEX of array A[] excluding A[i]
function constructMEX(arr, N)
{
    // Stores elements present in arr[]
    var hash = Array(MAXN).fill(0);

    // Mark all values 1, if present
    for (var i = 0; i < N; i++) {

        hash[arr[i]] = 1;
    }

    // Initialize variable to store MEX
    var MexOfArr;

    // Find MEX of arr[]
    for (var i = 1; i < MAXN; i++) {
        if (hash[i] == 0) {
            MexOfArr = i;
            break;
        }
    }

    // Stores MEX for all indices
    var B = Array(N);

    // Traverse the given array
    for (var i = 0; i < N; i++) {

        // Update MEX
        if (arr[i] < MexOfArr)
            B[i] = arr[i];

        // MEX default
        else
            B[i] = MexOfArr;
    }

    // Print the array B
    for (var i = 0; i < N; i++)
        document.write( B[i] + ' ');
}

// Driver Code
// Given array
var arr = [2, 1, 5, 3];
// Given size
var N = arr.length;
// Function call
constructMEX(arr, N);

</script>
```

**Output:** 

```
2 1 4 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)