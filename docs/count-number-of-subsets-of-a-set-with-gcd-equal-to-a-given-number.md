# 计算 GCD 等于给定数的集合的子集数

> 原文:[https://www . geeksforgeeks . org/count-集合的子集数-gcd-等于给定的数/](https://www.geeksforgeeks.org/count-number-of-subsets-of-a-set-with-gcd-equal-to-a-given-number/)

给定一组正整数元素，求 GCDs 等于给定数的子集数。
**例:**

```
Input:  arr[] = {2, 3, 4}, gcd[] = {2, 3}
Output: Number of subsets with gcd 2 is 2
        Number of subsets with gcd 3 is 1
The two subsets with GCD equal to 2 are {2} and {2, 4}.
The one subset with GCD equal to 3 ss {3}.

Input:  arr[] = {6, 3, 9, 2}, gcd = {3, 2}
Output: Number of subsets with gcd 3 is 5
        Number of subsets with gcd 2 is 2
The five subsets with GCD equal to 3 are {3}, {6, 3}, 
{3, 9}, {6, 9) and {6, 3, 9}.  
The two subsets with GCD equal to 2 are {2} and {2, 6}                
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
一个**简单的解决方案**是生成给定集合的所有子集，并找到每个子集的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。
下面是一个针对小数字的**高效解决方案**，即所有数字的最大值都不是很高。

```
1) Find the maximum number of given numbers.  Let the 
   maximum be arrMax.
2) Count occurrences of all numbers using a hash. Let 
   this hash be 'freq'
3) The maximum possible GCD can be arrMax. Run a loop 
   for i = arrMax to 1
     a) Count number of subsets for current GCD. 
4) Now we have counts for all possible GCDs, return
   count for given gcds. 
```

**步骤 3.a 是如何工作的？**
如何获取给定 GCD‘I’的子集数量，其中 I 位于从 1 到 arrMax 的范围内。想法是使用内置的“freq”步骤 2 计算 I 的所有倍数。假设有 I 的“相加”倍数。所有可能的具有“相加”数的子集的数量将是“幂(2，相加)–1”，不包括空集。例如，如果给定的数组是{2，3，6}并且 i = 3，则有 3 的 2 倍(3 和 6)。因此，将有 3 个子集{3}、{3，6}和{6}的 I 倍数为 GCD。这些子集还包括{6}，它没有 3 作为 GCD，而是 3 的倍数。所以我们需要减去这样的子集。我们将每个 GCD 的子集计数存储在另一个哈希映射“子集”中。假设‘sub’是具有多重‘I’作为 GCD 的子集的数量。“I”的任何倍数的“sub”值可以直接从子集[]获得，因为我们正在评估从 arrMax 到 1 的计数。
以下是上述思路的实现。

## C++

```
// C++ program to count number of subsets with given GCDs
#include<bits/stdc++.h>
using namespace std;

// n is size of arr[] and m is sizeof gcd[]
void ccountSubsets(int arr[], int n, int gcd[], int m)
{
    // Map to store frequency of array elements
    unordered_map<int, int> freq;

    // Map to store number of subsets with given gcd
    unordered_map<int, int> subsets;

    // Initialize maximum element. Assumption: all array
    // elements are positive.
    int arrMax = 0;

    // Find maximum element in array and fill frequency
    // map.
    for (int i=0; i<n; i++)
    {
        arrMax = max(arrMax, arr[i]);
        freq[arr[i]]++;
    }

    // Run a loop from max element to 1 to find subsets
    // with all gcds
    for (int i=arrMax; i>=1; i--)
    {
        int sub = 0;
        int add = freq[i];

        // Run a loop for all multiples of i
        for (int j = 2; j*i <= arrMax; j++)
        {
            // Sum the frequencies of every element which
            // is a multiple of i
            add += freq[j*i];

            // Excluding those subsets which have gcd > i but
            // not i i.e. which have gcd as multiple of i in
            // the subset for ex: {2,3,4} considering i = 2 and
            // subset we need to exclude are those having gcd as 4
            sub += subsets[j*i];
        }

        // Number of subsets with GCD equal to 'i' is pow(2, add)
        // - 1 - sub   
        subsets[i] = (1<<add) - 1 - sub;
    }

    for (int i=0; i<m; i++)
      cout << "Number of subsets with gcd " << gcd[i] << " is "
          << subsets[gcd[i]] << endl;
}

