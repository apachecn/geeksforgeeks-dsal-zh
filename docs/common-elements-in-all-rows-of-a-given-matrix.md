# 给定矩阵的所有行中的公共元素

> 原文： [https://www.geeksforgeeks.org/common-elements-in-all-rows-of-a-given-matrix/](https://www.geeksforgeeks.org/common-elements-in-all-rows-of-a-given-matrix/)

给定一个`m x n`矩阵，找到在`O(mn)`时间和矩阵的一个遍历中所有行中存在的所有公共元素。

**示例**：

```
Input:
mat[4][5] = {{1, 2, 1, 4, 8},
             {3, 7, 8, 5, 1},
             {8, 7, 7, 3, 1},
             {8, 1, 2, 7, 9},
            };

Output: 
1 8 or 8 1
8 and 1 are present in all rows.

```



**简单解决方案**是考虑每个元素，并检查所有行中是否存在该元素。 如果存在，请打印。

**更好的解决方案**是对矩阵中的所有行进行排序，并使用与[在这里](https://www.geeksforgeeks.org/find-common-element-rows-row-wise-sorted-matrix/)类似的方法。 排序将花费`O(mnlogn)`时间，而查找公用元素将花费`O(mn)`时间。 因此，此解决方案的总体时间复杂度为`O(mnlogn)`。

**我们能比`O(mnlogn)`做得更好吗？**

这个想法是使用地图。 首先，我们将第一行的所有元素插入到地图中。 对于剩余行中的所有其他元素，我们检查其是否存在于地图中。 如果它存在于地图中并且在当前行中没有重复，则我们将地图中元素的计数增加 1，否则我们将忽略该元素。 如果当前遍历的行是最后一行，则在元素出现`m-1`次之前，我们将对其进行打印。

以下是该想法的实现。

## C++ 

```cpp

// A Program to prints common element in all 
// rows of matrix 
#include <bits/stdc++.h> 
using namespace std; 

// Specify number of rows and columns 
#define M 4 
#define N 5 

// prints common element in all rows of matrix 
void printCommonElements(int mat[M][N]) 
{ 
    unordered_map<int, int> mp; 

    // initalize 1st row elements with value 1 
    for (int j = 0; j < N; j++) 
        mp[mat[0][j]] = 1; 

    // traverse the matrix 
    for (int i = 1; i < M; i++) 
    { 
        for (int j = 0; j < N; j++) 
        { 
            // If element is present in the map and 
            // is not duplicated in current row. 
            if (mp[mat[i][j]] == i) 
            { 
               // we increment count of the element 
               // in map by 1 
                mp[mat[i][j]] = i + 1; 

                // If this is last row 
                if (i==M-1) 
                  cout << mat[i][j] << " "; 
            } 
        } 
    } 
} 

// driver program to test above function 
int main() 
{ 
    int mat[M][N] = 
    { 
        {1, 2, 1, 4, 8}, 
        {3, 7, 8, 5, 1}, 
        {8, 7, 7, 3, 1}, 
        {8, 1, 2, 7, 9}, 
    }; 

    printCommonElements(mat); 

    return 0; 
} 

```

## Java

```java
// Java Program to prints common element in all 
// rows of matrix 
import java.util.*; 
  
class GFG  
{ 
  
// Specify number of rows and columns 
static int M = 4; 
static int N =5; 
  
// prints common element in all rows of matrix 
static void printCommonElements(int mat[][]) 
{ 
  
    Map<Integer,Integer> mp = new HashMap<>(); 
      
    // initalize 1st row elements with value 1 
    for (int j = 0; j < N; j++) 
        mp.put(mat[0][j],1); 
          
    // traverse the matrix 
    for (int i = 1; i < M; i++) 
    { 
        for (int j = 0; j < N; j++) 
        { 
            // If element is present in the map and 
            // is not duplicated in current row. 
            if (mp.get(mat[i][j]) != null && mp.get(mat[i][j]) == i) 
            { 
                // we increment count of the element 
                // in map by 1 
                mp.put(mat[i][j], i + 1); 
  
                // If this is last row 
                if (i == M - 1) 
                    System.out.print(mat[i][j] + " "); 
            } 
        } 
    } 
} 
  
// Driver code 
public static void main(String[] args)  
{ 
    int mat[][] = 
    { 
        {1, 2, 1, 4, 8}, 
        {3, 7, 8, 5, 1}, 
        {8, 7, 7, 3, 1}, 
        {8, 1, 2, 7, 9}, 
    }; 
  
    printCommonElements(mat); 
} 
} 
  
// This code contributed by Rajput-Ji
```

## Python3

```py
# A Program to prints common element  
# in all rows of matrix 
  
# Specify number of rows and columns 
M = 4
N = 5
  
# prints common element in all  
# rows of matrix 
def printCommonElements(mat): 
  
    mp = dict() 
  
    # initalize 1st row elements  
    # with value 1 
    for j in range(N): 
        mp[mat[0][j]] = 1
  
    # traverse the matrix 
    for i in range(1, M): 
        for j in range(N): 
              
            # If element is present in the 
            # map and is not duplicated in  
            # current row. 
            if (mat[i][j] in mp.keys() and
                             mp[mat[i][j]] == i): 
                                   
            # we increment count of the  
            # element in map by 1 
                mp[mat[i][j]] = i + 1
  
                # If this is last row 
                if i == M - 1: 
                    print(mat[i][j], end = " ") 
              
# Driver Code 
mat = [[1, 2, 1, 4, 8], 
       [3, 7, 8, 5, 1], 
       [8, 7, 7, 3, 1], 
       [8, 1, 2, 7, 9]] 
  
printCommonElements(mat) 
  
# This code is conteibuted  
# by mohit kumar 29
```

## C#

```cs
// C# Program to print common element in all 
// rows of matrix to another. 
using System;  
using System.Collections.Generic;  
  
class GFG  
{ 
  
// Specify number of rows and columns 
static int M = 4; 
static int N = 5; 
  
// prints common element in all rows of matrix 
static void printCommonElements(int [,]mat) 
{ 
  
    Dictionary<int, int> mp = new Dictionary<int, int>(); 
      
    // initalize 1st row elements with value 1 
    for (int j = 0; j < N; j++) 
    { 
        if(!mp.ContainsKey(mat[0, j])) 
            mp.Add(mat[0, j], 1); 
    } 
      
    // traverse the matrix 
    for (int i = 1; i < M; i++) 
    { 
        for (int j = 0; j < N; j++) 
        { 
            // If element is present in the map and 
            // is not duplicated in current row. 
            if (mp.ContainsKey(mat[i, j])&& 
               (mp[mat[i, j]] != 0 &&  
                mp[mat[i, j]] == i)) 
            { 
                // we increment count of the element 
                // in map by 1 
                if(mp.ContainsKey(mat[i, j])) 
                { 
                    var v = mp[mat[i, j]]; 
                    mp.Remove(mat[i, j]); 
                    mp.Add(mat[i, j], i + 1); 
                } 
                else
                    mp.Add(mat[i, j], i + 1); 
  
                // If this is last row 
                if (i == M - 1) 
                    Console.Write(mat[i, j] + " "); 
            } 
        } 
    } 
} 
  
// Driver code 
public static void Main(String[] args)  
{ 
    int [,]mat = {{1, 2, 1, 4, 8}, 
                  {3, 7, 8, 5, 1}, 
                  {8, 7, 7, 3, 1}, 
                  {8, 1, 2, 7, 9}}; 
  
    printCommonElements(mat); 
} 
} 
  
// This code is contributed by 29AjayKumar
```

输出：

```
8 1
```

该解决方案的时间复杂度为`O(m * n)`，我们只对矩阵进行一次遍历。