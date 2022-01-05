# 给定数组中可被 M 整除的最大 K 位整数

> 原文:[https://www . geeksforgeeks . org/给定数组中最大的 k 位整数可被 m 整除/](https://www.geeksforgeeks.org/largest-k-digit-integer-from-given-array-divisible-by-m/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和 2 个整数 **K** 和 **M** ，任务是从数组**arr【】**中找到最大的整数 **K** 位，该整数可被 **M** 整除。如果找不到这样的整数，打印 **-1** 。

> **注意:**的值 **K** 是这样的，找到的整数总是小于或等于 INT_MAX。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，N=6，K=3，M=4
> **输出:** 652
> **说明:**3 位中最大的一位由数字 6，5，2 和它们的索引 1 组成。四和五。
> 
> **输入:** arr[] = {4，5，4}，N=3，K=3，M=50
> **输出:** -1
> **解释** :-数组中不存在可被 50 整除的整数，因为不存在 0。

**天真方法**:这可以通过找到大小为 K 的所有[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)然后检查条件找到最大的一个来完成。
***时间复杂度**:O(2<sup>N</sup>)*
***辅助空间** : O(1)*

**高效方法**:想法是检查数组中 **M** 的倍数中的每个数字，看是否有可能形成那个数字。如果有可能，那就更新答案。按照以下步骤解决问题:

*   如果 **K** 大于 **N，**则打印 **-1** 返回。
*   [用值 **0** 初始化大小为 **10** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **freq[]** ，以存储数组所有元素的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) **arr[]。**
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** 并存储数组中每个元素的频率 **freq[]。**
*   [按升序排列数组 **arr[]** 。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   初始化变量 **X** 并将其值设置为数组**arr【】**中最大的 **K** 位数。
*   如果 **X** 小于 **M** ，则打印 **-1** 返回。
*   将变量**答案**初始化为 **-1** 保存答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【M，X】**，并执行以下步骤:
    *   将变量 **y** 初始化为 **i.**
    *   [用值 **0** 初始化大小为 **10** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **v[]** ，以存储数字 **y.** 的所有数字的[频率](https://www.geeksforgeeks.org/check-if-the-frequency-of-all-the-digits-in-a-number-is-same/)
    *   遍历向量 **freq[]** 和 **v[]** ，如果所有位置 **freq[j]** 都大于等于 **v[j]，**，则更新**答案**作为**答案**或 **y.** 的最大值
*   执行上述步骤后，打印变量**答案**作为答案。

下面是上述方法的实现。

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest integer
// of K digits divisible by M
void find(vector<int>& arr, int N, int K, int M)
{

    // Base Case, as there is no sub-sequence
    // of size greater than N is possible
    if (K > N) {
        cout << "-1\n";
        return;
    }

    // Vector to store the frequency of each
    // number from the array
    vector<int> freq(10, 0);

    // Calculate the frequency of each from
    // the array
    for (int i = 0; i < N; i++) {
        freq[arr[i]]++;
    }

    // Sort the array in ascending order
    sort(arr.begin(), arr.end());

    // Variable to store the maximum number
    // possible
    int X = 0;

    // Traverse and store the largest K digits
    for (int i = N - 1; K > 0; i--) {
        X = X * 10 + arr[i];
        K--;
    }

    // Base Case
    if (X < M) {
        cout << "-1\n";
        return;
    }

    // Variable to store the answer
    int answer = -1;

    // Traverse and check for each number
    for (int i = M; i <= X; i = i + M) {
        int y = i;
        vector<int> v(10, 0);

        // Calculate the frequency of each number
        while (y > 0) {
            v[y % 10]++;
            y = y / 10;
        }

        bool flag = true;

        // If frequency of any digit in y is less than
        // that in freq[], then it's not possible.
        for (int j = 0; j <= 9; j++) {
            if (v[j] > freq[j]) {
                flag = false;
                break;
            }
        }

        if (flag)
            answer = max(answer, i);
    }

    // Print the answer
    cout << answer << endl;
}

// Driver Code
int main()
{

    vector<int> arr = { 1, 2, 3, 4, 5, 6 };
    int N = 6, K = 3, M = 4;

    find(arr, N, K, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
import java.util.Arrays;;
class GFG
{

    // Function to find the largest integer
    // of K digits divisible by M
    static void find(int[] arr, int N, int K, int M)
    {

        // Base Case, as there is no sub-sequence
        // of size greater than N is possible
        if (K > N) {
            System.out.println("-1\n");
            return;
        }

        // Vector to store the frequency of each
        // number from the array
        int freq[] = new int[10];

        // Calculate the frequency of each from
        // the array
        for (int i = 0; i < N; i++) {
            freq[arr[i]]++;
        }

        // Sort the array in ascending order
        Arrays.sort(arr);

        // Variable to store the maximum number
        // possible
        int X = 0;

        // Traverse and store the largest K digits
        for (int i = N - 1; K > 0; i--) {
            X = X * 10 + arr[i];
            K--;
        }

        // Base Case
        if (X < M) {
            System.out.println("-1");
            return;
        }

        // Variable to store the answer
        int answer = -1;

        // Traverse and check for each number
        for (int i = M; i <= X; i = i + M) {
            int y = i;
            int v[] = new int[10];

            // Calculate the frequency of each number
            while (y > 0) {
                v[y % 10]++;
                y = y / 10;
            }

            boolean flag = true;

            // If frequency of any digit in y is less than
            // that in freq[], then it's not possible.
            for (int j = 0; j <= 9; j++) {
                if (v[j] > freq[j]) {
                    flag = false;
                    break;
                }
            }

            if (flag)
                answer = Math.max(answer, i);
        }

        // Print the answer
        System.out.println(answer);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int N = 6, K = 3, M = 4;

        find(arr, N, K, M);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the largest integer
# of K digits divisible by M
def find(arr, N, K, M):

    # Base Case, as there is no sub-sequence
    # of size greater than N is possible
    if (K > N):
        print("-1")
        return

    # Vector to store the frequency of each
    # number from the array
    freq = [0] * 10

    # Calculate the frequency of each from
    # the array
    for i in range(N):
        freq[arr[i]] += 1

    # Sort the array in ascending order
    arr.sort()

    # Variable to store the maximum number
    # possible
    X = 0

    # Traverse and store the largest K digits
    for i in range(N - 1, 2, -1):
        X = X * 10 + arr[i]
        K -= 1

    # Base Case
    if (X < M):
        print("-1")
        return

    # Variable to store the answer
    answer = -1

    # Traverse and check for each number
    for i in range(M, X + 1, M):
        y = i
        v = [0] * 10

        # Calculate the frequency of each number
        while (y > 0):
            v[y % 10] += 1
            y = y // 10

        flag = True

        # If frequency of any digit in y is less than
        # that in freq[], then it's not possible.
        for j in range(10):
            if (v[j] > freq[j]):
                flag = False
                break

        if (flag):
            answer = max(answer, i)

    # Print the answer
    print(answer)

# Driver Code
arr = [1, 2, 3, 4, 5, 6]
N = 6
K = 3
M = 4

find(arr, N, K, M)

# This code is contributed by gfgking.
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

    // Function to find the largest integer
    // of K digits divisible by M
    static void find(int[] arr, int N, int K, int M)
    {

        // Base Case, as there is no sub-sequence
        // of size greater than N is possible
        if (K > N) {
            Console.WriteLine("-1\n");
            return;
        }

        // Vector to store the frequency of each
        // number from the array
        int []freq = new int[10];

        // Calculate the frequency of each from
        // the array
        for (int i = 0; i < N; i++) {
            freq[arr[i]]++;
        }

        // Sort the array in ascending order
        Array.Sort(arr);

        // Variable to store the maximum number
        // possible
        int X = 0;

        // Traverse and store the largest K digits
        for (int i = N - 1; K > 0; i--) {
            X = X * 10 + arr[i];
            K--;
        }

        // Base Case
        if (X < M) {
            Console.WriteLine("-1");
            return;
        }

        // Variable to store the answer
        int answer = -1;

        // Traverse and check for each number
        for (int i = M; i <= X; i = i + M) {
            int y = i;
            int []v = new int[10];

            // Calculate the frequency of each number
            while (y > 0) {
                v[y % 10]++;
                y = y / 10;
            }

            bool flag = true;

            // If frequency of any digit in y is less than
            // that in freq[], then it's not possible.
            for (int j = 0; j <= 9; j++) {
                if (v[j] > freq[j]) {
                    flag = false;
                    break;
                }
            }

            if (flag)
                answer = Math.Max(answer, i);
        }

        // Print the answer
        Console.WriteLine(answer);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int N = 6, K = 3, M = 4;

        find(arr, N, K, M);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the largest integer
// of K digits divisible by M
function find(arr, N, K, M) {

  // Base Case, as there is no sub-sequence
  // of size greater than N is possible
  if (K > N) {
    document.write("-1<br>");
    return;
  }

  // Vector to store the frequency of each
  // number from the array
  let freq = new Array(10).fill(0);

  // Calculate the frequency of each from
  // the array
  for (let i = 0; i < N; i++) {
    freq[arr[i]]++;
  }

  // Sort the array in ascending order
  arr.sort((a, b) => a - b);

  // Variable to store the maximum number
  // possible
  let X = 0;

  // Traverse and store the largest K digits
  for (let i = N - 1; K > 0; i--) {
    X = X * 10 + arr[i];
    K--;
  }

  // Base Case
  if (X < M) {
    cout << "-1\n";
    return;
  }

  // Variable to store the answer
  let answer = -1;

  // Traverse and check for each number
  for (let i = M; i <= X; i = i + M) {
    let y = i;
    let v = new Array(10).fill(0);

    // Calculate the frequency of each number
    while (y > 0) {
      v[y % 10]++;
      y = Math.floor(y / 10);
    }

    let flag = true;

    // If frequency of any digit in y is less than
    // that in freq[], then it's not possible.
    for (let j = 0; j <= 9; j++) {
      if (v[j] > freq[j]) {
        flag = false;
        break;
      }
    }

    if (flag)
      answer = Math.max(answer, i);
  }

  // Print the answer
  document.write(answer);
}

// Driver Code
let arr = [1, 2, 3, 4, 5, 6];
let N = 6, K = 3, M = 4;

find(arr, N, K, M);

// This code is contributed by gfgking.
</script>
```

**Output**

```
652
```

***时间复杂度** : O(max(M，N))*
***辅助空间** : O(1)*