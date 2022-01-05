# 查询计数由给定整数组成的子阵作为最后一个元素

> 原文:[https://www . geeksforgeeks . org/查询计数子数组-由给定整数作为最后一个元素组成/](https://www.geeksforgeeks.org/queries-to-count-subarrays-consisting-of-given-integer-as-the-last-element/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个由 **Q** 查询组成的数组**查询【】**，每个 **i <sup>th</sup>** 查询的任务是计算以**查询【I】**作为最后一个元素的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量。
***注:**子阵列会因 **X.*** 的不同出现而被视为不同

**示例:**

> **输入:** arr[] = {1，5，4，5，6}，Q **=** 3，查询[] = {1，4，5}
> **输出:** 1 3 6
> **说明:**
> 查询 1:以 1 为最后一个元素的子阵为{1}
> 查询 2:以 4 为最后一个元素的子阵为{4}、{5，4}、{1，5，4}。因此，计数为 3。
> 查询 3:以 5 为最后一个元素的子阵为{1，5}、{5}、{1，5，4，5}、{5}、{4，5}、{5，4，5}。因此，计数为 6。
> 。
> **输入:** arr[] = {1，2，3，3}，Q = 3，查询[]={3，1，2}
> **输出:** 7 1 2

**天真方法:**解决问题最简单的方法是[为每个查询生成所有的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，检查它是否由 **X** 作为最后一个元素组成。
***时间复杂度:**O(q×N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，想法是使用 Hashing。[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并针对每个数组元素**arr【I】**，搜索其在数组中的出现。对于每个索引，说 **idx** ，其中 **arr[i]** 被找到，将 **(idx+1)** 添加到以 **arr[i]** 作为最后一个元素的子阵列的计数中。

按照以下步骤解决问题:

*   初始化一个[无序图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)，比如 **mp，**来存储以 **X** 作为最后一个元素的子阵的数量。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个整数 **arr[i]** ，将**MP【arr[I]】**增加 **(i+1)。**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **查询[]** ，对于每个查询**查询**，打印 **mp【查询[i]】。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform queries to count the
// number of subarrays having given numbers
// as the last integer
int subarraysEndingWithX(
    int arr[], int N,
    int query[], int Q)
{
    // Stores the number of subarrays having
    // x as the last element
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores current array element
        int val = arr[i];

        // Add contribution of subarrays
        // having arr[i] as last element
        mp[val] += (i + 1);
    }

    // Traverse the array of queries
    for (int i = 0; i < Q; i++) {

        int q = query[i];

        // Print the count of subarrays
        cout << mp[q] << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 5, 4, 5, 6 };

    // Number of queries
    int Q = 3;

    // Array of queries
    int query[] = { 1, 4, 5 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    subarraysEndingWithX(arr, N, query, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to perform queries to count the
// number of subarrays having given numbers
// as the last integer
static void subarraysEndingWithX(
    int arr[], int N,
    int query[], int Q)
{
    // Stores the number of subarrays having
    // x as the last element
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores current array element
        int val = arr[i];

        // Add contribution of subarrays
        // having arr[i] as last element
        if(mp.containsKey(val))
            mp.put(val, mp.get(val)+(i+1));
        else
            mp.put(val, i+1);
    }

    // Traverse the array of queries
    for (int i = 0; i < Q; i++) {

        int q = query[i];

        // Print the count of subarrays
        System.out.print(mp.get(q)+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 1, 5, 4, 5, 6 };

    // Number of queries
    int Q = 3;

    // Array of queries
    int query[] = { 1, 4, 5 };

    // Size of the array
    int N = arr.length;

    subarraysEndingWithX(arr, N, query, Q);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to perform queries to count the
# number of subarrays having given numbers
# as the last integer
def subarraysEndingWithX(arr, N, query, Q):

    # Stores the number of subarrays having
    # x as the last element
    mp = {}

    # Traverse the array
    for i in range(N):

        # Stores current array element
        val = arr[i]

        # Add contribution of subarrays
        # having arr[i] as last element
        if val in mp:
            mp[val] += (i + 1)
        else:
            mp[val] = mp.get(val, 0) + (i + 1);

    # Traverse the array of queries
    for i in range(Q):
        q = query[i]

        # Print the count of subarrays
        print(mp[q],end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr =  [1, 5, 4, 5, 6]

    # Number of queries
    Q = 3

    # Array of queries
    query  = [1, 4, 5]

    # Size of the array
    N = len(arr)
    subarraysEndingWithX(arr, N, query, Q)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to perform queries to count the
    // number of subarrays having given numbers
    // as the last integer
    static void subarraysEndingWithX(int[] arr, int N,
                                     int[] query, int Q)
    {

        // Stores the number of subarrays having
        // x as the last element
        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Stores current array element
            int val = arr[i];

            // Add contribution of subarrays
            // having arr[i] as last element
            if (mp.ContainsKey(val))
                mp[val] = mp[val] + (i + 1);
            else
                mp[val] = i + 1;
        }

        // Traverse the array of queries
        for (int i = 0; i < Q; i++)
        {
            int q = query[i];

            // Print the count of subarrays
            Console.Write(mp[q] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {

        // Given array
        int[] arr = { 1, 5, 4, 5, 6 };

        // Number of queries
        int Q = 3;

        // Array of queries
        int[] query = { 1, 4, 5 };

        // Size of the array
        int N = arr.Length;
        subarraysEndingWithX(arr, N, query, Q);
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to perform queries to count the
// number of subarrays having given numbers
// as the last leteger
function subarraysEndingWithX(arr, N, query, Q)
{
    // Stores the number of subarrays having
    // x as the last element
    let mp = new Map();

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // Stores current array element
        let val = arr[i];

        // Add contribution of subarrays
        // having arr[i] as last element
        if(mp.has(val))
            mp.set(val, mp.get(val)+(i+1));
        else
            mp.set(val, i+1);
    }

    // Traverse the array of queries
    for (let i = 0; i < Q; i++) {

        let q = query[i];

        // Prlet the count of subarrays
       document.write(mp.get(q)+ " ");
    }
}

// Driver Code

    // Given array
    let arr = [ 1, 5, 4, 5, 6 ];

    // Number of queries
    let Q = 3;

    // Array of queries
    let query = [ 1, 4, 5 ];

    // Size of the array
    let N = arr.length;

    subarraysEndingWithX(arr, N, query, Q);

</script>         
```

**Output:** 

```
1 3 6
```

***时间复杂度:** O(Q + N)*
***辅助空间:** O(N)*