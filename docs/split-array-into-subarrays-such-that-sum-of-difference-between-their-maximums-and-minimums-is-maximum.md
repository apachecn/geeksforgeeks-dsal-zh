# 将阵列分成子阵列，使其最大值和最小值之间的差值之和最大

> 原文:[https://www . geeksforgeeks . org/将数组拆分为子数组，这样它们的最大值和最小值之间的差值之和就是最大值/](https://www.geeksforgeeks.org/split-array-into-subarrays-such-that-sum-of-difference-between-their-maximums-and-minimums-is-maximum/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是将该数组拆分为[个子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的[最大元素和最小元素](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)之差之和最大。

**示例**:

> **输入:** arr[] = {8，1，7，9，2}
> **输出:** 14
> **解释:**
> 考虑将给定阵列拆分为{8，1}和{7，9，2}两个子阵列。最大和最小元素之间的区别是:
> 
> *   **{8，1}:** 差为(8–1)= 7。
> *   **{7，9，2}:** 差为(9–2)= 7。
> 
> 因此，差之和为 7 + 7 = 14。
> 
> **输入:** arr[] = {1，2，1，0，5}
> **输出:** 6

**方法:**给定的问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决问题:

*   初始化一个数组，比如说 **dp[]** ，其中 **dp[i]** 代表第一个 **i** 数组元素的所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的[最大和最小元素](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)之差的最大和。
*   将**DP【0】**初始化为 **0** 。
*   [在范围**【1，N–1】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   初始化一个变量，说 **min** 为**arr【I】**，该变量存储范围内的最小元素**【0，I】**。
    *   初始化一个变量，比如说 **max** 为**arr【I】**，该变量存储范围内的最大元素**【0，I】**。
    *   使用变量 **j** 以相反的顺序迭代范围**【0，I】**，并执行以下步骤:
        *   将 **min** 的值更新为 **min** 和**arr【j】**的最小值。
        *   将**最大值**更新为**最大值**和**arr【j】**的最小值。
        *   将 **dp[j]** 的值更新为 **dp[j]** 和**的最大值(最大–最小+ dp[i])** 。
*   完成上述步骤后，打印**DP【N–1】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum of
// difference between maximums and
// minimums in the splitted subarrays
int getValue(int arr[], int N)
{
    int dp[N];
    memset(dp, 0, sizeof(dp));

    // Base Case
    dp[0] = 0;

    // Traverse the array
    for(int i = 1; i < N; i++)
    {

        // Stores the maximum and
        // minimum elements upto
        // the i-th index
        int minn = arr[i];
        int maxx = arr[i];

        // Traverse the range [0, i]
        for(int j = i; j >= 0; j--)
        {

            // Update the minimum
            minn = min(arr[j], minn);

            // Update the maximum
            maxx = max(arr[j], maxx);

            // Update dp[i]
            dp[i] = max(dp[i], maxx - minn +
                   ((j >= 1) ? dp[j - 1] : 0));
        }
    }

    // Return the maximum
    // sum of difference
    return dp[N - 1];
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 7, 9, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getValue(arr, N);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
public class Main {

    // Function to find maximum sum of
    // difference between maximums and
    // minimums in the splitted subarrays
    static int getValue(int[] arr, int N)
    {
        int dp[] = new int[N];

        // Base Case
        dp[0] = 0;

        // Traverse the array
        for (int i = 1; i < N; i++) {

            // Stores the maximum and
            // minimum elements upto
            // the i-th index
            int min = arr[i];
            int max = arr[i];

            // Traverse the range [0, i]
            for (int j = i; j >= 0; j--) {

                // Update the minimum
                min = Math.min(arr[j], min);

                // Update the maximum
                max = Math.max(arr[j], max);

                // Update dp[i]
                dp[i] = Math.max(
                    dp[i],
                    max - min + ((j >= 1)
                                     ? dp[j - 1]
                                     : 0));
            }
        }

        // Return the maximum
        // sum of difference
        return dp[N - 1];
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 8, 1, 7, 9, 2 };
        int N = arr.length;
        System.out.println(getValue(arr, N));
    }
}
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find maximum sum of
// difference between maximums and
// minimums in the splitted subarrays
static int getValue(int[] arr, int N)
{
    int[] dp = new int[N];

    // Base Case
    dp[0] = 0;

    // Traverse the array
    for(int i = 1; i < N; i++)
    {

        // Stores the maximum and
        // minimum elements upto
        // the i-th index
        int min = arr[i];
        int max = arr[i];

        // Traverse the range [0, i]
        for(int j = i; j >= 0; j--)
        {

            // Update the minimum
            min = Math.Min(arr[j], min);

            // Update the maximum
            max = Math.Max(arr[j], max);

            // Update dp[i]
            dp[i] = Math.Max(
                dp[i],
                max - min + ((j >= 1) ?
                     dp[j - 1] : 0));
        }
    }

    // Return the maximum
    // sum of difference
    return dp[N - 1];
}

// Driver Code
static public void Main()
{
    int[] arr = { 8, 1, 7, 9, 2 };
    int N = arr.Length;

    Console.Write(getValue(arr, N));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find maximum sum of
# difference between maximums and
# minimums in the splitted subarrays
def getValue(arr, N):
    dp = [0 for i in range(N)]

    # Traverse the array
    for i in range(1, N):

        # Stores the maximum and
        # minimum elements upto
        # the i-th index
        minn = arr[i]
        maxx = arr[i]

        j = i

        # Traverse the range [0, i]
        while(j >= 0):

            # Update the minimum
            minn = min(arr[j], minn)

            # Update the maximum
            maxx = max(arr[j], maxx)

            # Update dp[i]
            dp[i] = max(dp[i], maxx - minn + (dp[j - 1] if (j >= 1) else 0))
            j -= 1

    # Return the maximum
    # sum of difference
    return dp[N - 1]

# Driver code
if __name__ == '__main__':
    arr = [8, 1, 7, 9, 2]
    N = len(arr)
    print(getValue(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to find maximum sum of
    // difference between maximums and
    // minimums in the splitted subarrays
    function getValue(arr, N)
    {
        let dp = Array.from({length: N}, (_, i) => 0);

        // Base Case
        dp[0] = 0;

        // Traverse the array
        for (let i = 1; i < N; i++) {

            // Stores the maximum and
            // minimum elements upto
            // the i-th index
            let min = arr[i];
            let max = arr[i];

            // Traverse the range [0, i]
            for (let j = i; j >= 0; j--) {

                // Update the minimum
                min = Math.min(arr[j], min);

                // Update the maximum
                max = Math.max(arr[j], max);

                // Update dp[i]
                dp[i] = Math.max(
                    dp[i],
                    max - min + ((j >= 1)
                                     ? dp[j - 1]
                                     : 0));
            }
        }

        // Return the maximum
        // sum of difference
        return dp[N - 1];
    }

// Driver code

        let arr = [ 8, 1, 7, 9, 2 ];
        let N = arr.length;
        document.write(getValue(arr, N));

</script>
```

**Output:** 

```
14
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*