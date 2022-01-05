# 清空数组所需的 K 个相等元素的最小移除量

> 原文:[https://www . geeksforgeeks . org/minimum-remove-k-equal-elements-需要清空数组/](https://www.geeksforgeeks.org/minimum-removal-of-k-equal-elements-required-to-empty-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算需要移除最多 K 个等元素使数组为空的最小次数**。**

**示例:**

> **输入:** arr[] = {1，3，1，1，3}，K = 2
> **输出:** 3
> **解释:**
> **第一步:**从数组中最多移除 2 个 1s。修改后的数组是{1，3，3}。
> **步骤 2:** 从阵列中最多移除 2 个 3s。修改后的数组是{1}。
> **步骤 3:** 从阵列中最多移除 2 个 1s。修改后的数组是{}。
> 3 步后，数组变为空。
> 因此，所需的最小步骤数为 3。
> 
> **输入** : arr[] = {4，4，7，3，1，1，2，1，7，3}，K = 5
> **输出** : 5

**天真法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[统计每个数组元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率，然后将每个元素的频率除以 **K** 再加到**计数**中。如果数组元素的频率不能被 **K** 整除，则递增**计数**。完成上述步骤后，打印**计数**的值作为结果。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过[哈希](https://www.geeksforgeeks.org/generic-map-in-java/)进行优化，存储每个数组元素的频率，然后统计所需的最小运算次数。按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，它存储所需的最小步数。
*   初始化 [Hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，存储数组中每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arraylists-java/)**arr【】**并将每个元素的[频率存储在 Hashmap 中。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历 Hashmap](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) ，将每个元素的频率值除以 **K** ，得到变量**计数**。如果当前数组元素的频率不能被 **K** 整除，那么将**计数**增加 **1** 。
*   完成上述步骤后，打印**计数**作为使数组为空所需的最小步骤数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of steps required to empty
// given array by removing at most K
// equal array elements in each operation
void minSteps(int arr[], int N, int K)
{

    // Stores the minimum number of
    // steps required to empty the array
    int count = 0;

    // Stores the occurrence
    // of each array element
    map<int, int> cntFreq;
    for (int i = 0; i < N; i++)
    {

        // Update the frequency
        cntFreq[arr[i]]++;
    }

    // Traverse the Hashmap
    for (auto i : cntFreq)
    {

        // Check if the frequency
        // is divisible by K or not
        if (i.first % K == 0)
            count += i.second / K;

        // Otherwise
        else
            count += (i.second / K) + 1;
    }

    // Print the count of
    // minimum steps required
    cout << (count);
}

// Driver Code
int main()
{

    int arr[] = { 4, 4, 7, 3, 1,
                 1, 2, 1, 7, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 5;
    minSteps(arr, N, K);
    return 0;
}

// This code is contributed by Dharanendra L V.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class GFG {

    // Function to count the minimum
    // number of steps required to empty
    // given array by removing at most K
    // equal array elements in each operation
    public static void minSteps(
        int[] arr, int N, int K)
    {
        // Stores the minimum number of
        // steps required to empty the array
        int count = 0;

        // Stores the occurrence
        // of each array element
        Map<Integer, Integer> cntFreq
            = new HashMap<Integer, Integer>();

        for (int i = 0; i < N; i++) {

            // Update the frequency
            cntFreq.put(
                arr[i],
                cntFreq.getOrDefault(
                    arr[i], 0)
                    + 1);
        }

        // Traverse the Hashmap
        for (Integer i : cntFreq.keySet()) {

            // Check if the frequency
            // is divisible by K or not
            if (cntFreq.get(i) % K == 0)
                count += cntFreq.get(i)
                         / K;

            // Otherwise
            else
                count += (cntFreq.get(i)
                          / K)
                         + 1;
        }

        // Print the count of
        // minimum steps required
        System.out.print(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 4, 4, 7, 3, 1,
                      1, 2, 1, 7, 3 };
        int N = arr.length;
        int K = 5;

        minSteps(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum
# number of steps required to empty
# given array by removing at most K
# equal array elements in each operation
def minSteps(arr, N, K) :

    # Stores the minimum number of
    # steps required to empty the array
    count = 0

    # Stores the occurrence
    # of each array element
    cntFreq = {}
    for i in range(N) :

        # Update the frequency
        if arr[i] in cntFreq :
            cntFreq[arr[i]] += 1
        else :
            cntFreq[arr[i]] = 1

    # Traverse the Hashmap
    for i in cntFreq :

        # Check if the frequency
        # is divisible by K or not
        if (i % K == 0) :
            count += cntFreq[i] // K

        # Otherwise
        else :
            count += (cntFreq[i] // K) + 1

    # Print the count of
    # minimum steps required
    print(count)

arr = [ 4, 4, 7, 3, 1, 1, 2, 1, 7, 3 ]
N = len(arr)
K = 5
minSteps(arr, N, K)

# This code is contributed by divyeshabadiya07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    // Function to count the minimum
    // number of steps required to empty
    // given array by removing at most K
    // equal array elements in each operation
    public static void minSteps(
        int[] arr, int N, int K)
    {
        // Stores the minimum number of
        // steps required to empty the array
        int count = 0;

        // Stores the occurrence
        // of each array element
        Dictionary<int, int> cntFreq
            = new Dictionary<int, int>();

        for (int i = 0; i < N; i++) {

            // Update the frequency
            if(cntFreq.ContainsKey(arr[i]))
                cntFreq[arr[i]] = cntFreq[arr[i]]+1;
            else

            cntFreq.Add(arr[i],1);
        }

        // Traverse the Hashmap
        foreach (int i in cntFreq.Keys) {

            // Check if the frequency
            // is divisible by K or not
            if (cntFreq[i] % K == 0)
                count += cntFreq[i]
                         / K;

            // Otherwise
            else
                count += (cntFreq[i]
                          / K)
                         + 1;
        }

        // Print the count of
        // minimum steps required
        Console.Write(count);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 4, 4, 7, 3, 1,
                      1, 2, 1, 7, 3 };
        int N = arr.Length;
        int K = 5;

        minSteps(arr, N, K);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count the minimum
      // number of steps required to empty
      // given array by removing at most K
      // equal array elements in each operation
      function minSteps(arr, N, K) {
        // Stores the minimum number of
        // steps required to empty the array
        var count = 0;

        // Stores the occurrence
        // of each array element
        var cntFreq = {};

        for (var i = 0; i < N; i++) {
          // Update the frequency
          if (cntFreq.hasOwnProperty(arr[i]))
              cntFreq[arr[i]] += 1;
          else
              cntFreq[arr[i]] = 1;
        }

        // Traverse the Hashmap
        for (const [key, value] of Object.entries(cntFreq)) {
          // Check if the frequency
          // is divisible by K or not
          if (key % K == 0)
              count += parseInt(cntFreq[key] / K);
          // Otherwise
          else
              count += parseInt(cntFreq[key] / K) + 1;
        }

        // Print the count of
        // minimum steps required
        document.write(count);
      }

      // Driver Code
      var arr = [4, 4, 7, 3, 1, 1, 2, 1, 7, 3];
      var N = arr.length;
      var K = 5;

      minSteps(arr, N, K);
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)