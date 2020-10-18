# 正整数数组中`k`个整数的最小积

> 原文： [https://www.geeksforgeeks.org/minimum-product-k-integers-array-positive-integers/](https://www.geeksforgeeks.org/minimum-product-k-integers-array-positive-integers/)

给定`n`个正整数数组。 我们需要编写一个程序来打印给定数组的`k`个整数的最小乘积。

**示例**：

```
Input : 198 76 544 123 154 675
         k = 2
Output : 9348
We get minimum product after multiplying
76 and 123.

Input : 11 8 5 7 5 100
        k = 4
Output : 1400

```



这个想法很简单，我们找到最小的`k`个元素并打印它们的乘法。 在下面的实现中，我们使用了基于[堆](https://www.geeksforgeeks.org/heap-data-structure/)的简单方法，将数组元素插入到最小堆中，然后找到前`k`个元素的乘积。

## C++ 

```cpp

// CPP program to find minimum product of 
// k elements in an array 
#include <bits/stdc++.h> 
using namespace std; 

int minProduct(int arr[], int n, int k) 
{ 
    priority_queue<int, vector<int>, greater<int> > pq; 
    for (int i = 0; i < n; i++) 
        pq.push(arr[i]); 

    int count = 0, ans = 1; 

    // One by one extract items from max heap 
    while (pq.empty() == false && count < k) { 
        ans = ans * pq.top(); 
        pq.pop(); 
        count++; 
    } 

    return ans; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {198, 76, 544, 123, 154, 675}; 
    int k = 2; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Minimum product is "
         << minProduct(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum product of  
// k elements in an array 
import java.util.PriorityQueue; 

class GFG 
{ 
    public static int minProduct(int[] arr, int n, int k)  
    { 
        PriorityQueue<Integer> pq = new PriorityQueue<>(); 
        for (int i = 0; i < n; i++) 
            pq.add(arr[i]); 

            int count = 0, ans = 1; 

            // One by one extract items 
            while(pq.isEmpty() == false && count < k) 
            { 
                ans = ans * pq.element(); 
                pq.remove(); 
                count++; 
            } 

            return ans; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int arr[] = {198, 76, 544, 123, 154, 675}; 
        int k = 2; 
        int n = arr.length; 
        System.out.print("Minimum product is " +  
                          minProduct(arr, n, k)); 
    } 
} 

// This code is contributed by sanjeev2552 

```

## Python3

```py

# Python3 program to find minimum 
# product of k elements in an array 
import math  
import heapq 

def minProduct(arr, n, k): 

    heapq.heapify(arr) 
    count = 0
    ans = 1

    # One by one extract  
    # items from min heap 
    while ( arr ) and count < k: 
        x = heapq.heappop(arr) 
        ans = ans * x 
        count = count + 1

    return ans; 

# Driver method 
arr = [198, 76, 544, 123, 154, 675] 
k = 2
n = len(arr) 
print ("Minimum product is", 
       minProduct(arr, n, k)) 

```

**输出**：

```
Minimum product is 9348

```

**时间复杂度**：`O(n * log n)`。

请注意，可以使用[这里](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)和[这里](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)讨论的方法在`O(n)`时间内解决上述问题。

