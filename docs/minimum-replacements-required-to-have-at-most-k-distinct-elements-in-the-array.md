# 阵列中最多需要 K 个不同元素的最小替换数

> 原文:[https://www . geesforgeks . org/最少替换-最多需要有 k 个不同的阵列元素/](https://www.geeksforgeeks.org/minimum-replacements-required-to-have-at-most-k-distinct-elements-in-the-array/)

给定一个由 **N** 正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】【】**，任务是找到需要被其他数组元素替换的最小数组元素数，使得该数组最多包含 **K** 个不同的元素。

> **输入:** arr[] = { 1，1，2，2，5 }，K = 2
> **输出:** 1
> **解释:**
> 将 arr[4]替换为 arr[0]将 arr[]修改为{ 1，1，2，2，1 }
> arr[]的不同数组元素为{ 1，2 }
> 因此，需要的输出为 1。
> 
> **输入:** arr[] = { 5，1，3，2，4，1，1，2，3，4 }，K = 3
> **输出:** 3
> **解释:**
> 用 arr[1]替换 arr[0]将 arr[]修改为{ 1，1，3，2，4，1，1，2，3，4 }
> 用 arr[0]替换 arr[2]将 arr[]修改为{ 1，1，2，4，1，1 2，4，1，1，2，1，4 }
> arr[]的不同数组元素为{ 1，2，4 }
> 因此，所需的输出为 3。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。想法是用较高频率的阵列元件代替较小频率的阵列元件。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** ，来存储每个不同数组元素的[频率。](https://www.geeksforgeeks.org/c-program-to-count-frequency-of-each-element-in-an-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[将数组中每个不同元素的频率存储到地图](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)中。
*   [使用地图的关键值作为 **i** 遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，将**MP【I】**的值插入一个数组，比如 **Freq[]** 。
*   [按降序排列数组**Freq[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   初始化一个变量，比如 **cntMin** ，来存储需要替换的数组元素的最小数量，使得数组中不同元素的数量最多为 **K** 。
*   初始化一个变量，比如说 **len** ，来存储数组的大小 **Freq[]** 。
*   使用变量 **i** 迭代范围**【K，len】**。对于每一个**I<sup>th</sup>T7】值，更新**cntMin+= Freq【I】**。**
*   最后，打印 **cntMin** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of array
// elements required to be replaced such that
// count of distinct elements is at most K
int min_elements(int arr[], int N, int K)
{

    // Store the frequency of each
    // distinct element of the array
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        mp[arr[i]]++;
    }

    // Store frequency of each distinct
    // element of the array
    vector<int> Freq;

    // Traverse the map
    for (auto it : mp) {

        // Stores key of the map
        int i = it.first;

        // Insert mp[i] into Freq[]
        Freq.push_back(mp[i]);
    }

    // Sort Freq[] in descending order
    sort(Freq.rbegin(), Freq.rend());

    // Stores size of Freq[]
    int len = Freq.size();

    // If len is less than
    // or equal to K
    if (len <= K) {

        return 0;
    }

    // Stores minimum count of array elements
    // required to be replaced such that
    // count of distinct elements is at most K
    int cntMin = 0;

    // Iterate over the range [K, len]
    for (int i = K; i < len; i++) {

        // Update cntMin
        cntMin += Freq[i];
    }

    return cntMin;
}

// Driver Code
int main()
{
    int arr[] = { 5, 1, 3, 2, 4, 1, 1, 2, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 3;
    cout << min_elements(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find minimum count of array
  // elements required to be replaced such that
  // count of distinct elements is at most K
  static int min_elements(int arr[], int N, int K)
  {

    // Store the frequency of each
    // distinct element of the array
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Update frequency
      // of arr[i]
      if(mp.containsKey(arr[i]))
      {
        mp.put(arr[i], mp.get(arr[i])+1);
      }
      else
      {
        mp.put(arr[i], 1);
      }
    }

    // Store frequency of each distinct
    // element of the array
    Vector<Integer> Freq = new Vector<Integer>();

    // Traverse the map
    for (Map.Entry<Integer,Integer> it : mp.entrySet())
    {

      // Stores key of the map
      int i = it.getKey();

      // Insert mp[i] into Freq[]
      Freq.add(mp.get(i));
    }

    // Sort Freq[] in descending order
    Collections.sort(Freq,Collections.reverseOrder());

    // Stores size of Freq[]
    int len = Freq.size();

    // If len is less than
    // or equal to K
    if (len <= K)
    {
      return 0;
    }

    // Stores minimum count of array elements
    // required to be replaced such that
    // count of distinct elements is at most K
    int cntMin = 0;

    // Iterate over the range [K, len]
    for (int i = K; i < len; i++)
    {

      // Update cntMin
      cntMin += Freq.get(i);
    }
    return cntMin;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 5, 1, 3, 2, 4, 1, 1, 2, 3, 4 };
    int N = arr.length;
    int K = 3;
    System.out.print(min_elements(arr, N, K));
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum count of array
# elements required to be replaced such that
# count of distinct elements is at most K
def min_elements(arr, N, K) :

    # Store the frequency of each
    # distinct element of the array
    mp = {}

    # Traverse the array
    for i in range(N) :

        # Update frequency
        # of arr[i]
        if arr[i] in mp :
            mp[arr[i]] += 1
        else :
            mp[arr[i]] = 1

    # Store frequency of each distinct
    # element of the array
    Freq = []

    # Traverse the map
    for it in mp :

        # Stores key of the map
        i = it

        # Insert mp[i] into Freq[]
        Freq.append(mp[i])

    # Sort Freq[] in descending order
    Freq.sort()
    Freq.reverse()

    # Stores size of Freq[]
    Len = len(Freq)

    # If len is less than
    # or equal to K
    if (Len <= K) :
        return 0

    # Stores minimum count of array elements
    # required to be replaced such that
    # count of distinct elements is at most K
    cntMin = 0

    # Iterate over the range [K, len]
    for i in range(K, Len) :

        # Update cntMin
        cntMin += Freq[i]

    return cntMin

  # Driver code
arr = [ 5, 1, 3, 2, 4, 1, 1, 2, 3, 4 ]
N = len(arr)
K = 3;
print(min_elements(arr, N, K))

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum count of array
// elements required to be replaced such that
// count of distinct elements is at most K
static int min_elements(int []arr, int N, int K)
{

    // Store the frequency of each
    // distinct element of the array
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        if (mp.ContainsKey(arr[i]))
        {
            mp[arr[i]] = mp[arr[i]] + 1;
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Store frequency of each distinct
    // element of the array
    List<int> Freq = new List<int>();

    // Traverse the map
    foreach (KeyValuePair<int, int> it in mp)
    {

        // Stores key of the map
        int i = it.Key;

        // Insert mp[i] into Freq[]
        Freq.Add(mp[i]);
    }

    // Sort Freq[] in descending order
    Freq.Sort();
    Freq.Reverse();

    // Stores size of Freq[]
    int len = Freq.Count;

    // If len is less than
    // or equal to K
    if (len <= K)
    {
        return 0;
    }

    // Stores minimum count of array elements
    // required to be replaced such that
    // count of distinct elements is at most K
    int cntMin = 0;

    // Iterate over the range [K, len]
    for(int i = K; i < len; i++)
    {

        // Update cntMin
        cntMin += Freq[i];
    }
    return cntMin;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 1, 3, 2, 4, 1, 1, 2, 3, 4 };
    int N = arr.Length;
    int K = 3;

    Console.Write(min_elements(arr, N, K));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find minimum count of array
// elements required to be replaced such that
// count of distinct elements is at most K
function min_elements(arr, N, K)
{

    // Store the frequency of each
    // distinct element of the array
    let mp = new Map();

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        if (mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else
        {
            mp.set(arr[i], 1)
        }
    }

    // Store frequency of each distinct
    // element of the array
    let Freq = [];

    // Traverse the map
    for(let it of mp)
    {

        // Stores key of the map
        let i = it[0];

        // Insert mp[i] into Freq[]
        Freq.push(mp.get(i));
    }

    // Sort Freq[] in descending order
    Freq.sort((a, b) => b - a);

    // Stores size of Freq[]
    let len = Freq.length;

    // If len is less than
    // or equal to K
    if (len <= K)
    {
        return 0;
    }

    // Stores minimum count of array elements
    // required to be replaced such that
    // count of distinct elements is at most K
    let cntMin = 0;

    // Iterate over the range [K, len]
    for(let i = K; i < len; i++)
    {

        // Update cntMin
        cntMin += Freq[i];
    }
    return cntMin;
}

// Driver Code
let arr = [ 5, 1, 3, 2, 4,
            1, 1, 2, 3, 4 ];
let N = arr.length;
let K = 3;

document.write(min_elements(arr, N, K));

// This code contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*