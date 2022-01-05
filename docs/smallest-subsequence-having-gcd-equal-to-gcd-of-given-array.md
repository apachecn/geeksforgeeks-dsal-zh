# 最小子序列，其 GCD 等于给定数组的 GCD

> 原文:[https://www . geesforgeks . org/最小子序列-having-gcd-等于给定数组的 gcd/](https://www.geeksforgeeks.org/smallest-subsequence-having-gcd-equal-to-gcd-of-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组的最小子序列，其子序列的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 等于给定数组 **的 [GCD。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)**如果存在多个这样的子序列，则打印其中的任何一个。

**示例:**

> **输入:** arr[] = {4，6，12}
> **输出:** 4 6
> **解释:**gcd 等于给定数组 gcd 的最小子序列(= 2)是{4，6}。因此，所需的输出是{4，6}
> 
> **输入:** arr[] = {6，12，18，24 }
> T3】输出: 6

**朴素方法:**解决这个问题最简单的方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并计算每个子序列的 GCD。打印 gcd 等于给定数组 gcd 的最小子序列。

***时间复杂度:** O(2 <sup>N</sup> * N * log X)，其中 X 是给定数组的最大元素。*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> gcd 等于给定数组 gcd 的最小子序列的长度必须是 1 或 2。
> 
> 考虑，给定数组的 gcd 为 **Y** 。
> 
> **如果 arr[idx] = Y** ，那么对于 **idx** 的某个值，最小子序列的长度必须是 **1** 。
> 
> 否则，最小子序列的长度必须为 **2** 。
> 
> 用矛盾法证明:
> 如果给定数组所有可能对的 gcd 大于 **Y** ，那么给定数组的 gcd 必须大于 **Y** ，这是不可能的。
> 因此，给定数组中至少存在一对 gcd 等于 **Y** 的数组。

按照以下步骤解决问题:

*   初始化一个变量 **gcdArr** 来存储数组的 [GCD。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查是否有任何数组元素等于 **gcdArr** 。如果发现是真的，打印该元素。
*   否则，打印给定数组中 gcd 等于 **gcdArr** 的一对。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print
// the smallest subsequence
// that satisfies the condition
void printSmallSub(int arr[], int N)
{
    // Stores gcd of the array.
    int gcdArr = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Update gcdArr
        gcdArr = __gcd(gcdArr, arr[i]);
    }

    // Traverse the given array.
    for (int i = 0; i < N; i++) {

        // If current element
        // equal to gcd of array.
        if (arr[i] == gcdArr) {
            cout << arr[i] << " ";
            return;
        }
    }

    // Generate all possible pairs.
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N;
             j++) {

            // If gcd of current pair
            // equal to gcdArr
            if (__gcd(arr[i], arr[j])
                == gcdArr) {

                // Print current pair
                // of the array
                cout << arr[i] << " " << arr[j];
                return;
            }
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 6, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    printSmallSub(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to calculate gcd
// of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to print
// the smallest subsequence
// that satisfies the condition
static void printSmallSub(int[] arr, int N)
{

    // Stores gcd of the array.
    int gcdArr = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Update gcdArr
        gcdArr = gcd(gcdArr, arr[i]);
    }

    // Traverse the given array.
    for(int i = 0; i < N; i++)
    {

        // If current element
        // equal to gcd of array.
        if (arr[i] == gcdArr)
        {
            System.out.print(arr[i] + " ");
            return;
        }
    }

    // Generate all possible pairs.
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // If gcd of current pair
            // equal to gcdArr
            if (gcd(arr[i], arr[j]) == gcdArr)
            {

                // Print current pair
                // of the array
                System.out.print(arr[i] + " " +
                                 arr[j]);
                return;
            }
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 12 };
    int N = arr.length;

    printSmallSub(arr, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to print the
# smallest subsequence
# that satisfies the condition
def printSmallSub(arr, N):

    # Stores gcd of the array.
    gcdArr = 0

    # Traverse the given array
    for i in range(0, N):

        # Update gcdArr
        gcdArr = math.gcd(gcdArr, arr[i])

    # Traverse the given array.
    for i in range(0, N):

        # If current element
        # equal to gcd of array.
        if (arr[i] == gcdArr):
            print(arr[i], end = " ")
            return

        # Generate all possible pairs.
        for i in range(0, N):
            for j in range(i + 1, N):

                # If gcd of current pair
                # equal to gcdArr
                if (math.gcd(arr[i],
                             arr[j]) == gcdArr):

                    # Print current pair
                    # of the array
                    print(arr[i], end = " ")
                    print(arr[j], end = " ")
                    return

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 6, 12 ]
    N = len(arr)

    printSmallSub(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate gcd
// of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to print the
// smallest subsequence
// that satisfies the condition
static void printSmallSub(int[] arr, int N)
{

    // Stores gcd of the array.
    int gcdArr = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Update gcdArr
        gcdArr = gcd(gcdArr, arr[i]);
    }

    // Traverse the given array.
    for(int i = 0; i < N; i++)
    {

        // If current element
        // equal to gcd of array.
        if (arr[i] == gcdArr)
        {
            Console.Write(arr[i] + " ");
            return;
        }
    }

    // Generate all possible pairs.
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // If gcd of current pair
            // equal to gcdArr
            if (gcd(arr[i], arr[j]) == gcdArr)
            {

                // Print current pair
                // of the array
                Console.Write(arr[i] + " " +
                              arr[j]);
                return;
            }
        }
    }
}

// Driver Code
public static void Main()
{

    int[] arr = { 4, 6, 12 };
    int N = arr.Length;

    printSmallSub(arr, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to calculate gcd
// of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to print
// the smallest subsequence
// that satisfies the condition
function printSmallSub(arr, N)
{
    // Stores gcd of the array.
    let gcdArr = 0;

    // Traverse the given array
    for (let i = 0; i < N; i++) {

        // Update gcdArr
        gcdArr = gcd(gcdArr, arr[i]);
    }

    // Traverse the given array.
    for (let i = 0; i < N; i++) {

        // If current element
        // equal to gcd of array.
        if (arr[i] == gcdArr) {
            document.write(arr[i] + " ");
            return;
        }
    }

    // Generate all possible pairs.
    for (let i = 0; i < N; i++) {
        for (let j = i + 1; j < N;
            j++) {

            // If gcd of current pair
            // equal to gcdArr
            if (gcd(arr[i], arr[j])
                == gcdArr) {

                // Print current pair
                // of the array
                document.write(arr[i] + " " + arr[j]);
                return;
            }
        }
    }
}

// Driver Code

    let arr = [ 4, 6, 12 ];
    let N = arr.length;

    printSmallSub(arr, N);

// This is code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
4 6
```

***时间复杂度:** (N <sup>2</sup> * log X)，其中 X 是给定数组的最大元素。*
***辅助空间:** O(1)*