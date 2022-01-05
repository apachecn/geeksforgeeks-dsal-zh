# 检查长度为 M 的子阵列是否连续重复至少 K 次

> 原文:[https://www . geeksforgeeks . org/check-if-any-subarray-of-length-m-repeats-至少 k 次-连续或不连续/](https://www.geeksforgeeks.org/check-if-any-subarray-of-length-m-repeats-at-least-k-times-consecutively-or-not/)

给定一个由 **N** 整数和两个正整数 **M** 和 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查是否存在长度为 **M** 的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，该子数组至少连续重复**K**次。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {2，1，2，1，1，1，3}，M = 2，K = 2
> **输出:**是
> **说明:**长度为 2 的子阵列{2，1}至少连续重复 K(= 2)次。
> 
> **输入:** arr[] = {7，1，3，1，1，1，3}，M = 1，K = 3
> **输出:**是

**天真方法:**最简单的方法是[生成所有可能的长度为 **M** 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查每个子阵列，在给定的阵列中，是否以一个[子阵列的形式将它精确地连接 **K** 次。如果发现是真的，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/check-whether-an-array-is-subarray-of-another-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to check if there exists
// any subarray of length M repeating
// at least K times consecutively
bool check(int arr[], int M, int K,
           int ind)
{
    // Iterate from i equal 0 to M
    for (int i = 0; i < M; i++) {

        // Iterate from j equals 1 to K
        for (int j = 1; j < K; j++) {

            // If elements at pos + i and
            // pos + i + j * M are not equal
            if (arr[ind + i]
                != arr[ind + i + j * M]) {

                return false;
            }
        }
    }
    return true;
}

// Function to check if a subarray repeats
// at least K times consecutively or not
bool SubarrayRepeatsKorMore(
    int arr[], int N, int M, int K)
{
    // Iterate from ind equal 0 to M
    for (int ind = 0;
         ind <= N - M * K; ind++) {

        // Check if subarray arr[i, i + M]
        // repeats atleast K times or not
        if (check(arr, M, K, ind)) {
            return true;
        }
    }

    // Otherwise, return false
    return false;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 2, 1, 1, 1, 3 };
    int M = 2, K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    if (SubarrayRepeatsKorMore(
            arr, N, M, K)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

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

// Function to check if there exists
// any subarray of length M repeating
// at least K times consecutively
static boolean check(int arr[], int M,
                     int K, int ind)
{

    // Iterate from i equal 0 to M
    for(int i = 0; i < M; i++)
    {

        // Iterate from j equals 1 to K
        for(int j = 1; j < K; j++)
        {

            // If elements at pos + i and
            // pos + i + j * M are not equal
            if (arr[ind + i] != arr[ind + i + j * M])
            {
                return false;
            }
        }
    }
    return true;
}

// Function to check if a subarray repeats
// at least K times consecutively or not
static boolean SubarrayRepeatsKorMore(int arr[], int N,
                                      int M, int K)
{

    // Iterate from ind equal 0 to M
    for(int ind = 0; ind <= N - M * K; ind++)
    {

        // Check if subarray arr[i, i + M]
        // repeats atleast K times or not
        if (check(arr, M, K, ind))
        {
            return true;
        }
    }

    // Otherwise, return false
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 2, 1, 1, 1, 3 };
    int M = 2, K = 2;
    int N = arr.length;

    if (SubarrayRepeatsKorMore(arr, N, M, K))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exists
# any subarray of length M repeating
# at least K times consecutively
def check(arr, M, K, ind):

    # Iterate from i equal 0 to M
    for i in range(M):

        # Iterate from j equals 1 to K
        for j in range(1, K, 1):

            # If elements at pos + i and
            # pos + i + j * M are not equal
            if (arr[ind + i] != arr[ind + i + j * M]):
                return False

    return True

# Function to check if a subarray repeats
# at least K times consecutively or not
def SubarrayRepeatsKorMore(arr, N, M, K):

    # Iterate from ind equal 0 to M
    for ind in range(N - M * K + 1):

        # Check if subarray arr[i, i + M]
        # repeats atleast K times or not
        if (check(arr, M, K, ind)):
            return True

    # Otherwise, return false
    return False

# Driver Code
if __name__ == '__main__':

    arr =  [2, 1, 2, 1, 1, 1, 3]
    M = 2
    K = 2
    N = len(arr)

    if (SubarrayRepeatsKorMore(arr, N, M, K)):
        print("Yes")
    else:
        print("No")

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if there exists
// any subarray of length M repeating
// at least K times consecutively
static bool check(int[] arr, int M, int K,
                  int ind)
{

    // Iterate from i equal 0 to M
    for(int i = 0; i < M; i++)
    {

        // Iterate from j equals 1 to K
        for(int j = 1; j < K; j++)
        {

            // If elements at pos + i and
            // pos + i + j * M are not equal
            if (arr[ind + i] != arr[ind + i + j * M])
            {
                return false;
            }
        }
    }
    return true;
}

// Function to check if a subarray repeats
// at least K times consecutively or not
static bool SubarrayRepeatsKorMore(int[] arr, int N,
                                   int M, int K)
{

    // Iterate from ind equal 0 to M
    for(int ind = 0; ind <= N - M * K; ind++)
    {

        // Check if subarray arr[i, i + M]
        // repeats atleast K times or not
        if (check(arr, M, K, ind))
        {
            return true;
        }
    }

    // Otherwise, return false
    return false;
}

// Driver code
static void Main()
{
    int[] arr = { 2, 1, 2, 1, 1, 1, 3 };
    int M = 2, K = 2;
    int N = arr.Length;

    if (SubarrayRepeatsKorMore(
            arr, N, M, K))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if there exists
// any subarray of length M repeating
// at least K times consecutively
function check(arr, M, K, ind)
{

    // Iterate from i equal 0 to M
    for(let i = 0; i < M; i++)
    {

        // Iterate from j equals 1 to K
        for(let j = 1; j < K; j++)
        {

            // If elements at pos + i and
            // pos + i + j * M are not equal
            if (arr[ind + i] !=
                arr[ind + i + j * M])
            {
                return false;
            }
        }
    }
    return true;
}

// Function to check if a subarray repeats
// at least K times consecutively or not
function SubarrayRepeatsKorMore(arr, N, M, K)
{

    // Iterate from ind equal 0 to M
    for(let ind = 0;
            ind <= N - M * K; ind++)
    {

        // Check if subarray arr[i, i + M]
        // repeats atleast K times or not
        if (check(arr, M, K, ind))
        {
            return true;
        }
    }

    // Otherwise, return false
    return false;
}

// Driver Code
let arr = [ 2, 1, 2, 1, 1, 1, 3 ];
let M = 2, K = 2;
let N = arr.length;

if (SubarrayRepeatsKorMore(arr, N, M, K))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N * M * K)*
T5**辅助空间:** O(1)

**高效方法:**上述方法可以通过使用[二指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)进行优化。按照以下步骤解决问题:

*   初始化一个变量，说**把**算作 **0** 。
*   [使用变量遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**在索引范围**【0，N–M】**内，说出 **i** ，并执行以下步骤:
    *   如果 **arr[i]** 的值等于 **arr[i + M]** ，那么将**计数**增加 **1** ，因为在子阵列中有一个**匹配**。
    *   否则，将**计数**更新为 **0** 作为相邻子阵列中有一个断点。
    *   如果**计数**的值为**M *(K–1)**，则表示存在长度 **M** 的 **K** 连续相等的子阵列。因此，打印**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果计数从未变为**M *(K–1)**，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to check if any subarray
// of length M repeats at least
// K times consecutively or not
bool checkExists(int arr[], int N,
                 int M, int K)
{
    // Stores the required count
    // of repeated subarrays
    int count = 0;

    for (int i = 0; i < N - M; i++) {

        // Check if the next continuous
        // subarray has equal elements
        if (arr[i] == arr[i + M])
            count++;
        else
            count = 0;

        // Check if K continuous subarray
        // of length M are found or not
        if (count == M * (K - 1))
            return true;
    }

    // If no subarrays are found
    return false;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 2, 1, 1, 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 2, K = 2;

    if (checkExists(arr, N, M, K)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

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

// Function to check if any subarray
// of length M repeats at least
// K times consecutively or not
static boolean checkExists(int arr[], int N,
                           int M, int K)
{

    // Stores the required count
    // of repeated subarrays
    int count = 0;

    for(int i = 0; i < N - M; i++)
    {

        // Check if the next continuous
        // subarray has equal elements
        if (arr[i] == arr[i + M])
            count++;
        else
            count = 0;

        // Check if K continuous subarray
        // of length M are found or not
        if (count == M * (K - 1))
            return true;
    }

    // If no subarrays are found
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 2, 1, 1, 1, 3 };
    int M = 2, K = 2;
    int N = arr.length;

    if (checkExists(arr, N, M, K))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if any subarray
# of length M repeats at least
# K times consecutively or not
def checkExists(arr, N, M, K):

    # Stores the required count
    # of repeated subarrays
    count = 0

    for i in range(N - M):

        # Check if the next continuous
        # subarray has equal elements
        if (arr[i] == arr[i + M]):
            count += 1
        else:
            count = 0

        # Check if K continuous subarray
        # of length M are found or not
        if (count == M * (K - 1)):
            return True

    # If no subarrays are found
    return False

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 1, 2, 1, 1, 1, 3 ]
    N = len(arr)
    M = 2
    K = 2

    if (checkExists(arr, N, M, K)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if any subarray
// of length M repeats at least
// K times consecutively or not
public static bool checkExists(int []arr, int N,
                               int M, int K)
{

    // Stores the required count
    // of repeated subarrays
    int count = 0;

    for(int i = 0; i < N - M; i++)
    {

        // Check if the next continuous
        // subarray has equal elements
        if (arr[i] == arr[i + M])
            count++;
        else
            count = 0;

        // Check if K continuous subarray
        // of length M are found or not
        if (count == M * (K - 1))
            return true;
    }

    // If no subarrays are found
    return false;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 1, 2, 1, 1, 1, 3 };
    int N = arr.Length;
    int M = 2, K = 2;

    if (checkExists(arr, N, M, K))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if any subarray
// of length M repeats at least
// K times consecutively or not
function checkExists(arr, N, M, K)
{
    // Stores the required count
    // of repeated subarrays
    let count = 0;

    for (let i = 0; i < N - M; i++) {

        // Check if the next continuous
        // subarray has equal elements
        if (arr[i] == arr[i + M])
            count++;
        else
            count = 0;

        // Check if K continuous subarray
        // of length M are found or not
        if (count == M * (K - 1))
            return true;
    }

    // If no subarrays are found
    return false;
}

// Driver Code
    let arr = [ 2, 1, 2, 1, 1, 1, 3 ];
    let N = arr.length;
    let M = 2, K = 2;

    if (checkExists(arr, N, M, K)) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)