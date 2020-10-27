# 检查矩阵

中是否存在具有给定绝对差的一对

给定一个 N×M 矩阵和一个 **K** 之差。 任务是检查矩阵中是否存在具有给定绝对差的一对。
**范例**：

```
Input: mat[N][M] = {{1, 2, 3, 4},
                    {5, 6, 7, 8},
                    {9, 10, 11, 12},
                    {13, 14, 15, 100}};
       K = 85
Output: YES

Input: mat[N][M] = {{1, 2, 3, 4},
                   {5, 6, 7, 8}};
       K = 150
Output: NO

```

**方法：**

*   初始化[哈希图](https://www.geeksforgeeks.org/hashing-data-structure/)，以跟踪矩阵中已访问的元素。
*   遍历矩阵，并检查当前元素与 k 的差是否已存在于哈希图中。 如果是，则当前元素以及该元素与 k 的差为所需对。
*   否则，将当前元素添加到地图中。

下面是上述方法的实现：

## C++

```cpp

// CPP code to check for pair with given 
// difference exists in the matrix or not 

#include <bits/stdc++.h> 
using namespace std; 

#define N 4 
#define M 4 

// Function to check if a pair with given 
// difference exists in the matrix 
bool isPairWithDiff(int mat[N][M], int k) 
{ 
    unordered_set <int> ump ;

    // Loop to iterate over the matrix
    for( int i = 0 ; i < N  ; i++ )
    {
        for( int j =0 ; j < M ; j++ )
        {
            if( mat[i][j] > k )
            {
                int m = mat[i][j] - k ;

                if( ump.find(m) != ump.end() )
                {
                    return true ;
                }
            }
            else
            {
                int m = k - mat[i][j] ;

                if( ump.find(m) != ump.end() )
                {
                    return true ;
                }
            }
            ump.insert(mat[i][j]);
        }
    }
  return false;
} 

// Driver Code 
int main() 
{ 
    // Input matrix 
    int mat[N][M] ={ { 5, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 100 } }; 

    // Given difference 
    int k = 85; 

    if (isPairWithDiff(mat, k)) 
        cout << "YES" << endl;     
    else
        cout << "NO" << endl; 

    return 0; 
}

```

## Java

```java

// Java code to check for pair with given
// difference exists in the matrix or not
import java.util.*;

class GFG 
{

static final int N = 4;
static final int M = 4;

// Function to check if a pair with given
// difference exists in the matrix
static boolean isPairWithDiff(int mat[][], int k)
{
    // Store elements in a hash
    HashSet<Integer> s = new HashSet<Integer>();

    // Loop to iterate over the 
    // elements of the matrix
    for (int i = 0; i < N; i++) 
    {
        for (int j = 0; j < M; j++) {
            if( mat[i][j] > k )
            {
                int m = mat[i][j] - k ;

                if(s.contains(m))
                {
                    return true ;
                }
            }
            else
            {
                int m = k - mat[i][j] ;

                if(s.contains(m))
                {
                    return true ;
                }
            }
            s.add(mat[i][j]);     
        }
    }  

    return false;
}

// Driver Code
public static void main(String[] args)
{
    // Input matrix
    int mat[][] = { { 5, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 100 } };

    // Given difference
    int k = 85;

    System.out.println(
      isPairWithDiff(mat, k) == true ? 
      "YES" : "NO"); 
}
}

// This code contributed by Rajput-Ji

```

## Python3

```py

# Python 3 program to check for pairs 
# with given difference exits in the 
# matrix or not 
N = 4
M = 4

# Function to check if a 
# pair with given
# difference exist in the matrix
def isPairWithDiff(mat, k):

    # Store elements in a hash
    s = set()

    # Store elements in dict 
    for i in range(N):
        for j in range(M):
            if mat[i][j] > k:
                m = mat[i][j] - k
                if m in s:
                    return True
            else:
                m = k - mat[i][j]
                if m in s:
                    return True
            s.add(mat[i][j])

    return False       

# Driver Code
n, m = 4, 4
mat = [[5, 2, 3, 4],
       [5, 6, 7, 8],
       [9, 10, 11, 12],
       [13, 14, 15, 100]]

# given difference
k = 85

if isPairWithDiff(mat, k):
    print("Yes")
else:
    print("No")

# This code is contributed by
# Mohit kumar 29 (IIIT gwalior)

```

## C#

```cs

// C# code to check for pair with given
// difference exists in the matrix or not
using System;
using System.Collections.Generic; 

class GFG 
{

static int N = 4;
static int M = 4;

// Function to check if a pair with given
// difference exists in the matrix
static Boolean isPairWithDiff(
             int [,]mat, int k)
{
    // Store elements in a hash
    HashSet<int> s = new HashSet<int>();
    for (int i = 0; i < N; i++) 
    {
        for (int j = 0; j < M; j++) 
        {
            if( mat[i, j] > k )
            {
                int m = mat[i, j] - k ;

                if(s.Contains(m))
                {
                    return true ;
                }
            }
            else
            {
                int m = k - mat[i, j];

                if(s.Contains(m))
                {
                    return true ;
                }
            }
            s.Add(mat[i, j]);   
        }
    }

    return false;
}

// Driver Code
public static void Main(String[] args)
{
    // Input matrix
    int [,]mat = { { 5, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 100 } };

    // Given difference
    int k = 85;

    Console.WriteLine(
      isPairWithDiff(mat, k) == true ? 
      "YES" : "NO"); 
}
}

/* This code contributed by PrinciRaj1992 */

```

**Output**

```
YES

```

***时间复杂度**：O（N * M）*
***辅助空间：** O（N * M）*



* * *

* * *



