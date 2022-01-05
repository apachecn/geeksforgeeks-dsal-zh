# 给定维数的矩阵的第 k 个最小元素，填充了指数的乘积

> 原文:[https://www . geeksforgeeks . org/kth-给定维度矩阵的最小元素-填充有指数乘积/](https://www.geeksforgeeks.org/kth-smallest-element-of-a-matrix-of-given-dimensions-filled-with-product-of-indices/)

给定一个整数 **K** 和一个大小为 **N x M** 的矩阵，其中每个矩阵元素等于其指数的乘积( **i * j** ，任务是在给定的矩阵中找到 **K <sup>th</sup> 最小元素**。
**示例:**

> **输入:** N = 2，M = 3，K = 5
> **输出:** 4
> **解释:**
> 给定维度可能的矩阵为{{1，2，3}，{2，4，6}}
> 矩阵元素的排序顺序:{1，2，2，3，4，6}
> 因此，第 5 个<sup>最小元素为 **4** 。
> **输入:** N = 1，M = 10，K = 8
> **输出:** 8
> **解释:**
> 给定维度可能的矩阵为{{1，2，3，4，5，6，7，8，9，10}}
> 因此，第 8 个<sup>最小元素为 **8** 。</sup></sup>

**天真法:**最简单的方法是将矩阵的所有元素存储在一个数组中，然后通过对数组进行排序，找到**K<sup>th</sup>T5】最小的元素。
***时间复杂度:**O(n×M×log(n×M))*
***辅助空间:** O(N×M)*
**高效途径:**
优化幼稚途径的思路是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法。按照以下步骤解决问题:**

1.  将 ***低*** 初始化为 **1** 和 ***高*** 为 **N×M，**为 **K <sup>th</sup>** 最小元素位于 **1** 和 **N×M 之间**
2.  找到 ***中间*** 元素之间的 ***低*** 和 ***高*** 元素*。*
3.  如果元素数量*少于 ***中*** 大于*或等于**K，**则更新 ***高*** 至 ***中-1*** 为 **Kth** 最小元素位于 ***低*** 和 ***中之间***
4.  如果元素数量*少于 ***中*** 是*少于*比**K，**则更新 ***低*** 为 ***中+1*** 为 **Kth** 最小元素位于 ***中**T25】和 ***高之间。*****
5.  由于**行中的元素是 ***i*** 的倍数，因此**行中少于 ***mid*** 的元素个数可以通过 ***min(mid/i，M)轻松计算出来。*** 所以，时间复杂度找元素数量少于 ***中期*** 只能在 ***O(N)*** 中完成。****
6.  ****执行二分搜索法直到*T1【低】T3*小于或等于 ***高*** 并返回 ***高+ 1*** 作为矩阵的 **Kth** 最小元素**n×m********

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define LL long long

// Function that returns true if the
// count of elements is less than mid
bool countLessThanMid(LL mid, LL N,
                    LL M, LL K)
{
    // To store count of elements
    // less than mid
    LL count = 0;

    // Loop through each row
    for (int i = 1;
        i <= min((LL)N, mid); ++i) {

        // Count elements less than
        // mid in the ith row
        count = count + min(mid / i, M);
    }

    if (count >= K)
        return false;
    else
        return true;
}

// Function that returns the Kth
// smallest element in the NxM
// Matrix after sorting in an array
LL findKthElement(LL N, LL M, LL K)
{
    // Initialize low and high
    LL low = 1, high = N * M;

    // Perform binary search
    while (low <= high) {

        // Find the mid
        LL mid = low + (high - low) / 2;

        // Check if the count of
        // elements is less than mid
        if (countLessThanMid(mid, N, M, K))
            low = mid + 1;
        else
            high = mid - 1;
    }

    // Return Kth smallest element
    // of the matrix
    return high + 1;
}

// Driver Code
int main()
{
    LL N = 2, M = 3;

    LL int K = 5;

    cout << findKthElement(N, M, K) << endl;

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to implement
// the above approach
class GFG{

// Function that returns true if the
// count of elements is less than mid
public static boolean countLessThanMid(int mid, int N,
                                       int M, int K)
{

    // To store count of elements
    // less than mid
    int count = 0;

    // Loop through each row
    for(int i = 1;
            i <= Math.min(N, mid); ++i)
    {

        // Count elements less than
        // mid in the ith row
        count = count + Math.min(mid / i, M);
    }

    if (count >= K)
        return false;
    else
        return true;
}

// Function that returns the Kth
// smallest element in the NxM
// Matrix after sorting in an array
public static int findKthElement(int N, int M, int K)
{

    // Initialize low and high
    int low = 1, high = N * M;

    // Perform binary search
    while (low <= high)
    {

        // Find the mid
        int mid = low + (high - low) / 2;

        // Check if the count of
        // elements is less than mid
        if (countLessThanMid(mid, N, M, K))
            low = mid + 1;
        else
            high = mid - 1;
    }

    // Return Kth smallest element
    // of the matrix
    return high + 1;
}

// Driver code
public static void main(String[] args)
{
    int N = 2, M = 3;
    int K = 5;

    System.out.println(findKthElement(N, M, K));
}
}

// This code is contributed by divyeshrabadiya07**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach
# Function that returns true if the
# count of elements is less than mid
def countLessThanMid(mid, N, M, K):

    # To store count of elements
    # less than mid
    count = 0

    # Loop through each row
    for i in range (1, min(N, mid) + 1):

        # Count elements less than
        # mid in the ith row
        count = count + min(mid // i, M)

    if (count >= K):
        return False
    else:
        return True

# Function that returns the Kth
# smallest element in the NxM
# Matrix after sorting in an array
def findKthElement(N, M, K):

    # Initialize low and high
    low = 1
    high = N * M

    # Perform binary search
    while (low <= high):

        # Find the mid
        mid = low + (high - low) // 2

        # Check if the count of
        # elements is less than mid
        if (countLessThanMid(mid, N, M, K)):
            low = mid + 1
        else:
            high = mid - 1

    # Return Kth smallest element
    # of the matrix
    return high + 1

# Driver Code
if __name__ == "__main__": 
    N = 2
    M = 3
    K = 5
    print(findKthElement(N, M, K))

# This code is contributed by Chitranayal**
```

## ****C#****

```
**// C# program to implement
// the above approach
using System;

class GFG{

// Function that returns true if the
// count of elements is less than mid
public static bool countLessThanMid(int mid, int N,
                                    int M, int K)
{

    // To store count of elements
    // less than mid
    int count = 0;

    // Loop through each row
    for(int i = 1;
            i <= Math.Min(N, mid); ++i)
    {

        // Count elements less than
        // mid in the ith row
        count = count + Math.Min(mid / i, M);
    }

    if (count >= K)
        return false;
    else
        return true;
}

// Function that returns the Kth
// smallest element in the NxM
// Matrix after sorting in an array
public static int findKthElement(int N, int M,
                                        int K)
{

    // Initialize low and high
    int low = 1, high = N * M;

    // Perform binary search
    while (low <= high)
    {

        // Find the mid
        int mid = low + (high - low) / 2;

        // Check if the count of
        // elements is less than mid
        if (countLessThanMid(mid, N, M, K))
            low = mid + 1;
        else
            high = mid - 1;
    }

    // Return Kth smallest element
    // of the matrix
    return high + 1;
}

// Driver code
public static void Main(String[] args)
{
    int N = 2, M = 3;
    int K = 5;

    Console.WriteLine(findKthElement(N, M, K));
}
}

// This code is contributed by Rajput-Ji**
```

## ****java 描述语言****

```
**<script>
// Javascript program for the above approach

// Function that returns true if the
// count of elements is less than mid
function countLessThanMid(mid, N, M, K)
{
    // To store count of elements
    // less than mid
    let count = 0;

    // Loop through each row
    for (let i = 1;
        i <= Math.min(N, mid); ++i) {

        // Count elements less than
        // mid in the ith row
        count = count + Math.min(parseInt(mid / i), M);
    }

    if (count >= K)
        return false;
    else
        return true;
}

// Function that returns the Kth
// smallest element in the NxM
// Matrix after sorting in an array
function findKthElement(N, M, K)
{
    // Initialize low and high
    let low = 1, high = N * M;

    // Perform binary search
    while (low <= high) {

        // Find the mid
        let mid = low + parseInt((high - low) / 2);

        // Check if the count of
        // elements is less than mid
        if (countLessThanMid(mid, N, M, K))
            low = mid + 1;
        else
            high = mid - 1;
    }

    // Return Kth smallest element
    // of the matrix
    return high + 1;
}

// Driver Code
    let N = 2, M = 3;

    let K = 5;

    document.write(findKthElement(N, M, K));

</script>**
```

******输出:******

```
**4**
```

*******时间复杂度:**O(n×log(n×M))*
***辅助空间:** O(1)*****