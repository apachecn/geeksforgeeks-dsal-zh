# 重新排列给定的数组，以在正好 X 个索引处获得正前缀和

> 原文:[https://www . geeksforgeeks . org/重排-给定-数组-获取-正前缀-x-indexs-sums/](https://www.geeksforgeeks.org/rearrange-given-array-to-obtain-positive-prefix-sums-at-exactly-x-indices/)

给定一个由绝对值不同的 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是通过以下操作找到给定数组的这种排列，使得它恰好在 **K** 处具有正前缀和:

*   选择两个整数 **i** 、 **j** ，并在索引 **i** 和 **j** 处交换元素的值，其中 **0 ≤ i，j < N** 和 **i ≠ j** 。
*   选择一个指数 **i** 并更改其符号，即在 **0 ≤ i < N** 的情况下，将正数更改为负数，反之亦然。

**示例:**

> ***输入:** arr* [] = {1，-2，4，5，-3}，K = 3
> **输出:** {-1，2，-4，3，5}
> **说明:**
> 给定数组的前缀和为{-1，1，-3，0，5}。
> 因此，正好 3 个指标的前缀和为正。
> 
> **输入:** arr[] = {1，4，3，2}，K = 2
> **输出:** {1，-4，2，3}
> **解释:**
> 给定数组的前缀和为 1，-3，-1，2}。
> 因此，正好有 2 个指数的前缀和为正。

**方法:**给定的问题可以通过观察只使用第一类操作就可以得到排序的数组来解决。人们可以用第二种运算把每个元素变成正元素。按照以下步骤解决问题:

