# 数组中元素的二进制表示中出现的集合位的计数乘积

> 原文:[https://www . geeksforgeeks . org/数组中元素的二进制表示的位数乘积/](https://www.geeksforgeeks.org/product-of-count-of-set-bits-present-in-binary-representations-of-elements-in-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在每个数组元素的[二进制表示中找到设置位](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)的[计数的乘积。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

**示例:**

> **输入:** arr[] = {3，2，4，1，5}
> **输出:** 4
> **解释:**
> 数组元素的二进制表示分别为{3，2，4，1，5}分别为{“11”，“10”，“100”，“1”，“101”}。
> 因此，集合比特数的乘积= (2 * 1 * 1 * 1 * 2) = 4。
> 
> **输入:** arr[] = {10，11，12 }
> T3】输出: 12

**方法:**给定的问题可以通过[计算每个数组元素的二进制表示](https://www.geeksforgeeks.org/count-total-bits-number/)中的总位数来解决。按照以下步骤解决问题:

*   初始化一个变量，比如**产品**，来存储结果产品。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   [计算一个整数的设定位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)**arr【I】**并将其存储在一个变量中，比如**位**。
    *   将**产品**的值更新为**产品*位**。
*   完成上述步骤后，打印**产品**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the
// set bits in an integer
int countbits(int n)
{
    // Stores the count of set bits
    int count = 0;

    // Iterate while N is not equal to 0
    while (n != 0) {

        // Increment count by 1
        if (n & 1)
            count++;

        // Divide N by 2
        n = n / 2;
    }

    // Return the total count obtained
    return count;
}

// Function to find the product
// of count of set bits present
// in each element of an array
int BitProduct(int arr[], int N)
{
    // Stores the resultant product
    int product = 1;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Stores the count
        // of set bits of arr[i]
        int bits = countbits(arr[i]);

        // Update the product
        product *= bits;
    }

    // Return the resultant product
    return product;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 4, 1, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << BitProduct(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to count the
    // set bits in an integer
    static int countbits(int n)
    {
        // Stores the count of set bits
        int count = 0;

        // Iterate while N is not equal to 0
        while (n != 0) {

            // Increment count by 1
            if ((n & 1) != 0)
                count++;

            // Divide N by 2
            n = n / 2;
        }

        // Return the total count obtained
        return count;
    }

    // Function to find the product
    // of count of set bits present
    // in each element of an array
    static int BitProduct(int arr[], int N)
    {

        // Stores the resultant product
        int product = 1;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Stores the count
            // of set bits of arr[i]
            int bits = countbits(arr[i]);

            // Update the product
            product *= bits;
        }

        // Return the resultant product
        return product;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 2, 4, 1, 5 };
        int N = arr.length;
        System.out.print(BitProduct(arr, N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the
# set bits in an integer
def countbits(n):

    # Stores the count of set bits
    count = 0

    # Iterate while N is not equal to 0
    while (n != 0):

        # Increment count by 1
        if (n & 1):
            count += 1

        # Divide N by 2
        n = n // 2

    # Return the total count obtained
    return count

# Function to find the product
# of count of set bits present
# in each element of an array
def BitProduct(arr, N):

    # Stores the resultant product
    product = 1

    # Traverse the array arr[]
    for i in range(N):

        # Stores the count
        # of set bits of arr[i]
        bits = countbits(arr[i])

        # Update the product
        product *= bits

    # Return the resultant product
    return product

# Driver Code
if __name__ == '__main__':
    arr = [3, 2, 4, 1, 5]
    N = len(arr)
    print(BitProduct(arr, N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to count the
    // set bits in an integer
    static int countbits(int n)
    {
        // Stores the count of set bits
        int count = 0;

        // Iterate while N is not equal to 0
        while (n != 0) {

            // Increment count by 1
            if ((n & 1) != 0)
                count++;

            // Divide N by 2
            n = n / 2;
        }

        // Return the total count obtained
        return count;
    }

    // Function to find the product
    // of count of set bits present
    // in each element of an array
    static int BitProduct(int[] arr, int N)
    {

        // Stores the resultant product
        int product = 1;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Stores the count
            // of set bits of arr[i]
            int bits = countbits(arr[i]);

            // Update the product
            product *= bits;
        }

        // Return the resultant product
        return product;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 3, 2, 4, 1, 5 };
        int N = arr.Length;
        Console.Write(BitProduct(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the
// set bits in an integer
function countbits( n)
{
    // Stores the count of set bits
    let count = 0;

    // Iterate while N is not equal to 0
    while (n != 0) {

        // Increment count by 1
        if ((n & 1) != 0)
            count++;

        // Divide N by 2
        n = Math.floor(n / 2);
        }

    // Return the total count obtained
    return count;
}

// Function to find the product
// of count of set bits present
// in each element of an array
function BitProduct( arr, N)
{

    // Stores the resultant product
    let product = 1;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

        // Stores the count
        // of set bits of arr[i]
        let bits = countbits(arr[i]);

        // Update the product
        product *= bits;
    }

    // Return the resultant product
    return product;
}

// Driver Code

let arr = [ 3, 2, 4, 1, 5 ];
let N = arr.length;
document.write(BitProduct(arr, N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log M)，M 是* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*