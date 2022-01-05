# X 的最小值，使得 arr[I]–X 上升到 brr[i]的幂的和小于或等于 K

> 原文:[https://www . geeksforgeeks . org/x 的最小值，即 x 的加总小于或等于 k/](https://www.geeksforgeeks.org/minimum-value-of-x-such-that-sum-of-arri-x-raised-to-the-power-of-brri-is-less-than-or-equal-to-k/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**和**brr【】**，任务是找到 **X** 的最小值，使得所有数组元素**(arr[I]–X，0)** 的最大值之和上升到 **brr[i]** 的幂

**示例:**

> **输入:** arr[] = {2，1，4，3，5} brr[] = { 4，3，2，3，1}，K = 12
> **输出:** 2
> **解释:**
> 把 X 的值看作 2，那么给定表达式的值是:
> =>max(2–2，0)<sup>4</sup>+max(1–2，0) <sup>3 【T13 0)<sup>3</sup>+最大值(5–2，0)<sup>1</sup>
> =>0<sup>4</sup>+0<sup>3</sup>+2<sup>2</sup>+1<sup>3</sup>+3<sup>1</sup>= 8<= K(= 12)。
> 因此，X 的合成值为 2，为最小值。</sup>
> 
> **输入:** arr[] = {2，1，4，3，5} brr[] = { 4，3，2，3，1}，K = 22
> **输出:** 1

