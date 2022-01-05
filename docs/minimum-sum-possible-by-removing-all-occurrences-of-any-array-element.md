# 通过移除任何数组元素的所有出现来最小化可能的总和

> 原文:[https://www . geeksforgeeks . org/通过移除任何数组元素的所有出现次数来最小化可能的总和/](https://www.geeksforgeeks.org/minimum-sum-possible-by-removing-all-occurrences-of-any-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过移除任何单个数组元素的所有出现来找到该数组的最小可能和。

**示例:**

> **输入:** N = 4，arr[] = {4，5，6，6}
> **输出:** 9
> **解释:**
> 所有不同的数组元素都是{4，5，6}。
> 删除所有出现的 4 将 arr[]修改为{5，6，6}
> 数组的总和= 17。
> 删除所有出现的 5 将 arr[]修改为{4，6，6}
> 数组的总和= 16。
> 删除所有出现的 6 将 arr[]修改为{4，5}
> 数组的总和= 9。
> 因此，最小可能和是 9，这是通过删除 6 的所有出现而获得的。
> 
> **输入:** N = 3，arr[] = {2，2，2 }
> T3】输出: 0

**方法:**解决这个问题的思路是先求数组中每个元素的[频率和数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的[和。然后对于每个唯一的元素，通过寻找阵列元素的**和与乘积与其频率**之间的差来寻找最小和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **mp** ，来存储数组元素的频率，初始化一个变量，比如说 **minSum** ，来存储去除所有数组元素后得到的最小和。
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**统计每个数组元素的频率并存储在**图**中，计算所有数组元素的**和**并存储在**和中。**
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并对每个键值对执行以下操作:
    *   从**和**中减去元素及其出现次数的乘积，并将获得的最小和存储在**存储器中。**
*   返回 **minSum** 作为得到的最小和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum sum after deletion
int minSum(int A[], int N)
{
    // Stores frequency of
    // array elements
    map<int, int> mp;

    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Calculate sum
        sum += A[i];

        // Update frequency of
        // the current element
        mp[A[i]]++;
    }

    // Stores the minimum
    // sum required
    int minSum = INT_MAX;

    // Traverse map
    for (auto it : mp) {

        // Find the minimum sum obtained
        minSum = min(
            minSum, sum - (it.first * it.second));
    }

    // Return minimum sum
    return minSum;
}

// Driver code
int main()
{
    // Input array
    int arr[] = { 4, 5, 6, 6 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minSum(arr, N) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find minimum sum after deletion
static int minSum(int A[], int N)
{

    // Stores frequency of
    // array elements
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Calculate sum
        sum += A[i];

        // Update frequency of
        // the current element
        if(mp.containsKey(A[i]))
        {
            mp.put(A[i], mp.get(A[i]) + 1);
        }
        else
        {
            mp.put(A[i], 1);
        }
    }

    // Stores the minimum
    // sum required
    int minSum = Integer.MAX_VALUE;

    // Traverse map
    for (Map.Entry<Integer,Integer> it : mp.entrySet())
    {

        // Find the minimum sum obtained
        minSum = Math.min(
            minSum, sum - (it.getKey() * it.getValue()));
    }

    // Return minimum sum
    return minSum;
}

// Driver code
public static void main(String[] args)
{

    // Input array
    int arr[] = { 4, 5, 6, 6 };

    // Size of array
    int N = arr.length;
    System.out.print(minSum(arr, N)+ "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find minimum sum after deletion
def minSum(A, N):

    # Stores frequency of
    # array elements
    mp = {}
    sum = 0

    # Traverse the array
    for i in range(N):

        # Calculate sum
        sum += A[i]

        # Update frequency of
        # the current element
        if A[i] in mp:
            mp[A[i]] += 1
        else:
            mp[A[i]] = 1

    # Stores the minimum
    # sum required
    minSum = float('inf')

    # Traverse map
    for it in mp:

        # Find the minimum sum obtained
        minSum = min(minSum, sum - (it * mp[it]))

    # Return minimum sum
    return minSum

# Driver code
# Input array
arr = [ 4, 5, 6, 6 ]

# Size of array
N = len(arr)
print(minSum(arr, N))

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to find minimum sum after deletion
  static int minSum(int []A, int N)
  {

    // Stores frequency of
    // array elements
    Dictionary<int,int> mp = new Dictionary<int,int>();
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Calculate sum
      sum += A[i];

      // Update frequency of
      // the current element
      if(mp.ContainsKey(A[i]))
      {
        mp[A[i]] = mp[A[i]] + 1;
      }
      else
      {
        mp.Add(A[i], 1);
      }
    }

    // Stores the minimum
    // sum required
    int minSum = int.MaxValue;

    // Traverse map
    foreach (KeyValuePair<int,int> it in mp)
    {

      // Find the minimum sum obtained
      minSum = Math.Min(
        minSum, sum - (it.Key * it.Value));
    }

    // Return minimum sum
    return minSum;
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Input array
    int []arr = { 4, 5, 6, 6 };

    // Size of array
    int N = arr.Length;
    Console.Write(minSum(arr, N)+ "\n");
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum sum after deletion
function minSum(A, N)
{

    // Stores frequency of
    // array elements
    let mp = new Map();

    let sum = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Calculate sum
        sum += A[i];

        // Update frequency of
        // the current element
        mp[A[i]]++;

        if (mp.has(A[i]))
        {
            mp.set(A[i], mp.get(A[i]) + 1)
        }
        else
        {
            mp.set(A[i], 1)
        }
    }

    // Stores the minimum
    // sum required
    let minSum = Number.MAX_SAFE_INTEGER;

    // Traverse map
    for(let it of mp)
    {

        // Find the minimum sum obtained
        minSum = Math.min(minSum,
                          sum - (it[0] * it[1]));
    }

    // Return minimum sum
    return minSum;
}

// Driver code

// Input array
let arr = [ 4, 5, 6, 6 ];

// Size of array
let N = arr.length

document.write(minSum(arr, N) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
9
```

***时间复杂度:*** *O(N)*
***辅助空间:*** *O(N)*