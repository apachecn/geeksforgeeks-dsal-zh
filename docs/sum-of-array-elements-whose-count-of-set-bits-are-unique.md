# 集合位计数唯一的数组元素之和

> 原文:[https://www . geesforgeks . org/数组元素之和-其集合位数是唯一的/](https://www.geeksforgeeks.org/sum-of-array-elements-whose-count-of-set-bits-are-unique/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出数组中具有不同[计数的设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)的所有数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {8，3，7，5，3}
> **输出:** 15
> **解释:**
> 每个元素数组中设置位的个数为:
> 
> 1.  arr[0] = 8 = (1000) <sub>2</sub> ，有 1 个设置位。
> 2.  arr[1] = 3 = (11) <sub>2</sub> ，有 2 个设置位。
> 3.  arr[2] = 7 = (111) <sub>2</sub> ，有 3 个设置位。
> 4.  arr[3] = 5 = (101) <sub>2</sub> ，有 2 个设置位。
> 5.  arr[4] = 3 = (11) <sub>2</sub> ，有 2 个设置位。
> 
> 因此，集合位计数唯一的数组元素的数量是 8 和 7。因此，所需的总和= 8 + 7 = 15。
> 
> **输入:** arr[] = {4，5，3，5，3，2 }
> T3】输出: 0

**方法:**想法是将具有相应设置位计数的元素存储在**映射**上，然后找到具有唯一设置位计数的元素之和。按照以下步骤解决问题:

*   初始化一个变量，比如说 **sum** 来存储元素的合成和，初始化一个 [Map](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ，比如说 **M** 来存储具有特定设置位计数的元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并根据[设置的比特数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)将元素**arr【I】**存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中。
*   现在，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，如果任何设置的比特计数的频率是 **1，**则在变量**和**中添加与之相关的相应值。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the approach
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of set bits in an integer N
int setBitCount(int n)
{

    // Stores the count of set bits
    int ans = 0;

    // Iterate until N is non-zero
    while (n)
    {
        ans += n & 1;
        n >>= 1;
    }

    // Stores the resultant count
    return ans;
}

// Function to calculate sum of all array
// elements whose count of set bits are unique
int getSum(int *arr, int n)
{

    // Stores frequency of all possible
    // count of set bits
    map<int, int> mp;

    // Stores the sum of array elements
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Count the number of set bits
        int key = setBitCount(arr[i]);
        mp[key] += 1;
    }

    // Traverse the array
    // And Update the value of ans
    for(int i = 0; i < n; i++)
    {
        int key = setBitCount(arr[i]);

        // If frequency is 1
        if (mp[key] == 1)
            ans += arr[i];
    }
    cout << ans;
}

// Driver Code
int main()
{
    int arr[5] = {8, 3, 7, 5, 3};
    int n = sizeof(arr) / sizeof(arr[0]);

    getSum(arr, n);

    return 0;
}

// This code is contributed by rohitsingh07052
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the approach
import java.util.*;
class GFG
{

  // Function to count the number
  // of set bits in an integer N
  static int setBitCount(int n)
  {

    // Stores the count of set bits
    int ans = 0;

    // Iterate until N is non-zero
    while (n != 0)
    {
      ans += n & 1;
      n >>= 1;
    }

    // Stores the resultant count
    return ans;
  }

  // Function to calculate sum of all array
  // elements whose count of set bits are unique
  static void getSum(int []arr, int n)
  {

    // Stores frequency of all possible
    // count of set bits
    Map<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Stores the sum of array elements
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

      // Count the number of set bits
      int key = setBitCount(arr[i]);
      if(mp.containsKey(key))
        mp.put(key,mp.get(key) + 1);
      else
        mp.put(key, 1);

    }

    // Traverse the array
    // And Update the value of ans
    for(int i = 0; i < n; i++)
    {
      int key = setBitCount(arr[i]);

      // If frequency is 1
      if (mp.containsKey(key) && mp.get(key) == 1)
        ans += arr[i];
    }
    System.out.print(ans);
  }

  // Driver Code
  public static void main(String args[])
  {
    int []arr = {8, 3, 7, 5, 3};
    int n = arr.length;

    getSum(arr, n);
  }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# Python3 program for the approach

# Function to count the number
# of set bits in an integer N
def setBitCount(n):

    # Stores the count of set bits
    ans = 0

    # Iterate until N is non-zero
    while n:

        ans += n & 1
        n >>= 1

    # Stores the resultant count
    return ans

# Function to calculate sum of all array
# elements whose count of set bits are unique
def getSum(arr):

    # Stores frequency of all possible
    # count of set bits
    mp = {}

    # Stores the sum of array elements
    ans = 0

    # Traverse the array
    for i in arr:

        # Count the number of set bits
        key = setBitCount(i)
        mp[key] = [0, i]

    # Traverse the array
    for i in arr:
        key = setBitCount(i)
        mp[key][0] += 1

    # Update the value of ans
    for i in mp:

        # If frequency is 1
        if mp[i][0] == 1:
            ans += mp[i][1]

    print(ans)

# Driver Code

arr = [8, 3, 7, 5, 3]
getSum(arr)
```

## C#

```
// C# program for the approach
using System;
using System.Collections.Generic;

class solution{

// Function to count the number
// of set bits in an integer N
static int setBitCount(int n)
{

    // Stores the count of set bits
    int ans = 0;

    // Iterate until N is non-zero
    while (n>0)
    {
        ans += n & 1;
        n >>= 1;
    }

    // Stores the resultant count
    return ans;
}

// Function to calculate sum of all array
// elements whose count of set bits are unique
static void getSum(int []arr, int n)
{

    // Stores frequency of all possible
    // count of set bits
    Dictionary<int, int> mp = new Dictionary<int,int>();

    // Stores the sum of array elements
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Count the number of set bits
        int key = setBitCount(arr[i]);
        if(mp.ContainsKey(key))
          mp[key] += 1;
        else
          mp[key] = 1;
    }

    // Traverse the array
    // And Update the value of ans
    for(int i = 0; i < n; i++)
    {
        int key = setBitCount(arr[i]);

        // If frequency is 1
        if (mp[key] == 1)
            ans += arr[i];
    }
   Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int []arr = {8, 3, 7, 5, 3};
    int n = arr.Length;

    getSum(arr, n);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number
  // of set bits in an integer N
  function setBitCount(n)
  {

    // Stores the count of set bits
    let ans = 0;

    // Iterate until N is non-zero
    while (n != 0)
    {
      ans += n & 1;
      n >>= 1;
    }

    // Stores the resultant count
    return ans;
  }

  // Function to calculate sum of all array
  // elements whose count of set bits are unique
  function getSum(arr, n)
  {

    // Stores frequency of all possible
    // count of set bits
    let mp = new Map();

    // Stores the sum of array elements
    let ans = 0;

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

      // Count the number of set bits
      let key = setBitCount(arr[i]);
      if(mp.has(key))
        mp.set(key,mp.get(key) + 1);
      else
        mp.set(key, 1);

    }

    // Traverse the array
    // And Update the value of ans
    for(let i = 0; i < n; i++)
    {
      let key = setBitCount(arr[i]);

      // If frequency is 1
      if (mp.has(key) && mp.get(key) == 1)
        ans += arr[i];
    }
    document.write(ans);
  }

// Driver Code

    let arr = [8, 3, 7, 5, 3];
    let n = arr.length;

    getSum(arr, n);

</script>        
```

**Output:** 

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)