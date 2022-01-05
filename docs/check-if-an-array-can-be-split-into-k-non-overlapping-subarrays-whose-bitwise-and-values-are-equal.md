# 检查一个数组是否可以拆分成 K 个不重叠的子数组，这些子数组的按位“与”值相等

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-can-split-in-k-non-overlapped-subarrays-其位和值相等/](https://www.geeksforgeeks.org/check-if-an-array-can-be-split-into-k-non-overlapping-subarrays-whose-bitwise-and-values-are-equal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是检查该数组是否可以拆分为 **K** 非重叠和非空的[子数组](https://www.geeksforgeeks.org/tag/subarray/)，使得所有子数组的[位与](https://www.geeksforgeeks.org/tag/bitwise-and)相等。如果发现为真，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = { 3，2，2，6，2 }，K = 3
> **输出:** YES
> **解释:**
> 将数组拆分为 K( = 3)个子数组为{ { 3，2 }，{ 2，6 }，{ 2 } }
> 因此，需要的输出为 YES。
> 
> **输入:** arr[] = { 4，3，5，2 }，K = 3
> T3】输出:否

**天真方法:**解决这个问题最简单的方法就是将阵列以各种可能的方式拆分成 **K** [子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，检查所有 **K** 子阵列的 Bitwise AND 是否相等。如果发现任何分割都是真的，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，想法是利用这样一个事实:如果子阵列的至少一个元素的**I<sup>th</sup>T5】位是 **0** ，那么该[子阵列的](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)[位的**with**位也是 **0** 。按照以下步骤解决问题:](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)**

*   初始化一个变量，说**标记**，检查数组是否可以被吐为 **K** 子数组，使得所有子数组的[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)相等。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **pref[][]** ，其中 **pref[i][j]** 存储直到**I<sup>th</sup>T9】索引的连续数组元素的计数，该索引的**j<sup>th</sup>T13】位被设置。****
*   迭代范围**【0，N–K】**。对于第 **i <sup>第</sup>元素**的每个 **j <sup>第</sup>T5】位，检查以下情况:**
    *   如果设置了直到第 **i <sup>第</sup>T7】索引的所有数组元素的第 **j <sup>第</sup>T3】位，并且在第 **i <sup>第</sup>T15】索引之后的数组的至少一个元素的第 **j <sup>第</sup>T11】位未设置，则更新**标志=假**。********
    *   如果直到第 **i <sup>第</sup>T7】索引的至少一个数组元素的第 j<sup>第</sup>**位没有被设置，并且在第 **i <sup>第</sup>T15】索引之后的所有数组元素的第 **j <sup>第</sup>位被设置，则更新**标志=假******
*   最后，检查标志是否等于真。如果发现为真，则打印**“是”**。
*   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to check if the array
// can be split into K subarrays whose
// bitwise AND are equal
bool equalPartitionUtil(int arr[], int N, int K)
{

    // pref[i][j]: Stores count of contiguous
    // array elements upto i-th index whose
    // j-th bit is set
    int pref[N][32];

    // Initialize pref[][] array
    memset(pref, 0, sizeof(pref));

    // Fill the prefix array
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < 32; j++) {
            if (i) {

                // Check if j-th bit set or not
                int X = ((arr[i] & (1 << j)) > 0);

                // Update pref[i][j]
                pref[i][j] = pref[i - 1][j] + X;
            }

            else {

                // Update pref[i][j]
                pref[i][j] = ((arr[i] & (1 << j)) > 0);
            }
        }
    }

    // Iterate over the range[0, N - K]
    for (int i = 0; i < N - K + 1; i++) {
        bool flag = true;

        for (int j = 0; j < 32; j++) {

            // Get count of elements that have
            // jth bit set
            int cnt = pref[i][j];

            // Check if first case is satisfied
            if (cnt == i + 1
                && pref[N - 1][j] - pref[i][j] != N - i - 1)
                flag = false;

            // Check if second case is satisfied
            if (cnt != i + 1
                && N - i - 1 - (pref[N - 1][j] - pref[i][j]) < K - 1)
                flag = false;
        }

        if (flag)
            return true;
    }

    return false;
}

