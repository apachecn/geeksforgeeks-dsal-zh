# 计算给定和的最大不重叠子阵列

> 原文:[https://www . geesforgeks . org/count-maximum-非重叠-subarray-with-given-sum/](https://www.geeksforgeeks.org/count-maximum-non-overlapping-subarrays-with-given-sum/)

给定一个由 **N 个**整数和一个整数**目标**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到最大数量的非空非重叠[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得每个[子数组](https://www.geeksforgeeks.org/tag/subarray/)中的数组元素之和等于**目标**。

**示例:**

> **输入:** arr[] = {2，-1，4，3，6，4，5，1}，目标= 6
> **输出:** 3
> **解释:**
> 子阵{-1，4，3}，{6}和{5，1}的和等于目标(= 6)。
> 
> **输入:** arr[] = {2，2，2，2，2}，目标= 4
> T3】输出: 2

**方法:**为了获得具有和**目标**的最小不重叠子阵列，目标是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术。按照以下步骤解决问题:

1.  将到目前为止计算的所有和存储在一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **mp** 中，键作为前缀的和，直到该索引和值作为具有该和的子阵列的结束索引。
2.  如果**前缀-sum** 直到索引 **i** ，比如 **sum** ，等于**目标**，检查**sum-target**是否存在于**映射**中。
3.  如果**地图**和**MP【sum-target】= idx**中存在**sum-target**，则表示来自**【idx+1，I】**的子阵具有等于 **target** 的 **sum** 。
4.  现在对于不重叠的子阵列，维护一个附加变量**availandx**(初始设置为-1)，只有当**MP【sum–target】≥availandx**时，才能从**【idx+1，I】**获取子阵列。
5.  每当找到这样的子阵列时，增加答案并将**的值变为当前索引。**
6.  同样，对于不重叠的子阵列，贪婪地将子阵列取尽可能小总是有益的。因此，对于找到的每个**前缀和**，更新其在地图中的索引，即使它已经存在。
7.  完成上述步骤后，打印**计数**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of non-overlapping subarrays with
// sum equals to the target
int maximumSubarrays(int arr[], int N,
                     int target)
{
    // Stores the final count
    int ans = 0;

    // Next subarray should start
    // from index >= availIdx
    int availIdx = -1;

    // Tracks the prefix sum
    int cur_sum = 0;

    // Map to store the prefix sum
    // for respective indices
    unordered_map<int, int> mp;
    mp[0] = -1;

    for (int i = 0; i < N; i++) {

        cur_sum += arr[i];

        // Check if cur_sum - target is
        // present in the array or not
        if (mp.find(cur_sum - target)
                != mp.end()
            && mp[cur_sum - target]
                   >= availIdx) {

            ans++;
            availIdx = i;
        }

        // Update the index of
        // current prefix sum
        mp[cur_sum] = i;
    }

    // Return the count of subarrays
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, -1, 4, 3,
                  6, 4, 5, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Given sum target
    int target = 6;

    // Function Call
    cout << maximumSubarrays(arr, N,
                             target);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count maximum number
// of non-overlapping subarrays with
// sum equals to the target
static int maximumSubarrays(int arr[], int N,
                            int target)
{

    // Stores the final count
    int ans = 0;

    // Next subarray should start
    // from index >= availIdx
    int availIdx = -1;

    // Tracks the prefix sum
    int cur_sum = 0;

    // Map to store the prefix sum
    // for respective indices
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();
    mp.put(0, 1);

    for(int i = 0; i < N; i++)
    {
        cur_sum += arr[i];

        // Check if cur_sum - target is
        // present in the array or not
        if (mp.containsKey(cur_sum - target) &&
            mp.get(cur_sum - target) >= availIdx)
        {
            ans++;
            availIdx = i;
        }

        // Update the index of
        // current prefix sum
        mp.put(cur_sum, i);
    }

    // Return the count of subarrays
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, -1, 4, 3,
                  6, 4, 5, 1 };

    int N = arr.length;

    // Given sum target
    int target = 6;

    // Function call
    System.out.print(maximumSubarrays(arr, N,
                                      target));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count maximum number
# of non-overlapping subarrays with
# sum equals to the target
def maximumSubarrays(arr, N, target):

    # Stores the final count
    ans = 0

    # Next subarray should start
    # from index >= availIdx
    availIdx = -1

    # Tracks the prefix sum
    cur_sum = 0

    # Map to store the prefix sum
    # for respective indices
    mp = {}
    mp[0] = -1

    for i in range(N):
        cur_sum += arr[i]

        # Check if cur_sum - target is
        # present in the array or not
        if ((cur_sum - target) in mp and
          mp[cur_sum - target] >= availIdx):
            ans += 1
            availIdx = i

        # Update the index of
        # current prefix sum
        mp[cur_sum] = i

    # Return the count of subarrays
    return ans

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, -1, 4, 3,
            6, 4, 5, 1 ]

    N = len(arr)

    # Given sum target
    target = 6

    # Function call
    print(maximumSubarrays(arr, N, target))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to count maximum number
// of non-overlapping subarrays with
// sum equals to the target
static int maximumSubarrays(int []arr, int N,
                            int target)
{
  // Stores the readonly count
  int ans = 0;

  // Next subarray should start
  // from index >= availIdx
  int availIdx = -1;

  // Tracks the prefix sum
  int cur_sum = 0;

  // Map to store the prefix sum
  // for respective indices
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();
  mp.Add(0, 1);

  for(int i = 0; i < N; i++)
  {
    cur_sum += arr[i];

    // Check if cur_sum - target is
    // present in the array or not
    if (mp.ContainsKey(cur_sum - target) &&
        mp[cur_sum - target] >= availIdx)
    {
      ans++;
      availIdx = i;
    }

    // Update the index of
    // current prefix sum
    if(mp.ContainsKey(cur_sum))
      mp[cur_sum] = i;
    else
      mp.Add(cur_sum, i);
  }

  // Return the count of subarrays
  return ans;
}

// Driver Code
public static void Main(String[] args)
{   
  // Given array []arr
  int []arr = {2, -1, 4, 3,
               6, 4, 5, 1};

  int N = arr.Length;

  // Given sum target
  int target = 6;

  // Function call
  Console.Write(maximumSubarrays(arr, N,
                                 target));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count maximum number
// of non-overlapping subarrays with
// sum equals to the target
function maximumSubarrays(arr, N, target)
{
    // Stores the final count
    var ans = 0;

    // Next subarray should start
    // from index >= availIdx
    var availIdx = -1;

    // Tracks the prefix sum
    var cur_sum = 0;

    // Map to store the prefix sum
    // for respective indices
    var mp = new Map();
    mp.set(0, 1);

    for (var i = 0; i < N; i++) {

        cur_sum += arr[i];

        // Check if cur_sum - target is
        // present in the array or not
        if (mp.has(cur_sum - target)
            && mp.get(cur_sum - target)
                   >= availIdx) {

            ans++;
            availIdx = i;
        }

        // Update the index of
        // current prefix sum
        mp.set(cur_sum , i);
    }

    // Return the count of subarrays
    return ans;
}

// Driver Code

// Given array arr[]
var arr = [2, -1, 4, 3,
              6, 4, 5, 1];
var N = arr.length;

// Given sum target
var target = 6;

// Function Call
document.write( maximumSubarrays(arr, N,
                         target));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)