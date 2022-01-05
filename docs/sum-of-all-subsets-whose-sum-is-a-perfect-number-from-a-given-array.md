# 给定数组中其和为完全数的所有子集的和

> 原文:[https://www . geeksforgeeks . org/所有子集的和-其和是给定数组的完全数/](https://www.geeksforgeeks.org/sum-of-all-subsets-whose-sum-is-a-perfect-number-from-a-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是从一个数组中找出所有子集的[和，其和是一个](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)[完全数](https://www.geeksforgeeks.org/perfect-number/)。

**示例:**

> **输入:** arr[] = {5，4，6}
> **输出:** 6
> **解释:**
> 数组 arr[]中所有可能的子集为:
> {5} → Sum = 5
> {4} → Sum = 4。
> {6} → Sum = 6。
> {5，4} → Sum = 9。
> {5，6} → Sum = 11。
> {4，6} → Sum = 10。
> {5，4，6} → Sum = 15。
> 在所有子集和中，只有 6 个和被发现是 2 `一个完全数。
> 
> **输入:** arr[] = {28，6，23，3，3 }
> T3】输出: 28 6 6

[**【递归】**](https://www.geeksforgeeks.org/recursion/) **方法:**思想是[从给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)生成所有可能的子集，并打印那些子集的和为[完全数](https://www.geeksforgeeks.org/perfect-number/)的和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check is a given number
// is a  perfect number or not
int isPerfect(int x)
{
    // Stores the sum of its divisors
    int sum_div = 1;

    // Add all divisors of x to sum_div
    for (int i = 2; i <= x / 2; ++i) {
        if (x % i == 0) {
            sum_div += i;
        }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x) {
        return 1;
    }

    // Otherwise, return false
    else
        return 0;
}

// Function to find sum of all
// subsets from an array whose
// sum is a perfect number
void subsetSum(int arr[], int l,
               int r, int sum = 0)
{
    // Print the current subset sum
    // if it is a perfect number
    if (l > r) {

        // Check if sum is a
        // perfect number or not
        if (isPerfect(sum)) {
            cout << sum << " ";
        }
        return;
    }

    // Calculate sum of the subset
    // including arr[l]
    subsetSum(arr, l + 1, r, sum + arr[l]);

    // Calculate sum of the subset
    // excluding arr[l]
    subsetSum(arr, l + 1, r, sum);
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    subsetSum(arr, 0, N - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check is a given number
// is a  perfect number or not
static int isPerfect(int x)
{

    // Stores the sum of its divisors
    int sum_div = 1;

    // Add all divisors of x to sum_div
    for(int i = 2; i <= x / 2; ++i)
    {
        if (x % i == 0)
        {
            sum_div += i;
        }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x)
    {
        return 1;
    }

    // Otherwise, return false
    else
        return 0;
}

// Function to find sum of all
// subsets from an array whose
// sum is a perfect number
static void subsetSum(int[] arr, int l,
                      int r, int sum)
{

    // Print the current subset sum
    // if it is a perfect number
    if (l > r)
    {

        // Check if sum is a
        // perfect number or not
        if (isPerfect(sum) != 0)
        {
            System.out.print(sum + " ");
        }
        return;
    }

    // Calculate sum of the subset
    // including arr[l]
    subsetSum(arr, l + 1, r, sum + arr[l]);

    // Calculate sum of the subset
    // excluding arr[l]
    subsetSum(arr, l + 1, r, sum);
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 5, 4, 6 };
    int N = arr.length;

    subsetSum(arr, 0, N - 1, 0);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check is a given number
# is a  perfect number or not
def isPerfect(x) :

    # Stores the sum of its divisors
    sum_div = 1

    # Add all divisors of x to sum_div
    for i in range(2, (x // 2) + 1) :
        if (x % i == 0) :
            sum_div += i

    # If the sum of divisors is equal
    # to the given number, return true
    if (sum_div == x) :
        return 1

    # Otherwise, return false
    else :
        return 0

# Function to find sum of all
# subsets from an array whose
# sum is a perfect number
def subsetSum(arr, l,
               r, sum) :

    # Print current subset sum
    # if it is a perfect number
    if (l > r) :

        # Check if sum is a
        # perfect number or not
        if (isPerfect(sum) != 0) :
            print(sum, end = " ")

        return

    # Calculate sum of the subset
    # including arr[l]
    subsetSum(arr, l + 1, r, sum + arr[l])

    # Calculate sum of the subset
    # excluding arr[l]
    subsetSum(arr, l + 1, r, sum)

# Driver Code
arr = [ 5, 4, 6 ]
N = len(arr)
subsetSum(arr, 0, N - 1, 0)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check is a given number
// is a  perfect number or not
static int isPerfect(int x)
{

    // Stores the sum of its divisors
    int sum_div = 1;

    // Add all divisors of x to sum_div
    for(int i = 2; i <= x / 2; ++i)
    {
        if (x % i == 0)
        {
            sum_div += i;
        }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x)
    {
        return 1;
    }

    // Otherwise, return false
    else
        return 0;
}

// Function to find sum of all
// subsets from an array whose
// sum is a perfect number
static void subsetSum(int[] arr, int l,
                      int r, int sum = 0)
{

    // Print the current subset sum
    // if it is a perfect number
    if (l > r)
    {

        // Check if sum is a
        // perfect number or not
        if (isPerfect(sum) != 0)
        {
            Console.Write(sum + " ");
        }
        return;
    }

    // Calculate sum of the subset
    // including arr[l]
    subsetSum(arr, l + 1, r, sum + arr[l]);

    // Calculate sum of the subset
    // excluding arr[l]
    subsetSum(arr, l + 1, r, sum);
}

// Driver code
static void Main()
{
    int[] arr = { 5, 4, 6 };
    int N = arr.Length;
    subsetSum(arr, 0, N - 1);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to check is a given number
    // is a perfect number or not
    function isPerfect(x) {

        // Stores the sum of its divisors
        var sum_div = 1;

        // Add all divisors of x to sum_div
        for (i = 2; i <= x / 2; ++i) {
            if (x % i == 0) {
                sum_div += i;
            }
        }

        // If the sum of divisors is equal
        // to the given number, return true
        if (sum_div == x) {
            return 1;
        }

        // Otherwise, return false
        else
            return 0;
    }

    // Function to find sum of all
    // subsets from an array whose
    // sum is a perfect number
    function subsetSum(arr , l , r , sum) {

        // Print the current subset sum
        // if it is a perfect number
        if (l > r) {

            // Check if sum is a
            // perfect number or not
            if (isPerfect(sum) != 0) {
                document.write(sum + " ");
            }
            return;
        }

        // Calculate sum of the subset
        // including arr[l]
        subsetSum(arr, l + 1, r, sum + arr[l]);

        // Calculate sum of the subset
        // excluding arr[l]
        subsetSum(arr, l + 1, r, sum);
    }

    // Driver code

        var arr = [ 5, 4, 6 ];
        var N = arr.length;

        subsetSum(arr, 0, N - 1, 0);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(M * 2 <sup>N</sup> ，其中 **M** 是数组* [*元素的和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)***arr【】***
***辅助空间:** O(1)*

**迭代方法:**由于从一个大小为 **N** 的数组中有**2<sup>N</sup>T5】个可能的子集，其思想是[迭代一个从 **0** 到**2<sup>N</sup>–1**](https://www.geeksforgeeks.org/range-based-loop-c/)的循环，对于每个数字，在当前数字的[二进制表示中选择对应于 **1** s 的所有数组元素，然后【T0 按照以下步骤解决问题:](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)**

*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，2<sup>N</sup>–1】**中迭代，并执行以下步骤:
    *   初始化一个变量，用 **0** 表示 **S** 来存储当前子集的和。
    *   [使用变量 **j** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
        *   如果在 **i** 的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中设置了 **j <sup>th</sup>** 位置，则将**arr【j】**的值加到 **S** 上。
    *   检查 **S** 是否为完全数，如果发现为**真**则打印 **S** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check is a given
// number is a perfect number or not
int isPerfect(int x)
{
    // Stores sum of divisors
    int sum_div = 1;

    // Add all divisors of x to sum_div
    for (int i = 2; i <= x / 2; ++i) {
        if (x % i == 0) {
            sum_div += i;
        }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x) {
        return 1;
    }

    // Otherwise, return false
    else
        return 0;
}

// Function to find the sum of all the
// subsets from an array whose sum is
// a perfect number
void subsetSum(int arr[], int n)
{
    // Stores the total number of
    // subsets, i.e. 2 ^ n
    long long total = 1 << n;

    // Consider all numbers from 0 to 2 ^ n - 1
    for (long long i = 0; i < total; i++) {
        long long sum = 0;

        // Consider array elements from
        // positions of set bits in the
        // binary representation of n
        for (int j = 0; j < n; j++)
            if (i & (1 << j))
                sum += arr[j];

        // If sum of chosen elements
        // is a perfect number
        if (isPerfect(sum)) {
            cout << sum << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    subsetSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to check is a given
  // number is a perfect number or not
  static int isPerfect(int x)
  {

    // Stores sum of divisors
    int sum_div = 1;

    // Add all divisors of x to sum_div
    for (int i = 2; i <= x / 2; ++i) {
      if (x % i == 0) {
        sum_div += i;
      }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x) {
      return 1;
    }

    // Otherwise, return false
    else
      return 0;
  }

  // Function to find the sum of all the
  // subsets from an array whose sum is
  // a perfect number
  static void subsetSum(int arr[], int n)
  {

    // Stores the total number of
    // subsets, i.e. 2 ^ n
    long total = 1 << n;

    // Consider all numbers from 0 to 2 ^ n - 1
    for (long i = 0; i < total; i++) {
      int sum = 0;

      // Consider array elements from
      // positions of set bits in the
      // binary representation of n
      for (int j = 0; j < n; j++)
        if ((i & (1 << j)) != 0)
          sum += arr[j];

      // If sum of chosen elements
      // is a perfect number
      if (isPerfect(sum) != 0) {
        System.out.print(sum + " ");
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 5, 4, 6 };
    int N = arr.length;
    subsetSum(arr, N);
  }
}

// This code is contributed by souravghosh0416.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check is a given
# number is a perfect number or not
def isPerfect(x):

    # Stores sum of divisors
    sum_div = 1

    # Add all divisors of x to sum_div
    for i in range(2, int(x/2 + 1)):
        if (x % i == 0):
            sum_div = sum_div + i

    # If the sum of divisors is equal
    # to the given number, return true
    if (sum_div == x):
        return 1

    # Otherwise, return false
    else:
        return 0

# Function to find the sum of all the
# subsets from an array whose sum is
# a perfect number
def subsetSum(arr, n):

    # Stores the total number of
    # subsets, i.e. 2 ^ n
    total = 1 << n

    # Consider all numbers from 0 to 2 ^ n - 1
    for i in range(total):
        sum = 0

        # Consider array elements from
        # positions of set bits in the
        # binary representation of n
        for j in range(n):
            if (i & (1 << j) != 0):
                sum = sum + arr[j]

        # If sum of chosen elements
        # is a perfect number
        if (isPerfect(sum)):
            print(sum, " ")

# Driver Code
arr = [5, 4, 6]
N = len(arr)

subsetSum(arr, N)

# This code is contributed by Dharanendra L V.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  // Function to check is a given
  // number is a perfect number or not
  static int isPerfect(int x)
  {

    // Stores sum of divisors
    int sum_div = 1;

    // Add all divisors of x to sum_div
    for (int i = 2; i <= x / 2; ++i) {
      if (x % i == 0) {
        sum_div += i;
      }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x) {
      return 1;
    }

    // Otherwise, return false
    else
      return 0;
  }

  // Function to find the sum of all the
  // subsets from an array whose sum is
  // a perfect number
  static void subsetSum(int[] arr, int n)
  {

    // Stores the total number of
    // subsets, i.e. 2 ^ n
    long total = 1 << n;

    // Consider all numbers from 0 to 2 ^ n - 1
    for (long i = 0; i < total; i++) {
      int sum = 0;

      // Consider array elements from
      // positions of set bits in the
      // binary representation of n
      for (int j = 0; j < n; j++)
        if ((i & (1 << j)) != 0)
          sum += arr[j];

      // If sum of chosen elements
      // is a perfect number
      if (isPerfect(sum) != 0) {
        Console.Write(sum + " ");
      }
    }
  }

// Driver Code
static public void Main()
{
    int[] arr = { 5, 4, 6 };
    int N = arr.Length;
    subsetSum(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
// javascript program for the above approach

 // Function to check is a given
  // number is a perfect number or not
  function isPerfect(x)
  {

    // Stores sum of divisors
    var sum_div = 1;

    // Add all divisors of x to sum_div
    for (var i = 2; i <= parseInt(x / 2); ++i) {
      if (x % i == 0) {
        sum_div += i;
      }
    }

    // If the sum of divisors is equal
    // to the given number, return true
    if (sum_div == x) {
      return 1;
    }

    // Otherwise, return false
    else
      return 0;
  }

  // Function to find the sum of all the
  // subsets from an array whose sum is
  // a perfect number
  function subsetSum(arr , n)
  {

    // Stores the total number of
    // subsets, i.e. 2 ^ n
    var total = 1 << n;

    // Consider all numbers from 0 to 2 ^ n - 1
    for (i = 0; i < total; i++) {
      var sum = 0;

      // Consider array elements from
      // positions of set bits in the
      // binary representation of n
      for (j = 0; j < n; j++)
        if ((i & (1 << j)) != 0)
          sum += arr[j];

      // If sum of chosen elements
      // is a perfect number
      if (isPerfect(sum) != 0) {
        document.write(sum + " ");
      }
    }
  }

  // Driver Code
  var arr = [ 5, 4, 6 ];
  var N = arr.length;
  subsetSum(arr, N);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O((N + M) * 2 <sup>N</sup> ，其中 **M** 是数组* [*元素的和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) *，**arr【】***
***辅助空间:** O(1)*