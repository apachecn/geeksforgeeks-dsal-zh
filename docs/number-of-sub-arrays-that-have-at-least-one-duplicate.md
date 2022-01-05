# 至少有一个副本的子阵列数量

> 原文:[https://www . geesforgeks . org/至少有一个副本的子数组数量/](https://www.geeksforgeeks.org/number-of-sub-arrays-that-have-at-least-one-duplicate/)

给定 n 个元素的数组 *arr* ，任务是找出给定数组中包含至少一个重复元素的子数组的数量。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 0
> 没有重复元素的子数组。
> **输入:** arr[] = {4，3，4，3}
> **输出:** 3
> 可能的子阵列有{4，3，4}、{4，3，4，3}和{3，4，3}

**进场:**

*   首先，找出该数组可以组成的子数组的总数，用 *total* 表示，然后用 *total = (n*(n+1))/2* 表示。
*   现在找到所有元素都不同的子数组(可以使用[窗口滑动技术](https://www.geeksforgeeks.org/window-sliding-technique/)找到)，并用*唯一的*表示。
*   最后，至少有一个元素重复的子数组的数量为*(总计–唯一)*

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return the count of the
// sub-arrays that have at least one duplicate
ll count(ll arr[], ll n)
{
    ll unique = 0;

    // two pointers
    ll i = -1, j = 0;

    // to store frequencies of the numbers
    unordered_map<ll, ll> freq;
    for (j = 0; j < n; j++) {
        freq[arr[j]]++;

        // number is not distinct
        if (freq[arr[j]] >= 2) {
            i++;
            while (arr[i] != arr[j]) {
                freq[arr[i]]--;
                i++;
            }
            freq[arr[i]]--;
            unique = unique + (j - i);
        }
        else
            unique = unique + (j - i);
    }

    ll total = n * (n + 1) / 2;

    return total - unique;
}

// Driver code
int main()
{
    ll arr[] = { 4, 3, 4, 3 };
    ll n = sizeof(arr) / sizeof(arr[0]);
    cout << count(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of the
// sub-arrays that have at least one duplicate
static Integer count(Integer arr[], Integer n)
{
    Integer unique = 0;

    // two pointers
    Integer i = -1, j = 0;

    // to store frequencies of the numbers
    Map<Integer, Integer> freq = new HashMap<>();
    for (j = 0; j < n; j++)
    {
        if(freq.containsKey(arr[j]))
        {
            freq.put(arr[j], freq.get(arr[j]) + 1);
        }
        else
        {
            freq.put(arr[j], 1);
        }

        // number is not distinct
        if (freq.get(arr[j]) >= 2)
        {
            i++;
            while (arr[i] != arr[j])
            {
                freq.put(arr[i], freq.get(arr[i]) - 1);
                i++;
            }
            freq.put(arr[i], freq.get(arr[i]) - 1);
            unique = unique + (j - i);
        }
        else
            unique = unique + (j - i);
    }

    Integer total = n * (n + 1) / 2;

    return total - unique;
}

// Driver code
public static void main(String[] args)
{
    Integer arr[] = { 4, 3, 4, 3 };
    Integer n = arr.length;
    System.out.println(count(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict

# Function to return the count of the
# sub-arrays that have at least one duplicate
def count(arr, n):

    unique = 0

    # two pointers
    i, j = -1, 0

    # to store frequencies of the numbers
    freq = defaultdict(lambda:0)
    for j in range(0, n):
        freq[arr[j]] += 1

        # number is not distinct
        if freq[arr[j]] >= 2:
            i += 1

            while arr[i] != arr[j]:
                freq[arr[i]] -= 1
                i += 1

            freq[arr[i]] -= 1
            unique = unique + (j - i)

        else:
            unique = unique + (j - i)

    total = (n * (n + 1)) // 2

    return total - unique

# Driver Code
if __name__ == "__main__":

    arr = [4, 3, 4, 3]
    n = len(arr)
    print(count(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{

// Function to return the count of the
// sub-arrays that have at least one duplicate
static int count(int []arr, int n)
{
    int unique = 0;

    // two pointers
    int i = -1, j = 0;

    // to store frequencies of the numbers
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();
    for (j = 0; j < n; j++)
    {
        if(freq.ContainsKey(arr[j]))
        {
            freq[arr[j]] = freq[arr[j]] + 1;
        }
        else
        {
            freq.Add(arr[j], 1);
        }

        // number is not distinct
        if (freq[arr[j]] >= 2)
        {
            i++;
            while (arr[i] != arr[j])
            {
                freq[arr[i]] = freq[arr[i]] - 1;
                i++;
            }
            freq[arr[i]] = freq[arr[i]] - 1;
            unique = unique + (j - i);
        }
        else
            unique = unique + (j - i);
    }

    int total = n * (n + 1) / 2;

    return total - unique;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 3, 4, 3 };
    int n = arr.Length;
    Console.WriteLine(count(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of the
// sub-arrays that have at least one duplicate
function count(arr, n)
{
    let unique = 0;

    // two pointers
    let i = -1, j = 0;

    // to store frequencies of the numbers
    let freq = new Map();
    for (j = 0; j < n; j++) {
        if(freq.has(arr[j])){
            freq.set(arr[j], freq.get(arr[j]) + 1)
        }else{
            freq.set(arr[j], 1)
        }

        // number is not distinct
        if (freq.get(arr[j]) >= 2) {
            i++;
            while (arr[i] != arr[j]) {
                freq.set(arr[i], freq.get(arr[i]) - 1)
                i++;
            }
            freq.set(arr[i], freq.get(arr[i]) - 1)
            unique = unique + (j - i);
        }
        else
            unique = unique + (j - i);
    }

    let total =  n *(n + 1) / 2;

    return total - unique;
}

// Driver code
    let arr = [ 4, 3, 4, 3 ];
    let n = arr.length;
    document.write(count(arr, n) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(N)