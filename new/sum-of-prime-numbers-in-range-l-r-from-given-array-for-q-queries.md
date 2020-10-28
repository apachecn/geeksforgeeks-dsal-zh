# Q 查询中给定数组在[L，R]范围内的质数之和

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)

给定 **N** 大小的**数组 arr []** ，然后是以下两种类型的 **Q 查询**数组：

*   查询类型 1：给定两个整数 L 和 R，找到从索引 L 到 R 的素数元素的总和，其中 0 <= L <= R <= N-1。

*   查询类型 2：给定两个整数 i 和 X，更改 arr [i] = X，其中 0 <= i <= n-1。

***注意**：子查询的每个第一个索引确定要回答的查询的类型。*

**示例**：

> **输入**：arr [] = {1，3，5，7，9，11}，Q = {{1，1，3}，{2，1，10}，{1，1， 3}}
> **输出**：
> 15
> 12
> **说明**：
> 第一个查询的类型为 1，因此答案为（3 + 5 + 7）= 15
> 第二个查询的类型为 2，因此 arr [1] = 10
> 第三个查询的类型为 1，其中 arr [1] = 10，它不是素数，因此答案为（5 + 7）= 12
> 
> **输入**：arr [] = {1、2、35、7、14、11}，Q = {{2，4，3}，{1，4，5}}
> **输出**：14
> **说明**：
> 第一个查询的类型为 2，因此更新 arr [4] = 3
> 第二个查询的类型为 1，因为 arr [4 ] = 3，这是素数。 所以答案是（3 + 11）= 14

**天真的方法**：的想法是针对 L 到 R 之间的每个查询进行迭代，并在给定的数组上执行所需的操作。

***时间复杂度**：O（Q * N *（O（sqrt（max（arr [i]）））*

