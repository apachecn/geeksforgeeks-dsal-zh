# 满足给定条件的子阵列排列

> 原文:[https://www . geesforgeks . org/subarray-满足给定条件的置换/](https://www.geeksforgeeks.org/subarray-permutation-that-satisfies-the-given-condition/)

给定从 **1** 到 **N** 的整数排列和一个整数 **M** ，任务是检查给定排列的任何子阵列是否是从 **1** 到 **M** 的整数排列。

**示例:**

> **输入:** arr[] = {4，5，1，3，2，6}，M = 3
> **输出:**是
> {4，5， **1，3，2** ，6}是需要的子阵。
> 
> **输入:** arr[] = {4，5，1，3，2，6}，M = 4
> T3】输出:否

**天真的方法:**天真的方法是生成所有 M 大小的子阵列，看看是否存在这样的子阵列。但是如果给定的排列太大，这种方法会很耗时，因为它是在 0(N<sup>3</sup>中运行的。

**高效方法:**更好的解决方案是使用 [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) 。

1.  从主排列来看，每个整数的位置存储在一个[图/字典](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  现在，观察如果存在一个从 1 到 m 的排列的子阵列，那么范围**【1，m】**中的所有数字将在主排列中占据 m 个连续的位置，无论是以排序还是随机的方式。
3.  当排序时，它们的位置也应该以 m 个连续数字的形式出现，从最小位置/值 x 及其 m-1 个连续位置开始。
4.  因此可以计算出每个整数 1 到 n 的**“位置之和”**，其中**位置之和(k) = sumcur=位置 _of_1 +位置 _ of _ 2+…位置 _of_k** 。
5.  让上述系列的**最小元素**为 **x** 。当位置被排序时，这将是第一个元素，其余的将是连续的。
6.  那么**如果需要的子阵列存在**，那么**位置之和(m)必须是 x + (x+1) +..(x+m-1) {m 个连续项} = x * m–m+m *(m+1)/2**。
7.  如果整数 1 到 m 的所有位置的和是这个和，那么对于给定的 m，返回 true，否则没有这样的子数组。

下面是上述方法的实现。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Function that returns true if the
// required subarray exists
// in the given array
bool subArray(ll* arr, ll n, ll m)
{
    ll i;

    // Map to store the positions of
    // each integer in the original
    // permutation
    unordered_map<ll, ll> mp;
    for (i = 0; i < n; i++) {

        // To store the address of each
        // entry in arr[n] but with
        // 1-based indexing
        mp[arr[i]] = i + 1;
    }

    ll sumcur = 0;

    // To track minimum position sumcur
    // for sum of all positions
    // till this position
    ll p = INT_MAX;
    vector<ll> ans;
    for (i = 1; i <= m; i++) {

        // Summing up addresses
        sumcur += mp[i];

        // Tracking minimum address
        // encountered till now
        p = min(p, mp[i]);

        // The sum of the addresses if
        // it forms the required subarray
        ll val = p * i - i + (i * (i + 1)) / 2;
        if (i == m) {

            // If current sum of address
            // is equal to val
            if (val == sumcur) {
                return true;
            }
            else
                return false;
        }
    }
}

// Driver code
int main()
{
    ll arr[] = { 4, 5, 1, 3, 2, 6 };
    int n = sizeof(arr) / sizeof(int);
    ll m = 3;

    if (subArray(arr, n, m))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if the
// required subarray exists
// in the given array
static boolean subArray(int[] arr, int n, int m)
{
    int i;

    // Map to store the positions of
    // each integer in the original
    // permutation
    HashMap<Integer, Integer> mp =
        new HashMap<Integer, Integer> ();
    for (i = 0; i < n; i++)
    {

        // To store the address of each
        // entry in arr[n] but with
        // 1-based indexing
        mp.put(arr[i], i + 1);
    }

    int sumcur = 0;

    // To track minimum position sumcur
    // for sum of aint positions
    // tiint this position
    int p = Integer.MAX_VALUE;
    Vector<Integer> ans = new Vector<Integer>();
    for (i = 1; i <= m; i++)
    {

        // Summing up addresses
        sumcur += mp.get(i);

        // Tracking minimum address
        // encountered tiint now
        p = Math.min(p, mp.get(i));

        // The sum of the addresses if
        // it forms the required subarray
        int val = p * i - i + (i * (i + 1)) / 2;
        if (i == m)
        {

            // If current sum of address
            // is equal to val
            if (val == sumcur)
            {
                return true;
            }
            else
                return false;
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 5, 1, 3, 2, 6 };
    int n = arr.length;
    int m = 3;

    if (subArray(arr, n, m))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the
# required subarray exists
# in the given array
def subArray(arr, n, m):
    i = 0

    # Map to store the positions of
    # each integer in the original
    # permutation
    mp = dict()
    for i in range(n):

        # To store the address of each
        # entry in arr[n] but with
        # 1-based indexing
        mp[arr[i]] = i + 1

    sumcur = 0

    # To track minimum position sumcur
    # for sum of a positions
    # ti this position
    p = 10**9
    ans = []
    for i in range(1, m + 1):

        # Summing up addresses
        sumcur += mp[i]

        # Tracking minimum address
        # encountered ti now
        p = min(p, mp[i])

        # The sum of the addresses if
        # it forms the required subarray
        val = p * i - i + (i * (i + 1)) / 2
        if (i == m):

            # If current sum of address
            # is equal to val
            if (val == sumcur):
                return True
            else:
                return False

# Driver code

arr = [4, 5, 1, 3, 2, 6]
n = len(arr)
m = 3

if (subArray(arr, n, m)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns true if the
// required subarray exists
// in the given array
static bool subArray(int[] arr, int n, int m)
{
    int i;

    // Map to store the positions of
    // each integer in the original
    // permutation
    Dictionary<int, int> mp =
        new Dictionary<int, int> ();
    for (i = 0; i < n; i++)
    {

        // To store the address of each
        // entry in arr[n] but with
        // 1-based indexing
        mp.Add(arr[i], i + 1);
    }

    int sumcur = 0;

    // To track minimum position sumcur
    // for sum of aint positions
    // tiint this position
    int p = int.MaxValue;
    List<int> ans = new List<int>();
    for (i = 1; i <= m; i++)
    {

        // Summing up addresses
        sumcur += mp[i];

        // Tracking minimum address
        // encountered tiint now
        p = Math.Min(p, mp[i]);

        // The sum of the addresses if
        // it forms the required subarray
        int val = p * i - i + (i * (i + 1)) / 2;
        if (i == m)
        {

            // If current sum of address
            // is equal to val
            if (val == sumcur)
            {
                return true;
            }
            else
                return false;
        }
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 5, 1, 3, 2, 6 };
    int n = arr.Length;
    int m = 3;

    if (subArray(arr, n, m))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if the
// required subarray exists
// in the given array
function subArray(arr, n, m)
{
    var i;

    // Map to store the positions of
    // each integer in the original
    // permutation
    var mp = new Map();
    for(i = 0; i < n; i++)
    {

        // To store the address of each
        // entry in arr[n] but with
        // 1-based indexing
        mp.set(arr[i], i + 1);
    }

    var sumcur = 0;

    // To track minimum position sumcur
    // for sum of all positions
    // till this position
    var p = 1000000000;
    var ans = [];
    for(i = 1; i <= m; i++)
    {

        // Summing up addresses
        sumcur += mp.get(i);

        // Tracking minimum address
        // encountered till now
        p = Math.min(p, mp.get(i));

        // The sum of the addresses if
        // it forms the required subarray
        var val = p * i - i +
        parseInt((i * (i + 1)) / 2);

        if (i == m)
        {

            // If current sum of address
            // is equal to val
            if (val == sumcur)
            {
                return true;
            }
            else
                return false;
        }
    }
}

// Driver code
var arr = [ 4, 5, 1, 3, 2, 6 ];
var n = arr.length;
var m = 3;

if (subArray(arr, n, m))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by famously

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)

**另一种有效的方法:使用滑动窗口**

我们将使用一个 M 大小的滑动窗口，其中我们将保持小于或等于 M 的数字计数，并在数组上迭代。如果计数等于 M，我们就找到了排列。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Function that returns true if the
// required subarray exists
// in the given array
bool subArray(ll* arr, ll n, ll m)
{
    int count = 0;//count less than m
      for (int i = 0; i < m; i++){
        if (arr[i] <= m)
          count++;
    }

      if (count == m)
      return true;

      for (int i = m; i < n; i++){
        if (arr[i-m] <= m)
          count--;
          if (arr[i] <= m)
          count++;
          if (count == m)
          return true;
    }
      return false;
}

// Driver code
int main()
{
    ll arr[] = { 4, 5, 1, 3, 2, 6 };
    int n = sizeof(arr) / sizeof(int);
    ll m = 3;

    if (subArray(arr, n, m))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

时间复杂度:0(N)

空间复杂性:O(N)