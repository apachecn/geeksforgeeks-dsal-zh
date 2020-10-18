# 数组中范围的乘积

> 原文： [https://www.geeksforgeeks.org/products-ranges-array/](https://www.geeksforgeeks.org/products-ranges-array/)

给定大小为`N`的数组`A[]`。解决`Q`个查询。 在模`P`下找到`[L, R]`范围内的乘积（`P`为质数）。

**示例**：

```
Input : A[] = {1, 2, 3, 4, 5, 6} 
          L = 2, R = 5, P = 229
Output : 120

Input : A[] = {1, 2, 3, 4, 5, 6},
         L = 2, R = 5, P = 113
Output : 7

```



**暴力**：

对于每个查询，遍历`[L, R]`范围内的每个元素并计算模`P`下的乘积。这将以`O(n)`回答每个查询。

## C++ 

```cpp

// Product in range  
// Queries in O(N) 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate  
// Product in the given range. 
int calculateProduct(int A[], int L,  
                     int R, int P) 
{ 
    // As our array is 0 based  
    // as and L and R are given 
    // as 1 based index. 
    L = L - 1; 
    R = R - 1; 

    int ans = 1; 
    for (int i = L; i <= R; i++)  
    { 
        ans = ans * A[i]; 
        ans = ans % P; 
    } 

    return ans; 
} 

// Driver code 
int main() 
{ 
    int A[] = { 1, 2, 3, 4, 5, 6 }; 
    int P = 229; 
    int L = 2, R = 5; 
    cout << calculateProduct(A, L, R, P) 
         << endl; 

    L = 1, R = 3; 
    cout << calculateProduct(A, L, R, P)  
         << endl; 

    return 0; 
} 

```