**方法**：要优化问题，请使用[细分树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)和[筛网筛网。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   首先，创建一个将标记素数的布尔数组。

*   现在，在制作段树时，仅将这些数组元素添加为素数的叶节点。

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

int const MAX = 1000001; 
bool prime[MAX]; 

// Function to find the prime numbers 
void SieveOfEratosthenes() 
{ 
    // Create a boolean array prime[] 
    // and initialize all entries it as true 
    // A value in prime[i] will 
    // finally be false if i is Not a prime 
    memset(prime, true, sizeof(prime)); 

    for (int p = 2; p * p <= MAX; p++) { 

        // Check if prime[p] is not 
        // changed, then it is a prime 
        if (prime[p] == true) { 

            // Update all multiples of p 
            // greater than or equal to 
            // the square of it numbers 
            // which are multiple of p 
            // and are less than p^2 are 
            // already been marked 
            for (int i = p * p; i <= MAX; i += p) 
                prime[i] = false; 
        } 
    } 
} 

// Function to get the middle 
// index from corner indexes 
int getMid(int s, int e) 
{ 
    return s + (e - s) / 2; 
} 

// Function to get the sum of 
// values in the given range 
// of the array 

int getSumUtil(int* st, int ss, 
               int se, int qs, 
               int qe, int si) 
{ 
    // If segment of this node is a 
    // part of given range, then 
    // return the sum of the segment 
    if (qs <= ss && qe >= se) 
        return st[si]; 

    // If segment of this node is 
    // outside the given range 
    if (se < qs || ss > qe) 
        return 0; 

    // If a part of this segment 
    // overlaps with the given range 
    int mid = getMid(ss, se); 

    return getSumUtil(st, ss, mid, 
                      qs, qe, 
                      2 * si + 1) 
           + getSumUtil(st, mid + 1, 
                        se, qs, qe, 
                        2 * si + 2); 
} 

// Function to update the nodes which 
// have the given index in their range 
void updateValueUtil(int* st, int ss, 
                     int se, int i, 
                     int diff, int si) 
{ 
    // If the input index lies 
    // outside the range of 
    // this segment 
    if (i < ss || i > se) 
        return; 

    // If the input index is in 
    // range of this node, then update 
    // the value of the node and its children 
    st[si] = st[si] + diff; 
    if (se != ss) { 
        int mid = getMid(ss, se); 
        updateValueUtil(st, ss, mid, i, 
                        diff, 2 * si + 1); 
        updateValueUtil(st, mid + 1, 
                        se, i, diff, 
                        2 * si + 2); 
    } 
} 

// Function to update a value in 
// input array and segment tree 
void updateValue(int arr[], int* st, 
                 int n, int i, 
                 int new_val) 
{ 
    // Check for erroneous input index 
    if (i < 0 || i > n - 1) { 
        cout << "-1"; 
        return; 
    } 

    // Get the difference between 
    // new value and old value 
    int diff = new_val - arr[i]; 

    int prev_val = arr[i]; 

    // Update the value in array 
    arr[i] = new_val; 

    // Update the values of 
    // nodes in segment tree 
    // only if either previous 
    // value or new value 
    // or both are prime 
    if (prime[new_val] 
        || prime[prev_val]) { 

        // If only new value is prime 
        if (!prime[prev_val]) 
            updateValueUtil(st, 0, n - 1, 
                            i, new_val, 0); 

        // If only new value is prime 
        else if (!prime[new_val]) 
            updateValueUtil(st, 0, n - 1, 
                            i, -prev_val, 0); 

        // If both are prime 
        else
            updateValueUtil(st, 0, n - 1, 
                            i, diff, 0); 
    } 
} 

// Return sum of elements in range 
// from index qs (quey start) to qe 
// (query end). It mainly uses getSumUtil() 
int getSum(int* st, int n, int qs, int qe) 
{ 
    // Check for erroneous input values 
    if (qs < 0 || qe > n - 1 || qs > qe) { 
        cout << "-1"; 
        return -1; 
    } 

    return getSumUtil(st, 0, n - 1, 
                      qs, qe, 0); 
} 

// Function that constructs Segment Tree 
int constructSTUtil(int arr[], int ss, 
                    int se, int* st, 
                    int si) 
{ 
    // If there is one element in 
    // array, store it in current node of 
    // segment tree and return 
    if (ss == se) { 

        // Only add those elements in segment 
        // tree which are prime 
        if (prime[arr[ss]]) 
            st[si] = arr[ss]; 
        else
            st[si] = 0; 
        return st[si]; 
    } 

    // If there are more than one 
    // elements, then recur for left and 
    // right subtrees and store the 
    // sum of values in this node 
    int mid = getMid(ss, se); 
    st[si] 
        = constructSTUtil(arr, ss, mid, 
                          st, si * 2 + 1) 
          + constructSTUtil(arr, mid + 1, 
                            se, st, 
                            si * 2 + 2); 
    return st[si]; 
} 

// Function to construct segment 
// tree from given array 
int* constructST(int arr[], int n) 
{ 
    // Allocate memory for the segment tree 

    // Height of segment tree 
    int x = (int)(ceil(log2(n))); 

    // Maximum size of segment tree 
    int max_size = 2 * (int)pow(2, x) - 1; 

    // Allocate memory 
    int* st = new int[max_size]; 

    // Fill the allocated memory st 
    constructSTUtil(arr, 0, n - 1, st, 0); 

    // Return the constructed segment tree 
    return st; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 3, 5, 7, 9, 11 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int Q[3][3] 
        = { { 1, 1, 3 }, 
            { 2, 1, 10 }, 
            { 1, 1, 3 } }; 

    // Function call 
    SieveOfEratosthenes(); 

    // Build segment tree from given array 
    int* st = constructST(arr, n); 

    // Print sum of values in 
    // array from index 1 to 3 
    cout << getSum(st, n, 1, 3) << endl; 

    // Update: set arr[1] = 10 
    // and update corresponding 
    // segment tree nodes 
    updateValue(arr, st, n, 1, 10); 

    // Find sum after the value is updated 
    cout << getSum(st, n, 1, 3) << endl; 
    return 0; 
}

```

## Python3

```py

# Python3 program for the above approach 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
import math 
MAX = 1000001

# Create a boolean array prime[] 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# and initialize all entires it as true 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# A value in prime[i] will  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# finally be false if i is Not a prime 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
prime = [True] * MAX

# Function to find prime numbers 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def SieveOfEratosthenes(): 

    p = 2
    while p * p <= MAX: 

        # Check if prime[p] is not  
        # changed, then it is a prime  
        if prime[p] == True: 

            # Update all multiples of p  
            # greater than or equal to  
            # the square of it numbers  
            # which are multiple of p  
            # and are less than p^2 are  
            # already been marked  
            for i in range(p * p, MAX, p): 
                prime[i] = False

        p += 1

# Function to get the middle  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# index from corner indexes  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def getMid(s, e): 

    return s + (e - s) // 2

# Function to get the sum of  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# values in the given range  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# of the array  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def getSumUtil(st, ss, se, qs, qe, si): 

    # If segment of this node is a  
    # part of given range, then  
    # return the sum of the segment  
    if qs <= ss and qe >= se: 
        return st[si] 

    # If segment of this node is  
    # outside the given range  
    if se < qs or ss > qe: 
        return 0

    # If a part of this segment  
    # overlaps with the given range  
    mid = getMid(ss, se) 

    return (getSumUtil(st, ss, mid, qs, 
                       qe, 2 * si + 1) +
            getSumUtil(st, mid + 1, se, 
                       qs, qe, 2 * si + 2)) 

# Function to update the nodes which  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# have the given index in their range  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def updateValueUtil(st, ss, se, i, diff, si): 

    # If the input index lies  
    # outside the range of  
    # this segment  
    if i < ss or i > se: 
        return

    # If the input index is in  
    # range of this node, then update  
    # the value of the node and its children  
    st[si] = st[si] + diff 

    if se != ss: 
        mid = getMid(ss, se) 
        updateValueUtil(st, ss, mid, i, 
                        diff, 2 * si + 1) 
        updateValueUtil(st, mid + 1, se, i, 
                        diff, 2 * si + 2) 

# Function to update a value in  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# input array and segment tree  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def updateValue(arr, st, n, i, new_val): 

    # Check for errorneous imput index 
    if i < 0 or i > n - 1: 
        print(-1) 
        return

    # Get the difference between  
    # new value and old value  
    diff = new_val - arr[i] 

    prev_val = arr[i] 

    # Update the value in array 
    arr[i] = new_val 

    # Update the values of nodes 
    # in segment tree only if  
    # either previous value or  
    # new value or both are prime  
    if prime[new_val] or prime[prev_val]: 

        # If only new value is prime 
        if not prime[prev_val]: 
            updateValueUtil(st, 0, n - 1,  
                            i, new_val, 0) 

        # If only old value is prime 
        elif not prime[new_val]: 
            updateValueUtil(st, 0, n - 1, i, 
                            -prev_val, 0) 

        # If both are prime 
        else: 
            updateValueUtil(st, 0, n - 1, 
                            i, diff, 0) 

# Return sum of elements in range  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# from index qs (quey start) to qe  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# (query end). It mainly uses getSumUtil()  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def getSum(st, n, qs, qe): 

    # Check for erroneous input values  
    if qs < 0 or qe > n-1 or qs > qe: 
        return -1

    return getSumUtil(st, 0, n - 1, qs, qe, 0) 

# Function that constructs the Segment Tree 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def constructSTUtil(arr, ss, se, st, si): 

    # If there is one element in  
    # array, store it in current   
    # node of segment tree and return  
    if ss == se: 

        # Only add those elements in segment  
        # tree which are prime  
        if prime[arr[ss]]: 
            st[si] = arr[ss] 
        else: 
            st[si] = 0

        return st[si] 

    # If there are more than one  
    # elements, then recur for left and  
    # right subtrees and store the  
    # sum of values in this node  
    mid = getMid(ss, se) 
    st[si] = (constructSTUtil(arr, ss, mid, st, 
                              2 * si + 1) +
              constructSTUtil(arr, mid + 1, se,  
                              st, 2 * si + 2)) 
    return st[si] 

# Function to construct segment  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# tree from given array  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
def constructST(arr, n): 

    # Allocate memory for the segment tree 

    # Height of segment tree 
    x = int(math.ceil(math.log2(n))) 

    # Maximum size of segment tree 
    max_size = 2 * int(pow(2, x)) - 1

    # Allocate memory 
    st = [0] * max_size 

    # Fill the allocated memory st  
    constructSTUtil(arr, 0, n - 1, st, 0) 

    # Return the constructed segment tree  
    return st 

# Driver code 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
arr = [ 1, 3, 5, 7, 9, 11 ] 
n = len(arr) 

Q = [ [ 1, 1, 3 ], 
      [ 2, 1, 10 ], 
      [ 1, 1, 3 ] ] 

# Function call 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
SieveOfEratosthenes() 

# Build segment tree from given array 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
st = constructST(arr, n) 

# Print sum of values in  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# array from index 1 to 3  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
print(getSum(st, n, 1, 3)) 

# Update: set arr[1] = 10  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# and update corresponding  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
# segment tree nodes  

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
updateValue(arr, st, n, 1, 10) 

# Find sum after value is updated 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)
print(getSum(st, n, 1, 3)) 

# This code is contrinuted by Stuti Pathak 

> 原文：[https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/](https://www.geeksforgeeks.org/sum-of-prime-numbers-in-range-l-r-from-given-array-for-q-queries/)

```

**Output:** 

```
15
12

```

***时间复杂度**：O（Q * log N）*

***辅助空间**：O（N）*



* * *

* * *



