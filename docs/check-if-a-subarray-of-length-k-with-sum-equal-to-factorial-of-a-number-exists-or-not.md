# 检查长度为 K 且和等于一个数的阶乘的子阵列是否存在

> 原文:[https://www . geeksforgeeks . org/check-如果一个长度为 k 的子数组的和等于一个数的阶乘存在与否/](https://www.geeksforgeeks.org/check-if-a-subarray-of-length-k-with-sum-equal-to-factorial-of-a-number-exists-or-not/)

给定一个由 **N** 个整数和一个整数 **K、**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到一个长度为 **K** 的子数组，其元素之和等于任意数[的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)。如果不存在这样的子阵列，打印“**-1”**。

**示例:**

> **输入:** arr[] = {23，45，2，4，6，9，3，32}，K = 5
> **输出:** 2 4 6 9 3
> **解释:**
> Subarray {2，4，6，9，3}带 sum 24 (= 4！)满足要求的条件。
> 
> **输入:** arr[] = {23，45，2，4，6，9，3，32}，K = 3
> **输出:** -1
> **解释:**
> 不存在这样的长度为 K (= 3)的子阵。

**天真方法:**解决问题最简单的方法是计算所有长度子阵列的[和**K**T5】并检查这些和中是否有任何一个是任意数的](https://www.geeksforgeeks.org/sum-of-all-subarrays-of-size-k/)[阶乘](https://www.geeksforgeeks.org/check-if-a-given-number-is-factorial-of-any-number/)。如果发现任何子阵列为真，打印该子阵列。否则，打印**-1”**。

***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，思路是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)计算长度为 K 的所有子阵列的[和](https://www.geeksforgeeks.org/sum-of-all-subarrays-of-size-k/)，然后[检查和是否为阶乘](https://www.geeksforgeeks.org/check-if-a-given-number-is-factorial-of-any-number/)。以下是步骤:

1.  计算第一个 **K** 数组元素的和，并将和存储在一个变量中，比如**和**。
2.  然后[遍历剩余数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并不断更新**和**得到当前大小子阵的和 **K** 通过从前一个子阵中减去第一个元素再加上当前数组元素。
3.  要检查**和**是否是一个数的阶乘，将**和**除以 2、3，以此类推，直到不能再除为止。如果数字减为 1，总和就是数字的阶乘。
4.  如果上面步骤中的和是一个数的阶乘，存储该子阵列的开始和结束索引以打印该子阵列。
5.  完成上述步骤后，如果没有找到这样的子阵列，打印**-1”**。否则，打印存储了开始和结束索引的子阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is factorial of a number or not
int isFactorial(int n)
{
    int i = 2;
    while (n != 1) {

        // If n is not a factorial
        if (n % i != 0) {
            return 0;
        }
        n /= i;
        i++;
    }
    return i - 1;
}

// Function to return the index of
// the valid subarray
pair<int, int> sumFactorial(
    vector<int> arr, int K)
{
    int i, sum = 0, ans;

    // Calculate the sum of
    // first subarray of length K
    for (i = 0; i < K; i++) {

        sum += arr[i];
    }

    // Check if sum is a factorial
    // of any number or not
    ans = isFactorial(sum);

    // If sum of first K length subarray
    // is factorial of a number
    if (ans != 0) {
        return make_pair(ans, 0);
    }

    // Find the number formed from the
    // subarray which is a factorial
    for (int j = i; j < arr.size(); j++) {

        // Update sum of current subarray
        sum += arr[j] - arr[j - K];

        // Check if sum is a factorial
        // of any number or not
        ans = isFactorial(sum);

        // If ans is true, then return
        // index of the current subarray
        if (ans != 0) {
            return make_pair(ans,
                             j - K + 1);
        }
    }

    // If the required subarray is
    // not possible
    return make_pair(-1, 0);
}

// Function to print the subarray whose
// sum is a factorial of any number
void printRes(pair<int, int> answer,
              vector<int> arr, int K)
{

    // If no such subarray exists
    if (answer.first == -1) {

        cout << -1 << endl;
    }

    // Otherwise
    else {

        int i = 0;
        int j = answer.second;

        // Iterate to print subarray
        while (i < K) {

            cout << arr[j] << " ";
            i++;
            j++;
        }
    }
}

// Driver Code
int main()
{
    vector<int> arr
        = { 23, 45, 2, 4,
            6, 9, 3, 32 };

    // Given sum K
    int K = 5;

    // Function Call
    pair<int, int> answer
        = sumFactorial(arr, K);

    // Print the result
    printRes(answer, arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Pair class
public static class Pair
{
    int x;
    int y;

    Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// Function to check if a number
// is factorial of a number or not
static int isFactorial(int n)
{
    int i = 2;
    while (n != 1)
    {

        // If n is not a factorial
        if (n % i != 0)
        {
            return 0;
        }
        n /= i;
        i++;
    }
    return i - 1;
}

// Function to return the index of
// the valid subarray
static ArrayList<Pair> sumFactorial(int arr[],
                                    int K)
{
    ArrayList<Pair> pair = new ArrayList<>();

    int i, sum = 0, ans;

    // Calculate the sum of
    // first subarray of length K
    for(i = 0; i < K; i++)
    {
        sum += arr[i];
    }

    // Check if sum is a factorial
    // of any number or not
    ans = isFactorial(sum);

    // If sum of first K length subarray
    // is factorial of a number
    if (ans != 0)
    {
        Pair p = new Pair(ans, 0);
        pair.add(p);
        return pair;
    }

    // Find the number formed from the
    // subarray which is a factorial
    for(int j = i; j < arr.length; j++)
    {

        // Update sum of current subarray
        sum += arr[j] - arr[j - K];

        // Check if sum is a factorial
        // of any number or not
        ans = isFactorial(sum);

        // If ans is true, then return
        // index of the current subarray
        if (ans != 0)
        {
            Pair p = new Pair(ans, j - K + 1);
            pair.add(p);
            return pair;
        }
    }

    // If the required subarray is
    // not possible
    Pair p = new Pair(-1, 0);
    pair.add(p);
    return pair;
}

// Function to print the subarray whose
// sum is a factorial of any number
static void printRes(ArrayList<Pair> answer,
                     int arr[], int K)
{

    // If no such subarray exists
    if (answer.get(0).x == -1)
    {

        // cout << -1 << endl;
        System.out.println("-1");
    }

    // Otherwise
    else
    {
        int i = 0;
        int j = answer.get(0).y;

        // Iterate to print subarray
        while (i < K)
        {
            System.out.print(arr[j] + " ");
            i++;
            j++;
        }
    }
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[] and brr[]
    int arr[] = { 23, 45, 2, 4,
                  6, 9, 3, 32 };

    int K = 5;
    ArrayList<Pair> answer = new ArrayList<>();

    // Function call
    answer = sumFactorial(arr,K);

    // Print the result
    printRes(answer, arr, K);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a number
# is factorial of a number or not
def isFactorial(n):

    i = 2

    while (n != 1):

        # If n is not a factorial
        if (n % i != 0):
            return 0

        n = n // i
        i += 1

    return i - 1

# Function to return the index of
# the valid subarray
def sumFactorial(arr, K):

    i, Sum = 0, 0

    # Calculate the sum of
    # first subarray of length K
    while(i < K):
        Sum += arr[i]
        i += 1

    # Check if sum is a factorial
    # of any number or not
    ans = isFactorial(Sum)

    # If sum of first K length subarray
    # is factorial of a number
    if (ans != 0):
        return (ans, 0)

    # Find the number formed from the
    # subarray which is a factorial
    for j in range(i, len(arr)):

        # Update sum of current subarray
        Sum = Sum + arr[j] - arr[j - K]

        # Check if sum is a factorial
        # of any number or not
        ans = isFactorial(Sum)

        # If ans is true, then return
        # index of the current subarray
        if (ans != 0):
            return (ans, j - K + 1)

    # If the required subarray is
    # not possible
    return (-1, 0)

# Function to print the subarray whose
# sum is a factorial of any number
def printRes(answer, arr, K):

    # If no such subarray exists
    if (answer[0] == -1):
        print(-1)

    # Otherwise
    else:
        i = 0
        j = answer[1]

        # Iterate to print subarray
        while (i < K):
            print(arr[j], end = " ")
            i += 1
            j += 1

# Driver code
arr = [ 23, 45, 2, 4, 6, 9, 3, 32 ]

# Given sum K
K = 5

# Function call
answer = sumFactorial(arr, K)

# Print the result
printRes(answer, arr, K)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Pair class
public class Pair
{
  public int x;
  public int y;

  public Pair(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
}

// Function to check if a number
// is factorial of a number or not
static int isFactorial(int n)
{
  int i = 2;
  while (n != 1)
  {
    // If n is not
    // a factorial
    if (n % i != 0)
    {
      return 0;
    }
    n /= i;
    i++;
  }
  return i - 1;
}

// Function to return the index of
// the valid subarray
static List<Pair> sumFactorial(int []arr,
                               int K)
{
  List<Pair> pair = new List<Pair>();
  int i, sum = 0, ans;

  // Calculate the sum of
  // first subarray of length K
  for(i = 0; i < K; i++)
  {
    sum += arr[i];
  }

  // Check if sum is a factorial
  // of any number or not
  ans = isFactorial(sum);

  // If sum of first K length subarray
  // is factorial of a number
  if (ans != 0)
  {
    Pair p = new Pair(ans, 0);
    pair.Add(p);
    return pair;
  }

  // Find the number formed from the
  // subarray which is a factorial
  for(int j = i; j < arr.Length; j++)
  {
    // Update sum of current subarray
    sum += arr[j] - arr[j - K];

    // Check if sum is a factorial
    // of any number or not
    ans = isFactorial(sum);

    // If ans is true, then return
    // index of the current subarray
    if (ans != 0)
    {
      Pair p = new Pair(ans, j - K + 1);
      pair.Add(p);
      return pair;
    }
  }

  // If the required subarray is
  // not possible
  Pair p1 = new Pair(-1, 0);
  pair.Add(p1);
  return pair;
}

// Function to print the subarray whose
// sum is a factorial of any number
static void printRes(List<Pair> answer,
                     int []arr, int K)
{
  // If no such subarray exists
  if (answer[0].x == -1)
  {
    // cout << -1 << endl;
    Console.WriteLine("-1");
  }

  // Otherwise
  else
  {
    int i = 0;
    int j = answer[0].y;

    // Iterate to print subarray
    while (i < K)
    {
      Console.Write(arr[j] + " ");
      i++;
      j++;
    }
  }
}

// Driver Code
public static void Main(String []args)
{    
  // Given array []arr and brr[]
  int []arr = {23, 45, 2, 4,
               6, 9, 3, 32};
  int K = 5;
  List<Pair> answer = new List<Pair>();

  // Function call
  answer = sumFactorial(arr, K);

  // Print the result
  printRes(answer, arr, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach
    // Function to check if a number
    // is factorial of a number or not
    function isFactorial(n)
    {
        let i = 2;
        while (n != 1) {

            // If n is not a factorial
            if (n % i != 0) {
                return 0;
            }
            n = parseInt(n / i, 10);
            i++;
        }
        return i - 1;
    }

    // Function to return the index of
    // the valid subarray
    function sumFactorial(arr,K)
    {
        let i, sum = 0, ans;

        // Calculate the sum of
        // first subarray of length K
        for (i = 0; i < K; i++) {

            sum += arr[i];
        }

        // Check if sum is a factorial
        // of any number or not
        ans = isFactorial(sum);

        // If sum of first K length subarray
        // is factorial of a number
        if (ans != 0) {
            return [ans, 0];
        }

        // Find the number formed from the
        // subarray which is a factorial
        for (let j = i; j < arr.length; j++) {

            // Update sum of current subarray
            sum += arr[j] - arr[j - K];

            // Check if sum is a factorial
            // of any number or not
            ans = isFactorial(sum);

            // If ans is true, then return
            // index of the current subarray
            if (ans != 0) {
                return [ans, j - K + 1];
            }
        }

        // If the required subarray is
        // not possible
        return [-1, 0];
    }

    // Function to print the subarray whose
    // sum is a factorial of any number
    function printRes(answer,arr,K)
    {

        // If no such subarray exists
        if (answer[0] == -1) {

            document.write(-1);
        }

        // Otherwise
        else {

            let i = 0;
            let j = answer[1];

            // Iterate to print subarray
            while (i < K) {

                document.write(arr[j] + " ");
                i++;
                j++;
            }
        }
    }

    // Driver Code

    let arr= [ 23, 45, 2, 4,
            6, 9, 3, 32 ];

    // Given sum K
    let K = 5;

    // Function Call
    let answer= sumFactorial(arr, K);

    // Print the result
    printRes(answer, arr, K);

</script>
```

**Output:** 

```
2 4 6 9 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)