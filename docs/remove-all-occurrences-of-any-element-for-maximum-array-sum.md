# 移除最大数组和的任何元素的所有出现

> 原文:[https://www . geeksforgeeks . org/remove-任何元素的所有出现次数-针对最大数组-sum/](https://www.geeksforgeeks.org/remove-all-occurrences-of-any-element-for-maximum-array-sum/)

给定一个正整数数组，移除所有出现的元素，得到剩余数组的最大和。

**示例:**

> 输入:arr = {1，1，3}
> 输出:3
> 从数组中移除 1 后，我们得到{3}。总值是 3
> 
> 输入:arr = {1，1，3，3，2，2，1，1，1}
> 输出:11
> 从数组中移除 2 后，我们得到{1，1，3，3，1，1，1}。总值是 11。

**蛮力解**是先求一个数组的和，之后求数组中元素的所有频率。找出它们对数组和的贡献值。选择其中的最小值。移除后得到数组的最大和是和的总值与单个元素的总频繁值贡献的最小值的相等差。
T3】时间复杂度: O(n <sup>2</sup>

A **更好的逼近**我们先求数组的总和，然后对数组进行排序，遍历数组的同时统计各个频率，得到最大值。排序后，我们可以使用 O(n)时间内所有元素的频率，
该方法的时间复杂度为 O(n ^ Log n)

一种有效的方法是在遍历数组时使用散列来计算元素的频率。使用存储在数组中的频率找到最小值

## C++

```
#include <bits/stdc++.h>
using namespace std;

int maxSumArray(int arr[], int n)
{
    // Find total sum and frequencies of elements
    int sum = 0;
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        mp[arr[i]]++;
    }

    // Find minimum value to be subtracted.
    int minimum = INT_MAX;
    for (auto x : mp)
        minimum = min(minimum, x.second * x.first);

    // Find maximum sum after removal
    return (sum - minimum);
}

// Drivers code
int main()
{
    int arr[] = { 1, 1, 3, 3, 2, 2, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(int);
    cout << maxSumArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert fractional decimal
// to binary number
import java.util.*;

class GFG
{

static int maxSumArray(int arr[], int n)
{
    // Find total sum and frequencies of elements
    int sum = 0;
    Map<Integer,Integer> m = new HashMap<>();
    for (int i = 0 ; i < n; i++)
    {
        sum += arr[i];
        if(m.containsKey(arr[i]))
        {
            m.put(arr[i], m.get(arr[i])+1);
        }
        else
        {
            m.put(arr[i], 1);
        }
    }

    // Find minimum value to be subtracted.
    int minimum = Integer.MAX_VALUE;
    for (Map.Entry<Integer,Integer> x : m.entrySet())
        minimum = Math.min(minimum, x.getValue() * x.getKey());

    // Find maximum sum after removal
    return (sum - minimum);
}

// Drivers code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 3, 3, 2, 2, 1, 1, 1 };
    int n = arr.length;
    System.out.println(maxSumArray(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to convert
# fractional decimal to binary number
from sys import maxsize
def maxSumArray(arr, n):

    # Find total sum and frequencies of elements
    sum1 = 0
    mp = {i:0 for i in range(4)}
    for i in range(n):
        sum1 += arr[i]
        mp[arr[i]] += 1

    # Find minimum value to be subtracted.
    minimum = maxsize
    for key, value in mp.items():
        if(key == 0):
            continue
        minimum = min(minimum, value * key)

    # Find maximum sum after removal
    return (sum1 - minimum)

# Driver Code
if __name__ =='__main__':
    arr = [1, 1, 3, 3, 2, 2, 1, 1, 1]
    n = len(arr)
    print(maxSumArray(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to convert fractional decimal
// to binary number
using System;
using System.Collections.Generic;

class GFG
{

static int maxSumArray(int []arr, int n)
{
    // Find total sum and frequencies of elements
    int sum = 0;
    Dictionary<int,int> m = new Dictionary<int,int>();
    for (int i = 0 ; i < n; i++)
    {
        sum += arr[i];
        if(m.ContainsKey(arr[i]))
        {
            var val = m[arr[i]];
            m.Remove(arr[i]);
            m.Add(arr[i], val + 1);
        }
        else
        {
            m.Add(arr[i], 1);
        }
    }

    // Find minimum value to be subtracted.
    int minimum = int.MaxValue;
    foreach(KeyValuePair<int, int> x in m)
        minimum = Math.Min(minimum, (x.Value * x.Key));

    // Find maximum sum after removal
    return (sum - minimum);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 3, 3, 2, 2, 1, 1, 1 };
    int n = arr.Length;
    Console.WriteLine(maxSumArray(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

function maxSumArray(arr, n)
{
    // Find total sum and frequencies of elements
    var sum = 0;
    var mp = new Map();
    for (var i = 0; i < n; i++) {
        sum += arr[i];
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else   
            mp.set(arr[i], 1)
    }

    // Find minimum value to be subtracted.
    var minimum = 1000000000;
    mp.forEach((value, key) => {
        minimum = Math.min(minimum, value * key);
    });

    // Find maximum sum after removal
    return (sum - minimum);
}

// Drivers code
var arr = [1, 1, 3, 3, 2, 2, 1, 1, 1];
var n = arr.length;
document.write( maxSumArray(arr, n));

</script>
```

**Output:** 

```
11
```

**时间复杂度:** O(n)