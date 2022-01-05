# 绝对差之和最小的数组元素|集合 2

> 原文:[https://www . geesforgeks . org/array-element-with-minimum-sum-of-differences-set-2/](https://www.geeksforgeeks.org/array-element-with-minimum-sum-of-absolute-differences-set-2/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到一个数组元素 **X** ，使得它与每个数组元素的绝对差之和最小。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 3
> **解释:**
> 
> 1.  **对于元素 arr[0](= 1):**|(1–1)|+|(2–1)|+|(3–1)|+|(4–1)|+|(5–1)| = 0+1+2+3+4 = 10。
> 2.  **对于元素 arr[1](= 2):**|(1–2)|+|(2–2)|+|(3–2)|+|(4–2)|+|(5–2)| = 1+0+1+2+3 = 7。
> 3.  **对于元素 arr[2](= 3):**|(1–3)|+|(2–3)|+|(3–3)|+|(4–3)|+|(5–3)| = 2+1+0+1+2 = 6。
> 4.  **对于元素 arr[3](= 4):**|(1–4)|+|(2–4)|+|(3–4)|+|(4–4)|+|(5–4)| = 3+2+1+0+1 = 7。
> 5.  **对于元素 arr[4](= 5):**|(1–5)|+|(2–5)|+|(3–5)|+|(4–5)|+|(5–5)| = 4+3+2+1+0 = 10。
> 
> 因此，与所有数组元素具有最小绝对差和的元素是 3。
> 
> **输入:** arr[] = {15，12，13，10 }
> T3】输出: 12

**天真法:**解决给定问题最简单的方法是逐个求数组元素与数组中每个元素的绝对差之和，打印出差之和较小的那个元素。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**基于中位数的方法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/array-element-with-minimum-sum-of-absolute-differences/)使用中位数寻找技术来解决这个问题。
***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过最小化每个数组元素 **X** 的所有数组元素**–X * N)**之和 **(** [**的值并找到结果元素 **X** 来优化。按照以下步骤解决问题:**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   初始化一个变量，比如说 **res** 为**arr【0】**，它存储结果数组元素，数组元素与 **res** 的绝对差之和最小。
*   [求数组元素的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)存储在变量中，比如**和**。
*   初始化一个变量，说 **minDiff** 作为**和**的值。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果**(sum –( arr[I]* N))**的绝对值小于 **minDiff** ，则将 **minDiff** 更新为该值并将 **res** 作为当前数组元素，即 **arr[i]** 。
*   完成上述步骤后，打印 **res** 的值作为结果数组元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the element with
// minimum sum of differences between
// any elements in the array
int minimumDiff(int arr[], int N)
{
    // Stores the required X and
    // sum of absolute differences
    int res = arr[0], sum = 0;

    // Calculate sum of array elements
    for (int i = 0; i < N; i++)
        sum += arr[i];

    // The sum of absolute differences
    // can't be greater than sum
    int min_diff = sum;

    // Update res that gives
    // the minimum sum
    for (int i = 0; i < N; i++) {

        // If the current difference
        // is less than the previous
        // difference
        if (abs(sum - (arr[i] * N))
            < min_diff) {

            // Update min_diff and res
            min_diff = abs(sum - (arr[i] * N));
            res = arr[i];
        }
    }

    // Print the resultant value
    cout << res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    minimumDiff(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the element with
// minimum sum of differences between
// any elements in the array
static void minimumDiff(int[] arr, int N)
{

    // Stores the required X and
    // sum of absolute differences
    int res = arr[0], sum = 0;

    // Calculate sum of array elements
    for(int i = 0; i < N; i++)
        sum += arr[i];

    // The sum of absolute differences
    // can't be greater than sum
    int min_diff = sum;

    // Update res that gives
    // the minimum sum
    for(int i = 0; i < N; i++)
    {

        // If the current difference
        // is less than the previous
        // difference
        if (Math.abs(sum - (arr[i] * N)) < min_diff)
        {

            // Update min_diff and res
            min_diff = Math.abs(sum - (arr[i] * N));
            res = arr[i];
        }
    }

    // Print the resultant value
    System.out.println(res);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    minimumDiff(arr, N);
}
}

// This code is contributed by subham348
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the element with
// minimum sum of differences between
// any elements in the array
static void minimumDiff(int[] arr, int N)
{

    // Stores the required X and
    // sum of absolute differences
    int res = arr[0], sum = 0;

    // Calculate sum of array elements
    for(int i = 0; i < N; i++)
        sum += arr[i];

    // The sum of absolute differences
    // can't be greater than sum
    int min_diff = sum;

    // Update res that gives
    // the minimum sum
    for(int i = 0; i < N; i++)
    {

        // If the current difference
        // is less than the previous
        // difference
        if (Math.Abs(sum - (arr[i] * N)) < min_diff)
        {

            // Update min_diff and res
            min_diff = Math.Abs(sum - (arr[i] * N));
            res = arr[i];
        }
    }

    // Print the resultant value
    Console.Write(res);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    minimumDiff(arr, N);
}
}

// This code is contributed by subham348
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find the element with
# minimum sum of differences between
# any elements in the array
def minimumDiff(arr, N):

    # Stores the required X and
    # sum of absolute differences
    res = arr[0]
    sum1 = 0

    # Calculate sum of array elements
    for i in range(N):
        sum1 += arr[i]

    # The sum of absolute differences
    # can't be greater than sum
    min_diff = sum1

    # Update res that gives
    # the minimum sum
    for i in range(N):

        # If the current difference
        # is less than the previous
        # difference
        if (abs(sum1 - (arr[i] * N)) < min_diff):

            # Update min_diff and res
            min_diff = abs(sum1 - (arr[i] * N))
            res = arr[i]

    # Print the resultant value
    print(res)

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5]
    N = len(arr)
    minimumDiff(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the element with
// minimum sum of differences between
// any elements in the array
function minimumDiff(arr, N)
{
    // Stores the required X and
    // sum of absolute differences
    let res = arr[0], sum = 0;

    // Calculate sum of array elements
    for (let i = 0; i < N; i++)
        sum += arr[i];

    // The sum of absolute differences
    // can't be greater than sum
    let min_diff = sum;

    // Update res that gives
    // the minimum sum
    for (let i = 0; i < N; i++) {

        // If the current difference
        // is less than the previous
        // difference
        if (Math.abs(sum - (arr[i] * N))
            < min_diff) {

            // Update min_diff and res
            min_diff = Math.abs(sum - (arr[i] * N));
            res = arr[i];
        }
    }

    // Print the resultant value
    document.write(res);
}

// Driver Code
    let arr = [ 1, 2, 3, 4, 5 ];
    let N = arr.length;
    minimumDiff(arr, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)