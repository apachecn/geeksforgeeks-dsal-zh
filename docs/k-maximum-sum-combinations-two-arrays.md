# 来自两个数组的`K`个最大和组合

> 原文： [https://www.geeksforgeeks.org/k-maximum-sum-combinations-two-arrays/](https://www.geeksforgeeks.org/k-maximum-sum-combinations-two-arrays/)

给定两个大小相等的数组（`A`，`B`）和`N`（两个数组的大小）。

通过将数组`A`中的一个元素与数组`B`中的另一个元素相加来构成**和组合**。从所有可能的和组合中显示**最大`K`个有效和组合**。

例子：

```
Input :  A[] : {3, 2} 
         B[] : {1, 4}
         K : 2 [Number of maximum sum
               combinations to be printed]
Output : 7    // (A : 3) + (B : 4)
         6    // (A : 2) + (B : 4)

Input :  A[] : {4, 2, 5, 1}
         B[] : {8, 0, 3, 5}
         K : 3
Output : 13   // (A : 5) + (B : 8)
         12   // (A : 4) + (B :  8)
         10   // (A : 2) + (B : 8)  

```



**方法 1（朴素算法）**：

我们可以通过将数组`A`中的一个元素和数组`B`中的另一个元素插入到最大堆中来进行所有可能的组合使用暴力。 在最大堆中，最大元素位于根节点，因此，每当我们从最大堆弹出时，我们都会获得堆中存在的最大元素。 插入所有总和组合后，我们从最大堆中取出`K`个元素并显示出来。

下面是上述方法的实现。

## C++ 

```cpp

// A simple C++ program to find N maximum 
// combinations from two arrays, 
#include <bits/stdc++.h> 
using namespace std; 

// function to display first N maximum sum 
// combinations 
void KMaxCombinations(int A[], int B[], int N, 
                                        int K) 
{ 
    // max heap. 
    priority_queue<int> pq; 

    // insert all the possible combinations  
    // in max heap. 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            pq.push(A[i] + B[j]); 

    // pop first N elements from max heap 
    // and display them. 
    int count = 0; 
    while (count < K) { 
        cout << pq.top() << endl; 
        pq.pop(); 
        count++; 
    } 
} 

// Driver Code. 
int main() 
{ 
    int A[] = { 4, 2, 5, 1 }; 
    int B[] = { 8, 0, 5, 3 }; 
    int N = sizeof(A)/sizeof(A[0]); 
    int K = 3; 
    KMaxCombinations(A, B, N, K); 
    return 0; 
} 

```

## Java

```java
// Java program to find K
// maximum combinations 
// from two arrays,
import java.io.*;
import java.util.*;
 
class GFG 
{
     
    // function to display first K 
    // maximum sum combinations
    static void KMaxCombinations(int A[], int B[], int N,
                                                   int K)
    {
        // max heap.
        PriorityQueue<Integer> pq =
                            new PriorityQueue<
            Integer>(Collections.reverseOrder());
     
        // Insert all the possible 
        // combinations in max heap.
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                pq.add(A[i] + B[j]);
     
        // Pop first N elements 
        // from max heap and 
        // display them.
        int count = 0;
         
        while (count < K)
        {
            System.out.println(pq.peek());
            pq.remove();
            count++;
        }
    }
     
    // Driver Code
    public static void main (String[] args) 
    {
        int A[] = { 4, 2, 5, 1 };
        int B[] = { 8, 0, 5, 3 };
        int N = A.length;
        int K = 3;
         
        // Function Call
        NMaxCombinations(A, B, N, K);       
    }
}
 
// This code is contributed by Gitanjali.
```

## Python 3

```py
# Python program to find 
# K maximum combinations 
# from two arrays
import math 
from queue import PriorityQueue
 
# Function to display first K 
# maximum sum combinations
def KMaxCombinations( A, B, N, K):
     
    # Max heap.
    pq = PriorityQueue() 
     
    # Insert all the possible  
    # combinations in max heap.
    for i in range(0, N):
        for j in range(0, N):
           a = A[i] + B[j] 
           pq.put((-a, a))
             
    # Pop first N elements from 
    # max heap and display them.
    count = 0
    while (count < K):
        print(pq.get()[1])
        count = count + 1
         
# Driver method
A = [ 4, 2, 5, 1 ]
B = [ 8, 0, 5, 3 ]
N = len(A)
K = 3
KMaxCombinations(A, B, N, K)
 
# This code is contributed 
# by Gitanjali.
```

输出：

```
13
12
10
```

时间复杂度：`O(N ^ 2)`

方法 2（排序，最大堆，映射）：

代替对所有可能的和组合进行强行强制，我们应该找到一种方法将搜索空间限制为可能的候选和组合。

1.  对数组`A`和数组`B`进行排序。
2.  在 C++ 中创建一个最大堆，即·，以存储总和组合以及组成总和的数组`A`和`B`中元素的索引。堆按总和排序。
3.  以最大可能的总和组合（即`[A[N – 1] + B[N – 1]`，其中`N`是数组的大小）和两个数组中元素的索引`(N – 1, N – 1)`。最大堆中的元组将为`（A[N - 1] + B[N – 1], N – 1, N – 1)`。堆按第一个值（即两个元素的总和）排序。
4.  弹出堆以获取当前的最大和以及组成该和的元素的索引。让元组为`(sum, i, j)`。
    +   接下来将`(A[i – 1] + B[j], i – 1, j)`和`(A[i] + B[j – 1], i, j – 1)`插入最大堆，但请确保一对索引（即`(i – 1, j)`和`(i，j – 1)`）在最大堆中不存在。要检查这一点，我们可以使用 C++ 中的集合。
    +   执行 4 `K`次。

下面是上述方法的实现：

## CPP

```cpp
// An efficient C++ program to find top K elements
// from two arrays.
#include <bits/stdc++.h>
using namespace std;
 
// Function prints k maximum possible combinations
void KMaxCombinations(vector<int>& A, 
                      vector<int>& B, int K)
{
    // sort both arrays A and B
    sort(A.begin(), A.end());
    sort(B.begin(), B.end());
 
    int N = A.size();
 
    // Max heap which contains tuple of the format
    // (sum, (i, j)) i and j are the indices 
    // of the elements from array A
    // and array B which make up the sum.
    priority_queue<pair<int, pair<int, int> > > pq;
 
    // my_set is used to store the indices of 
    // the  pair(i, j) we use my_set to make sure
    // the indices doe not repeat inside max heap.
    set<pair<int, int> > my_set;
 
    // initialize the heap with the maximum sum
    // combination ie (A[N - 1] + B[N - 1])
    // and also push indices (N - 1, N - 1) along 
    // with sum.
    pq.push(make_pair(A[N - 1] + B[N - 1],
                      make_pair(N-1, N-1)));
 
    my_set.insert(make_pair(N - 1, N - 1));
 
    // iterate upto K
    for (int count=0; count<K; count++) {
 
        // tuple format (sum, (i, j)).
        pair<int, pair<int, int> > temp = pq.top();
        pq.pop();
 
        cout << temp.first << endl;
 
        int i = temp.second.first;
        int j = temp.second.second;
 
        int sum = A[i - 1] + B[j];
 
        // insert (A[i - 1] + B[j], (i - 1, j)) 
        // into max heap.
        pair<int, int> temp1 = make_pair(i - 1, j);
 
        // insert only if the pair (i - 1, j) is 
        // not already present inside the map i.e.
        // no repeating pair should be present inside 
        // the heap.
        if (my_set.find(temp1) == my_set.end()) {
            pq.push(make_pair(sum, temp1));
            my_set.insert(temp1);
        }
 
        // insert (A[i] + B[j - 1], (i, j - 1)) 
        // into max heap.
        sum = A[i] + B[j - 1];
        temp1 = make_pair(i, j - 1);
 
        // insert only if the pair (i, j - 1)
        // is not present inside the heap.
        if (my_set.find(temp1) == my_set.end()) {
            pq.push(make_pair(sum, temp1));
            my_set.insert(temp1);
        }
    }
}
 
// Driver Code.
int main()
{
    vector<int> A = { 1, 4, 2, 3 };
    vector<int> B = { 2, 5, 1, 6 };
    int K = 4;
    KMaxCombinations(A, B, K);
    return 0;
}
```

输出：

```
10
9
9
8
```

时间复杂度：假设`K <= N`，则`O(N log N)`。