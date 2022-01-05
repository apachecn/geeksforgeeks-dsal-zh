# 其和至少为剩余数组元素的对子集的最小大小

> 原文:[https://www . geesforgeks . org/最小大小的对子集，其和至少是剩余的数组元素/](https://www.geeksforgeeks.org/minimum-size-of-subset-of-pairs-whose-sum-is-at-least-the-remaining-array-elements/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**都由 **N** 正整数组成，任务是找到元素对 **(A[i]，B[i])** 的子集的最小大小，使得所有子集对的和至少是不包括在子集即 **(A[0] + B[0])中的剩余数组元素**A【】**的和**

**示例:**

> **输入:** A[] = {3，2，2}，B[] = {2，3，1}
> **输出:** 1
> **说明:**
> 选择子集为{(3，2)}。现在，子集之和为 3 + 2 = 5，大于剩余 A[] = 3 + 1 = 4 的和。
> 
> **输入:** A[] = {2，2，2，2，2}，B[] = {1，1，1，1，1 }
> T3】输出: 3

**天真方法:**最简单的方法是[生成给定元素对的所有可能子集](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)，并打印满足给定标准且具有最小大小的子集的大小。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，其思想是使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)，并且可以观察到选择 **i <sup>th</sup>** 对作为结果子集的一部分，两个子集之间的差减少了量 **(2*S[i] + U[i])** 。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说大小为 **N** 的**差[]** ，该数组存储每对元素的 **(2*A[i] + B[i])** 的值。
*   初始化一个变量，比如说 **sum** 保持跟踪剩余数组元素的总和**A【I】**。
*   初始化一个变量，比如 **K** 来跟踪结果子集的大小。
*   迭代范围**【0，N】**，将**差值【I】**的值更新为 **(2*A[i] + B[i])** 的值，将**和**的值减 **A[i]** 的值。
*   [按照递增顺序](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)对给定数组**差异[]** 进行排序。
*   [反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **差【】**，直到**和**为负，将**差【I】**的值加到**和**上，并将 **K** 的值增加 **1** 。
*   完成以上步骤后，打印 **K** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum size
// of subset satisfying given criteria
void maximizeApples(vector<int>& U, vector<int>& S, int N)
{

    // Stores the value of 2*S[i] + U[i]
    vector<int> x(N);

    // Stores the difference between
    // the 2 subsets
    int sum = 0;

    for (int i = 0; i < N; i++) {

        // Update the value of sum
        sum -= S[i];
        x[i] += 2 * S[i] + U[i];
    }

    // Sort the array X[] in an
    // ascending order
    sort(x.begin(), x.end());
    int ans = 0;
    int j = N - 1;

    // Traverse the array
    while (sum <= 0) {

        // Update the value of sum
        sum += x[j--];

        // Increment value of ans
        ans++;
    }

    // Print the resultant ans
    cout << ans;
}

// Driver Code
int main()
{
    vector<int> A = { 1, 1, 1, 1, 1 };
    vector<int> B = { 2, 2, 2, 2, 2 };
    int N = A.size();
    maximizeApples(A, B, N);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum size
    // of subset satisfying given criteria
    private static void maximizeApples(
        int[] U, int[] S, int N)
    {
        // Stores the value of 2*S[i] + U[i]
        int[] x = new int[N];

        // Stores the difference between
        // the 2 subsets
        int sum = 0;

        for (int i = 0; i < N; i++) {

            // Update the value of sum
            sum -= S[i];
            x[i] += 2 * S[i] + U[i];
        }

        // Sort the array X[] in an
        // ascending order
        Arrays.sort(x);
        int ans = 0;
        int j = N - 1;

        // Traverse the array
        while (sum <= 0) {

            // Update the value of sum
            sum += x[j--];

            // Increment value of ans
            ans++;
        }

        // Print the resultant ans
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] A = new int[] { 1, 1, 1, 1, 1 };
        int[] B = new int[] { 2, 2, 2, 2, 2 };
        int N = A.length;
        maximizeApples(A, B, N);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum size
# of subset satisfying given criteria
def maximizeApples(U, S, N):

    # Stores the value of 2*S[i] + U[i]
    x = [0]*N

    # Stores the difference between
    # the 2 subsets
    sum = 0

    for i in range(N):

        # Update the value of sum
        sum -= S[i]
        x[i] += 2 * S[i] + U[i]

    # Sort the array X[] in an
    # ascending order
    x.sort()
    ans = 0
    j = N - 1

    # Traverse the array
    while sum <= 0:

        # Update the value of sum
        sum += x[j]
        j = j - 1

        # Increment value of ans
        ans = ans + 1

    # Print the resultant ans
    print(ans)

# Driver Code
A = [1, 1, 1, 1, 1]
B = [2, 2, 2, 2, 2]
N = len(A)
maximizeApples(A, B, N)

# This code is contributed by Potta Lokesh
```

## C#

```
//  c# program for the above approach
using System.Collections.Generic;
using System;
class GFG
{

    // Function to find the minimum size
    // of subset satisfying given criteria
    static void maximizeApples(int[] U, int[] S, int N)
    {

        // Stores the value of 2*S[i] + U[i]
        List<int> x = new List<int>();

        // Stores the difference between
        // the 2 subsets
        int sum = 0;

        for (int i = 0; i < N; i++)
        {

            // Update the value of sum
            sum -= S[i];
            x.Add( 2 * S[i] + U[i]);
        }

        // Sort the array X[] in an
        // ascending order
        x.Sort();
        int ans = 0;
        int j = N - 1;

        // Traverse the array
        while (sum <= 0) {

            // Update the value of sum
            sum += x[j--];

            // Increment value of ans
            ans++;
        }

        // Print the resultant ans
        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main()
    {
        int[] A = new int[] { 1, 1, 1, 1, 1 };
        int[] B = new int[] { 2, 2, 2, 2, 2 };
        int N = A.Length;
        maximizeApples(A, B, N);
    }
}

// This code is contributed by amreshkumar3.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum size
// of subset satisfying given criteria
function maximizeApples(U, S, N) {
  // Stores the value of 2*S[i] + U[i]
  let x = new Array(N).fill(0);

  // Stores the difference between
  // the 2 subsets
  let sum = 0;

  for (let i = 0; i < N; i++) {
    // Update the value of sum
    sum -= S[i];
    x[i] += 2 * S[i] + U[i];
  }

  // Sort the array X[] in an
  // ascending order
  x.sort((a, b) => a - b);

  let ans = 0;
  let j = N - 1;

  // Traverse the array
  while (sum <= 0) {
    // Update the value of sum
    sum += x[j--];

    // Increment value of ans
    ans++;
  }

  // Prlet the resultant ans
  document.write(ans);
}

// Driver Code

let A = [1, 1, 1, 1, 1];
let B = [2, 2, 2, 2, 2];
let N = A.length;
maximizeApples(A, B, N);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*