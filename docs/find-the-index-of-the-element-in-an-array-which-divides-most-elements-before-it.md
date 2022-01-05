# 在一个数组中找到元素的索引，这个数组将它前面的大部分元素分开

> 原文:[https://www . geeksforgeeks . org/find-数组中元素的索引-在它之前划分最多的元素/](https://www.geeksforgeeks.org/find-the-index-of-the-element-in-an-array-which-divides-most-elements-before-it/)

给定一个数组 **arr** ，任务是在一个数组中找到元素的索引，这个数组在它之前划分了大部分元素
**示例:**

```
Input: arr = {5, 2, 1, 4, 5, 8, 2}
Output: 6
Explanation
arr[6] = 2 
it divides 2, 4, and 8 (3 elements)

Input: arr = {8, 1, 28, 4, 1, 6, 7}
Output: 4
```

**进场:**

*   维护一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。
*   对于每个 arr[i]，通过查看 ar[i]的映射来更新计数变量，并将 ar[i]的所有除数插入到映射中。
*   如果 cnt > maxx，则更新 maxElement。
*   最后用 maxElement 返回索引。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program find the index of the element
// in an array which divides
// most elements before it

#include <bits/stdc++.h>
using namespace std;

// Function to get the max element
// divisible by arr[i]
int maxElement(int arr[], int n)
{

    map<int, int> mp;
    int maxx = -1, maxElement = -1;

    for (int i = 0; i < n; i++) {
        int num = arr[i];
        int cnt = 0;

        // Update count for A[i]
        if (mp.find(num) != mp.end()) {
            cnt += mp[num];
        }

        // Generate Divisor For A[i]
        for (int j = 1; j * j <= num; j++) {
            if (num % j == 0) {
                mp[j]++;
                if (j != num / j)
                    mp[num / j]++;
            }
        }

        // Update Max Element
        if (cnt > maxx) {
            maxElement = i;
            maxx = cnt;
        }
    }

    return maxElement;
}

// Driver code
int main()
{

    int arr[] = { 5, 2, 1, 4, 5, 8, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxElement(arr, n) << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find the index of the element
// in an array which divides
// most elements before it
import java.util.*;

class GFG
{

    // Function to get the max element
    // divisible by arr[i]
    static int maxElement(int arr[], int n)
    {

        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();
        int maxx = -1, maxElement = -1;

        for (int i = 0; i < n; i++)
        {
            int num = arr[i];
            int cnt = 0;

            // Update count for A[i]
            if (mp.containsKey(num))
            {
                cnt += mp.get(num);
            }

            // Generate Divisor For A[i]
            for (int j = 1; j * j <= num; j++)
            {
                if (num % j == 0)
                {
                    if (mp.containsKey(j))
                        mp.put(j, mp.get(j) + 1);
                    else
                        mp.put(j, 1);
                    if (j != num / j)
                        if (mp.containsKey(num / j))
                            mp.put(num / j, mp.get(num / j) + 1);
                        else
                            mp.put(num / j, 1);
                }
            }

            // Update Max Element
            if (cnt > maxx)
            {
                maxElement = i;
                maxx = cnt;
            }
        }

        return maxElement;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 5, 2, 1, 4, 5, 8, 2 };
        int n = arr.length;

        System.out.print(maxElement(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python3 program find the index of the element
# in an array which divides
# most elements before it

# Function to get the max element
# divisible by arr[i]
def maxElement(arr, n):

    mp = dict()
    maxx = -1
    maxElement = -1

    for i in range(n):
        num = arr[i]
        cnt = 0

        # Update count for A[i]
        if (num in mp):
            cnt += mp[num]

        # Generate Divisor For A[i]
        j = 1

        while j * j <= num:
            if (num % j == 0):
                mp[j] = mp.get(j, 0) + 1
                if (j != num // j):
                    mp[num // j] = mp.get(num//j, 0) + 1
            j += 1

        # Update Max Element
        if (cnt > maxx):
            maxElement = i
            maxx = cnt

    return maxElement

# Driver code
arr = [5, 2, 1, 4, 5, 8, 2]
n = len(arr)

print(maxElement(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program find the index of the element
// in an array which divides
// most elements before it
using System;
using System.Collections.Generic;

class GFG
{

    // Function to get the max element
    // divisible by arr[i]
    static int maxElement(int []arr, int n)
    {

        Dictionary<int, int> mp = new Dictionary<int, int>();
        int maxx = -1, maxElement = -1;

        for (int i = 0; i < n; i++)
        {
            int num = arr[i];
            int cnt = 0;

            // Update count for A[i]
            if (mp.ContainsKey(num))
            {
                cnt += mp[num];
            }

            // Generate Divisor For A[i]
            for (int j = 1; j * j <= num; j++)
            {
                if (num % j == 0)
                {
                    if (mp.ContainsKey(j))
                        mp[j] = mp[j] + 1;
                    else
                        mp.Add(j, 1);
                    if (j != num / j)
                        if (mp.ContainsKey(num / j))
                            mp[num / j] = mp[num / j] + 1;
                        else
                            mp.Add(num / j, 1);
                }
            }

            // Update Max Element
            if (cnt > maxx)
            {
                maxElement = i;
                maxx = cnt;
            }
        }

        return maxElement;
    }

    // Driver code
    public static void Main(String[] args)
    {

        int []arr = { 5, 2, 1, 4, 5, 8, 2 };
        int n = arr.Length;

        Console.Write(maxElement(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript program find the index of the element
      // in an array which divides
      // most elements before it
      // Function to get the max element
      // divisible by arr[i]
      function maxElement(arr, n) {
        var mp = {};
        var maxx = -1,
          maxElement = -1;

        for (var i = 0; i < n; i++) {
          var num = arr[i];
          var cnt = 0;

          // Update count for A[i]
          if (mp.hasOwnProperty(num)) {
            cnt += mp[num];
          }

          // Generate Divisor For A[i]
          for (var j = 1; j * j <= num; j++) {
            if (num % j === 0) {
              if (mp.hasOwnProperty(j)) mp[j] = mp[j] + 1;
              else mp[j] = 1;
              if (j !== num / j)
                if (mp.hasOwnProperty(num / j)) mp[num / j] = mp[num / j] + 1;
                else mp[num / j] = 1;
            }
          }

          // Update Max Element
          if (cnt > maxx) {
            maxElement = i;
            maxx = cnt;
          }
        }

        return maxElement;
      }

      // Driver code
      var arr = [5, 2, 1, 4, 5, 8, 2];
      var n = arr.length;

      document.write(maxElement(arr, n));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
6
```

**时间复杂度** : O(N√max(Arr))