# 具有形式 k^m 之和的子阵列的数量，m > = 0

> 原文:[https://www . geeksforgeeks . org/子阵列数量-具有形式之和-km-m-0/](https://www.geeksforgeeks.org/number-of-subarrays-having-sum-of-the-form-km-m-0/)

给定一个整数 **k** 和一个数组 **arr[]** ，任务是计算子数组的数量，这些子数组的和等于 k 的某个正整数幂
**例:**

> **输入:** arr[] = { 2，2，2，2 } K = 2
> **输出:** 8
> 以下索引的子数组有效:
> 【1，1】、【2，2】、【3，3】、【4，4】、【1，2】、
> 【2，3】、【3，4】、【1，4】
> **输入:** arr[] = { 3，-6，-3，12 } K

**天真方法**:天真方法是遍历所有子数组，检查每个子数组的和是否等于 k 的某个整数次幂
**高效方法**:更好的方法是维护前缀和数组 **prefix_sum** 和映射前缀和到其计数的映射 **m** 。 *m[a] = 1 表示 **a** 是某个前缀的前缀和。*

> 沿*向后方向*迭代数组，并仔细遵循下面的讨论。假设在遍历数组时，我们位于第 i <sup>个</sup>索引处，在遍历索引后，我们执行操作 **op = m[prefix_sum[i]]++** 。因此，当我们在索引 **i** ， **op** 还没有执行。请参见代码以获得生动的解释。
> 如果 **m[a + b] = c** 其中 *a = prefix_sum[i]，b = k <sup>p</sup> 和 c 是从地图*中提取的值，那么意味着从 i <sup>第</sup>个索引开始到数组末尾，有 c 个子数组的和等于 b，将 **c** 加到当前和。
> 这是因为对于每个索引 **j > i，已经执行了 m[prefix _ sum[j]]+**。因此，地图具有关于以 **j > i** 结束的前缀的前缀和的信息。将 **b** 加到前缀和上，我们可以得到所有那些和的计数 **a + b** ，这将表明存在一个和等于 **b** 的子数组。

**注意** : k = 1 和 k = -1 需要分开处理。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define ll long long
#define MAX 100005

using namespace std;

// Function to count number of sub-arrays
// whose sum is k^p where p>=0
ll countSubarrays(int* arr, int n, int k)
{
    ll prefix_sum[MAX];
    prefix_sum[0] = 0;

    partial_sum(arr, arr + n, prefix_sum + 1);

    ll sum;

    if (k == 1) {

        sum = 0;
        map<ll, int> m;

        for (int i = n; i >= 0; i--) {

            // If m[a+b] = c, then add c to the current sum.
            if (m.find(prefix_sum[i] + 1) != m.end())
                sum += m[prefix_sum[i] + 1];

            // Increase count of prefix sum.
            m[prefix_sum[i]]++;
        }

        return sum;
    }

    if (k == -1) {

        sum = 0;
        map<ll, int> m;

        for (int i = n; i >= 0; i--) {

            // If m[a+b] = c, then add c to the current sum.
            if (m.find(prefix_sum[i] + 1) != m.end())
                sum += m[prefix_sum[i] + 1];

            if (m.find(prefix_sum[i] - 1) != m.end())
                sum += m[prefix_sum[i] - 1];

            // Increase count of prefix sum.
            m[prefix_sum[i]]++;
        }

        return sum;
    }

    sum = 0;

    // b = k^p, p>=0
    ll b;
    map<ll, int> m;

    for (int i = n; i >= 0; i--) {

        b = 1;
        while (true) {

            // k^m can be maximum equal to 10^14.
            if (b > 100000000000000)
                break;

            // If m[a+b] = c, then add c to the current sum.
            if (m.find(prefix_sum[i] + b) != m.end())
                sum += m[prefix_sum[i] + b];

            b *= k;
        }

        // Increase count of prefix sum.
        m[prefix_sum[i]]++;
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 2, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << countSubarrays(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
class GFG{

static final int MAX = 100005;

// partial_sum
static long[] partial_sum(long []prefix_sum,
                          int[]arr, int n)
{
  for (int i = 1; i <= n; i++)
  {
    prefix_sum[i] = (prefix_sum[i - 1] +
                     arr[i - 1]);
  }

  return prefix_sum;
}

// Function to count number of
// sub-arrays whose sum is k^p
// where p>=0
static int countSubarrays(int []arr,
                          int n, int k)
{
  long []prefix_sum = new long[MAX];
  prefix_sum[0] = 0;
  prefix_sum = partial_sum(prefix_sum ,
                           arr, n);
  int sum;

  if (k == 1)
  {
    sum = 0;
    HashMap<Long,
            Integer> m = new HashMap<>();

    for (int i = n; i >= 0; i--)
    {
      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.containsKey(prefix_sum[i] + 1))
        sum += m.get(prefix_sum[i] + 1);

      // Increase count of prefix sum.
      if(m.containsKey(prefix_sum[i]))
        m.put(prefix_sum[i],
        m.get(prefix_sum[i]) + 1);
      else
        m.put(prefix_sum[i], 1);
    }
    return sum;
  }

  if (k == -1)
  {
    sum = 0;
    HashMap<Long,
            Integer> m = new HashMap<>();

    for (int i = n; i >= 0; i--)
    {
      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.containsKey(prefix_sum[i] + 1))
        sum += m.get(prefix_sum[i] + 1);

      if (m.containsKey(prefix_sum[i] - 1))
        sum += m.get(prefix_sum[i] - 1);

      // Increase count of prefix sum.
      if(m.containsKey(prefix_sum[i]))
        m.put(prefix_sum[i],
        m.get(prefix_sum[i]) + 1);
      else
        m.put(prefix_sum[i], 1);
    }
    return sum;
  }

  sum = 0;

  // b = k^p, p>=0
  long b, l = 100000000000000L;
  HashMap<Long,
          Integer> m = new HashMap<>();

  for (int i = n; i >= 0; i--)
  {
    b = 1;
    while (true)
    {
      // k^m can be maximum equal
      // to 10^14.
      if (b > l)
        break;

      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.containsKey(prefix_sum[i] + b))
        sum += m.get(prefix_sum[i] + b);

      b *= k;
    }

    // Increase count of prefix sum.
    if(m.containsKey(prefix_sum[i]))
      m.put((prefix_sum[i]),
      m.get(prefix_sum[i]) + 1);
    else
      m.put((prefix_sum[i]), 1);
  }
  return sum;
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {2, 2, 2, 2};
  int n = arr.length;
  int k = 2;
  System.out.print(countSubarrays(arr,
                                  n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
from collections import defaultdict
MAX = 100005

def partial_sum(prefix_sum,
                arr, n):

  for i in range(1 , n + 1):
    prefix_sum[i] = (prefix_sum[i - 1] +
                     arr[i - 1])
  return prefix_sum

# Function to count number of
# sub-arrays whose sum is k^p
# where p>=0
def countSubarrays(arr, n, k):

    prefix_sum = [0] * MAX
    prefix_sum[0] = 0

    prefix_sum = partial_sum(prefix_sum,
                             arr, n)
    if (k == 1):
        sum = 0
        m = defaultdict(int)

        for i in range(n, -1, -1):

            # If m[a+b] = c, then add
            # c to the current sum.
            if ((prefix_sum[i] + 1) in m):
                sum += m[prefix_sum[i] + 1]

            # Increase count of prefix sum.
            m[prefix_sum[i]] += 1

        return sum

    if (k == -1):
        sum = 0
        m = defaultdict(int)

        for i in range(n, -1, -1):

            # If m[a+b] = c, then add c
            # to the current sum.
            if ((prefix_sum[i] + 1) in m):
                sum += m[prefix_sum[i] + 1]

            if ((prefix_sum[i] - 1) in m):
                sum += m[prefix_sum[i] - 1]

            # Increase count of prefix sum.
            m[prefix_sum[i]] += 1

        return sum

    sum = 0

    # b = k^p, p>=0
    m = defaultdict(int)

    for i in range(n, -1, -1):
        b = 1
        while (True):

            # k^m can be maximum equal
            # to 10^14.
            if (b > 100000000000000):
                break

            # If m[a+b] = c, then add c
            # to the current sum.
            if ((prefix_sum[i] + b) in m):
                sum += m[prefix_sum[i] + b]

            b *= k

        # Increase count of prefix
        # sum.
        m[prefix_sum[i]] += 1
    return sum

# Driver code
if __name__ == "__main__":

    arr = [2, 2, 2, 2]
    n = len(arr)
    k = 2
    print(countSubarrays(arr, n, k))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
class GFG{

static readonly int MAX = 100005;

// partial_sum
static long[] partial_sum(long []prefix_sum,
                          int[]arr, int n)
{
  for (int i = 1; i <= n; i++)
  {
    prefix_sum[i] = (prefix_sum[i - 1] +
                     arr[i - 1]);
  }

  return prefix_sum;
}

// Function to count number of
// sub-arrays whose sum is k^p
// where p>=0
static int countSubarrays(int []arr,
                          int n, int k)
{
  long []prefix_sum = new long[MAX];
  prefix_sum[0] = 0;
  prefix_sum = partial_sum(prefix_sum ,
                           arr, n);
  int sum;

  if (k == 1)
  {
    sum = 0;
    Dictionary<long,
               int> mp =
               new Dictionary<long,
                              int>();

    for (int i = n; i >= 0; i--)
    {
      // If m[a+b] = c, then add c to
      // the current sum.
      if (mp.ContainsKey(prefix_sum[i] + 1))
        sum += mp[prefix_sum[i] + 1];

      // Increase count of prefix sum.
      if(mp.ContainsKey(prefix_sum[i]))
        mp.Add(prefix_sum[i],
        mp[prefix_sum[i]] + 1);
      else
        mp.Add(prefix_sum[i], 1);
    }
    return sum;
  }

  if (k == -1)
  {
    sum = 0;
    Dictionary<long,
               int> map =
               new Dictionary<long,
                              int>();

    for (int i = n; i >= 0; i--)
    {
      // If m[a+b] = c, then add c to
      // the current sum.
      if (map.ContainsKey(prefix_sum[i] + 1))
        sum += map[prefix_sum[i] + 1];

      if (map.ContainsKey(prefix_sum[i] - 1))
        sum += map[prefix_sum[i] - 1];

      // Increase count of prefix sum.
      if(map.ContainsKey(prefix_sum[i]))
        map.Add(prefix_sum[i],
        map[prefix_sum[i]] + 1);
      else
        map.Add(prefix_sum[i], 1);
    }
    return sum;
  }

  sum = 0;

  // b = k^p, p>=0
  long b, l = 100000000000000L;
  Dictionary<long,
             int> m =
             new Dictionary<long,
                            int>();

  for (int i = n; i >= 0; i--)
  {
    b = 1;
    while (true)
    {
      // k^m can be maximum equal
      // to 10^14.
      if (b > l)
        break;

      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.ContainsKey(prefix_sum[i] + b))
        sum += m[prefix_sum[i] + b];

      b *= k;
    }

    // Increase count of prefix sum.
    if(m.ContainsKey(prefix_sum[i]))
      m.Add((prefix_sum[i]),
      m[prefix_sum[i]] + 1);
    else
      m.Add((prefix_sum[i]), 1);
  }
  return sum;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {2, 2, 2, 2};
  int n = arr.Length;
  int k = 2;
  Console.Write(countSubarrays(arr,
                               n, k));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

let MAX = 100005;

// partial_sum
function partial_sum(prefix_sum,arr,n)
{
    for (let i = 1; i <= n; i++)
  {
    prefix_sum[i] = (prefix_sum[i - 1] +
                     arr[i - 1]);
  }

  return prefix_sum;
}

// Function to count number of
// sub-arrays whose sum is k^p
// where p>=0
function countSubarrays(arr,n,k)
{
    let prefix_sum = new Array(MAX);
  prefix_sum[0] = 0;
  prefix_sum = partial_sum(prefix_sum ,
                           arr, n);
  let sum;

  if (k == 1)
  {
    sum = 0;
    let m = new Map();

    for (let i = n; i >= 0; i--)
    {
      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.has(prefix_sum[i] + 1))
        sum += m.get(prefix_sum[i] + 1);

      // Increase count of prefix sum.
      if(m.has(prefix_sum[i]))
        m.set(prefix_sum[i],
        m.get(prefix_sum[i]) + 1);
      else
        m.set(prefix_sum[i], 1);
    }
    return sum;
  }

  if (k == -1)
  {
    sum = 0;
    let m = new Map();

    for (let i = n; i >= 0; i--)
    {
      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.has(prefix_sum[i] + 1))
        sum += m.get(prefix_sum[i] + 1);

      if (m.has(prefix_sum[i] - 1))
        sum += m.get(prefix_sum[i] - 1);

      // Increase count of prefix sum.
      if(m.has(prefix_sum[i]))
        m.set(prefix_sum[i],
        m.get(prefix_sum[i]) + 1);
      else
        m.set(prefix_sum[i], 1);
    }
    return sum;
  }

  sum = 0;

  // b = k^p, p>=0
  let b, l = 100000000000000;
  let m = new Map();

  for (let i = n; i >= 0; i--)
  {
    b = 1;
    while (true)
    {
      // k^m can be maximum equal
      // to 10^14.
      if (b > l)
        break;

      // If m[a+b] = c, then add c to
      // the current sum.
      if (m.has(prefix_sum[i] + b))
        sum += m.get(prefix_sum[i] + b);

      b *= k;
    }

    // Increase count of prefix sum.
    if(m.has(prefix_sum[i]))
      m.set((prefix_sum[i]),
      m.get(prefix_sum[i]) + 1);
    else
      m.set((prefix_sum[i]), 1);
  }
  return sum;
}

// Driver code
let arr=[2, 2, 2, 2];
let n = arr.length;
let k = 2;
document.write(countSubarrays(arr,
                                  n, k));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
8
```