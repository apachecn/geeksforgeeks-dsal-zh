# 给定数组的所有可能子集和值的集合包含数字[0，K]

的 K 的最大值

> 原文:[https://www . geesforgeks . org/k 的最大值一组给定数组的所有可能子集和值包含数字-0-k/](https://www.geeksforgeeks.org/largest-value-of-k-that-a-set-of-all-possible-subset-sum-values-of-given-array-contains-numbers-0-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出 **K** 的最大计数，即从 0 到 K 的[个连续整数](https://www.geeksforgeeks.org/longest-consecutive-subsequence/)，存在于[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) **S** 中，其中 **S** 包含[数组**arr【】**的所有可能子集和](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)值。

**示例:**

> **输入:** arr[] = {1，3}
> **输出:** 2
> **解释:**可能的子集是{}、{1}、{3}、{1，3}，它们各自的和是{0，1，3，4}。因此，包含所有子集和的集合中从 0 开始的连续整数的最大计数是 2(即{0，1})。
> 
> **输入:** arr[] = {1，1，1，4}
> **输出:** 8
> **解释:**包含给定数组所有子集和的集合为{0，1，2，3，4，5，6，7}。因此，从 0 开始的连续整数的最大计数是 8。

**天真方法:**给定的问题可以通过使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决，方法是将所有可能的子集和保持在一个数组中，该数组可以使用[背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)技术来完成。此后，计算连续整数的最大计数。

***时间复杂度:** O(N*K)其中 K 代表数组中所有元素的总和 **arr[]** 。*
***辅助空间:** O(K)*

**高效方法:**上述问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。假设包含数组所有子集和的集合 **arr[]** 包含范围**【0，X】**内的所有整数。如果在数组中引入一个新的数字 **Y** ，则**【Y，X+Y】**范围内的所有整数也可以作为子集和。利用这一观察，可以使用以下步骤解决给定的问题:

*   [按非递减顺序对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。
*   维护一个变量，比如说 **X** 为 **0** ，这表示范围**【0，X】**内的整数有可能作为给定数组**arr【】**的子集和。
*   为了保持连续整数的连续性， **arr[i] < = X + 1** 必须为真。因此，[遍历范围**【0，N)** 中每个 **i** 的给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果 **arr[i] < = X + 1** 的值，则更新 **X = X + arr[i]** 的值。否则，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，范围**【0，X】**即 **(X + 1)** 内的整数个数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum count of
// consecutive integers from 0 in set
// S of all possible subset-sum
int maxConsecutiveCnt(vector<int> arr)
{
    // Stores the maximum possible integer
    int X = 0;

    // Sort the given array in
    // non-decreasing order
    sort(arr.begin(), arr.end());

    // Iterate the given array
    for (int i = 0; i < arr.size(); i++) {

        // If arr[i] <= X+1, then update
        // X otherwise break the loop
        if (arr[i] <= (X + 1)) {
            X = X + arr[i];
        }
        else {
            break;
        }
    }

    // Return Answer
    return X + 1;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1, 1, 4 };
    cout << maxConsecutiveCnt(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG {

    // Function to find maximum count of
    // consecutive integers from 0 in set
    // S of all possible subset-sum
    public static int maxConsecutiveCnt(int[] arr)
    {

        // Stores the maximum possible integer
        int X = 0;

        // Sort the given array in
        // non-decreasing order
        Arrays.sort(arr);

        // Iterate the given array
        for (int i = 0; i < arr.length; i++) {

            // If arr[i] <= X+1, then update
            // X otherwise break the loop
            if (arr[i] <= (X + 1)) {
                X = X + arr[i];
            } else {
                break;
            }
        }

        // Return Answer
        return X + 1;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 1, 1, 1, 4 };
        System.out.println(maxConsecutiveCnt(arr));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find maximum count of
# consecutive integers from 0 in set
# S of all possible subset-sum
def maxConsecutiveCnt(arr):

    # Stores the maximum possible integer
    X = 0

    # Sort the given array in
    # non-decreasing order
    arr.sort()

    # Iterate the given array
    for i in range(0, len(arr)):

        # If arr[i] <= X+1, then update
        # X otherwise break the loop
        if (arr[i] <= (X + 1)):
            X = X + arr[i]

        else:
            break

    # Return Answer
    return X + 1

# Driver Code
if __name__ == "__main__":

    arr = [1, 1, 1, 4]
    print(maxConsecutiveCnt(arr))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find maximum count of
    // consecutive integers from 0 in set
    // S of all possible subset-sum
    public static int maxConsecutiveCnt(int[] arr)
    {

        // Stores the maximum possible integer
        int X = 0;

        // Sort the given array in
        // non-decreasing order
        Array.Sort(arr);

        // Iterate the given array
        for (int i = 0; i < arr.Length; i++)
        {

            // If arr[i] <= X+1, then update
            // X otherwise break the loop
            if (arr[i] <= (X + 1))
            {
                X = X + arr[i];
            }
            else
            {
                break;
            }
        }

        // Return Answer
        return X + 1;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 1, 1, 4 };
        Console.Write(maxConsecutiveCnt(arr));
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
       // JavaScript Program to implement
        // the above approach

        // Function to find maximum count of
        // consecutive integers from 0 in set
        // S of all possible subset-sum
        function maxConsecutiveCnt(arr)
        {

            // Stores the maximum possible integer
            let X = 0;

            // Sort the given array in
            // non-decreasing order
            arr.sort(function (a, b) { return a - b })

            // Iterate the given array
            for (let i = 0; i < arr.length; i++) {

                // If arr[i] <= X+1, then update
                // X otherwise break the loop
                if (arr[i] <= (X + 1)) {
                    X = X + arr[i];
                }
                else {
                    break;
                }
            }

            // Return Answer
            return X + 1;
        }

        // Driver Code
        let arr = [1, 1, 1, 4];
        document.write(maxConsecutiveCnt(arr));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*