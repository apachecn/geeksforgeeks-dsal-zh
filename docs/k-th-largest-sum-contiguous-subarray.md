# 连续子数组的第`K`个最大和

> 原文： [https://www.geeksforgeeks.org/k-th-largest-sum-contiguous-subarray/](https://www.geeksforgeeks.org/k-th-largest-sum-contiguous-subarray/)

给定一个整数数组。 编写程序以在具有负数和正数的数字数组中找到连续的子数组的第`K`个最大和。

**示例**：

```

Input: a[] = {20, -5, -1} 
         k = 3
Output: 14
Explanation: All sum of contiguous 
subarrays are (20, 15, 14, -5, -6, -1) 
so the 3rd largest sum is 14.

Input: a[] = {10, -10, 20, -40} 
         k = 6
Output: -10 
Explanation: The 6th largest sum among 
sum of all contiguous subarrays is -10.

```



**暴力方法**方法是将所有连续的和存储在另一个数组中并对其进行排序，然后打印出第`k`个最大的和。 但是在元素数量很大的情况下，我们存储连续和的数组将耗尽内存，因为连续子数组的数量将很大（二次顺序）

一种有效的**方法**将数组的前和存储在`sum[]`数组中。 我们可以找到从索引`i`到`j`的连续子数组的和为`sum[j] - sum[i-1]`。

现在要存储第`K`个最大和，请使用最小堆（优先级队列），在其中将连续和推入直到获得`K`个元素，一旦有了`K`个元素，请检查该元素是否大于第`K`个元素，插入最小堆并弹出最小堆中的顶部元素，否则不插入。 最后，最小堆中的最高元素将是您的答案。

下面是上述方法的实现。

## C++ 

```cpp

// CPP program to find the k-th largest sum 
// of subarray 
#include <bits/stdc++.h> 
using namespace std; 

// function to calculate kth largest element 
// in contiguous subarray sum 
int kthLargestSum(int arr[], int n, int k) 
{ 
    // array to store predix sums 
    int sum[n + 1]; 
    sum[0] = 0; 
    sum[1] = arr[0]; 
    for (int i = 2; i <= n; i++) 
        sum[i] = sum[i - 1] + arr[i - 1]; 

    // priority_queue of min heap 
    priority_queue<int, vector<int>, greater<int> > Q; 

    // loop to calculate the contigous subarray 
    // sum position-wise 
    for (int i = 1; i <= n; i++) 
    { 

        // loop to traverse all positions that 
        // form contiguous subarray 
        for (int j = i; j <= n; j++) 
        { 
            // calculates the contiguous subarray 
            // sum from j to i index 
            int x = sum[j] - sum[i - 1]; 

            // if queue has less then k elements, 
            // then simply push it 
            if (Q.size() < k) 
                Q.push(x); 

            else
            { 
                // it the min heap has equal to 
                // k elements then just check 
                // if the largest kth element is 
                // smaller than x then insert 
                // else its of no use 
                if (Q.top() < x) 
                { 
                    Q.pop(); 
                    Q.push(x); 
                } 
            } 
        } 
    } 

    // the top element will be then kth 
    // largest element 
    return Q.top(); 
} 

// Driver program to test above function 
int main() 
{ 
    int a[] = { 10, -10, 20, -40 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int k = 6; 

    // calls the function to find out the 
    // k-th largest sum 
    cout << kthLargestSum(a, n, k); 
    return 0; 
} 

```

## Java

```java
// Java program to find the k-th  
// argest sum of subarray 
import java.util.*; 
  
class KthLargestSumSubArray 
{ 
    // function to calculate kth largest  
    // element in contiguous subarray sum 
    static int kthLargestSum(int arr[], int n, int k) 
    { 
        // array to store predix sums 
        int sum[] = new int[n + 1]; 
        sum[0] = 0; 
        sum[1] = arr[0]; 
        for (int i = 2; i <= n; i++) 
            sum[i] = sum[i - 1] + arr[i - 1]; 
          
        // priority_queue of min heap 
        PriorityQueue<Integer> Q = new PriorityQueue<Integer> (); 
          
        // loop to calculate the contigous subarray 
        // sum position-wise 
        for (int i = 1; i <= n; i++) 
        { 
      
            // loop to traverse all positions that 
            // form contiguous subarray 
            for (int j = i; j <= n; j++) 
            { 
                // calculates the contiguous subarray 
                // sum from j to i index 
                int x = sum[j] - sum[i - 1]; 
      
                // if queue has less then k elements, 
                // then simply push it 
                if (Q.size() < k) 
                    Q.add(x); 
      
                else
                { 
                    // it the min heap has equal to 
                    // k elements then just check 
                    // if the largest kth element is 
                    // smaller than x then insert 
                    // else its of no use 
                    if (Q.peek() < x) 
                    { 
                        Q.poll(); 
                        Q.add(x); 
                    } 
                } 
            } 
        } 
          
        // the top element will be then kth 
        // largest element 
        return Q.poll(); 
    } 
      
    // Driver Code 
    public static void main(String[] args)  
    { 
        int a[] = new int[]{ 10, -10, 20, -40 }; 
        int n = a.length; 
        int k = 6; 
  
        // calls the function to find out the 
        // k-th largest sum 
        System.out.println(kthLargestSum(a, n, k));  
    } 
} 
  
/* This code is contributed by Danish Kaleem */
```

## Python

```py
# Python program to find the k-th largest sum  
# of subarray  
import heapq 
  
# function to calculate kth largest element  
# in contiguous subarray sum  
def kthLargestSum(arr, n, k): 
      
    # array to store predix sums  
    sum = [] 
    sum.append(0) 
    sum.append(arr[0]) 
    for i in range(2, n + 1): 
        sum.append(sum[i - 1] + arr[i - 1]) 
          
    # priority_queue of min heap  
    Q = [] 
    heapq.heapify(Q) 
      
    # loop to calculate the contigous subarray  
    # sum position-wise  
    for i in range(1, n + 1): 
          
        # loop to traverse all positions that  
        # form contiguous subarray  
        for j in range(i, n + 1): 
            x = sum[j] - sum[i - 1] 
              
            # if queue has less then k elements,  
            # then simply push it  
            if len(Q) < k: 
                heapq.heappush(Q, x) 
            else: 
                # it the min heap has equal to  
                # k elements then just check  
                # if the largest kth element is  
                # smaller than x then insert  
                # else its of no use  
                if Q[0] < x: 
                    heapq.heappop(Q) 
                    heapq.heappush(Q, x)  
      
    # the top element will be then kth  
    # largest element  
    return Q[0] 
  
# Driver program to test above function  
a = [10,-10,20,-40] 
n = len(a) 
k = 6
  
# calls the function to find out the  
# k-th largest sum  
print(kthLargestSum(a,n,k)) 
  
  
# This code is contributed by Kumar Suman  
```

输出：

```
-10
```

时间复杂度：`O(n ^ 2 log(k))`。

辅助空间：`O(k)`用于最小堆，我们可以将`sum`数组存储在数组本身中，因为它没有用。