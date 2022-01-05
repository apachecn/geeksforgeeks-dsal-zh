# 给定数组中数字 K 的计数频率

> 原文:[https://www . geesforgeks . org/count-给定数组中数字 k 的频率/](https://www.geeksforgeeks.org/count-frequency-of-digit-k-in-given-array/)

给定一个大小为 **N** 的整数的 [**数组**](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个单个数字的整数**K。**任务是找出数组中数字 K 出现的**总数**

**示例:**

> **输入:** arr[] = {15，66，26，91}，K = 6
> **输出:** 3
> **说明:**每个数组元素中 6 的出现次数分别为:0，2，1，0。
> 因此，总出现次数= 0 + 2 + 1 + 0 = 3
> 
> **输入:** arr[] = {20，21，0}，K = 0
> T3】输出: 2

**方法:**想法是遍历数组，对于每个单独的数组元素，计算其中数字 K 的出现次数，并更新总计数。按照以下步骤解决问题:

1.  初始化数字 K 的总出现次数，比如**计数**，为 0。
2.  从**起点**元素**到终点**遍历给定数组。
3.  对于**每个遍历的元素**，找到该元素中数字 **K** 的**频率**。
4.  **将**计数加到**总和**中。
5.  返回总和作为答案。

下面是上述方法的实现:

## C++

```
// C++ code to count frequency
// of digit K in given Array

#include <bits/stdc++.h>
using namespace std;

// Function to count occurrences
// in an element
int countOccurrences(int num, int K)
{
    // If num is 0
    if (K == 0 && num == 0)
        return 1;

    // Initialize count
    int count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
        if (num % 10 == K)
            count++;
        num /= 10;
    }
    return count;
}

// Function to return sum of
// total occurrences of digit K
int totalOccurrences(int arr[], int N, int K)
{

    // Initialize sum
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        sum += countOccurrences(arr[i], K);
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 15, 66, 26, 91 };
    int K = 6;

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << totalOccurrences(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

  // Function to count occurrences
  // in an element
  static int countOccurrences(int num, int K)
  {

    // If num is 0
    if (K == 0 && num == 0)
      return 1;

    // Initialize count
    int count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
      if (num % 10 == K)
        count++;
      num /= 10;
    }
    return count;
  }

  // Function to return sum of
  // total occurrences of digit K
  static int totalOccurrences(int arr[], int N, int K)
  {

    // Initialize sum
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
      sum += countOccurrences(arr[i], K);
    }

    return sum;
  }

  // Driver Code
  public static void main (String[] args)
  {

    int arr[] = { 15, 66, 26, 91 };
    int K = 6;
    int N = arr.length;
    System.out.println( totalOccurrences(arr, N, K));
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 code to count frequency
# of digit K in given array

# Function to count occurrences
# in an element
def countOccurrences(num, K):

    # If num is 0
    if (K == 0 and num == 0):
        return 1

    # Initialize count
    count = 0

    # Count for occurrences of digit K
    while (num > 0):
        if (num % 10 == K):
            count += 1

        num = (num // 10)

    return count

# Function to return sum of
# total occurrences of digit K
def totalOccurrences(arr, N, K):

    # Initialize sum
    sum = 0

    # Traverse the array
    for i in range(N):
        sum += countOccurrences(arr[i], K)

    return sum

# Driver Code
arr = [ 15, 66, 26, 91 ]
K = 6

N = len(arr)

print(totalOccurrences(arr, N, K))

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to count occurrences
  // in an element
  static int countOccurrences(int num, int K)
  {

    // If num is 0
    if (K == 0 && num == 0)
      return 1;

    // Initialize count
    int count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
      if (num % 10 == K)
        count++;
      num /= 10;
    }
    return count;
  }

  // Function to return sum of
  // total occurrences of digit K
  static int totalOccurrences(int []arr, int N, int K)
  {

    // Initialize sum
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
      sum += countOccurrences(arr[i], K);
    }

    return sum;
  }

  // Driver Code
  public static void Main ()
  {

    int []arr = { 15, 66, 26, 91 };
    int K = 6;
    int N = arr.Length;
    Console.Write( totalOccurrences(arr, N, K));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// Javascript code to count frequency
// of digit K in given Array

// Function to count occurrences
// in an element
function countOccurrences(num, K)
{

    // If num is 0
    if (K == 0 && num == 0)
        return 1;

    // Initialize count
    let count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
        if (num % 10 == K)
            count++;
        num = Math.floor(num / 10);
    }
    return count;
}

// Function to return sum of
// total occurrences of digit K
function totalOccurrences(arr, N, K) {

    // Initialize sum
    let sum = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {
        sum += countOccurrences(arr[i], K);
    }

    return sum;
}

// Driver Code
let arr = [15, 66, 26, 91];
let K = 6;

let N = arr.length
document.write(totalOccurrences(arr, N, K));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
3
```

**时间复杂度:** O(N*D)其中 D 是数组元素中最大位数
T3】辅助空间: O(1)