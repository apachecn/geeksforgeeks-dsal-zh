# 按升序打印频率等于 K 次方的所有数组元素

> 原文:[https://www . geesforgeks . org/print-all-array-elements-with-frequency-等于 k 的幂的升序/](https://www.geeksforgeeks.org/print-all-array-elements-having-frequencies-equal-to-powers-of-k-in-ascending-order/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出频率在 **K** 次方的数组元素，即 **K <sup>1</sup> ，K <sup>2</sup> ，K <sup>3</sup> 等等**。

**示例:**

> **输入:** arr[] = {1，3，2，1，2，2，3，3，4}，K = 2
> **输出:** 1 2
> **说明:**
> 1 的频率为 2，即可以表示为 K 的幂(= 2)，即 2 <sup>1</sup> 。
> 2 的频率为 4，可以表示为 K 的幂(= 2)，即 2 <sup>2</sup> 。
> 
> **输入:** arr[] = {6，1，3，1，2，2，1}，K = 2
> **输出:** 2 3 6

**天真法:**最简单的方法是[统计每个阵元](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率，如果任意一个阵元的频率是 **K** 的[完美幂，那么打印该阵元。否则，检查下一个元素。](https://www.geeksforgeeks.org/count-perfect-power-of-k-in-a-range-l-r/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来优化，用于将数组元素的频率存储在[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中，然后检查所需的条件。按照以下步骤解决给定的问题:

*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将每个数组元素的频率存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，比如说 **M** 。
*   现在，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并执行以下步骤:
    *   将映射中每个值的频率存储在一个变量中，比如 **F** 。
    *   如果**(log F)/(log K)****K<sup>(log F)/(log K)</sup>T5】的值相同，那么电流元素的频率与 **K** 的完美功率相同。因此，打印当前元素。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the array elements
// whose frequency is a power of K
void countFrequency(int arr[], int N,
                    int K)
{
    // Stores the frequency of each
    // array elements
    unordered_map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of
        // array elements
        freq[arr[i]]++;
    }

    // Traverse the map freq
    for (auto i : freq) {

        // Calculate the log value of the
        // current frequency with base K
        int lg = log(i.second) / log(K);

        // Find the power of K of log value
        int a = pow(K, lg);

        // If the values are equal
        if (a == i.second) {

            // Print the current element
            cout << i.first << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 4, 4, 2,
                  1, 2, 3, 2, 2 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countFrequency(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to find the array elements
    // whose frequency is a power of K
    static void countFrequency(int arr[], int N, int K)
    {

        // Stores the frequency of each
        // array elements
        HashMap<Integer, Integer> freq = new HashMap<>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update frequency of
            // array elements
            freq.put(arr[i],
                     freq.getOrDefault(arr[i], 0) + 1);
        }

        // Traverse the map freq
        for (int key : freq.keySet()) {

            // Calculate the log value of the
            // current frequency with base K
            int lg = (int)(Math.log(freq.get(key))
                           / Math.log(K));

            // Find the power of K of log value
            int a = (int)(Math.pow(K, lg));

            // If the values are equal
            if (a == freq.get(key)) {

                // Print the current element
                System.out.print(key + " ");
            }
        }
    }
    // Driver Code
    public static void main(String[] args)
    {

        int arr[] = { 1, 4, 4, 2, 1, 2, 3, 2, 2 };
        int K = 2;
        int N = arr.length;

        // Function Call
        countFrequency(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the array elements
from math import log

def countFrequency(arr, N, K):

    # Stores the frequency of each
    # array elements
    freq = {}

    # Traverse the array
    for i in range(N):

        # Update frequency of
        # array elements
        if (arr[i] in freq):
            freq[arr[i]] += 1
        else:
            freq[arr[i]] = 1

    # Traverse the map freq
    for key,value in freq.items():

        # Calculate the log value of the
        # current frequency with base K
        lg = log(value) // log(K)

        # Find the power of K of log value
        a = pow(K, lg)

        # If the values are equal
        if (a == value):

            # Print the current element
            print(key, end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [1, 4, 4, 2, 1, 2, 3, 2, 2]
    K = 2
    N = len(arr)

    # Function Call
    countFrequency(arr, N, K)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the array elements
// whose frequency is a power of K
static void countFrequency(int []arr, int N,
                           int K)
{

    // Stores the frequency of each
    // array elements
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency of
        // array elements
        if (freq.ContainsKey(arr[i]))
            freq[arr[i]] += 1;
        else
            freq[arr[i]] = 1;
    }

    // Traverse the map freq
    foreach (KeyValuePair<int, int> entry in freq)
    {
        int temp = entry.Key;

        // Calculate the log value of the
        // current frequency with base K
        int lg = (int)(Math.Log(entry.Value) /
                       Math.Log(K));

        // Find the power of K of log value
        int a = (int)Math.Pow(K, lg);

        // If the values are equal
        if (a == entry.Value)
        {

            // Print the current element
            Console.Write(entry.Key + " ");
        }
    }
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 4, 4, 2,
                  1, 2, 3, 2, 2 };
    int K = 2;
    int N = arr.Length;

    // Function Call
    countFrequency(arr, N, K);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the array elements
    // whose frequency is a power of K
    function countFrequency(arr, N, K)
    {

        // Stores the frequency of each
        // array elements
        let freq = new Map();
        key = [3, 2, 1, 4]

        // Traverse the array
        for(let i = 0; i < N; i++)
        {

            // Update frequency of
            // array elements
            if (freq.has(arr[i]))
                freq.set(arr[i], freq.get(arr[i]) + 1);
            else
                freq.set(arr[i], 1);
        }
        let i = 0;
        freq.forEach((values,keys)=>{
            let temp = keys;

            // Calculate the log value of the
            // current frequency with base K
            let lg = parseInt(Math.log(values) /
                           Math.log(K), 10);

            // Find the power of K of log value
            let a = parseInt(Math.pow(K, lg), 10);

            // If the values are equal
            if (a == values)
            {

                // Print the current element
                document.write(key[i] + " ");
                i++;
            }
        })
    }

    let arr = [ 1, 4, 4, 2,
                  1, 2, 3, 2, 2 ];
    let K = 2;
    let N = arr.length;

    // Function Call
    countFrequency(arr, N, K);

  // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3 2 1 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)