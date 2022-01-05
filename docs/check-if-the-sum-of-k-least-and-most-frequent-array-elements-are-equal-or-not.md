# 检查 K 个最少和最频繁数组元素的和是否相等

> 原文:[https://www . geeksforgeeks . org/check-of-k-最少和最频繁数组元素是否相等/](https://www.geeksforgeeks.org/check-if-the-sum-of-k-least-and-most-frequent-array-elements-are-equal-or-not/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查 [K 个最频繁数组元素](https://www.geeksforgeeks.org/find-k-numbers-occurrences-given-array/)的和与 [K 个最不频繁数组元素](https://www.geeksforgeeks.org/least-frequent-element-array/)的和在[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 中是否相等。如果发现**为真**，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** arr[] = { 3，2，1，2，3，3，4 }，K=2
> **输出:**是
> **说明:**
> 各元素的频率由下式给出:
> 
> *   3，频率是 3。
> *   2，频率是 2。
> *   1，频率是 1。
> *   4、频率为 1。
> 
> K(= 2)个最频繁元素之和为 3 + 2 = 5，K(= 2)个最不频繁元素之和为 1 + 4 =5。因此，打印“是”。
> 
> **输入:** arr[] = {1，2，4，1，1，3，2，4，2，5，3}，K = 3
> **输出:**否

**方法:**给定的问题可以通过[用](https://www.geeksforgeeks.org/find-k-most-frequent-in-linear-time/)[用频率索引散列](https://www.geeksforgeeks.org/hashing-data-structure/)找到 K 个最频繁的元素来解决，根据频率数组找到 [K 个最频繁的](https://www.geeksforgeeks.org/find-k-numbers-occurrences-given-array/)元素的和等于[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中 [K 个最不频繁的](https://www.geeksforgeeks.org/least-frequent-element-array/)元素的和。按照以下步骤解决问题:

*   [初始化一个无序图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，说 **M** 统计每个数组元素的频率。
*   [迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**并将每个数组元素的频率存储在[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** 中。
*   [初始化尺寸为 **N + 1** 的二维向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **freq** ，以在地图 **M** 中以给定频率存储元素。
*   [迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**并执行以下步骤:
    *   将变量 **f** 初始化为 **arr[i]，**的频率，即**M【arr[I]】**。
    *   如果 **f** 不等于 **-1** ，则[将元素](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)**arr【I】**推入[向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **freq** 为频率 **f** ，并将**m【arr【I】】**的值设置为 **-1** 。
*   将变量**计数**初始化为 **0** ，以跟踪 [K 最频繁](https://www.geeksforgeeks.org/find-k-numbers-occurrences-given-array/)元素和 [K 最不频繁](https://www.geeksforgeeks.org/least-frequent-element-array/)数组元素。
*   将变量 **kleastfreqelem** 初始化为 **0** ，存储 K 个最不频繁数组元素的和。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   [迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，freq[I]】**并执行以下步骤:
        *   将 **freq[i][j]** 的值添加到变量 **kleastfreqelem** 中，并将**计数**的值增加 **1** 。
        *   如果**计数**等于 **K，**则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   如果**计数**等于 **K，**则断开回路。
*   将**计数**的值设置为 **0** 。
*   将变量 **kmostfreqelem** 初始化为 **0** ，以存储[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的 [K 个最不频繁](https://www.geeksforgeeks.org/least-frequent-element-array/)元素之和。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**，并执行以下步骤:
    *   [迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，freq[I]】**并执行以下步骤:
        *   将 **freq[i][j]** 的值添加到变量 **kmostfreqelem** 中，并将**计数**的值增加 **1** 。
        *   如果**计数**等于 **K** ，则脱离循环。
    *   如果**计数**等于 **K** ，则脱离循环。
*   如果 **kmostfreqelem** 的值等于 **kleastelem** ，则打印**是**。否则，打印**否**。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to compare the sum of K
// most and least occurrences
string checkSum(int arr[], int n, int k)
{
    // Stores frequency of array element
    unordered_map<int, int> m;
    for (int i = 0; i < n; i++)
        m[arr[i]]++;

    // Stores the frequencies as indexes
    // and putelements with the frequency
    // in a vector
    vector<int> freq[n + 1];
    for (int i = 0; i < n; i++) {

        // Find the frequency
        int f = m[arr[i]];

        if (f != -1) {

            // Insert in the vector
            freq[f].push_back(arr[i]);
            m[arr[i]] = -1;
        }
    }

    // Stores the count of elements
    int count = 0;

    int kleastfreqsum = 0;

    // Traverse the frequency array
    for (int i = 0; i <= n; i++) {

        // Find the kleastfreqsum
        for (int x : freq[i]) {
            kleastfreqsum += x;
            count++;
            if (count == k)
                break;
        }

        // If the count is K, break
        if (count == k)
            break;
    }

    // Reinitialize the count to zero
    count = 0;

    int kmostfreqsum = 0;

    // Traverse the frequency
    for (int i = n; i >= 0; i--) {

        // Find the kmostfreqsum
        for (int x : freq[i]) {
            kmostfreqsum += x;
            count++;
            if (count == k)
                break;
        }

        // If the count is K, break
        if (count == k)
            break;
    }

    // Comparing the sum
    if (kleastfreqsum == kmostfreqsum)
        return "Yes";

    // Otherwise, return No
    return "No";
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1, 2, 3, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << checkSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to compare the sum of K
// most and least occurrences
static String checkSum(int arr[], int n, int k)
{

    // Stores frequency of array element
    HashMap<Integer,Integer> m = new HashMap<Integer,Integer>();
    for (int i = 0; i < n; i++)
        if(m.containsKey(arr[i])){
            m.put(arr[i], m.get(arr[i])+1);
        }
        else{
            m.put(arr[i], 1);
        }

    // Stores the frequencies as indexes
    // and putelements with the frequency
    // in a vector
    Vector<Integer> []freq = new Vector[n + 1];
    for (int i = 0; i < freq.length; i++)
        freq[i] = new Vector<Integer>();
    for (int i = 0; i < n; i++) {

        // Find the frequency
        int f = m.get(arr[i]);

        if (f != -1) {

            // Insert in the vector
            freq[f].add(arr[i]);
            m.put(arr[i], -1);
        }
    }

    // Stores the count of elements
    int count = 0;

    int kleastfreqsum = 0;

    // Traverse the frequency array
    for (int i = 0; i <= n; i++) {

        // Find the kleastfreqsum
        for (int x : freq[i]) {
            kleastfreqsum += x;
            count++;
            if (count == k)
                break;
        }

        // If the count is K, break
        if (count == k)
            break;
    }

    // Reinitialize the count to zero
    count = 0;

    int kmostfreqsum = 0;

    // Traverse the frequency
    for (int i = n; i >= 0; i--) {

        // Find the kmostfreqsum
        for (int x : freq[i]) {
            kmostfreqsum += x;
            count++;
            if (count == k)
                break;
        }

        // If the count is K, break
        if (count == k)
            break;
    }

    // Comparing the sum
    if (kleastfreqsum == kmostfreqsum)
        return "Yes";

    // Otherwise, return No
    return "No";
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 1, 2, 3, 3, 4 };
    int N = arr.length;
    int K = 2;

    System.out.print(checkSum(arr, N, K));
}
}

// This code is contributed by 29AjayKumar.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to compare the sum of K
# most and least occurrences
def checkSum(arr, n, k):

    # Stores frequency of array element
    m = {}

    for i in range(n):
        if arr[i] in m:
            m[arr[i]] += 1
        else:
            m[arr[i]] = 1

    # Stores the frequencies as indexes
    # and putelements with the frequency
    # in a vector
    freq = [[] for i in range(n + 1)]

    for i in range(n):

        # Find the frequency
        f = m[arr[i]]

        if (f != -1):

            # Insert in the vector
            freq[f].append(arr[i])
            m[arr[i]] = -1

    # Stores the count of elements
    count = 0

    kleastfreqsum = 0

    # Traverse the frequency array
    for i in range(n + 1):

        # Find the kleastfreqsum
        for x in freq[i]:
            kleastfreqsum += x
            count += 1

            if (count == k):
                break

        # If the count is K, break
        if (count == k):
            break

    # Reinitialize the count to zero
    count = 0

    kmostfreqsum = 0

    # Traverse the frequency
    i = n

    while (i >= 0):

        # Find the kmostfreqsum
        for x in freq[i]:
            kmostfreqsum += x
            count += 1

            if (count == k):
                break

        i -= 1

        # If the count is K, break
        if (count == k):
            break

    # Comparing the sum
    if (kleastfreqsum == kmostfreqsum):
        return "Yes"

    # Otherwise, return No
    return "No"

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 2, 1, 2, 3, 3, 4 ]
    N = len(arr)
    K = 2

    print(checkSum(arr, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

  // Function to compare the sum of K
  // most and least occurrences
  static String checkSum(int[] arr, int n, int k)
  {

    // Stores frequency of array element
    Dictionary<int, int> m = new Dictionary<int, int>();
    for (int i = 0; i < n; i++)
      if (m.ContainsKey(arr[i])) {
        m[arr[i]] = m[arr[i]] + 1;
      }
    else {
      m.Add(arr[i], 1);
    }

    // Stores the frequencies as indexes
    // and putelements with the frequency
    // in a vector
    List<int>[] freq = new List<int>[ n + 1 ];
    for (int i = 0; i < freq.Length; i++)
      freq[i] = new List<int>();
    for (int i = 0; i < n; i++) {

      // Find the frequency
      int f = m[arr[i]];

      if (f != -1) {

        // Insert in the vector
        freq[f].Add(arr[i]);
        if (m.ContainsKey(arr[i])) {
          m[arr[i]] = -1;
        }
        else {
          m.Add(arr[i], -1);
        }
      }
    }

    // Stores the count of elements
    int count = 0;

    int kleastfreqsum = 0;

    // Traverse the frequency array
    for (int i = 0; i <= n; i++) {

      // Find the kleastfreqsum
      foreach(int x in freq[i])
      {
        kleastfreqsum += x;
        count++;
        if (count == k)
          break;
      }

      // If the count is K, break
      if (count == k)
        break;
    }

    // Reinitialize the count to zero
    count = 0;

    int kmostfreqsum = 0;

    // Traverse the frequency
    for (int i = n; i >= 0; i--) {

      // Find the kmostfreqsum
      foreach(int x in freq[i])
      {
        kmostfreqsum += x;
        count++;
        if (count == k)
          break;
      }

      // If the count is K, break
      if (count == k)
        break;
    }

    // Comparing the sum
    if (kleastfreqsum == kmostfreqsum)
      return "Yes";

    // Otherwise, return No
    return "No";
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 3, 2, 1, 2, 3, 3, 4 };
    int N = arr.Length;
    int K = 2;

    Console.Write(checkSum(arr, N, K));
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to compare the sum of K
        // most and least occurrences
        function checkSum(arr, n, k) {
            // Stores frequency of array element
            let m = new Map();
            for (let i = 0; i < n; i++) {
                if (m.has(arr[i])) {
                    m.set(m.get(arr[i]), m.get(arr[i]) + 1)
                }
                else {
                    m.set(arr[i], 1);
                }

            }

            // Stores the frequencies as indexes
            // and putelements with the frequency
            // in a vector
            let freq = new Array(n + 1);
            for (let i = 0; i < n; i++) {

                // Find the frequency
                let f = m.get(arr[i]);

                if (f != -1) {

                    // Insert in the vector
                    freq[f] = new Array();
                    freq[f].push(arr[i]);
                    m.set(arr[i], -1);
                }
            }

            // Stores the count of elements
            let count = 0;

            let kleastfreqsum = 0;

            // Traverse the frequency array
            for (let i = 0; i <= n; i++) {

                // Find the kleastfreqsum
                for (let x in freq[i]) {
                    kleastfreqsum += x;
                    count++;
                    if (count == k)
                        break;
                }

                // If the count is K, break
                if (count == k)
                    break;
            }

            // Reinitialize the count to zero
            count = 0;

            let kmostfreqsum = 0;

            // Traverse the frequency
            for (let i = n; i >= 0; i--) {

                // Find the kmostfreqsum
                for (let x in freq[i]) {
                    kmostfreqsum += x;
                    count++;
                    if (count == k)
                        break;
                }

                // If the count is K, break
                if (count == k)
                    break;
            }

            // Comparing the sum
            if (kleastfreqsum == kmostfreqsum)
                return "Yes";

            // Otherwise, return No
            return "No";
        }

        // Driver Code

        let arr = [3, 2, 1, 2, 3, 3, 4];
        let N = arr.length;
        let K = 2;

        document.write(checkSum(arr, N, K));

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)