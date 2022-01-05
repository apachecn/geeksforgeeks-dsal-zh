# 使所有剩余阵列元素的频率相等所需的最小移除量

> 原文:[https://www . geesforgeks . org/minimum-removes-要求使所有剩余数组元素的频率相等/](https://www.geeksforgeeks.org/minimum-removals-required-to-make-frequency-of-all-remaining-array-elements-equal/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到需要移除的最小数量的阵列元素，使得剩余阵列元素的频率相等。

**示例:**

> **输入:** arr[] = {2，4，3，2，5，3}
> **输出:** 2
> **解释:**存在以下两种可能性:
> 1)要么移除 2 和 3 的出现。数组 arr[]修改为{2，4，3，5}。因此，所有元素的频率变得相等。
> 2)或者，删除出现的 4 和 5。数组 arr[]修改为{2，3，2，3}。因此，所有元素的频率变得相等。
> 
> **输入:** arr[] = {1，1，2，1}
> **输出:** 1

**天真方法:**我们统计数组中每个元素的出现频率。然后对于频率图中的每个值 *v* ，我们遍历频率图并检查这个当前值是否小于 *v* ，如果是，那么我们将这个当前值添加到我们的结果中，如果是假的，那么我们将当前值和 *v* 之间的差值添加到我们的结果中。每次遍历后，存储当前结果和先前结果的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get minimum removals required
// to make frequency of all remaining elements equal
int minDelete(int arr[], int n)
{
    // Create an hash map and store frequencies of all
    // array elements in it using element as key and
    // frequency as value
    unordered_map<int, int> freq;
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Initialize the result to store the minimum deletions
    int tempans, res = INT_MAX;

    // Find deletions required for each element and store
    // the minimum deletions in result
    for (auto itr = freq.begin(); itr != freq.end();
         itr++) {
        tempans = 0;
        for (auto j = freq.begin(); j != freq.end(); j++) {
            if (j->second < itr->second) {
                tempans = tempans + j->second;
            }
            else {
                tempans
                    = tempans + (j->second - itr->second);
            }
        }
        res = min(res, tempans);
    }

    return res;
}

