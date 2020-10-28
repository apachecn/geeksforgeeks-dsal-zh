# 具有完全 K 个完美平方数的子数组的计数

> 原文：[https://www.geeksforgeeks.org/count-of-subarrays-having-exactly-k-perfect-square-numbers/](https://www.geeksforgeeks.org/count-of-subarrays-having-exactly-k-perfect-square-numbers/)

给定未排序的整数数组 **arr []** 和整数 **K** 。 任务是使用正整数 K [完美平方数](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)来计数子数组的数量。

**范例**：

> **输入**：arr [] = {2，4，9，3}，K = 2
> **输出**：4
> **说明**：
> 由于数组中的完美平方数总数为 2。
> 因此具有 2 个完美平方数的 4 个子数组为：
> 1\. {2，4，9}
> 2\. {2，4， 9，3}
> 3\. {4，9}
> 4\. {4，9，3}
> 
> **输入**：arr [] = {4，2，5}，K = 3
> **输出**：0

**简单方法**：

如果计数等于 K，则生成所有子数组并计算给定子数组中的完美数数量，并增加 ans 变量的数量。

***时间复杂度**：O（N <sup>2</sup> ）*

**有效方法**：

1.  遍历给定的数组 arr []并检查元素是否为[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。

2.  如果当前元素是 Perfect Square，则将该索引处的 array 值更改为 1，否则将该索引处的值更改为 0。

3.  现在，给定的数组将转换为二进制数组。

4.  现在，使用本文[中讨论的方法，在上述二进制数组中找到总和等于 K 的子数组的计数。](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/)

下面是上述方法的实现。

## C++

```cpp

// C++ program to Count of subarrays having 
// exactly K perfect square numbers. 

#include <bits/stdc++.h> 
using namespace std; 

// A utility function to check if 
// the number n is perfect square 
// or not 
bool isPerfectSquare(long double x) 
{ 
    // Find floating point value of 
    // square root of x. 
    long double sr = sqrt(x); 

    // If square root is an integer 
    return ((sr - floor(sr)) == 0); 
} 

// Function to find number of subarrays 
// with sum exactly equal to k 
int findSubarraySum(int arr[], int n, int K) 
{ 
    // STL map to store number of subarrays 
    // starting from index zero having 
    // particular value of sum. 
    unordered_map<int, int> prevSum; 

    int res = 0; 

    // To store the sum of element traverse 
    // so far 
    int currsum = 0; 

    for (int i = 0; i < n; i++) { 

        // Add current element to currsum 
        currsum += arr[i]; 

        // If currsum = K, then a new 
        // subarray is found 
        if (currsum == K) { 
            res++; 
        } 

        // If currsum > K then find the 
        // no. of subarrays with sum 
        // currsum - K and exclude those 
        // subarrays 
        if (prevSum.find(currsum - K) 
            != prevSum.end()) 
            res += (prevSum[currsum - K]); 

        // Add currsum to count of 
        // different values of sum 
        prevSum[currsum]++; 
    } 

    // Return the final result 
    return res; 
} 

// Function to count the subarray with K 
// perfect square numbers 
void countSubarray(int arr[], int n, int K) 
{ 
    // Update the array element 
    for (int i = 0; i < n; i++) { 

        // If current element is perfect 
        // square then update the 
        // arr[i] to 1 
        if (isPerfectSquare(arr[i])) { 
            arr[i] = 1; 
        } 

        // Else change arr[i] to 0 
        else { 
            arr[i] = 0; 
        } 
    } 

    // Function Call 
    cout << findSubarraySum(arr, n, K); 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 2, 4, 9, 2 }; 
    int K = 2; 
    int N = sizeof(arr) / sizeof(arr[0]); 

    // Function Call 
    countSubarray(arr, N, K); 
    return 0; 
} 

```

## Java

```java

// Java program to Count of subarrays having 
// exactly K perfect square numbers. 
import java.util.*; 

class GFG { 

// A utility function to check if 
// the number n is perfect square 
// or not 
static boolean isPerfectSquare(double x) 
{ 

    // Find floating point value of 
    // square root of x. 
    double sr = Math.sqrt(x); 

    // If square root is an integer 
    return ((sr - Math.floor(sr)) == 0); 
} 

// Function to find number of subarrays 
// with sum exactly equal to k 
static int findSubarraySum(int arr[],  
                           int n, int K) 
{ 

    // Map to store number of subarrays 
    // starting from index zero having 
    // particular value of sum. 
    Map<Integer, Integer> prevSum = new HashMap<>(); 

    int res = 0; 

    // To store the sum of element  
    // traverse so far 
    int currsum = 0; 

    for(int i = 0; i < n; i++) 
    { 

       // Add current element to currsum 
       currsum += arr[i]; 

       // If currsum = K, then a new 
       // subarray is found 
       if (currsum == K) 
       { 
           res++; 
       } 

       // If currsum > K then find the 
       // no. of subarrays with sum 
       // currsum - K and exclude those 
       // subarrays 
       if (prevSum.containsKey(currsum - K)) 
           res += (prevSum.get(currsum - K)); 

       // Add currsum to count of 
       // different values of sum 
       prevSum.put(currsum,  
                   prevSum.getOrDefault(currsum, 0) + 1); 
    } 

    // Return the final result 
    return res; 
} 

// Function to count the subarray with K 
// perfect square numbers 
static void countSubarray(int arr[], int n, int K) 
{ 

    // Update the array element 
    for(int i = 0; i < n; i++) 
    { 

       // If current element is perfect 
       // square then update the 
       // arr[i] to 1 
       if (isPerfectSquare(arr[i])) 
       { 
           arr[i] = 1; 
       } 

       // Else change arr[i] to 0 
       else 
       { 
           arr[i] = 0; 
       } 
    } 

    // Function Call 
    System.out.println(findSubarraySum(arr, n, K)); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = { 2, 4, 9, 2 }; 
    int K = 2; 
    int N = arr.length; 

    // Function Call 
    countSubarray(arr, N, K); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to count of subarrays  
# having exactly K perfect square numbers. 
from collections import defaultdict  
import math  

# A utility function to check if 
# the number n is perfect square 
# or not 
def isPerfectSquare(x): 

    # Find floating point value of 
    # square root of x. 
    sr = math.sqrt(x) 

    # If square root is an integer 
    return ((sr - math.floor(sr)) == 0) 

# Function to find number of subarrays 
# with sum exactly equal to k 
def findSubarraySum(arr, n, K): 

    # STL map to store number of subarrays 
    # starting from index zero having 
    # particular value of sum. 
    prevSum = defaultdict(int) 

    res = 0

    # To store the sum of element traverse 
    # so far 
    currsum = 0

    for i in range(n): 

        # Add current element to currsum 
        currsum += arr[i] 

        # If currsum = K, then a new 
        # subarray is found 
        if (currsum == K): 
            res += 1

        # If currsum > K then find the 
        # no. of subarrays with sum 
        # currsum - K and exclude those 
        # subarrays 
        if ((currsum - K) in prevSum): 
            res += (prevSum[currsum - K]) 

        # Add currsum to count of 
        # different values of sum 
        prevSum[currsum] += 1

    # Return the final result 
    return res 

# Function to count the subarray with K 
# perfect square numbers 
def countSubarray(arr, n, K): 

    # Update the array element 
    for i in range(n): 

        # If current element is perfect 
        # square then update the 
        # arr[i] to 1 
        if (isPerfectSquare(arr[i])): 
            arr[i] = 1

        # Else change arr[i] to 0 
        else: 
            arr[i] = 0

    # Function Call 
    print(findSubarraySum(arr, n, K)) 

# Driver Code 
if __name__ == "__main__": 

    arr = [ 2, 4, 9, 2 ] 
    K = 2
    N = len(arr) 

    # Function Call 
    countSubarray(arr, N, K) 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# program to count of subarrays having 
// exactly K perfect square numbers. 
using System;  
using System.Collections;  
using System.Collections.Generic;  

class GFG{ 

// A utility function to check if 
// the number n is perfect square 
// or not 
static bool isPerfectSquare(double x) 
{ 

    // Find floating point value of 
    // square root of x. 
    double sr = Math.Sqrt(x); 

    // If square root is an integer 
    return ((sr - Math.Floor(sr)) == 0); 
} 

// Function to find number of subarrays 
// with sum exactly equal to k 
static int findSubarraySum(int []arr,  
                           int n, int K) 
{ 

    // Map to store number of subarrays 
    // starting from index zero having 
    // particular value of sum. 
    Dictionary<int, 
               int> prevSum = new Dictionary<int,  
                                             int>();  

    int res = 0; 

    // To store the sum of element  
    // traverse so far 
    int currsum = 0; 

    for(int i = 0; i < n; i++) 
    { 

        // Add current element to currsum 
        currsum += arr[i]; 

        // If currsum = K, then a new 
        // subarray is found 
        if (currsum == K) 
        { 
            res++; 
        } 

        // If currsum > K then find the 
        // no. of subarrays with sum 
        // currsum - K and exclude those 
        // subarrays 
        if (prevSum.ContainsKey(currsum - K)) 
            res += (prevSum[currsum - K]); 

        // Add currsum to count of 
        // different values of sum 
        if(prevSum.ContainsKey(currsum)) 
        { 
            prevSum[currsum]++; 
        } 
        else
        { 
            prevSum[currsum] = 1; 
        } 
    } 

    // Return the final result 
    return res; 
} 

// Function to count the subarray with K 
// perfect square numbers 
static void countSubarray(int []arr, int n, 
                                     int K) 
{ 

    // Update the array element 
    for(int i = 0; i < n; i++) 
    { 

        // If current element is perfect 
        // square then update the 
        // arr[i] to 1 
        if (isPerfectSquare(arr[i])) 
        { 
            arr[i] = 1; 
        } 

        // Else change arr[i] to 0 
        else
        { 
            arr[i] = 0; 
        } 
    } 

    // Function call 
    Console.Write(findSubarraySum(arr, n, K)); 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    int []arr = { 2, 4, 9, 2 }; 
    int K = 2; 
    int N = arr.Length; 

    // Function call 
    countSubarray(arr, N, K); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:**

```
4

```

***时间复杂度**：O（N）

**空间复杂度**：O（N）*



* * *

* * *



