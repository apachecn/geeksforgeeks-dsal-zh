# 查找给定数组的所有唯一子数组总和。

> 原文：[https://www.geeksforgeeks.org/find-sum-unique-sub-array-sum-given-array/](https://www.geeksforgeeks.org/find-sum-unique-sub-array-sum-given-array/)

给定一组`n`个正元素。 子数组总和定义为特定子数组的所有元素的总和，任务是找到所有唯一子数组总和的总和。

注意：唯一子数组总和表示没有其他子数组具有相同的总和值。

**范例**：

> 输入：`arr[] = {3, 4, 5}`
>
> 输出：40
>
> 说明：所有可能的唯一子数组及其和为：
>
> `(3), (4), (5), (3 + 4), (4 + 5), (3 + 4 + 5)`。 这里都是唯一的，因此所需的总和= 40
>
> 输入：`arr[] = {2, 4, 2}`
>
> 输出：12
>
> 说明：所有可能的唯一子数组及其总和如下：
>
> `(2), (4), (2), (2 + 4), (4 + 2), (2 + 4 + 2)`。 这里只有`(4)`和`(2 + 4 + 2)`是唯一的。

**方法 1（基于排序）**

1.  计算数组的累加和。

2.  将所有子数组总和存储在向量中。

3.  对向量进行排序。

4.  将所有重复的子数组总和标记为零。

5.  计算并返回`totalSum`。

## C++

```cpp

// C++ for finding sum of all unique
// subarray sum
#include <bits/stdc++.h>
using namespace std;

// function for finding grandSum
long long int findSubarraySum(int arr[], int n)
{
    int i, j;

    // calculate cumulative sum of array
    // cArray[0] will store sum of zero elements
    long long int cArray[n + 1] = { 0 };
    for (i = 0; i < n; i++)
        cArray[i + 1] = cArray[i] + arr[i];

    vector<long long int> subArrSum;

    // store all subarray sum in vector
    for (i = 1; i <= n; i++)
        for (j = i; j <= n; j++)
            subArrSum.push_back(cArray[j] - 
                                cArray[i - 1]);

    // sort the vector
    sort(subArrSum.begin(), subArrSum.end());

    // mark all duplicate sub-array 
    // sum to zero
    long long totalSum = 0;
    for (i = 0; i < subArrSum.size() - 1; i++)
    {
        if (subArrSum[i] == subArrSum[i + 1]) 
        {
            j = i + 1;
            while (subArrSum[j] == subArrSum[i] && 
                                   j < subArrSum.size())
            {
                subArrSum[j] = 0;
                j++;
            }
            subArrSum[i] = 0;
        }
    }

    // calculate total sum
    for (i = 0; i < subArrSum.size(); i++)
        totalSum += subArrSum[i];

    // return totalSum
    return totalSum;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 3, 1, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSubarraySum(arr, n);
    return 0;
}

```

## Java

```java

// Java for finding sum of all unique
// subarray sum
import java.util.*;

class GFG{

// Function for finding grandSum
static int findSubarraySum(int arr[], int n)
{
    int i, j;

    // Calculate cumulative sum of array
    // cArray[0] will store sum of zero elements
    int cArray[] = new int[n + 1];
    for(i = 0; i < n; i++)
        cArray[i + 1] = cArray[i] + arr[i];

    Vector<Integer> subArrSum = new Vector<Integer>();

    // Store all subarray sum in vector
    for(i = 1; i <= n; i++)
        for(j = i; j <= n; j++)
            subArrSum.add(cArray[j] - 
                          cArray[i - 1]);

    // Sort the vector
    Collections.sort(subArrSum);

    // Mark all duplicate sub-array 
    // sum to zero
    int totalSum = 0;
    for(i = 0; i < subArrSum.size() - 1; i++)
    {
        if (subArrSum.get(i) == 
            subArrSum.get(i + 1)) 
        {
            j = i + 1;
            while (subArrSum.get(j) == 
                   subArrSum.get(i) && 
               j < subArrSum.size())
            {
                subArrSum.set(j, 0);
                j++;
            }
            subArrSum.set(i, 0);
        }
    }

    // Calculate total sum
    for(i = 0; i < subArrSum.size(); i++)
        totalSum += subArrSum.get(i);

    // Return totalSum
    return totalSum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 3, 1, 4 };
    int n = arr.length;

    System.out.print(findSubarraySum(arr, n));
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 for finding sum of all 
# unique subarray sum

# function for finding grandSum
def findSubarraySum(arr, n):

    # calculate cumulative sum of array
    # cArray[0] will store sum of zero elements
    cArray = [0 for i in range(n + 1)]
    for i in range(0, n, 1):
        cArray[i + 1] = cArray[i] + arr[i]

    subArrSum = []

    # store all subarray sum in vector
    for i in range(1, n + 1, 1):
        for j in range(i, n + 1, 1):
            subArrSum.append(cArray[j] -
                             cArray[i - 1])

    # sort the vector
    subArrSum.sort(reverse = False)

    # mark all duplicate sub-array
    # sum to zero
    totalSum = 0
    for i in range(0, len(subArrSum) - 1, 1):
        if (subArrSum[i] == subArrSum[i + 1]):
            j = i + 1
            while (subArrSum[j] == subArrSum[i] and
                           j < len(subArrSum)):
                subArrSum[j] = 0
                j += 1
            subArrSum[i] = 0

    # calculate total sum
    for i in range(0, len(subArrSum), 1):
        totalSum += subArrSum[i]

    # return totalSum
    return totalSum

# Drivers code
if __name__ == '__main__':
    arr = [3, 2, 3, 1, 4]
    n = len(arr)
    print(findSubarraySum(arr, n))

# This code is contributed by
# Sahil_Shelangia

```

## C#

```cs

// C# for finding sum of all unique
// subarray sum
using System;
using System.Collections.Generic;
class GFG{

// Function for finding grandSum
static int findSubarraySum(int []arr, 
                           int n)
{
  int i, j;

  // Calculate cumulative sum 
  // of array cArray[0] will 
  // store sum of zero elements
  int []cArray = new int[n + 1];

  for(i = 0; i < n; i++)
    cArray[i + 1] = cArray[i] + arr[i];

  List<int> subArrSum = new List<int>();

  // Store all subarray sum in vector
  for(i = 1; i <= n; i++)
    for(j = i; j <= n; j++)
      subArrSum.Add(cArray[j] - 
                    cArray[i - 1]);

  // Sort the vector
  subArrSum.Sort();

  // Mark all duplicate 
  // sub-array sum to zero
  int totalSum = 0;
  for(i = 0; i < subArrSum.Count - 1; i++)
  {
    if (subArrSum[i] == 
        subArrSum[i + 1]) 
    {
      j = i + 1;
      while (subArrSum[j] == 
             subArrSum[i] && 
             j < subArrSum.Count)
      {
        subArrSum[j] = 0;
        j++;
      }
      subArrSum[i] = 0;
    }
  }

  // Calculate total sum
  for(i = 0; i < subArrSum.Count; i++)
    totalSum += subArrSum[i];

  // Return totalSum
  return totalSum;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {3, 2, 3, 1, 4};
    int n = arr.Length;    
    Console.Write(findSubarraySum(arr, n));
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
41

```

**方法 2（基于哈希）**的想法是制作一个空的哈希表。 我们生成所有子数组。 对于每个子数组，我们计算其总和以及哈希表中总和的增量计数。 最后，我们将所有计数为 1 的总和相加。

## C++

```cpp

// C++ for finding sum of all unique subarray sum
#include <bits/stdc++.h>
using namespace std;

// function for finding grandSum
long long int findSubarraySum(int arr[], int n)
{
    int res = 0;

    // Go through all subarrays, compute sums
    // and count occurrences of sums.
    unordered_map<int, int> m;
    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += arr[j];
            m[sum]++;
        }
    }

    // Print all those sums that appear
    // once.
    for (auto x : m)
        if (x.second == 1)
            res += x.first;

    return res;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 3, 1, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSubarraySum(arr, n);
    return 0;
}

```

## Java

```java

// Java for finding sum of all
// unique subarray sum
import java.util.*;

class GFG
{

// function for finding grandSum
static int findSubarraySum(int []arr, int n)
{
    int res = 0;

    // Go through all subarrays, compute sums
    // and count occurrences of sums.
    HashMap<Integer,
            Integer> m = new HashMap<Integer,
                                     Integer>();
    for (int i = 0; i < n; i++) 
    {
        int sum = 0;
        for (int j = i; j < n; j++)
        {
            sum += arr[j];
            if (m.containsKey(sum)) 
            {
                m.put(sum, m.get(sum) + 1);
            } 
            else
            {
                m.put(sum, 1);
            }
        }
    }

    // Print all those sums that appear
    // once.
    for (Map.Entry<Integer, 
                   Integer> x : m.entrySet())
        if (x.getValue() == 1)
            res += x.getKey();

    return res;
}

// Driver code
public static void main(String[] args) 
{
    int arr[] = { 3, 2, 3, 1, 4 };
    int n = arr.length;
    System.out.println(findSubarraySum(arr, n));
}
}

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 for finding sum of all
# unique subarray sum

# function for finding grandSum
def findSubarraySum(arr, n):

    res = 0

    # Go through all subarrays, compute sums
    # and count occurrences of sums.
    m = dict()
    for i in range(n):
        Sum = 0
        for j in range(i, n):
            Sum += arr[j]
            m[Sum] = m.get(Sum, 0) + 1

    # Print all those Sums that appear
    # once.
    for x in m:
        if m[x] == 1:
            res += x

    return res

# Driver code
arr = [3, 2, 3, 1, 4]
n = len(arr)
print(findSubarraySum(arr, n))

# This code is contributed by mohit kumar

```

## C#

```cs

// C# for finding sum of all
// unique subarray sum
using System;
using System.Collections.Generic;

class GFG
{

// function for finding grandSum
static int findSubarraySum(int []arr, int n)
{
    int res = 0;

    // Go through all subarrays, compute sums
    // and count occurrences of sums.
    Dictionary<int, 
               int> m = new Dictionary<int, 
                                       int>();
    for (int i = 0; i < n; i++) 
    {
        int sum = 0;
        for (int j = i; j < n; j++)
        {
            sum += arr[j];
            if (m.ContainsKey(sum)) 
            {
                m[sum] = m[sum] + 1;
            } 
            else
            {
                m.Add(sum, 1);
            }
        }
    }

    // Print all those sums that appear
    // once.
    foreach(KeyValuePair<int, int> x in m)
        if (x.Value == 1)
            res += x.Key;

    return res;
}

// Driver code
public static void Main(String[] args) 
{
    int []arr = { 3, 2, 3, 1, 4 };
    int n = arr.Length;
    Console.WriteLine(findSubarraySum(arr, n));
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
41

```



* * *

* * *



