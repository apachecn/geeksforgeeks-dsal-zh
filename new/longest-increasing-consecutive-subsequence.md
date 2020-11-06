# 最长的连续子序列

> 原文：[https://www.geeksforgeeks.org/longest-increasing-consecutive-subsequence/](https://www.geeksforgeeks.org/longest-increasing-consecutive-subsequence/)

给定`N`个元素，编写一个程序，打印出相邻元素之差为 1 的最长递增子序列的长度。

**示例**：

> 输入：`a[] = {3, 10, 3, 11, 4, 5, 6, 7, 8, 12}`
>
> 输出：6
>
> 说明：3、4、5、6、7、8 为最长的递增子序列，其相邻元素相差一。
>
> 输入：`a[] = {6, 7, 8, 3, 4, 5, 9, 10}`
>
> 输出：5
>
> 说明：6，7，8，9，10 是最长的递增子序列

**朴素的方法**：一种正常的方法是对每个元素进行迭代并找出最长的递增子序列。 对于任何特定元素，请找到从该元素开始的子序列的长度。 打印由此形成的子序列的最长长度。 该方法的时间复杂度将为`O(N ^ 2)`。

**动态规划方法**：让`DP[i]`存储以`A[i]`结尾的最长子序列的长度。 对于每个`A[i]`，如果在第`i`个索引之前的数组中存在`A[i] - 1`，则`A[i]`将添加到具有`A[i] - 1`的递增子序列中。 因此，`DP [i] = DP[index(A[i] - 1)] + 1`。 如果在第`i`个索引之前的数组中不存在`A[i] - 1`，则`DP[i] = 1`，因为`A[i]`元素形成了一个以`A[i]`开头的子序列。 因此，`DP[i]`的关系为：

> 如果在第`i`个索引之前存在`A[i] - 1`：
> 
> *   `DP[i] = DP[index(A[i] - 1)] + 1`
> 
> 其他：
> 
> *   `DP[i] = 1`

下面是上述方法的说明：

## C++

```cpp

// CPP program to find length of the
// longest increasing subsequence
// whose adjacent element differ by 1
#include <bits/stdc++.h>
using namespace std;

// function that returns the length of the
// longest increasing subsequence
// whose adjacent element differ by 1
int longestSubsequence(int a[], int n)
{
    // stores the index of elements
    unordered_map<int, int> mp;

    // stores the length of the longest
    // subsequence that ends with a[i]
    int dp[n];
    memset(dp, 0, sizeof(dp));

    int maximum = INT_MIN;

    // iterate for all element
    for (int i = 0; i < n; i++) {

        // if a[i]-1 is present before i-th index
        if (mp.find(a[i] - 1) != mp.end()) {

            // last index of a[i]-1
            int lastIndex = mp[a[i] - 1] - 1;

            // relation
            dp[i] = 1 + dp[lastIndex];
        }
        else
            dp[i] = 1;

        // stores the index as 1-index as we need to
        // check for occurrence, hence 0-th index
        // will not be possible to check
        mp[a[i]] = i + 1;

        // stores the longest length
        maximum = max(maximum, dp[i]);
    }

    return maximum;
}

// Driver Code
int main()
{
    int a[] = { 3, 10, 3, 11, 4, 5, 6, 7, 8, 12 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << longestSubsequence(a, n);
    return 0;
}

```

## Java

```java

// Java program to find length of the
// longest increasing subsequence
// whose adjacent element differ by 1

import java.util.*;
class lics {
    static int LongIncrConseqSubseq(int arr[], int n)
    {
        // create hashmap to save latest consequent 
        // number as "key" and its length as "value"
        HashMap<Integer, Integer> map = new HashMap<>();

        // put first element as "key" and its length as "value"
        map.put(arr[0], 1);
        for (int i = 1; i < n; i++) {

            // check if last consequent of arr[i] exist or not
            if (map.containsKey(arr[i] - 1)) {

                // put the updated consequent number 
                // and increment its value(length)
                map.put(arr[i], map.get(arr[i] - 1) + 1);

                // remove the last consequent number
                map.remove(arr[i] - 1);
            }

            // if their is no last consequent of
            // arr[i] then put arr[i]
            else {
                map.put(arr[i], 1);
            }
        }
        return Collections.max(map.values());
    }

    // driver code
    public static void main(String args[])
    {
        // Take input from user
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int arr[] = new int[n];
        for (int i = 0; i < n; i++)
            arr[i] = sc.nextInt();
        System.out.println(LongIncrConseqSubseq(arr, n));
    }
}
// This code is contributed by CrappyDoctor

```

## Python3

```py

# python program to find length of the 
# longest increasing subsequence 
# whose adjacent element differ by 1 

from collections import defaultdict
import sys

# function that returns the length of the 
# longest increasing subsequence 
# whose adjacent element differ by 1 

def longestSubsequence(a, n):
    mp = defaultdict(lambda:0)

    # stores the length of the longest 
    # subsequence that ends with a[i] 
    dp = [0 for i in range(n)]
    maximum = -sys.maxsize

    # iterate for all element 
    for i in range(n):

        # if a[i]-1 is present before i-th index 
        if a[i] - 1 in mp:

            # last index of a[i]-1 
            lastIndex = mp[a[i] - 1] - 1

            # relation 
            dp[i] = 1 + dp[lastIndex]
        else:
            dp[i] = 1

            # stores the index as 1-index as we need to 
            # check for occurrence, hence 0-th index 
            # will not be possible to check 
        mp[a[i]] = i + 1

        # stores the longest length 
        maximum = max(maximum, dp[i])
    return maximum

# Driver Code 
a = [3, 10, 3, 11, 4, 5, 6, 7, 8, 12]
n = len(a)
print(longestSubsequence(a, n))

# This code is contributed by Shrikant13

```

## C#

```cs

// C# program to find length of the
// longest increasing subsequence
// whose adjacent element differ by 1
using System;
using System.Collections.Generic;
class GFG{

static int longIncrConseqSubseq(int []arr, 
                                int n)
{
  // Create hashmap to save 
  // latest consequent number 
  // as "key" and its length 
  // as "value"
  Dictionary<int, 
             int> map = new Dictionary<int, 
                                       int>();

  // Put first element as "key" 
  // and its length as "value"
  map.Add(arr[0], 1);
  for (int i = 1; i < n; i++) 
  {
    // Check if last consequent 
    // of arr[i] exist or not
    if (map.ContainsKey(arr[i] - 1)) 
    {
      // put the updated consequent number 
      // and increment its value(length)
      map.Add(arr[i], map[arr[i] - 1] + 1);

      // Remove the last consequent number
      map.Remove(arr[i] - 1);
    }

    // If their is no last consequent of
    // arr[i] then put arr[i]
    else
    {
      if(!map.ContainsKey(arr[i]))
        map.Add(arr[i], 1);
    }
  }

  int max = int.MinValue;
  foreach(KeyValuePair<int, 
                       int> entry in map)
  {
    if(entry.Value > max)
    {
      max = entry.Value;
    }
  }
  return max;
}

// Driver code
public static void Main(String []args)
{
  // Take input from user
  int []arr = {3, 10, 3, 11, 
               4, 5, 6, 7, 8, 12};
  int n = arr.Length;
  Console.WriteLine(longIncrConseqSubseq(arr, n));
}
}

// This code is contributed by gauravrajput1

```

**Output:** 

```
6

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



