# 每个数组元素出现的索引的绝对差之和

> 原文:[https://www . geeksforgeeks . org/每个数组元素出现次数的绝对差值总和/](https://www.geeksforgeeks.org/sum-of-absolute-differences-of-indices-of-occurrences-of-each-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，每个数组元素 **arr[i]** 的任务是打印所有可能索引 **j** 的**| I–j |**的和，使得 **arr[i] = arr[j]** 。

**示例:**

> ***输入:** arr[] = {1，3，1，1，2}*
> ***输出:** 5 0 3 4 0*
> ***解释:***
> *对于 arr[0]，求和= | 0–0 |+| 0–2 |+| 0–3 | = 5。*
> *对于 arr[1]，sum = | 1–1 | = 0。*
> *为 arr[2]，和= | 2–0 |+| 2–2 |+| 2–3 | = 3。*
> *对于 arr[3]，sum = | 3–0 |+| 3–2 |+| 3–3 | = 4。*
> *为 arr[4]，求和= | 4–4 | = 0。*
> *因此，所需输出为 5 0 3 4 0。*
> 
> **输入:** arr[] = {1，1，1}
> **输出:** 3 2 3

**天真方法:**最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素**arr【I】**(**0≤I≤N**)，[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，检查**arr【I】**是否与**arr【j】**(**0≤j≤N**)相同。如果发现为真，将**ABS(I–j)**加到总和中，打印每个数组元素的总和。

***时间复杂度:** O(N <sup>2</sup> )其中 **N** 是给定数组的大小。*
***辅助空间:** O(N)*

**高效途径:**思路是利用[地图数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)对上述途径进行优化。按照以下步骤解决问题:

1.  初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储数组中每个唯一元素的重复索引的[向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)。
2.  [遍历从 **i = 0 到 N–1**的给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素 **arr[i]** ，用 **0** 和[初始化和，遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **映射【arr[I]】**，该映射存储元素 **arr[i]** 出现的索引。
3.  对于向量中存在的每个值 **j** ，将总和增加**ABS(I–j)**。
4.  遍历向量后，将元素的和存储在索引 **i** 处，并打印和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find sum of differences
// of indices of occurrences of each
// unique array element
void sum(int arr[], int n)
{
    // Stores indices of each
    // array element
    map<int, vector<int> > mp;

    // Store the indices
    for (int i = 0; i < n; i++) {
        mp[arr[i]].push_back(i);
    }

    // Stores the sums
    int ans[n];

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Find sum for each element
        int sum = 0;

        // Iterate over the Map
        for (auto it : mp[arr[i]]) {

            // Calculate sum of
            // occurrences of arr[i]
            sum += abs(it - i);

        }

        // Store sum for
        // current element
        ans[i] = sum;
    }

    // Print answer for each element
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
    return;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 3, 1, 1, 2 };

    // Given size
    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    sum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find sum of differences
// of indices of occurrences of each
// unique array element
static void sum(int arr[], int n)
{

    // Stores indices of each
    // array element
    HashMap<Integer, Vector<Integer>> mp = new HashMap<>();

    // Store the indices
    for(int i = 0; i < n; i++)
    {
        Vector<Integer> v = new Vector<>();
        v.add(i);

        if (mp.containsKey(arr[i]))
            v.addAll(mp.get(arr[i]));

        mp.put(arr[i], v);
    }

    // Stores the sums
    int []ans = new int[n];

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Find sum for each element
        int sum = 0;

        // Iterate over the Map
        for(int it : mp.get(arr[i]))
        {

            // Calculate sum of
            // occurrences of arr[i]
            sum += Math.abs(it - i);
        }

        // Store sum for
        // current element
        ans[i] = sum;
    }

    // Print answer for each element
    for(int i = 0; i < n; i++)
    {
        System.out.print(ans[i] + " ");
    }
    return;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 3, 1, 1, 2 };

    // Given size
    int n = arr.length;

    // Function call
    sum(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find sum of differences
# of indices of occurrences of each
# unique array element
def sum_i(arr, n):

    # Stores indices of each
    # array element
    mp = defaultdict(lambda : [])

    # Store the indices
    for i in range(n):
        mp[arr[i]].append(i)

    # Stores the sums
    ans = [0] * n

    # Traverse the array
    for i in range(n):

        # Find sum for each element
        sum = 0

        # Iterate over the Map
        for it in mp[arr[i]]:

            # Calculate sum of
            # occurrences of arr[i]
            sum += abs(it - i)

            # Store sum for
            # current element
            ans[i] = sum

    # Print answer for each element
    for i in range(n):
        print(ans[i], end = " ")

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 3, 1, 1, 2 ]

    # Given size
    n = len(arr)

    # Function Call
    sum_i(arr, n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find sum of differences
// of indices of occurrences of each
// unique array element
static void sum(int []arr, int n)
{

    // Stores indices of each
    // array element
    Dictionary<int,
          List<int>> mp = new Dictionary<int,
                                    List<int>>();

    // Store the indices
    for(int i = 0; i < n; i++)
    {
        List<int> v = new List<int>();
        v.Add(i);

        if (mp.ContainsKey(arr[i]))
            v.AddRange(mp[arr[i]]);

        mp[arr[i]]= v;
    }

    // Stores the sums
    int []ans = new int[n];

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Find sum for each element
        int sum = 0;

        // Iterate over the Map
        foreach(int it in mp[arr[i]])
        {

            // Calculate sum of
            // occurrences of arr[i]
            sum += Math.Abs(it - i);
        }

        // Store sum for
        // current element
        ans[i] = sum;
    }

    // Print answer for each element
    for(int i = 0; i < n; i++)
    {
        Console.Write(ans[i] + " ");
    }
    return;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 3, 1, 1, 2 };

    // Given size
    int n = arr.Length;

    // Function call
    sum(arr, n);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find sum of differences
// of indices of occurrences of each
// unique array element
function sum(arr, n)
{
    // Stores indices of each
    // array element
    var mp = new Map();

    // Store the indices
    for (var i = 0; i < n; i++) {
        if(mp.has(arr[i]))
        {
            var tmp = mp.get(arr[i]);
            tmp.push(i);
            mp.set(arr[i], tmp);
        }
        else
        {
            mp.set(arr[i], [i]);
        }
    }

    // Stores the sums
    var ans = Array(n);

    // Traverse the array
    for (var i = 0; i < n; i++) {

        // Find sum for each element
        var sum = 0;

        // Iterate over the Map
        mp.get(arr[i]).forEach(it => {

            // Calculate sum of
            // occurrences of arr[i]
            sum += Math.abs(it - i);

        });

        // Store sum for
        // current element
        ans[i] = sum;
    }

    // Print answer for each element
    for (var i = 0; i < n; i++) {
        document.write( ans[i] + " ");
    }
    return;
}

// Driver Code

// Given array
var arr = [1, 3, 1, 1, 2];

// Given size
var n = arr.length;

// Function call
sum(arr, n);

</script>
```

**Output:** 

```
5 0 3 4 0
```

***时间复杂度:** O(N * L)其中 **N** 是给定数组的大小， **L** 是任意数组元素的最大频率。*
***辅助空间:** O(N)*