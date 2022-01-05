# 根据数组元素中数字 K 的递增频率对数组进行排序

> 原文:[https://www . geesforgeks . org/按数组元素中数字 k 的递增频率对数组进行排序/](https://www.geeksforgeeks.org/sort-an-array-according-to-the-increasing-frequency-of-the-digit-k-in-the-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，以及一个代表一个数字的整数 **K** ，任务是根据数字 **K** 在数组元素中的递增[频率，以递增的顺序打印给定的数组。](https://www.geeksforgeeks.org/find-the-array-element-having-maximum-frequency-of-the-digit-k/)

**示例:**

> **输入:** arr[] = {15，66，26，91}，K = 6
> **输出:** 15 91 26 66
> **说明:**
> 数组元素中数字 6 的出现频率为{0，2，1，0}。{15，91，26，66}中数字 6 的频率递增顺序的元素。
> 
> **输入:** arr[] = {20，21，0}，K = 0
> **输出:** 21 20 0
> **说明:**
> 数组元素中数字 0 出现的频率为{1，0，1}。数字 0 的频率递增顺序是{21，20，0}。

**方法:**思路是[统计数组每个元素的数字 **K**](https://www.geeksforgeeks.org/count-the-occurence-of-digit-k-in-a-given-number-n-using-recursion/) 的出现次数[根据它对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。按照以下步骤解决问题:

*   初始化一个[多重映射](https://www.geeksforgeeks.org/multimap-associative-containers-the-c-standard-template-library-stl/)，比如说 **mp** ，将 **K** 的出现按排序顺序存储在每个元素中。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下操作:
    *   将数字 **K** 在**arr【I】**中的[出现存储在变量 **cnt** 中。](https://www.geeksforgeeks.org/count-the-occurence-of-digit-k-in-a-given-number-n-using-recursion/)
    *   在 **mp** 中插入一对 **cnt** 和**arr【I】**。
*   [打印 **mp**](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) 中的数组元素，得到需要的排序顺序。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the occurrences
// of digit K in an element
int countOccurrences(int num, int K)
{
    // If num and K are both 0
    if (K == 0 && num == 0)
        return 1;

    // Initialize count as 0
    int count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
        if (num % 10 == K)
            count++;
        num /= 10;
    }

    // Return the count
    return count;
}

// Function to print the given array
// in increasing order of the digit
// K in the array elements
void sortOccurrences(int arr[],
                     int N, int K)
{
    // Stores the occurrences of K
    // in each element
    multimap<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Count the frequency
        // of K in arr[i]
        int count = countOccurrences(
            arr[i], K);

        // Insert elements in mp
        mp.insert(pair<int, int>(
            count, arr[i]));
    }

    // Print the elements in the map, mp
    for (auto& itr : mp) {
        cout << itr.second << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 15, 66, 26, 91 };
    int K = 6;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortOccurrences(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to count the occurrences
  // of digit K in an element
  static int countOccurrences(int num, int K)
  {
    // If num and K are both 0
    if (K == 0 && num == 0)
      return 1;

    // Initialize count as 0
    int count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
      if (num % 10 == K)
        count++;
      num /= 10;
    }

    // Return the count
    return count;
  }

  // Pair class
  static class Pair {

    int idx;
    int freq;

    Pair(int idx, int freq)
    {
      this.idx = idx;
      this.freq = freq;
    }
  }

  // Function to print the given array
  // in increasing order of the digit
  // K in the array elements
  static void sortOccurrences(int arr[], int N, int K)
  {

    // Stores the Pair with index
    // and occurrences of K of each element
    Pair mp[] = new Pair[N];

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Count the frequency
      // of K in arr[i]
      int count = countOccurrences(arr[i], K);

      // Insert Pair in mp
      mp[i] = new Pair(i, count);
    }

    // sort the mp in increasing order of freq
    // if freq equal then according to index
    Arrays.sort(mp, (p1, p2) -> {
      if (p1.freq == p2.freq)
        return p1.idx - p2.idx;
      return p1.freq - p2.freq;
    });

    // Print the elements in the map, mp
    for (Pair p : mp) {
      System.out.print(arr[p.idx] + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 15, 66, 26, 91 };
    int K = 6;
    int N = arr.length;

    // Function Call
    sortOccurrences(arr, N, K);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the occurrences
# of digit K in an element
def countOccurrences( num, K):

    # If num and K are both 0
    if (K == 0 and num == 0):
        return 1

    # Initialize count as 0
    count = 0

    # Count for occurrences of digit K
    while (num > 0):
        if (num % 10 == K):
            count += 1
        num //= 10

    # Return the count
    return count

# Function to print the given array
# in increasing order of the digit
# K in the array elements
def sortOccurrences(arr, N, K):

    # Stores the occurrences of K
    # in each element
    mp = []

    # Traverse the array
    for i in range(N):

        # Count the frequency
        # of K in arr[i]
        count = countOccurrences(arr[i], K)

        # Insert elements in mp
        mp.append([count, arr[i]])

    # Print the elements in the map, mp
    mp = sorted(mp)

    for itr in mp:
        print(itr[1], end = ' ')

# Driver Code
arr = [ 15, 66, 26, 91 ]
K = 6
N = len(arr)

# Function Call
sortOccurrences(arr, N, K);

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to count the occurrences
  // of digit K in an element
  static int countOccurrences(int num, int K)
  {
    // If num and K are both 0
    if (K == 0 && num == 0)
      return 1;

    // Initialize count as 0
    int count = 0;

    // Count for occurrences of digit K
    while (num > 0) {
      if (num % 10 == K)
        count++;
      num /= 10;
    }

    // Return the count
    return count;
  }

  // Pair class
  class Pair : IComparable<Pair> {

    public int idx;
    public int freq;

    public Pair(int idx, int freq)
    {
      this.idx = idx;
      this.freq = freq;
    }
      public int CompareTo(Pair p)
      {
          if (this.freq == p.freq)
            return this.idx - p.idx;
          return this.freq - p.freq;

      }
  }

  // Function to print the given array
  // in increasing order of the digit
  // K in the array elements
  static void sortOccurrences(int []arr, int N, int K)
  {

    // Stores the Pair with index
    // and occurrences of K of each element
    Pair []mp = new Pair[N];

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Count the frequency
      // of K in arr[i]
      int count = countOccurrences(arr[i], K);

      // Insert Pair in mp
      mp[i] = new Pair(i, count);
    }

    // sort the mp in increasing order of freq
    // if freq equal then according to index
    Array.Sort(mp);

    // Print the elements in the map, mp
    foreach (Pair p in mp) {
      Console.Write(arr[p.idx] + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    int []arr = { 15, 66, 26, 91 };
    int K = 6;
    int N = arr.Length;

    // Function Call
    sortOccurrences(arr, N, K);
  }
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
15 91 26 66
```

***时间复杂度:**O(N * log<sub>10</sub>N)*
***辅助空间:** O(N)*