// Driver program
int main()
{
    int gcd[] = {2, 3};
    int arr[] = {9, 6, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = sizeof(gcd)/sizeof(gcd[0]);
    ccountSubsets(arr, n, gcd, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// number of subsets with
// given GCDs
import java.util.*;
class GFG{

// n is size of arr[] and
// m is sizeof gcd[]
static void ccountSubsets(int arr[], int n,
                          int gcd[], int m)
{
  // Map to store frequency
  // of array elements
  HashMap<Integer,
          Integer> freq =
          new HashMap<Integer,
                      Integer>();

  // Map to store number of
  // subsets with given gcd
  HashMap<Integer,
          Integer> subsets =
          new HashMap<Integer,
                      Integer>();

  // Initialize maximum element.
  // Assumption: all array
  // elements are positive.
  int arrMax = 0;

  // Find maximum element in
  // array and fill frequency
  // map.
  for (int i = 0; i < n; i++)
  {
    arrMax = Math.max(arrMax,
                      arr[i]);
    if(freq.containsKey(arr[i]))
    {
      freq.put(arr[i],
      freq.get(arr[i]) + 1);
    }
    else
    {
      freq.put(arr[i], 1);
    }
  }

  // Run a loop from max element
  // to 1 to find subsets
  // with all gcds
  for (int i = arrMax; i >= 1; i--)
  {
    int sub = 0;
    int add = 0;
    if(freq.containsKey(i))
      add = freq.get(i);

    // Run a loop for all multiples
    // of i
    for (int j = 2; j * i <= arrMax; j++)
    {
      // Sum the frequencies of
      // every element which
      // is a multiple of i
      if(freq.containsKey(i * j))
        add += freq.get(j * i);

      // Excluding those subsets
      // which have gcd > i but
      // not i i.e. which have
      // gcd as multiple of i in
      // the subset for ex: {2,3,4}
      // considering i = 2 and
      // subset we need to exclude
      // are those having gcd as 4
      sub += subsets.get(j * i);
    }

    // Number of subsets with GCD
    // equal to 'i' is Math.pow(2, add)
    // - 1 - sub  
    subsets.put(i, (1 << add) -
                1 - sub);
  }

  for (int i = 0; i < m; i++)
    System.out.print("Number of subsets with gcd " + 
                     gcd[i] + " is " +
                     subsets.get(gcd[i]) + "\n");
}

// Driver program
public static void main(String[] args)
{
  int gcd[] = {2, 3};
  int arr[] = {9, 6, 2};
  int n = arr.length;
  int m = gcd.length;
  ccountSubsets(arr, n, gcd, m);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to count number of
# subsets with given GCDs

# n is size of arr[] and m is sizeof gcd[]
def countSubsets(arr, n, gcd, m):

    # Map to store frequency of array elements
    freq = dict()

    # Map to store number of subsets
    # with given gcd
    subsets = dict()

    # Initialize maximum element.
    # Assumption: all array elements
    # are positive.
    arrMax = 0

    # Find maximum element in array and
    # fill frequency map.
    for i in range(n):
        arrMax = max(arrMax, arr[i])
        if arr[i] not in freq:
            freq[arr[i]] = 1
        else:
            freq[arr[i]] += 1

    # Run a loop from max element to 1
    # to find subsets with all gcds
    for i in range(arrMax, 0, -1):
        sub = 0
        add = 0
        if i in freq:
            add = freq[i]
        j = 2

        # Run a loop for all multiples of i
        while j * i <= arrMax:

            # Sum the frequencies of every element
            # which is a multiple of i
            if j * i in freq:
                add += freq[j * i]

            # Excluding those subsets which have
            # gcd > i but not i i.e. which have gcd
            # as multiple of i in the subset.
            # for ex: {2,3,4} considering i = 2 and
            # subset we need to exclude are those
            # having gcd as 4
            sub += subsets[j * i]
            j += 1

        # Number of subsets with GCD equal
        # to 'i' is pow(2, add) - 1 - sub
        subsets[i] = (1 << add) - 1 - sub

    for i in range(m):
        print("Number of subsets with gcd %d is %d" %
             (gcd[i], subsets[gcd[i]]))

# Driver Code
if __name__ == "__main__":
    gcd = [2, 3]
    arr = [9, 6, 2]
    n = len(arr)
    m = len(gcd)
    countSubsets(arr, n, gcd, m)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to count
// number of subsets with
// given GCDs
using System;
using System.Collections.Generic;
class GFG{

// n is size of []arr and
// m is sizeof gcd[]
static void ccountSubsets(int []arr, int n,
                          int []gcd, int m)
{
  // Map to store frequency
  // of array elements
  Dictionary<int,
             int> freq =
             new Dictionary<int,
                            int>();

  // Map to store number of
  // subsets with given gcd
  Dictionary<int,
             int> subsets =
             new Dictionary<int,
                            int>();

  // Initialize maximum element.
  // Assumption: all array
  // elements are positive.
  int arrMax = 0;

  // Find maximum element in
  // array and fill frequency
  // map.
  for (int i = 0; i < n; i++)
  {
    arrMax = Math.Max(arrMax,
                      arr[i]);
    if(freq.ContainsKey(arr[i]))
    {
      freq.Add(arr[i],
      freq[arr[i]] + 1);
    }
    else
    {
      freq.Add(arr[i], 1);
    }
  }

  // Run a loop from max element
  // to 1 to find subsets
  // with all gcds
  for (int i = arrMax; i >= 1; i--)
  {
    int sub = 0;
    int add = 0;
    if(freq.ContainsKey(i))
      add = freq[i];

    // Run a loop for all
    // multiples of i
    for (int j = 2;
             j * i <= arrMax; j++)
    {
      // Sum the frequencies of
      // every element which
      // is a multiple of i
      if(freq.ContainsKey(i * j))
        add += freq[j * i];

      // Excluding those subsets
      // which have gcd > i but
      // not i i.e. which have
      // gcd as multiple of i in
      // the subset for ex: {2,3,4}
      // considering i = 2 and
      // subset we need to exclude
      // are those having gcd as 4
      sub += subsets[j * i];
    }

    // Number of subsets with GCD
    // equal to 'i' is Math.Pow(2, add)
    // - 1 - sub  
    subsets.Add(i, (1 << add) -
                1 - sub);
  }

  for (int i = 0; i < m; i++)
    Console.Write("Number of subsets with gcd " + 
                   gcd[i] + " is " +
                   subsets[gcd[i]] + "\n");
}

// Driver code
public static void Main(String[] args)
{
  int []gcd = {2, 3};
  int []arr = {9, 6, 2};
  int n = arr.Length;
  int m = gcd.Length;
  ccountSubsets(arr, n, gcd, m);
}
}

// This code is contributed by Rajput-Ji
```

**输出:**

```
Number of subsets with gcd 2 is 2
Number of subsets with gcd 3 is 1
```

**练习:**扩展上述解决方案，使所有计算都在模 1000000007 下进行，以避免溢出。

本文由 [**Ekta Goel**](https://www.linkedin.com/pub/ekta-goel/75/12a/3a6) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。