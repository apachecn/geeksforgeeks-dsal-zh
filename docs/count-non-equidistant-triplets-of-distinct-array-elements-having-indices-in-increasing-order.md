# 按递增顺序计数具有索引的不同数组元素的非等距三元组

> 原文:[https://www . geeksforgeeks . org/count-非等距-不同数组元素的三元组-具有递增顺序的索引/](https://www.geeksforgeeks.org/count-non-equidistant-triplets-of-distinct-array-elements-having-indices-in-increasing-order/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，该数组仅由 **0** s、 **1** s 和 **2** s 组成，任务是找到包含不同数组元素的索引 **(i，j，k)** 的三元组的计数，使得 **i < j < k** 和数组元素不等距，即**=(k–j)**。

**示例:**

> **输入:** arr[] = { 0，1，2，1 }
> **输出:** 1
> **解释:**
> 只有三元组(0，2，3)包含不同的数组元素和(2–0)！= (3 – 2).
> 因此，要求的输出为 1。
> 
> **输入:** arr[] = { 0，1，2 }
> **输出:** 0
> **说明:**
> 不存在满足条件的三元组。
> 因此，要求的输出为 0。

**方法:**思想是将数组元素 **0** s、 **1** s 和 **2** s 的索引存储在三个独立的数组中，然后找到满足给定条件的计数三元组。按照以下步骤解决问题:

*   初始化两个数组，比如 **zero_i[]** 和 **one_i[]** ，分别存储给定数组中 **0** s 和 **1** s 的索引。
*   初始化一个地图，比如说 **mp** ，来存储给定数组中 **2** s 的索引。
*   通过将 **zero_i[]** 、 **one_i[]** 和 **mp** 的大小相乘，找出所有可能的三胞胎的总数。
*   现在，减去所有违反给定条件的三胞胎。
*   为了找到这样的三元组，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **zero_i[]** 和 **one_i[]** 并尝试在地图中找到违反条件的第三个索引。
*   要找到违反条件的第三个指标，会出现以下三种情况:
    1.  第三个索引与两个索引等距，并且位于两个索引之间。
    2.  第三个索引与两个索引等距，位于第一个索引的左侧。
    3.  第三个索引与两个索引等距，位于第二个索引的右侧。
*   从三胞胎总数中删除所有这样的三胞胎。
*   最后，打印获得的三胞胎总数。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total count of
// triplets (i, j, k) such that i < j < k
// and (j - i) != (k - j)
int countTriplets(int* arr, int N)
{

    // Stores indices of 0s
    vector<int> zero_i;

    // Stores indices of 1s
    vector<int> one_i;

    // Stores indices of 2s
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current array element
        // is 0
        if (arr[i] == 0)
            zero_i.push_back(i + 1);

        // If current array element is 1
        else if (arr[i] == 1)
            one_i.push_back(i + 1);

        // If current array element
        // is 2
        else
            mp[i + 1] = 1;
    }

    // Total count of triplets
    int total = zero_i.size()
                * one_i.size() * mp.size();

    // Traverse  the array zero_i[]
    for (int i = 0; i < zero_i.size();
         i++) {

        // Traverse the array one_i[]
        for (int j = 0; j < one_i.size();
             j++) {

            // Stores index of 0s
            int p = zero_i[i];

            // Stores index of 1s
            int q = one_i[j];

            // Stores third element of
            // triplets that does not
            // satisfy the condition
            int r = 2 * p - q;

            // If r present
            // in the map
            if (mp[r] > 0)
                total--;

            // Update r
            r = 2 * q - p;

            // If r present
            // in the map
            if (mp[r] > 0)
                total--;

            // Update r
            r = (p + q) / 2;

            // If r present in the map
            // and equidistant
            if (mp[r] > 0 && abs(r - p) == abs(r - q))
                total--;
        }
    }

    // Print the obtained count
    cout << total;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 2, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    countTriplets(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the total count of
// triplets (i, j, k) such that i < j < k
// and (j - i) != (k - j)
static void countTriplets(int []arr, int N)
{

    // Stores indices of 0s
    Vector<Integer> zero_i = new Vector<Integer>();

    // Stores indices of 1s
    Vector<Integer> one_i = new Vector<Integer>();

    // Stores indices of 2s
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current array element
        // is 0
        if (arr[i] == 0)
            zero_i.add(i + 1);

        // If current array element is 1
        else if (arr[i] == 1)
            one_i.add(i + 1);

        // If current array element
        // is 2
        else
            mp.put(i + 1, 1);
    }

    // Total count of triplets
    int total = zero_i.size() *
                 one_i.size() * mp.size();

    // Traverse  the array zero_i[]
    for(int i = 0; i < zero_i.size(); i++)
    {

        // Traverse the array one_i[]
        for(int j = 0; j < one_i.size(); j++)
        {

            // Stores index of 0s
            int p = zero_i.get(i);

            // Stores index of 1s
            int q = one_i.get(j);

            // Stores third element of
            // triplets that does not
            // satisfy the condition
            int r = 2 * p - q;

            // If r present
            // in the map
            if (mp.containsKey(r) && mp.get(r) > 0)
                total--;

            // Update r
            r = 2 * q - p;

            // If r present
            // in the map
            if (mp.containsKey(r) && mp.get(r) > 0)
                total--;

            // Update r
            r = (p + q) / 2;

            // If r present in the map
            // and equidistant
            if (mp.containsKey(r) &&
                    mp.get(r) > 0 &&
                  Math.abs(r - p) == Math.abs(r - q))
                total--;
        }
    }

    // Print the obtained count
    System.out.print(total);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 2, 1 };
    int N = arr.length;

    countTriplets(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the total count of
# triplets (i, j, k) such that i < j < k
# and (j - i) != (k - j)
def countTriplets(arr, N):

    # Stores indices of 0s
    zero_i = []

    # Stores indices of 1s
    one_i = []

    # Stores indices of 2s
    mp = {}

    # Traverse the array
    for i in range(N):

        # If current array element
        # is 0
        if (arr[i] == 0):
            zero_i.append(i + 1)

        # If current array element is 1
        elif (arr[i] == 1):
            one_i.append(i + 1)

        # If current array element
        # is 2
        else:
            mp[i + 1] = 1

    # Total count of triplets
    total = len(zero_i) * len(one_i) * len(mp)

    # Traverse  the array zero_i[]
    for i in range(len(zero_i)):

        # Traverse the array one_i[]
        for j in range(len(one_i)):

            # Stores index of 0s
            p = zero_i[i]

            # Stores index of 1s
            q = one_i[j]

            # Stores third element of
            # triplets that does not
            # satisfy the condition
            r = 2 * p - q

            # If r present
            # in the map
            if (r in mp):
                total -= 1

            # Update r
            r = 2 * q - p

            # If r present
            # in the map
            if (r in mp):
                total -= 1

            # Update r
            r = (p + q) // 2

            # If r present in the map
            # and equidistant
            if ((r in mp) and abs(r - p) == abs(r - q)):
                total -= 1

    # Print the obtained count
    print (total)

# Driver Code
if __name__ == '__main__':
    arr = [0, 1, 2, 1]
    N = len(arr)
    countTriplets(arr, N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the total count of
// triplets (i, j, k) such that i < j < k
// and (j - i) != (k - j)
static void countTriplets(int []arr, int N)
{

    // Stores indices of 0s
    List<int> zero_i = new List<int>();

    // Stores indices of 1s
    List<int> one_i = new List<int>();

    // Stores indices of 2s
    Dictionary<int,
            int> mp = new Dictionary<int,
                                      int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current array element
        // is 0
        if (arr[i] == 0)
            zero_i.Add(i + 1);

        // If current array element is 1
        else if (arr[i] == 1)
            one_i.Add(i + 1);

        // If current array element
        // is 2
        else
            mp.Add(i + 1, 1);
    }

    // Total count of triplets
    int total = zero_i.Count *
                 one_i.Count * mp.Count;

    // Traverse  the array zero_i[]
    for(int i = 0; i < zero_i.Count; i++)
    {

        // Traverse the array one_i[]
        for(int j = 0; j < one_i.Count; j++)
        {

            // Stores index of 0s
            int p = zero_i[i];

            // Stores index of 1s
            int q = one_i[j];

            // Stores third element of
            // triplets that does not
            // satisfy the condition
            int r = 2 * p - q;

            // If r present
            // in the map
            if (mp.ContainsKey(r) && mp[r] > 0)
                total--;

            // Update r
            r = 2 * q - p;

            // If r present
            // in the map
            if (mp.ContainsKey(r) && mp[r] > 0)
                total--;

            // Update r
            r = (p + q) / 2;

            // If r present in the map
            // and equidistant
            if (mp.ContainsKey(r) &&
                    mp[r] > 0 &&
                  Math.Abs(r - p) == Math.Abs(r - q))
                total--;
        }
    }

    // Print the obtained count
    Console.Write(total);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 2, 1 };
    int N = arr.Length;
    countTriplets(arr, N);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the total count of
// triplets (i, j, k) such that i < j < k
// and (j - i) != (k - j)
function countTriplets(arr, N)
{

    // Stores indices of 0s
    var zero_i = [];

    // Stores indices of 1s
    var one_i = [];

    // Stores indices of 2s
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // If current array element
        // is 0
        if (arr[i] == 0)
            zero_i.push(i + 1);

        // If current array element is 1
        else if (arr[i] == 1)
            one_i.push(i + 1);

        // If current array element
        // is 2
        else
            mp.set(i + 1, 1);
    }

    // Total count of triplets
    var total = zero_i.length
                * one_i.length * mp.size;

    // Traverse  the array zero_i[]
    for (var i = 0; i < zero_i.length;
         i++) {

        // Traverse the array one_i[]
        for (var j = 0; j < one_i.length;
             j++) {

            // Stores index of 0s
            var p = zero_i[i];

            // Stores index of 1s
            var q = one_i[j];

            // Stores third element of
            // triplets that does not
            // satisfy the condition
            var r = 2 * p - q;

            // If r present
            // in the map
            if (mp.has(r))
                total--;

            // Update r
            r = 2 * q - p;

            // If r present
            // in the map
            if (mp.has(r))
                total--;

            // Update r
            r = (p + q) / 2;

            // If r present in the map
            // and equidistant
            if (mp.has(r) && Math.abs(r - p) == Math.abs(r - q))
                total--;
        }
    }

    // Print the obtained count
    document.write( total);
}

// Driver Code
var arr = [0, 1, 2, 1];
var N = arr.length;
countTriplets(arr, N);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*