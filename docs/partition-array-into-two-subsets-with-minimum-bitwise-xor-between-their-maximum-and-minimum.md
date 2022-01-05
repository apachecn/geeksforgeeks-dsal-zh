# 将数组划分为两个子集，在它们的最大值和最小值之间进行最小位异或

> 原文:[https://www . geesforgeks . org/partition-array-in-two-subset-with-minimum-bitwise-xor-and-minimum/](https://www.geeksforgeeks.org/partition-array-into-two-subsets-with-minimum-bitwise-xor-between-their-maximum-and-minimum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是将数组分成两个子集，使得第一个子集的最大值和第二个子集的最小值之间的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)最小。

**示例:**

> **输入:** arr[] = {3，1，2，6，4}
> **输出:** 1
> **解释:**
> 将给定数组拆分为两个子集{1，3}、{2，4，6}。
> 第一个子集的最大值为 3，第二个子集的最小值为 2。
> 因此，它们的按位异或等于 1。
> 
> **输入:** arr[] = {2，1，3，2，4，3}
> **输出:** 0

**方法:**想法是找到数组中的两个元素，使得两个数组元素之间的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)最小。按照以下步骤解决问题:

*   初始化一个变量，比如 **minXOR** ，以存储一个子集的最大元素和另一个子集的最小元素之间的[逐位 XOR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 的最小可能值。
*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并更新 [minXOR = min(minXOR，arr[I]^ arr[I–1])](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to split the array into two subset
// such that the Bitwise XOR between the maximum
// of one subset and minimum of other is minimum
int splitArray(int arr[], int N)
{
    // Sort the array in
    // increasing order
    sort(arr, arr + N);

    int result = INT_MAX;

    // Calculating the min Bitwise XOR
    // between consecutive elements
    for (int i = 1; i < N; i++) {
        result = min(result,
                     arr[i] - arr[i - 1]);
    }

    // Return the final
    // minimum Bitwise XOR
    return result;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 1, 2, 6, 4 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << splitArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.util.*;
class GFG{

// Function to split the array into two subset
// such that the Bitwise XOR between the maximum
// of one subset and minimum of other is minimum
static int splitArray(int arr[], int N)
{
    // Sort the array in
    // increasing order
    Arrays.sort(arr);

    int result = Integer.MAX_VALUE;

    // Calculating the min Bitwise XOR
    // between consecutive elements
    for (int i = 1; i < N; i++)
    {
        result = Math.min(result,
                          arr[i] - arr[i - 1]);
    }

    // Return the final
    // minimum Bitwise XOR
    return result;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 3, 1, 2, 6, 4 };

    // Size of array
    int N = arr.length;

    // Function Call
    System.out.print(splitArray(arr, N));
}
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to split the array into two subset
# such that the Bitwise XOR between the maximum
# of one subset and minimum of other is minimum
def splitArray(arr, N):

    # Sort the array in increasing
    # order
    arr = sorted(arr)

    result = 10 ** 9

    # Calculating the min Bitwise XOR
    # between consecutive elements
    for i in range(1, N):
        result = min(result, arr[i] ^ arr[i - 1])

    # Return the final
    # minimum Bitwise XOR
    return result

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 3, 1, 2, 6, 4 ]

    # Size of array
    N = len(arr)

    # Function Call
    print(splitArray(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to split the array into two subset
// such that the Bitwise XOR between the maximum
// of one subset and minimum of other is minimum
static int splitArray(int []arr, int N)
{
    // Sort the array in increasing order
    Array.Sort(arr);

    int result = Int32.MaxValue;

    // Calculating the min Bitwise XOR
    // between consecutive elements
    for (int i = 1; i < N; i++)
    {
        result = Math.Min(result,
                          arr[i] ^ arr[i - 1]);
    }

    // Return the final
    // minimum Bitwise XOR
    return result;
}

// Driver Code
public static void Main()
{
    // Given array arr[]
    int []arr = { 3, 1, 2, 6, 4 };

    // Size of array
    int N = arr.Length;

    // Function Call
    Console.Write(splitArray(arr, N));
}
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to split the array into two subset
// such that the Bitwise XOR between the maximum
// of one subset and minimum of other is minimum
function splitArray(arr, N)
{
    // Sort the array in
    // increasing order
    arr.sort();

    let result = Number.MAX_VALUE;

    // Calculating the min Bitwise XOR
    // between consecutive elements
    for (let i = 1; i < N; i++) {
        result = Math.min(result,
                     arr[i] - arr[i - 1]);
    }

    // Return the final
    // minimum Bitwise XOR
    return result;
}

// Driver Code
    // Given array arr[]
    let arr = [ 3, 1, 2, 6, 4 ];

    // Size of array
    let N = arr.length;

    // Function Call
    document.write(splitArray(arr, N));

</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*