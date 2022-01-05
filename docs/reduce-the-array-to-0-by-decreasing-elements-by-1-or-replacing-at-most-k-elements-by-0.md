# 通过将元素减少 1 或最多用 0 替换 K 个元素来将数组减少到 0

> 原文:[https://www . geeksforgeeks . org/通过将元素减少 1 或最多用 0 替换 k 个元素来将数组减少到 0/](https://www.geeksforgeeks.org/reduce-the-array-to-0-by-decreasing-elements-by-1-or-replacing-at-most-k-elements-by-0/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个正整数 **K** ，任务是找到将所有数组元素减少到 **0** 所需的最小操作数，以便在每次操作中将任意数组元素减少 **1** 并独立地将最多**K**个数组元素减少到 **0** 。

**示例:**

> **输入:** arr[] = {4，1，5}，K = 1
> **输出:** 5
> **说明:**以下是将所有数组元素转换为 0 的操作:
> 这里 K = 1，所以用 0 替换 arr[2]，将 arr[]转换为{4，1，0 }–>操作次数= 0。
> 将 arr[1]减少 1，将 arr[]转换为{4，0，0 }–>运算次数= 1。
> 将 arr[0]减少 1 四倍，将 arr[]转换为{0，0，0 }–>运算次数= 4。
> 因此，操作总数= 0 + 1 + 4 = 5，这是最小可能。
> 
> **输入:** arr[] = {4，2，10，9，18}，K = 2
> T3】输出: 15

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，该方法基于的思想是首先[以非递减顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对给定的数组 arr[]进行排序，然后将 [K 最大元素](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)更新为 **0** ，并对剩余的数组元素执行给定的操作。按照以下步骤解决给定的问题:

*   如果 **N** 的值最多为 **K** ，那么将所有数组元素替换为 **0** 。因此，这种情况下所需的操作次数为 **0** 。
*   [按照非递减顺序](https://www.geeksforgeeks.org/find-the-non-decreasing-order-array-from-given-array/)对数组 **arr[]** 进行排序。
*   将最后一个 **K** 元素替换为 **0** 。
*   打印第一个**(N–K)**元素的总和作为操作的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// operations needed to convert all the
// array elements to 0
int minOperations(vector<int> arr,
                  int K, int N)
{

    // If K is greater then 0 then
    // replace all array elements to 0
    if (K >= N)
        return 0;

    // Sort array in non-decreasing order
    sort(arr.begin(), arr.end());

    // Stores the count of operations
    // required
    int countOperations = 0;

    // Iterate loop until N - K times
    for (int i = 0; i < N - K; i++) {

        // Take sum of elements
        countOperations += arr[i];
    }

    // Return countOperations as
    // the required answer
    return countOperations;
}

// Driver Code
int main()
{

    vector<int> arr{ 4, 1, 5 };
    int N = arr.size();
    int K = 1;

    cout << minOperations(arr, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

public class GFG {

    // Function to find the minimum number
    // operations needed to convert all the
    // array elements to 0
    static int minOperations(int []arr,
                      int K, int N)
    {

        // If K is greater then 0 then
        // replace all array elements to 0
        if (K >= N)
            return 0;

        // Sort array in non-decreasing order
        Arrays.sort(arr) ;

        // Stores the count of operations
        // required
        int countOperations = 0;

        // Iterate loop until N - K times
        for (int i = 0; i < N - K; i++) {

            // Take sum of elements
            countOperations += arr[i];
        }

        // Return countOperations as
        // the required answer
        return countOperations;
    }

    // Driver Code
    public static void main (String[] args)
    {

        int[] arr = { 4, 1, 5 };
        int N = arr.length;
        int K = 1;

        System.out.println(minOperations(arr, K, N));
    }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# operations needed to convert all the
# array elements to 0
def minOperations(arr, K, N) :

    # If K is greater then 0 then
    # replace all array elements to 0
    if (K >= N) :
        return 0;

    # Sort array in non-decreasing order
    arr.sort();

    # Stores the count of operations
    # required
    countOperations = 0;

    # Iterate loop until N - K times
    for i in range(N - K) :

        # Take sum of elements
        countOperations += arr[i];

    # Return countOperations as
    # the required answer
    return countOperations;

# Driver Code
if __name__ == "__main__" :

    arr = [ 4, 1, 5 ];
    N = len(arr);
    K = 1;

    print(minOperations(arr, K, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find the minimum number
    // operations needed to convert all the
    // array elements to 0
    static int minOperations(int []arr,
                      int K, int N)
    {

        // If K is greater then 0 then
        // replace all array elements to 0
        if (K >= N)
            return 0;

        // Sort array in non-decreasing order
        Array.Sort(arr) ;

        // Stores the count of operations
        // required
        int countOperations = 0;

        // Iterate loop until N - K times
        for (int i = 0; i < N - K; i++) {

            // Take sum of elements
            countOperations += arr[i];
        }

        // Return countOperations as
        // the required answer
        return countOperations;
    }

    // Driver Code
    public static void Main (string[] args)
    {

        int[] arr = { 4, 1, 5 };
        int N = arr.Length;
        int K = 1;

        Console.WriteLine(minOperations(arr, K, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number
// operations needed to convert all the
// array elements to 0
function minOperations(arr, K, N)
{

  // If K is greater then 0 then
  // replace all array elements to 0
  if (K >= N) return 0;

  // Sort array in non-decreasing order
  arr.sort((a, b) => a - b);

  // Stores the count of operations
  // required
  let countOperations = 0;

  // Iterate loop until N - K times
  for (let i = 0; i < N - K; i++) {
    // Take sum of elements
    countOperations += arr[i];
  }

  // Return countOperations as
  // the required answer
  return countOperations;
}

// Driver Code

let arr = [4, 1, 5];
let N = arr.length;
let K = 1;

document.write(minOperations(arr, K, N));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*