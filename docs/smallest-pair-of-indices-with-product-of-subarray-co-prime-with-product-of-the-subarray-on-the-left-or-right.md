# 子阵列乘积与左侧或右侧子阵列乘积同素的最小指数对

> 原文:[https://www . geeksforgeeks . org/最小对子阵积指数-左或右子阵积同素/](https://www.geeksforgeeks.org/smallest-pair-of-indices-with-product-of-subarray-co-prime-with-product-of-the-subarray-on-the-left-or-right/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到最小的一对索引 **(i，j)** ，使得子阵列**arr【I+1，j–1】**中元素的乘积与子阵列**arr【0，I】**或子阵列**arr【j，N】的乘积同素如果不存在这样的配对，打印【T16 "-" 1 "**。

**示例:**

> **输入:** arr[] = {2，4，1，3，7}
> **输出:** (0，2)
> **说明:**子阵{arr[1]，arr[1]}的乘积为 4。右子阵的乘积= 1 * 3 * 7 = 21。由于 4 和 21 是同素的，那么打印范围(0，2)作为答案。
> 
> **输入:** arr[] = {21，3，11，7，18}
> **输出:** (1，3)
> **说明:**子阵{arr[1]，arr[2]}的乘积为 11。右子阵的乘积是 7 * 18 = 126。由于 11 和 126 是同素的，那么打印范围(1，3)作为答案。

**天真方法:**最简单的方法是遍历每一对可能的索引 **(i，j)** ，对于每一对，找到子阵列**arr【0，I】**和**arr【j，N】**的乘积，并检查它是否与子阵列**arr【I+1，j–1】**的乘积同素。如果发现是真的，那就打印那对索引。如果不存在这样的配对，则打印【T10 "-" 1 "。

***时间复杂度:** O((N <sup>3</sup> )*log(M))，其中 **M** 是数组所有元素的乘积。*
***辅助空间:** O(1)*

**高效方式:**对上述方式进行优化，思路是使用一个辅助数组来存储数组元素的[后缀积](https://www.geeksforgeeks.org/prefix-product-array/)。按照以下步骤解决问题:

*   将后缀元素的乘积存储在 **rightProd[]** 中，其中 **rightProd[i]** 存储来自 **arr[i]、arr[N–1]**的元素的乘积。
*   [求数组中所有元素的乘积](https://www.geeksforgeeks.org/program-for-product-of-array/)为 **totalProd。**
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下操作:
    *   初始化一个变量，说**积**。
    *   [使用范围**【I，N–1】**中的变量 **j** 迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)。
    *   通过将**产品**乘以**arr【j】**更新**产品**。
    *   将**左产品**初始化为**总/右产品【I】**。
    *   检查产品是否与**左侧产品**或**右侧产品**之一共灌注。如果发现是真的，则打印配对**(I–1，j + 1)** 和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果不存在这样的配对，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD
// of two integers
int gcd(int a, int b)
{
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to find the lexicographically
// smallest pair of indices whose product
// is co-prime with the product of the
// subarrays on its left and right
void findPair(int A[], int N)
{
    // Stores the suffix product
    // of array elements
    int right_prod[N];

    // Set 0/1 if pair satisfies the
    // given condition or not
    int flag = 0;

    // Initialize array right_prod[]
    right_prod[N - 1] = A[N - 1];

    // Update the suffix product
    for (int i = N - 2; i >= 0; i--)
        right_prod[i] = right_prod[i + 1]
                        * A[i];

    // Stores product of all elements
    int total_prod = right_prod[0];

    // Stores the product of subarray
    // in between the pair of indices
    int product;

    // Iterate through every pair of
    // indices (i, j)
    for (int i = 1; i < N - 1; i++) {

        product = 1;
        for (int j = i; j < N - 1; j++) {

            // Store product of A[i, j]
            product *= A[j];

            // Check if product is co-prime
            // to product of either the left
            // or right subarrays
            if (gcd(product,
                    right_prod[j + 1])
                    == 1
                || gcd(product,
                       total_prod
                           / right_prod[i])
                       == 1) {

                flag = 1;
                cout << "(" << i - 1
                     << ", " << j + 1
                     << ")";
                break;
            }
        }
        if (flag == 1)
            break;
    }

    // If no such pair is found,
    // then print -1
    if (flag == 0)
        cout << -1;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 1, 3, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findPair(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate GCD
// of two integers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to find the lexicographically
// smallest pair of indices whose product
// is co-prime with the product of the
// subarrays on its left and right
static void findPair(int A[], int N)
{

    // Stores the suffix product
    // of array elements
    int right_prod[] = new int[N];

    // Set 0/1 if pair satisfies the
    // given condition or not
    int flag = 0;

    // Initialize array right_prod[]
    right_prod[N - 1] = A[N - 1];

    // Update the suffix product
    for(int i = N - 2; i >= 0; i--)
        right_prod[i] = right_prod[i + 1] * A[i];

    // Stores product of all elements
    int total_prod = right_prod[0];

    // Stores the product of subarray
    // in between the pair of indices
    int product;

    // Iterate through every pair of
    // indices (i, j)
    for(int i = 1; i < N - 1; i++)
    {
        product = 1;
        for(int j = i; j < N - 1; j++)
        {

            // Store product of A[i, j]
            product *= A[j];

            // Check if product is co-prime
            // to product of either the left
            // or right subarrays
            if (gcd(product, right_prod[j + 1]) == 1 ||
                gcd(product, total_prod /
                    right_prod[i]) == 1)
            {
                flag = 1;
                System.out.println("(" + (i - 1) + ", " +
                                         (j + 1) + ")");
                break;
            }
        }

        if (flag == 1)
            break;
    }

    // If no such pair is found,
    // then print -1
    if (flag == 0)
        System.out.print(-1);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 1, 3, 7 };
    int N = arr.length;

    // Function Call
    findPair(arr, N);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate GCD
# of two integers
def gcd(a, b):

    if (b == 0):
        return a

    # Recursively calculate GCD
    return gcd(b, a % b)

# Function to find the lexicographically
# smallest pair of indices whose product
# is co-prime with the product of the
# subarrays on its left and right
def findPair(A, N):

    # Stores the suffix product
    # of array elements
    right_prod = [0] * N

    # Set 0/1 if pair satisfies the
    # given condition or not
    flag = 0

    # Initialize array right_prod
    right_prod[N - 1] = A[N - 1]

    # Update the suffix product
    for i in range(N - 2, 0, -1):
        right_prod[i] = right_prod[i + 1] * A[i]

    # Stores product of all elements
    total_prod = right_prod[0]

    # Stores the product of subarray
    # in between the pair of indices
    product = 1

    # Iterate through every pair of
    # indices (i, j)
    for i in range(1, N - 1):
        product = 1
        for j in range(i, N - 1):

            # Store product of A[i, j]
            product *= A[j]

            # Check if product is co-prime
            # to product of either the left
            # or right subarrays
            if (gcd(product, right_prod[j + 1]) == 1 or
                gcd(product, total_prod /
                             right_prod[i]) == 1):
                flag = 1
                print("(" , (i - 1) , ", " ,
                            (j + 1) ,")")
                break

        if (flag == 1):
            break

    # If no such pair is found,
    # then pr-1
    if (flag == 0):
        print(-1)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 4, 1, 3, 7 ]
    N = len(arr)

    # Function Call
    findPair(arr, N)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate GCD
// of two integers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to find the lexicographically
// smallest pair of indices whose product
// is co-prime with the product of the
// subarrays on its left and right
static void findPair(int []A, int N)
{

    // Stores the suffix product
    // of array elements
    int []right_prod = new int[N];

    // Set 0/1 if pair satisfies the
    // given condition or not
    int flag = 0;

    // Initialize array right_prod[]
    right_prod[N - 1] = A[N - 1];

    // Update the suffix product
    for(int i = N - 2; i >= 0; i--)
        right_prod[i] = right_prod[i + 1] * A[i];

    // Stores product of all elements
    int total_prod = right_prod[0];

    // Stores the product of subarray
    // in between the pair of indices
    int product;

    // Iterate through every pair of
    // indices (i, j)
    for(int i = 1; i < N - 1; i++)
    {
        product = 1;

        for(int j = i; j < N - 1; j++)
        {

            // Store product of A[i, j]
            product *= A[j];

            // Check if product is co-prime
            // to product of either the left
            // or right subarrays
            if (gcd(product, right_prod[j + 1]) == 1 ||
                gcd(product, total_prod /
                    right_prod[i]) == 1)
            {
                flag = 1;
                Console.WriteLine("(" + (i - 1) + ", " +
                                        (j + 1) + ")");
                break;
            }
        }

        if (flag == 1)
            break;
    }

    // If no such pair is found,
    // then print -1
    if (flag == 0)
        Console.Write(-1);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 4, 1, 3, 7 };
    int N = arr.Length;

    // Function Call
    findPair(arr, N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate GCD
// of two integers
function gcd(a, b)
{
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to find the lexicographically
// smallest pair of indices whose product
// is co-prime with the product of the
// subarrays on its left and right
function findPair(A, N)
{

    // Stores the suffix product
    // of array elements
    let right_prod = [];

    // Set 0/1 if pair satisfies the
    // given condition or not
    let flag = 0;

    // Initialize array right_prod[]
    right_prod[N - 1] = A[N - 1];

    // Update the suffix product
    for(let i = N - 2; i >= 0; i--)
        right_prod[i] = right_prod[i + 1] * A[i];

    // Stores product of all elements
    let total_prod = right_prod[0];

    // Stores the product of subarray
    // in between the pair of indices
    let product;

    // Iterate through every pair of
    // indices (i, j)
    for(let i = 1; i < N - 1; i++)
    {
        product = 1;
        for(let j = i; j < N - 1; j++)
        {

            // Store product of A[i, j]
            product *= A[j];

            // Check if product is co-prime
            // to product of either the left
            // or right subarrays
            if (gcd(product, right_prod[j + 1]) == 1 ||
                gcd(product, total_prod /
                    right_prod[i]) == 1)
            {
                flag = 1;
                document.write("(" + (i - 1) + ", " +
                                     (j + 1) + ")");
                break;
            }
        }

        if (flag == 1)
            break;
    }

    // If no such pair is found,
    // then prlet -1
    if (flag == 0)
        document.write(-1);
}

// Driver code
let arr = [ 2, 4, 1, 3, 7 ];
let N = arr.length;

// Function Call
findPair(arr, N);

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
(0, 2)
```

***时间复杂度:** O(N <sup>2</sup> *log(M))，其中 M 是数组中所有元素的乘积*
***辅助空间:** O(N)*