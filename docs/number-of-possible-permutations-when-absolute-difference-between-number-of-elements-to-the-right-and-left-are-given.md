# 当给定左右元素数量的绝对差值时可能的排列数量

> 原文:[https://www . geeksforgeeks . org/当给定左右元素数量的绝对差值时，可能的排列数量/](https://www.geeksforgeeks.org/number-of-possible-permutations-when-absolute-difference-between-number-of-elements-to-the-right-and-left-are-given/)

给定一个由 N 个元素组成的数组，其中每一个元素都是 I，那么它的右边和左边的元素总数之间的绝对差值就给出了。找出实际数组元素的可能排序数。
**例:**

> **输入:** N = 5，arr[] = {2，4，4，0，2}
> **输出:** 4
> 有四种可能的顺序，如下:
> 2，1，4，5，3
> 2，5，4，1，3
> 3，1，4，5，2
> 3，5，4，1，2
> **输入:** N = 7，arr[] = {6，4，0，0

**做法:**把问题分成两部分。当 N 为奇数时，当 N 为偶数时。

*   **情况 1:**N 为奇数时。
    考虑 N = 7，有 7 个空格，左右元素的绝对差一定像[6 4 2 0 2 4 6]。观察中间的元素必须有绝对差 0，而其他元素从 2 到 N-1，它们的每个计数应该是 2。如果它没有实现它，那么对于从 2 到 N-1 的每个元素 I，没有有效的顺序，我们有 2 种方法来填充空间，因此总的方法将是所有方法的乘积。

*   **情况 2:** 当 N 为偶数时。
    考虑 N = 6，有 6 个空间，就像[5 3 1 3 5]，其中 a[i]给出了左右元素数量的绝对差。对于每一个 a[i]，我们有 2 种方式，因此答案将是所有方式的产物。

以下是实施办法:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of permutations
// possible of the original array to satisfy
// the given absolute differences
int totalways(int* arr, int n)
{
    // To store the count of each
    // a[i] in a map
    unordered_map<int, int> cnt;
    for (int i = 0; i < n; ++i) {
        cnt[arr[i]]++;
    }

    // if n is odd
    if (n % 2 == 1) {
        int start = 0, endd = n - 1;

        // check the count of each whether
        // it satisfy the given criteria or not
        for (int i = start; i <= endd; i = i + 2) {
            if (i == 0) {

                // there is only 1 way
                // for middle element.
                if (cnt[i] != 1) {
                    return 0;
                }
            }
            else {

                // for others there are 2 ways.
                if (cnt[i] != 2) {
                    return 0;
                }
            }
        }

        // now find total ways
        int ways = 1;
        start = 2, endd = n - 1;
        for (int i = start; i <= endd; i = i + 2) {
            ways = ways * 2;
        }
        return ways;
    }

    // When n is even.
    else if (n % 2 == 0) {

        // there will be no middle element so
        // for each a[i] there will be 2 ways
        int start = 1, endd = n - 1;
        for (int i = 1; i <= endd; i = i + 2) {
            if (cnt[i] != 2)
                return 0;
        }
        int ways = 1;
        for (int i = start; i <= endd; i = i + 2) {
            ways = ways * 2;
        }
        return ways;
    }
}

// Driver Code
int main()
{
    int N = 5;

    int arr[N] = { 2, 4, 4, 0, 2 };

    cout<<totalways(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to find the number of permutations
// possible of the original array to satisfy
// the given absolute differences
static int totalways(int[] arr, int n)
{
    // To store the count of each
    // a[i] in a map
    HashMap<Integer,
            Integer>cnt = new HashMap<Integer,
                                      Integer>();

    for (int i = 0 ; i < n; i++)
    {
        if(cnt.containsKey(arr[i]))
        {
            cnt.put(arr[i], cnt.get(arr[i])+1);
        }
        else
        {
            cnt.put(arr[i], 1);
        }
    }

    // if n is odd
    if (n % 2 == 1)
    {
        int start = 0, endd = n - 1;

        // check the count of each whether
        // it satisfy the given criteria or not
        for (int i = start; i <= endd; i = i + 2)
        {
            if (i == 0)
            {

                // there is only 1 way
                // for middle element.
                if (cnt.get(i) != 1)
                {
                    return 0;
                }
            }
            else
            {

                // for others there are 2 ways.
                if (cnt.get(i) != 2)
                {
                    return 0;
                }
            }
        }

        // now find total ways
        int ways = 1;
        start = 2; endd = n - 1;
        for (int i = start; i <= endd; i = i + 2)
        {
            ways = ways * 2;
        }
        return ways;
    }

    // When n is even.
    else if (n % 2 == 0)
    {

        // there will be no middle element so
        // for each a[i] there will be 2 ways
        int start = 1, endd = n - 1;
        for (int i = 1; i <= endd; i = i + 2)
        {
            if (cnt.get(i) != 2)
                return 0;
        }
        int ways = 1;
        for (int i = start; i <= endd; i = i + 2)
        {
            ways = ways * 2;
        }
        return ways;
    }
    return Integer.MIN_VALUE;
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;

    int []arr = { 2, 4, 4, 0, 2 };

    System.out.println(totalways(arr, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the number of permutations
# possible of the original array to satisfy
# the given absolute differences
def totalways(arr, n):

    # To store the count of each
    # a[i] in a map
    cnt = dict()
    for i in range(n):
        cnt[arr[i]] = cnt.get(arr[i], 0) + 1

    # if n is odd
    if (n % 2 == 1):
        start, endd = 0, n - 1

        # check the count of each whether
        # it satisfy the given criteria or not
        for i in range(start, endd + 1, 2):
            if (i == 0):

                # there is only 1 way
                # for middle element.
                if (cnt[i] != 1):
                    return 0
            else:

                # for others there are 2 ways.
                if (cnt[i] != 2):
                    return 0

        # now find total ways
        ways = 1
        start = 2
        endd = n - 1
        for i in range(start, endd + 1, 2):
            ways = ways * 2
        return ways

    # When n is even.
    elif (n % 2 == 0):

        # there will be no middle element so
        # for each a[i] there will be 2 ways
        start = 1
        endd = n - 1
        for i in range(1, endd + 1, 2):
            if (cnt[i] != 2):
                return 0
        ways = 1
        for i in range(start, endd + 1, 2):
            ways = ways * 2
        return ways

# Driver Code
N = 5

arr = [2, 4, 4, 0, 2 ]

print(totalways(arr, N))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the number of permutations
// possible of the original array to satisfy
// the given absolute differences
static int totalways(int[] arr, int n)
{
    // To store the count of each
    // a[i] in a map
    Dictionary<int,
               int> cnt = new Dictionary<int,
                                         int>();

    for (int i = 0 ; i < n; i++)
    {
        if(cnt.ContainsKey(arr[i]))
        {
            cnt[arr[i]] = cnt[arr[i]] + 1;
        }
        else
        {
            cnt.Add(arr[i], 1);
        }
    }

    // if n is odd
    if (n % 2 == 1)
    {
        int start = 0, endd = n - 1;

        // check the count of each whether
        // it satisfy the given criteria or not
        for (int i = start; i <= endd; i = i + 2)
        {
            if (i == 0)
            {

                // there is only 1 way
                // for middle element.
                if (cnt[i] != 1)
                {
                    return 0;
                }
            }
            else
            {

                // for others there are 2 ways.
                if (cnt[i] != 2)
                {
                    return 0;
                }
            }
        }

        // now find total ways
        int ways = 1;
        start = 2; endd = n - 1;
        for (int i = start; i <= endd; i = i + 2)
        {
            ways = ways * 2;
        }
        return ways;
    }

    // When n is even.
    else if (n % 2 == 0)
    {

        // there will be no middle element so
        // for each a[i] there will be 2 ways
        int start = 1, endd = n - 1;
        for (int i = 1; i <= endd; i = i + 2)
        {
            if (cnt[i] != 2)
                return 0;
        }

        int ways = 1;
        for (int i = start; i <= endd; i = i + 2)
        {
            ways = ways * 2;
        }
        return ways;
    }
    return int.MinValue;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;

    int []arr = { 2, 4, 4, 0, 2 };

    Console.WriteLine(totalways(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // JavaScript implementation of the above approach
      // Function to find the number of permutations
      // possible of the original array to satisfy
      // the given absolute differences
      function totalways(arr, n) {
        // To store the count of each
        // a[i] in a map
        var cnt = {};

        for (var i = 0; i < n; i++) {
          if (cnt.hasOwnProperty(arr[i])) {
            cnt[arr[i]] = cnt[arr[i]] + 1;
          } else {
            cnt[arr[i]] = 1;
          }
        }

        // if n is odd
        if (n % 2 === 1) {
          var start = 0,
            endd = n - 1;

          // check the count of each whether
          // it satisfy the given criteria or not
          for (var i = start; i <= endd; i = i + 2) {
            if (i === 0) {
              // there is only 1 way
              // for middle element.
              if (cnt[i] !== 1) {
                return 0;
              }
            } else {
              // for others there are 2 ways.
              if (cnt[i] !== 2) {
                return 0;
              }
            }
          }

          // now find total ways
          var ways = 1;
          start = 2;
          endd = n - 1;
          for (var i = start; i <= endd; i = i + 2) {
            ways = ways * 2;
          }
          return ways;
        }

        // When n is even.
        else if (n % 2 === 0) {
          // there will be no middle element so
          // for each a[i] there will be 2 ways
          var start = 1,
            endd = n - 1;
          for (var i = 1; i <= endd; i = i + 2) {
            if (cnt[i] !== 2) return 0;
          }

          var ways = 1;
          for (var i = start; i <= endd; i = i + 2) {
            ways = ways * 2;
          }
          return ways;
        }
        return -2147483648;
      }

      // Driver Code
      var N = 5;
      var arr = [2, 4, 4, 0, 2];

      document.write(totalways(arr, N));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)