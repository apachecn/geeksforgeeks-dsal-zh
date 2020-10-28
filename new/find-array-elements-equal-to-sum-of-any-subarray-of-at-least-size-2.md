# 查找等于至少大小为 2 的任何子数组之和的数组元素

> 原文：[https://www.geeksforgeeks.org/find-array-elements-equal-to-sum-of-any-subarray-of-at-least-size-2/](https://www.geeksforgeeks.org/find-array-elements-equal-to-sum-of-any-subarray-of-at-least-size-2/)

给定一个数组 **arr []** ，任务是从该数组中查找等于大小大于 1 的任何子数组之和的元素。

**示例**：

> **输入**：arr [] = {1、2、3、4、5、6}
> **输出**：3、5、6
> **说明**：
> 元素 3、5、6 分别等于子数组{1、2}，{2、3}和{1、2、3}的总和。
> **输入**：arr [] = {5，6，10，1，3，4，8，16}
> **输出**：4，8，16
> **解释**：
> 元素 4、8、16 分别等于子数组{1，3}，{1、3、4}，{1、3、4、8}的总和

**方法**：的想法是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)解决给定的问题。 创建一个 **prefix []** 数组，该数组为每个索引存储其所有先前元素的前缀和。 将所有子数组的总和存储在映射中，并搜索映射中是否存在任何数组元素。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation to find array 
// elements equal to the sum 
// of any subarray of at least size 2 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find all elements 
void findElements(int* arr, int n) 
{ 
    if (n == 1) 
        return; 

    int pre[n]; 

    // Create a prefix array 
    pre[0] = arr[0]; 

    for (int i = 1; i < n; i++) 
        pre[i] = arr[i] + pre[i - 1]; 

    unordered_map<int, bool> mp; 

    // Mark the sum of all sub arrays as true 
    for (int i = 1; i < n - 1; i++) { 
        mp[pre[i]] = true; 

        for (int j = i + 1; j < n; j++) { 
            mp[pre[j] - pre[i - 1]] = true; 
        } 
    } 

    // Check all elements 
    // which are marked 
    // true in the map 
    for (int i = 0; i < n; i++) { 
        if (mp[arr[i]]) { 
            cout << arr[i] << " "; 
        } 
    } 
    cout << endl; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = { 1, 2, 3, 4, 5, 6 }; 

    int n1 = sizeof(arr1) / sizeof(arr1[0]); 

    findElements(arr1, n1); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find array
// elements equal to the sum of any 
// subarray of at least size 2
import java.util.*;

class GFG{

// Function to find all elements
static void findElements(int[] arr, int n)
{
    if (n == 1)
        return;

    int pre[] = new int[n];

    // Create a prefix array
    pre[0] = arr[0];

    for(int i = 1; i < n; i++)
        pre[i] = arr[i] + pre[i - 1];

    HashMap<Integer, Boolean> mp = new HashMap<>();

    // Mark the sum of all sub arrays as true
    for(int i = 1; i < n - 1; i++)
    {
        mp.put(pre[i], true);

        for(int j = i + 1; j < n; j++)
        {
            mp.put(pre[j] - pre[i - 1], true);
        }
    }

    // Check all elements
    // which are marked
    // true in the map
    for(int i = 0; i < n; i++)
    {
        if (mp.get(arr[i]) != null)
        {
            System.out.print(arr[i] + " ");
        }
    }
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    int arr1[] = { 1, 2, 3, 4, 5, 6 };

    int n1 = arr1.length;

    findElements(arr1, n1);
}
}

// This code is contributed by jrishabh99

```

## Python3

```py

# Python3 implementation to find array 
# elements equal to the sum of any
# subarray of at least size 2 

# Function to find all elements 
def findElements(arr, n): 

    if (n == 1):
        return; 

    pre = [0] * n; 

    # Create a prefix array 
    pre[0] = arr[0]; 

    for i in range(1, n): 
        pre[i] = arr[i] + pre[i - 1]; 

    mp = {}; 

    # Mark the sum of all sub arrays as true 
    for i in range(1, n - 1):
        mp[pre[i]] = True; 

        for j in range(i + 1, n):
            mp[pre[j] - pre[i - 1]] = True; 

    # Check all elements which 
    # are marked true in the map 
    for i in range(n):
        if arr[i] in mp:
            print(arr[i], end = " "); 
        else:
            pass

    print()

# Driver Code 
if __name__ == "__main__": 

    arr1 = [ 1, 2, 3, 4, 5, 6 ]; 
    n1 = len(arr1); 

    findElements(arr1, n1); 

# This code is contributed by AnkitRai01

```

## C#

```cs

// C# implementation to find array
// elements equal to the sum of any 
// subarray of at least size 2
using System;
using System.Collections.Generic;
class GFG{

// Function to find all elements
static void findElements(int[] arr, 
                         int n)
{
  if (n == 1)
    return;

  int []pre = new int[n];

  // Create a prefix array
  pre[0] = arr[0];

  for(int i = 1; i < n; i++)
    pre[i] = arr[i] + pre[i - 1];

  Dictionary<int, 
             Boolean> mp = new Dictionary<int, 
                                          Boolean>();

  // Mark the sum of all sub arrays as true
  for(int i = 1; i < n - 1; i++)
  {
    if(!mp.ContainsKey(pre[i]))
      mp.Add(pre[i], true);

    for(int j = i + 1; j < n; j++)
    {
      if(!mp.ContainsKey(pre[j] - pre[i - 1]))
        mp.Add(pre[j] - pre[i - 1], true);
    }
  }

  // Check all elements
  // which are marked
  // true in the map
  for(int i = 0; i < n; i++)
  {
    if (mp.ContainsKey(arr[i]))
    {
      Console.Write(arr[i] + " ");
    }
  }
  Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
  int []arr1 = {1, 2, 3, 4, 5, 6};
  int n1 = arr1.Length;
  findElements(arr1, n1);
}
}

// This code is contributed by gauravrajput1

```

**Output:** 

```
3 5 6

```



* * *

* * *



