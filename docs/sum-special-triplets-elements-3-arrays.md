# 具有来自 3 个数组的元素的特殊三元组的和

> 原文:[https://www . geesforgeks . org/sum-special-triples-elements-3-arrays/](https://www.geeksforgeeks.org/sum-special-triplets-elements-3-arrays/)

给定三个数组 A、B 和 C，任务是找出所有**特殊三元组**的值之和。特殊三元组定义为三元组(X，Y，Z)，其中条件:
**X ≤ Y 且 Z ≤ Y** 始终成立。每个三元组(X，Y，Z)的值由下式给出:

```
f(X, Y, Z) = (X + Y) * (Y + Z)
```

**注**:如果一个三元组不‘特殊’，则该特定三元组的 f(x，y，z) = 0。
**例:**

```
Input : A = {1, 4, 5}, B = {2, 3}, C = {2, 1, 3}
Output : 81
Explanation
The special triplets and their values are given below
Triplet      f(x, y, z) = (x + y) * (y + z)
(1, 2, 2)         (1 + 2) * (2 + 2)  = 12
(1, 2, 1)         (1 + 2) * (2 + 1)  =  9
(1, 3, 2)         (1 + 3) * (3 + 2)  = 20
(1, 3, 1)         (1 + 3) * (3 + 1)  = 16
(1, 3, 3)         (1 + 3) * (3 + 3)  = 24
-------------------------------------
                           Sum = 81
```

**方法 1(蛮力)**我们生成所有三元组并检查三元组是否是特殊三元组，我们使用 f(x，y，z)计算三元组的值，其中(x，y，z)是特殊三元组，并将其添加到所有这些特殊三元组的最终总和中

## C++

```
// C++ Program to find sum of values of
// all special triplets
#include <bits/stdc++.h>
using namespace std;

/* Finding special triplets (x, y, z) where
   x belongs to A; y belongs to B and z
   belongs to C; p, q and r are size of
   A, B and C respectively */
int findSplTripletsSum(int a[], int b[], int c[],
                             int p, int q, int r)
{

    int sum = 0;
    for (int i = 0; i < p; i++) {
        for (int j = 0; j < q; j++) {
            for (int k = 0; k < r; k++) {

                // (a[i], b[j], c[k]) is special if
                // a[i] <= b[j] and c[k] <= b[j];
                if (a[i] <= b[j] && c[k] <= b[j]) {

                    // calculate the value of this special
                    // triplet and add sum of all values
                    // of such triplets
                    sum +=  (a[i] + b[j]) * (b[j] + c[k]);
                }
            }
        }
    }
    return sum;
}

// Driver Code
int main()
{
    int A[] = { 1, 4, 5 };
    int B[] = { 2, 3 };
    int C[] = { 2, 1, 3 };

    int p = sizeof(A) / sizeof(A[0]);
    int q = sizeof(B) / sizeof(B[0]);
    int r = sizeof(C) / sizeof(C[0]);

    cout << "Sum of values of all special triplets = "
         << findSplTripletsSum(A, B, C, p, q, r) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of values of
// all special triplets
class GFG
{

/* Finding special triplets (x, y, z) where
x belongs to A; y belongs to B and z
belongs to C; p, q and r are size of
A, B and C respectively */
static int findSplTripletsSum(int a[], int b[], int c[],
                            int p, int q, int r)
{

    int sum = 0;
    for (int i = 0; i < p; i++)
    {
        for (int j = 0; j < q; j++)
        {
            for (int k = 0; k < r; k++)
            {

                // (a[i], b[j], c[k]) is special if
                // a[i] <= b[j] and c[k] <= b[j];
                if (a[i] <= b[j] && c[k] <= b[j])
                {

                    // calculate the value of this special
                    // triplet and add sum of all values
                    // of such triplets
                    sum += (a[i] + b[j]) * (b[j] + c[k]);
                }
            }
        }
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 4, 5 };
    int B[] = { 2, 3 };
    int C[] = { 2, 1, 3 };

    int p = A.length;
    int q = B.length;
    int r = C.length;

    System.out.print("Sum of values of all special triplets = "
                    + findSplTripletsSum(A, B, C, p, q, r) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to find sum of values of
# all special triplets

# Finding special triplets (x, y, z) where
# x belongs to A y belongs to B and z
# belongs to C p, q and r are size of
# A, B and C respectively
def findSplTripletsSum(a, b, c, p, q, r):
    summ = 0
    for i in range(p):
        for j in range(q):
            for k in range(r):

                # (a[i], b[j], c[k]) is special if
                # a[i] <= b[j] and c[k] <= b[j]
                if (a[i] <= b[j] and c[k] <= b[j]):

                    # calculate the value of this special
                    # triplet and add sum of all values
                    # of such triplets
                    summ += (a[i] + b[j]) * (b[j] + c[k])
    return summ

# Driver Code
A = [1, 4, 5 ]
B = [2, 3 ]
C = [2, 1, 3 ]

p = len(A)
q = len(B)
r = len(C)

print("Sum of values of all special triplets = ",
            findSplTripletsSum(A, B, C, p, q, r))

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# Program to find sum of values of
// all special triplets
using System;

class GFG
{

/* Finding special triplets (x, y, z) where
x belongs to A; y belongs to B and z
belongs to C; p, q and r are size of
A, B and C respectively */
static int findSplTripletsSum(int []a, int []b, int []c,
                            int p, int q, int r)
{

    int sum = 0;
    for (int i = 0; i < p; i++)
    {
        for (int j = 0; j < q; j++)
        {
            for (int k = 0; k < r; k++)
            {

                // (a[i], b[j], c[k]) is special if
                // a[i] <= b[j] and c[k] <= b[j];
                if (a[i] <= b[j] && c[k] <= b[j])
                {

                    // calculate the value of this special
                    // triplet and add sum of all values
                    // of such triplets
                    sum += (a[i] + b[j]) * (b[j] + c[k]);
                }
            }
        }
    }
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 1, 4, 5 };
    int []B = { 2, 3 };
    int []C = { 2, 1, 3 };

    int p = A.Length;
    int q = B.Length;
    int r = C.Length;

    Console.Write("Sum of values of all special triplets = "
                    + findSplTripletsSum(A, B, C, p, q, r) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript Program to find sum of values of
// all special triplets   
     /* Finding special triplets (x, y, z) where x belongs to A;
        y belongs to B and z  belongs to C; p, q and r are size
        of A, B and C respectively */
    function findSplTripletsSum(a , b , c , p , q , r) {

        var sum = 0;
        for (i = 0; i < p; i++) {
            for (j = 0; j < q; j++) {
                for (k = 0; k < r; k++) {

                    // (a[i], b[j], c[k]) is special if
                    // a[i] <= b[j] and c[k] <= b[j];
                    if (a[i] <= b[j] && c[k] <= b[j]) {

                        // calculate the value of this special
                        // triplet and add sum of all values
                        // of such triplets
                        sum += (a[i] + b[j]) * (b[j] + c[k]);
                    }
                }
            }
        }
        return sum;
    }

    // Driver Code

        var A = [ 1, 4, 5 ];
        var B = [ 2, 3 ];
        var C = [ 2, 1, 3 ];

        var p = A.length;
        var q = B.length;
        var r = C.length;

        document.write("Sum of values of all special triplets = "
        + findSplTripletsSum(A, B, C, p, q, r) + "\n");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Sum of values of all special triplets = 81
```