*   使用第二次运算使数组的所有值都为正，即把所有负数的符号翻转为正。
*   [将数组 arr[]按照升序](https://www.geeksforgeeks.org/sort-c-stl/)排序，并将 **K** 设置为**(N–K)**。
*   如果给定数组**arr【】**中的 **K** 和[计数 0 之和大于 **N** ，则不可能有任何这种可能的排列。遂印 **"-1"** 。否则执行以下操作。](https://www.geeksforgeeks.org/find-number-zeroes/)
*   [在范围**【0，N–1】**内遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并遵循以下步骤:
    *   通过 **2 <sup>和</sup>操作**将**I<sup>th</sup>T3【元素变为负值。**
    *   将 **i** 增加 **2** ，将 **K** 减少 **1** 。
    *   如果 **K** 等于 **0** ，则断开。
*   检查 **K** 是否仍然大于 **0** ，然后从最后一个开始遍历数组，直到 **K** 大于 **0** ，将每一个正元素变为负元素，以 **1** 递减 **K** 。
*   完成上述步骤后，[按要求排列打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array
// according to the given condition
void rearrange(int* a, int n, int x)
{
    // Using 2nd operation making
    // all values positive
    for (int i = 0; i < n; i++)
        a[i] = abs(a[i]);

    // Sort the array
    sort(a, a + n);

    // Assign K = N - K
    x = n - x;

    // Count number of zeros
    int z = count(a, a + n, 0);

    // If number of zeros if greater
    if (x > n - z) {
        cout << "-1\n";
        return;
    }

    for (int i = 0; i < n && x > 0;
         i += 2) {

        // Using 2nd operation convert
        // it into one negative
        a[i] = -a[i];
        x--;
    }

    for (int i = n - 1; i >= 0
                        && x > 0;
         i--) {

        // Using 2nd operation convert
        // it into one negative
        if (a[i] > 0) {
            a[i] = -a[i];
            x--;
        }
    }

    // Print the array
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 0, -2, 4, 5, -3 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    rearrange(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int count(int[] a)
{
    int counter = 0;

    for(int i = 0; i < a.length; i++)
    {
        if (a[i] == 0)
        {
            counter++;
        }
    }
    return counter;
}

// Function to rearrange the array
// according to the given condition
static void rearrange(int[] a, int n, int x)
{

    // Using 2nd operation making
    // all values positive
    for(int i = 0; i < n; i++)
        a[i] = Math.abs(a[i]);

    // Sort the array
    Arrays.sort(a);

    // Assign K = N - K
    x = n - x;

    // Count number of zeros
    int z = count(a);

    // If number of zeros if greater
    if (x > n - z)
    {
        System.out.println("-1");
        return;
    }

    for(int i = 0; i < n && x > 0; i += 2)
    {

        // Using 2nd operation convert
        // it into one negative
        a[i] = -a[i];
        x--;
    }

    for(int i = n - 1; i >= 0 && x > 0; i--)
    {

        // Using 2nd operation convert
        // it into one negative
        if (a[i] > 0)
        {
            a[i] = -a[i];
            x--;
        }
    }

    // Print the array
    for(int i = 0; i < n; i++)
    {
        System.out.print(a[i] + " ");
    }
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 0, -2, 4, 5, -3 };
    int K = 3;
    int N = arr.length;

    // Function Call
    rearrange(arr, N, K);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rearrange the array
# according to the given condition
def rearrange(a, n, x):

    # Using 2nd operation making
    # all values positive
    for i in range(n):
        a[i] = abs(a[i])

    # Sort the array
    a = sorted(a)

    # Assign K = N - K
    x = n - x;

    # Count number of zeros
    z = a.count(0)

    # If number of zeros if greater
    if (x > n - z):
        print("-1")
        return
    for i in range(0, n, 2):
        if x <= 0:
            break

        # Using 2nd operation convert
        # it into one negative
        a[i] = -a[i]
        x -= 1
    for i in range(n - 1, -1, -1):
        if x <= 0:
            break

        # Using 2nd operation convert
        # it into one negative
        if (a[i] > 0):
            a[i] = -a[i]
            x -= 1

    # Print array
    for i in range(n):
        print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [0, -2, 4, 5, -3]
    K = 3
    N = len(arr)

    # Function Call
    rearrange(arr, N, K)

    # This code is co tributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int count(int[] a)
{
    int counter = 0;

    for(int i = 0; i < a.Length; i++)
    {
        if (a[i] == 0)
        {
            counter++;
        }
    }
    return counter;
}

// Function to rearrange the array
// according to the given condition
static void rearrange(int[] a, int n, int x)
{

    // Using 2nd operation making
    // all values positive
    for(int i = 0; i < n; i++)
        a[i] = Math.Abs(a[i]);

    // Sort the array
    Array.Sort(a);

    // Assign K = N - K
    x = n - x;

    // Count number of zeros
    int z = count(a);

    // If number of zeros if greater
    if (x > n - z)
    {
        Console.WriteLine("-1");
        return;
    }

    for(int i = 0; i < n && x > 0; i += 2)
    {

        // Using 2nd operation convert
        // it into one negative
        a[i] = -a[i];
        x--;
    }

    for(int i = n - 1; i >= 0 && x > 0; i--)
    {

        // Using 2nd operation convert
        // it into one negative
        if (a[i] > 0)
        {
            a[i] = -a[i];
            x--;
        }
    }

    // Print the array
    for(int i = 0; i < n; i++)
    {
        Console.Write(a[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 0, -2, 4, 5, -3 };
    int K = 3;
    int N = arr.Length;

    // Function Call
    rearrange(arr, N, K);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    function count(a)
    {
    let counter = 0;

    for(let i = 0; i < a.length; i++)
    {
        if (a[i] == 0)
        {
            counter++;
        }
    }
    return counter;
}

// Function to rearrange the array
// according to the given condition
function rearrange(a, n, x)
{

    // Using 2nd operation making
    // all values positive
    for(let i = 0; i < n; i++)
        a[i] = Math.abs(a[i]);

    // Sort the array
    a.sort();

    // Assign K = N - K
    x = n - x;

    // Count number of zeros
    let z = count(a);

    // If number of zeros if greater
    if (x > n - z)
    {
        document.write("-1");
        return;
    }

    for(let i = 0; i < n && x > 0; i += 2)
    {

        // Using 2nd operation convert
        // it into one negative
        a[i] = -a[i];
        x--;
    }

    for(let i = n - 1; i >= 0 && x > 0; i--)
    {

        // Using 2nd operation convert
        // it into one negative
        if (a[i] > 0)
        {
            a[i] = -a[i];
            x--;
        }
    }

    // Print the array
    for(let i = 0; i < n; i++)
    {
        document.write(a[i] + " ");
    }
}

// driver function

    let arr = [ 0, -2, 4, 5, -3 ];
    let K = 3;
    let N = arr.length;

    // Function Call
    rearrange(arr, N, K);

    // This code is contributed by souravghosh0416.
</script>   
```

**Output:** 

```
0 2 -3 4 5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*