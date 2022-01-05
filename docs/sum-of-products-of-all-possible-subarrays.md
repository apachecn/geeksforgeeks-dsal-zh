# 所有可能的子阵列乘积之和

> 原文:[https://www . geeksforgeeks . org/所有可能子阵列的产品总和/](https://www.geeksforgeeks.org/sum-of-products-of-all-possible-subarrays/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出所有可能的子数组元素的乘积之和。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 20
> **解释:**可能的子阵有:{1}、{2}、{3}、{1，2}、{2，3}、{1，2，3}。
> 以上所有子阵的产品分别为 1、2、3、2、6、6。
> 所有乘积之和= 1 + 2 + 3 + 2 + 6 + 6 = 20。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 84
> **解释:**
> 可能的子阵有:{1}、{2}、{3}、{4}、{1，2}、{2，3}、{3，4}、{1，2，3}、{2，3，4}、{1，2，3，4}。上述所有子阵列的乘积是 1、2、3、4、2、6、12、6、24 和 24。
> 所有乘积之和= 1 + 2 + 3 + 4 + 2 + 6 + 12 + 6 + 24 + 24 = 84。

**天真法:**解决问题最简单的方法就是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)计算出每个子阵所有元素的乘积，并加到最终的和上。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是将问题观察成某种模式。假设我们有四个数字 **a** 、 **b** 、 **c** 和 **d** 。我们可以将所有可能的子阵列产品写成:

> a+b+ c+ab+BC+CD+ABC+BCD+ABCD
> =(a+ab+ABC+ABCD)+(b+BC+BCD)+(c+CD)+d
> = a *(1+<u>b+ BC+BCD</u>)+<u>(b+BC+BCD)</u>+(c+CD)+d
> 
> 现在，带下划线的表达式(b + bc + bcd)的值可以计算一次并使用两次。
> 再次，(b+ BC+BCD)+(c+CD)= b *(1+<u>c+CD</u>)+(<u>c+CD</u>
> 
> 同样，表达式(c + cd)可以使用两次。
> 后半部分同上。

按照以下步骤解决问题:

*   迭代最后一个元素，用每个元素更新重复出现的表达式，并进一步使用它。在此过程中，相应地更新结果。
*   将 **ans** 初始化为 **0** ，将存储最终总和，将 **res** 初始化为 **0** ，将跟踪前一子阵列所有元素的乘积值。
*   [从后面遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，**arr【I】**执行以下操作:
    *   用**arr【I】**和 **(1 + res)** 的乘积增加 ans。
    *   将 res 更新为 **arr[i]*(1 + res)** 。
*   完成上述步骤后，打印**和**中存储的所有子阵列的乘积之和。**T3】**

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the sum of
// products of all subarray of arr[]
void sumOfSubarrayProd(int arr[], int n)
{

    // Stores sum of all subarrays
    int ans = 0;
    int res = 0;

    // Iterate array from behind
    for(int i = n - 1; i >= 0; i--)
    {
        int incr = arr[i] * (1 + res);

        // Update the ans
        ans += incr;

        // Update the res
        res = incr;
    }

    // Print the final sum
    cout << (ans);
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 1, 2, 3 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    sumOfSubarrayProd(arr, N);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
class GFG {

    // Function that finds the sum of
    // products of all subarray of arr[]
    static void sumOfSubarrayProd(int arr[],
                                  int n)
    {
        // Stores sum of all subarrays
        int ans = 0;
        int res = 0;

        // Iterate array from behind
        for (int i = n - 1; i >= 0; i--) {
            int incr = arr[i] * (1 + res);

            // Update the ans
            ans += incr;

            // Update the res
            res = incr;
        }

        // Print the final sum
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 1, 2, 3 };

        // Size of array
        int N = arr.length;

        // Function Call
        sumOfSubarrayProd(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the sum of
# products of all subarray of arr[]
def sumOfSubarrayProd(arr, n):

    # Stores sum of all subarrays
    ans = 0
    res = 0

    # Iterate array from behind
    i = n - 1
    while(i >= 0):
        incr = arr[i] * (1 + res)

        # Update the ans
        ans += incr

        # Update the res
        res = incr
        i -= 1

    # Print the final sum
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3 ]

    # Size of array
    N = len(arr)

    # Function call
    sumOfSubarrayProd(arr, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the
// above approach
using System;

// Function that finds
// the sum of products
// of all subarray of arr[]
class solution{

static void sumOfSubarrayProd(int []arr,
                              int n)
{   
  // Stores sum of all
  // subarrays
  int ans = 0;
  int res = 0;

  // Iterate array from behind
  for(int i = n - 1; i >= 0; i--)
  {
    int incr = arr[i] * (1 + res);

    // Update the ans
    ans += incr;

    // Update the res
    res = incr;
  }

  // Print the final sum
  Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)
{   
  // Given array arr[]
  int []arr = {1, 2, 3 };

  // Size of array
  int N = arr.Length;
  // Function call
  sumOfSubarrayProd(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function that finds the sum of
    // products of all subarray of arr[]
    function sumOfSubarrayProd(arr, n)
    {
        // Stores sum of all subarrays
        let ans = 0;
        let res = 0;

        // Iterate array from behind
        for (let i = n - 1; i >= 0; i--) {
            let incr = arr[i] * (1 + res);

            // Update the ans
            ans += incr;

            // Update the res
            res = incr;
        }

        // Prlet the final sum
        document.write(ans);
    }

    // Driver Code

     // Given array arr[]
        let arr = [ 1, 2, 3 ];

        // Size of array
        let N = arr.length;

        // Function Call
        sumOfSubarrayProd(arr, N);

</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)