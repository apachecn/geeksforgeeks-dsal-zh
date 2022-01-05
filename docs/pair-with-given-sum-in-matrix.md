# 与矩阵中给定的和配对

> 原文:[https://www . geeksforgeeks . org/与给定矩阵相加/](https://www.geeksforgeeks.org/pair-with-given-sum-in-matrix/)

给定一个 NxM 矩阵和一个和 s，任务是检查矩阵中是否存在给定和的对。
**例** :

```
Input: mat[N][M] = {{1, 2, 3, 4},
                {5, 6, 7, 8},
                {9, 10, 11, 12},
                {13, 14, 15, 16}};
       sum = 31
Output: YES

Input: mat[N][M] = {{1, 2, 3, 4},
                {5, 6, 7, 8}};
       sum = 150
Output: NO
```

**进场:**

*   取一个散列来存储散列中矩阵的所有元素。
*   开始遍历矩阵，并在遍历时检查散列中是否存在 abs(sum-matrix_element)。
*   如果存在，则返回 true，否则将当前矩阵元素插入散列。
*   如果遍历了矩阵的所有元素，但没有找到对，则返回 false。

以下是上述方法的实现:

## C++

```
// CPP code to check for pair with given sum
#include <bits/stdc++.h>
using namespace std;

#define N 4
#define M 4

// Function to check if a pair with given sum
// exists in the matrix
bool isPairWithSum(int mat[N][M], int sum)
{
    // hash to store elements
    unordered_set<int> s;

    // looping through elements
    // if present in the matrix
    // return true, else push
    // the element in matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if (s.find(sum - mat[i][j]) != s.end()) {
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

    // given sum
    int sum = 11;

    if (isPairWithSum(mat, sum)) {
        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check for pair
// with given sum
import java.util.*;

class GFG
{

// Function to check if a pair with
// given sum exists in the matrix
static final int N = 4;
static final int M = 4;
static boolean isPairWithSum(int [][]mat,
                             int sum)
{
    // hash to store elements
    Set<Integer> s = new HashSet<Integer>();

    // looping through elements
    // if present in the matrix
    // return true, else push
    // the element in matrix
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            if (s.contains(sum - mat[i][j]))
            {
                return true;
            }
            else
            {
                s.add(mat[i][j]);
            }
        }
    }

    return false;
}

// Driver code
public static void main(String []args)
{

    // Input matrix
    int [][]mat = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    // given sum
    int sum = 11;

    if (isPairWithSum(mat, sum))
    {
        System.out.println("YES");
    }
    else
        System.out.println("NO");
}
}

// This code is contributed by ihritik
```

## C#

```
// C# code to check for pair
// with given sum
using System;
using System.Collections.Generic;

class GFG
{

// Function to check if a pair with
// given sum exists in the matrix
static readonly int N = 4;
static readonly int M = 4;
static bool isPairWithSum(int [,]mat,
                            int sum)
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
            if (s.Contains(sum - mat[i, j]))
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
public static void Main(String []args)
{

    // Input matrix
    int [,]mat = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    // given sum
    int sum = 11;

    if (isPairWithSum(mat, sum))
    {
        Console.WriteLine("YES");
    }
    else
        Console.WriteLine("NO");
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# python code to check for pair with given sum

N= 4
M= 4

# Function to check if a pair with given sum
# exists in the matrix
def isPairWithSum(mat, sum):
    # hash to store elements
    s = set()

    # looping through elements
    # if present in the matrix
    # return true, else push
    # the element in matrix
    for i in range(N):
        for j in range(M):
            if (sum - mat[i][j]) in s :
                return True

            else :
                s.add(mat[i][j])

    return False

# Driver code
if __name__ == '__main__':

    # Input matrix
    mat = [[ 1, 2, 3, 4 ],
                    [ 5, 6, 7, 8] ,
                    [ 9, 10, 11, 12] ,
                    [13, 14, 15, 16]] 

    # given sum
    sum = 11

    if (isPairWithSum(mat, sum)) :
        print("YES")

    else:
        print("NO")

# This code is contributed by AbhiThakur
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check for pair with given sum

$N = 4;
$M = 4;

// Function to check if a pair with given sum
// exists in the matrix
function isPairWithSum(&$mat, $sum)
{
    global $N,$M;
    // array to store elements
    $s = array();

    // looping through elements
    // if present in the matrix
    // return true, else push
    // the element in matrix
    for ($i = 0; $i < $N; $i++) {
        for ($j = 0; $j < $M; $j++) {
            if (in_array($sum - $mat[$i][$j],$s) != end($s)) {
                return true;
            }
            else {
                array_push($s,$mat[$i][$j]);
            }
        }
    }

    return false;
}

// Driver code

    // Input matrix
    $mat = array(array( 1, 2, 3, 4 ),
                 array( 5, 6, 7, 8 ),
                 array( 9, 10, 11, 12 ),
                 array(13, 14, 15, 16 ));

    // given sum
    $sum = 11;

    if (isPairWithSum($mat, $sum)) {
        echo "YES" ."\n";
    }
    else
        echo "NO" ."\n";

    return 0;
?>
```

## java 描述语言

```
<script>
// Javascript code to check for pair
// with given sum

    // Function to check if a pair with
// given sum exists in the matrix
    let N = 4;
    let M = 4;

    function isPairWithSum(mat,sum)
    {
        // hash to store elements
    let s = new Set();

    // looping through elements
    // if present in the matrix
    // return true, else push
    // the element in matrix
    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < M; j++)
        {
            if (s.has(sum - mat[i][j]))
            {
                return true;
            }
            else
            {
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

    // given sum
    let sum = 11;

    if (isPairWithSum(mat, sum))
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