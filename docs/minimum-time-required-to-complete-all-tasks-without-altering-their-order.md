# 在不改变顺序的情况下完成所有任务所需的最短时间

> 原文:[https://www . geeksforgeeks . org/在不改变订单的情况下完成所有任务所需的最短时间/](https://www.geeksforgeeks.org/minimum-time-required-to-complete-all-tasks-without-altering-their-order/)

给定一个由 **N** 字符(代表要执行的任务)和正整数 **K** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到按给定顺序完成所有给定任务所需的最短时间，使得每个任务需要一个时间单位，并且同一类型的每个任务必须以 **K 个单位**的间隔执行。

**示例:**

> **输入:** S = "ABACCA "，K = 2
> **输出:** 9
> **说明:**
> 下面是要完成的任务顺序:
> A→B→_→A→C→_→C→A .
> 因此，需要的总时间为 9 个单位。
> 
> **输入:**S =“AAAA”，K = 3
> T3】输出: 13

**方法:**给定的问题可以通过[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来解决，方法是跟踪每个任务的最后时刻，并相应地找到总的最短时间。按照以下步骤解决问题:

*   初始化一个 [hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如 **M** ，来记录每个任务的最后时刻。
*   初始化一个变量，比如说**和**为 **0** ，以存储合成的最短时间。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，并执行以下步骤:
    *   如果字符 **S[i]** 出现在 **M** 中，那么将 **S[i]** 的最后一个瞬间存储在一个变量中，比如 **t** 。
    *   如果**(ans–t)**的值最多为**K**，那么**T5】将**K –( ans–t)+1**的值加到变量 **ans** 上。**
    *   将 **M** 中**S【I】**字符的最后时刻更新为 **ans** ，并将 **ans** 的值增加 **1** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// time required to complete
// tasks without changing their order
void findMinimumTime(string tasks, int K)
{
    // Keeps track of the last
    // time instant of each task
    unordered_map<char, int> map;

    // Stores the required result
    int curr_time = 0;

    // Traverse the given string
    for (char c : tasks) {

        // Check last time instant of
        // task, if it exists before
        if (map.find(c) != map.end()) {

            // Increment the time
            // if task is within
            // the K units of time
            if (curr_time - map <= K) {

                curr_time += K - (curr_time - map) + 1;
            }
        }

        // Update the time of the
        // current task in the map
        map = curr_time;

        // Increment the time by 1
        curr_time++;
    }

    // Print the result
    cout << curr_time;
}

// Driver Code
int main()
{
    string S = "ABACCA";
    int K = 2;
    findMinimumTime(S, K);

    return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the minimum
    // time required to complete
    // tasks without changing their order
    static void findMinimumTime(
        String tasks, int K)
    {
        // Keeps track of the last
        // time instant of each task
        Map<Character, Integer> map
            = new HashMap<>();

        // Stores the required result
        int curr_time = 0;

        // Traverse the given string
        for (char c : tasks.toCharArray()) {

            // Check last time instant of
            // task, if it exists before
            if (map.containsKey(c)) {

                // Increment the time
                // if task is within
                // the K units of time
                if (curr_time
                        - map.get(c)
                    <= K) {

                    curr_time += K
                                 - (curr_time
                                    - map.get(c))
                                 + 1;
                }
            }

            // Update the time of the
            // current task in the map
            map.put(c, curr_time);

            // Increment the time by 1
            curr_time++;
        }

        // Print the result
        System.out.println(curr_time);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "ABACCA";
        int K = 2;
        findMinimumTime(S, K);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach

# Function to find the minimum
# time required to complete
# tasks without changing their order

def findMinimumTime(tasks, K):

    # Keeps track of the last
    # time instant of each task
    map = {}

    # Stores the required result
    curr_time = 0

    # Traverse the given string
    for c in tasks:

        # Check last time instant of
        # task, if it exists before
        if (c in map):

            # Increment the time
            # if task is within
            # the K units of time
            if (curr_time - map <= K):

                curr_time += K - (curr_time - map) + 1

        # Update the time of the
        # current task in the map
        map = curr_time

        # Increment the time by 1
        curr_time += 1

    # Print the result
    print(curr_time)

# Driver Code
if __name__ == "__main__":

    S = "ABACCA"
    K = 2
    findMinimumTime(S, K)

  #  This code is contributed by ukasp.
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum
// time required to complete
// tasks without changing their order
static void findMinimumTime(String tasks, int K)
{

    // Keeps track of the last
    // time instant of each task
    Dictionary<char,
               int> map = new Dictionary<char,
                                         int>();

    // Stores the required result
    int curr_time = 0;

    // Traverse the given string
    foreach (char c in tasks.ToCharArray())
    {

        // Check last time instant of
        // task, if it exists before
        if (map.ContainsKey(c))
        {

            // Increment the time
            // if task is within
            // the K units of time
            if (curr_time - map <= K)
            {
                curr_time += K - (curr_time - map) + 1;
            }

        }

        // Update the time of the
        // current task in the map
        if (!map.ContainsKey(c))
            map.Add(c, curr_time);
        else
            map = curr_time;

        // Increment the time by 1
        curr_time++;
    }

    // Print the result
    Console.WriteLine(curr_time);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "ABACCA";
    int K = 2;

    findMinimumTime(S, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to find the minimum
// time required to complete
// tasks without changing their order
function findMinimumTime(tasks, K)
{
    // Keeps track of the last
    // time instant of each task
    var map = new Map();

    // Stores the required result
    var curr_time = 0;

    // Traverse the given string
    tasks.split('').forEach(c => {

        // Check last time instant of
        // task, if it exists before
        if (map.has(c)) {

            // Increment the time
            // if task is within
            // the K units of time
            if (curr_time - map.get(c) <= K) {

                curr_time += K - (curr_time - map.get(c)) + 1;
            }
        }

        // Update the time of the
        // current task in the map
        map.set(c, curr_time);

        // Increment the time by 1
        curr_time++;
    });

    // Print the result
    document.write( curr_time);
}

// Driver Code
var S = "ABACCA";
var K = 2;
findMinimumTime(S, K);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(256)