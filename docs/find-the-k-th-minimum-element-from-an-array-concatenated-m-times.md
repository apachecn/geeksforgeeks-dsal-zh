# 从串联 M 次的数组中找到第 K 个最小元素

> 原文:[https://www . geeksforgeeks . org/find-the-k-th-最小数组元素-串联-m-times/](https://www.geeksforgeeks.org/find-the-k-th-minimum-element-from-an-array-concatenated-m-times/)

给定一个数组 arr[]和两个整数 **K** 和 **M** 。问题是在将数组连接到自身 **M 次**后找到**第 K 个最小元素**。
**举例:**

```
Input  : arr[] = {3, 1, 2}, K = 4, M = 3 
Output : 4'th Minimum element is : 2
Explanation: Concatenate array 3 times (ie., M = 3)
              arr[] = [3, 1, 2, 3, 1, 2, 3, 1, 2]
              arr[] = [1, 1, 1, 2, 2, 2, 3, 3, 3]
              Now 4'th Minimum element is 2

Input  : arr[] = {1, 13, 9, 17, 1, 12}, K = 19, M = 7 
Output : 19'th Minimum element is : 9
```

**简单方法:**

1.  将给定的数组添加到一个向量或任何其他数组中，比如 V，表示 **M** 次。
2.  将向量或数组 **V** 按升序排序。
3.  返回向量 **V** 的索引 **( K-1 )** 处的值，即返回**V【K–1】。**

以下是上述方法的实现:

## C++

```
// C++ programme to find the K'th minimum
// element from an array concatenated M times

#include <bits/stdc++.h>
using namespace std;

// Function to find the K-th minimum element
// from an array concatenated M times
int KthMinValAfterMconcatenate(int A[], int N,
                                 int M, int K)
{
    vector<int> V;

    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            V.push_back(A[j]);
        }
    }

    // sort the elements in ascending order
    sort(V.begin(), V.end());

    // return K'th Min element
    // present at K-1 index
    return (V[K - 1]);
}

// Driver Code
int main()
{
    int A[] = { 3, 1, 2 };

    int M = 3, K = 4;
    int N = sizeof(A) / sizeof(A[0]);

    cout << KthMinValAfterMconcatenate(A, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.ArrayList;
import java.util.Collections;

// Java programme to find the K'th minimum
// element from an array concatenated M times
class GFG
{

    // Function to find the K-th minimum element
    // from an array concatenated M times
    static int KthMinValAfterMconcatenate(int[] A, int N,
            int M, int K)
    {
        ArrayList V = new ArrayList();

        for (int i = 0; i < M; i++)
        {
            for (int j = 0; j < N; j++)
            {
                V.add(A[j]);
            }
        }

        // sort the elements in ascending order
        Collections.sort(V);

        // return K'th Min element
        // present at K-1 index
        return ((int) V.get(K - 1));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] A = {3, 1, 2};
        int M = 3, K = 4;
        int N = A.length;
        System.out.println(KthMinValAfterMconcatenate(A, N, M, K));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find the K'th minimum 
# element from an array concatenated M times

# Function to find the K-th minimum element 
# from an array concatenated M times
def KthMinValAfterMconcatenate(A, N, M, K):

    V = []

    for i in range(0, M): 
        for j in range(0, N): 
            V.append(A[j])

    # sort the elements in ascending order
    V.sort()

    # return K'th Min element
    # present at K-1 index
    return V[K - 1]

# Driver Code
if __name__ == "__main__":

    A = [3, 1, 2] 

    M, K = 3, 4
    N = len(A)

    print(KthMinValAfterMconcatenate(A, N, M, K))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# programme to find the K'th minimum
// element from an array concatenated M times
using System;
using System.Collections;

class GFG
{

// Function to find the K-th minimum element
// from an array concatenated M times
static int KthMinValAfterMconcatenate(int []A, int N,
                                int M, int K)
{
    ArrayList V=new ArrayList();

    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
        {
            V.Add(A[j]);
        }
    }

    // sort the elements in ascending order
    V.Sort();

    // return K'th Min element
    // present at K-1 index
    return ((int)V[K - 1]);
}

// Driver Code
static void Main()
{
    int []A = { 3, 1, 2 };

    int M = 3, K = 4;
    int N = A.Length;

    Console.WriteLine(KthMinValAfterMconcatenate(A, N, M, K));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP programme to find the K'th minimum
// element from an array concatenated M times

// Function to find the K-th minimum element
// from an array concatenated M times
function KthMinValAfterMconcatenate($A, $N,
                                    $M, $K)
{
    $V = array();

    for ($i = 0; $i < $M; $i++)
    {
        for ($j = 0; $j < $N; $j++)
        {
            array_push($V, $A[$j]);
        }
    }

    // sort the elements in ascending order
    sort($V);

    // return K'th Min element
    // present at K-1 index
    return ($V[$K - 1]);
}

// Driver Code
$A = array( 3, 1, 2 );

$M = 3;
$K = 4;
$N = count($A);

echo KthMinValAfterMconcatenate($A, $N, $M, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript programme to find the K'th minimum
// element from an array concatenated M times

// Function to find the K-th minimum element
// from an array concatenated M times
function KthMinValAfterMconcatenate(A, N, M, K)
{
    var V = [];

    for (var i = 0; i < M; i++) {
        for (var j = 0; j < N; j++) {
            V.push(A[j]);
        }
    }

    // sort the elements in ascending order
    V.sort();

    // return K'th Min element
    // present at K-1 index
    return (V[K - 1]);
}

// Driver Code
var A = [3, 1, 2];
var M = 3, K = 4;
var N = A.length;
document.write( KthMinValAfterMconcatenate(A, N, M, K));

</script>
```

**Output:** 

```
2
```

**有效方法:**如果 M 的值很小，上述方法可以很好地工作，但是对于
来说，M 的值很大，会产生内存错误或超时错误。
想法是观察给定数组排序后，当我们将它串联 M 次并再次排序时，每个元素现在都会在新的串联数组中出现 M 次。所以，

1.  给定数组按升序排序。
2.  返回给定数组 ie 的索引 **( (K-1) / M )** 处的值。，返回 **arr[((K-1) / M)]。**

以下是上述方法的实现:

## C++

```
// C++ programme to find the K'th minimum element
// from an array concatenated M times

#include <bits/stdc++.h>
using namespace std;

// Function to find the K-th minimum element
// from an array concatenated M times
int KthMinValAfterMconcatenate(int A[], int N,
                                  int M, int K)
{
    // Sort the elements in
    // ascending order
    sort(A, A + N);

    // Return the K'th Min element
    // present at ( (K-1) / M ) index
    return (A[((K - 1) / M)]);
}

// Driver Code
int main()
{
    int A[] = { 3, 1, 2 };

    int M = 3, K = 4;
    int N = sizeof(A) / sizeof(A[0]);

    cout << KthMinValAfterMconcatenate(A, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java programme to find the K'th minimum element
// from an array concatenated M times
import java.util.*;

class GFG1
{

    // Function to find the K-th minimum element
    // from an array concatenated M times
    static int KthMinValAfterMconcatenate(int[] A, int N,
                                            int M, int K)
    {
        // Sort the elements in
        // ascending order
        Arrays.sort(A);

        // Return the K'th Min element
        // present at ( (K-1) / M ) index
        return (A[((K - 1) / M)]);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] A = {3, 1, 2};

        int M = 3, K = 4;
        int N = A.length;

        System.out.println(KthMinValAfterMconcatenate(A, N, M, K));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the K'th minimum
# element from an array concatenated M times

# Function to find the K-th minimum element
# from an array concatenated M times
def KthMinValAfterMconcatenate(A, N, M, K):

    V = []

    for i in range(0, M):
        for j in range(0, N):
            V.append(A[j])

    # sort the elements in ascending order
    V.sort()

    # return K'th Min element
    # present at K-1 index
    return V[K - 1]

# Driver Code
if __name__ == "__main__":

    A = [3, 1, 2]

    M, K = 3, 4
    N = len(A)

    print(KthMinValAfterMconcatenate(A, N, M, K))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# programme to find the K'th minimum element
// from an array concatenated M times
using System;

class GFG
{

// Function to find the K-th minimum element
// from an array concatenated M times
static int KthMinValAfterMconcatenate(int []A, int N,
                                int M, int K)
{
    // Sort the elements in
    // ascending order
    Array.Sort(A);

    // Return the K'th Min element
    // present at ( (K-1) / M ) index
    return (A[((K - 1) / M)]);
}

// Driver Code
static void Main()
{
    int []A = { 3, 1, 2 };

    int M = 3, K = 4;
    int N = A.Length;

    Console.WriteLine(KthMinValAfterMconcatenate(A, N, M, K));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP programme to find the K'th minimum element
// from an array concatenated M times

// Function to find the K-th minimum element
// from an array concatenated M times
function KthMinValAfterMconcatenate($A, $N, $M, $K)
{
    // Sort the elements in
    // ascending order
    sort($A);

    // Return the K'th Min element
    // present at ( (K-1) / M ) index
    return ($A[(($K - 1) / $M)]);
}

// Driver Code
$A = array(3, 1, 2);

$M = 3; $K = 4;
$N = sizeof($A);

echo(KthMinValAfterMconcatenate($A, $N, $M, $K));

// This code contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript programme to find the K'th minimum element
// from an array concatenated M times

// Function to find the K-th minimum element
// from an array concatenated M times
function KthMinValAfterMconcatenate(A,  N, M,  K)
{
    // Sort the elements in
    // ascending order
    A.sort((a,b)=>a-b)

    // Return the K'th Min element
    // present at ( (K-1) / M ) index
    return (A[((K - 1) / M)]);
}

// Driver Code
var A = [3, 1, 2 ];
var M = 3, K = 4;
var N = A.length;
document.write( KthMinValAfterMconcatenate(A, N, M, K));

</script>
```

**Output:** 

```
2
```