# 计数递减到使所有数组元素相等所需的最近的较小元素

> 原文:[https://www . geesforgeks . org/count-递减到最近的较小元素-要求使所有数组元素相等/](https://www.geeksforgeeks.org/count-decrements-to-nearest-smaller-element-required-to-make-all-array-elements-equal/)

给定一个由非负整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出使所有数组元素相等所需的运算次数。在每个操作中，任何数组元素都可以更改为其最近的较小数组元素。

**例:**

> **输入:** arr[] = {2，5，4，3，5，4}
> **输出:** 11
> **说明:**
> 第一步:将所有 5s 替换为 4s。因此，arr[] = {2，4，4，3，4，4}。操作次数= 2
> 第二步:用 3s 替换所有 4。因此，arr[] = {2，3，3，3，3，3}。操作次数= 4
> 步骤 3:用 2s 替换所有 3s。因此，arr[] = {2，2，2，2，2，2}。操作数= 5
> 因此，操作总数= 11
> 
> **输入:** arr[] = {2，2，2 }
> T3】输出: 0

**方法:**想法是使用[一个排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)和[一个地图数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。按照以下步骤解决问题:

1.  初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储每个数组元素的[频率，除了最小元素**键(K)** 是唯一元素的集合，**值(V)** 是它们的频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
2.  [根据关键点按降序排列](https://www.geeksforgeeks.org/sorting-algorithms/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。
3.  用 **0** 初始化两个变量 **ans** 和 **prev_val** ，分别存储当前答案和[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
4.  现在迭代[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)并将每个元素的对应频率与 **prev_val** 一起添加到 **ans** 中，作为 **ans = ans + (freq) + prev_val**
5.  迭代[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)时，每次按当前元素的频率递增 **prev_val** 。
6.  遍历完**地图**后，打印**和**作为最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the minimum number of
// decrements to make all elements equals
int MinimumNoOfOperations(int arr[], int n)
{

    // Find minimum element
    int min_ele = INT_MAX;
    for (int i = 0; i < n; ++i) {
        min_ele = min(min_ele, arr[i]);
    }

    // Stores frequencies of array elements
    map<int, int, greater<int> > mp;

    // Update frequencies in the Map
    for (int i = 0; i < n; ++i) {

        if (arr[i] == min_ele)
            continue;
        else
            mp[arr[i]]++;
    }

    // Iterate the map
    map<int, int>::iterator it;

    // Stores the count of
    // decrements at each iteration
    int prev_val = 0;

    // Stores the total
    // count of decrements
    int ans = 0;

    // Calculate the number of decrements
    for (it = mp.begin(); it != mp.end();
         ++it) {

        ans += (it->second + prev_val);
        prev_val += it->second;
    }

    // Return minimum operations
    return ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 5, 4, 3, 5, 4 };

    // Given size
    int size = sizeof(arr)
               / sizeof(arr[0]);

    // Function call
    cout << MinimumNoOfOperations(
        arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class solution{

// Function to print the minimum
// number of decrements to make
// all elements equals
static int MinimumNoOfOperations(int arr[],
                                 int n)
{
  // Find minimum element
  int min_ele = Integer.MAX_VALUE;

  for (int i = 0; i < n; ++i)
  {
    min_ele = Math.min(min_ele,
                       arr[i]);
  }

  // Stores frequencies of array
  // elements
  TreeMap<Integer,
          Integer> mp =
          new TreeMap<Integer,
                      Integer>(
          Collections.reverseOrder());

  // Update frequencies in
  // the Map
  for (int i = 0; i < n; ++i)
  {
    if (arr[i] == min_ele)
      continue;
    else
      mp.put(arr[i],
      mp.getOrDefault(arr[i], 0) + 1);
  }

  // Stores the count of
  // decrements at each
  // iteration
  int prev_val = 0;

  // Stores the total
  // count of decrements
  int ans = 0;

  // Calculate the number of
  // decrements
  for (Map.Entry<Integer,
                 Integer> it : mp.entrySet())
  {
    ans += (it.getValue() + prev_val);
    prev_val += it.getValue();
  }

  // Return minimum operations
  return ans;
}

// Driver Code
public static void main(String args[])
{
  // Given array
  int arr[] = {2, 5, 4, 3, 5, 4};

  // Given size
  int size = arr.length;

  // Function call
  System.out.println(
  MinimumNoOfOperations(arr, size));
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to print the minimum number of
# decrements to make all elements equals
def MinimumNoOfOperations(arr, n):

    # Find minimum element
    min_ele = sys.maxsize

    for i in range(n):
        min_ele = min(min_ele, arr[i])

    # Stores frequencies of array elements
    mp = {}

    # Update frequencies in the Map
    for i in range(n):
        if (arr[i] == min_ele):
            continue
        else:
            mp[arr[i]] = mp.get(arr[i], 0) + 1

    # Stores the count of
    # decrements at each iteration
    prev_val = 0

    # Stores the total
    # count of decrements
    ans = 0

    # Calculate the number of decrements
    for it in mp:
        ans += (mp[it] + prev_val)
        prev_val += mp[it]

    # Return minimum operations
    return ans

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 5, 4, 3, 5, 4 ]

    # Given size
    size = len(arr)

    # Function call
    print(MinimumNoOfOperations(arr, size))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System.Collections.Generic;
using System;
using System.Linq;

class GFG{

// Function to print the minimum
// number of decrements to make
// all elements equals
static int MinimumNoOfOperations(int []arr,
                                 int n)
{

  // Find minimum element
  int min_ele = 1000000000;

  for(int i = 0; i < n; ++i)
  {
      min_ele = Math.Min(min_ele, arr[i]);
  }

  // Stores frequencies of array
  // elements
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();

  // Update frequencies in
  // the Map
  for(int i = 0; i < n; ++i)
  {
    if (arr[i] == min_ele)
      continue;
    else
    {
      if (mp.ContainsKey(arr[i]) == true)
        mp[arr[i]] += 1;
      else
        mp[arr[i]] = 1;   
    }
  }

  // Stores the count of
  // decrements at each
  // iteration
  int prev_val = 0;

  // Stores the total
  // count of decrements
  int ans = 0;

  // Calculate the number of
  // decrements
  var val = mp.Keys.ToList();
  foreach(var key in val)
  {
    ans += (mp[key] + prev_val);
    prev_val += mp[key];
  }

  // Return minimum operations
  return ans;
}

// Driver Code
public static void Main(String[] args)
{

  // Given array
  int []arr = { 2, 5, 4, 3, 5, 4 };

  // Given size
  int size = arr.Length;

  // Function call
  Console.WriteLine(MinimumNoOfOperations(
    arr, size));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the minimum number of
// decrements to make all elements equals
function MinimumNoOfOperations(arr, n)
{

    // Find minimum element
    var min_ele = 1000000000;
    for (var i = 0; i < n; ++i) {
        min_ele = Math.min(min_ele, arr[i]);
    }

    // Stores frequencies of array elements
    var mp = new Map();

    // Update frequencies in the Map
    for (var i = 0; i < n; ++i) {

        if (arr[i] == min_ele)
            continue;
        else
        {
            if(mp.has(arr[i]))
            {
                mp.set(arr[i], mp.get(arr[i])+1);
            }
            else
            {
                mp.set(arr[i], 1);
            }
        }
    }

    // Stores the count of
    // decrements at each iteration
    var prev_val = 0;

    // Stores the total
    // count of decrements
    var ans = 0;
    var keys = [];

    mp.forEach((value, key) => {
        keys.push(key);
    });
    keys.sort((a,b)=>b-a);
    // Calculate the number of decrements
    keys.forEach(value => {
        ans += (mp.get(value) + prev_val);
        prev_val += mp.get(value);
    });

    // Return minimum operations
    return ans;
}

// Driver Code
// Given array
var arr = [2, 5, 4, 3, 5, 4];
// Given size
var size = arr.length
// Function call
document.write( MinimumNoOfOperations(
    arr, size));

</script>
```

**Output:** 

```
11
```

***时间复杂度:** O(N)其中 N 是数组的大小。*
***辅助空间:** O(N)*