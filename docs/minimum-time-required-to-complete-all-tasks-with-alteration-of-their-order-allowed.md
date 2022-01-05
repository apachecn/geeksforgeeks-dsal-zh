# 完成所有任务所需的最短时间，允许改变其顺序

> 原文:[https://www . geesforgeks . org/完成所有允许更改订单的任务所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-complete-all-tasks-with-alteration-of-their-order-allowed/)

给定一个由 **N** 字符(代表要执行的任务)和正整数 **K** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出以任何顺序完成所有给定任务所需的最短时间，假设每个任务需要一个时间单位，并且同一类型的每个任务必须以 **K 个单位**的间隔执行。

**示例:**

> **输入:**S =“aabbb”，K = 2
> **输出:** 8
> **说明:**
> 下面是要完成的任务顺序:
> A → B → _ → A → B → _ → A → B
> 因此，需要的总时间为 8 个单位。
> 
> **输入:**S =“aabbb”，K = 0
> T3】输出: 6

**方法:**给定的问题可以基于以下观察来解决:

*   为了在最短的时间内完成任务，想法是找到数组中出现最多的字符，并首先完成这些任务。
*   让最大出现字符为 **X** ，其频率为 **freq** 。
*   现在，要先完成 **X** 类型的任务，它们之间必须有 **K** 的差异，这就在 **X** 的任务之间留下了总数为**(freq–1)* K**的空槽。
*   然后，通过遍历其他任务来填充这些空槽，因为其他任务的频率小于或等于 **X** 的频率。

按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) ，比如说 **M** ，即[存储给定字符串 **S**](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) 中每个字符的频率。
*   初始化两个变量 **maxchar** 和 **maxfreq** ，分别存储最大出现字符及其频率。
*   [遍历给定的字符串 **S**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) ，增加地图 **M** 中**S【I】**的频率，如果大于 **maxfreq** 、**T11】，将 **maxchar** 的值更新为**S【I】**，将 **maxfreq** 的值更新为其频率。**
*   将空槽数存储在一个变量中，如 **S** ，为**(maxfreq–1)* K**。
*   [遍历 HashMap](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) 、 **M** ，对于除 **maxchar** 以外的每个字符，通过从 **S** 中减去**(maxfreq–1)**和**M【S[I]】**的[最小值](https://www.geeksforgeeks.org/stdmin-in-cpp/)来更新空槽 **S** 的值。
*   如果 **S 的值≥ 0** ，将所需的最短时间存储在变量**和**中，作为 **N** 和 **S** 的总和。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum time
// required to complete the tasks if
// the order of tasks can be changed
void findMinimumTime(string& S, int N,
                     int K)
{
    // If there is no task, print 0
    if (N == 0) {
        cout << 0;
        return;
    }

    // Store the maximum occurring
    // character and its frequency
    int maxfreq = INT_MIN;
    char maxchar;

    // Stores the frequency of each
    // character
    unordered_map<char, int> um;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Increment the frequency of
        // the current character
        um[S[i]]++;

        // Update maxfreq and maxchar
        if (um[S[i]] > maxfreq) {
            maxfreq = um[S[i]];
            maxchar = S[i];
        }
    }

    // Store the number of empty slots
    int emptySlots = (maxfreq - 1) * K;

    // Traverse the hashmap, um
    for (auto& it : um) {

        if (it.first == maxchar)
            continue;

        // Fill the empty slots
        emptySlots -= min(it.second,
                          maxfreq - 1);
    }

    // Store the required result
    int ans = N + max(0, emptySlots);

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    string S = "AAABBB";
    int K = 2;
    int N = S.length();
    findMinimumTime(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
import java.util.Map;

class GFG{

// Function to find the minimum time
// required to complete the tasks if
// the order of tasks can be changed
static void findMinimumTime(String S, int N, int K)
{

    // If there is no task, print 0
    if (N == 0)
    {
        System.out.println(0);
        return;
    }

    // Store the maximum occurring
    // character and its frequency
    int maxfreq = Integer.MIN_VALUE;
    char maxchar = ' ';

    // Stores the frequency of each
    // character
    HashMap<Character, Integer> um = new HashMap<>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Increment the frequency of
        // the current character
        um.put(S.charAt(i),
               um.getOrDefault(S.charAt(i), 0) + 1);

        // Update maxfreq and maxchar
        if (um.get(S.charAt(i)) > maxfreq)
        {
            maxfreq = um.get(S.charAt(i));
            maxchar = S.charAt(i);
        }
    }

    // Store the number of empty slots
    int emptySlots = (maxfreq - 1) * K;

    // Traverse the hashmap, um
    for(Map.Entry<Character, Integer> it :
        um.entrySet())
    {
        if (it.getKey() == maxchar)
            continue;

        // Fill the empty slots
        emptySlots -= Math.min(
            it.getValue(), maxfreq - 1);
    }

    // Store the required result
    int ans = N + Math.max(0, emptySlots);

    // Print the result
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    String S = "AAABBB";
    int K = 2;
    int N = S.length();

    findMinimumTime(S, N, K);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys
from collections import defaultdict

# Function to find the minimum time
# required to complete the tasks if
# the order of tasks can be changed
def findMinimumTime(S, N, K):

    # If there is no task, print 0
    if (N == 0):
        print(0)
        return

    # Store the maximum occurring
    # character and its frequency
    maxfreq = -sys.maxsize

    # Stores the frequency of each
    # character
    um = defaultdict(int)

    # Traverse the string S
    for i in range(N):

        # Increment the frequency of
        # the current character
        um[S[i]] += 1

        # Update maxfreq and maxchar
        if (um[S[i]] > maxfreq):
            maxfreq = um[S[i]]
            maxchar = S[i]

    # Store the number of empty slots
    emptySlots = (maxfreq - 1) * K

    # Traverse the hashmap, um
    for it in um:
        if (it == maxchar):
            continue

        # Fill the empty slots
        emptySlots -= min(um[it],
                          maxfreq - 1)

    # Store the required result
    ans = N + max(0, emptySlots)

    # Print the result
    print(ans)

# Driver Code
if __name__ == "__main__":

    S = "AAABBB"
    K = 2
    N = len(S)

    findMinimumTime(S, N, K)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum time
// required to complete the tasks if
// the order of tasks can be changed
static void findMinimumTime(string S, int N, int K)
{

    // If there is no task, print 0
    if (N == 0)
    {
        Console.Write(0);
        return;
    }

    // Store the maximum occurring
    // character and its frequency
    int maxfreq = Int32.MinValue;
    char maxchar = ' ';

    // Stores the frequency of each
    // character
    Dictionary<char,
               int> um = new Dictionary<char,
                                        int>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // Increment the frequency of
        // the current character
        if (um.ContainsKey(S[i]))
            um[S[i]]++;
        else
            um.Add(S[i], 1);

        // Update maxfreq and maxchar
        if (um.ContainsKey(S[i]) &&
            um[S[i]] > maxfreq)
        {
            maxfreq = um[S[i]];
            maxchar = S[i];
        }
    }

    // Store the number of empty slots
    int emptySlots = (maxfreq - 1) * K;

    // Traverse the hashmap, um
    foreach(KeyValuePair<char, int> kvp in um)
    {

        if (kvp.Key == maxchar)
            continue;

        // Fill the empty slots
        emptySlots -= Math.Min(kvp.Value,
                               maxfreq - 1);
    }

    // Store the required result
    int ans = N + Math.Max(0, emptySlots);

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    string S = "AAABBB";
    int K = 2;
    int N = S.Length;

    findMinimumTime(S, N, K);
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum time
// required to complete the tasks if
// the order of tasks can be changed
function findMinimumTime(s, N, K)
{

    // If there is no task, print 0
    if (N == 0)
    {
        document.write(0);
        return;
    }

    // Store the maximum occurring
    // character and its frequency
    let maxfreq = Number.MIN_SAFE_INTEGER;
    let maxchar;

    // Stores the frequency of each
    // character
    let um = new Map();

    // Traverse the string S
    for(let i = 0; i < N; i++)
    {

        // Increment the frequency of
        // the current character
        if (um.has(s[i]))
        {
           um.set(s[i], um.get(s[i]) + 1)
        }
        else
        {
            um.set(s[i], 1)
        }

        // Update maxfreq and maxchar
        if (um.get(S[i]) > maxfreq)
        {
            maxfreq = um.get(S[i]);
            maxchar = S[i];
        }
    }

    // Store the number of empty slots
    let emptySlots = (maxfreq - 1) * K;

    // Traverse the hashmap, um
    for(let it of um)
    {
        if (it[0] == maxchar)
            continue;

        // Fill the empty slots
        emptySlots -= Math.min(
            it[1], maxfreq - 1);
    }

    // Store the required result
    let ans = N + Math.max(0, emptySlots);

    // Print the result
    document.write(ans);
}

// Driver Code
let S = "AAABBB";
let K = 2;
let N = S.length;

findMinimumTime(S, N, K);

// This code is contributed by _saurabh_jaiswal.

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(256)