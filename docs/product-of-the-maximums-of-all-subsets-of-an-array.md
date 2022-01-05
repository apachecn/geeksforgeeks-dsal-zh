# 数组所有子集的最大值的乘积

> 原文:[https://www . geeksforgeeks . org/数组所有子集的最大乘积/](https://www.geeksforgeeks.org/product-of-the-maximums-of-all-subsets-of-an-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到给定数组的所有可能子集的[最大值](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的乘积。由于产品可以很大，打印到[模 **(10 <sup>9</sup> + 7)**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:**
> **解释:**
> 给定数组的所有可能子集及其各自的最大元素是:
> 
> 1.  {1}，最大元素是 1。
> 2.  {2}，最大元素是 2。
> 3.  {3}，最大元素是 3。
> 4.  {1，2}，最大元素是 2。
> 5.  {1，3}，最大元素是 3。
> 6.  {2，3}，最大元素是 3。
> 7.  {1，2，3}，最大元素是 3。
> 
> 以上所有最大元素的乘积是 1*2*3*2*3*3*3 = 324。
> 
> **输入:** arr[] = {1，1，1，1}
> **输出:** 1

**天真法:**解决给定问题最简单的方法是[生成给定数组的所有可能子集](https://www.geeksforgeeks.org/print-subsets-given-size-set/)，求所有生成子集最大值的乘积模 **(10 <sup>9</sup> + 7)** 作为结果乘积。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   其思想是[计算每个数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)作为所有可能形成的子集中最大元素出现的次数。
*   一个数组元素 **arr[i]** 是一个最大值，当且仅当除了 **arr[i]** 之外的所有元素都小于或等于它。
*   因此，由小于或等于每个阵列元素的所有元素形成的子集的数量 **arr[i]** 有助于具有 **arr[i]** 作为最大元素的子集的计数。

按照以下步骤解决问题:

*   初始化一个变量，比如说**最大乘积**为 **1** ，它存储所有子集的最大元素的乘积。
*   按递增顺序对给定数组 **arr[]** 进行排序。
*   [使用变量 **i** 从头到尾遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   找出小于当前元素**arr【I】**的子集数作为**(2<sup>I</sup>–1)**，并将其存储在一个变量中，比如 **P** 。
    *   由于数组元素**arr【I】**贡献 **P** 次，因此将值**arr【I】**、 **P** 次乘以变量**最大产量**。
*   用**求数组元素的[乘积，最大乘积](https://www.geeksforgeeks.org/program-for-product-of-array/)**包括**大小 1** 的所有子集。
*   完成上述步骤后，打印**最大乘积**的值作为最终最大乘积。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the product of the
// maximum of all possible subsets
long maximumProduct(int arr[], int N)
{
    long mod = 1000000007;

    // Sort the given array arr[]
    sort(arr, arr + N);

    // Stores the power of 2
    long power[N + 1];
    power[0] = 1;

    // Calculate the power of 2
    for (int i = 1; i <= N; i++) {
        power[i] = 2 * power[i - 1];
        power[i] %= mod;
    }

    // Stores the resultant product
    long result = 1;

    // Traverse the array from the back
    for (int i = N - 1; i > 0; i--) {

        // Find the value of 2^i - 1
        long value = (power[i] - 1);

        // Iterate value number of times
        for (int j = 0; j < value; j++) {

            // Multiply value with
            // the result
            result *= 1LL * arr[i];
            result %= mod;
        }
    }

    // Calculate the product of array
    // elements with result to consider
    // the subset of size 1
    for (int i = 0; i < N; i++) {
        result *= 1LL * arr[i];
        result %= mod;
    }

    // Return the resultant product
    return result;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumProduct(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to find the product of the
// maximum of all possible subsets
static long maximumProduct(int arr[], int N)
{
    long mod = 1000000007;

    // Sort the given array arr[]
    Arrays.sort(arr);

    // Stores the power of 2
    long power[] = new long[N + 1];
    power[0] = 1;

    // Calculate the power of 2
    for(int i = 1; i <= N; i++)
    {
        power[i] = 2 * power[i - 1];
        power[i] %= mod;
    }

    // Stores the resultant product
    long result = 1;

    // Traverse the array from the back
    for(int i = N - 1; i > 0; i--)
    {

        // Find the value of 2^i - 1
        long value = (power[i] - 1);

        // Iterate value number of times
        for(int j = 0; j < value; j++)
        {

            // Multiply value with
            // the result
            result *= arr[i];
            result %= mod;
        }
    }

    // Calculate the product of array
    // elements with result to consider
    // the subset of size 1
    for(int i = 0; i < N; i++)
    {
        result *= arr[i];
        result %= mod;
    }

    // Return the resultant product
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int N = arr.length;

    System.out.println(maximumProduct(arr, N));
}
}

// This code is contributed by rishavmahato348
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the product of the
# maximum of all possible subsets
def maximumProduct(arr, N):

    mod = 1000000007

    # Sort the given array arr[]
    arr = sorted(arr)

    # Stores the power of 2
    power = [0] * (N + 1)
    power[0] = 1

    # Calculate the power of 2
    for i in range(1, N + 1):
        power[i] = 2 * power[i - 1]
        power[i] %= mod

    # Stores the resultant product
    result = 1

    # Traverse the array from the back
    for i in range(N - 1, -1, -1):

        # Find the value of 2^i - 1
        value = (power[i] - 1)

        # Iterate value number of times
        for j in range(value):

            # Multiply value with
            # the result
            result *= arr[i]
            result %= mod

    # Calculate the product of array
    # elements with result to consider
    # the subset of size 1
    for i in range(N):
        result *= arr[i]
        result %= mod

    # Return the resultant product
    return result

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3 ]
    N = len(arr)

    print(maximumProduct(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the product of the
// maximum of all possible subsets
static long maximumProduct(int []arr, int N)
{
    long mod = 1000000007;

    // Sort the given array arr[]
    Array.Sort(arr);

    // Stores the power of 2
    long []power = new long[N + 1];
    power[0] = 1;

    // Calculate the power of 2
    for (int i = 1; i <= N; i++) {
        power[i] = 2 * power[i - 1];
        power[i] %= mod;
    }

    // Stores the resultant product
    long result = 1;

    // Traverse the array from the back
    for (int i = N - 1; i > 0; i--) {

        // Find the value of 2^i - 1
        long value = (power[i] - 1);

        // Iterate value number of times
        for (int j = 0; j < value; j++) {

            // Multiply value with
            // the result
            result *= 1 * arr[i];
            result %= mod;
        }
    }

    // Calculate the product of array
    // elements with result to consider
    // the subset of size 1
    for (int i = 0; i < N; i++) {
        result *= 1 * arr[i];
        result %= mod;
    }

    // Return the resultant product
    return result;
}

// Driver Code
public static void Main()
{

    int []arr = {1, 2, 3};
    int N = arr.Length;
    Console.Write(maximumProduct(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the product of the
// maximum of all possible subsets
function maximumProduct(arr, N)
{
    let mod = 1000000007;

    // Sort the given array arr[]
    arr.sort((a, b) =>  a - b);

    // Stores the power of 2
    let power = new Array(N + 1);
    power[0] = 1;

    // Calculate the power of 2
    for (let i = 1; i <= N; i++) {
        power[i] = 2 * power[i - 1];
        power[i] %= mod;
    }

    // Stores the resultant product
    let result = 1;

    // Traverse the array from the back
    for (let i = N - 1; i > 0; i--) {

        // Find the value of 2^i - 1
        let value = (power[i] - 1);

        // Iterate value number of times
        for (let j = 0; j < value; j++) {

            // Multiply value with
            // the result
            result *= 1 * arr[i];
            result %= mod;
        }
    }

    // Calculate the product of array
    // elements with result to consider
    // the subset of size 1
    for (let i = 0; i < N; i++) {
        result *= 1 * arr[i];
        result %= mod;
    }

    // Return the resultant product
    return result;
}

// Driver Code

let arr = [1, 2, 3 ];
let N = arr.length;
document.write(maximumProduct(arr, N));

</script>
```

**Output:** 

```
324
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*