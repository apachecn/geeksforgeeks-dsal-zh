# 总和等于 k 的子数组数

> 原文：[https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/)

给定一个未排序的整数数组，找到总和等于给定数 k 的子数组的数量。

**示例**：

```
Input : arr[] = {10, 2, -2, -20, 10}, 
        k = -10
Output : 3
Subarrays: arr[0...3], arr[1...4], arr[3..4]
have sum exactly equal to -10.

Input : arr[] = {9, 4, 20, 3, 10, 5},
            k = 33
Output : 2
Subarrays : arr[0...2], arr[2...4] have sum
exactly equal to 33.

```

**天真的解决方案–**

一个简单的解决方案是遍历所有子数组并计算其总和。 如果总和等于所需总和，则增加子数组的数量。 打印子数组的最终计数。 天真的解决方案的 Java 实现-

## C++

```cpp

// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;
int main()
{
  int arr[] = {10, 2, -2, -20, 10};
  int k = -10;
  int n = sizeof(arr) / sizeof(arr[0]);
  int res = 0;

  // Calculate all subarrays
  for (int i = 0; i < n; i++) 
  {
    int sum = 0;
    for (int j = i; j < n; j++)
    {
      // Calculate required sum
      sum += arr[j];

      // Check if sum is equal to
      // required sum
      if (sum == k)
        res++;
    }
  }
  cout << (res) << endl;
}

// This code is contributed by Chitranayal

```

## Java

```java

import java.util.*;
class Solution {

    public static void main(String[] args)
    {
        int arr[] = { 10, 2, -2, -20, 10 };
        int k = -10;
        int n = arr.length;
        int res = 0;

        // calculate all subarrays
        for (int i = 0; i < n; i++) {

            int sum = 0;
            for (int j = i; j < n; j++) {

                // calculate required sum
                sum += arr[j];

                // check if sum is equal to
                // required sum
                if (sum == k)
                    res++;
            }
        }
        System.out.println(res);
    }
}

```

**Output:** 

```
3

```

**高效解决方案–**

高效解决方案是遍历数组时，以求和方式存储到目前为止的总和。 另外，请在地图中维护不同的求和值计数。 如果在任何情况下，currsum 的值等于所需的总和，则子数组的个数增加 1。 currsum 的值超过 currsum – sum 的期望总和。 如果从并购中删除此值，则可以获得所需的总和。 从图中找到先前发现的总和等于 currsum-sum 的子数组的数量。 从当前子阵列中排除所有这些子阵列，将得到具有所需总和的新子阵列。 因此，通过此类子数组的数量增加计数。 请注意，当 currsum 等于所需的总和时，还应检查先前总和等于 0 的子数组的数量。从当前子数组中排除这些子数组会得到具有所需总和的新子数组。 在这种情况下，将计数增加总和为 0 的子数组的数量。

## C++

```cpp

// C++ program to find number of subarrays
// with sum exactly equal to k.
#include <bits/stdc++.h>
using namespace std;

// Function to find number of subarrays
// with sum exactly equal to k.
int findSubarraySum(int arr[], int n, int sum)
{
    // STL map to store number of subarrays
    // starting from index zero having
    // particular value of sum.
    unordered_map<int, int> prevSum;

    int res = 0;

    // Sum of elements so far.
    int currsum = 0;

    for (int i = 0; i < n; i++) {

        // Add current element to sum so far.
        currsum += arr[i];

        // If currsum is equal to desired sum,
        // then a new subarray is found. So
        // increase count of subarrays.
        if (currsum == sum)
            res++;

        // currsum exceeds given sum by currsum
        //  - sum. Find number of subarrays having
        // this sum and exclude those subarrays
        // from currsum by increasing count by
        // same amount.
        if (prevSum.find(currsum - sum) != prevSum.end())
            res += (prevSum[currsum - sum]);

        // Add currsum value to count of
        // different values of sum.
        prevSum[currsum]++;
    }

    return res;
}

int main()
{
    int arr[] = { 10, 2, -2, -20, 10 };
    int sum = -10;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSubarraySum(arr, n, sum);
    return 0;
}

```

## Java

