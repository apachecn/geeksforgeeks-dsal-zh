# 两个给定数组中最长公共素子序列的长度

> 原文:[https://www . geeksforgeeks . org/两个给定数组中最长公共素子序列的长度/](https://www.geeksforgeeks.org/length-of-longest-common-prime-subsequence-from-two-given-arrays/)

给定两个长度分别为 **N** 和 **M** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和 **arr2[]** ，任务是从两个给定数组中找出**最长公共素数** [**子序列**](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) 的长度。

**示例:**

> **输入:** arr1[] = {1，2，3，4，5，6，7，8，9}，arr2[] = {2，5，6，3，7，9，8}
> **输出:** 4
> **解释:**
> 两个数组中最长的公共素子序列是{2，3，5，7}。
> 
> **输入:** arr1[] = {1，3，5，7，9}，arr2[] = {2，4，6，8，10}
> **输出:** 0
> **说明:**
> 在上述数组中，arr1[]的素子序列为{1，3，5，7}，arr2[]为{2}。因此，两个数组中不存在公共素数。因此，结果是 0。

**天真的做法:**最简单的想法是考虑**arr 1【】**的所有子序列，检查这个子序列中的所有数字是否都是质数并且出现在**arr 2【】**中。然后找出这些子序列的最长长度。

**时间复杂度:**O(M * 2<sup>N</sup>)
T5】辅助空间: O(N)

**有效方法:**想法是从两个数组中找到所有素数，然后使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)从它们中找到最长的公共素数子序列。按照以下步骤解决问题:

1.  使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)算法找出数组最小元素和数组最大元素之间的所有[素数](https://www.geeksforgeeks.org/prime-numbers/)。
2.  存储数组 **arr1[]** 和 **arr2[]** 中的素数序列。
3.  找到两个素数序列的 [LCS](https://www.geeksforgeeks.org/longest-common-subsequence/) 。

下面是上述方法的实现:

## C++

```
// CPP implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the LCS
int recursion(vector<int> arr1,
              vector<int> arr2, int i,
              int j, map<pair<int, int>,
              int> dp)
{
    if (i >= arr1.size() or j >= arr2.size())
        return 0;
    pair<int, int> key = { i, j };
    if (arr1[i] == arr2[j])
        return 1
               + recursion(arr1, arr2,
                            i + 1, j + 1,
                           dp);
    if (dp.find(key) != dp.end())
        return dp[key];

    else
        dp[key] = max(recursion(arr1, arr2,
                                i + 1, j, dp),
                      recursion(arr1, arr2, i,
                                j + 1, dp));
    return dp[key];
}

// Function to generate
// all the possible
// prime numbers
vector<int> primegenerator(int n)
{
    int cnt = 0;
    vector<int> primes(n + 1, true);
    int p = 2;
    while (p * p <= n)
    {
        for (int i = p * p; i <= n; i += p)
            primes[i] = false;
        p += 1;
    }
    return primes;
}

// Function which returns the
// length of longest common
// prime subsequence
int longestCommonSubseq(vector<int> arr1,
                        vector<int> arr2)
{

    // Minimum element of
    // both arrays
    int min1 = *min_element(arr1.begin(),
                            arr1.end());
    int min2 = *min_element(arr2.begin(),
                            arr2.end());

    // Maximum element of
    // both arrays
    int max1 = *max_element(arr1.begin(),
                            arr1.end());
    int max2 = *max_element(arr2.begin(),
                            arr2.end());

    // Generating all primes within
    // the max range of arr1
    vector<int> a = primegenerator(max1);

    // Generating all primes within
    // the max range of arr2
    vector<int> b = primegenerator(max2);

    vector<int> finala;
    vector<int> finalb;

    // Store precomputed values
    map<pair<int, int>, int> dp;

    // Store all primes in arr1[]
    for (int i = min1; i <= max1; i++)
    {
        if (find(arr1.begin(), arr1.end(), i)
            != arr1.end()
            and a[i] == true)
            finala.push_back(i);
    }

    // Store all primes of arr2[]
    for (int i = min2; i <= max2; i++)
    {
        if (find(arr2.begin(), arr2.end(), i)
            != arr2.end()
            and b[i] == true)
            finalb.push_back(i);
    }

    // Calculating the LCS
    return recursion(finala, finalb, 0, 0, dp);
}

// Driver Code
int main()
{
    vector<int> arr1 = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    vector<int> arr2 = { 2, 5, 6, 3, 7, 9, 8 };

    // Function Call
    cout << longestCommonSubseq(arr1, arr2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of the above approach
import java.util.*;
import java.io.*;
import java.math.*;
public class GFG
{

  // Function to calculate the LCS
  static int recursion(ArrayList<Integer> arr1,
                       ArrayList<Integer> arr2, int i,
                       int j, Map<ArrayList<Integer>,
                       Integer> dp)
  {
    if (i >= arr1.size() || j >= arr2.size())
      return 0;
    ArrayList<Integer> key = new ArrayList<>();
    key.add(i);
    key.add(j);
    if (arr1.get(i) == arr2.get(j))
      return 1 + recursion(arr1, arr2,
                           i + 1, j + 1,
                           dp);
    if (dp.get(key) != dp.get(dp.size()-1))
      return dp.get(key);

    else
      dp.put(key,Math.max(recursion(arr1, arr2,
                                    i + 1, j, dp),
                          recursion(arr1, arr2, i,
                                    j + 1, dp)));
    return dp.get(key);
  }

  // Function to generate
  // all the possible
  // prime numbers
  static ArrayList<Boolean> primegenerator(int n)
  {
    int cnt = 0;
    ArrayList<Boolean> primes = new ArrayList<>();
    for(int i = 0; i < n + 1; i++)
      primes.add(true);
    int p = 2;
    while (p * p <= n)
    {
      for (int i = p * p; i <= n; i += p)
        primes.set(i,false);
      p += 1;
    }
    return primes;
  }

  // Function that returns the Minimum element of an ArrayList
  static int min_element(ArrayList<Integer> al)
  {
    int min = Integer.MAX_VALUE;
    for(int i = 0; i < al.size(); i++)
    {
      min=Math.min(min, al.get(i));
    }
    return min;
  }

  // Function that returns the Minimum element of an ArrayList
  static int max_element(ArrayList<Integer> al)
  {
    int max = Integer.MIN_VALUE;
    for(int i = 0; i < al.size(); i++)
    {
      max = Math.max(max, al.get(i));
    }
    return max;
  }

  // Function which returns the
  // length of longest common
  // prime subsequence
  static int longestCommonSubseq(ArrayList<Integer> arr1,
                                 ArrayList<Integer> arr2)
  {

    // Minimum element of
    // both arrays
    int min1 = min_element(arr1);
    int min2 = min_element(arr2);

    // Maximum element of
    // both arrays
    int max1 = max_element(arr1);
    int max2 = max_element(arr2);

    // Generating all primes within
    // the max range of arr1
    ArrayList<Boolean> a = primegenerator(max1);

    // Generating all primes within
    // the max range of arr2
    ArrayList<Boolean> b = primegenerator(max2);
    ArrayList<Integer> finala = new ArrayList<>();
    ArrayList<Integer> finalb = new ArrayList<>();

    // Store precomputed values
    Map<ArrayList<Integer>,Integer> dp =
      new HashMap <ArrayList<Integer>,Integer> ();

    // Store all primes in arr1[]
    for (int i = min1; i <= max1; i++)
    {
      if (arr1.contains(i)
          && a.get(i) == true)
        finala.add(i);
    }

    // Store all primes of arr2[]
    for (int i = min2; i <= max2; i++)
    {
      if (arr2.contains(i)
          && b.get(i) == true)
        finalb.add(i);
    }

    // Calculating the LCS
    return recursion(finala, finalb, 0, 0, dp);
  }

  // Driver Code
  public static void main(String args[])
  {
    int a1[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int a2[] = { 2, 5, 6, 3, 7, 9, 8 };

    // Converting into list
    ArrayList<Integer> arr1 = new ArrayList<Integer>();
    for(int i = 0; i < a1.length; i++)
      arr1.add(a1[i]);

    ArrayList<Integer> arr2 = new ArrayList<Integer>();
    for(int i = 0; i < a2.length; i++)
      arr2.add(a2[i]);

    // Function Call
    System.out.println(longestCommonSubseq(arr1, arr2));
  }
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to calculate the LCS

def recursion(arr1, arr2, i, j, dp):
    if i >= len(arr1) or j >= len(arr2):
        return 0
    key = (i, j)
    if arr1[i] == arr2[j]:
        return 1 + recursion(arr1, arr2,
                             i + 1, j + 1, dp)
    if key in dp:
        return dp[key]
    else:
        dp[key] = max(recursion(arr1, arr2,
                                i + 1, j, dp),
                      recursion(arr1, arr2,
                                i, j + 1, dp))
    return dp[key]

# Function to generate
# all the possible
# prime numbers

def primegenerator(n):
    cnt = 0
    primes = [True for _ in range(n + 1)]
    p = 2
    while p * p <= n:
        for i in range(p * p, n + 1, p):
            primes[i] = False
        p += 1
    return primes

# Function which returns the
# length of longest common
# prime subsequence

def longestCommonSubseq(arr1, arr2):

    # Minimum element of
    # both arrays
    min1 = min(arr1)
    min2 = min(arr2)

    # Maximum element of
    # both arrays
    max1 = max(arr1)
    max2 = max(arr2)

    # Generating all primes within
    # the max range of arr1
    a = primegenerator(max1)

    # Generating all primes within
    # the max range of arr2
    b = primegenerator(max2)

    finala = []
    finalb = []

    # Store precomputed values
    dp = dict()

    # Store all primes in arr1[]
    for i in range(min1, max1 + 1):
        if i in arr1 and a[i] == True:
            finala.append(i)

    # Store all primes of arr2[]
    for i in range(min2, max2 + 1):
        if i in arr2 and b[i] == True:
            finalb.append(i)

    # Calculating the LCS
    return recursion(finala, finalb,
                     0, 0, dp)

# Driver Code
arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9]
arr2 = [2, 5, 6, 3, 7, 9, 8]

# Function Call
print(longestCommonSubseq(arr1, arr2))
```

**Output**

```
4
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N * M)