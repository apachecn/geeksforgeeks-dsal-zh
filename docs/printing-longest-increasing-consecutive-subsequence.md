# 打印最长的递增连续子序列

> 原文:[https://www . geesforgeks . org/printing-最长-递增-连续-子序列/](https://www.geeksforgeeks.org/printing-longest-increasing-consecutive-subsequence/)

给定 n 个元素，编写一个程序，打印相邻元素差为 1 的最长递增子序列。
**例:**

> 输入:a[] = {3，10，3，11，4，5，6，7，8，12}
> 输出:3 4 5 6 7 8
> 说明:3，4，5，6，7，8 是相邻元素相差 1 的最长递增子序列。
> 输入:a[] = {6，7，8，3，4，5，9，10}
> 输出:6 7 8 9 10
> 说明:6，7，8，9，10 是最长的递增子序列

我们已经讨论了[如何找到最长递增连续子序列](https://www.geeksforgeeks.org/longest-increasing-consecutive-subsequence/)的长度。为了打印子序列，我们存储最后一个元素的索引。然后我们打印以最后一个元素结尾的连续元素。
下面给出的是上述方法的实施:

## C++

```
// CPP program to find length of the
// longest increasing subsequence
// whose adjacent element differ by 1
#include <bits/stdc++.h>
using namespace std;

// function that returns the length of the
// longest increasing subsequence
// whose adjacent element differ by 1
void longestSubsequence(int a[], int n)
{
    // stores the index of elements
    unordered_map<int, int> mp;

    // stores the length of the longest
    // subsequence that ends with a[i]
    int dp[n];
    memset(dp, 0, sizeof(dp));

    int maximum = INT_MIN;

    // iterate for all element
    int index = -1;
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
        if (maximum < dp[i]) {
            maximum = dp[i];
            index = i;
        }
    }

    // We know last element of sequence is
    // a[index]. We also know that length
    // of subsequence is "maximum". So We
    // print these many consecutive elements
    // starting from "a[index] - maximum + 1"
    // to a[index].
    for (int curr = a[index] - maximum + 1;
         curr <= a[index]; curr++)
        cout << curr << " ";
}

// Driver Code
int main()
{
    int a[] = { 3, 10, 3, 11, 4, 5, 6, 7, 8, 12 };
    int n = sizeof(a) / sizeof(a[0]);
    longestSubsequence(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the
// longest increasing subsequence
// whose adjacent element differ by
import java.util.HashMap;

class GFG
{

    // function that returns the length of the
    // longest increasing subsequence
    // whose adjacent element differ by 1
    public static void longestSubsequence(int[] a,
                                          int n)
    {

        // stores the index of elements
        HashMap<Integer,
                Integer> mp = new HashMap<>();

        // stores the length of the longest
        // subsequence that ends with a[i]
        int[] dp = new int[n];

        int maximum = Integer.MIN_VALUE;

        // iterate for all element
        int index = -1;
        for(int i = 0; i < n; i++)
        {

            // if a[i]-1 is present before i-th index
            if (mp.get(a[i] - 1) != null)
            {

                // last index of a[i]-1
                int lastIndex = mp.get(a[i] - 1) - 1;

                // relation
                dp[i] = 1 + dp[lastIndex];
            }
            else
                dp[i] = 1;

            // stores the index as 1-index as we need to
            // check for occurrence, hence 0-th index
            // will not be possible to check
            mp.put(a[i], i +  1);

            // stores the longest length
            if (maximum < dp[i])
            {
                maximum = dp[i];
                index = i;
            }
        }

        // We know last element of sequence is
        // a[index]. We also know that length
        // of subsequence is "maximum". So We
        // print these many consecutive elements
        // starting from "a[index] - maximum + 1"
        // to a[index].
        for (int curr = a[index] - maximum + 1;
            curr <= a[index]; curr++)
            System.out.print(curr + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 3, 10, 3, 11, 4,
                    5, 6, 7, 8, 12 };
        int n = a.length;
        longestSubsequence(a, n);
    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python 3 program to find length of
# the longest increasing subsequence
# whose adjacent element differ by 1
import sys

# function that returns the length
# of the longest increasing subsequence
# whose adjacent element differ by 1
def longestSubsequence(a, n):

    # stores the index of elements
    mp = {i:0 for i in range(13)}

    # stores the length of the longest
    # subsequence that ends with a[i]
    dp = [0 for i in range(n)]

    maximum = -sys.maxsize - 1

    # iterate for all element
    index = -1
    for i in range(n):

        # if a[i]-1 is present before
        # i-th index
        if ((a[i] - 1 ) in mp):

            # last index of a[i]-1
            lastIndex = mp[a[i] - 1] - 1

            # relation
            dp[i] = 1 + dp[lastIndex]
        else:
            dp[i] = 1

        # stores the index as 1-index as we
        # need to check for occurrence, hence
        # 0-th index will not be possible to check
        mp[a[i]] = i + 1

        # stores the longest length
        if (maximum < dp[i]):
            maximum = dp[i]
            index = i

    # We know last element of sequence is
    # a[index]. We also know that length
    # of subsequence is "maximum". So We
    # print these many consecutive elements
    # starting from "a[index] - maximum + 1"
    # to a[index].
    for curr in range(a[index] - maximum + 1,
                      a[index] + 1, 1):
        print(curr, end = " ")

# Driver Code
if __name__ == '__main__':
    a = [3, 10, 3, 11, 4, 5,
                6, 7, 8, 12]
    n = len(a)
    longestSubsequence(a, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find length of the
// longest increasing subsequence
// whose adjacent element differ by
using System;
using System.Collections.Generic;

class GFG
{

    // function that returns the length of the
    // longest increasing subsequence
    // whose adjacent element differ by 1
    static void longestSubsequence(int[] a, int n)
    {

        // stores the index of elements
        Dictionary<int,
                   int> mp = new Dictionary<int,
                                            int>();

        // stores the length of the longest
        // subsequence that ends with a[i]
        int[] dp = new int[n];

        int maximum = -100000000;

        // iterate for all element
        int index = -1;
        for(int i = 0; i < n; i++)
        {

            // if a[i]-1 is present before i-th index
            if (mp.ContainsKey(a[i] - 1) == true)
            {

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
            if (maximum < dp[i])
            {
                maximum = dp[i];
                index = i;
            }
        }

        // We know last element of sequence is
        // a[index]. We also know that length
        // of subsequence is "maximum". So We
        // print these many consecutive elements
        // starting from "a[index] - maximum + 1"
        // to a[index].
        for (int curr = a[index] - maximum + 1;
            curr <= a[index]; curr++)
            Console.Write(curr + " ");
    }

    // Driver Code
    static void Main()
    {
        int[] a = { 3, 10, 3, 11, 4,
                    5, 6, 7, 8, 12 };
        int n = a.Length;
        longestSubsequence(a, n);
    }
}

// This code is contributed by mohit kumar
```

## java 描述语言

```
<script>
// Javascript program to find length of the
// longest increasing subsequence
// whose adjacent element differ by

    // function that returns the length of the
    // longest increasing subsequence
    // whose adjacent element differ by 1
    function longestSubsequence(a, n)
    {

        // stores the index of elements
        let mp = new Map();

        // stores the length of the longest
        // subsequence that ends with a[i]
        let dp = new Array(n);

        let maximum = Number.MIN_VALUE;

        // iterate for all element
        let index = -1;
        for(let i = 0; i < n; i++)
        {

            // if a[i]-1 is present before i-th index
            if (mp.get(a[i] - 1) != null)
            {

                // last index of a[i]-1
                let lastIndex = mp.get(a[i] - 1) - 1;

                // relation
                dp[i] = 1 + dp[lastIndex];
            }
            else
                dp[i] = 1;

            // stores the index as 1-index as we need to
            // check for occurrence, hence 0-th index
            // will not be possible to check
            mp.set(a[i], i +  1);

            // stores the longest length
            if (maximum < dp[i])
            {
                maximum = dp[i];
                index = i;
            }
        }

        // We know last element of sequence is
        // a[index]. We also know that length
        // of subsequence is "maximum". So We
        // print these many consecutive elements
        // starting from "a[index] - maximum + 1"
        // to a[index].
        for (let curr = a[index] - maximum + 1;
            curr <= a[index]; curr++)
            document.write(curr + " ");
    }

    // Driver Code
    let a=[3, 10, 3, 11, 4,
                    5, 6, 7, 8, 12 ];

    let n = a.length;
    longestSubsequence(a, n);

// This code is contributed by patel2127
</script>
```

**输出:**

```
3 4 5 6 7 8 
```

**时间复杂度:**O(nlogn)
T3】辅助空间: O(n)