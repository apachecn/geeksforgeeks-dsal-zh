# 使用稀疏表进行范围总和查询

> 原文： [https://www.geeksforgeeks.org/range-sum-query-using-sparse-table/](https://www.geeksforgeeks.org/range-sum-query-using-sparse-table/)

我们有一个数组`arr[]`。 我们需要找到`L`和`R`范围内所有元素的总和，其中`0 <= L <= R <= n-1`。 考虑存在许多范围查询的情况。

**示例**：

```
Input : 3 7 2 5 8 9
        query(0, 5)
        query(3, 5)
        query(2, 4)
Output : 34
         22
         15

Note : array is 0 based indexed
       and queries too.

```



由于没有更新/修改，因此我们使用[稀疏表](http://www.geeksforgeeks.org/sparse-table/)有效地回答查询。 在稀疏表中，我们以 2 的幂来分解查询。

```
Suppose we are asked to compute sum of 
elements from arr[i] to arr[i+12]. 
We do the following:

// Use sum of 8 (or 23) elements 
table[i][3] = sum(arr[i], arr[i + 1], ...
                               arr[i + 7]).

// Use sum of 4 elements
table[i+8][2] = sum(arr[i+8], arr[i+9], ..
                                arr[i+11]).

// Use sum of single element
table[i + 12][0] = sum(arr[i + 12]).

Our result is sum of above values.
```

请注意，对于大小为 13 的子数组，只需要执行 4 个操作即可计算结果。

## C++ 

```cpp

// CPP program to find the sum in a given 
// range in an array using sparse table. 
#include <bits/stdc++.h> 
using namespace std; 

// Because 2^17 is larger than 10^5 
const int k = 16; 

// Maximum value of array 
const int N = 1e5; 

// k + 1 because we need to access 
// table[r][k] 
long long table[N][k + 1]; 

// it builds sparse table. 
void buildSparseTable(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        table[i][0] = arr[i]; 

    for (int j = 1; j <= k; j++) 
        for (int i = 0; i <= n - (1 << j); i++) 
            table[i][j] = table[i][j - 1] + 
               table[i + (1 << (j - 1))][j - 1]; 
} 

// Returns the sum of the elements in the range 
// L and R. 
long long query(int L, int R) 
{ 
    // boundaries of next query, 0-indexed 
    long long answer = 0; 
    for (int j = k; j >= 0; j--) { 
        if (L + (1 << j) - 1 <= R) { 
            answer = answer + table[L][j]; 

            // instead of having L', we 
            // increment L directly 
            L += 1 << j; 
        } 
    } 
    return answer; 
} 

// Driver program. 
int main() 
{ 
    int arr[] = { 3, 7, 2, 5, 8, 9 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    buildSparseTable(arr, n); 

    cout << query(0, 5) << endl; 
    cout << query(3, 5) << endl; 
    cout << query(2, 4) << endl; 

    return 0; 
} 

```

## Java

```java
// Java program to find the sum  
// in a given range in an array  
// using sparse table. 
class GFG 
{ 
      
// Because 2^17 is larger than 10^5 
static int k = 16; 
  
// Maximum value of array 
static int N = 100000; 
  
// k + 1 because we need 
// to access table[r][k] 
static long table[][] = new long[N][k + 1]; 
  
// it builds sparse table. 
static void buildSparseTable(int arr[], 
                             int n) 
{ 
    for (int i = 0; i < n; i++) 
        table[i][0] = arr[i]; 
  
    for (int j = 1; j <= k; j++) 
        for (int i = 0; i <= n - (1 << j); i++) 
            table[i][j] = table[i][j - 1] + 
            table[i + (1 << (j - 1))][j - 1]; 
} 
  
// Returns the sum of the  
// elements in the range L and R. 
static long query(int L, int R) 
{ 
    // boundaries of next query, 
    // 0-indexed 
    long answer = 0; 
    for (int j = k; j >= 0; j--)  
    { 
        if (L + (1 << j) - 1 <= R)  
        { 
            answer = answer + table[L][j]; 
  
            // instead of having L', we 
            // increment L directly 
            L += 1 << j; 
        } 
    } 
    return answer; 
} 
  
// Driver Code 
public static void main(String args[]) 
{ 
    int arr[] = { 3, 7, 2, 5, 8, 9 }; 
    int n = arr.length; 
  
    buildSparseTable(arr, n); 
  
    System.out.println(query(0, 5)); 
    System.out.println(query(3, 5)); 
    System.out.println(query(2, 4)); 
} 
} 
  
// This code is contributed  
// by Kirti_Mangal
```

## C#

```cs
// C# program to find the  
// sum in a given range 
// in an array using 
// sparse table. 
using System; 
  
class GFG 
{ 
    // Because 2^17 is 
    // larger than 10^5 
    static int k = 16; 
      
    // Maximum value  
    // of array 
    static int N = 100000; 
      
    // k + 1 because we  
    // need to access table[r,k] 
    static long [,]table =  
           new long[N, k + 1]; 
      
    // it builds sparse table. 
    static void buildSparseTable(int []arr,  
                                 int n) 
    { 
        for (int i = 0; i < n; i++) 
            table[i, 0] = arr[i]; 
      
        for (int j = 1; j <= k; j++) 
            for (int i = 0;      
                     i <= n - (1 << j); i++) 
                table[i, j] = table[i, j - 1] + 
                table[i + (1 << (j - 1)), j - 1]; 
    }      
      
    // Returns the sum of the 
    // elements in the range 
    // L and R. 
    static long query(int L, int R) 
    { 
        // boundaries of next  
        // query, 0-indexed 
        long answer = 0; 
        for (int j = k; j >= 0; j--)  
        { 
            if (L + (1 << j) - 1 <= R)  
            { 
                answer = answer +  
                         table[L, j]; 
      
                // instead of having  
                // L', we increment  
                // L directly 
                L += 1 << j; 
            } 
        } 
        return answer; 
    } 
      
    // Driver Code 
    static void Main() 
    { 
        int []arr = new int[]{3, 7, 2,  
                              5, 8, 9}; 
        int n = arr.Length; 
      
        buildSparseTable(arr, n); 
      
        Console.WriteLine(query(0, 5)); 
        Console.WriteLine(query(3, 5)); 
        Console.WriteLine(query(2, 4)); 
    } 
} 
  
// This code is contributed by  
// Manish Shaw(manishshaw1)
```

## Python3

```py
# Python3 program to find the sum in a given 
# range in an array using sparse table. 
  
# Because 2^17 is larger than 10^5 
k = 16
  
# Maximum value of array 
n = 100000
  
# k + 1 because we need to access 
# table[r][k] 
  
table = [[0 for j in range(k+1)] for i in range(n)] 
  
# it builds sparse table 
def buildSparseTable(arr, n): 
    global table, k 
    for i in range(n): 
        table[i][0] = arr[i] 
  
    for j in range(1,k+1): 
        for i in range(0,n-(1<<j)+1): 
            table[i][j] = table[i][j-1] + \ 
                          table[i + (1 << (j - 1))][j - 1] 
  
# Returns the sum of the elements in the range 
# L and R. 
def query(L, R): 
    global table, k 
  
    # boundaries of next query, 0 - indexed 
    answer = 0
    for j in range(k,-1,-1): 
        if (L + (1 << j) - 1 <= R): 
            answer = answer + table[L][j] 
  
            # instead of having L ', we 
            # increment L directly 
            L+=1<<j 
  
    return answer 
  
# Driver program 
if __name__ == '__main__': 
    arr = [3, 7, 2, 5, 8, 9] 
    n = len(arr) 
  
    buildSparseTable(arr, n) 
    print(query(0,5)) 
    print(query(3,5)) 
    print(query(2,4)) 
      
# This code is contributed by  
# chaudhary_19 (Mayank Chaudhary)
```

输出：

```
34
22
15
```

这种用稀疏表回答查询的算法适用于`O(k)`，即`O(log(n))`，因为我们选择最小的`k`使得`2 ^ k + 1 > n`。

稀疏表构造的时间复杂度：外循环以`O(k)`运行，内循环以`O(n)`运行。 因此，总的来说，我们得到`O(n * k)= O(n * log(n))`。