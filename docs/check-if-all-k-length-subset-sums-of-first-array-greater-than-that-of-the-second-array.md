# 检查第一个数组的所有 K 长度子集和是否大于第二个数组的所有 K 长度子集和

> 原文:[https://www . geesforgeks . org/check-if-all-k-length-子集-第一个数组的和大于第二个数组的和/](https://www.geeksforgeeks.org/check-if-all-k-length-subset-sums-of-first-array-greater-than-that-of-the-second-array/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和**B【】**以及一个整数 **K** ，任务是检查[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**A【】**的大小为 **K** 的子集的所有可能的[子集和](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)是否大于[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**B【**。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** A[] = {12，11，10，13}，B[] = {7，10，6，2}，K = 3
> **输出:** YES
> **说明:**A[]中大小 K(= 3)的所有可能子集和为{33，36，35，34}。
> B[]中大小 K(= 3)的所有可能子集和为{23，19，15，18}。
> 由于数组 A[]中大小为 K 的所有子集和都大于数组 B[]中大小为 K 的所有可能子集和，因此要求的输出为“是”。
> 
> **输入:** A[] = {5，3，3，4，4，6，1}，B[] = {9，10，9，8，4，6，2}，K = 6
> **输出:**否

**天真方法:**解决这个问题最简单的方法是[从数组 **A[]和 B[]** 中生成所有可能的大小子集 **K**](https://www.geeksforgeeks.org/print-subsets-given-size-set/) ，并计算它们各自的和。检查数组 **A[]** 中得到的所有和是否超过数组 **B[]** 的和。如果发现为真，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(K×N<sup>2K</sup>)*
***辅助空间:** O(N <sup>K</sup> )*

**高效方法:**对上述方法进行优化，思路是基于这样一个事实:如果数组**A【】**的最小子集-大小之和 **K** 大于数组**B【】**的最大子集-大小之和 **K** ，则打印**“是”**。否则，打印**“否”。**按照以下步骤解决问题:

*   [按](https://www.geeksforgeeks.org/sort-c-stl/)升序排列阵**甲【】**。
*   [按降序排列数组 **B[]** 。](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查数组 **A[]** 的第一个 **K** 元素之和是否大于数组 **B[]** 的第一个 **K** 元素之和。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

以下是上述方法的实施情况；

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check all subset-sums
// of K-length subsets in A[] is greater
// that that in the array B[] or not
bool checkSubsetSum(int A[], int B[], int N,
                    int K)
{
    // Sort the array in
    // ascending order
    sort(A, A + N);

    // Sort the array in
    // descending order
    sort(B, B + N,
         greater<int>());

    // Stores sum of first K
    // elements of A[]
    int sum1 = 0;

    // Stores sum of first K
    // elements of B[]
    int sum2 = 0;

    // Traverse both the arrays
    for (int i = 0; i < K; i++) {

        // Update sum1
        sum1 += A[i];

        // Update sum2
        sum2 += B[i];
    }

    // If sum1 exceeds sum2
    if (sum1 > sum2) {
        return true;
    }

    return false;
}

// Driver Code
int main()
{
    int A[] = { 12, 11, 10, 13 };
    int B[] = { 7, 10, 6, 2 };

    int N = sizeof(A) / sizeof(A[0]);

    int K = 3;
    if (checkSubsetSum(A, B, N, K)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function reverses the elements of the array
static void reverse(int myArray[])
{
    Collections.reverse(Arrays.asList(myArray));
}

// Function to check all subset-sums
// of K-length subsets in A[] is greater
// that that in the array B[] or not
static boolean checkSubsetSum(int A[], int B[],
                              int N, int K)
{

    // Sort the array in
    // ascending order
    Arrays.sort(A);

    // Sort the array in
    // descending order
    Arrays.sort(B);
    reverse(B);

    // Stores sum of first K
    // elements of A[]
    int sum1 = 0;

    // Stores sum of first K
    // elements of B[]
    int sum2 = 0;

    // Traverse both the arrays
    for(int i = 0; i < K; i++)
    {

        // Update sum1
        sum1 += A[i];

        // Update sum2
        sum2 += B[i];
    }

    // If sum1 exceeds sum2
    if (sum1 > sum2)
    {
        return true;
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 12, 11, 10, 13 };
    int B[] = { 7, 10, 6, 2 };

    int N = A.length;
    int K = 3;

    if (checkSubsetSum(A, B, N, K))
    {
        System.out.print("YES");
    }
    else
    {
        System.out.print("NO");
    }
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check all subset-sums
# of K-length subsets in A[] is greater
# that that in the array B[] or not
def checkSubsetSum(A, B, N, K):

    # Sort the array in
    # ascending order
    A.sort()

    # Sort the array in
    # descending order
    B.sort(reverse = True)

    # Stores sum of first K
    # elements of A[]
    sum1 = 0

    # Stores sum of first K
    # elements of B[]
    sum2 = 0

    # Traverse both the arrays
    for i in range(K):

        # Update sum1
        sum1 += A[i]

        # Update sum2
        sum2 += B[i]

    # If sum1 exceeds sum2
    if (sum1 > sum2):
        return True

    return False

# Driver Code
A = [ 12, 11, 10, 13 ]
B = [ 7, 10, 6, 2]

N = len(A)
K = 3

if (checkSubsetSum(A, B, N, K)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to implement
// the above approach
using System;

public class GFG{

// Function reverses the elements of the array
static void reverse(int []myArray)
{
    Array.Sort(myArray);
    Array.Reverse(myArray);
}

// Function to check all subset-sums
// of K-length subsets in []A is greater
// that that in the array []B or not
static bool checkSubsetSum(int []A, int []B,
                              int N, int K)
{

    // Sort the array in
    // ascending order
    Array.Sort(A);

    // Sort the array in
    // descending order
    Array.Sort(B);
    reverse(B);

    // Stores sum of first K
    // elements of []A
    int sum1 = 0;

    // Stores sum of first K
    // elements of []B
    int sum2 = 0;

    // Traverse both the arrays
    for(int i = 0; i < K; i++)
    {

        // Update sum1
        sum1 += A[i];

        // Update sum2
        sum2 += B[i];
    }

    // If sum1 exceeds sum2
    if (sum1 > sum2)
    {
        return true;
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 12, 11, 10, 13 };
    int []B = { 7, 10, 6, 2 };

    int N = A.Length;
    int K = 3;

    if (checkSubsetSum(A, B, N, K))
    {
        Console.Write("YES");
    }
    else
    {
        Console.Write("NO");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check all subset-sums
// of K-length subsets in A[] is greater
// that that in the array B[] or not
function checkSubsetSum(A, B, N, K)
{
    // Sort the array in
    // ascending order
    A.sort((a,b)=> a-b);

    // Sort the array in
    // descending order
    B.sort((a,b)=>b-a);

    // Stores sum of first K
    // elements of A[]
    var sum1 = 0;

    // Stores sum of first K
    // elements of B[]
    var sum2 = 0;

    // Traverse both the arrays
    for (var i = 0; i < K; i++) {

        // Update sum1
        sum1 += A[i];

        // Update sum2
        sum2 += B[i];
    }

    // If sum1 exceeds sum2
    if (sum1 > sum2) {
        return true;
    }

    return false;
}

// Driver Code
var A = [12, 11, 10, 13];
var B = [7, 10, 6, 2];
var N = A.length;
var K = 3;
if (checkSubsetSum(A, B, N, K)) {
    document.write( "YES");
}
else {
    document.write( "NO");
}

</script>
```

**Output:** 

```
YES
```

**时间复杂度:***O(N * log(N)*
T5】辅助空间: *O(1)*