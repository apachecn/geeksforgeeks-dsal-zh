# 移除`K`个元素后的最大不同元素

> 原文：[https://www.geeksforgeeks.org/maximum-distinct-elements-removing-k-elements/](https://www.geeksforgeeks.org/maximum-distinct-elements-removing-k-elements/)

给定包含`n`个元素的数组`arr[]`。 问题是从数组中删除`K`个元素后，找到最大数量的非重复元素（非重复）。

**注意**：`1 < = k < = n`。

**示例**：

```
Input : arr[] = {5, 7, 5, 5, 1, 2, 2}, k = 3
Output : 4
Remove 2 occurrences of element 5 and
1 occurrence of element 2.

Input : arr[] = {1, 2, 3, 4, 5, 6, 7}, k = 5
Output : 2

Input : arr[] = {1, 2, 2, 2}, k = 1
Output : 1

```

**方法**：以下是步骤：

1.  建立频率图

2.  将所有`freq = 1`的数字相加得到结果，并将其他推入最小堆。

3.  当`K > 0`时，如果将`freq == 1`添加到结果中，则选择顶部以减少 1。

4.  否则，减少`k`并将顶部的那个推入最小堆。

## C++

```cpp

// CPP implementation of the above approach
#include <bits/stdc++.h> 
using namespace std; 

// function to find maximum distinct elements 
// after removing k elements 
int maxDistinctNum(int arr[], int n, int k) 
{
    unordered_map<int, int> numToFreq;

    // Build frequency map
    for(int i = 0 ; i < n ; i++)
        ++numToFreq[ arr[i] ];

    int result=0;

    // Min-heap
    priority_queue<int, 
               vector<int>, greater<int> > minHeap;

    // Add all number with freq=1 to 
    // result and push others to minHeap
    for( auto p : numToFreq ) 
    {
        if( p.second == 1 ) // already distinct
            ++result;
        else
           minHeap.push( p.second );
    }

    // Perform k operations
    while( k && !minHeap.empty() ) 
    {

        // Pop the top() element
        auto t = minHeap.top(); 
        minHeap.pop();

          // Increment Result
        if( t == 1 )
        {
          ++result;
        }

        // Reduce t and k 
        // Push it again
        else
        {
            --t;
            --k;
            minHeap.push( t );
        }
    }

    // Return result
    return result;
}

// Driver Code
int main() 
{ 
    int arr[] = { 5, 7, 5, 5, 1, 2, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 

    // Function Call
    cout << "Maximum distinct elements = "
         << maxDistinctNum(arr, n, k); 
    return 0; 
} 

// This code is contributed by Sonu Giri

```

## Java

```java

// Java implementation of the 
// above approach
import java.util.*;
class GFG{

// Function to find maximum 
// distinct elements after 
// removing k elements 
static int maxDistinctNum(int arr[], 
                          int n, int k) 
{
  HashMap<Integer, 
          Integer> numToFreq = new HashMap<>(); 

  // Build frequency map
  for(int i = 0 ; i < n ; i++)
  {
    numToFreq.put(arr[i],
    numToFreq.getOrDefault(arr[i], 0) + 1);
  }

  int result = 0;

  // Min-heap
  PriorityQueue<Integer> minHeap = 
                new PriorityQueue<Integer>();

  // Add all number with freq=1 to 
  // result and push others to minHeap
  for(Map.Entry<Integer, 
                Integer> p : numToFreq.entrySet()) 
  {
    if(p.getValue() == 1) 
      ++result;
    else
      minHeap.add(p.getValue());
  }

  // Perform k operations
  while(k != 0 && !minHeap.isEmpty()) 
  {
    // Pop the top() element
    Integer t = minHeap.poll(); 

    // Increment Result
    if(t == 1)
    {
      ++result;
    }

    // Reduce t and k 
    // Push it again
    else
    {
      --t;
      --k;
      minHeap.add(t);
    }
  }

  // Return result
  return result;
}

// Driver code
public static void main(String[] args) 
{        
  int arr[] = {5, 7, 5, 5, 1, 2, 2}; 
  int n = arr.length; 
  int k = 3; 

  // Function Call
  System.out.println("Maximum distinct elements = " +  
                      maxDistinctNum(arr, n, k));
}
}

// This code is contributed by rutvik_56

```

**输出**：

```
Maximum distinct elements = 4

```

**时间复杂度**：`O(k * logd)`，其中`d`是给定数组中不同元素的数量。



* * *

* * *



