# 从数组中选择至少两个元素，使它们的 GCD 为 1，成本最小

> 原文:[https://www . geeksforgeeks . org/从数组中选择至少两个元素，这样它们的 gcd 就是 1，成本就是最小值/](https://www.geeksforgeeks.org/choose-atleast-two-elements-from-array-such-that-their-gcd-is-1-and-cost-is-minimum/)

给定两个整数数组 **arr[]** 和 **cost[]** ，其中 **cost[i]** 是选择 **arr[i]** 的成本。任务是选择具有至少两个元素的子集，使得该子集的所有元素的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 1，并且选择这些元素的成本尽可能最小，然后打印最小成本。
**举例:**

> **输入:** arr[] = {5，10，12，1}，成本[] = {2，1，2，6}
> **输出:** 4
> {5，12}是成本= 2 + 2 = 4
> **输入:** arr[] = {50，100，150，200，300}，成本[] = {2，3，4，5，6}
> **输出:【T0**

**方法:**将任意两个元素的 gcd 添加到地图中，现在对于每个元素 **arr[i]** 用目前找到的所有 gcd 值(保存在地图中)计算其 GCD，并更新**地图[gcd] = min(地图[gcd]，地图[gcd] +成本[i])** 。如果最终地图不包含 **gcd = 1** 的任何条目，则打印 **-1** 否则打印存储的最小成本。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost required
int getMinCost(int arr[], int n, int cost[])
{

    // Map to store <gcd, cost> pair where
    // cost is the cost to get the current gcd
    map<int, int> mp;
    mp.clear();
    mp[0] = 0;

    for (int i = 0; i < n; i++) {
        for (auto it : mp) {
            int gcd = __gcd(arr[i], it.first);

            // If current gcd value already exists in map
            if (mp.count(gcd) == 1)

                // Update the minimum cost
                // to get the current gcd
                mp[gcd] = min(mp[gcd], it.second + cost[i]);

            else
                mp[gcd] = it.second + cost[i];
        }
    }

    // If there can be no sub-set such that
    // the gcd of all the elements is 1
    if (mp[1] == 0)
        return -1;
    else
        return mp[1];
}

// Driver code
int main()
{
    int arr[] = { 5, 10, 12, 1 };
    int cost[] = { 2, 1, 2, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getMinCost(arr, n, cost);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;
import java.util.concurrent.ConcurrentHashMap;

class GFG{

// Function to return the minimum cost required
static int getMinCost(int arr[], int n, int cost[])
{

    // Map to store <gcd, cost> pair where
    // cost is the cost to get the current gcd
    Map<Integer,Integer> mp = new ConcurrentHashMap<Integer,Integer>();
    mp.clear();
    mp.put(0, 0);

    for (int i = 0; i < n; i++) {
        for (Map.Entry<Integer,Integer> it : mp.entrySet()){
            int gcd = __gcd(arr[i], it.getKey());

            // If current gcd value already exists in map
            if (mp.containsKey(gcd))

                // Update the minimum cost
                // to get the current gcd
                mp.put(gcd, Math.min(mp.get(gcd), it.getValue() + cost[i]));

            else
                mp.put(gcd,it.getValue() + cost[i]);
        }
    }

    // If there can be no sub-set such that
    // the gcd of all the elements is 1
    if (!mp.containsKey(1))
        return -1;
    else
        return mp.get(1);
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}
// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 10, 12, 1 };
    int cost[] = { 2, 1, 2, 6 };
    int n = arr.length;

    System.out.print(getMinCost(arr, n, cost));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

# Function to return the minimum cost required
def getMinCost(arr, n, cost):

    # Map to store <gcd, cost> pair where
    # cost is the cost to get the current gcd
    mp = dict()
    mp[0] = 0

    for i in range(n):
        for it in list(mp):
            gcd = __gcd(arr[i], it)

            # If current gcd value
            # already exists in map
            if (gcd in mp):

                # Update the minimum cost
                # to get the current gcd
                mp[gcd] = min(mp[gcd],
                              mp[it] + cost[i])

            else:
                mp[gcd] = mp[it] + cost[i]

    # If there can be no sub-set such that
    # the gcd of all the elements is 1
    if (mp[1] == 0):
        return -1
    else:
        return mp[1]

# Driver code
arr = [ 5, 10, 12, 1]
cost = [ 2, 1, 2, 6]
n = len(arr)

print(getMinCost(arr, n, cost))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{
  static int __gcd(int a, int b)  
  {  
    return b == 0? a:__gcd(b, a % b);     
  }

  // Function to return the minimum cost required
  static int getMinCost(int[] arr, int n, int[] cost)
  {

    // Map to store <gcd, cost> pair where
    // cost is the cost to get the current gcd
    Dictionary<int, int> mp = new Dictionary<int, int>();
    mp.Add(0, 0);
    for (int i = 0; i < n; i++)
    {

      foreach (int it in mp.Keys.ToList())
      {
        int gcd = __gcd(arr[i], it);

        // If current gcd value already exists in map
        if(mp.ContainsKey(gcd))
        {

          // Update the minimum cost
          // to get the current gcd
          mp[gcd] = Math.Min(mp[gcd], mp[it] + cost[i]);
        }
        else
        {
          mp.Add(gcd, mp[it] + cost[i]);
        }
      } 
    }

    // If there can be no sub-set such that
    // the gcd of all the elements is 1
    if (mp[1] == 0)
    {
      return -1;
    }
    else
    {
      return mp[1];
    }       
  }

  // Driver code
  static public void Main ()
  {
    int[] arr = { 5, 10, 12, 1 };
    int[] cost = { 2, 1, 2, 6 };
    int n = arr.Length;
    Console.WriteLine(getMinCost(arr, n, cost));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum cost required
function getMinCost(arr,n,cost)
{
    // Map to store <gcd, cost> pair where
    // cost is the cost to get the current gcd
    let mp = new Map();

    mp.set(0, 0);

    for (let i = 0; i < n; i++) {
        for (let [key, value] of mp.entries()){
            let gcd = __gcd(arr[i], key);

            // If current gcd value already exists in map
            if (mp.has(gcd))

                // Update the minimum cost
                // to get the current gcd
                mp.set(gcd, Math.min(mp.get(gcd), value + cost[i]));

            else
                mp.set(gcd,value + cost[i]);
        }
    }

    // If there can be no sub-set such that
    // the gcd of all the elements is 1
    if (!mp.has(1))
        return -1;
    else
        return mp.get(1);
}

function __gcd(a,b)
{
    return b == 0? a:__gcd(b, a % b);
}

// Driver code
let arr=[5, 10, 12, 1 ];
let cost=[2, 1, 2, 6 ];
let n = arr.length;
document.write(getMinCost(arr, n, cost));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```