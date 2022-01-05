# 计数给定数组中某个范围的索引[L，R]中存在的 1

> 原文:[https://www . geeksforgeeks . org/count-1s-在给定数组中存在一系列索引-l-r-/](https://www.geeksforgeeks.org/count-1s-present-in-a-range-of-indices-l-r-in-a-given-array/)

给定一个由单个元素**N**(*1≤N≤10<sup>6</sup>*)和两个整数 **L** 和 **R** 、( *1 ≤ L ≤ R ≤ 10 <sup>5</sup>* )组成的[阵列 **arr【】】,任务是使所有阵列元素成为 **0** 或 **1****](https://www.geeksforgeeks.org/array-data-structure/)

*   从阵列**arr【】**中选择一个元素 **P** 使得 **P > 1** 。
*   将 **P** 替换为同一位置的三个元素，依次为**楼层(P/2)、P%2、楼层(P/2** )。因此，每次操作后阵列**arr【】**的大小增加 **2** 。

执行完所有操作后，在数组**arr【】**中打印指数【total，R】范围内 **1** s 的总数的计数。
***注:**保证 **R** 不大于最终数组 **Arr** 的长度。*

**示例:**

> ***输入:** N = 7，L = 2，R = 5*
> ***输出:** 4*
> ***解释:***
> **第一步:**arr[]=【7】。选择 7 会将 arr[]修改为{3，1，3}。
> **第二步:** arr[] = [3，1，3]。选择 3 会将 arr[]修改为{1，1，1，1，3}。
> **第三步:** arr[] = [1，1，1，1，3]。选择 3 将 arr[]修改为{1，1，1，1，1，1}
> 因此，范围[2，5]中的所有索引都用 1 填充。因此，计数为 4。
> 
> **输入:** N = 7，L = 2，R = 2
> *T4】输出: 1*

**方法:**按照以下步骤使用[递归](https://www.geeksforgeeks.org/recursion/)解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   当给定数组最初只包含一个元素时，声明一个函数 **FindSize(N)** 来查找修改后数组的大小，即 **N.**
*   声明一个函数 **CountOnes(N)** 递归计算 **CountOnes(N / 2)** 、 **N % 2** 和 **CountOnes(N / 2)** 。

下面是给定方法的实现:

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the size of the
// array if the array initially
// contains a single element
int findSize(int N)
{
    // Base case
    if (N == 0)
        return 1;
    if (N == 1)
        return 1;

    int Size = 2 * findSize(N / 2) + 1;

    // P / 2 -> findSize(N / 2)
    // P % 2 -> 1
    // P / 2 -> findSize(N / 2)
    return Size;
}

// Function to return the count
// of 1s in the range [L, R]
int CountOnes(int N, int L, int R)
{
    if (L > R) {
        return 0;
    }

    // Base Case
    if (N <= 1) {

        return N;
    }

    int ret = 0;
    int M = N / 2;
    int Siz_M = findSize(M);

    // PART 1 -> N / 2
    // [1, Siz_M]
    if (L <= Siz_M) {

        // Update the right end point
        // of the range to min(Siz_M, R)
        ret += CountOnes(
            N / 2, L, min(Siz_M, R));
    }

    // PART 2 -> N % 2
    // [SizM + 1, Siz_M + 1]
    if (L <= Siz_M + 1 && Siz_M + 1 <= R) {
        ret += N % 2;
    }

    // PART 3 -> N / 2
    // [SizM + 2, 2 * Siz_M - 1]
    // Same as PART 1
    // Property of Symmetricity
    // Shift the coordinates according to PART 1
    // Subtract (Siz_M + 1) from both L, R

    if (Siz_M + 1 < R) {
        ret += CountOnes(N / 2,
                         max(1, L - Siz_M - 1),
                         R - Siz_M - 1);
    }

    return ret;
}

// Driver Code
int main()
{
    // Input
    int N = 7, L = 2, R = 5;

    // Counts the number of 1's in
    // the range [L, R]
    cout << CountOnes(N, L, R) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find the size of the
// array if the array initially
// contains a single element
static int findSize(int N)
{

    // Base case
    if (N == 0)
        return 1;
    if (N == 1)
        return 1;
    int Size = 2 * findSize(N / 2) + 1;

    // P / 2 -> findSize(N / 2)
    // P % 2 -> 1
    // P / 2 -> findSize(N / 2)
    return Size;
}

// Function to return the count
// of 1s in the range [L, R]
static int CountOnes(int N, int L, int R)
{
    if (L > R)
    {
        return 0;
    }

    // Base Case
    if (N <= 1)
    {
        return N;
    }  
    int ret = 0;
    int M = N / 2;
    int Siz_M = findSize(M);

    // PART 1 -> N / 2
    // [1, Siz_M]
    if (L <= Siz_M)
    {

        // Update the right end point
        // of the range to min(Siz_M, R)
        ret += CountOnes(N / 2, L,
                         Math.min(Siz_M, R));
    }

    // PART 2 -> N % 2
    // [SizM + 1, Siz_M + 1]
    if (L <= Siz_M + 1 && Siz_M + 1 <= R)
    {
        ret += N % 2;
    }

    // PART 3 -> N / 2
    // [SizM + 2, 2 * Siz_M - 1]
    // Same as PART 1
    // Property of Symmetricity
    // Shift the coordinates according to PART 1
    // Subtract (Siz_M + 1) from both L, R
    if (Siz_M + 1 < R)
    {
        ret += CountOnes(N / 2,
                         Math.max(1, L - Siz_M - 1),
                         R - Siz_M - 1);
    }
    return ret;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 7, L = 2, R = 5;

    // Counts the number of 1's in
    // the range [L, R]
    System.out.println(CountOnes(N, L, R));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the size of the
# array if the array initially
# contains a single element
def findSize(N):

    # Base case
    if (N == 0):
        return 1
    if (N == 1):
        return 1

    Size = 2 * findSize(N // 2) + 1

    # P / 2 -> findSize(N // 2)
    # P % 2 -> 1
    # P / 2 -> findSize(N / 2)
    return Size

# Function to return the count
# of 1s in the range [L, R]
def CountOnes(N, L, R):

    if (L > R):
        return 0

    # Base Case
    if (N <= 1):
        return N

    ret = 0
    M = N // 2
    Siz_M = findSize(M)

    # PART 1 -> N / 2
    # [1, Siz_M]
    if (L <= Siz_M):

        # Update the right end point
        # of the range to min(Siz_M, R)
        ret += CountOnes(
            N // 2, L, min(Siz_M, R))

    # PART 2 -> N % 2
    # [SizM + 1, Siz_M + 1]
    if (L <= Siz_M + 1 and Siz_M + 1 <= R):
        ret += N % 2

    # PART 3 -> N / 2
    # [SizM + 2, 2 * Siz_M - 1]
    # Same as PART 1
    # Property of Symmetricity
    # Shift the coordinates according to PART 1
    # Subtract (Siz_M + 1) from both L, R

    if (Siz_M + 1 < R):
        ret += CountOnes(N // 2,
                         max(1, L - Siz_M - 1),
                         R - Siz_M - 1)

    return ret

# Driver Code
if __name__ == "__main__":

    # Input
    N = 7
    L = 2
    R = 5

    # Counts the number of 1's in
    # the range [L, R]
    print(CountOnes(N, L, R))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the size of the
// array if the array initially
// contains a single element
static int findSize(int N)
{

    // Base case
    if (N == 0)
        return 1;
    if (N == 1)
        return 1;

    int Size = 2 * findSize(N / 2) + 1;

    // P / 2 -> findSize(N / 2)
    // P % 2 -> 1
    // P / 2 -> findSize(N / 2)
    return Size;
}

// Function to return the count
// of 1s in the range [L, R]
static int CountOnes(int N, int L, int R)
{
    if (L > R)
    {
        return 0;
    }

    // Base Case
    if (N <= 1)
    {
        return N;
    }

    int ret = 0;
    int M = N / 2;
    int Siz_M = findSize(M);

    // PART 1 -> N / 2
    // [1, Siz_M]
    if (L <= Siz_M)
    {

        // Update the right end point
        // of the range to min(Siz_M, R)
        ret += CountOnes(N / 2, L,
                         Math.Min(Siz_M, R));
    }

    // PART 2 -> N % 2
    // [SizM + 1, Siz_M + 1]
    if (L <= Siz_M + 1 && Siz_M + 1 <= R)
    {
        ret += N % 2;
    }

    // PART 3 -> N / 2
    // [SizM + 2, 2 * Siz_M - 1]
    // Same as PART 1
    // Property of Symmetricity
    // Shift the coordinates according to PART 1
    // Subtract (Siz_M + 1) from both L, R
    if (Siz_M + 1 < R)
    {
        ret += CountOnes(N / 2,
                         Math.Max(1, L - Siz_M - 1),
                         R - Siz_M - 1);
    }
    return ret;
}

// Driver code
static void Main()
{

    // Input
    int N = 7, L = 2, R = 5;

    // Counts the number of 1's in
    // the range [L, R]
    Console.WriteLine(CountOnes(N, L, R));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to find the size of the
    // array if the array initially
    // contains a single element
    function findSize(N)
    {

        // Base case
        if (N == 0)
            return 1;
        if (N == 1)
            return 1;

        let Size = 2 *
                   findSize(parseInt(N / 2, 10)) + 1;

        // P / 2 -> findSize(N / 2)
        // P % 2 -> 1
        // P / 2 -> findSize(N / 2)
        return Size;
    }

    // Function to return the count
    // of 1s in the range [L, R]
    function CountOnes(N, L, R)
    {
        if (L > R)
        {
            return 0;
        }

        // Base Case
        if (N <= 1)
        {
            return N;
        }

        let ret = 0;
        let M = parseInt(N / 2, 10);
        let Siz_M = findSize(M);

        // PART 1 -> N / 2
        // [1, Siz_M]
        if (L <= Siz_M)
        {

            // Update the right end point
            // of the range to min(Siz_M, R)
            ret += CountOnes(parseInt(N / 2, 10), L,
            Math.min(Siz_M, R));
        }

        // PART 2 -> N % 2
        // [SizM + 1, Siz_M + 1]
        if (L <= Siz_M + 1 && Siz_M + 1 <= R)
        {
            ret += N % 2;
        }

        // PART 3 -> N / 2
        // [SizM + 2, 2 * Siz_M - 1]
        // Same as PART 1
        // Property of Symmetricity
        // Shift the coordinates according to PART 1
        // Subtract (Siz_M + 1) from both L, R
        if (Siz_M + 1 < R)
        {
            ret += CountOnes(parseInt(N / 2, 10),
            Math.max(1, L - Siz_M - 1), R - Siz_M - 1);
        }
        return ret;
    }

    // Input
    let N = 7, L = 2, R = 5;

    // Counts the number of 1's in
    // the range [L, R]
    document.write(CountOnes(N, L, R));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)(利用大师定理，T(N)= 2 * T(N/2)+1 =>T(N)= O(N))*
***辅助空间:** O(N)*