// Driver program to run the case
int main()
{
    int arr[] = {2, 4, 3, 2, 5, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minDelete(arr, n);
    return 0;
}
```

**Output**

```
2
```

**高效方法:**按照以下步骤解决问题:

*   初始化一个[有序图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如**频率，**来存储所有阵元的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并存储数组元素各自的[频率。](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)
*   初始化一个向量，比如 **v、**来存储地图中存储的所有频率。
*   [排序向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **v.**
*   初始化一个变量，比如说 **ans，**来存储最终的计数。
*   [遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **v** ，对于每个频率，计算需要移除的元素数量，使剩余元素的频率相等。
*   打印获得的所有清除计数的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// removals required to make frequency
// of all array elements equal
int minDeletions(int arr[], int N)
{
    // Stores frequency of
    // all array elements
    map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        freq[arr[i]]++;
    }

    // Stores all the frequencies
    vector<int> v;

    // Traverse the map
    for (auto z : freq) {
        v.push_back(z.second);
    }

    // Sort the frequencies
    sort(v.begin(), v.end());

    // Count of frequencies
    int size = v.size();

    // Stores the final count
    int ans = N - (v[0] * size);

    // Traverse the vector
    for (int i = 1; i < v.size(); i++) {

        // Count the number of removals
        // for each frequency and update
        // the minimum removals required
        if (v[i] != v[i - 1]) {
            int safe = v[i] * (size - i);
            ans = min(ans, N - safe);
        }
    }

    // Print the final count
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 4, 3, 2, 5, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to print the minimum
    // number of removals required
    minDeletions(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.HashMap;
import java.util.Map;
import java.util.ArrayList;
import java.util.Collections;

class GFG {
  public static void minDeletions(int arr[], int N)
  {

    // Stores frequency of
    // all array elements
    HashMap<Integer, Integer> map = new HashMap<>();
    ;

    // Traverse the array
    for (int i = 0; i < N; i++) {
      Integer k = map.get(arr[i]);
      map.put(arr[i], (k == null) ? 1 : k + 1);
    }

    // Stores all the frequencies
    ArrayList<Integer> v = new ArrayList<>();

    // Traverse the map
    for (Map.Entry<Integer, Integer> e :
         map.entrySet()) {
      v.add(e.getValue());
    }

    // Sort the frequencies
    Collections.sort(v);

    // Count of frequencies
    int size = v.size();

    // Stores the final count
    int ans = N - (v.get(0) * size);

    // Traverse the vector
    for (int i = 1; i < v.size(); i++) {

      // Count the number of removals
      // for each frequency and update
      // the minimum removals required
      if (v.get(i) != v.get(i - 1)) {
        int safe = v.get(i) * (size - i);
        ans = Math.min(ans, N - safe);
      }
    }

    // Print the final count
    System.out.println(ans);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 2, 4, 3, 2, 5, 3 };

    // Size of the array
    int N = 6;

    // Function call to print the minimum
    // number of removals required
    minDeletions(arr, N);
  }
}

// This code is contributed by aditya7409.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict

# Function to count the minimum
# removals required to make frequency
# of all array elements equal
def minDeletions(arr, N):

    # Stores frequency of
    # all array elements
    freq = defaultdict(int)

    # Traverse the array
    for i in range(N):
        freq[arr[i]] += 1

    # Stores all the frequencies
    v = []

    # Traverse the map
    for z in freq.keys():
        v.append(freq[z])

    # Sort the frequencies
    v.sort()

    # Count of frequencies
    size = len(v)

    # Stores the final count
    ans = N - (v[0] * size)

    # Traverse the vector
    for i in range(1, len(v)):

        # Count the number of removals
        # for each frequency and update
        # the minimum removals required
        if (v[i] != v[i - 1]):
            safe = v[i] * (size - i)
            ans = min(ans, N - safe)

    # Print the final count
    print(ans)

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [2, 4, 3, 2, 5, 3]

    # Size of the array
    N = len(arr)

    # Function call to print the minimum
    # number of removals required
    minDeletions(arr, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

  // Function to count the minimum
  // removals required to make frequency
  // of all array elements equal
  static void minDeletions(int []arr, int N)
  {

    // Stores frequency of
    // all array elements
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
      if(freq.ContainsKey(arr[i]))
        freq[arr[i]]++;
      else
        freq[arr[i]] = 1;
    }

    // Stores all the frequencies
    List<int> v = new List<int>();

    // Traverse the map
    foreach (var z in freq) {
      v.Add(z.Value);
    }

    // Sort the frequencies
    int sz = v.Count;
    int []temp = new int[sz];
    for(int i = 0; i < v.Count; i++)
      temp[i] = v[i];
    Array.Sort(temp);
    for(int i = 0; i < v.Count; i++)
      v[i] = temp[i];

    // Count of frequencies
    int size = v.Count;

    // Stores the final count
    int ans = N - (v[0] * size);

    // Traverse the vector
    for (int i = 1; i < v.Count; i++) {

      // Count the number of removals
      // for each frequency and update
      // the minimum removals required
      if (v[i] != v[i - 1]) {
        int safe = v[i] * (size - i);
        ans = Math.Min(ans, N - safe);
      }
    }

    // Print the final count
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main()
  {

    // Given array
    int []arr = { 2, 4, 3, 2, 5, 3 };

    // Size of the array
    int N = arr.Length;

    // Function call to print the minimum
    // number of removals required
    minDeletions(arr, N);
  }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the minimum
// removals required to make frequency
// of all array elements equal
function minDeletions(arr, N)
{
    // Stores frequency of
    // all array elements
    var freq = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {
        if(freq.has(arr[i]))
        {
            freq.set(arr[i], freq.get(arr[i])+1);
        }
        else
        {
            freq.set(arr[i], 1);
        }
    }

    // Stores all the frequencies
    var v = [];

    // Traverse the map
    freq.forEach((value, key) => {
        v.push(value);
    });

    // Sort the frequencies
    v.sort();

    // Count of frequencies
    var size = v.length;

    // Stores the final count
    var ans = N - (v[0] * size);

    // Traverse the vector
    for (var i = 1; i < v.length; i++) {

        // Count the number of removals
        // for each frequency and update
        // the minimum removals required
        if (v[i] != v[i - 1]) {
            var safe = v[i] * (size - i);
            ans = Math.min(ans, N - safe);
        }
    }

    // Print the final count
    document.write( ans);
}

// Driver Code
// Given array
var arr = [ 2, 4, 3, 2, 5, 3 ];
// Size of the array
var N = arr.length;
// Function call to print the minimum
// number of removals required
minDeletions(arr, N);

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)