```java

// Java program to find number of subarrays
// with sum exactly equal to k.
import java.util.HashMap;
import java.util.Map;

public class GfG {

    // Function to find number of subarrays
    // with sum exactly equal to k.
    static int findSubarraySum(int arr[], int n, int sum)
    {
        // HashMap to store number of subarrays
        // starting from index zero having
        // particular value of sum.
        HashMap<Integer, Integer> prevSum = new HashMap<>();

        int res = 0;

        // Sum of elements so far.
        int currsum = 0;

        for (int i = 0; i < n; i++) {

            // Add current element to sum so far.
            currsum += arr[i];

            // If currsum is equal to desired sum,
            // then a new subarray is found. So
            // increase count of subarrays.
            if (currsum == sum)
                res++;

            // currsum exceeds given sum by currsum
            //  - sum. Find number of subarrays having
            // this sum and exclude those subarrays
            // from currsum by increasing count by
            // same amount.
            if (prevSum.containsKey(currsum - sum))
                res += prevSum.get(currsum - sum);

            // Add currsum value to count of
            // different values of sum.
            Integer count = prevSum.get(currsum);
            if (count == null)
                prevSum.put(currsum, 1);
            else
                prevSum.put(currsum, count + 1);
        }

        return res;
    }

    public static void main(String[] args)
    {

        int arr[] = { 10, 2, -2, -20, 10 };
        int sum = -10;
        int n = arr.length;
        System.out.println(findSubarraySum(arr, n, sum));
    }
}

// This code is contributed by Rituraj Jain

```

## Python3

```py

# Python3 program to find the number of 
# subarrays with sum exactly equal to k. 
from collections import defaultdict

# Function to find number of subarrays  
# with sum exactly equal to k. 
def findSubarraySum(arr, n, Sum): 

    # Dictionary to store number of subarrays 
    # starting from index zero having  
    # particular value of sum. 
    prevSum = defaultdict(lambda : 0)

    res = 0

    # Sum of elements so far. 
    currsum = 0

    for i in range(0, n):  

        # Add current element to sum so far. 
        currsum += arr[i] 

        # If currsum is equal to desired sum, 
        # then a new subarray is found. So 
        # increase count of subarrays. 
        if currsum == Sum:  
            res += 1        

        # currsum exceeds given sum by currsum  - sum.
        # Find number of subarrays having  
        # this sum and exclude those subarrays 
        # from currsum by increasing count by  
        # same amount. 
        if (currsum - Sum) in prevSum:
            res += prevSum[currsum - Sum] 

        # Add currsum value to count of  
        # different values of sum. 
        prevSum[currsum] += 1

    return res 

if __name__ == "__main__":

    arr =  [10, 2, -2, -20, 10]  
    Sum = -10
    n = len(arr) 
    print(findSubarraySum(arr, n, Sum)) 

# This code is contributed by Rituraj Jain

```

## C#

```cs

// C# program to find number of subarrays
// with sum exactly equal to k.
using System;
using System.Collections.Generic;

class GFG {
    // Function to find number of subarrays
    // with sum exactly equal to k.
    public static int findSubarraySum(int[] arr,
                                      int n, int sum)
    {

        // HashMap to store number of subarrays
        // starting from index zero having
        // particular value of sum.
        Dictionary<int, int> prevSum = new Dictionary<int, int>();

        int res = 0;

        // Sum of elements so far
        int currsum = 0;

        for (int i = 0; i < n; i++) {

            // Add current element to sum so far.
            currsum += arr[i];

            // If currsum is equal to desired sum,
            // then a new subarray is found. So
            // increase count of subarrays.
            if (currsum == sum)
                res++;

            // currsum exceeds given sum by currsum
            // - sum. Find number of subarrays having
            // this sum and exclude those subarrays
            // from currsum by increasing count by
            // same amount.
            if (prevSum.ContainsKey(currsum - sum))
                res += prevSum[currsum - sum];

            // Add currsum value to count of
            // different values of sum.
            if (!prevSum.ContainsKey(currsum))
                prevSum.Add(currsum, 1);
            else {
                int count = prevSum[currsum];
                prevSum[currsum] = count + 1;
            }
        }
        return res;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 10, 2, -2, -20, 10 };
        int sum = -10;
        int n = arr.Length;
        Console.Write(findSubarraySum(arr, n, sum));
    }
}

// This code is contributed by
// sanjeev2552

```

**Output:** 

```
3

```

**时间复杂度**：O（nlogn）

**辅助空间**：O（n）



* * *

* * *



