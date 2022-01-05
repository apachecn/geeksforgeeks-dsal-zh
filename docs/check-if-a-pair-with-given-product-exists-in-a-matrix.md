# 检查矩阵中是否存在给定产品的配对

> 原文:[https://www . geesforgeks . org/check-if-a-pair-with-给定产品-存在于矩阵中/](https://www.geeksforgeeks.org/check-if-a-pair-with-given-product-exists-in-a-matrix/)

给定一个 NxM 矩阵和一个产品 k。任务是检查矩阵中是否存在与给定产品的配对。
**例** :

```
Input: mat[N][M] = {{1, 2, 3, 4},
                    {5, 6, 7, 8},
                    {9, 10, 11, 12},
                    {13, 14, 15, 16}};
       K = 42
Output: YES

Input: mat[N][M] = {{1, 2, 3, 4},
                   {5, 6, 7, 8}};
       K = 150
Output: NO
```

**进场:**

*   取一个散列来存储散列中矩阵的所有元素。
*   开始遍历矩阵，遍历时检查矩阵的当前元素是否能被给定的乘积整除，当乘积 K 被当前元素除时，得到的被除数也出现在散列中。
    即

```
(k % mat[i][j] == 0) && (mp[k / mat[i][j]] > 0)
```

*   如果存在，则返回 true，否则将当前元素插入哈希。
*   如果遍历了矩阵的所有元素，但没有找到对，则返回 false。

以下是上述方法的实现:

## C++

```
// CPP code to check for pair with given product
// exists in the matrix or not
#include <bits/stdc++.h>
using namespace std;

#define N 4
#define M 4

// Function to check if a pair with given
// product exists in the matrix
bool isPairWithProductK(int mat[N][M], int k)
{
    // hash to store elements
    unordered_set<int> s;

    // looping through elements
    // if present in the matrix
    // return true, else push
    // the element in matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if ((k % mat[i][j] == 0) && (s.find(k / mat[i][j]) != s.end())) {
                return true;
            }
            else {
                s.insert(mat[i][j]);
            }
        }
    }

    return false;
}

// Driver code
int main()
{
    // Input matrix
    int mat[N][M] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    // given product
    int k = 42;

    if (isPairWithProductK(mat, k)) {
        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check for pair with given product
// exists in the matrix or not
import java.util.*;
class GFG
{
     static final int N=4;
     static final int M=4;

    // Function to check if a pair with given
    // product exists in the matrix
    static boolean isPairWithProductK(int mat[][], int k)
    {
        // hash to store elements
        Set<Integer> s=new HashSet<Integer>();

        // looping through elements
        // if present in the matrix
        // return true, else push
        // the element in matrix
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if ((k % mat[i][j] == 0) && s.contains(k / mat[i][j])) {
                    return true;
                }
                else {
                    s.add(mat[i][j]);
                }
            }
        }

        return false;
    }

    // Driver code
    public static void main(String [] args)
    {

        // Input matrix
        int mat[][] = { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 9, 10, 11, 12 },
                        { 13, 14, 15, 16 } };

        // given product
        int k = 42;

        if (isPairWithProductK(mat, k)) {
            System.out.println("YES");
        }
        else
            System.out.println("NO");

    }

    // This code is contributed by ihritik
}
```

## 蟒蛇 3

```
# Python 3 code to check for pair with
# given product exists in the matrix or not
N = 4
M = 4

# Function to check if a pair with
# given product exists in the matrix
def isPairWithProductK(mat, k):

    # hash to store elements
    s = []

    # looping through elements if present
    # in the matrix return true, else push
    # the element in matrix
    for i in range(N) :
        for j in range(M):
            if ((k % mat[i][j] == 0) and
                (k // mat[i][j]) in s):
                return True

            else :
                s.append(mat[i][j])

    return False

# Driver code
if __name__ == "__main__":

    # Input matrix
    mat = [[ 1, 2, 3, 4 ],
           [ 5, 6, 7, 8 ],
           [ 9, 10, 11, 12 ],
           [ 13, 14, 15, 16 ]]

    # given product
    k = 42

    if (isPairWithProductK(mat, k)):
        print( "YES")

    else:
        print("NO")

# This code is contributed by ita_c
```

## C#

```
// C# code to check for pair with given product
// exists in the matrix or not
using System;
using System.Collections.Generic;

class GFG
{
    static readonly int N = 4;
    static readonly int M = 4;

    // Function to check if a pair with given
    // product exists in the matrix
    static bool isPairWithProductK(int [,]mat, int k)
    {
        // hash to store elements
        HashSet<int> s = new HashSet<int>();

        // looping through elements
        // if present in the matrix
        // return true, else push
        // the element in matrix
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if ((k % mat[i, j] == 0) &&
                    s.Contains(k / mat[i, j]))
                {
                    return true;
                }
                else
                {
                    s.Add(mat[i, j]);
                }
            }
        }

        return false;
    }

    // Driver code
    public static void Main()
    {

        // Input matrix
        int [,]mat = { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 9, 10, 11, 12 },
                        { 13, 14, 15, 16 } };

        // given product
        int k = 42;

        if (isPairWithProductK(mat, k))
        {
            Console.WriteLine("YES");
        }
        else
            Console.WriteLine("NO");
    }
}

// This code has been contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript code to check for pair with given product
// exists in the matrix or not

    let N = 4;
    let M = 4;

    function isPairWithProductK(mat,k)
    {
        // hash to store elements
        let s=new Set();

        // looping through elements
        // if present in the matrix
        // return true, else push
        // the element in matrix
        for (let i = 0; i < N; i++) {
            for (let j = 0; j < M; j++) {
                if ((k % mat[i][j] == 0) && s.has(Math.floor(k / mat[i][j]))) {
                    return true;
                }
                else {
                    s.add(mat[i][j]);
                }
            }
        }

        return false;
    }

    // Driver code

    // Input matrix
    let mat = [[ 1, 2, 3, 4 ],
                    [ 5, 6, 7, 8] ,
                    [ 9, 10, 11, 12] ,
                    [13, 14, 15, 16]] ;

    // given product

    let k = 42;

    if (isPairWithProductK(mat, k))
    {
        document.write("YES");
    }
    else
        document.write("NO");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
YES
```

**时间复杂度** : O(N*M)