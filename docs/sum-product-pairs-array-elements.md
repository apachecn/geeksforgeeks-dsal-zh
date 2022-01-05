# 所有数组元素对的乘积之和

> 原文:[https://www . geesforgeks . org/sum-product-pairs-array-elements/](https://www.geeksforgeeks.org/sum-product-pairs-array-elements/)

给定一个整数数组 A[]求所有数组元素对的乘积之和，也就是说，我们需要在执行以下伪代码后求乘积之和

```
product = 0
for i = 1:n
    for j = i+1:n
        product = product + A[i]*A[j]
```

**示例:**

```
Input : A[] = {1, 3, 4}
Output : 19
Possible Pairs : (1,3), (1,4), (3,4)
Sum of Product : 1*3 + 1*4 + 3*4 = 19
```

## 天真的解决方案:

对于每个索引 I，我们循环遍历 j=i+1 到 j=n，每次添加 A[i]*A[j]。下面是相同的实现。

## C++

```
// A naive C++ program to find sum of product
#include <iostream>
using namespace std;

// Returns sum of pair products
int findProductSum(int A[], int n)
{
    int product = 0;
    for (int i = 0; i < n; i++)
        for (int j = i+1; j < n; j++)
            product = product + A[i]*A[j];
    return product;
}

// Driver code
int main()
{
    int A[] = {1, 3, 4};
    int n = sizeof(A)/sizeof(A[0]);

    cout << "sum of product of all pairs "
    "of array elements : " << findProductSum(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
// A naive Java program to find sum of product
import java.io.*;
class test
{
    // Returns sum of pair products
    int findProductSum(int A[], int n)
    {
    int product = 0;
    for (int i = 0; i < n; i++)
        for (int j = i+1; j < n; j++)
            product = product + A[i]*A[j];
    return product;
    }
}
class GFG {

// Driver code
    public static void main (String[] args) {

    int A[] = {1, 3, 4};
    int n = A.length;
    test t = new test();
    System.out.print("sum of product of all pairs of array elements : ");
    System.out.println(t.findProductSum(A, n));

    }
}
```

## 蟒蛇 3

```
# A naive python3 program to find sum of product

# Returns sum of pair products
def findProductSum(A,n):

    product = 0
    for i in range (n):
        for j in range ( i+1,n):
            product = product + A[i]*A[j]
    return product

# Driver code
if __name__=="__main__":

    A = [1, 3, 4]
    n = len (A)

    print("sum of product of all pairs "
    "of array elements : " ,findProductSum(A, n))
```

## C#

```
// A naive C# program to find sum of product
using System;

class GFG
{

// Returns sum of pair products
static int findProductSum(int[] A, int n)
{
    int product = 0;
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            product = product + A[i] * A[j];
    return product;
}

// Driver code
public static void Main()
{
    int[] A = {1, 3, 4};
    int n = A.Length;
    Console.WriteLine("sum of product of all " +
                      "pairs of array elements : ");
    Console.WriteLine(findProductSum(A, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive PHP program to find
// sum of product

// Returns sum of pair products
function findProductSum($A, $n)
{
    $product = 0;
    for ($i = 0; $i < $n; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            $product = $product + $A[$i] * $A[$j];
    return $product;
}

    // Driver code
    $A = array (1, 3, 4);
    $n = sizeof($A);

    echo "sum of product of all pairs ",
         "of array elements : "
         ,findProductSum($A, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// A naive Javascript program to find sum of product

// Returns sum of pair products
function findProductSum(A, n)
{
    let product = 0;
    for (let i= 0; i < n; i++)
        for (let j = i+1; j < n; j++)
            product = product + A[i]*A[j];
    return product;
}

// Driver code
    let A = [1, 3, 4];
    let n = A.length;

    document.write("sum of product of all pairs " +
    "of array elements : " + findProductSum(A, n));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
sum of product of all pairs of array elements : 19
```

**时间复杂度:**O(n<sup>2</sup>)
T5】空间复杂度: O(1)

## 高效的操作系统解决方案:

```
We know that
(a + b + c)2 = a2 + b2 + c2 + 2*(a*b + b*c + c*a)
Let required sum be P
Let E = (a1 + a2 + a3 + a4 ... + an)^2 
=> E = a12 + a22 + ... + an2 + 2*(a1*a2 + a1*a3 + ....)
=> E = a12 + a22 + ... + an2 + 2*(P)
=> P = ( E - (a12 + a22 + .... + an2) ) / 2
```

## C++

```
// Efficient C++ program to find sum pair products
// in an array.
#include <iostream>
using namespace std;

// required function
int findProductSum(int A[], int n)
{
    // calculating array sum (a1 + a2  ... + an)
    int array_sum = 0;
    for (int i = 0; i < n; i++)
        array_sum = array_sum + A[i];

    // calculating square of array sum
    // (a1 + a2 + ... + an)^2
    int array_sum_square = array_sum * array_sum;

    // calculating a1^2 + a2^2 + ... + an^2
    int individual_square_sum = 0;
    for (int i = 0; i < n; i++)
        individual_square_sum += A[i]*A[i];

    // required sum is (array_sum_square -
    // individual_square_sum) / 2
    return (array_sum_square - individual_square_sum)/2;
}

// Driver code
int main()
{
    int A[] = {1, 3, 4};
    int n = sizeof(A)/sizeof(A[0]);
    cout << "sum of product of all pairs of array "
            "elements : " << findProductSum(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find sum pair products
// in an array.
class GFG
{

// required function
static int findProductSum(int A[], int n)
{
    // calculating array sum (a1 + a2 ... + an)
    int array_sum = 0;
    for (int i = 0; i < n; i++)
        array_sum = array_sum + A[i];

    // calculating square of array sum
    // (a1 + a2 + ... + an)^2
    int array_sum_square = array_sum * array_sum;

    // calculating a1^2 + a2^2 + ... + an^2
    int individual_square_sum = 0;
    for (int i = 0; i < n; i++)
        individual_square_sum += A[i] * A[i];

    // required sum is (array_sum_square -
    // individual_square_sum) / 2
    return (array_sum_square - individual_square_sum) / 2;
}

// Driver code
public static void main(String[] args)
{
    int A[] = {1, 3, 4};
    int n = A.length;
    System.out.println("sum of product of all pairs of array "
            +"elements : " + findProductSum(A, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Efficient python 3 program to find sum
# pair products in an array.

# required function
def findProductSum(A, n):

    # calculating array sum (a1 + a2 ... + an)
    array_sum = 0
    for i in range(0, n, 1):
        array_sum = array_sum + A[i]

    # calculating square of array sum
    # (a1 + a2 + ... + an)^2
    array_sum_square = array_sum * array_sum

    # calculating a1^2 + a2^2 + ... + an^2
    individual_square_sum = 0
    for i in range(0, n, 1):
        individual_square_sum += A[i] * A[i]

    # required sum is (array_sum_square -
    # individual_square_sum) / 2
    return (array_sum_square -
            individual_square_sum) / 2

# Driver code
if __name__ == '__main__':
    A = [1, 3, 4]
    n = len(A)
    print("sum of product of all pairs of",
          "array elements :", int(findProductSum(A, n)))

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// Efficient C# program to find sum pair
// products in an array.
using System;

class GFG
{

// required function
static int findProductSum(int[] A, int n)
{
    // calculating array sum (a1 + a2 ... + an)
    int array_sum = 0;
    for (int i = 0; i < n; i++)
        array_sum = array_sum + A[i];

    // calculating square of array sum
    // (a1 + a2 + ... + an)^2
    int array_sum_square = array_sum * array_sum;

    // calculating a1^2 + a2^2 + ... + an^2
    int individual_square_sum = 0;
    for (int i = 0; i < n; i++)
        individual_square_sum += A[i] * A[i];

    // required sum is (array_sum_square -
    // individual_square_sum) / 2
    return (array_sum_square -
            individual_square_sum) / 2;
}

// Driver code
public static void Main()
{
    int[] A = {1, 3, 4};
    int n = A.Length;
    Console.WriteLine("sum of product of all " +
                      "pairs of array elements : " +
                       findProductSum(A, n));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find sum
// pair products in an array.

// required function
function findProductSum(&$A, $n)
{
    // calculating array sum (a1 + a2 ... + an)
    $array_sum = 0;
    for ($i = 0; $i < $n; $i++)
        $array_sum = $array_sum + $A[$i];

    // calculating square of array sum
    // (a1 + a2 + ... + an)^2
    $array_sum_square = $array_sum * $array_sum;

    // calculating a1^2 + a2^2 + ... + an^2
    $individual_square_sum = 0;
    for ($i = 0; $i < $n; $i++)
        $individual_square_sum += $A[$i] * $A[$i];

    // required sum is (array_sum_square -
    // individual_square_sum) / 2
    return ($array_sum_square -
            $individual_square_sum) / 2;
}

// Driver code
$A = array(1, 3, 4);
$n = sizeof($A);
echo("sum of product of all pairs " .
             "of array elements : ");
echo (findProductSum($A, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Efficient Javascript program to find sum pair
    // products in an array.

    // required function
    function findProductSum(A, n)
    {
        // calculating array sum (a1 + a2 ... + an)
        let array_sum = 0;
        for (let i = 0; i < n; i++)
            array_sum = array_sum + A[i];

        // calculating square of array sum
        // (a1 + a2 + ... + an)^2
        let array_sum_square = array_sum * array_sum;

        // calculating a1^2 + a2^2 + ... + an^2
        let individual_square_sum = 0;
        for (let i = 0; i < n; i++)
            individual_square_sum += A[i] * A[i];

        // required sum is (array_sum_square -
        // individual_square_sum) / 2
        return (array_sum_square - individual_square_sum) / 2;
    }

    let A = [1, 3, 4];
    let n = A.length;
    document.write("sum of product of all " +
                      "pairs of array elements : " +
                       findProductSum(A, n));

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
sum of product of all pairs of array elements : 19
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)
本文由 [**Pratik Chhajer**](https://github.com/pratik-chhajer) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。