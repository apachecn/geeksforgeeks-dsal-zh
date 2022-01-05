# 用于 Q 查询的数组的所有子集的按位“与”的按位“或”

> 原文:[https://www . geesforgeks . org/q 查询数组的所有子集的逐位或运算/](https://www.geeksforgeeks.org/bitwise-or-of-bitwise-and-of-all-subsets-of-an-array-for-q-queries/)

给定两个大小为 **N** 的[**arr【】**和大小为 **Q、**的查询，任务是找到数组](https://www.geeksforgeeks.org/array-data-structure/)的[和](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)[子集的](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)[或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。在每个查询中，给你一个索引和值，你必须用给定值替换[数组](https://www.geeksforgeeks.org/array-data-structure/)给定索引处的值，并在每个查询后打印数组所有[子集的](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)[和](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的[或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = {3，5，7}，N = 3，查询[] = {{1，2}，{2，1}}，Q = 2
> **输出:** 7
> 3
> **解释:**
> 对于**第一个查询**将索引 1 处的值替换为值 2，更新后的数组 arr[]为{3，2，7}。
> 然后取所有子集的 AND，即 AND(3) = 3，AND(2) = 2，AND(7) = 7，AND(3，2) = 2，AND(3，7) = 3，AND(3，2，7) = 2。
> 所有子集的“与”的“或”为“或”(3，2，7，2，3，2) = 7。
> 现在，对于第二个查询**用值 1 替换索引 2 处的值，更新后的数组 arr[]为{3，2，1}。
> 然后取所有子集的 AND，即 AND(3) = 3，AND(2) = 2，AND(1) = 1，AND(3，2) = 2，AND(3，1) = 1，AND(3，2，1) = 0。
> 所有子集 OR(3，2，1，2，1，0) = 3 的“与”的“或”。**
> 
> ****输入:** arr[] = {1，2，3}，N = 3，查询[] = {{2，4}，{1，8}}，Q = 2
> **输出:** 7
> 13**

****方法:**这个问题可以用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:**

*   **初始化大小为 **32** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **位[]** ，并存储所有元素的设置位的计数。**
*   **[使用变量 **p** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，Q-1】**中迭代

    *   首先减去先前值的位，然后加上新值的位。
    *   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，31】**中迭代
        *   如果当前位被设置为前一个值，则用索引从**处的**位【】**数组中减去一位。**
        *   如果当前位被设置为新值，则在具有索引的**处向**位[]** 数组添加一位。**
    *   用给定数组中的前一个值替换新值 **arr[]。**
    *   初始化一个变量**和**来存储**位**数组的**或**。
    *   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，31】**中迭代
        *   如果当前位不等于 0，则将当前位的**或**加到**和**中。
    *   完成上述步骤后，打印**和**作为每个查询所需的答案。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the OR of AND of all
// subsets of the array for each query
void Or_of_Ands_for_each_query(int arr[], int n,
                               int queries[][2], int q)
{
    // An array to store the bits
    int bits[32] = { 0 };

    // Iterate for all the bits
    for (int i = 0; i < 32; i++) {
        // Iterate over all the numbers and
        // store the bits in bits[] array
        for (int j = 0; j < n; j++) {
            if ((1 << i) & arr[j]) {
                bits[i]++;
            }
        }
    }

    // Iterate over all the queries
    for (int p = 0; p < q; p++) {

        // Replace the bits of the value
        // at arr[queries[p][0]] with the bits
        // of queries[p][1]
        for (int i = 0; i < 32; i++) {
            if ((1 << i) & arr[queries[p][0]]) {
                bits[i]--;
            }
            if (queries[p][1] & (1 << i)) {
                bits[i]++;
            }
        }

        // Substitute the value in the array
        arr[queries[p][0]] = queries[p][1];
        int ans = 0;

        // Find OR of the bits[] array
        for (int i = 0; i < 32; i++) {
            if (bits[i] != 0) {
                ans |= (1 << i);
            }
        }
        // Print the answer
        cout << ans << endl;
    }
}

// Driver Code
int main()
{
    // Given Input
    int n = 3, q = 2;
    int arr[] = { 3, 5, 7 };
    int queries[2][2] = { { 1, 2 }, { 2, 1 } };

    // Function Call
    Or_of_Ands_for_each_query(arr, n, queries, q);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// java program for the above approach
import java.util.*;

class GFG {

    // Function to find the OR of AND of all
    // subsets of the array for each query
    static void Or_of_Ands_for_each_query(int arr[], int n,
                                          int queries[][],
                                          int q)
    {
        // An array to store the bits
        int bits[] = new int[32];
        Arrays.fill(bits, 0);

        // Iterate for all the bits
        for (int i = 0; i < 32; i++) {
            // Iterate over all the numbers and
            // store the bits in bits[] array
            for (int j = 0; j < n; j++) {
                if (((1 << i) & arr[j]) != 0) {
                    bits[i]++;
                }
            }
        }

        // Iterate over all the queries
        for (int p = 0; p < q; p++) {

            // Replace the bits of the value
            // at arr[queries[p][0]] with the bits
            // of queries[p][1]
            for (int i = 0; i < 32; i++) {
                if (((1 << i) & arr[queries[p][0]]) != 0) {
                    bits[i]--;
                }
                if ((queries[p][1] & (1 << i)) != 0) {
                    bits[i]++;
                }
            }

            // Substitute the value in the array
            arr[queries[p][0]] = queries[p][1];
            int ans = 0;

            // Find OR of the bits[] array
            for (int i = 0; i < 32; i++) {
                if (bits[i] != 0) {
                    ans |= (1 << i);
                }
            }

            // Print the answer
            System.out.println(ans);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int n = 3, q = 2;
        int arr[] = { 3, 5, 7 };
        int queries[][] = { { 1, 2 }, { 2, 1 } };

        // Function Call
        Or_of_Ands_for_each_query(arr, n, queries, q);
    }
}

// This code is contributed by subhammahato348.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the OR of AND of all
# subsets of the array for each query

def Or_of_Ands_for_each_query(arr, n, queries, q):

    # An array to store the bits
    bits = [0 for x in range(32)]

    # Iterate for all the bits
    for i in range(0, 32):

        # Iterate over all the numbers and
        # store the bits in bits[] array
        for j in range(0, n):
            if ((1 << i) & arr[j]):
                bits[i] += 1

    # Iterate over all the queries
    for p in range(0, q):

        # Replace the bits of the value
        # at arr[queries[p][0]] with the bits
        # of queries[p][1]
        for i in range(0, 32):
            if ((1 << i) & arr[queries[p][0]]):
                bits[i] -= 1
            if (queries[p][1] & (1 << i)):
                bits[i] += 1

        # Substitute the value in the array
        arr[queries[p][0]] = queries[p][1]
        ans = 0

        # Find OR of the bits[] array
        for i in range(0, 32):
            if (bits[i] != 0):
                ans |= (1 << i)

        # Print the answer
        print(ans)

#  Driver Code

#  Given Input
n = 3
q = 2
arr = [3, 5, 7]
queries = [[1, 2], [2, 1]]

# Function Call
Or_of_Ands_for_each_query(arr, n, queries, q)

# This code is contributed by amreshkumar3
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to find the OR of AND of all
// subsets of the array for each query
static void Or_of_Ands_for_each_query(int[] arr, int n,
                                      int[,] queries,
                                      int q)
{

    // An array to store the bits
    int[] bits = new int[32];
    for(int i = 0; i < 32; i++)
    {
        bits[i] = 0;
    }

    // Iterate for all the bits
    for(int i = 0; i < 32; i++)
    {

        // Iterate over all the numbers and
        // store the bits in bits[] array
        for(int j = 0; j < n; j++)
        {
            if (((1 << i) & arr[j]) != 0)
            {
                bits[i]++;
            }
        }
    }

    // Iterate over all the queries
    for(int p = 0; p < q; p++)
    {

        // Replace the bits of the value
        // at arr[queries[p][0]] with the bits
        // of queries[p][1]
        for(int i = 0; i < 32; i++)
        {
            if (((1 << i) & arr[queries[p, 0]]) != 0)
            {
                bits[i]--;
            }
            if ((queries[p, 1] & (1 << i)) != 0)
            {
                bits[i]++;
            }
        }

        // Substitute the value in the array
        arr[queries[p, 0]] = queries[p, 1];
        int ans = 0;

        // Find OR of the bits[] array
        for(int i = 0; i < 32; i++)
        {
            if (bits[i] != 0)
            {
                ans |= (1 << i);
            }
        }

        // Print the answer
        Console.WriteLine(ans);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int n = 3, q = 2;
    int[] arr = { 3, 5, 7 };
    int[,] queries = { { 1, 2 }, { 2, 1 } };

    // Function Call
    Or_of_Ands_for_each_query(arr, n, queries, q);
}
}

// This code is contributed by target_2
```

## **java 描述语言**

```
<script>

        // JavaScript program for the above approach

        // Function to find the OR of AND of all
        // subsets of the array for each query
        function Or_of_Ands_for_each_query(arr, n, queries, q) {
            // An array to store the bits
            let bits = new Array(32).fill(0);

            // Iterate for all the bits
            for (let i = 0; i < 32; i++) {
                // Iterate over all the numbers and
                // store the bits in bits[] array
                for (let j = 0; j < n; j++) {
                    if ((1 << i) & arr[j]) {
                        bits[i]++;
                    }
                }
            }

            // Iterate over all the queries
            for (let p = 0; p < q; p++) {

                // Replace the bits of the value
                // at arr[queries[p][0]] with the bits
                // of queries[p][1]
                for (let i = 0; i < 32; i++) {
                    if ((1 << i) & arr[queries[p][0]]) {
                        bits[i]--;
                    }
                    if (queries[p][1] & (1 << i)) {
                        bits[i]++;
                    }
                }

                // Substitute the value in the array
                arr[queries[p][0]] = queries[p][1];
                let ans = 0;

                // Find OR of the bits[] array
                for (let i = 0; i < 32; i++) {
                    if (bits[i] != 0) {
                        ans |= (1 << i);
                    }
                }
                // Prlet the answer
                document.write(ans + "<br>");
            }
        }

        // Driver Code

        // Given Input
        let n = 3, q = 2;
        let arr = [3, 5, 7];
        let queries = [[1, 2],
        [2, 1]];

        // Function Call
        Or_of_Ands_for_each_query(arr, n, queries, q);

    // This code is contributed by Potta Lokesh

</script>
```

****Output**

```
7
3
```** 

*****时间复杂度:** O(max(N，Q))*
***辅助空间:** O(1)***