# 删除`M`个项目后，不同元素的最小数量 | 系列 2

> 原文：[https://www.geeksforgeeks.org/minimum-number-of-distinct-elements-after-removing-m-items-set-2/](https://www.geeksforgeeks.org/minimum-number-of-distinct-elements-after-removing-m-items-set-2/)

给定一个项目的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，第`i`个索引元素表示该项目的 ID，给定一个数字`m`，任务是删除`m`个元素，以使剩余的唯一 ID 最少。 打印不同 ID 的数量。

**示例**：

> **输入**：`arr[] = {2, 2, 1, 3, 3, 3} m = 3`
>
> **输出**：1
>
> **说明**：
>
> 删除 1 和两个 2。
>
> 因此，仅剩 3 个，因此元素的不同数目为 1。
> 
> **输入**：`arr[] = {2, 4, 1, 5, 3, 5, 1, 3}, m = 2`
>
> **输出**：3
>
> **说明**：
>
> 完全卸下 2 和 4。
>
> 因此，剩下的 1、3 和 5，即 3 个元素。

对于`O(N * log N)`方法，请参考[先前的文章](https://www.geeksforgeeks.org/minimum-number-of-distinct-elements-after-removing-m-items/)。

**高效方法**：这个想法是将每个元素的出现存储在[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)中，然后再次计算每个频率在哈希中的出现。 步骤如下：

1.  遍历给定的数组元素，[对每个数字](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/)的出现进行计数，并将其存储到[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)中。

2.  现在，不对频率进行排序，而是将频率的出现计数到另一个数组中，例如`freq_arr[]`。

3.  计算不重复编号的总数（例如`ans`）。

4.  现在，遍历`freq_arr[]`数组，如果`freq_arr[i] > 0`，则从`ans`中删除`m / i`和`freq_arr[i]`的最小值（例如`t`），然后从`m`中减去`i * t`来移除任何数字`i`的出现。

下面是上述方法的实现。

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum distinct
// character after M removals
int distinctNumbers(int arr[], int m,
                    int n)
{
    unordered_map<int, int> count;

    // Count the occurences of number
    // and store in count
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    // Count the occurences of the
    // frequencies
    vector<int> fre_arr(n + 1, 0);
    for (auto it : count) {
        fre_arr[it.second]++;
    }

    // Take answer as total unique numbers
    // and remove the frequency and
    // subtract the answer
    int ans = count.size();

    for (int i = 1; i <= n; i++) {
        int temp = fre_arr[i];
        if (temp == 0)
            continue;

        // Remove the minimum number
        // of times
        int t = min(temp, m / i);
        ans -= t;
        m -= i * t;
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Initialize array
    int arr[] = { 2, 4, 1, 5, 3, 5, 1, 3 };

    // Size of array
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 2;

    // Function call
    cout << distinctNumbers(arr, m, n);
    return 0;
}

```

## Java

```java

// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to return minimum distinct
// character after M removals
static int distinctNumbers(int arr[], int m,
                                      int n)
{
    Map<Integer, 
        Integer> count = new HashMap<Integer,
                                     Integer>();

    // Count the occurences of number
    // and store in count
    for (int i = 0; i < n; i++)
    count.put(arr[i],
              count.getOrDefault(arr[i], 0) + 1);

    // Count the occurences of the
    // frequencies
    int[] fre_arr = new int[n + 1];
    for(Integer it : count.values())
    {
        fre_arr[it]++;
    }

    // Take answer as total unique numbers
    // and remove the frequency and
    // subtract the answer
    int ans = count.size();

    for(int i = 1; i <= n; i++) 
    {
        int temp = fre_arr[i];
        if (temp == 0)
            continue;

        // Remove the minimum number
        // of times
        int t = Math.min(temp, m / i);
        ans -= t;
        m -= i * t;
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Initialize array
    int arr[] = { 2, 4, 1, 5, 3, 5, 1, 3 };

    // Size of array
    int n = arr.length;
    int m = 2;

    // Function call
    System.out.println(distinctNumbers(arr, m, n)); 
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program for the above approach

# Function to return minimum distinct
# character after M removals
def distinctNumbers(arr, m, n):

    count = {}

    # Count the occurences of number
    # and store in count
    for i in range(n):
        count[arr[i]] = count.get(arr[i], 0) + 1

    # Count the occurences of the
    # frequencies
    fre_arr = [0] * (n + 1)
    for it in count:
        fre_arr[count[it]] += 1

    # Take answer as total unique numbers
    # and remove the frequency and
    # subtract the answer
    ans = len(count)

    for i in range(1, n + 1):
        temp = fre_arr[i]
        if (temp == 0):
            continue

        # Remove the minimum number
        # of times
        t = min(temp, m // i)
        ans -= t
        m -= i * t

    # Return the answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Initialize array
    arr = [ 2, 4, 1, 5, 3, 5, 1, 3 ]

    # Size of array
    n = len(arr)
    m = 2

    # Function call
    print(distinctNumbers(arr, m, n))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return minimum distinct
// character after M removals
static int distinctNumbers(int []arr, 
                           int m, int n)
{
  Dictionary<int, 
             int> count = new Dictionary<int,
                                         int>();

  // Count the occurences of number
  // and store in count
  for (int i = 0; i < n; i++)
    if(count.ContainsKey(arr[i]))
    {
      count[arr[i]] = count[arr[i]] + 1;
    }
  else
  {
    count.Add(arr[i], 1);
  }

  // Count the occurences of the
  // frequencies
  int[] fre_arr = new int[n + 1];
  foreach(int it in count.Values)
  {
    fre_arr[it]++;
  }

  // Take answer as total unique numbers
  // and remove the frequency and
  // subtract the answer
  int ans = count.Count;

  for(int i = 1; i <= n; i++) 
  {
    int temp = fre_arr[i];
    if (temp == 0)
      continue;

    // Remove the minimum number
    // of times
    int t = Math.Min(temp, m / i);
    ans -= t;
    m -= i * t;
  }

  // Return the answer
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  // Initialize array
  int []arr = {2, 4, 1, 5, 3, 5, 1, 3};

  // Size of array
  int n = arr.Length;
  int m = 2;

  // Function call
  Console.WriteLine(distinctNumbers(arr, m, n)); 
}
}

// This code is contributed by Princi Singh

```

**输出**： 

```
3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