// Function to check if the array
// can be split into K subarrays
// having equal value of bitwise AND
void equalPartition(int arr[], int N, int K)
{
    if (equalPartitionUtil(arr, N, K))
        cout << "YES";
    else
        cout << "NO";
}

// Driver code
int main()
{
    // Given array
    int arr[] = { 3, 2, 2, 6, 2 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 3;

    // Function Call
    equalPartition(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Utility function to check if the array
// can be split into K subarrays whose
// bitwise AND are equal
static boolean equalPartitionUtil(int arr[],
                                  int N, int K)
{

    // pref[i][j]: Stores count of contiguous
    // array elements upto i-th index whose
    // j-th bit is set
    int [][]pref = new int[N][32];

    // Fill the prefix array
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if (i > 0)
            {

                // Check if j-th bit set or not
                int X = ((arr[i] & (1 << j)) > 0) ? 1 : 0;

                // Update pref[i][j]
                pref[i][j] = pref[i - 1][j] + X;
            }

            else
            {

                // Update pref[i][j]
                pref[i][j] = ((arr[i] & (1 << j)) > 0) ? 1 : 0;
            }
        }
    }

    // Iterate over the range[0, N - K]
    for(int i = 0; i < N - K + 1; i++)
    {
        boolean flag = true;

        for(int j = 0; j < 32; j++)
        {

            // Get count of elements that have
            // jth bit set
            int cnt = pref[i][j];

            // Check if first case is satisfied
            if (cnt == i + 1 && pref[N - 1][j] -
                   pref[i][j] != N - i - 1)
                flag = false;

            // Check if second case is satisfied
            if (cnt != i + 1 && N - i - 1 - (
                pref[N - 1][j] - pref[i][j]) < K - 1)
                flag = false;
        }
        if (flag)
            return true;
    }
    return false;
}

// Function to check if the array
// can be split into K subarrays
// having equal value of bitwise AND
static void equalPartition(int arr[], int N, int K)
{
    if (equalPartitionUtil(arr, N, K))
        System.out.print("YES");
    else
        System.out.print("NO");
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 3, 2, 2, 6, 2 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 3;

    // Function Call
    equalPartition(arr, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Utility function to check if the array
# can be split into K subarrays whose
# bitwise AND are equal
def equalPartitionUtil(arr, N, K):

    # pref[i][j]: Stores count of contiguous
    # array elements upto i-th index whose
    # j-th bit is set
    pref = [[0 for x in range(32)]for y in range(N)]

    # Fill the prefix array
    for i in range(N):
        for j in range(32):
            if (i):

                # Check if j-th bit set or not
                X = ((arr[i] & (1 << j)) > 0)

                # Update pref[i][j]
                pref[i][j] = pref[i - 1][j] + X

            else:

                # Update pref[i][j]
                pref[i][j] = ((arr[i] & (1 << j)) > 0)

    # Iterate over the range[0, N - K]
    for i in range(N - K + 1):
        flag = True
        for j in range(32):

            # Get count of elements that have
            # jth bit set
            cnt = pref[i][j]

            # Check if first case is satisfied
            if (cnt == i + 1
                    and pref[N - 1][j] - pref[i][j] != N - i - 1):
                flag = False

            # Check if second case is satisfied
            if (cnt != i + 1
                    and N - i - 1 - (pref[N - 1][j] - pref[i][j]) < K - 1):
                flag = False
        if (flag):
            return True
    return False

# Function to check if the array
# can be split into K subarrays
# having equal value of bitwise AND
def equalPartition(arr, N, K):
    if (equalPartitionUtil(arr, N, K)):
        print("YES")
    else:
        print("NO")

# Driver code
if __name__ == "__main__":

    # Given array
    arr = [3, 2, 2, 6, 2]

    # Size of the array
    N = len(arr)

    # Given K
    K = 3

    # Function Call
    equalPartition(arr, N, K)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Utility function to check if the array
// can be split into K subarrays whose
// bitwise AND are equal
static bool equalPartitionUtil(int []arr,
                               int N, int K)
{

    // pref[i,j]: Stores count of contiguous
    // array elements upto i-th index whose
    // j-th bit is set
    int [,]pref = new int[N, 32];

    // Fill the prefix array
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if (i > 0)
            {

                // Check if j-th bit set or not
                int X = ((arr[i] & (1 << j)) > 0) ? 1 : 0;

                // Update pref[i,j]
                pref[i, j] = pref[i - 1, j] + X;
            }

            else
            {

                // Update pref[i,j]
                pref[i, j] = ((arr[i] & (1 << j)) > 0) ? 1 : 0;
            }
        }
    }

    // Iterate over the range[0, N - K]
    for(int i = 0; i < N - K + 1; i++)
    {
        bool flag = true;

        for(int j = 0; j < 32; j++)
        {

            // Get count of elements that have
            // jth bit set
            int cnt = pref[i, j];

            // Check if first case is satisfied
            if (cnt == i + 1 && pref[N - 1, j] -
                pref[i, j] != N - i - 1)
                flag = false;

            // Check if second case is satisfied
            if (cnt != i + 1 && N - i - 1 - (
                pref[N - 1, j] - pref[i, j]) < K - 1)
                flag = false;
        }
        if (flag)
            return true;
    }
    return false;
}

// Function to check if the array
// can be split into K subarrays
// having equal value of bitwise AND
static void equalPartition(int []arr, int N, int K)
{
    if (equalPartitionUtil(arr, N, K))
        Console.Write("YES");
    else
        Console.Write("NO");
}

// Driver code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 3, 2, 2, 6, 2 };

    // Size of the array
    int N = arr.Length;

    // Given K
    int K = 3;

    // Function Call
    equalPartition(arr, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Utility function to check if the array
// can be split into K subarrays whose
// bitwise AND are equal
function equalPartitionUtil(arr, N, K)
{

    // pref[i][j]: Stores count of contiguous
    // array elements upto i-th index whose
    // j-th bit is set
    var pref = Array.from(Array(N), ()=> Array(32).fill(0));

    // Fill the prefix array
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < 32; j++) {
            if (i) {

                // Check if j-th bit set or not
                var X = ((arr[i] & (1 << j)) > 0);

                // Update pref[i][j]
                pref[i][j] = pref[i - 1][j] + X;
            }

            else {

                // Update pref[i][j]
                pref[i][j] = ((arr[i] & (1 << j)) > 0);
            }
        }
    }

    // Iterate over the range[0, N - K]
    for (var i = 0; i < N - K + 1; i++) {
        var flag = true;

        for (var j = 0; j < 32; j++) {

            // Get count of elements that have
            // jth bit set
            var cnt = pref[i][j];

            // Check if first case is satisfied
            if (cnt == i + 1
                && pref[N - 1][j] - pref[i][j] != N - i - 1)
                flag = false;

            // Check if second case is satisfied
            if (cnt != i + 1
                && N - i - 1 - (pref[N - 1][j] - pref[i][j]) < K - 1)
                flag = false;
        }

        if (flag)
            return true;
    }

    return false;
}

// Function to check if the array
// can be split into K subarrays
// having equal value of bitwise AND
function equalPartition(arr, N, K)
{
    if (equalPartitionUtil(arr, N, K))
        document.write( "YES");
    else
        document.write( "NO");
}

// Driver code
// Given array
var arr = [ 3, 2, 2, 6, 2 ];

// Size of the array
var N = arr.length;

// Given K
var K = 3;

// Function Call
equalPartition(arr, N, K);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(32 * N)*
***辅助空间:** O(32 * N)*