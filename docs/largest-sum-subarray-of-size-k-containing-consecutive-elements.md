# 包含连续元素的大小为 K 的最大和子阵列

> 原文:[https://www . geeksforgeeks . org/包含连续元素的大小 k 的最大和子数组/](https://www.geeksforgeeks.org/largest-sum-subarray-of-size-k-containing-consecutive-elements/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找到大小为 **K** 的子数组的[最大和，使其包含任意组合的 **K** 个连续元素。](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

**示例:**

> **输入:** arr[] = {10，12，9，8，10，15，1，3，2}，K = 3
> **输出:** 27
> **说明:**
> 具有 K (= 3)个连续元素的子阵列为{9，8，10}，其元素之和为 9 + 8 + 10 = 27，最大。
> 
> **输入:** arr[] = {7，20，2，3，4}，K = 2
> T3】输出: 7

**方法:**可以通过检查每个大小为 **K** 的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)是否包含连续元素，然后相应地最大化[子阵列](https://www.geeksforgeeks.org/sum-of-all-subarrays/)的总和来解决给定的问题。按照以下步骤解决问题:

*   初始化一个变量，比如说 **currSum** 来存储 **K** 元素的当前子阵列的和，如果这些元素是连续的。
*   初始化一个变量 **maxSum** ，该变量存储任何大小的子阵列 **K** 的最大合成和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–K】**，并执行以下步骤:
    *   将从 **i** 开始的 **K** 元素储存在[阵](https://www.geeksforgeeks.org/array-data-structure/)T6【V】中。
    *   [按递增顺序排列阵列**V[]**](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)。
    *   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **V[]** 检查所有元素是否连续。如果发现为真，则将当前子阵列的总和存储在 **currSum** 中，并将 **maxSum** 更新为 **maxSum** 和 **currSum** 的最大值。
*   完成以上步骤后，打印 **maxSum** 的值作为结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest sum
// subarray such that it contains K
// consecutive elements
int maximumSum(vector<int> A, int N,
               int K)
{
    // Stores sum of subarray having
    // K consecutive elements
    int curr_sum = 0;

    // Stores the maximum sum among all
    // subarrays of size K having
    // consecutive elements
    int max_sum = INT_MIN;

    // Traverse the array
    for (int i = 0; i < N - K + 1; i++) {

        // Store K elements of one
        // subarray at a time
        vector<int> dupl_arr(
            A.begin() + i,
            A.begin() + i + K);

        // Sort the duplicate array
        // in ascending order
        sort(dupl_arr.begin(),
             dupl_arr.end());

        // Checks if elements in subarray
        // are consecutive or not
        bool flag = true;

        // Traverse the k elements
        for (int j = 1; j < K; j++) {

            // If not consecutive, break
            if (dupl_arr[j]
                    - dupl_arr[j - 1]
                != 1) {
                flag = false;
                break;
            }
        }

        // If flag is true update the
        // maximum sum
        if (flag) {
            int temp = 0;

            // Stores the sum of elements
            // of the current subarray
            curr_sum = accumulate(
                dupl_arr.begin(),
                dupl_arr.end(), temp);

            // Update the max_sum
            max_sum = max(max_sum,
                          curr_sum);

            // Reset curr_sum
            curr_sum = 0;
        }
    }

    // Return the result
    return max_sum;
}

// Driver Code
int main()
{
    vector<int> arr = { 10, 12, 9, 8, 10,
                        15, 1, 3, 2 };
    int K = 3;
    int N = arr.size();
    cout << maximumSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG
{

    // Function to find the largest sum
    // subarray such that it contains K
    // consecutive elements
public static Integer maximumSum(int[] A, int N, int K)
{

    // Stores sum of subarray having
    // K consecutive elements
    int curr_sum = 0;

    // Stores the maximum sum among all
    // subarrays of size K having
    // consecutive elements
    int max_sum = Integer.MIN_VALUE;

    // Traverse the array
    for (int i = 0; i < N - K + 1; i++) {

        // Store K elements of one
        // subarray at a time
        int[] dupl_arr = Arrays.copyOfRange(A, i, i + K);

        // Sort the duplicate array
        // in ascending order
        Arrays.sort(dupl_arr);

        // Checks if elements in subarray
        // are consecutive or not
        Boolean flag = true;

        // Traverse the k elements
        for (int j = 1; j < K; j++) {

            // If not consecutive, break
            if (dupl_arr[j] - dupl_arr[j - 1]
                != 1) {
                flag = false;
                break;
            }
        }

        // If flag is true update the
        // maximum sum
        if (flag) {
            int temp = 0;

            // Stores the sum of elements
            // of the current subarray
            curr_sum = 0;

            for(int x = 0; x < dupl_arr.length; x++){
                curr_sum += dupl_arr[x];
            }

            // Update the max_sum
            max_sum = Math.max(max_sum,
                          curr_sum);

            // Reset curr_sum
            curr_sum = 0;
        }
    }

    // Return the result
    return max_sum;
}

    // Driver Code
public static void main(String args[]) {
        int[] arr = { 10, 12, 9, 8, 10, 15, 1, 3, 2 };
        int K = 3;
        int N = arr.length;
        System.out.println(maximumSum(arr, N, K));
    }

}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the largest sum
# subarray such that it contains K
# consecutive elements
def maximumSum(A, N, K):

    # Stores sum of subarray having
    # K consecutive elements
    curr_sum = 0

    # Stores the maximum sum among all
    # subarrays of size K having
    # consecutive elements
    max_sum = -sys.maxsize - 1

    # Traverse the array
    for i in range(N - K + 1):

        # Store K elements of one
        # subarray at a time
        dupl_arr = A[i:i + K]

        # Sort the duplicate array
        # in ascending order
        dupl_arr.sort()

        # Checks if elements in subarray
        # are consecutive or not
        flag = True

        # Traverse the k elements
        for j in range(1, K, 1):

            # If not consecutive, break
            if (dupl_arr[j] - dupl_arr[j - 1] != 1):
                flag = False
                break

        # If flag is true update the
        # maximum sum
        if (flag):
            temp = 0

            # Stores the sum of elements
            # of the current subarray
            curr_sum = temp
            curr_sum = sum(dupl_arr)

            # Update the max_sum
            max_sum = max(max_sum, curr_sum)

            # Reset curr_sum
            curr_sum = 0

    # Return the result
    return max_sum

# Driver Code
if __name__ == '__main__':

    arr = [ 10, 12, 9, 8, 10,
            15, 1, 3, 2 ]
    K = 3
    N = len(arr)

    print(maximumSum(arr, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the largest sum
// subarray such that it contains K
// consecutive elements
function maximumSum(A, N, K) {
    // Stores sum of subarray having
    // K consecutive elements
    let curr_sum = 0;

    // Stores the maximum sum among all
    // subarrays of size K having
    // consecutive elements
    let max_sum = Number.MIN_SAFE_INTEGER;

    // Traverse the array
    for (let i = 0; i < N - K + 1; i++) {

        // Store K elements of one
        // subarray at a time
        let dupl_arr = [...A.slice(i, i + K)];

        // Sort the duplicate array
        // in ascending order
        dupl_arr.sort((a, b) => a - b)

        // Checks if elements in subarray
        // are consecutive or not
        let flag = true;

        // Traverse the k elements
        for (let j = 1; j < K; j++) {

            // If not consecutive, break
            if (dupl_arr[j]
                - dupl_arr[j - 1]
                != 1) {
                flag = false;
                break;
            }
        }

        // If flag is true update the
        // maximum sum
        if (flag) {
            let temp = 0;

            // Stores the sum of elements
            // of the current subarray
            curr_sum = dupl_arr.reduce((acc, cur) => acc + cur, 0)

            // Update the max_sum
            max_sum = Math.max(max_sum,
                curr_sum);

            // Reset curr_sum
            curr_sum = 0;
        }
    }

    // Return the result
    return max_sum;
}

// Driver Code

let arr = [10, 12, 9, 8, 10,
    15, 1, 3, 2];
let K = 3;
let N = arr.length;
document.write(maximumSum(arr, N, K));

</script>
```

**Output:** 

```
27
```

***时间复杂度:**O(N * K * log K)*
T5**辅助空间:** O(K)