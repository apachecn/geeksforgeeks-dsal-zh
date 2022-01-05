# 最大差值为 1 的最大子集

> 原文:[https://www . geesforgeks . org/最大子集-最大差异-1/](https://www.geeksforgeeks.org/largest-subset-maximum-difference-1/)

给定正整数的数组**arr[]****n**。任务是找出由给定数组的元素形成的子集的大小，并且集合中任意两个元素之间的绝对差小于或等于 1。
**例:**

```
Input : arr[] = {8, 9, 8, 7, 8, 9, 10, 11}
Output : 5
If we make subset with elements {8, 9, 8, 8, 9}. 
Each pair in the subset has an absolute 
difference <= 1 

Input : arr[] = {4, 5, 2, 4, 4, 4}
Output : 5
Subset is {4, 5, 4, 4, 4}
```

请注意，由于我们希望任何两个元素之间的绝对差值小于或等于 1，因此最多可以有两个不同的数字。因此，我们选择的子集将是{a，a，a，…..，b，b，b}或{a，a，a，a，…..}.
现在，为了找到这个子集的大小，我们将找到每个元素的频率，比如 c <sub>1</sub> ，c <sub>2</sub> ，c <sub>3</sub> ，…。，c <sub>j</sub> ，…。，c<sub>arr</sub>中的最大元素。那么我们的答案就是 c <sub>i</sub> + c <sub>i+1</sub> 的最大值。
以下是本办法的实施情况:

## C++

```
// CPP Program to find the size of
// the subset formed from the elements
// of the given array such that the
// maximum difference is 1
#include <bits/stdc++.h>
using namespace std;

// Return the maximum size of subset with
// absolute difference between any element
// is less than 1.
int maxsizeSubset(int arr[], int n)
{
    // Inserting elements and their
    // frequencies in a hash table.
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Traverse through map, for every element
    // x in map, find if x+1 also exists in map.
    // If exists, see if sum of their frequencies
    // is more than current result.
    int res = 0;
    for (auto x : mp)
    if (mp.find(x.first + 1) != mp.end())
    {
        res = max(res, mp[x.first] + mp[x.first+1]);
    }
    else
    {
        res=max(res,mp[x.first]);
    }
    return res;
}

// Driven Program
int main()
{
    int arr[] = {1, 2, 2, 3, 1, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxsizeSubset(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the size of
// the subset formed from the elements
// of the given array such that the
// maximum difference is 1
import java.util.*;

class GFG
{

    // Return the maximum size of subset with
    // absolute difference between any element
    // is less than 1.
    static int maxsizeSubset(int arr[], int n)
    {
        // Inserting elements and their
        // frequencies in a hash table.
        Map<Integer, Integer> mp = new HashMap<>();
        for (int i = 0; i < n; i++)
        {
            if (mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
            else
            {
                mp.put(arr[i], 1);
            }
        }

        // Traverse through map, for every element
        // x in map, find if x+1 also exists in map.
        // If exists, see if sum of their frequencies
        // is more than current result.
        int res = 0;
        for (Map.Entry<Integer, Integer> x : mp.entrySet())
        {
            if (mp.containsKey(x.getKey() + 1))
            {
                res = Math.max(res, mp.get(x.getKey()) + mp.get(x.getKey() + 1));
            }
            else
            {
                res = Math.max(res, mp.get(x.getKey()));
            }
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 2, 3, 1, 2};
        int n = arr.length;
        System.out.println(maxsizeSubset(arr, n));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## C#

```
// C# Program to find the size of
// the subset formed from the elements
// of the given array such that the
// maximum difference is 1
using System;
using System.Collections.Generic;

class GFG
{

    // Return the maximum size of subset with
    // absolute difference between any element
    // is less than 1.
    static int maxsizeSubset(int []arr, int n)
    {
        // Inserting elements and their
        // frequencies in a hash table.
        Dictionary<int,
                   int> mp = new Dictionary<int,
                                            int>();
        for (int i = 0 ; i < n; i++)
        {
            if(mp.ContainsKey(arr[i]))
            {
                var val = mp[arr[i]];
                mp.Remove(arr[i]);
                mp.Add(arr[i], val + 1);
            }
            else
            {
                mp.Add(arr[i], 1);
            }
        }

        // Traverse through map, for every element
        // x in map, find if x+1 also exists in map.
        // If exists, see if sum of their frequencies
        // is more than current result.
        int res = 0;
        foreach(KeyValuePair<int, int > x in mp)
        {
            if (mp.ContainsKey(x.Key + 1))
            {
                res = Math.Max(res, mp[x.Key] + mp[x.Key + 1]);
            }
            else
            {
                res = Math.Max(res, mp[x.Key]);
            }
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 2, 2, 3, 1, 2};
        int n = arr.Length;
        Console.WriteLine(maxsizeSubset(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program to find the size of
// the subset formed from the elements
// of the given array such that the
// maximum difference is 1

// Return the maximum size of subset with
// absolute difference between any element
// is less than 1.
function maxsizeSubset(arr, n) {
    // Inserting elements and their
    // frequencies in a hash table.
    let mp = new Map();
    for (let i = 0; i < n; i++) {
        if (mp.has(arr[i])) {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else {
            mp.set(arr[i], 1)
        }
    }

    // Traverse through map, for every element
    // x in map, find if x+1 also exists in map.
    // If exists, see if sum of their frequencies
    // is more than current result.
    let res = 0;
    for (let x of mp)
        if (mp.has(x[0] + 1)) {
            res = Math.max(res, mp.get(x[0]) + mp.get(x[0] + 1));
        }
        else {
            res = Math.max(res, mp.get(x[0]));
        }
    return res;
}

// Driven Program
let arr = [1, 2, 2, 3, 1, 2];
let n = arr.length;
document.write(maxsizeSubset(arr, n) + "<br>");

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)