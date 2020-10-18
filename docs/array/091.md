# 在两个数组中找到具有最小和的`k`对

> 原文： [https://www.geeksforgeeks.org/find-k-pairs-smallest-sums-two-arrays/](https://www.geeksforgeeks.org/find-k-pairs-smallest-sums-two-arrays/)

给定两个按升序排列的整数数组`arr1[]`和`arr2[]`和一个整数`k`。 查找具有最小和的`k`对，以使对中的一个元素属于`arr1[]`，而另一个元素属于`arr2[]`。

例子：

```
Input :  arr1[] = {1, 7, 11}
         arr2[] = {2, 4, 6}
         k = 3
Output : [1, 2],
         [1, 4],
         [1, 6]
Explanation: The first 3 pairs are returned 
from the sequence [1, 2], [1, 4], [1, 6], 
[7, 2], [7, 4], [11, 2], [7, 6], [11, 4], 
[11, 6]

```



**方法 1（简单）**：

1.  查找所有对并存储其总和。 此步骤的时间复杂度为`O(n1 * n2)`，其中`n1`和`n2`是输入数组的大小。

2.  然后根据总和对。 此步骤的时间复杂度为`O(n1 * n2 * log(n1 * n2))`。

总时间复杂度：`O(n1 * n2 * log(n1 * n2))`。

**方法 2（有效）**：

我们从最小和对开始一个接一个地找到`k`个最小和对。 这个想法是跟踪已经为每个元素`arr1[i1]`考虑过的`arr2[]`的所有元素，因此在迭代中我们仅考虑下一个元素。 为此，我们使用索引数组`index2[]`来跟踪另一个数组中下一个元素的索引。 它仅表示在每次迭代中将第二个数组的哪个元素与第一个数组的元素相加。 我们在索引数组中为形成下一个最小值对的元素增加值。

## C++ 

```cpp

// C++ program to prints first k pairs with least sum from two 
// arrays. 
#include<bits/stdc++.h> 

using namespace std; 

// Function to find k pairs with least sum such 
// that one elemennt of a pair is from arr1[] and 
// other element is from arr2[] 
void kSmallestPair(int arr1[], int n1, int arr2[], 
                                   int n2, int k) 
{ 
    if (k > n1*n2) 
    { 
        cout << "k pairs don't exist"; 
        return ; 
    } 

    // Stores current index in arr2[] for 
    // every element of arr1[]. Initially 
    // all values are considered 0\. 
    // Here current index is the index before 
    // which all elements are considered as 
    // part of output. 
    int index2[n1]; 
    memset(index2, 0, sizeof(index2)); 

    while (k > 0) 
    { 
        // Initialize current pair sum as infinite 
        int min_sum = INT_MAX; 
        int min_index = 0; 

        // To pick next pair, traverse for all elements 
        // of arr1[], for every element, find corresponding 
        // current element in arr2[] and pick minimum of 
        // all formed pairs. 
        for (int i1 = 0; i1 < n1; i1++) 
        { 
            // Check if current element of arr1[] plus 
            // element of array2 to be used gives minimum 
            // sum 
            if (index2[i1] < n2 && 
                arr1[i1] + arr2[index2[i1]] < min_sum) 
            { 
                // Update index that gives minimum 
                min_index = i1; 

                // update minimum sum 
                min_sum = arr1[i1] + arr2[index2[i1]]; 
            } 
        } 

        cout << "(" << arr1[min_index] << ", "
             << arr2[index2[min_index]] << ") "; 

        index2[min_index]++; 

        k--; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr1[] = {1, 3, 11}; 
    int n1 = sizeof(arr1) / sizeof(arr1[0]); 

    int arr2[] = {2, 4, 8}; 
    int n2 = sizeof(arr2) / sizeof(arr2[0]); 

    int k = 4; 
    kSmallestPair( arr1, n1, arr2, n2, k); 

    return 0; 
} 

```

## Java

```java
// Java code to print first k pairs with least 
// sum from two arrays. 
import java.io.*; 
   
class KSmallestPair 
{ 
    // Function to find k pairs with least sum such 
    // that one elemennt of a pair is from arr1[] and 
    // other element is from arr2[] 
    static void kSmallestPair(int arr1[], int n1, int arr2[], 
                                            int n2, int k) 
    { 
        if (k > n1*n2) 
        { 
            System.out.print("k pairs don't exist"); 
            return ; 
        } 
       
        // Stores current index in arr2[] for 
        // every element of arr1[]. Initially 
        // all values are considered 0. 
        // Here current index is the index before 
        // which all elements are considered as 
        // part of output. 
        int index2[] = new int[n1]; 
       
        while (k > 0) 
        { 
            // Initialize current pair sum as infinite 
            int min_sum = Integer.MAX_VALUE; 
            int min_index = 0; 
       
            // To pick next pair, traverse for all  
            // elements of arr1[], for every element, find  
            // corresponding current element in arr2[] and 
            // pick minimum of all formed pairs. 
            for (int i1 = 0; i1 < n1; i1++) 
            { 
                // Check if current element of arr1[] plus 
                // element of array2 to be used gives  
                // minimum sum 
                if (index2[i1] < n2 &&  
                    arr1[i1] + arr2[index2[i1]] < min_sum) 
                { 
                    // Update index that gives minimum 
                    min_index = i1; 
       
                    // update minimum sum 
                    min_sum = arr1[i1] + arr2[index2[i1]]; 
                } 
            } 
       
            System.out.print("(" + arr1[min_index] + ", " + 
                            arr2[index2[min_index]]+ ") "); 
       
            index2[min_index]++; 
            k--; 
        } 
    } 
  
    // Driver code 
    public static void main (String[] args) 
    { 
        int arr1[] = {1, 3, 11}; 
        int n1 = arr1.length; 
       
        int arr2[] = {2, 4, 8}; 
        int n2 = arr2.length; 
       
        int k = 4; 
        kSmallestPair( arr1, n1, arr2, n2, k); 
    } 
} 
/*This code is contributed by Prakriti Gupta*/
```

## Python3

```py
# Python3 program to prints first k pairs with least sum from two 
# arrays. 
  
import sys 
# Function to find k pairs with least sum such 
# that one elemennt of a pair is from arr1[] and 
# other element is from arr2[] 
def kSmallestPair(arr1, n1, arr2, n2, k): 
    if (k > n1*n2): 
        print("k pairs don't exist") 
        return
  
    # Stores current index in arr2[] for 
    # every element of arr1[]. Initially 
    # all values are considered 0. 
    # Here current index is the index before 
    # which all elements are considered as 
    # part of output. 
    index2 = [0 for i in range(n1)] 
  
    while (k > 0): 
        # Initialize current pair sum as infinite 
        min_sum = sys.maxsize 
        min_index = 0
  
        # To pick next pair, traverse for all elements 
        # of arr1[], for every element, find corresponding 
        # current element in arr2[] and pick minimum of 
        # all formed pairs. 
        for i1 in range(0,n1,1): 
            # Check if current element of arr1[] plus 
            # element of array2 to be used gives minimum 
            # sum 
            if (index2[i1] < n2 and arr1[i1] + arr2[index2[i1]] < min_sum): 
                # Update index that gives minimum 
                min_index = i1 
  
                # update minimum sum 
                min_sum = arr1[i1] + arr2[index2[i1]] 
          
        print("(",arr1[min_index],",",arr2[index2[min_index]],")",end = " ") 
  
        index2[min_index] += 1
  
        k -= 1
  
# Driver code 
if __name__ == '__main__': 
    arr1 = [1, 3, 11] 
    n1 = len(arr1) 
  
    arr2 = [2, 4, 8] 
    n2 = len(arr2) 
  
    k = 4
    kSmallestPair( arr1, n1, arr2, n2, k) 
  
# This code is contributed by 
# Shashank_Sharma 
```

## C#

```cs
// C# code to print first k pairs with  
// least with least sum from two arrays. 
using System; 
  
class KSmallestPair 
{ 
    // Function to find k pairs with least  
    // sum such that one elemennt of a pair  
    // is from arr1[] and other element is 
    // from arr2[] 
    static void kSmallestPair(int []arr1, int n1,  
                        int []arr2, int n2, int k) 
    { 
        if (k > n1 * n2) 
        { 
            Console.Write("k pairs don't exist"); 
            return; 
        } 
      
        // Stores current index in arr2[] for 
        // every element of arr1[]. Initially 
        // all values are considered 0. Here 
        // current index is the index before 
        // which all elements are considered  
        // as part of output. 
        int []index2 = new int[n1]; 
      
        while (k > 0) 
        { 
            // Initialize current pair sum as infinite 
            int min_sum = int.MaxValue; 
            int min_index = 0; 
      
            // To pick next pair, traverse for all  
            // elements of arr1[], for every element,   
            // find corresponding current element in  
            // arr2[] and pick minimum of all formed pairs. 
            for (int i1 = 0; i1 < n1; i1++) 
            { 
                // Check if current element of arr1[]  
                // plus element of array2 to be used   
                // gives minimum sum 
                if (index2[i1] < n2 && arr1[i1] +  
                    arr2[index2[i1]] < min_sum) 
                { 
                    // Update index that gives minimum 
                    min_index = i1; 
      
                    // update minimum sum 
                    min_sum = arr1[i1] + arr2[index2[i1]]; 
                } 
            } 
      
        Console.Write("(" + arr1[min_index] + ", " + 
                        arr2[index2[min_index]] + ") "); 
      
            index2[min_index]++; 
            k--; 
        } 
    } 
  
    // Driver code 
    public static void Main (String[] args) 
    { 
        int []arr1 = {1, 3, 11}; 
        int n1 = arr1.Length; 
      
        int []arr2 = {2, 4, 8}; 
        int n2 = arr2.Length; 
      
        int k = 4; 
        kSmallestPair( arr1, n1, arr2, n2, k); 
    } 
} 
  
// This code is contributed by Parashar. 
```

输出：

```
(1, 2) (1, 4) (3, 2) (3, 4)
```

时间复杂度：`O(k*n1)`。

方法 3 - 使用排序，最小堆，映射：

代替对所有可能的和组合进行强行强制，我们应该找到一种方法将搜索空间限制为可能的候选和组合。

1.  对数组`A`和数组`B`进行排序。
2.  在 C++ 中创建一个最小堆，即`priority_queue`，以存储总和组合以及组成总和的数组A和B中元素的索引。堆按总和排序。
3.  用可能的最小总和组合（即`A[0] + B[0]`）和两个数组中元素的索引`(0, 0)`初始化堆。最小堆中的元组将为`（A[0] + B[0], 0, 0）`。堆按第一个值（即两个元素的总和）排序。
4.  弹出堆以获取当前的最小和，以及组成该和的元素的索引。让元组为`(sum, i, j)`。
    +   接下来，将`(A[i + 1] + A[j], i + 1, j）`和`(A[i] + A[j + 1], i, j + 1)`插入最小堆，但请确保最小堆中不存在一对索引，即`(i + 1, j)`和`(i, j + 1)`。要检查这一点，我们可以使用 C++ 中的集合。
    +   返回 4 直到`K`次。

## C++

```cpp
// C++ program to Prints first k pairs with  
// least sum from two arrays. 
  
#include<bits/stdc++.h> 
  
using namespace std; 
// Function to find k pairs with least sum such 
// that one elemennt of a pair is from arr1[] and 
// other element is from arr2[] 
vector<int> kSmallestPair(vector<int> A, vector<int> B, int K) 
{ 
    sort(A.begin(), A.end()); 
    sort(B.begin(), B.end()); 
   
    int N = A.size(); 
 // Min heap which contains tuple of the format 
    // (sum, (i, j)) i and j are the indices  
    // of the elements from array A 
    // and array B which make up the sum. 
  
    priority_queue< pair<int, pair<int, int> >,vector< pair<int, pair<int, int> > >,greater< pair<int, pair<int, int> > > > pq; 
   
// my_set is used to store the indices of  
    // the  pair(i, j) we use my_set to make sure 
    // the indices doe not repeat inside min heap. 
      
    set<pair<int, int> > my_set; 
  
// initialize the heap with the minimum sum 
    // combination i.e. (A[0] + B[0]) 
    // and also push indices (0,0) along  
    // with sum. 
  
    pq.push(make_pair(A[0] + B[0], make_pair(0,0))); 
   
    my_set.insert(make_pair(0,0)); 
   
    // iterate upto K 
  
    for (int count=0; count<K; count++){     
  
        // tuple format (sum, i, j). 
        pair<int, pair<int, int> > temp = pq.top(); 
        pq.pop(); 
   
        int i = temp.second.first; 
        int j = temp.second.second; 
           
        cout<<"("<<A[i]<<", "<<B[j]<<")"<<endl;         //Extracting pair with least sum such that one element 
                                              //is from arr1 and another is from arr2 
   
        int sum = A[i+1] + B[j]; 
        // insert (A[i + 1] + B[j], (i + 1, j))  
        // into min heap.   
        pair<int, int> temp1 = make_pair(i+1, j); 
          
        // insert only if the pair (i + 1, j) is  
        // not already present inside the map i.e. 
        // no repeating pair should be present inside  
        // the heap. 
  
        if (my_set.find(temp1) == my_set.end()) { 
            pq.push(make_pair(sum, temp1)); 
            my_set.insert(temp1); 
        } 
  
        // insert (A[i] + B[j + 1], (i, j + 1))  
        // into min heap. 
  
        sum = A[i] + B[j+1]; 
        temp1 = make_pair(i, j+1); 
  
        // insert only if the pair (i, j + 1) 
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
    vector<int> A = {1,3,11}; 
    vector<int> B = {2,4,8}; 
    int K = 4; 
    kSmallestPair(A, B, K); 
    return 0; 
} 
  
// This code is contributed by Dhairya. 
```

输出：

```
(1, 2) (1, 4) (3, 2) (3, 4)
```

时间复杂度：`O(n * logn)`假设`k <= n`。