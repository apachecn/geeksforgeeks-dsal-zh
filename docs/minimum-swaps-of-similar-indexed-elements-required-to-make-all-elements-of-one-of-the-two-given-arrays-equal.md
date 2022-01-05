# 使两个给定数组之一的所有元素相等所需的相似索引元素的最小互换量

> 原文:[https://www . geeksforgeeks . org/相似索引元素的最小互换-要求使两个给定数组中的一个数组的所有元素相等/](https://www.geeksforgeeks.org/minimum-swaps-of-similar-indexed-elements-required-to-make-all-elements-of-one-of-the-two-given-arrays-equal/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是计算使两个给定数组中的一个相等所需的相似索引元素的最小交换次数。如果不可能使一个数组的所有元素相等，则打印 **-1** 。

**示例:**

> **输入:** A[] = {3，4，1，3，1，3，4}，B[] = {1，3，3，1，3，4，3}
> **输出:** 3
> **解释:**
> 交换(A[0]，B[0])将 A[]修改为{1，4，1，3，1，3，4}，将 B[]修改为{3，3，3，1，3，4，3}。
> 交换(A[3]，B[3])将 A[]修改为{1，4，1，1，1，3，4}，将 B[]修改为{3，3，3，3，3，4，3}。
> 交换(A[5]，B[5])将 A[]修改为{1，4，1，1，1，4，4}，将 B[]修改为{3，3，3，3，3，3，3}。
> 由于数组 B[]只包含单个不同的元素，因此所需的输出为 3。
> 
> **输入:** A[] = {1，2，4，1，6，5，10}，B[] = {2，3，5，4，1，8，2}
> **输出:** -1

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如 **minSwaps** ，以存储所需的最小交换次数，这样至少一个数组只包含一个不同的值。
*   初始化另一个变量，比如**交换所需的**，以存储所需的交换次数，这样至少一个数组只包含一个不同的值。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如 **countA[]** ，来存储数组 **A[]** 中每个不同元素的[频率。](https://www.geeksforgeeks.org/c-program-to-count-frequency-of-each-element-in-an-array/)
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如 **countB[]** ，来存储数组 **B[]** 中每个不同元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说 **countAB[]** ，以存储出现在 **A[]** 和 **B[]** 相同索引处的每个不同元素的频率。
*   [使用变量 **i** 遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**(countA[I]+countB[I]–countAB[I]= = N)**的值是否为真。如果发现为真，则更新**swap required = min(countA[I]，countB[I])–countAB[I]**并更新**minswap = min(minswap，swap required)**。
*   最后，打印 **minSwaps** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of swap
// require such that either of the array
// contain a single distinct value
int minimumNumOfSwap(int A[], int B[], int N)
{

    // Stores largest element of
    // the array A[]
    int MaxA = *max_element(A, A + N);

    // Stores largest element of
    // the array B[]
    int MaxB = *max_element(B, B + N);

    // Stores maximum value
    // of (MaxA, MaxB)
    int M = max(MaxA, MaxB);

    // Store the frequency of
    // each distinct element of A[]
    int countA[M + 1] = { 0 };

    // Store the frequency of
    // each distinct element of B[]
    int countB[M + 1] = { 0 };

    // Store frequency of each distinct
    // element which is present at
    // same indices in A[] and B[]
    int equalAB[M + 1] = { 0 };

    // Stores count of swaps required such
    // that at least one of the arrays
    // contain a single distinct value
    int swapsRequired;

    // Stores minimum count of swaps required
    // such that at least one of the arrays
    // contain single distinct value
    int minSwaps = N;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of A[i]
        countA[A[i]]++;

        // Update frequency of B[i]
        countB[B[i]]++;

        // If A[i] and B[i] are equal
        if (A[i] == B[i]) {

            // Update frequency
            // of A[i] and B[i]
            equalAB[A[i]]++;
        }
    }

    // Traverse each distinct
    // element of A[] and B[]
    for (int i = 1; i <= M; i++) {

        // If sum of frequency of i in A and B
        // present at different indices is N
        if ((countA[i] + countB[i]
             - equalAB[i])
            == N) {

            // Update swapsRequired
            swapsRequired
                = min(countA[i], countB[i])
                  - equalAB[i];

            // Update minSwaps
            minSwaps = min(minSwaps,
                           swapsRequired);
        }
    }

    // If minSwaps is equal to N
    if (minSwaps == N) {
        return -1;
    }
    else {
        return minSwaps;
    }
}

// Driver Code
int main()
{
    int A[] = { 3, 4, 1, 3, 1, 3, 4 };
    int B[] = { 1, 3, 3, 1, 3, 4, 3 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << minimumNumOfSwap(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

public class Main
{
    // Function to count minimum number of swap
    // require such that either of the array
    // contain a single distinct value
    public static int minimumNumOfSwap(int A[], int B[], int N)
    {

        // Stores largest element of
        // the array A[]
        int MaxA = Arrays.stream(A).max().getAsInt();

        // Stores largest element of
        // the array B[]
        int MaxB = Arrays.stream(B).max().getAsInt();

        // Stores maximum value
        // of (MaxA, MaxB)
        int M = Math.max(MaxA, MaxB);

        // Store the frequency of
        // each distinct element of A[]
        int[] countA = new int[M + 1];

        // Store the frequency of
        // each distinct element of B[]
        int[] countB = new int[M + 1];

        // Store frequency of each distinct
        // element which is present at
        // same indices in A[] and B[]
        int[] equalAB = new int[M + 1];

        // Stores count of swaps required such
        // that at least one of the arrays
        // contain a single distinct value
        int swapsRequired;

        // Stores minimum count of swaps required
        // such that at least one of the arrays
        // contain single distinct value
        int minSwaps = N;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Update frequency of A[i]
            countA[A[i]]++;

            // Update frequency of B[i]
            countB[B[i]]++;

            // If A[i] and B[i] are equal
            if (A[i] == B[i])
            {

                // Update frequency
                // of A[i] and B[i]
                equalAB[A[i]]++;
            }
        }

        // Traverse each distinct
        // element of A[] and B[]
        for (int i = 1; i <= M; i++)
        {

            // If sum of frequency of i in A and B
            // present at different indices is N
            if ((countA[i] + countB[i]
                 - equalAB[i])
                == N)
            {

                // Update swapsRequired
                swapsRequired
                    = Math.min(countA[i], countB[i])
                      - equalAB[i];

                // Update minSwaps
                minSwaps = Math.min(minSwaps,
                               swapsRequired);
            }
        }

        // If minSwaps is equal to N
        if (minSwaps == N)
        {
            return -1;
        }
        else
        {
            return minSwaps;
        }
    }

    public static void main(String[] args)
    {
        int A[] = { 3, 4, 1, 3, 1, 3, 4 };
        int B[] = { 1, 3, 3, 1, 3, 4, 3 };

        int N = A.length;

        System.out.println(minimumNumOfSwap(A, B, N));
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count minimum number of swap
# require such that either of the array
# contain a single distinct value
def minimumNumOfSwap(A, B, N) :

    # Stores largest element of
    # the array A[]
    MaxA = max(A)

    # Stores largest element of
    # the array B[]
    MaxB = max(B)

    # Stores maximum value
    # of (MaxA, MaxB)
    M = max(MaxA, MaxB)

    # Store the frequency of
    # each distinct element of A[]
    countA = [0] * (M + 1)

    # Store the frequency of
    # each distinct element of B[]
    countB = [0] * (M + 1)

    # Store frequency of each distinct
    # element which is present at
    # same indices in A[] and B[]
    equalAB = [0] * (M + 1)

    # Stores count of swaps required such
    # that at least one of the arrays
    # contain a single distinct value
    swapsRequired = 0

    # Stores minimum count of swaps required
    # such that at least one of the arrays
    # contain single distinct value
    minSwaps = N

    # Traverse the array
    for i in range(N) :

        # Update frequency of A[i]
        countA[A[i]] += 1

        # Update frequency of B[i]
        countB[B[i]] += 1

        # If A[i] and B[i] are equal
        if (A[i] == B[i]) :

            # Update frequency
            # of A[i] and B[i]
            equalAB[A[i]] += 1

    # Traverse each distinct
    # element of A[] and B[]
    for i in range(1, M + 1) :

        # If sum of frequency of i in A and B
        # present at different indices is N
        if ((countA[i] + countB[i] - equalAB[i]) == N) :

            # Update swapsRequired
            swapsRequired = min(countA[i], countB[i]) - equalAB[i]

            # Update minSwaps
            minSwaps = min(minSwaps, swapsRequired)

    # If minSwaps is equal to N
    if (minSwaps == N) :
        return -1
    else :
        return minSwaps

# Driver code
A = [ 3, 4, 1, 3, 1, 3, 4 ]
B = [ 1, 3, 3, 1, 3, 4, 3 ]

N = len(A)

print(minimumNumOfSwap(A, B, N))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Linq;

class GFG{

// Function to count minimum number of swap
// require such that either of the array
// contain a single distinct value
public static int minimumNumOfSwap(int []A, int []B,
                                   int N)
{

    // Stores largest element of
    // the array A[]
    int MaxA = A.Max();

    // Stores largest element of
    // the array B[]
    int MaxB = B.Max();

    // Stores maximum value
    // of (MaxA, MaxB)
    int M = Math.Max(MaxA, MaxB);

    // Store the frequency of
    // each distinct element of A[]
    int[] countA = new int[M + 1];

    // Store the frequency of
    // each distinct element of B[]
    int[] countB = new int[M + 1];

    // Store frequency of each distinct
    // element which is present at
    // same indices in A[] and B[]
    int[] equalAB = new int[M + 1];

    // Stores count of swaps required such
    // that at least one of the arrays
    // contain a single distinct value
    int swapsRequired;

    // Stores minimum count of swaps required
    // such that at least one of the arrays
    // contain single distinct value
    int minSwaps = N;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency of A[i]
        countA[A[i]]++;

        // Update frequency of B[i]
        countB[B[i]]++;

        // If A[i] and B[i] are equal
        if (A[i] == B[i])
        {

            // Update frequency
            // of A[i] and B[i]
            equalAB[A[i]]++;
        }
    }

    // Traverse each distinct
    // element of A[] and B[]
    for(int i = 1; i <= M; i++)
    {

        // If sum of frequency of i in A and B
        // present at different indices is N
        if ((countA[i] + countB[i] - equalAB[i]) == N)
        {

            // Update swapsRequired
            swapsRequired = Math.Min(countA[i],
                                     countB[i]) -
                                     equalAB[i];

            // Update minSwaps
            minSwaps = Math.Min(minSwaps,
                                swapsRequired);
        }
    }

    // If minSwaps is equal to N
    if (minSwaps == N)
    {
        return -1;
    }
    else
    {
        return minSwaps;
    }
}

// Driver Code
public static void Main(string[] args)
{
    int []A = { 3, 4, 1, 3, 1, 3, 4 };
    int []B = { 1, 3, 3, 1, 3, 4, 3 };

    int N = A.Length;

    Console.WriteLine(minimumNumOfSwap(A, B, N));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to count minimum number of swap
    // require such that either of the array
    // contain a single distinct value
    function minimumNumOfSwap(A, B, N)
    {

        // Stores largest element of
        // the array A[]
        let MaxA = 0;
        for(let i = 0; i < A.length; i++)
        {
            MaxA = Math.max(MaxA, A[i]);
        }

        // Stores largest element of
        // the array B[]
        let MaxB = 0;
        for(let i = 0; i < B.length; i++)
        {
            MaxB = Math.max(MaxB, B[i]);
        }

        // Stores maximum value
        // of (MaxA, MaxB)
        let M = Math.max(MaxA, MaxB);

        // Store the frequency of
        // each distinct element of A[]
        let countA = new Array(M + 1);
        countA.fill(0);

        // Store the frequency of
        // each distinct element of B[]
        let countB = new Array(M + 1);
        countB.fill(0);

        // Store frequency of each distinct
        // element which is present at
        // same indices in A[] and B[]
        let equalAB = new Array(M + 1);
        equalAB.fill(0);

        // Stores count of swaps required such
        // that at least one of the arrays
        // contain a single distinct value
        let swapsRequired;

        // Stores minimum count of swaps required
        // such that at least one of the arrays
        // contain single distinct value
        let minSwaps = N;

        // Traverse the array
        for(let i = 0; i < N; i++)
        {

            // Update frequency of A[i]
            countA[A[i]]++;

            // Update frequency of B[i]
            countB[B[i]]++;

            // If A[i] and B[i] are equal
            if (A[i] == B[i])
            {

                // Update frequency
                // of A[i] and B[i]
                equalAB[A[i]]++;
            }
        }

        // Traverse each distinct
        // element of A[] and B[]
        for(let i = 1; i <= M; i++)
        {

            // If sum of frequency of i in A and B
            // present at different indices is N
            if ((countA[i] + countB[i] - equalAB[i]) == N)
            {

                // Update swapsRequired
                swapsRequired = Math.min(countA[i],
                                         countB[i]) -
                                         equalAB[i];

                // Update minSwaps
                minSwaps = Math.min(minSwaps,
                                    swapsRequired);
            }
        }

        // If minSwaps is equal to N
        if (minSwaps == N)
        {
            return -1;
        }
        else
        {
            return minSwaps;
        }
    }

    // Driver code
    let A = [ 3, 4, 1, 3, 1, 3, 4 ];
    let B = [ 1, 3, 3, 1, 3, 4, 3 ];
    let N = A.length;
    document.write(minimumNumOfSwap(A, B, N));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(M + N)，其中 M 是 A[]和 B[]中最大的元素。*
***辅助空间:** O(M)*