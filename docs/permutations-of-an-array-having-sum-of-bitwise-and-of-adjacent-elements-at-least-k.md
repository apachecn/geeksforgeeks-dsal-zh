# 相邻元素的位与之和至少为 K 的数组的排列

> 原文:[https://www . geeksforgeeks . org/具有相邻元素按位和的数组排列-至少-k/](https://www.geeksforgeeks.org/permutations-of-an-array-having-sum-of-bitwise-and-of-adjacent-elements-at-least-k/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到数组 **arr[]** 的所有[排列，使得每个排列中相邻元素的](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)[位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 之和大于或等于 **K** 。如果不存在这样的排列，打印**-1”**。

**示例:**

> ***输入:** arr[] = {1，2，3，4，5}，K = 8*
> ***输出:***
> *2，3，1，5，4*
> *4，5，1，3，2*
> ***解释:***
> *为排列{2，3，1，5，4}*
> *对于排列{4，5，1，3，2 }:(4&5)+(5&1)+(1&3)+(3&2)= 8，至少为 K( = 8)。*
> 
> ***输入:** arr[] = {1，2，3}，K = 4*
> ***输出:** -1*

**方法:**想法是[生成**arr【】**T5】的所有可能排列，并检查每个排列，如果要求的条件满足或不满足。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)

*   初始化一个布尔变量，说**标记**为**假**，检查是否存在任何需要的排列。
*   [生成数组 **arr[]**](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/) 的所有可能排列，并执行以下步骤:
    *   计算当前排列中所有相邻数组元素对的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)之和，并将 t 存储在一个变量中，比如**和**。
    *   [在**【0，N–2】**范围内遍历当前排列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将**arr【I】**和**arr【I+1】**的**位与**相加至**和**。
    *   如果**和**的值至少为 **K** ，则将**标志**设置为**真**，打印当前排列。
*   完成上述步骤后，如果**标志**的值为**假**，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print all permutations of
// arr[] such that the sum of Bitwise AND
// of all adjacent element is at least K
void printPermutation(int arr[], int n,
                      int k)
{
    // To check if any permutation
    // exists or not
    bool flag = false;

    // Sort the given array
    sort(arr, arr + n);

    // Find all possible permutations
    do {

        // Stores the sum of bitwise AND
        // of adjacent elements of the
        // current permutation
        int sum = 0;

        // Traverse the current
        // permutation of arr[]
        for (int i = 0; i < n - 1; i++) {

            // Update the sum
            sum += arr[i] & arr[i + 1];
        }

        // If the sum is at least K, then
        // print the current permutation
        if (sum >= k) {

            // Set the flag variable
            flag = true;

            // Print the current permutation
            for (int i = 0; i < n; i++) {
                cout << arr[i] << " ";
            }
            cout << "\n";
        }

    } while (next_permutation(arr, arr + n));

    // If flag is unset, then print -1
    if (flag == false) {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int K = 8;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printPermutation(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to print all permutations of
  // arr[] such that the sum of Bitwise AND
  // of all adjacent element is at least K
  static void printPermutation(int arr[], int n,
                               int k)
  {

    // To check if any permutation
    // exists or not
    boolean flag = false;

    // Sort the given array
    Arrays.sort(arr);

    // Find all possible permutations
    do
    {

      // Stores the sum of bitwise AND
      // of adjacent elements of the
      // current permutation
      int sum = 0;

      // Traverse the current
      // permutation of arr[]
      for (int i = 0; i < n - 1; i++)
      {

        // Update the sum
        sum += arr[i] & arr[i + 1];
      }

      // If the sum is at least K, then
      // print the current permutation
      if (sum >= k)
      {

        // Set the flag variable
        flag = true;

        // Print the current permutation
        for (int i = 0; i < n; i++)
        {
          System.out.print(arr[i]+ " ");
        }
        System.out.print("\n");
      }

    } while (next_permutation(arr));

    // If flag is unset, then print -1
    if (flag == false)
    {
      System.out.print("-1");
    }
  }
  static boolean next_permutation(int[] p) {
    for (int a = p.length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.length - 1;; --b)
          if (p[b] > p[a]) {
            int t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.length - 1; a < b; ++a, --b) {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 2, 3, 4, 5 };
    int K = 8;
    int N = arr.length;

    // Function Call
    printPermutation(arr, N, K);
  }
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  // Function to print all permutations of
  // []arr such that the sum of Bitwise AND
  // of all adjacent element is at least K
  static void printPermutation(int []arr, int n,
                               int k)
  {

    // To check if any permutation
    // exists or not
    bool flag = false;

    // Sort the given array
    Array.Sort(arr);

    // Find all possible permutations
    do
    {

      // Stores the sum of bitwise AND
      // of adjacent elements of the
      // current permutation
      int sum = 0;

      // Traverse the current
      // permutation of []arr
      for (int i = 0; i < n - 1; i++)
      {

        // Update the sum
        sum += arr[i] & arr[i + 1];
      }

      // If the sum is at least K, then
      // print the current permutation
      if (sum >= k)
      {

        // Set the flag variable
        flag = true;

        // Print the current permutation
        for (int i = 0; i < n; i++)
        {
          Console.Write(arr[i] + " ");
        }
        Console.Write("\n");
      }

    } while (next_permutation(arr));

    // If flag is unset, then print -1
    if (flag == false)
    {
      Console.Write("-1");
    }
  }
  static bool next_permutation(int[] p) {
    for (int a = p.Length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.Length - 1;; --b)
          if (p[b] > p[a]) {
            int t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.Length - 1; a < b; ++a, --b) {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 1, 2, 3, 4, 5 };
    int K = 8;
    int N = arr.Length;

    // Function Call
    printPermutation(arr, N, K);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
def next_permutation(a):
    for i in reversed(range(len(a) - 1)):
        if a[i] < a[i + 1]:
            break
    else:
        return False
    j = next(j for j in
             reversed(range(i + 1, len(a)))
             if a[i] < a[j])
    a[i], a[j] = a[j], a[i]
    a[i + 1:] = reversed(a[i + 1:])
    return True

# Function to print all permutations of
# arr[] such that the sum of Bitwise AND
# of all adjacent element is at least K
def printPermutation(arr, n, k):

    # To check if any permutation
    # exists or not
    flag = False

    # Sort the given array
    arr.sort()

    # Find all possible permutations
    while True:

        # Stores the sum of bitwise AND
        # of adjacent elements of the
        # current permutation
        sum = 0

        # Traverse the current
        # permutation of arr[]
        for i in range(n - 1):

            # Update the sum
            sum += arr[i] & arr[i + 1]

        # If the sum is at least K, then
        # print the current permutation
        if (sum >= k):

            # Set the flag variable
            flag = True

            # Print the current permutation
            for i in range(n):
                print(arr[i], end = " ")

            print()
        if (next_permutation(arr) == False):
            break

        # If flag is unset, then print -1
    if (flag == False):
        print("-1")

# Driver Code
arr = [1, 2, 3, 4, 5]
K = 8
N = len(arr)

# Function Call
printPermutation(arr, N, K)

# This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

  // Function to print all permutations of
  // arr[] such that the sum of Bitwise AND
  // of all adjacent element is at least K
  function printPermutation(arr, n, k)
  {

    // To check if any permutation
    // exists or not
    let flag = false;

    // Sort the given array
    arr.sort();

    // Find all possible permutations
    do
    {

      // Stores the sum of bitwise AND
      // of adjacent elements of the
      // current permutation
      let sum = 0;

      // Traverse the current
      // permutation of arr[]
      for (let i = 0; i < n - 1; i++)
      {

        // Update the sum
        sum += arr[i] & arr[i + 1];
      }

      // If the sum is at least K, then
      // print the current permutation
      if (sum >= k)
      {

        // Set the flag variable
        flag = true;

        // Print the current permutation
        for (let i = 0; i < n; i++)
        {
          document.write(arr[i]+ " ");
        }
        document.write("<br/>");
      }

    } while (next_permutation(arr));

    // If flag is unset, then print -1
    if (flag == false)
    {
      System.out.print("-1");
    }
  }
  function next_permutation(p) {
    for (let a = p.length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (let b = p.length - 1;; --b)
          if (p[b] > p[a]) {
            let t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.length - 1; a < b; ++a, --b) {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

// Driver code

    let arr = [ 1, 2, 3, 4, 5 ];
    let K = 8;
    let N = arr.length;

    // Function Call
    printPermutation(arr, N, K);

</script>
```

**Output:** 

```
2 3 1 5 4 
4 5 1 3 2
```

***时间复杂度:** O(N*(N！))*
***辅助空间:** O(1)*