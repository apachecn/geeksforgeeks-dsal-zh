# 一个数组中第 k 个最小的元素，它包含的 A[i]正好是 B[i]倍

> 原文:[https://www . geeksforgeeks . org/kth-包含-ai-精确-双次的数组中最小元素/](https://www.geeksforgeeks.org/kth-smallest-element-in-an-array-that-contains-ai-exactly-bi-times/)

给定由 **N** 正整数和一个整数 **K** 组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是从[数组](https://www.geeksforgeeks.org/array-data-structure/)A【】中取**I<sup>th</sup>T19】元素形成的[数组](https://www.geeksforgeeks.org/array-data-structure/)中找到**K<sup>th</sup>T13】最小元素如果不存在这样的元素，则打印 **-1** 。****

**示例:**

> **输入:** K = 4，A[] = {1，2，3}，B[] = {1，2，3}
> **输出:** 3
> **说明:**
> 取 A[0]，B[0] (= 1)次，A[1]，B[1] (= 2)次，A[2]，B[2]( = 3)次得到的数组为{1，2，2，3，3，3}。因此，数组的第 4 个<sup>元素是 3。</sup>
> 
> **输入:** K = 4，A[] = {3，4，5}，B[] = {2，1，3}
> **输出:** 3
> **说明:**形成的数组为{3，3，4，5，5，5}。因此，阵列的第 4 个<sup>元素，即 5。</sup>

**天真法:**最简单的方法是[迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**并将数组 **i <sup>th</sup>** 索引处的元素，**B【I】**次推入新数组。最后[对数组进行升序排序后，打印得到的数组的 **K <sup>第</sup>** 个元素。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)

***时间复杂度:** O(N*log(N))，其中 **N** 为新数组中的元素个数。*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过使用[频率阵列](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)来保持每个元素的计数来优化。按照以下步骤解决问题:

*   [找到数组的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **A[]** 存储在变量中，比如 **M** 。
*   初始化一个数组，用{ **0** }表示 **M + 1** 大小的 **freq[]** ，存储每个元素的频率。
*   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   在**频率【A[i]】中增加 **B[i]** 。**
*   初始化一个变量，说**将**求和为 **0，**将[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)存储到一个特定的索引。
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，比如 **i** :
    *   在**总和中加上**频率【I】**。**
    *   如果**之和**大于或等于 **K** ，则返回 **i.**
*   最后，返回 **-1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Kth smallest element
// that contains A[i] exactly B[i] times
int KthSmallest(int A[], int B[], int N, int K)
{

    int M = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        M = max(A[i], M);
    }

    // Stores the frequency
    // of every elements
    int freq[M + 1] = { 0 };

    // Traverse the given array
    for (int i = 0; i < N; i++) {
        freq[A[i]] += B[i];
    }

    // Initialize a variable to
    // store the prefix sums
    int sum = 0;

    // Iterate over the range [0, M]
    for (int i = 0; i <= M; i++) {

        // Increment sum by freq[i]
        sum += freq[i];

        // If sum is greater
        // than or equal to K
        if (sum >= K) {

            // Return the current
            // element as answer
            return i;
        }
    }
    // Return -1
    return -1;
}

// Driver Code
int main()
{

    // Given Input
    int A[] = { 3, 4, 5 };
    int B[] = { 2, 1, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 4;

    // Function call
    cout << KthSmallest(A, B, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG_JAVA {

    // Function to find the Kth smallest element
    // that contains A[i] exactly B[i] times
    static int KthSmallest(int A[], int B[], int N, int K)
    {

        int M = 0;

        // Traverse the given array
        for (int i = 0; i < N; i++) {

            M = Math.max(A[i], M);
        }

        // Stores the frequency
        // of every elements
        int freq[] = new int[M + 1];

        // Traverse the given array
        for (int i = 0; i < N; i++) {
            freq[A[i]] += B[i];
        }

        // Initialize a variable to
        // store the prefix sums
        int sum = 0;

        // Iterate over the range [0, M]
        for (int i = 0; i <= M; i++) {

            // Increment sum by freq[i]
            sum += freq[i];

            // If sum is greater
            // than or equal to K
            if (sum >= K) {

                // Return the current
                // element as answer
                return i;
            }
        }
        // Return -1
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    { // Given Input
        int A[] = { 3, 4, 5 };
        int B[] = { 2, 1, 3 };
        int N = A.length;
        int K = 4;

        // Function call
        System.out.println(KthSmallest(A, B, N, K));
    }
}
// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Kth smallest element
# that contains A[i] exactly B[i] times
def KthSmallest(A, B, N, K):

    M = 0

    # Traverse the given array
    for i in range(N):
        M = max(A[i], M)

    # Stores the frequency
    # of every elements
    freq = [0] * (M + 1)

    # Traverse the given array
    for i in range(N):
        freq[A[i]] += B[i]

    # Initialize a variable to
    # store the prefix sums
    sum = 0

    # Iterate over the range [0, M]
    for i in range(M + 1):

        # Increment sum by freq[i]
        sum += freq[i]

        # If sum is greater
        # than or equal to K
        if (sum >= K):

            # Return the current
            # element as answer
            return i

    # Return -1
    return -1

# Driver Code
if __name__ == "__main__" :

    # Given Input
    A = [ 3, 4, 5 ]
    B = [ 2, 1, 3 ]
    N = len(A)
    K = 4

    # Function call
    print(KthSmallest(A, B, N, K))

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the Kth smallest element
// that contains A[i] exactly B[i] times
static int KthSmallest(int []A, int []B,
                       int N, int K)
{
    int M = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {
        M = Math.Max(A[i], M);
    }

    // Stores the frequency
    // of every elements
    int []freq = new int[M + 1];

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {
        freq[A[i]] += B[i];
    }

    // Initialize a variable to
    // store the prefix sums
    int sum = 0;

    // Iterate over the range [0, M]
    for(int i = 0; i <= M; i++)
    {

        // Increment sum by freq[i]
        sum += freq[i];

        // If sum is greater
        // than or equal to K
        if (sum >= K)
        {

            // Return the current
            // element as answer
            return i;
        }
    }

    // Return -1
    return -1;
}

// Driver code
public static void Main(String[] args)
{  

    // Given Input
    int []A = { 3, 4, 5 };
    int []B = { 2, 1, 3 };
    int N = A.Length;
    int K = 4;

    // Function call
    Console.Write(KthSmallest(A, B, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the Kth smallest element
    // that contains A[i] exactly B[i] times
    function KthSmallest(A, B, N, K)
    {

        let M = 0;

        // Traverse the given array
        for (let i = 0; i < N; i++) {

            M = Math.max(A[i], M);
        }

        // Stores the frequency
        // of every elements
        let freq = Array.from({length:  M + 1}, (_, i) => 0);

        // Traverse the given array
        for (let i = 0; i < N; i++) {
            freq[A[i]] += B[i];
        }

        // Initialize a variable to
        // store the prefix sums
        let sum = 0;

        // Iterate over the range [0, M]
        for (let i = 0; i <= M; i++) {

            // Increment sum by freq[i]
            sum += freq[i];

            // If sum is greater
            // than or equal to K
            if (sum >= K) {

                // Return the current
                // element as answer
                return i;
            }
        }
        // Return -1
        return -1;
    }

// Driver Code

    // Given Input
        let A = [ 3, 4, 5 ];
        let B = [ 2, 1, 3 ];
        let N = A.length;
        let K = 4;

        // Function call
        document.write(KthSmallest(A, B, N, K));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)，其中 **N** 是数组 **A[]** 和 **B[]。***
***辅助空间:** O(M)，其中 **M** 为数组的最大元素 **A[]** 。*