# 频率与值相同的元素的数组范围查询

> 原文： [https://www.geeksforgeeks.org/array-range-queries-elements-frequency-value/](https://www.geeksforgeeks.org/array-range-queries-elements-frequency-value/)

给定一个由`N`个数字组成的数组，任务是回答以下类型的`Q`个查询：

```
query(start, end) = Number of times a 
number x occurs exactly x times in a 
subarray from start to end

```

**示例**：

> 输入: `arr = {1, 2, 2, 3, 3, 3}`
> 
> 查询 1: `start = 0`, `end = 1`, 
> 
> 查询 2: `start = 1`, `end = 1`, 
> 
> 查询 3: `start = 0`, `end = 2`, 
> 
> 查询 4: `start = 1,` `end = 3`, 
> 
> 查询 5: `start = 3`,` end = 5`, 
> 
> 查询 6: `start = 0`, `end = 5`
> 
> 输出: `1 0 2 1 1 3`

**说明**：

在查询 1 中，元素 1 在子数组`[1, 2]`中出现一次；

在查询 2 中，没有元素满足子数组`[2]`的条件。

在查询 3 中，元素 1 在子数组`[1, 2, 2]`中出现一次，而元素 2 出现两次；

在查询 4 中，元素 2 在子数组`[2, 2, 3]`中出现两次；

在查询 5 中，元素 3 在子数组`[3, 3, 3]`中发生三次。

在查询 6 中，元素 1 在子数组`[1, 2, 2, 3, 3, 3]`中发生一次，2 发生两次，3 发生三次。



**方法 1（暴力）**：

计算每个查询下子数组中每个元素的频率。 如果在每个查询覆盖的子数组中任何数字`x`的频率为`x`，我们将增加计数器。

## C++ 

```cpp

/* C++ Program to answer Q queries to  
   find number of times an element x  
   appears x times in a Query subarray */
#include <bits/stdc++.h> 
using namespace std; 

/* Returns the count of number x with 
   frequency x in the subarray from  
   start to end */
int solveQuery(int start, int end, int arr[]) 
{ 
    // map for frequency of elements 
    unordered_map<int, int> frequency; 

    // store frequency of each element  
    // in arr[start; end] 
    for (int i = start; i <= end; i++)  
        frequency[arr[i]]++;     

    // Count elements with same frequency 
    // as value 
    int count = 0; 
    for (auto x : frequency)  
        if (x.first == x.second)  
            count++;     
    return count; 
} 

int main() 
{ 
    int A[] = { 1, 2, 2, 3, 3, 3 }; 
    int n = sizeof(A) / sizeof(A[0]); 

    // 2D array of queries with 2 columns 
    int queries[][3] = { { 0, 1 }, 
                         { 1, 1 }, 
                         { 0, 2 }, 
                         { 1, 3 }, 
                         { 3, 5 }, 
                         { 0, 5 } }; 

    // calculating number of queries 
    int q = sizeof(queries) / sizeof(queries[0]); 

    for (int i = 0; i < q; i++) { 
        int start = queries[i][0]; 
        int end = queries[i][1]; 
        cout << "Answer for Query " << (i + 1) 
             << " = " << solveQuery(start, 
             end, A) << endl; 
    } 

    return 0; 
} 

```

## Java

```java
/* Java Program to answer Q queries to  
find number of times an element x  
appears x times in a Query subarray */
import java.util.HashMap; 
import java.util.Map; 
  
class GFG  
{ 
  
  
/* Returns the count of number x with 
frequency x in the subarray from  
start to end */
static int solveQuery(int start, int end, int arr[]) 
{ 
    // map for frequency of elements 
    Map<Integer,Integer> mp = new HashMap<>(); 
  
    // store frequency of each element  
    // in arr[start; end] 
    for (int i = start; i <= end; i++)  
        mp.put(arr[i],mp.get(arr[i]) == null?1:mp.get(arr[i])+1);  
  
    // Count elements with same frequency 
    // as value 
    int count = 0; 
    for (Map.Entry<Integer,Integer> entry : mp.entrySet())  
        if (entry.getKey() == entry.getValue())  
            count++;  
    return count; 
} 
  
// Driver code 
public static void main(String[] args)  
{ 
    int A[] = { 1, 2, 2, 3, 3, 3 }; 
    int n = A.length; 
  
    // 2D array of queries with 2 columns 
    int [][]queries = { { 0, 1 }, 
                        { 1, 1 }, 
                        { 0, 2 }, 
                        { 1, 3 }, 
                        { 3, 5 }, 
                        { 0, 5 } }; 
  
    // calculating number of queries 
    int q = queries.length; 
  
    for (int i = 0; i < q; i++)  
    { 
        int start = queries[i][0]; 
        int end = queries[i][1]; 
        System.out.println("Answer for Query " + (i + 1) 
            + " = " + solveQuery(start, 
            end, A)); 
    } 
} 
} 
  
// This code is contributed by Rajput-Ji 
```

## Python3

```py
# Python 3 Program to answer Q queries  
# to find number of times an element x  
# appears x times in a Query subarray 
import math as mt 
  
# Returns the count of number x with 
# frequency x in the subarray from  
# start to end 
def solveQuery(start, end, arr): 
  
    # map for frequency of elements 
    frequency = dict() 
  
    # store frequency of each element  
    # in arr[start end] 
    for i in range(start, end + 1): 
  
  
        if arr[i] in frequency.keys(): 
            frequency[arr[i]] += 1
        else: 
            frequency[arr[i]] = 1
                  
    # Count elements with same  
    # frequency as value 
    count = 0
    for x in frequency:  
        if x == frequency[x]:  
            count += 1
    return count 
  
# Driver code  
A = [1, 2, 2, 3, 3, 3 ] 
n = len(A) 
  
# 2D array of queries with 2 columns 
queries = [[ 0, 1 ], [ 1, 1 ], 
           [ 0, 2 ], [ 1, 3 ], 
           [ 3, 5 ], [ 0, 5 ]] 
  
# calculating number of queries 
q = len(queries) 
  
for i in range(q): 
    start = queries[i][0] 
    end = queries[i][1] 
    print("Answer for Query ", (i + 1),  
          " = ", solveQuery(start,end, A)) 
            
# This code is contributed  
# by Mohit kumar 29 
```

## C#

```cs
// C# Program to answer Q queries to  
// find number of times an element x  
// appears x times in a Query subarray 
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
    /* Returns the count of number x with  
    frequency x in the subarray from  
    start to end */
    public static int solveQuery(int start,  
                                 int end,  
                                 int[] arr) 
    { 
  
        // map for frequency of elements  
        Dictionary<int,  
                   int> mp = new Dictionary<int,  
                                            int>(); 
  
        // store frequency of each element  
        // in arr[start; end]  
        for (int i = start; i <= end; i++) 
        { 
            if (mp.ContainsKey(arr[i])) 
                mp[arr[i]]++; 
            else
                mp.Add(arr[i], 1); 
        } 
  
        // Count elements with same frequency  
        // as value  
        int count = 0; 
        foreach (KeyValuePair<int,  
                              int> entry in mp) 
        { 
            if (entry.Key == entry.Value) 
                count++; 
        } 
        return count; 
    } 
  
    // Driver code  
    public static void Main(String[] args) 
    { 
        int[] A = { 1, 2, 2, 3, 3, 3 }; 
        int n = A.Length; 
  
        // 2D array of queries with 2 columns  
        int[,] queries = {{ 0, 1 }, { 1, 1 }, 
                          { 0, 2 }, { 1, 3 }, 
                          { 3, 5 }, { 0, 5 }}; 
  
        // calculating number of queries  
        int q = queries.Length; 
  
        for (int i = 0; i < q; i++) 
        { 
            int start = queries[i, 0]; 
            int end = queries[i, 1]; 
            Console.WriteLine("Answer for Query " + (i + 1) + 
                              " = " + solveQuery(start, end, A)); 
        } 
    } 
} 
  
// This code is contributed by 
// sanjeev2552 
```

输出：

```
Answer for Query 1 = 1
Answer for Query 2 = 0
Answer for Query 3 = 2
Answer for Query 4 = 1
Answer for Query 5 = 1
Answer for Query 6 = 3
```

时间复杂度：`O(Q * N)`。

方法 2（高效）：

我们可以使用 MO 的算法解决此问题。

我们为每个查询分配开始索引，结束索引和查询编号，每个查询采用以下形式：

+   起始索引（`L`）：查询涵盖的子数组的起始索引；
+   结束索引（`R`）：查询所涵盖的子数组的结束索引；
+   查询编号（`Index`）：由于查询已排序，因此可以告诉我们查询的原始位置，以便我们按原始顺序回答查询。

首先，我们将查询分为多个块，然后使用自定义比较器对查询进行排序。

现在我们离线处理查询，其中每个传入查询保留两个指针，即`MO_RIGHT`和`MO_LEFT`，我们将这些指针向前和向后移动，并根据当前查询的开始和结束索引插入和删除元素。

让当前运行的答案为`current_ans`。

每当我们插入一个元素时，我们都会增加包含元素的频率，如果该频率等于我们刚刚包含的元素，则我们会增加`current_ans`。如果该元素的频率变为（当前元素加 1），则意味着该元素的位置更早当它等于其频率时被计入`current_ans`，因此在这种情况下我们需要减小`current_ans`。

每当我们删除/删除一个元素时，我们都会降低被排除元素的频率，如果该频率等于我们刚刚排除的元素，则我们会增加`current_ans`。如果该元素的频率变为（当前元素减 1），则意味着当此元素等于它的频率时，该元素被计入`current_ans`中，因此在这种情况下，我们需要减小`current_ans`。

```cpp
/* C++ Program to answer Q queries to 
   find number of times an element x  
   appears x times in a Query subarray */
#include <bits/stdc++.h> 
using namespace std; 
  
// Variable to represent block size.  
// This is made global so compare()  
// of sort can use it. 
int block; 
  
// Structure to represent a query range 
struct Query { 
    int L, R, index; 
}; 
  
/* Function used to sort all queries  
   so that all queries of same block 
   are arranged together and within  
   a block, queries are sorted in  
   increasing order of R values. */
bool compare(Query x, Query y) 
{ 
    // Different blocks, sort by block. 
    if (x.L / block != y.L / block) 
        return x.L / block < y.L / block; 
  
    // Same block, sort by R value 
    return x.R < y.R; 
} 
  
/* Inserts element (x) into current range 
   and updates current answer */
void add(int x, int& currentAns,  
         unordered_map<int, int>& freq) 
{ 
  
    // increment frequency of this element 
    freq[x]++; 
  
    // if this element was previously  
    // contributing to the currentAns, 
    // decrement currentAns 
    if (freq[x] == (x + 1)) 
        currentAns--; 
  
    // if this element has frequency  
    // equal to its value, increment 
    // currentAns 
    else if (freq[x] == x) 
        currentAns++; 
} 
  
/* Removes element (x) from current  
   range btw L and R and updates  
   current Answer */
void remove(int x, int& currentAns,  
            unordered_map<int, int>& freq) 
{ 
  
    // decrement frequency of this element 
    freq[x]--; 
  
    // if this element has frequency equal  
    // to its value, increment currentAns 
    if (freq[x] == x) 
        currentAns++; 
  
    // if this element was previously  
    // contributing to the currentAns  
    // decrement currentAns 
    else if (freq[x] == (x - 1))  
        currentAns--; 
} 
  
/* Utility Function to answer all queries 
   and build the ans array in the original  
   order of queries */
void queryResultsUtil(int a[], Query q[],  
                        int ans[], int m) 
{ 
  
    // map to store freq of each element 
    unordered_map<int, int> freq; 
  
    // Initialize current L, current R 
    // and current sum 
    int currL = 0, currR = 0; 
    int currentAns = 0; 
  
    // Traverse through all queries 
    for (int i = 0; i < m; i++) { 
        // L and R values of current range 
        int L = q[i].L, R = q[i].R;  
        int index = q[i].index; 
  
        // Remove extra elements of previous 
        // range. For example if previous  
        // range is [0, 3] and current range  
        // is [2, 5], then a[0] and a[1] are  
        // removed 
        while (currL < L) { 
            remove(a[currL], currentAns, freq); 
            currL++; 
        } 
  
        // Add Elements of current Range 
        while (currL > L) { 
            currL--; 
            add(a[currL], currentAns, freq); 
        } 
        while (currR <= R) { 
            add(a[currR], currentAns, freq); 
            currR++; 
        } 
  
        // Remove elements of previous range.  For example 
        // when previous range is [0, 10] and current range 
        // is [3, 8], then a[9] and a[10] are Removed 
        while (currR > R + 1) { 
            currR--; 
            remove(a[currR], currentAns, freq); 
        } 
  
        // Store current ans as the Query ans for 
        // Query number index 
        ans[index] = currentAns; 
    } 
} 
  
/* Wrapper for queryResultsUtil() and outputs the 
   ans array constructed by answering all queries */
void queryResults(int a[], int n, Query q[], int m) 
{ 
    // Find block size 
    block = (int)sqrt(n); 
  
    // Sort all queries so that queries of same blocks 
    // are arranged together. 
    sort(q, q + m, compare); 
  
    int* ans = new int[m]; 
    queryResultsUtil(a, q, ans, m); 
  
    for (int i = 0; i < m; i++) { 
        cout << "Answer for Query " << (i + 1) 
             << " = " << ans[i] << endl; 
    } 
} 
  
// Driver program 
int main() 
{ 
    int A[] = { 1, 2, 2, 3, 3, 3 }; 
  
    int n = sizeof(A) / sizeof(A[0]); 
  
    // 2D array of queries with 2 columns 
    Query queries[] = { { 0, 1, 0 }, 
                        { 1, 1, 1 }, 
                        { 0, 2, 2 }, 
                        { 1, 3, 3 }, 
                        { 3, 5, 4 }, 
                        { 0, 5, 5 } }; 
  
    // calculating number of queries 
    int q = sizeof(queries) / sizeof(queries[0]); 
  
    // Print result for each Query 
    queryResults(A, n, queries, q); 
  
    return 0; 
} 
```

输出：

```
Answer for Query 1 = 1
Answer for Query 2 = 0
Answer for Query 3 = 2
Answer for Query 4 = 1
Answer for Query 5 = 1
Answer for Query 6 = 3
```

使用 MO 算法的这种方法的时间复杂度为`O(Q * sqrt(N) * logA)`，其中`logA`是为每个查询将元素`A`插入`unordered_map`中的复杂度。