# 执行某些操作后从 D 可导出的数组元素数量

> 原文:[https://www . geeksforgeeks . org/数组元素数量-执行某些操作后可从 d 中导出/](https://www.geeksforgeeks.org/number-of-array-elements-derivable-from-d-after-performing-certain-operations/)

给定一个由 N 个整数和 3 个整数 D、A 和 b 组成的数组。任务是通过对 D 执行以下操作来找到我们可以将 D 转换成的数组元素的数量:

*   添加 A (+A)
*   减去 A (-A)
*   添加 B (+B)
*   减去 B (-B)

**注**:可以进行任意类型任意数量的操作。
**例:**

```
Input :  arr = {1, 2, 3}, D = 6, A = 3, B = 2 
Output :  3
Explanation: 
We can derive 1 from D by performing (6 - 3(A) - 2(B))
We can derive 2 from D by performing (6 - 2(A) - 2(A))
We can derive 3 from D by performing (6 - 3(A))
Thus, All array elements can be derived from D.

Input :  arr = {1, 2, 3}, D = 7, A = 4, B = 2 
Output :  2
Explanation: 
We can derive 1 from D by performing (7 - 4(A) - 2(B))
We can derive 3 from D by performing (7 - 4(A))
Thus, we can derive {1, 3}
```

假设我们要检查元素**a<sub>I</sub>T3 是否可以从 D:
中导出，假设我们执行:** 

*   类型 1 的操作(即添加 A) P 次。
*   类型 2 的运算(即减去 A) Q 次。
*   类型 3 的操作(即添加 B) R 次。
*   类型 4 的运算(即减去 B) S 次。

> 让我们在执行这些操作后得到的值为 X，那么，
> ->X = P * A–Q * A+R * B–S * B
> ->X =(P–Q)* A+(R–S)* B
> 假设我们成功地从 D 中导出了 A <sub>i</sub> ，即 X = | A<sub>I</sub>–D |，
> ->| A<sub>I</sub>–D | =(P–Q)* A+(R–S)* B
> 让(P–Q)=某个常数比如 U
> 同样让(R–S)为常数 V
> ->| A<sub>I</sub>–D | = U * A+V * B
> 这是以[线性丢番图方程](https://www.geeksforgeeks.org/linear-diophantine-equations/)的形式

因此，现在我们可以简单地迭代数组并计算所有这样的 A <sub>i</sub> ，其中| A<sub>I</sub>–D |可被 gcd(a，b)整除。
以下是上述方法的实施:

## C++

```
// CPP program to find the number of array elements
// which can be derived by perming (+A, -A, +B, -B)
// operations on D
#include <bits/stdc++.h>

using namespace std;

// Function to return
// gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

/* Function to Return the number of elements
   of arr[] which can be derived from D by
   performing (+A, -A, +B, -B) */
int findPossibleDerivables(int arr[], int n, int D,
                                      int A, int B)
{
    // find the gcd of A and B
    int gcdAB = gcd(A, B);

    // counter stores the number of
    // array elements which
    // can be derived from D
    int counter = 0;

    for (int i = 0; i < n; i++) {
        // arr[i] can be derived from D only if
        // |arr[i] - D| is divisible by gcd of A and B
        if ((abs(arr[i] - D) % gcdAB) == 0) {
            counter++;
        }
    }

    return counter;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 7, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int D = 5, A = 4, B = 2;
    cout << findPossibleDerivables(arr, n, D, A, B) <<"\n";

    int a[] = { 1, 2, 3 };
    n = sizeof(a) / sizeof(a[0]);
    D = 6, A = 3, B = 2;
    cout << findPossibleDerivables(a, n, D, A, B) <<"\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find the number of array elements
// which can be derived by perming (+A, -A, +B, -B)
// operations on D

import java.io.*;

class GFG {

// Function to return
// gcd of a and b
 static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

/* Function to Return the number of elements
of arr[] which can be derived from D by
performing (+A, -A, +B, -B) */
static int findPossibleDerivables(int arr[], int n, int D,
                                    int A, int B)
{
    // find the gcd of A and B
    int gcdAB = gcd(A, B);

    // counter stores the number of
    // array elements which
    // can be derived from D
    int counter = 0;

    for (int i = 0; i < n; i++) {
        // arr[i] can be derived from D only if
        // |arr[i] - D| is divisible by gcd of A and B
        if ((Math.abs(arr[i] - D) % gcdAB) == 0) {
            counter++;
        }
    }

    return counter;
}

// Driver Code

    public static void main (String[] args) {
            int arr[] = { 1, 2, 3, 4, 7, 13 };
    int n = arr.length;
    int D = 5, A = 4, B = 2;
    System.out.println( findPossibleDerivables(arr, n, D, A, B));

    int a[] = { 1, 2, 3 };
    n = a.length;
    D = 6;
    A = 3;
    B = 2;
    System.out.println( findPossibleDerivables(a, n, D, A, B));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find the number of array
# elements which can be derived by perming
# (+A, -A, +B, -B) operations on D

# Function to return gcd of a and b
def gcd(a, b) :

    if (a == 0) :
        return b

    return gcd(b % a, a);

""" Function to Return the number of elements
of arr[] which can be derived from D by
performing (+A, -A, +B, -B) """
def findPossibleDerivables(arr, n, D, A, B) :

    # find the gcd of A and B
    gcdAB = gcd(A, B)

    # counter stores the number of
    # array elements which
    # can be derived from D
    counter = 0

    for i in range(n) :

        # arr[i] can be derived from D only
        # if |arr[i] - D| is divisible by
        # gcd of A and B
        if ((abs(arr[i] - D) % gcdAB) == 0) :
            counter += 1

    return counter

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 7, 13 ]
    n = len(arr)
    D, A, B = 5, 4, 2

    print(findPossibleDerivables(arr, n, D, A, B))

    a = [ 1, 2, 3 ]
    n = len(a)
    D, A, B = 6, 3, 2

    print(findPossibleDerivables(a, n, D, A, B))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the number of array elements
// which can be derived by perming (+A, -A, +B, -B)
// operations on D
using System;   
public class GFG {

    // Function to return
    // gcd of a and b
     static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    /* Function to Return the number of elements
    of arr[] which can be derived from D by
    performing (+A, -A, +B, -B) */
    static int findPossibleDerivables(int []arr, int n, int D,
                                        int A, int B)
    {
        // find the gcd of A and B
        int gcdAB = gcd(A, B);

        // counter stores the number of
        // array elements which
        // can be derived from D
        int counter = 0;

        for (int i = 0; i < n; i++) {
            // arr[i] can be derived from D only if
            // |arr[i] - D| is divisible by gcd of A and B
            if ((Math.Abs(arr[i] - D) % gcdAB) == 0) {
                counter++;
            }
        }

        return counter;
    }

    // Driver Code

    public static void Main () {
            int []arr = { 1, 2, 3, 4, 7, 13 };
    int n = arr.Length;
    int D = 5, A = 4, B = 2;
    Console.WriteLine( findPossibleDerivables(arr, n, D, A, B));

    int []a = { 1, 2, 3 };
    n = a.Length;
    D = 6;
    A = 3;
    B = 2;
    Console.WriteLine( findPossibleDerivables(a, n, D, A, B));
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// array elements which can be derived by
// perming (+A, -A, +B, -B) operations on D

// Function to return gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

/* Function to Return the number of elements
of arr[] which can be derived from D by
performing (+A, -A, +B, -B) */

function findPossibleDerivables($arr, $n,
                                $D, $A, $B)
{
    // find the gcd of A and B
    $gcdAB = gcd($A, $B);

    // counter stores the number of
    // array elements which
    // can be derived from D
    $counter = 0;

    for ($i = 0; $i < $n; $i++)
    {
        // arr[i] can be derived from D only
        // if |arr[i] - D| is divisible by
        // gcd of A and B
        if ((abs($arr[$i] - $D) % $gcdAB) == 0)
        {
            $counter++;
        }
    }

    return $counter;
}

// Driver Code
$arr = array( 1, 2, 3, 4, 7, 13 );
$n = sizeof($arr);
$D = 5;
$A = 4;
$B = 2;
echo findPossibleDerivables($arr, $n,
                            $D, $A, $B), "\n";

$a = array( 1, 2, 3 );
$n = sizeof($a);
$D = 6;
$A = 3;
$B = 2;
echo findPossibleDerivables($arr, $n,
                            $D, $A, $B), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// javascript  program to find the number of array elements
// which can be derived by perming (+A, -A, +B, -B)
// operations on D   

// Function to return
    // gcd of a and b
    function gcd(a , b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    /*
     * Function to Return the number of elements of arr which can be derived from
     * D by performing (+A, -A, +B, -B)
     */
    function findPossibleDerivables(arr , n , D , A , B) {
        // find the gcd of A and B
        var gcdAB = gcd(A, B);

        // counter stores the number of
        // array elements which
        // can be derived from D
        var counter = 0;

        for (i = 0; i < n; i++)
        {

            // arr[i] can be derived from D only if
            // |arr[i] - D| is divisible by gcd of A and B
            if ((Math.abs(arr[i] - D) % gcdAB) == 0) {
                counter++;
            }
        }

        return counter;
    }

    // Driver Code
        var arr = [ 1, 2, 3, 4, 7, 13 ];
        var n = arr.length;
        var D = 5, A = 4, B = 2;
        document.write(findPossibleDerivables(arr, n, D, A, B)+"<br/>");

        var a = [ 1, 2, 3 ];
        n = a.length;
        D = 6;
        A = 3;
        B = 2;
        document.write(findPossibleDerivables(a, n, D, A, B));

// This code is contributed by todaysgaurav.
</script>
```

**Output:** 

```
4
3
```

**时间复杂度:** O(N)，其中 N 为数组元素个数。
**辅助空间** : O(log(max(A，B))。