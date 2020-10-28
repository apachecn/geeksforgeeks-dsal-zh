# 为每个数组元素计数数组中所有重复的元素对。

给定 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 。 对于数组中的每个元素，任务是计算可能的对（i，j），不包括当前元素，以使 **i < j** 和 **arr [i] = arr [ j]** 。

**示例**：

> **输入**：arr [] = {1，1，2，1，2}
> **输出**：2 2 3 2 3
> **说明**：
> 对于索引 1，不包括当前元素的其余元素为[1、2、1、2]。 因此计数为 2。
> 对于索引 2，在索引 2 处排除元素之后的其余元素为[1、2、1、2]。 因此计数为 2。
> 对于索引 3，在索引 3 处排除元素之后的其余元素为[1、1、1、2]。 因此计数为 3。
> 对于索引 4，排除索引 4 处的元素之后的其余元素为[1、1、2、2]。 因此计数为 2。
> 对于索引 5，在索引 5 处排除元素之后的其余元素为[1、1、2、1。因此，计数为 3。
> 
> **输入**：arr [] = {1,2,3,4}
> **输出**：0 0 0 0
> **说明**：
> 由于所有元素都是不同的，因此不存在具有相等值的对。

**天真的方法**：天真的想法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，从数组中排除当前元素，并使用其余的数组元素找到所有可能的对**（ i，j）**使得 **arr [i]等于 arr [j]** 和 **i < j** 。 打印每个元素的对数。

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N）*

**高效方法**：的想法是[存储每个元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率，并在给定条件下计算所有可能的对（例如 **cnt** ）。 对每个元素执行上述步骤后，从总计数 cnt 中删除相等的可能对的计数并打印该值。 请按照以下步骤解决问题：

1.  将每个元素的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

2.  创建一个变量来存储每个元素的贡献。

3.  可以用 **freq [x] *（freq [x] – 1）除以 2** 来计算 **x** 的贡献，其中 **freq [x]** 为 **x** 的频率。

4.  遍历给定的数组，并从总数中除去每个元素的贡献，并将其存储在 **ans []** 中。

5.  打印存储在 **ans []** 中的所有元素。

下面是上述方法的实现：

## C++

```cpp

// C++ program for
// the above approach
#include <bits/stdc++.h>
#define int long long int
using namespace std;

// Function to print the required
// count of pairs excluding the
// current element
void solve(int arr[], int n)
{
    // Store the frequency
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++) {
        mp[arr[i]]++;
    }

    // Find all the count
    int cnt = 0;
    for (auto x : mp) {
        cnt += ((x.second)
                * (x.second - 1) / 2);
    }

    int ans[n];

    // Delete the contribution of
    // each element for equal pairs
    for (int i = 0; i < n; i++) {

        ans[i] = cnt - (mp[arr[i]] - 1);
    }

    // Print the answer
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int32_t main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 2, 1, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    solve(arr, N);
    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG{

// Function to print the required
// count of pairs excluding the
// current element
static void solve(int arr[], 
                  int n)
{
  // Store the frequency
  HashMap<Integer,
          Integer> mp = new HashMap<Integer,
                                    Integer>();
  for (int i = 0; i < n; i++) 
  {
    if(mp.containsKey(arr[i]))
    {
      mp.put(arr[i], mp.get(arr[i]) + 1);
    }
    else
    {
      mp.put(arr[i], 1);
    }
  }

  // Find all the count
  int cnt = 0;
  for (Map.Entry<Integer,
                 Integer> x : mp.entrySet())
  {
    cnt += ((x.getValue()) * 
            (x.getValue() - 1) / 2);
  }

  int []ans = new int[n];

  // Delete the contribution of
  // each element for equal pairs
  for (int i = 0; i < n; i++) 
  {
    ans[i] = cnt - (mp.get(arr[i]) - 1);
  }

  // Print the answer
  for (int i = 0; i < n; i++) 
  {
    System.out.print(ans[i] + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 1, 2, 1, 2};

  int N = arr.length;

  // Function Call
  solve(arr, N);
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```py

# Python3 program for 
# the above approach

# Function to prthe required
# count of pairs excluding the
# current element
def solve(arr, n):

    # Store the frequency
    mp = {}
    for i in arr:
        mp[i] = mp.get(i, 0) + 1

    # Find all the count
    cnt = 0
    for x in mp:
        cnt += ((mp[x]) *
                (mp[x] - 1) // 2)

    ans = [0] * n

    # Delete the contribution of
    # each element for equal pairs
    for i in range(n):
        ans[i] = cnt - (mp[arr[i]] - 1)

    # Print the answer
    for i in ans:
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [1, 1, 2, 1, 2]

    N = len(arr)

    # Function call
    solve(arr, N)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to print the required
// count of pairs excluding the
// current element
static void solve(int []arr, 
                  int n)
{
  // Store the frequency
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();
  for (int i = 0; i < n; i++) 
  {
    if(mp.ContainsKey(arr[i]))
    {
      mp[arr[i]] =  mp[arr[i]] + 1;
    }
    else
    {
      mp.Add(arr[i], 1);
    }
  }

  // Find all the count
  int cnt = 0;
  foreach (KeyValuePair<int,
                        int> x in mp)
  {
    cnt += ((x.Value) * 
            (x.Value - 1) / 2);
  }

  int []ans = new int[n];

  // Delete the contribution of
  // each element for equal pairs
  for (int i = 0; i < n; i++) 
  {
    ans[i] = cnt - (mp[arr[i]] - 1);
  }

  // Print the answer
  for (int i = 0; i < n; i++) 
  {
    Console.Write(ans[i] + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 1, 2, 1, 2};

  int N = arr.Length;

  // Function Call
  solve(arr, N);
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
2 2 3 2 3

```

***时间复杂度**：O（NlogN）*

***辅助空间**：O（N）*



* * *

* * *



