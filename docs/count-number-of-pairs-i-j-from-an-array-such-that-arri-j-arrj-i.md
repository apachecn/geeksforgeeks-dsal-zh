# 计算数组中的对(I，j)的数量，使得 arr[i] * j = arr[j] * i

> 原文:[https://www . geesforgeks . org/count-对数-I-j-from-a-arri-j-arrj-I/](https://www.geeksforgeeks.org/count-number-of-pairs-i-j-from-an-array-such-that-arri-j-arrj-i/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算数组中可能的对 **(i，j)** 的数量，使得 **arr[j] * i = arr[i] * j** ，其中 **1 ≤ i < j ≤ N.**

**示例:**

> **输入:** arr[] = {1，3，5，6，5}
> **输出:** 2
> **说明:**
> 对(1，5)满足条件，因为 arr[1] * 5 = arr[5] * 1。
> 对(2，4)满足条件，因为 arr[2] * 4 = arr[4] * 2。
> 因此，满足给定条件的对的总数是 2。
> 
> **输入:** arr[] = {2，1，3 }
> T3】输出: 0

**天真方法:**解决问题最简单的方法是[从数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并检查每个对，给定的条件是否满足。增加满足条件的对的计数。最后，打印所有这些对的计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**为了优化上述方法，该思想基于给定等式 **arr[i] * j = arr[j] * i** 到 **arr[i] / i = arr[j] / j** 的重排。
按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，以存储满足给定条件的对的总计数。
*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如 **mp，**来计算值**arr【I/I】**的频率。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并更新[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中**arr【I/I】**的频率。
*   打印**数**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs from an
// array satisfying given conditions
void countPairs(int arr[], int N)
{
    // Stores the total
    // count of pairs
    int count = 0;

    // Stores count of a[i] / i
    unordered_map<double, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        double val = 1.0 * arr[i];
        double idx = 1.0 * (i + 1);

        // Updating count
        count += mp[val / idx];

        // Update frequency
        // in the Map
        mp[val / idx]++;
    }

    // Print count of pairs
    cout << count;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 3, 5, 6, 5 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to count pairs
    // satisfying given conditions
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count pairs from an
// array satisfying given conditions
static void countPairs(int []arr, int N)
{

    // Stores the total
    // count of pairs
    int count = 0;

    // Stores count of a[i]/i
    Map<Double, Integer>  mp
            = new HashMap<Double, Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        Double val = 1.0 * arr[i];
        Double idx = 1.0 * (i + 1);

        // Updating count
        if (mp.containsKey(val / idx))
            count += mp.get(val/idx);

        // Update frequency
        // in the Map
        if (mp.containsKey(val / idx))
            mp.put(val / idx, mp.getOrDefault(val / idx, 0) + 1);
        else
            mp.put(val/idx, 1);
    }

    // Print count of pairs
    System.out.print(count);
}

// Driver Code
public static void main(String args[])
{

    // Given array
    int []arr = { 1, 3, 5, 6, 5 };

    // Size of the array
    int N = arr.length;

    // Function call to count pairs
    // satisfying given conditions
    countPairs(arr, N);
}
}

// This code is contributed by ipg2016107.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to count pairs from an
# array satisfying given conditions
def countPairs(arr, N):

    # Stores the total
    # count of pairs
    count = 0

    # Stores count of a[i] / i
    mp = defaultdict(int)

    # Traverse the array
    for i in range(N):
        val = 1.0 * arr[i]
        idx = 1.0 * (i + 1)

        # Updating count
        count += mp[val / idx]

        # Update frequency
        # in the Map
        mp[val / idx] += 1

    # Print count of pairs
    print(count)

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [1, 3, 5, 6, 5]

    # Size of the array
    N = len(arr)

    # Function call to count pairs
    # satisfying given conditions
    countPairs(arr, N)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count pairs from an
// array satisfying given conditions
static void countPairs(int []arr, int N)
{

    // Stores the total
    // count of pairs
    int count = 0;

    // Stores count of a[i]/i
    Dictionary<double,
               int> mp = new Dictionary<double,
                                        int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        double val = 1.0 * arr[i];
        double idx = 1.0 * (i + 1);

        // Updating count
        if (mp.ContainsKey(val / idx))
            count += mp[val/idx];

        // Update frequency
        // in the Map
        if (mp.ContainsKey(val / idx))
            mp[val / idx]++;
        else
            mp[val/idx] = 1;
    }

    // Print count of pairs
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{

    // Given array
    int []arr = { 1, 3, 5, 6, 5 };

    // Size of the array
    int N = arr.Length;

    // Function call to count pairs
    // satisfying given conditions
    countPairs(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count pairs from an
// array satisfying given conditions
function countPairs(arr, N)
{
    // Stores the total
    // count of pairs
    var count = 0;

    // Stores count of a[i] / i
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {
        var val = 1.0 * arr[i];
        var idx = 1.0 * (i + 1);

        // Updating count
        count += mp.has(val/idx)?mp.get(val/idx):0

        // Update frequency
        // in the Map
        if(mp.has(val/idx))
            mp.set(val/idx, mp.get(val/idx)+1)
        else
            mp.set(val/idx, 1)

    }

    // Print count of pairs
    document.write( count);
}

// Driver Code
// Given array
var arr = [1, 3, 5, 6, 5];

// Size of the array
var N = arr.length;

// Function call to count pairs
// satisfying given conditions
countPairs(arr, N);

// This code is contributed by itsok.

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)