**天真法:**解决给定问题最简单的方法是检查从 **0** 到数组的[最大元素的 **X** 的每个值，如果存在满足给定条件的 **X** 的任何值，则打印出 **X** 和](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)[的那个值脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。

***时间复杂度:** O(N*M)，其中，M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*

**高效法:**上述方法也可以通过使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到 **X** 的值来优化，如果 **X** 的某个特定值满足上述条件，那么，所有更大的值也会满足，因此，然后尝试搜索更小的值。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **检查(a[]，b[]，k，n，x):**
    *   将变量 **sum** 初始化为 **0** 以根据数组 **arr[]** 和 **brr[]。**
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并将**幂(max(arr[I]–x，0)，brr[i])** 的值加到变量**和**上。
    *   如果**和**的值小于等于 **K** ，则返回**真**。否则，返回**假**。
*   初始化变量，说**低**为 **0** ，说**高**为数组最大值。
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**低**小于**高**，执行以下步骤:
    *   将变量**中间**初始化为**低**和**高**的平均值。
    *   通过调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **检查(arr[]，brr[]，k，n，mid)** ，检查 **mid** 的值是否满足给定条件。
    *   如果[功能](https://www.geeksforgeeks.org/functions-in-c/) **检查(arr[]，brr[]，n，k，mid)** 返回**真**，则将**高**更新为**中**。否则，将**低电平**的值更新为**(中间+ 1)** 。
    *   完成上述步骤后，将**低值**作为函数的结果返回。
*   执行上述步骤后，将**低的值**打印为期望的值 **X** 作为答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exists an
// X that satisfies the given conditions
bool check(int a[], int b[], int k, int n, int x)
{
    int sum = 0;

    // Find the required value of the
    // given expression
    for (int i = 0; i < n; i++) {
        sum = sum + pow(max(a[i] - x, 0), b[i]);
    }

    if (sum <= k)
        return true;
    else
        return false;
}

// Function to find the minimum value
// of X using binary search.
int findMin(int a[], int b[], int n, int k)
{
    // Boundaries of the Binary Search
    int l = 0, u = *max_element(a, a + n);

    while (l < u) {

        // Find the middle value
        int m = (l + u) / 2;

        // Check for the middle value
        if (check(a, b, k, n, m)) {

            // Update the upper
            u = m;
        }
        else {

            // Update the lower
            l = m + 1;
        }
    }
    return l;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 4, 3, 5 };
    int brr[] = { 4, 3, 2, 3, 1 };
    int K = 12;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findMin(arr, brr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if it is possible to
// get desired result
static boolean check(int a[], int b[], int k, int x)
{
    int sum = 0;
    for(int i = 0; i < a.length; i++)
    {
        sum = sum + (int)Math.pow(
                         Math.max(a[i] - x, 0), b[i]);
    }
    if (sum <= k)
        return true;
    else
        return false;
}

// Function to find the minimum value
// of X using binary search.
static int findMin(int a[], int b[], int n, int k)
{

    // Boundaries of the Binary Search
    int l = 0, u = (int)1e9;

    while (l < u)
    {

        // Find the middle value
        int m = (l + u) / 2;

        // Check for the middle value
        if (check(a, b, k, m))

            // Update the upper
            u = m;
        else

            // Update the lower
            l = m + 1;
    }
    return l;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    int k = 12;
    int a[] = { 2, 1, 4, 3, 5 };
    int b[] = { 4, 3, 2, 3, 1 };

    System.out.println(findMin(a, b, n, k));
}
}

// This code is contributed by ayush_dragneel
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if there exists an
# X that satisfies the given conditions
def check(a, b, k, n, x):
    sum = 0

    # Find the required value of the
    # given expression
    for i in range(n):
        sum = sum + pow(max(a[i] - x, 0), b[i])

    if (sum <= k):
        return True
    else:
        return False

# Function to find the minimum value
# of X using binary search.
def findMin(a, b, n, k):
    # Boundaries of the Binary Search
    l = 0
    u = max(a)
    while (l < u):
        # Find the middle value
        m = (l + u) // 2

        # Check for the middle value
        if (check(a, b, k, n, m)):
            # Update the upper
            u = m
        else:

            # Update the lower
            l = m + 1
    return l

# Driver Code
if __name__ == '__main__':
    arr = [2, 1, 4, 3, 5]
    brr = [4, 3, 2, 3, 1]
    K = 12
    N = len(arr)
    print(findMin(arr, brr, N, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to check if it is possible to
// get desired result
static bool check(int []a, int []b, int k, int x)
{
    int sum = 0;
    for(int i = 0; i < a.Length; i++)
    {
        sum = sum + (int)Math.Pow(
                         Math.Max(a[i] - x, 0), b[i]);
    }
    if (sum <= k)
        return true;
    else
        return false;
}

// Function to find the minimum value
// of X using binary search.
static int findMin(int []a, int []b, int n, int k)
{

    // Boundaries of the Binary Search
    int l = 0, u = (int)1e9;

    while (l < u)
    {

        // Find the middle value
        int m = (l + u) / 2;

        // Check for the middle value
        if (check(a, b, k, m))

            // Update the upper
            u = m;
        else

            // Update the lower
            l = m + 1;
    }
    return l;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    int k = 12;
    int []a = { 2, 1, 4, 3, 5 };
    int []b = { 4, 3, 2, 3, 1 };

    Console.WriteLine(findMin(a, b, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

        // JavaScript program for the above approache9 + 7;

        // Function to check if there exists an
        // X that satisfies the given conditions
        function check(a, b, k, n, x) {
            let sum = 0;

            // Find the required value of the
            // given expression
            for (let i = 0; i < n; i++) {
                sum = sum + Math.pow(Math.max(a[i] - x, 0), b[i]);
            }

            if (sum <= k)
                return true;
            else
                return false;
        }
        function max_element(a) {
            let maxi = Number.MIN_VALUE;

            for (let i = 0; i < a.length; i++) {
                if (a[i] > maxi) {
                    maxi = a[i];
                }
            }
            return maxi;
        }
        // Function to find the minimum value
        // of X using binary search.
        function findMin(a, b, n, k) {
            // Boundaries of the Binary Search
            let l = 0, u = max_element(a);

            while (l < u) {

                // Find the middle value
                let m = Math.floor((l + u) / 2);

                // Check for the middle value
                if (check(a, b, k, n, m)) {

                    // Update the upper
                    u = m;
                }
                else {

                    // Update the lower
                    l = m + 1;
                }
            }
            return l;
        }

        // Driver Code
        let arr = [2, 1, 4, 3, 5];
        let brr = [4, 3, 2, 3, 1];
        let K = 12;
        let N = arr.length;
        document.write(findMin(arr, brr, N, K));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度:** O(N*log M)，其中，M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*