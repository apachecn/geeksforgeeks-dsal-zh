# 差异小于`K`的对

> 原文： [https://www.geeksforgeeks.org/pairs-difference-less-k/](https://www.geeksforgeeks.org/pairs-difference-less-k/)

给定一个由`n`个整数组成的数组，我们需要找到所有差异小于`k`的对。

**示例**：

```
Input : a[] = {1, 10, 4, 2}
        K = 3
Output : 2
We can make only two pairs 
with difference less than 3.
(1, 2) and (4, 2)

Input : a[] = {1, 8, 7}
        K = 7
Output : 2
Pairs with difference less than 7
are (1, 7) and (8, 7)

```



**方法 1（简单）**：运行两个嵌套循环。 外循环逐个选择每个元素`x`。 内部循环考虑`x`之后的所有元素，并检查差异是否在限制范围内。

## C++ 

```cpp

// CPP code to find count of Pairs with  
// difference less than K. 
#include <bits/stdc++.h> 
using namespace std; 

int countPairs(int a[], int n, int k) 
{ 
    int res = 0; 
    for (int i = 0; i < n; i++)  
      for (int j=i+1; j<n; j++) 
         if (abs(a[j] - a[i]) < k)  
            res++; 

    return res; 
} 

// Driver code 
int main() 
{ 
    int a[] =  {1, 10, 4, 2}; 
    int k = 3; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << countPairs(a, n, k) << endl;  
    return 0; 
} 

```