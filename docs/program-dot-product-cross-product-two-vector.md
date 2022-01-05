# 两个向量的点积和叉积程序

> 原文:[https://www . geesforgeks . org/program-dot-product-cross-product-two-vector/](https://www.geeksforgeeks.org/program-dot-product-cross-product-two-vector/)

有两个向量 **A** 和 **B** ，我们要求两个向量数组的点积和叉积。点积也称为标量积，叉积也称为向量积。
**点积–**让我们给出两个向量 **A** = a1 * i + a2 * j + a3 * k 和 **B** = b1 * i + b2 * j + b3 * k，其中 I、j 和 k 是沿 x、y 和 z 方向的单位向量。那么点积计算为点积= a1 * b1 + a2 * b2 + a3 * b3
**例–**

```
A = 3 * i + 5 * j + 4 * k
B = 2 * i + 7 * j + 5 * k
dot product = 3 * 2 + 5 * 7 + 4 * 5
            = 6 + 35 + 20
            = 61
```

**叉积–**假设我们已经给出了两个向量 **A** = a1 * i + a2 * j + a3 * k 和 **B** = b1 * i + b2 * j + b3 * k，那么叉积计算为叉积=(a2 * B3–a3 * B2)* I+(a3 * B1–a1 * B3)* j+(a1 * B2–a2 * B1)* k， 其中[(a2 * B3–a3 * B2)，(a3 * B1–a1 * B3)，(a1 * B2–a2 * B1)]是沿 I、j 和 k 方向的单位向量的系数。
**示例–**

```
A = 3 * i + 5 * j + 4 * k
B = 2 * i + 7 * j + 5 * k
cross product 
= (5 * 5 - 4 * 7) * i 
      + (4 * 2 - 3 * 5) * j + (3 * 7 - 5 * 2) * k
= (-3)*i + (-7)*j + (11)*k
```

**示例–**

```
Input: vect_A[] = {3, -5, 4}
        vect_B[] = {2, 6, 5}
Output: Dot product: -4
         Cross product = -49 -7 28
```

**代码-**

## C++

```
// C++ implementation for dot product
// and cross product of two vector.
#include <bits/stdc++.h>
#define n 3

using namespace std;

// Function that return
// dot product of two vector array.
int dotProduct(int vect_A[], int vect_B[])
{

    int product = 0;

    // Loop for calculate cot product
    for (int i = 0; i < n; i++)

        product = product + vect_A[i] * vect_B[i];
    return product;
}

// Function to find
// cross product of two vector array.
void crossProduct(int vect_A[], int vect_B[], int cross_P[])

{

    cross_P[0] = vect_A[1] * vect_B[2] - vect_A[2] * vect_B[1];
    cross_P[1] = vect_A[2] * vect_B[0] - vect_A[0] * vect_B[2];
    cross_P[2] = vect_A[0] * vect_B[1] - vect_A[1] * vect_B[0];
}

// Driver function
int main()
{

    int vect_A[] = { 3, -5, 4 };
    int vect_B[] = { 2, 6, 5 };
    int cross_P[n];

    // dotProduct function call
    cout << "Dot product:";
    cout << dotProduct(vect_A, vect_B) << endl;

    // crossProduct function call
    cout << "Cross product:";
    crossProduct(vect_A, vect_B, cross_P);

    // Loop that print
    // cross product of two vector array.
    for (int i = 0; i < n; i++)

        cout << cross_P[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation for dot product
// and cross product of two vector.
import java.io.*;

class GFG {

    static int n = 3;

    // Function that return
    // dot product of two vector array.
    static int dotProduct(int vect_A[], int vect_B[])
    {

        int product = 0;

        // Loop for calculate cot product
        for (int i = 0; i < n; i++)
            product = product + vect_A[i] * vect_B[i];
        return product;
    }

    // Function to find
    // cross product of two vector array.
    static void crossProduct(int vect_A[], int vect_B[],
                             int cross_P[])

    {

        cross_P[0] = vect_A[1] * vect_B[2]
                     - vect_A[2] * vect_B[1];
        cross_P[1] = vect_A[2] * vect_B[0]
                     - vect_A[0] * vect_B[2];
        cross_P[2] = vect_A[0] * vect_B[1]
                     - vect_A[1] * vect_B[0];
    }

    // Driver code
    public static void main(String[] args)
    {
        int vect_A[] = { 3, -5, 4 };
        int vect_B[] = { 2, 6, 5 };
        int cross_P[] = new int[n];

        // dotProduct function call
        System.out.print("Dot product:");
        System.out.println(dotProduct(vect_A, vect_B));

        // crossProduct function call
        System.out.print("Cross product:");
        crossProduct(vect_A, vect_B, cross_P);

        // Loop that print
        // cross product of two vector array.
        for (int i = 0; i < n; i++)

            System.out.print(cross_P[i] + " ");
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 implementation for dot product
# and cross product of two vector.

n = 3

# Function that return
# dot product of two vector array.
def dotProduct(vect_A, vect_B):

    product = 0

    # Loop for calculate cot product
    for i in range(0, n):
        product = product + vect_A[i] * vect_B[i]

    return product

# Function to find
# cross product of two vector array.
def crossProduct(vect_A, vect_B, cross_P):

    cross_P.append(vect_A[1] * vect_B[2] - vect_A[2] * vect_B[1])
    cross_P.append(vect_A[2] * vect_B[0] - vect_A[0] * vect_B[2])
    cross_P.append(vect_A[0] * vect_B[1] - vect_A[1] * vect_B[0])

# Driver function
if __name__=='__main__':
    vect_A = [3, -5, 4]
    vect_B = [2, 6, 5]
    cross_P = []

# dotProduct function call
    print("Dot product:", end =" ")
    print(dotProduct(vect_A, vect_B))

# crossProduct function call
    print("Cross product:", end =" ")
    crossProduct(vect_A, vect_B, cross_P)

# Loop that print
# cross product of two vector array.
    for i in range(0, n):
        print(cross_P[i], end =" ")

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation for dot product
// and cross product of two vector.
using System;

class GFG {

    static int n = 3;

    // Function that return dot
    // product of two vector array.
    static int dotProduct(int[] vect_A,
                          int[] vect_B)
    {

        int product = 0;

        // Loop for calculate cot product
        for (int i = 0; i < n; i++)
            product = product + vect_A[i] * vect_B[i];
        return product;
    }

    // Function to find cross product
    // of two vector array.
    static void crossProduct(int[] vect_A,
                             int[] vect_B, int[] cross_P)

    {

        cross_P[0] = vect_A[1] * vect_B[2]
                     - vect_A[2] * vect_B[1];
        cross_P[1] = vect_A[2] * vect_B[0]
                     - vect_A[0] * vect_B[2];
        cross_P[2] = vect_A[0] * vect_B[1]
                     - vect_A[1] * vect_B[0];
    }

    // Driver code
    public static void Main()
    {
        int[] vect_A = { 3, -5, 4 };
        int[] vect_B = { 2, 6, 5 };
        int[] cross_P = new int[n];

        // dotProduct function call
        Console.Write("Dot product:");

        Console.WriteLine(
            dotProduct(vect_A, vect_B));

        // crossProduct function call
        Console.Write("Cross product:");
        crossProduct(vect_A, vect_B, cross_P);

        // Loop that print
        // cross product of two vector array.
        for (int i = 0; i < n; i++)
            Console.Write(cross_P[i] + " ");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation for dot
// product and cross product
// of two vector.
$n = 3;

// Function that return
// dot product of two
// vector array.
function dotproduct($vect_A, $vect_B)
{
    global $n;
    $product = 0;

    // Loop for calculate
    // cot product
    for ($i = 0; $i < $n; $i++)

        $product = $product + $vect_A[$i] *
                            $vect_B[$i];
    return $product;
}

// Function to find
// cross product of
// two vector array.
function crossproduct($vect_A,
                    $vect_B, $cross_P)

{

    $cross_P[0] = $vect_A[1] * $vect_B[2] -
                $vect_A[2] * $vect_B[1];
    $cross_P[1] = $vect_A[2] * $vect_B[0] -
                $vect_A[0] * $vect_B[2];
    $cross_P[2] = $vect_A[0] * $vect_B[1] -
                $vect_A[1] * $vect_B[0];
    return $cross_P;
}

// Driver Code
$vect_A = array( 3, -5, 4 );
$vect_B = array( 2, 6, 5 );
$cross_P = array_fill(0, $n, 0);

// dotproduct function call
echo "Dot product:";
echo dotproduct($vect_A, $vect_B);

// crossproduct function call
echo "\nCross product:";
$cross_P = crossproduct($vect_A,
                        $vect_B,
                        $cross_P);

// Loop that print
// cross product of
// two vector array.
for ($i = 0; $i < $n; $i++)

    echo $cross_P[$i] . " ";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation for dot product
// and cross product of two vector.

let n = 3;

    // Function that return
    // dot product of two vector array.
    function dotProduct(vect_A, vect_B)
    {

        let product = 0;

        // Loop for calculate cot product
        for (let i = 0; i < n; i++)
            product = product + vect_A[i] * vect_B[i];
        return product;
    }

    // Function to find
    // cross product of two vector array.
    function crossProduct(vect_A, vect_B,
                             cross_P)

    {

        cross_P[0] = vect_A[1] * vect_B[2]
                     - vect_A[2] * vect_B[1];
        cross_P[1] = vect_A[2] * vect_B[0]
                     - vect_A[0] * vect_B[2];
        cross_P[2] = vect_A[0] * vect_B[1]
                     - vect_A[1] * vect_B[0];
    }

// Driver code

        let vect_A = [ 3, -5, 4 ];
        let vect_B = [ 2, 6, 5 ];
        let cross_P = [];

        // dotProduct function call
        document.write("Dot product:");
        document.write(dotProduct(vect_A, vect_B) + "<br/>");

        // crossProduct function call
        document.write("Cross product:");
        crossProduct(vect_A, vect_B, cross_P);

        // Loop that prlet
        // cross product of two vector array.
        for (let i = 0; i < n; i++)

            document.write(cross_P[i] + " ");

       // This code is contributed by sanjoy_62.            
</script>
```

**Output:** 

```
Dot product:-4
Cross product:-49 -7 28
```

本文由 [**达曼德拉·库马尔**](https://auth.geeksforgeeks.org/profile.php?user=dharammnnit) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。