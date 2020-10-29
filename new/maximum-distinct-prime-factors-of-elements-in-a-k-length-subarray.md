# K 长度子数组

> 原文：[https://www.geeksforgeeks.org/maximum-distinct-prime-factors-of-elements-in-a-k-length-subarray/](https://www.geeksforgeeks.org/maximum-distinct-prime-factors-of-elements-in-a-k-length-subarray/)

中元素的最大不同素因数

给定 **N** 个正整数的数组 **arr []** 和一个整数 **K** ，任务是在 长度为 **K** 的[子阵列](https://www.geeksforgeeks.org/tag/subarray/)。

**示例**：

> **输入**：arr [] = {5，9，14，6，10，77}，K = 3
> **输出**：5
> **说明**：[
> 长度为 3 的子数组，具有最大不同的素因数为 6、10、77，素因数为 2、3、5、7、11。
> 
> **输入**：arr [] = {4，2，6，10}，K = 3
> **输出**：3
> **说明**：
> 长度为 3 的子数组，其最大素因数最大为 2、6、10，素因数为 2、3、5。

**朴素的方法**：最简单的方法是[生成长度为 **K** 的所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并遍历每个子阵列并计算不同的[主因子](http://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) 它的元素。 最后，打印为任何子阵列获得的独特素数的最大数量。

**时间复杂度**：O（N <sup>2</sup> log N）

**辅助空间**：`O(n)`

**高效方法**：的想法是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)解决此问题。 请按照以下步骤操作：

1.  使用[筛选](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成并存储每个元素的[最小素数](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)。

2.  将前 K 个数组元素的不同素数存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

3.  通过将当前元素添加到前一个子数组并删除前一个子数组的第一个元素，遍历保留 K 长度窗口的剩余数组

4.  找到新添加的元素到子数组的所有主要因子，并将其存储在 **Map** 中。 从**映射**中减去删除元素的质数因子的频率。

5.  对整个阵列完成上述操作后，打印为任何子阵列获得的最大[映射大小](https://www.geeksforgeeks.org/mapsize-c-stl/)作为答案。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

#define Max 100001 

// Stores smallest prime 
// factor for every number 
int spf[Max]; 

// Function to calculate smallest 
// prime factor of every number 
void sieve() 
{ 
    // Marking smallest prime factor 
    // of every number to itself 
    for (int i = 1; i < Max; i++) 
        spf[i] = i; 

    // Seperately marking smallest prime 
    // factor of every even number to be 2 
    for (int i = 4; i < Max; i = i + 2) 
        spf[i] = 2; 

    for (int i = 3; i * i < Max; i++) 

        // If i is prime 
        if (spf[i] == i) { 

            // Mark spf for all numbers divisible by i 
            for (int j = i * i; j < Max; j = j + i) { 

                // Marking spf[j] if it is not 
                // previously marked 
                if (spf[j] == j) 
                    spf[j] = i; 
            } 
        } 
} 

// Function to find maximum distinct 
// prime factors of subarray of length k 
int maximumDPF(int arr[], int n, int k) 
{ 
    // Precalculate Smallest 
    // Prime Factors 
    sieve(); 

    int ans = 0, num; 

    // Stores distinct prime factors 
    // for subarrays of size k 
    unordered_map<int, int> maps; 

    // Calculate total prime factors 
    // for first k array elements 
    for (int i = 0; i < k; i++) { 

        // Calculate prime factors of 
        // every element in O(logn) 
        num = arr[i]; 
        while (num != 1) { 

            maps[spf[num]]++; 
            num = num / spf[num]; 
        } 
    } 

    // Update maximum distinct 
    // prime factors obtained 
    ans = max((int)maps.size(), ans); 

    for (int i = k; i < n; i++) { 

        // Remove prime factors of 
        // the removed element 
        num = arr[i - k]; 
        while (num != 1) { 

            // Reduce frequencies 
            // of prime factors 
            maps[spf[num]]--; 

            if (maps[spf[num]] == 0) 

                // Erase that index from map 
                maps.erase(spf[num]); 

            num = num / spf[num]; 
        } 

        // Find prime factoes of 
        // added element 
        num = arr[i]; 
        while (num != 1) { 

            // Increase frequencies 
            // of prime factors 
            maps[spf[num]]++; 
            num = num / spf[num]; 
        } 

        // Update maximum distinct 
        // prime factors obtained 
        ans = max((int)maps.size(), ans); 
    } 

    return ans; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 4, 2, 6, 10 }; 
    int k = 3; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << maximumDPF(arr, n, k) << endl; 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.io.*; 
import java.util.*; 

class GFG { 

    static int Max = 100001; 
    static int spf[] = new int[Max]; 

    // Function to precalculate smallest 
    // prime factor of every number 
    public static void sieve() 
    { 
        // Marking smallest prime factor 
        // of every number to itself. 
        for (int i = 1; i < Max; i++) 
            spf[i] = i; 

        // Seperately marking smallest prime 
        // factor of every even number to be 2 
        for (int i = 4; i < Max; i = i + 2) 
            spf[i] = 2; 

        for (int i = 3; i * i < Max; i++) 

            // If i is prime 
            if (spf[i] == i) { 

                // Mark spf for all numbers divisible by i 
                for (int j = i * i; j < Max; j = j + i) { 

                    // Marking spf[j] if it is not 
                    // previously marked 
                    if (spf[j] == j) 
                        spf[j] = i; 
                } 
            } 
    } 

    // Function to find maximum distinct 
    // prime factors of subarray of length k 
    public static int maximumDPF(int arr[], int n, int k) 
    { 
        // Precalculate smallest 
        // prime factor 
        sieve(); 

        int ans = 0, num; 

        // Stores distinct prime factors 
        // for subarrays of size k 
        Map<Integer, Integer> maps 
            = new HashMap<Integer, Integer>(); 

        // Calculate total prime factors 
        // for first k array elements 
        for (int i = 0; i < k; i++) { 

            // Calculate prime factors of 
            // every element in O(logn) 
            num = arr[i]; 
            while (num != 1) { 

                maps.put(spf[num], 
                         maps.getOrDefault(spf[num], 0) 
                             + 1); 
                num = num / spf[num]; 
            } 
        } 

        // Update maximum distinct 
        // prime factors obtained 
        ans = Math.max((int)maps.size(), ans); 

        for (int i = k; i < n; i++) { 

            // Remove prime factors of 
            // the removed element 
            num = arr[i - k]; 
            while (num != 1) { 

                // Reduce frequencies 
                // of prime factors 
                maps.put(spf[num], 
                         maps.getOrDefault(spf[num], 0) 
                             - 1); 

                if (maps.get(spf[num]) == 0) 
                    maps.remove(spf[num]); 

                num = num / spf[num]; 
            } 

            // Insert prime factors of 
            // the added element 
            num = arr[i]; 
            while (num != 1) { 

                // Increase frequencies 
                // of prime factors 
                maps.put(spf[num], 
                         maps.getOrDefault(spf[num], 0) 
                             + 1); 
                num = num / spf[num]; 
            } 

            // Update maximum distinct 
            // prime factors obtained 
            ans = Math.max((int)maps.size(), ans); 
        } 

        return ans; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int arr[] = { 4, 2, 6, 10 }; 

        int k = 3; 
        int n = arr.length; 

        System.out.println(maximumDPF(arr, n, k)); 
    } 
} 

```

## Python3

```py

# Python program for the above approach 
import math as mt 

Max = 100001

# Stores smallest prime factor for 
# every number 
spf = [0 for i in range(Max)] 

# Function to precalculate smallest 
# prime factor of every number 

def sieve(): 

  # Marking smallest prime factor of every 
    # number to itself. 
    for i in range(1, Max): 
        spf[i] = i 

    # Separately marking spf for 
    # every even number as 2 
    for i in range(4, Max, 2): 
        spf[i] = 2

    for i in range(3, mt.ceil(mt.sqrt(Max))): 

        # Checking if i is prime 
        if (spf[i] == i): 

            # marking SPF for all numbers 
            # divisible by i 
            for j in range(i * i, Max, i): 

                # marking spf[j] if it is 
                # not previously marked 
                if (spf[j] == j): 
                    spf[j] = i 

# Function to find maximum  
# distinct prime factors 
# of the subarray of length k 

def maximumDPF(arr, n, k): 

    # precalculating Smallest Prime Factor 
    sieve() 

    ans = 0

    # map to store distinct prime factor 
    # for subarray of size k 
    maps = {} 

    # Calculating the total prime factors 
    # for first k elements 
    for i in range(0, k): 

        # Calculating prime factors of 
        # every element in O(logn) 
        num = arr[i] 
        while num != 1: 
            maps[spf[num]] = maps.get( 
                             spf[num], 0)+1
            num = int(num / spf[num]) 

    ans = max(len(maps), ans) 

    for i in range(k, n): 

        # Perform operation for 
        # removed element 
        num = arr[i - k] 
        while num != 1: 

            maps[spf[num]] = maps.get( 
                             spf[num], 0)-1

            # if value in map become 0, 
            # then erase that index from map 
            if maps.get(spf[num], 0) == 0: 
                maps.pop(spf[num]) 

            num = int(num / spf[num]) 

        # Perform operation for 
        # added element 
        num = arr[i] 
        while num != 1: 

            maps[spf[num]] = int(maps.get( 
                                 spf[num], 0))+1
            num = int(num / spf[num]) 

        ans = max(len(maps), ans) 

    return ans 

# Driver Code 
if __name__ == '__main__': 

    # Given array arr 
    arr = [4, 2, 6, 10] 

    # Given subarray size K 
    k = 3
    n = len(arr) 

    # Function call 
    print(maximumDPF(arr, n, k)) 

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

public class GFG { 

    public static int Max = 100001; 

    static int[] spf = new int[Max]; 

    // Function to precalculate smallest 
    // prime factor of every number 
    public static void sieve() 
    { 
        // Marking smallest prime factor 
        // of every number to itself 
        for (int i = 1; i < Max; i++) 
            spf[i] = i; 

        // Marking smallest prime factor 
        // of every even number to be 2 
        for (int i = 4; i < Max; i = i + 2) 
            spf[i] = 2; 

        for (int i = 3; i * i < Max; i++) 

            // checking if i is prime 
            if (spf[i] == i) { 

                // Marking spf for all 
                // numbers divisible by i 
                for (int j = i * i; j < Max; j = j + i) { 

                    // Marking spf[j] if it is not 
                    // previously marked 
                    if (spf[j] == j) 
                        spf[j] = i; 
                } 
            } 
    } 

    // Function to find maximum 
    // distinct prime factors 
    // of the subarray of length k 
    public static int maximumDPF(int[] arr, 
                                 int n, int k) 
    { 
        // precalculating Smallest Prime Factor 
        sieve(); 

        int ans = 0, num, currentCount; 

        // Stores distinct prime factors 
        // for subarrays of size k 
        var maps = new Dictionary<int, int>(); 

        // Calculating the total prime factors 
        // for first k array elements 
        for (int i = 0; i < k; i++) { 

            // Calculating prime factors of 
            // every element in O(logn) 
            num = arr[i]; 
            while (num != 1) { 

                // Increase frequencies of 
                // prime factors 
                maps.TryGetValue(spf[num], 
                                 out currentCount); 
                maps[spf[num]] = currentCount + 1; 
                num = num / spf[num]; 
            } 
        } 

        // Update maximum distinct 
        // prime factors obtained 
        ans = Math.Max(maps.Count, ans); 

        for (int i = k; i < n; i++) { 

            // Remove prime factors of 
            // removed element 
            num = arr[i - k]; 
            while (num != 1) { 

                // Reduce frequencies 
                // of prime factors 
                maps.TryGetValue(spf[num], 
                                 out currentCount); 
                maps[spf[num]] = currentCount - 1; 

                if (maps[spf[num]] == 0) 

                    // Erase that index from map 
                    maps.Remove(spf[num]); 

                num = num / spf[num]; 
            } 

            // Insert prime factors 
            // added element 
            num = arr[i]; 
            while (num != 1) { 

                // Increase frequencies 
                // of prime factors 
                maps.TryGetValue(spf[num], 
                                 out currentCount); 
                maps[spf[num]] = currentCount + 1; 
                num = num / spf[num]; 
            } 

            ans = Math.Max(maps.Count, ans); 
        } 

        // Update maximum distinct 
        // prime factors obtained 
        return ans; 
    } 

    // Driver code 
    static public void Main() 
    { 

        // Given array arr[] 
        int[] arr = { 4, 2, 6, 10 }; 

        // Given subarray size K 
        int k = 3; 
        int n = arr.Length; 

        Console.Write(maximumDPF(arr, n, k)); 
    } 
}

```

**Output:**

```
3

```

**时间复杂度**：O（N * log N）

**辅助空间**：`O(n)`



* * *

* * *



