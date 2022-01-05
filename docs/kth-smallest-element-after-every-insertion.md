# 每次插入后的第 Kth 个最大元素

> 原文:[https://www . geesforgeks . org/kth-每次插入后最小元素/](https://www.geeksforgeeks.org/kth-smallest-element-after-every-insertion/)

给定一个无限长的整数流，在任意时间点找到第 k 个最大的元素。可以假设 1 <= k <= n. 

```
Input:
stream[] = {10, 20, 11, 70, 50, 40, 100, 5, ...}
k = 3
Output:    {_,   _, 10, 11, 20, 40, 50,  50, ...}
```

允许的额外空间为 0(k)。

想法是使用 min heap。
1)在最小堆中存储前 k 个元素。
2)对于第(k+1)到第 n 个元素，执行以下操作。
……a)打印堆的根。
……b)如果当前元素多于堆的根，弹出根并插入

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find k-th largest element in a
// stream after every insertion.
#include <bits/stdc++.h>
using namespace std;

int kthLargest(int stream[], int n, int k)
{
   // Create a min heap and store first k-1 elements
   // of stream into
   priority_queue<int, vector<int>, greater<int> > pq;

   // Push first k elements and print "_" (k-1) times
   for (int i=0; i<k-1; i++)
   {
      pq.push(stream[i]);
      cout << "_ ";
   }
   pq.push(stream[k-1]);

   for (int i=k; i<n; i++)
   {
       // We must insert last element before we
       // decide last k-th largest output.
          cout << pq.top() << " ";

       if (stream[i] > pq.top())
       {
           pq.pop();
           pq.push(stream[i]);
       } 
   } 

   // Print last k-th largest element (after
   // (inserting last element)
   cout << pq.top();
}

// Driver code
int main()
{
   int arr[] = {10, 20, 11, 70, 50, 40, 100, 55};
   int k = 3;
   int n = sizeof(arr)/sizeof(arr[0]);
   kthLargest(arr, n, k);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;
class GFG
{
  static void kthLargest(int stream[], int n, int k)
  {

    // Create a min heap and store first k-1 elements
    // of stream into
    Vector<Integer> pq = new Vector<Integer>(n);

    // Push first k elements and print "_" (k-1) times
    for (int i = 0; i < k - 1; i++)
    {
      pq.add(stream[i]);
      System.out.print("_ ");
    }
    pq.add(stream[k - 1]);

    for (int i = k; i < n; i++)
    {

      // We must insert last element before we
      // decide last k-th largest output.
      Collections.sort(pq);
      System.out.print(pq.get(0) + " ");     
      if (stream[i] > pq.get(0))
      {
        pq.remove(0);
        pq.add(stream[i]);
      }  
    }  

    // Print last k-th largest element (after
    // (inserting last element)
    Collections.sort(pq);
    System.out.print(pq.get(0));
  }

  // Driver code
  public static void main(String[] args) {
    int arr[] = {10, 20, 11, 70, 50, 40, 100, 55};
    int k = 3;
    int n = arr.length;
    kthLargest(arr, n, k);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python Program for the above approach
def kthLargest(stream, n, k):

    # Create a min heap and store first k-1 elements
    # of stream into
    pq = []

    # Push first k elements and print "_" (k-1) times
    for i in range(k - 1):
        pq.append(stream[i])
        print("_ ", end = "")
    pq.append(stream[k - 1])   
    for i in range(k, n):

        # We must insert last element before we
        # decide last k-th largest output.
        pq.sort()
        print(pq[0], end = " ")
        if(stream[i] > pq[0]):
            del pq[0]
            pq.append(stream[i])

    # Print last k-th largest element (after
    # (inserting last element)
    pq.sort()
    print(pq[0], end = "")

# Driver code
arr = [10, 20, 11, 70, 50, 40, 100, 55]
k = 3
n = len(arr)
kthLargest(arr, n, k)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find k-th largest element in a 
// stream after every insertion.
using System;
using System.Collections.Generic;
class GFG
{
  static void kthLargest(int[] stream, int n, int k)
  {

    // Create a min heap and store first k-1 elements
    // of stream into
    List<int> pq = new List<int>();

    // Push first k elements and print "_" (k-1) times
    for (int i = 0; i < k - 1; i++)
    {
      pq.Add(stream[i]);
      Console.Write("_ ");
    }
    pq.Add(stream[k - 1]);

    for (int i = k; i < n; i++)
    {

      // We must insert last element before we
      // decide last k-th largest output.
      pq.Sort();
      Console.Write(pq[0] + " ");     
      if (stream[i] > pq[0])
      {
        pq.RemoveAt(0);
        pq.Add(stream[i]);
      }  
    }  

    // Print last k-th largest element (after
    // (inserting last element)
    pq.Sort();
    Console.Write(pq[0]);
  }

  // Driver code
  static void Main()
  {
    int[] arr = {10, 20, 11, 70, 50, 40, 100, 55};
    int k = 3;
    int n = arr.Length;
    kthLargest(arr, n, k);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// JavaScript program to find k-th largest element in a
// stream after every insertion.

function kthLargest(stream, n, k) {

    // Create a min heap and store first k-1 elements
    // of stream into
    let pq = new Array();

    // Push first k elements and print "_" (k-1) times
    for (let i = 0; i < k - 1; i++) {
        pq.push(stream[i]);
        document.write("_ ");
    }
    pq.push(stream[k - 1]);

    for (let i = k; i < n; i++) {

        // We must insert last element before we
        // decide last k-th largest output.
        pq.sort((a, b) => a - b);
        document.write(pq[0] + " ");
        if (stream[i] > pq[0]) {
            pq.shift(0);
            pq.push(stream[i]);
        }
    }

    // Print last k-th largest element (after
    // (inserting last element)
    pq.sort((a, b) => a - b);
    document.write(pq[0]);
}

// Driver code

let arr = [10, 20, 11, 70, 50, 40, 100, 55];
let k = 3;
let n = arr.length;
kthLargest(arr, n, k);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
_ _ 10 11 20 40 50 55
```

如果流包含非原语类型的元素，我们可以[定义自己的压缩函数，并相应地创建一个 priority_queue](https://www.geeksforgeeks.org/stl-priority-queue-for-structure-or-class/) 。