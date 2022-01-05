# 使用优先级队列的未排序数组中的第 K 个最小元素

> 原文:[https://www . geesforgeks . org/k-th-未排序数组中的最小元素-使用优先级-队列/](https://www.geeksforgeeks.org/k-th-smallest-element-in-an-unsorted-array-using-priority-queue/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)找到数组中的 **K <sup>第</sup>** 个最小元素。

**示例:**

> **输入:** arr[] = {5，20，10，7，1}，N = 5，K = 2
> **输出:** 5
> **说明:**在给定数组中，2 <sup>nd</sup> 最小元素为 5。因此，所需的输出为 5。
> 
> **输入:** arr[] = {5，20，10，7，1}，N = 5，K = 5
> **输出:** 20
> **说明:**在给定数组中，第 5 <sup>个</sup>最小元素为 20。因此，所需的输出为 20。

**方法:**思路是使用 Java 中的[priority queue Collection](https://www.geeksforgeeks.org/priority-queue-class-in-java-2/)或 [priority_queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) STL 库实现 **Max_Heap** 找到 **K <sup>th</sup>** 最小数组元素。按照以下步骤解决问题:

1.  使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)实现**最大堆**。
2.  [先将 **K** 阵元推入**优先级 _ 队列**](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) 。
3.  从那时起，每次插入数组元素后，将该元素放在优先级队列的[顶部。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
4.  完成数组的[遍历后，将优先队列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)顶部的[元素打印为所需答案。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find kth smallest array element
void kthSmallest(vector<int>& v, int N, int K)
{
    // Implement Max Heap using
    // a Priority Queue
    priority_queue<int> heap1;

    for (int i = 0; i < N; ++i) {

        // Insert elements into
        // the priority queue
        heap1.push(v[i]);

        // If size of the priority
        // queue exceeds k
        if (heap1.size() > K) {
            heap1.pop();
        }
    }

    // Print the k-th smallest element
    cout << heap1.top() << endl;
}

// Driver code
int main()
{
    // Given array
    vector<int> vec = { 5, 20, 10, 7, 1 };

    // Size of array
    int N = vec.size();

    // Given K
    int K = 2;

    // Function Call
    kthSmallest(vec, N, K % N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class CustomComparator implements Comparator<Integer> {

    @Override
    public int compare(Integer number1, Integer number2) {
        int value =  number1.compareTo(number2);

        // elements are sorted in reverse order
        if (value > 0) {
            return -1;
        }
        else if (value < 0) {
            return 1;
        }
        else {
            return 0;
        }
    }
}
class GFG{

// Function to find kth smallest array element
static void kthSmallest(int []v, int N, int K)
{
    // Implement Max Heap using
    // a Priority Queue
    PriorityQueue<Integer> heap1 = new PriorityQueue<Integer>(new CustomComparator());

    for (int i = 0; i < N; ++i) {

        // Insert elements into
        // the priority queue
        heap1.add(v[i]);

        // If size of the priority
        // queue exceeds k
        if (heap1.size() > K) {
            heap1.remove();
        }
    }

    // Print the k-th smallest element
    System.out.print(heap1.peek() +"\n");
}

// Driver code
public static void main(String[] args)
{
    // Given array
    int []vec = { 5, 20, 10, 7, 1 };

    // Size of array
    int N = vec.length;

    // Given K
    int K = 2;

    // Function Call
    kthSmallest(vec, N, K % N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find kth smallest array element
def kthSmallest(v, N, K):

    # Implement Max Heap using
    # a Priority Queue
    heap1 = []

    for i in range(N):

        # Insert elements into
        # the priority queue
        heap1.append(v[i])

        # If size of the priority
        # queue exceeds k
        if (len(heap1) > K):
            heap1.sort()
            heap1.reverse()
            del heap1[0]

    # Print the k-th smallest element
    heap1.sort()
    heap1.reverse()
    print(heap1[0])

# Driver code

# Given array
vec = [ 5, 20, 10, 7, 1 ]

# Size of array
N = len(vec)

# Given K
K = 2

# Function Call
kthSmallest(vec, N, K % N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to find kth smallest array element
static void kthSmallest(int []v, int N, int K)
{

    // Implement Max Heap using
    // a Priority Queue
    List<int> heap1 = new List<int>();
    for (int i = 0; i < N; ++i) {

        // Insert elements into
        // the priority queue
        heap1.Add(v[i]);

        // If size of the priority
        // queue exceeds k
        if (heap1.Count > K) {
            heap1.Sort();
            heap1.Reverse();
            heap1.RemoveAt(0);
        }
    }
    heap1.Sort();
            heap1.Reverse();

    // Print the k-th smallest element
    Console.WriteLine(heap1[0]);
}

// Driver code
public static void Main(String[] args)
{

    // Given array
    int []vec = { 5, 20, 10, 7, 1 };

    // Size of array
    int N = vec.Length;

    // Given K
    int K = 2;

    // Function Call
    kthSmallest(vec, N, K % N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find kth smallest array element
function kthSmallest(v,N,K)
{
    let heap1 = [];
     for (let i = 0; i < N; ++i) {

        // Insert elements into
        // the priority queue
        heap1.push(v[i]);

        // If size of the priority
        // queue exceeds k
        if (heap1.length > K)
        {
            heap1.sort(function(a,b){
                return a-b;
            });
            heap1.reverse();
            heap1.shift();
        }
    }
    heap1.sort(function(a,b){
                return a-b;
            });
            heap1.reverse();
    // Print the k-th smallest element
    document.write(heap1[0] +"<br>");
}

// Driver code
// Given array
let vec=[5, 20, 10, 7, 1 ];
// Size of array
let N = vec.length;

// Given K
let K = 2;

// Function Call
kthSmallest(vec, N, K % N);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N LogK)*
***辅助空间:** O(K)，因为优先级队列 ay 任何时候都保持在最大 K 个元素。*